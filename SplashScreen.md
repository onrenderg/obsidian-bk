**Xamarin vs MAUI Splash Screen Differences:**

In your **Xamarin version**, the splash screen was handled through Android's native theme system:

- The MainActivity uses `Theme = "@style/MainTheme"`
- Android automatically shows the app icon during the theme-based splash screen
- The icon was displayed as part of the native Android launch sequence

In your **MAUI version**, the splash screen works differently:

- MAUI uses a custom splash screen system with `MauiSplashScreen`
- The issue is that you're trying to use a PNG file (ic_launcher_appicon.png) but MAUI splash screens work best with SVG files
- PNG files might not render properly or at all in MAUI splash screens

I see the issue! In MAUI, the Android splash screen is controlled by the `Maui.SplashTheme` but there's no 

styles.xml file in your Android platform folder to customize it. The .NET logo is showing because MAUI's default splash screen theme is being used.

Let me create the missing 

styles.xml file to properly configure the splash screen: