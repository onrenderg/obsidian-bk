


@Dashboard.xaml@res-xam

* root container 
	* navigation header  with logo and title 
	* toolbar with home button and *theme aware icon*
* main layout structure
	* grid root layout container 
		* stacklayout MainContent wrapped with spacing and padding 



Document current layout structure with purposes : Dashboard.xaml

[[md_34343]]

Create documentation showing what needs to be changed for obsolete warnings

[[md_3322]]
[[aimd_dfdf]]


## Warning 

View.HorizontalOptions

FillAndExpand is obselete : The Stacklayout optsions are depricated use Grid instead 

## Solution

### **Modern Grid Approach (Recommended)**

### **Modern Approach (Option 2)**

- Replace entire `StackLayout` structure with `Grid`
- Use `ColumnDefinitions` for layout control
- Eliminates nested `StackLayout` complexity



```xml
<NavigationPage.TitleView>
    <StackLayout x:Name="Custom_Navigation" Orientation="Horizontal" HorizontalOptions="FillAndExpand" VerticalOptions="CenterAndExpand">
        <Image Source="ic_himachallogo.png" HeightRequest="40" WidthRequest="40" VerticalOptions="CenterAndExpand"/>
        <StackLayout Orientation="Vertical" VerticalOptions="CenterAndExpand" HorizontalOptions="CenterAndExpand" Spacing="0">
            <Label x:Name="lbl_navigation_header" TextColor="White" FontSize="20" FontAttributes="Bold" HorizontalTextAlignment="Center" VerticalTextAlignment="Center" />
        </StackLayout>
    </StackLayout>
</NavigationPage.TitleView>
```

To 

```xml
<NavigationPage.TitleView>
    <Grid x:Name="Custom_Navigation" HorizontalOptions="Fill" VerticalOptions="Center">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto"/>
            <ColumnDefinition Width="*"/>
        </Grid.ColumnDefinitions>
        
        <Image Grid.Column="0" Source="ic_himachallogo.png" HeightRequest="40" WidthRequest="40" VerticalOptions="Center"/>
        <Label Grid.Column="1" x:Name="lbl_navigation_header" TextColor="White" FontSize="20" FontAttributes="Bold" 
               HorizontalTextAlignment="Center" VerticalTextAlignment="Center" HorizontalOptions="Center" VerticalOptions="Center"/>
    </Grid>
</NavigationPage.TitleView>
```


**Option 1** is cleaner - define ToolbarItems at the NavigationPage level where they logically belong, rather than mixing them with ContentPage content.

```cs
public partial class App : Application
{
    public App()
    {
        InitializeComponent();
        
        var navPage = new NavigationPage(new DashboardPage());
        navPage.ToolbarItems.Add(new ToolbarItem
        {
            IconImageSource = new AppThemeBinding 
            { 
                Light = "ic_home.png", 
                Dark = "ic_homewhite.png" 
            }
        });
        
        MainPage = navPage;
    }
}
```


```xml
<NavigationPage.TitleView>
    <StackLayout x:Name="Custom_Navigation" Orientation="Horizontal" HorizontalOptions="Fill" VerticalOptions="Center">
        <Image Source="ic_himachallogo.png" HeightRequest="40" WidthRequest="40" VerticalOptions="Center"/>
        <Label x:Name="lbl_navigation_header" TextColor="White" FontSize="20" FontAttributes="Bold" 
               HorizontalTextAlignment="Center" VerticalTextAlignment="Center" 
               HorizontalOptions="Fill" VerticalOptions="Center"/>
        <ImageButton Clicked="ToolbarItem_Clicked" HeightRequest="40" WidthRequest="40" 
                     BackgroundColor="Transparent" VerticalOptions="Center">
            <ImageButton.Source>
                <AppThemeBinding Light="ic_home.png" Dark="ic_homewhite.png"/>
            </ImageButton.Source>
        </ImageButton>
    </StackLayout>
</NavigationPage.TitleView>
```

```xml
<NavigationPage.TitleView>
    <Grid HorizontalOptions="Fill" VerticalOptions="Center">
        <Grid.ColumnDefinitions>
            <ColumnDefinition Width="Auto"/>
            <ColumnDefinition Width="*"/>
            <ColumnDefinition Width="Auto"/>
        </Grid.ColumnDefinitions>
        
        <Image Grid.Column="0" Source="ic_himachallogo.png" HeightRequest="40"/>
        <Label Grid.Column="1" x:Name="lbl_navigation_header" TextColor="White"/>
        <ImageButton Grid.Column="2" Clicked="ToolbarItem_Clicked">
            <ImageButton.Source>
                <AppThemeBinding Light="ic_home.png" Dark="ic_homewhite.png"/>
            </ImageButton.Source>
        </ImageButton>
    </Grid>
</NavigationPage.TitleView>
```

