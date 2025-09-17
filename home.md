
[[Haks]]



https://obsidian-base-deploy.vercel.app/



[[CERS-basetwo-git-]]

[[sep-5-mauiport]]
[[maui-app]]
[[xam-port-maui]]
remove all stacklayout with grid

## Maui app have xaml xml files having controls like :
## **Controls (UI Elements)**

- **`Image`** - Displays pictures/graphics
- **`Label`** - Shows text content
- **`Button`** - Interactive clickable element
## & 
## **Containers (Layout Elements)**

- **`ContentPage`** - Root page container
- **`ScrollView`** - Enables scrolling for overflow content
- **`VerticalStackLayout`** - Arranges children vertically

# Purpose and Behaviour of Containers 

[[det_8973]]

# Key points  Mwcb= minworkcodeblock

```xml
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="CERS.MainPage">
</ContentPage>
```
- **`<ContentPage>`**: Root container representing a single page/screen
- **`xmlns="...maui"`**: Default namespace for MAUI controls (Image, Label, Button)
- **`xmlns:x="...xaml"`**: XAML namespace for XAML-specific features (x:Name, x:Class)
- **`x:Class="CERS.MainPage"`**: Links this XAML to the MainPage.xaml.cs code-behind class



## **Additional Common Controls & Containers**

### **More Controls:**

- `Entry` - Text input field
- `Picker` - Dropdown selection
- `Switch` - Toggle on/off
- `Slider` - Range selector
- `DatePicker` - Date selection

### **More Containers:**

- `HorizontalStackLayout` - Arranges children horizontally
- `Grid` - Flexible rows/columns layout
- `StackLayout` - General stacking (vertical/horizontal)
- `Frame` - Container with border/shadow
- `Border` - Decorative container with styling

## **Pattern:**


```xml

<Container>  
    <Control Property="Value" />  
    <AnotherContainer>  
        <Control />  
    </AnotherContainer>  
</Container>
```

Your understanding is spot-on - MAUI uses this hierarchical structure where **containers** hold and arrange **controls** to build the UI layout.



# CS file  Purpose  line by line 

## App sepecefic 

* InitializeComponent(); Start of UI lifecycle
* Preferences.Set(...) App secrets, encryption, BasicAuth
* languageMasterDatabase.GetLanguageMaster(...) Check if local resources need loading
* savePreferenceDatabase.GetSavePreference(...) Load user preferences
* GetLabelByKey(...) Load labels using language preference
* if (Preferences.Get("UserType", "")...) Determine app navigation
* MainPage = new NavigationPage(...) Final app page load
* q
## 🛠️ Tips for Better Debugging:

- Use **F11** instead of F10 to **step into** methods like `GetLabelByKey`, `LocalResources_Get`, etc.
    
- Watch `Preferences.Get(...)` values in your locals/watch window.
    
- Use conditional breakpoints if you want to break only when a specific `UserType` or language is used.
- `F10` will **skip** the internal logic and just execute the line.
    
- `F11` will **go inside** the `GetLabelByKey` method and let you see how it works — e.g., how it searches through `MyLanguage`.


## Agentic debug

- 1. Open the Copilot Chat window.
        
    2. Switch the mode dropdown from "Ask" to **Agent**.
        
    3. Enter your prompt and Copilot begins planning, editing, running tests, and iterating.[Microsoft Learn](https://learn.microsoft.com/visualstudio/ide/copilot-agent-mode?utm_source=chatgpt.com)




## xam-to-maui: cers


* There are still several database classes using the deprecated `DependencyService.Get<ISQLite>()` which could be causing crashes. Let me fix these remaining database classes:

* app is crashing at the `Preferences.Set` calls in the App constructor. This is likely because the `AESCryptography.EncryptAES` method is failing or the `HttpUtility.UrlEncode` is having issues. Let me check and fix this:

* stacktrace info to agent 


```cs

# App.xaml.cs
public static string? DB_Name = "CERS.db";


# In all other places in place of old xamrian dbPath statment 
var dbPath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData), ResillentConstruction.App.DB_Name);
```
# Skey 

* shift+ ecs
* ctrl+ alt o

```cs




catch (Exception ex) 
{

	System.Diagnostics.Debug.WriteLine($"MGOGO:  {ex.Message}")
	throw new Exception("mgogo");
}



	using Raygun4Maui;


catch (Exception ex) 
{
	System.Diagnostics.Debug.WriteLine($"LocalResources error: {ex.Message}");
	RaygunMauiClient.Current?.SendInBackground(ex);
	
//	throw new Exception("mgogo");
}




try

{

	throw new Exception("mgogo");
}

catch (Exception ex)

{

	System.Diagnostics.Debug.WriteLine($"LocalResources error: {ex.Message}");

	RaygunMauiClient.Current?.SendInBackground(ex);

//  throw new Exception("mgogo");

}

            
//Console.WriteLine("mgogo");
//Console.WriteLine($"Error in getRijndaelManaged: {ex.Message}");

```


# Windsurf opt : 
* Auto-continued response




# Raygun



You're correct! The Raygun crash reporting is configured in MauiProgram.cs, but you need to actually use Raygun's logging methods to send custom information. Let me add Raygun logging to your App.xaml.cs:

**You can add more Raygun logging throughout your app:**

- `RaygunClient.Current.Send(exception)` - Send any caught exceptions
- `RaygunClient.Current.SendInformation(message, customData)` - Send custom events
- `RaygunClient.Current.RecordBreadcrumb(message)` - Track user actions leading to crashes


# MauiProgram.cs


```cs
using Microsoft.Extensions.Logging;

using Raygun4Maui;

  

namespace CERS

{

    public static class MauiProgram

    {

        public static MauiApp CreateMauiApp()

        {

            var builder = MauiApp.CreateBuilder();

            builder

                .UseMauiApp<App>()

                .ConfigureFonts(fonts =>

                {

                    fonts.AddFont("OpenSans-Regular.ttf", "OpenSansRegular");

                    fonts.AddFont("OpenSans-Semibold.ttf", "OpenSansSemibold");

                });

  

            builder.AddRaygun(options =>

            {

                options.RaygunSettings.ApiKey = "1LQOobUQR69pOjRj2FQ0g";

                options.RaygunSettings.CatchUnhandledExceptions = true;

            });

  
  

#if DEBUG

            builder.Logging.AddDebug();

#endif

  

            return builder.Build();

        }

    }

}
```


##  .proj

```xml
<Project Sdk="Microsoft.NET.Sdk">

  

    <PropertyGroup>

        <TargetFrameworks>net8.0-android;net8.0-ios;net8.0-maccatalyst</TargetFrameworks>

        <TargetFrameworks Condition="$([MSBuild]::IsOSPlatform('windows'))">$(TargetFrameworks);net8.0-windows10.0.19041.0</TargetFrameworks>

        <!-- Uncomment to also build the tizen app. You will need to install tizen by following this: https://github.com/Samsung/Tizen.NET -->

        <!-- <TargetFrameworks>$(TargetFrameworks);net8.0-tizen</TargetFrameworks> -->

  

        <!-- Note for MacCatalyst:

        The default runtime is maccatalyst-x64, except in Release config, in which case the default is maccatalyst-x64;maccatalyst-arm64.

        When specifying both architectures, use the plural <RuntimeIdentifiers> instead of the singular <RuntimeIdentifier>.

        The Mac App Store will NOT accept apps with ONLY maccatalyst-arm64 indicated;

        either BOTH runtimes must be indicated or ONLY macatalyst-x64. -->

        <!-- For example: <RuntimeIdentifiers>maccatalyst-x64;maccatalyst-arm64</RuntimeIdentifiers> -->

  

        <OutputType>Exe</OutputType>

        <RootNamespace>CERS</RootNamespace>

        <UseMaui>true</UseMaui>

        <SingleProject>true</SingleProject>

        <ImplicitUsings>enable</ImplicitUsings>

        <Nullable>enable</Nullable>

  

        <!-- Display name -->

        <ApplicationTitle>CERS</ApplicationTitle>

  

        <!-- App Identifier -->

        <ApplicationId>com.companyname.cers</ApplicationId>

  

        <!-- Versions -->

        <ApplicationDisplayVersion>1.0</ApplicationDisplayVersion>

        <ApplicationVersion>1</ApplicationVersion>

  

        <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'ios'">11.0</SupportedOSPlatformVersion>

        <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'maccatalyst'">13.1</SupportedOSPlatformVersion>

        <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'">24.0</SupportedOSPlatformVersion>

        <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'windows'">10.0.17763.0</SupportedOSPlatformVersion>

        <TargetPlatformMinVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'windows'">10.0.17763.0</TargetPlatformMinVersion>

        <SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'tizen'">6.5</SupportedOSPlatformVersion>

    </PropertyGroup>

  

    <ItemGroup>

        <!-- App Icon -->

        <MauiIcon Include="Resources\AppIcon\appicon.svg" ForegroundFile="Resources\AppIcon\appiconfg.svg" Color="#512BD4" />

  

        <!-- Splash Screen -->

        <MauiSplashScreen Include="Resources\Splash\splash.svg" Color="#512BD4" BaseSize="128,128" />

  

        <!-- Images -->

        <MauiImage Include="Resources\Images\*" />

        <MauiImage Update="Resources\Images\dotnet_bot.png" Resize="True" BaseSize="300,185" />

  

        <!-- Custom Fonts -->

        <MauiFont Include="Resources\Fonts\*" />

  

        <!-- Raw Assets (also remove the "Resources\Raw" prefix) -->

        <MauiAsset Include="Resources\Raw\**" LogicalName="%(RecursiveDir)%(Filename)%(Extension)" />

    </ItemGroup>

  

    <ItemGroup>

        <PackageReference Include="Microsoft.Maui.Controls" Version="8.0.91" />

        <PackageReference Include="Microsoft.Maui.Controls.Compatibility" Version="8.0.91" />

        <PackageReference Include="Microsoft.Maui.Essentials" Version="8.0.91" />

        <PackageReference Include="Microsoft.Extensions.Logging.Debug" Version="8.0.1" />

        <PackageReference Include="Newtonsoft.Json" Version="13.0.3" />

        <PackageReference Include="Raygun4Maui" Version="2.3.0" />

        <PackageReference Include="sqlite-net-pcl" Version="1.8.116" />

        <PackageReference Include="SQLitePCLRaw.bundle_green" Version="2.1.6" />

    </ItemGroup>

  

</Project>
```



```cs


public static string? DB_Name = "CERS.db";

var databasePath = Path.Combine(Environment.GetFolderPath(Environment.SpecialFolder.LocalApplicationData), CERS.App.DB_Name);


```


[[raygun-one]]
