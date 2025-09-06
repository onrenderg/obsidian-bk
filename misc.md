# Flow MAUI App

*   `MauiProgram.cs` Configuration related statements
*   `App.xaml.cs` constructor runs next - this is where the navigation logic is determined

    ```csharp
    MainPage = new NavigationPage(new MainPage());
    ```

    1.  `MainPage =`
        *   This is assigning a value to the `MainPage` property of the `App` class.
        *   `MainPage` is a property that determines what page the app shows first.

    2.  `new NavigationPage(...)`
        *   Creates a new object of type `NavigationPage`.
        *   `NavigationPage` is a MAUI container that provides navigation features (back button, navigation stack, etc.).

    3.  `new MainPage()`
        *   Creates a new object of the `MainPage` class (your content page).
        *   This is passed as a parameter to the `NavigationPage` constructor.
        *   Yes, this creates a new instance/object of your `MainPage` class.

# Raygun Setup
https://app.raygun.com/onboarding/setup-raygun/2cvw8d5

This is an Android SDK version compatibility issue with the Raygun library. The error shows that your project's minimum SDK version (21) is lower than what the Raygun network monitor library requires (24).

Let me check your project file and fix this:

# Raygun only supports min Android API level 24

# Project file
```xml
		<SupportedOSPlatformVersion Condition="$([MSBuild]::GetTargetPlatformIdentifier('$(TargetFramework)')) == 'android'">24.0</SupportedOSPlatformVersion>
```

# Debugging

## Hotkeys
*   `alt + ctrl + o` = debug window
*   `f11, f10, f5` (step into, step over, continue)
*   Debug > Windows > Call Stack (`Ctrl + Alt + C`)





**             InitializeComponent(); will carsh if issue with xaml file   in inlizer of constuctor of  respected csf **
If you want to ensure the MainPage is fully loaded before continuing, you can move the database initialization to the MainPage's OnAppearing() method or use an event-based approach.


# Cers flow 

* database initialization 
* login page navigated if user ?


now look into @CERS  till login form is navigated by app.xaml.cs what is happenign in flow 