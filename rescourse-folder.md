

Resources are defined in the `<Application.Resources>` section of your `App.xaml` file. They can be:

1.  **Colors:**

    ```xml
    <Color x:Key="Light_Btn_Text_Color">White</Color>
    ```

2.  **Styles:**

    ```xml
    <Style x:Key="LabelStyle" TargetType="Label">
        <Setter Property="TextColor" Value="Black" />
        <Setter Property="FontSize" Value="14" />
    </Style>
    ```

3.  **Other objects** like brushes, converters, etc.

### How Resources Work

**Define once in App.xaml:**

```xml
<Application.Resources>
    <Style x:Key="MyButtonStyle" TargetType="Button">
        <Setter Property="BackgroundColor" Value="Blue" />
    </Style>
</Application.Resources>
```

**Use anywhere with StaticResource:**

```xml
<Button Style="{StaticResource MyButtonStyle}" Text="Click me" />
```

### The Problem in Your MainPage

Your `MainPage.xaml` was trying to use:

```xml
Style="{StaticResource Headline}"
Style="{StaticResource SubHeadline}"
```

But these resources (`Headline` and `SubHeadline`) were not defined in your `App.xaml` resources section. When the app tried to find them, it couldn't locate them and crashed.

### The Solution

I replaced them with resources that do exist in your `App.xaml`:

*   `LabelStyle_PageTitle`
*   `LabelStyle`