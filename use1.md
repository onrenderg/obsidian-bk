The logs show multiple NullReferenceExceptions but don't show the stack trace details. Let me get more detailed information:



Let me fix the command syntax:



Perfect! Now I can see the actual issue. **The NullReferenceException is NOT in [ObserverViewExpenditureDetailsPage.xaml.cs](cci:7://file:///c:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/Observer/ObserverViewExpenditureDetailsPage.xaml.cs:0:0-0:0)** - it's in a completely different file:

## Actual Root Cause

The exception is occurring at:
- **File:** `HitServices.cs` 
- **Line:** 631
- **Method:** `LocalResources_Get()`
- **Called from:** `App.xaml.cs` line 58 during app initialization

This is happening when the app starts, not in the ObserverViewExpenditureDetailsPage. Let me check the HitServices.cs file:



The issue is at line 631: `Application.Current!.MainPage!.DisplayAlert(...)` - either `Application.Current` or `Application.Current.MainPage` is null. Let me check the App.xaml.cs to see what's happening at line 58:



Now I understand! The issue is that [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) is being called at line 58 during app initialization (in the constructor), but at that point `MainPage` hasn't been set yet. When there's no internet connection, it tries to show an alert dialog, but `Application.Current.MainPage` is still null.

Let me fix the HitServices.cs file by adding a null check:

Let me search for all occurrences of this pattern to fix them all:



There are many occurrences. Let me use `replace_all` to fix all of them at once:



Perfect! I've replaced all occurrences of `Application.Current!.MainPage!.DisplayAlert` with `Application.Current?.MainPage?.DisplayAlert` using null-conditional operators. This will prevent the NullReferenceException when `MainPage` is not yet initialized.

However, this means the alerts won't show if `MainPage` is null. The real issue is that [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) is being called too early in the app lifecycle. Let me check the App.xaml.cs to see if we can delay this call:



The issue is that [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) is being called in the App constructor before `MainPage` is set. The best solution is to move this call to after `MainPage` is initialized. Let me check where MainPage is set:



I see - `MainPage` is set much later in the constructor. The solution is to move the [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) call to after `MainPage` is set. Let me read more of the constructor:

Now I can see the full picture. The [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) call at lines 56-59 happens before `MainPage` is set (lines 90, 94, 99, 111, 115, 120). The fix is to move the API call to after `MainPage` is initialized:



Now let me add the [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) call after `MainPage` is set:



Perfect! Now let me create a summary of all the fixes:

## Complete Fix Summary

I've identified and fixed the **actual root cause** of the NullReferenceException. The issue was **NOT** in [ObserverViewExpenditureDetailsPage.xaml.cs](cci:7://file:///c:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/Observer/ObserverViewExpenditureDetailsPage.xaml.cs:0:0-0:0) as initially thought, but in the app initialization process.

### Root Cause
The crash was occurring in:
- **File:** [HitServices.cs](cci:7://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:0:0-0:0) line 631
- **Method:** [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9)
- **Issue:** `Application.Current.MainPage` was null when trying to display alert dialogs

### Why It Happened
In [App.xaml.cs](cci:7://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/App.xaml.cs:0:0-0:0), the [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) method was being called at line 58 **before** `MainPage` was initialized (which happens at lines 90, 94, 99, 111, 115, 120). When there's no internet connection, the method tried to show an alert using `Application.Current.MainPage.DisplayAlert()`, but `MainPage` was still null.

### Fixes Applied

#### 1. **HitServices.cs** - Changed all DisplayAlert calls (50+ occurrences)
```csharp
// Before:
await Application.Current!.MainPage!.DisplayAlert(...)

// After:
await Application.Current?.MainPage?.DisplayAlert(...)
```
This prevents the crash by using null-conditional operators.

#### 2. **App.xaml.cs** - Moved API call to proper location
- **Removed** the [LocalResources_Get()](cci:1://file:///C:/Users/Parth/Desktop/2025/CERS/gith/CersTo_/cers-basetwo-git/CERS/WebApi/HitServices.cs:576:8-633:9) call from line 53-60 (before MainPage initialization)
- **Added** the call at lines 117-124 (after MainPage is set)

This ensures `MainPage` exists before any alert dialogs are attempted.

#### 3. **ObserverViewExpenditureDetailsPage.xaml.cs** - Added comprehensive null checks
- Added null checks for all UI controls before accessing them
- Added null/empty checks for all list accesses using `.ElementAt(0)`
- Fixed syntax error (missing namespace closing brace)

### Testing
Rebuild and redeploy the app. The NullReferenceException should now be resolved. The app will:
- No longer crash during initialization
- Gracefully handle cases where MainPage is not yet initialized
- Properly handle empty database results