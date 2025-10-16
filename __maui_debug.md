## Using logcat & Console.WriteLine


```cmd
adb kill-server
adb start-server
adb devices

adb -s R9ZY40RDV0K logcat -d | Select-String "Loaded.*items|Observer data|DEBUG:" | Select-Object -Last 20

# View logs in real-time  
adb -s R9ZY40RDV0K logcat | findstr "NICVC"

# Monitor all app logs in real-time  
adb -s R9ZY40RDV0K logcat | findstr "nic.hp.nicvc\|NICVC\|mono\|DEBUG"


```

# writeline eq debugging 


```cs
Console.WriteLine($"[CONSTRUCTOR] EditExpenditureDetailsPage created with ExpenseID: {expendid}");
```

```cmd
adb logcat -c
adb logcat | Select-String "\[CONSTRUCTOR\]|\[ONAPPEARING\]|\[EDIT_LOAD\]"
```


# Misc 
## Vscode 

ms-dotnettools.dotnet-maui
ms-dotnettools.csdevkit

XAML Styler
XAML Completion
xaml-snippets

This extension provides snippets for simplifying the creation of XAML and C# code in Visual Studio Code.

## Features

This extension provides snippets for the following XAML elements:

- `Label`
- `Button`
- `TextBox`
- `TextBlock`
- `CheckBox`
- `RadioButton`
- `Image`
- `StackPanel`
- `Grid`
- `RowDefinition`
- `ColumnDefinition`

And csharp code snippets for event handlers:

- `private void Button_Click(object sender, RoutedEventArgs e)`
