

[[xaml-xamlToMaui-kbase]]


[[xaml-xamlToMaui-kbase]]
## Imports

```csharp
using Xamarin.Essentials;
using Xamarin.Forms;
using Xamarin.Forms.Xaml;

// Changed to:
using Microsoft.Maui.Essentials;
using Microsoft.Maui.Controls;
using Microsoft.Maui.Controls.Xaml;

```

1.  **Updated C# Using Statements**

    *   Changed `using Xamarin.Forms;` → `using Microsoft.Maui.Controls;`
    *   Changed `using Xamarin.Essentials;` → `using Microsoft.Maui.Essentials;`
    *   Changed `using Xamarin.Forms.Xaml;` → `using Microsoft.Maui.Controls.Xaml;`
    *   Updated `Device.BeginInvokeOnMainThread` → `MainThread.BeginInvokeOnMainThread`

    **Original (Xamarin):**
    ```csharp
    using Xamarin.Essentials;
    using Xamarin.Forms;
    using Xamarin.Forms.Xaml;
    ```

    **New (MAUI):**
    ```csharp
    using Microsoft.Maui.Essentials;
    using Microsoft.Maui.Controls;
    using Microsoft.Maui.Controls.Xaml;
    ```



2. Updated xaml Usign statement 

# MainPage.xaml


<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ResillentConstruction.MainPage"
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core" xmlns:resillentconstruction="clr-namespace:ResillentConstruction"
             ios:Page.UseSafeArea="true">


<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ResillentConstruction.MainPage"
             xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls" xmlns:resillentconstruction="clr-namespace:ResillentConstruction"
             ios:Page.UseSafeArea="true">




# misc 

xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls"



# Folder copy all 

* androidfolder/Resources/drawable/ --> mainfolder/Resources/Images 
* androidfolder/Assets --> mainfolder/Resources/Raw
* other folder files 1 to 1 
* Images namding no upper



# csproj 

```
    <ItemGroup>
        <PackageReference Include="Microsoft.Maui.Controls" Version="$(MauiVersion)" />
        <PackageReference Include="Microsoft.Maui.Controls.Compatibility" Version="$(MauiVersion)" />
        <PackageReference Include="Microsoft.Maui.Essentials" Version="$(MauiVersion)" />
        <PackageReference Include="Microsoft.Extensions.Logging.Debug" Version="8.0.1" />
        <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />
        <PackageReference Include="sqlite-net-pcl" Version="1.8.116" />
    </ItemGroup>
```


---

# Folder Copy All

*   `asset` --> `raw`
*   `drawable` --> `images` * no img in uppercase name*
*   Other folder files: 1 to 1

---

# Files

## Xam
*(No specific files listed for Xamarin in the original input)*

## Maui
*   `App.xaml`
*   `*` (Implies all other files, needs clarification if specific files are intended)

# prj specefic 

* CERS 
