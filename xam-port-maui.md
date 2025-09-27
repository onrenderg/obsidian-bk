[[x10]]

 error dialogs to the user, let me output the errors to the debug console/output screen
# Poup err handling 
Ah, I understand! You're asking about the code that shows error messages as popups in the app UI. Here are the places where I added popup error handling:

## 🔍 **Error Popup Code I Added**

### **1. In PostLoginDashboardPage.xaml.cs (Navigation Error Handling):**
```csharp
MainThread.BeginInvokeOnMainThread(() =>
{
    try
    {
        // Use mainWindow.Page instead of Navigation.PushAsync for FlyoutPage
        mainWindow.Page = new NewUserRegistrationMasterPage(1);
    }
    catch (Exception ex)
    {
        DisplayAlert("Navigation Error", $"Failed to navigate: {ex.Message}", "OK");  // ← THIS POPUP
    }
});
```

### **2. Also in PostLoginDashboardPage.xaml.cs (Window Check Error):**
```csharp
else
{
    await DisplayAlert("Error", "Could not find main window", "OK");  // ← THIS POPUP
}
```

### **3. In NewUserRegistrationMasterPage.xaml.cs (Page Loading Error):**
```csharp
catch (Exception ex)
{
    // Fallback to a simple page if PersonalDetailsPage fails
    Detail = new NavigationPage(new ContentPage 
    { 
        Title = "Error",
        Content = new Label 
        { 
            Text = $"Error loading page: {ex.Message}",  // ← THIS SHOWS ON PAGE (not popup)
            HorizontalOptions = LayoutOptions.Center,
            VerticalOptions = LayoutOptions.Center
        }
    });
}
```

## 📱 **The Popup UI Code:**

The `DisplayAlert()` method is what creates the popup dialogs you're seeing. It's a built-in MAUI method that shows:
- **Title** (like "Navigation Error")
- **Message** (the actual error details)
- **Button** (like "OK")

**So when you see error popups, they're coming from the `DisplayAlert()` calls I added to help debug what's going wrong with the navigation.**

Is this what you were asking about? Or do you want me to remove these error popups?
## ## Logcat  crash etc log 


adb -s R9ZY40RDV0K logcat -c
adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at "
adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at "

dotnet build -f net8.0-android -t:Install
dotnet build -f net8.0-android -c Release  -t:Install


adb -s R9ZY40RDV0K logcat *:S AndroidRuntime:E ActivityManager:E


adb -s R9ZY40RDV0K shell pm list packages | findstr -i nicvc


dotnet build -f net8.0-android -c Debug -t:Install


dotnet build -f net8.0-android -c Debug -t:Uninstall;Install -p:AdbInstallExtraArgs="--user 0"

dotnet build -f net8.0-android -c Debug -t:Install -p:AdbInstallExtraArgs="--user 0"

adb -s R9ZY40RDV0K install --user 0 .apk

adb -s R9ZY40RDV0K shell pm list packages --user 150 | findstr -i nicvc



adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at "
adb -s R9ZY40RDV0K logcat | findstr -i "AndroidRuntime.*at "

dotnet build -f net8.0-android -t:Install
dotnet build -f net8.0-android -c Release  -t:Install

# ## Wanring only ouput 

* **dotnet build --nologo -v q --property WarningLevel=0 /clp:ErrorsOnly**
		dotnet build --nologo -v q --property WarningLevel=0 /clp:ErrorsOnly
- `--nologo` suppresses the header
- `-v q` sets output verbosity to quiet
- `--property WarningLevel=0` is for MsBuild, and described well in other answers.
- `/clp:ErrorsOnly` means **C**onsole**L**ogger**P**arameters

# Try with specific device ID
dotnet run -f net8.0-android --device R9ZY40RDV0K
adb -s R9ZY40RDV0K logcat | findstr -i "nicvc\|crash\|exception"



#####################
adb -s R9ZY40RDV0K logcat *:E


# ## **Check APK Manifest**
adb -s R9ZY40RDV0K shell pm dump com.companyname.nicvc | findstr -i "activity\|intent"
adb -s R9ZY40RDV0K shell am start -D -n 
com.companyname.nicvc/crc64a73e961ec6240ec4.MainActivity

----------------------------------------------------
dotnet build -f net8.0-android -c Release

Stack Trace : 
# Get exception message + stack trace + some context
adb -s R9ZY40RDV0K logcat | findstr -B 2 -A 15 "FATAL EXCEPTION\|AndroidRuntime.*Exception"

# Clean and rebuild
dotnet clean
dotnet build -f net8.0-android -c Debug

# Install the fixed version
dotnet build -f net8.0-android -c Debug -t:Install

# Test launch with monitoring
adb -s R9ZY40RDV0K logcat -c
adb -s R9ZY40RDV0K logcat *:E &
adb -s R9ZY40RDV0K shell am start -n com.companyname.nicvc/crc64a73e961ec6240ec4.MainActivity



# Setup 
* adb https://developer.android.com/tools/releases/platform-tools


✅ **Project Structure**: Converted from Xamarin to MAUI project format  
✅ **Package References**: Added SQLite, Newtonsoft.Json, MAUI Essentials  
✅ **XAML Namespaces**: Updated from Xamarin.Forms to MAUI namespaces  
✅ **XAML Syntax**: Fixed broken XML syntax in namespace declarations  
✅ **C# Using Statements**: Replaced Xamarin.Forms with MAUI equivalents  
✅ **Global Usings**: Set up proper global using statements



## Approach of port 

 a Xamarin.Forms concept that doesn't exist in MAUI. 
handle concpet not in maui 

[[xaml-xamlToMaui-kbase]]


[[xaml-xamlToMaui-kbase]]


[[sep-5-mauiport]]
# Copy part 


* dotnet clean && dotnet build
# workload  install part if any 


##    global.json file.

* dotnet --list-sdks

* dotnet --version
# Install MAUI workload for .NET 8  

* dotnet workload install maui

### **Step : Clean and Rebuild**

After installing MAUI workload:

1. Close Visual Studio
2. Delete bin and obj folders from your project
3. Reopen Visual Studio
4. Clean Solution (`Build` → `Clean Solution`)
5. Rebuild Solution (`Build` → `Rebuild Solution`)


# Use globalusing  file

# Build

## Wanring only ouput 

* **dotnet build --nologo -v q --property WarningLevel=0 /clp:ErrorsOnly**
		dotnet build --nologo -v q --property WarningLevel=0 /clp:ErrorsOnly
- `--nologo` suppresses the header
- `-v q` sets output verbosity to quiet
- `--property WarningLevel=0` is for MsBuild, and described well in other answers.
- `/clp:ErrorsOnly` means **C**onsole**L**ogger**P**arameters

For reasons, I have not fully explored, `dotnet run` does not always


# Run 

dotnet build -f net8.0-android

dotnet run -f net8.0-android
dotnet run -f net9.0-android

### **Use a Global.json File**

If you want to ensure you're using a specific .NET 8 version, let's create a `global.json` file:

{  
"sdk": {  
"version": "8.0.0",  
"rollForward": "latestFeature"  
}  
}




# If you get errors, try updating workloads first  
dotnet workload update


## vscode 

skey = shift + alt+ f & replace all  in dropdown 




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

```html
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

```

* Updated XAML Using Statements

#### * MainPage.xaml

**Original:**

```xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ResillentConstruction.MainPage"
             xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core" xmlns:resillentconstruction="clr-namespace:ResillentConstruction"
             ios:Page.UseSafeArea="true">
```

**To:**

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="ResillentConstruction.MainPage"
             xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls" xmlns:resillentconstruction="clr-namespace:ResillentConstruction"
             ios:Page.UseSafeArea="true">
```


http://xamarin.com/schemas/2014/forms
http://schemas.microsoft.com/dotnet/2021/maui

```txt

<!-- ✅  -->
"http://xamarin.com/schemas/2014/forms"
"http://schemas.microsoft.com/dotnet/2021/maui"





<!-- ✅  -->
FROM: 
xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
TO:   
xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls"




<!-- ✅  -->
using Microsoft.Maui.Controls.PlatformConfiguration;
using Microsoft.Maui.Controls.PlatformConfiguration.AndroidSpecific;

using Microsoft.Maui.Controls.PlatformConfiguration;
using Microsoft.Maui.Controls.PlatformConfiguration.AndroidSpecific;
```







*   `xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"`
    *   **To:** `xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls"`



# misc 

```xml

xmlns:ios="clr-namespace:Xamarin.Forms.PlatformConfiguration.iOSSpecific;assembly=Xamarin.Forms.Core"
xmlns:ios="clr-namespace:Microsoft.Maui.Controls.PlatformConfiguration.iOSSpecific;assembly=Microsoft.Maui.Controls"
```





# Folder copy all 

* androidfolder/Resources/drawable/ --> mainfolder/Resources/Images 
* androidfolder/Assets --> mainfolder/Resources/Raw
* other folder files 1 to 1 
* Images namding no upper



# xaml fiel
xmlns="http://xamarin.com/schemas/2014/forms"
- Replace: `xmlns="http://schemas.microsoft.com/dotnet/2021/maui"`
xmlns:d="http://xamarin.com/schemas/2014/forms/design"
- Replace: _(delete the entire line)_

`mc:Ignorable="d"`
- Replace: _(delete the entire line)_


# csproj 


```html
<ItemGroup>  
<PackageReference Include="Microsoft.Maui.Controls" Version="$(MauiVersion)" />  
<PackageReference Include="Microsoft.Maui.Controls.Compatibility" Version="$(MauiVersion)" />  
<PackageReference Include="Microsoft.Extensions.Logging.Debug" Version="8.0.1" />  
<PackageReference Include="Newtonsoft.Json" Version="13.0.3" />  
<PackageReference Include="sqlite-net-pcl" Version="1.9.172" />  
<PackageReference Include="SQLitePCLRaw.bundle_green" Version="2.1.8" />  
</ItemGroup>
```


dotnet restore   && dotnet build




```html
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
