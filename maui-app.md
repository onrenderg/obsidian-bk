

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

[[rescourse-folder]]
* location :   
	* Resources/Styles/Styles.xaml
	* Resources/Styles/Styles.xaml


! Everything defined in App.xaml applies **globally** throughout your entire MAUI application.


! Everything defined in `App.xaml` applies globally throughout your entire MAUI application.

---

🌍 **Global Scope of App.xaml**
`App.xaml` is the application-level resource dictionary - it's like the "master stylesheet" for your entire app.

**What Gets Applied Globally:**

1.  **Colors:**
    ```xml
    <Color x:Key="Primary">#512BD4</Color>
    ```
    *Available in every page as `{StaticResource Primary}`*

2.  **Styles:**
    ```xml
    <Style x:Key="ButtonStyle" TargetType="Button">
        <Setter Property="BackgroundColor" Value="Blue" />
    </Style>
    ```
    *Can be used on any page as `Style="{StaticResource ButtonStyle}"`*

3.  **Default Styles (without `x:Key`):**
    ```xml
    <Style TargetType="Button">
        <Setter Property="BackgroundColor" Value="Red" />
    </Style>
    ```
    *Automatically applied to ALL buttons in your entire app*

---

📄 **Page-Level Resources**
You can also define resources at the page level:

```xml
<ContentPage.Resources>
    <Color x:Key="PageSpecificColor">Green</Color>
</ContentPage.Resources>
```
*Only available within that specific page*

---

🔄 **Resource Hierarchy**
1.  `App.xaml` (Global - highest priority)
2.  `Page.Resources` (Page-specific)
3.  `Control.Resources` (Control-specific)

---

💡 **Why This is Powerful**
*   **Consistency:** One place to define your app's theme
*   **Maintainability:** Change a color once, updates everywhere
*   **Reusability:** Define once, use anywhere

---

So yes, your `App.xaml` is your global design system that affects every page, control, and element in your MAUI app!


	This app was missing the `MergedDictionaries` section that tells MAUI to load the standard resource files.

---

**What Was Missing**
Your original `App.xaml` had:

```xml
<Application.Resources>
    <Style x:Key="NavigationLabelColor" ...>
    <!-- Your custom styles -->
</Application.Resources>
```

**What Was Needed**
```xml
<Application.Resources>
    <ResourceDictionary>
        <ResourceDictionary.MergedDictionaries>
            <ResourceDictionary Source="Resources/Styles/Colors.xaml" />
            <ResourceDictionary Source="Resources/Styles/Styles.xaml" />
        </ResourceDictionary.MergedDictionaries>
        
        <!-- Your existing custom styles -->
    </ResourceDictionary>
</Application.Resources>
```

---

**Why This Matters**

**Without `MergedDictionaries`:**
*   Your app only had access to your custom styles
*   Standard MAUI styles like `Headline`, `SubHeadline` were not loaded
*   `MainPage` crashed when trying to use `{StaticResource Headline}`

**With `MergedDictionaries`:**
*   Your app loads both standard MAUI resources AND your custom styles
*   All the colors from `Colors.xaml` (Primary, Gray100, etc.) are available
*   All the styles from `Styles.xaml` (Headline, SubHeadline, default Button styles) are available
*   Your custom styles still work as before

📁 **Location of Colors and Styles in MAUI**

Standard MAUI Resources (in `Resources` folder):

```
📁 CERS/
  📁 Resources/
    📁 Styles/
      📄 Colors.xaml     ← Standard MAUI colors
      📄 Styles.xaml     ← Standard MAUI styles
```


