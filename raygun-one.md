Add Raygun exception reporting to all catch blocks in

Find all files in the app startup flow before LoginPage loads
Find all statmenets/blocks/functions in the app startup flow before LoginPage loads


using Raygun4Maui;

throw new Exception("mgogo");

// Send custom info to Raygun before UI initialization
RaygunClient.Current.SendInformation("App Constructor Started", new { 
    Timestamp = DateTime.Now,
    Platform = DeviceInfo.Platform.ToString(),
    Version = AppInfo.VersionString
});

i want to send crash info error info not custom info to able to find cause of errors   in this case the cause is throw new Exception("mgogo");

RaygunMauiClient.Current.Send(new Exception("App Constructor Started"), new List<string> { "AppConstructor", "Startup" });

RaygunMauiClient.Current.SendInBackground(new Exception("App Constructor Started"), new List<string> { "AppConstructor", "Startup" });



The Send method expects:

First parameter: Exception object
Second parameter: IList<string> for tags


1
Add manual Raygun crash reporting using RaygunMauiClient.Current.SendInBackground

RaygunMauiClient.Current.SendInBackground(ex, new List<string> ...

hdhdq@apkn.tech  Rarth123!


using Raygun4Maui;
try
{
    throw new Exception("Test crash for Raygun");
}
catch (Exception ex)
{
    // Manual Raygun reporting
    RaygunMauiClient.Current.SendInBackground(ex, new List<string> { "test-crash", "app-constructor" });
    throw; // Re-throw to still crash the app
}

