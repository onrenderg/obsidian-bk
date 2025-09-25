## App startup and initialization (MAUI end-to-end)

### Boot sequence
- Android/iOS entrypoint boots the MAUI host and calls `MauiProgram.CreateMauiApp()`.
- `MauiProgram.CreateMauiApp()`:
  - Builds the DI container (`builder.Services`)
  - Registers fonts/handlers/lifecycle events
  - Returns `MauiApp`
- `App` (App.xaml.cs) is constructed
  - Set `MainPage` (e.g., `new NavigationPage(new DashboardPage())` or Shell)
  - App-level resources are loaded (App.xaml)
- First `Window` is created (multi-window on desktop)

### Where to put initialization
- `MauiProgram.CreateMauiApp()`: register services, configuration, handlers, fonts
- `App` constructor: global theme, main navigation root, global event wiring
- Platform lifecycle events (optional): `builder.ConfigureLifecycleEvents(...)`
- Per-page: do not fetch heavy data in constructor; prefer `OnAppearing`

## Page lifecycle (ContentPage)

- Constructor
  - `InitializeComponent()` wires XAML to fields; keep it fast
  - Set `BindingContext`, inject services (via ctor or `ServiceProvider`)
- `OnNavigatedTo` (Shell only) or navigation parameter handling
- `OnAppearing` (called each time page appears)
  - Safe place to load/refresh data
  - If awaiting, use `protected override async void OnAppearing()`
  - Use guards to avoid double loads
- `OnDisappearing`
  - Stop timers, cancel in-flight ops (via `CancellationTokenSource`), detach events
- Disposal
  - MAUI disposes handlers when page is popped; unsubscribe events you added manually

### Practical rules for your Edit page
- Keep constructor minimal; set only UI text, DI services, `ItemsSource` pointing to cached lists
- Load DB/network data in `OnAppearing` with try/catch
- Use a CTS to cancel loads if user navigates away
- Toggle overlays (`Loading_activity.IsVisible`) around awaited work
- Unsubscribe any event handlers you added in code-behind in `OnDisappearing`

## Navigation models

- NavigationPage
  - `await Navigation.PushAsync(new EditExpenditureDetailsPage(id));`
  - Back button pops; `OnAppearing` runs again when revisiting
- Shell
  - URI-based navigation and `OnNavigatedTo/From` for parameter binding

## Dependency Injection (DI)

- Register in `MauiProgram`:
  - `builder.Services.AddSingleton<HitServices>();`
  - `builder.Services.AddSingleton<PaymentModesDatabase>();`
  - `builder.Services.AddTransient<EditExpenditureDetailsPage>();`
- Resolve:
  - Constructor inject services: `public EditExpenditureDetailsPage(PaymentModesDatabase db, HitServices svc) { ... }`
  - Or `var svc = Application.Current.Services.GetRequiredService<HitServices>();`

## Threading and UI

- Only update UI on the UI thread
  - Inside `await` continuations you’re on UI thread by default
  - Use `MainThread.BeginInvokeOnMainThread(...)` when coming from background threads
- Use `IDispatcher` for timed work on UI thread
- Avoid long work on UI thread; offload to `Task.Run` and marshal back

## Permissions and platform specifics

- Request permissions with `Permissions.RequestAsync<TPermission>()`
- Android-specific setup lives in `Platforms/Android` (Manifest, activities)
- iOS-specific in `Platforms/iOS` (info.plist keys)

## Error handling patterns

- Use small try/catch blocks around awaited DB/network calls
- Surface user-friendly errors with `DisplayAlert`
- Log details to `Console.WriteLine` or a logging service

## State, preferences, and caching

- `Preferences.Get/Set` for small key-values (you already use `Preferences.Set("Active", ...)`)
- Cache lookups (e.g., payment modes) to avoid repeated queries in `OnAppearing`
- Use `ObservableCollection<T>` if the UI must react to list changes

## Applying this to EditExpenditureDetailsPage

- Constructor
  - `InitializeComponent();`
  - Set simple text, wire `ItemsSource` to cached list
  - Do not hit DB/network here
- `OnAppearing` (async)
  - Guard double calls if needed:
    - `if (_loaded) return; _loaded = true;`
  - Show `Loading_activity`
  - Fetch user details, set min dates
  - Load expenditure by `expenseid` with try/catch
  - Hide `Loading_activity`
- `OnDisappearing`
  - Cancel CTS, hide overlays, detach any temporary events
- Data load method
  - Accept `CancellationToken`
  - Validate empty result, avoid `ElementAt(0)` without checks
  - Set fields for both languages

Example skeleton you can adapt:

```csharp
private readonly PaymentModesDatabase _paymentModesDb;
private readonly ExpenditureDetailsDatabase _expenditureDb;
private readonly UserDetailsDatabase _userDb;
private readonly HitServices _service;

private bool _loadedOnce;
private CancellationTokenSource? _loadCts;

public EditExpenditureDetailsPage(
    PaymentModesDatabase paymentModesDb,
    ExpenditureDetailsDatabase expenditureDb,
    UserDetailsDatabase userDb,
    HitServices service,
    string expendid) // or set via property if using Shell nav
{
    InitializeComponent();
    _paymentModesDb = paymentModesDb;
    _expenditureDb = expenditureDb;
    _userDb = userDb;
    _service = service;
    expenseid = expendid;

    btn_uploadpdf.Text = App.GetLabelByKey("SelectFile");
    picker_payMode.ItemsSource = _paymentModesDb.GetPaymentModes("Select * from PaymentModes").ToList();
    picker_payMode.ItemDisplayBinding = new Binding(App.Language == 0 ? "paymode_Desc" : "paymode_Desc_Local");
}

protected override async void OnAppearing()
{
    base.OnAppearing();

    _loadCts?.Cancel();
    _loadCts = new CancellationTokenSource();
    var ct = _loadCts.Token;

    try
    {
        Loading_activity.IsVisible = true;

        var users = _userDb.GetUserDetails("Select * from UserDetails").ToList();
        if (users.Count == 0) return;

        var user = users[0];
        datepicker_expdate.MinimumDate = Convert.ToDateTime(user.NominationDate);
        datepicker_paymentdate.MinimumDate = Convert.ToDateTime(user.NominationDate);

        await LoadPreviousDataAsync(expenseid, ct);
    }
    catch (OperationCanceledException)
    {
        // ignore
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error in OnAppearing: {ex}");
        await DisplayAlert(App.GetLabelByKey("AppName"), App.GetLabelByKey("exchfl"), App.Btn_Close);
    }
    finally
    {
        Loading_activity.IsVisible = false;
    }
}

protected override void OnDisappearing()
{
    base.OnDisappearing();
    _loadCts?.Cancel();
}

private Task LoadPreviousDataAsync(string expendid, CancellationToken ct)
{
    return Task.Run(() =>
    {
        ct.ThrowIfCancellationRequested();
        var list = _expenditureDb.GetExpenditureDetails($"Select * from ExpenditureDetails where ExpenseID='{expendid}'").ToList();
        if (list.Count == 0) return;

        var item = list[0];

        MainThread.BeginInvokeOnMainThread(() =>
        {
            Entry_expdate.Text = item.expDateDisplay;
            expendituredateselected = item.expDate.Replace('-', '/');

            editor_exptype.Text = (App.Language == 0) ? item.ExpTypeName : item.ExpTypeNameLocal;
            expendituresourcecode = item.expCode;

            entry_amount.Text = item.amount;
            entry_amountoutstanding.Text = item.amountoutstanding;
            Entry_paymentdate.Text = item.paymentDateDisplay;
            paymentdateselected = item.paymentDate.Replace('-', '/');

            entry_voucherBillNumber.Text = item.voucherBillNumber;

            var idx = (_paymentModesDb.GetPaymentModes("Select * from PaymentModes").ToList())
                .FindIndex(p => p.paymode_code == item.payMode);
            picker_payMode.SelectedIndex = Math.Max(0, idx);

            entry_payeeName.Text = item.payeeName;
            entry_payeeAddress.Text = item.payeeAddress;
            entry_sourceMoney.Text = item.sourceMoney;
            entry_remarks.Text = item.remarks;
            imgbtn_viewpdf.IsVisible = item.evidenceFile == "Y";
        });
    }, ct);
}
```

Key takeaways:
- Keep constructors light; use `OnAppearing` for data loads.
- Use DI for your services and databases.
- Guard for cancellation and exceptions.
- Use overlays for UX and keep the UI thread clean.