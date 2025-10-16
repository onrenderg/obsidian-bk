# Updated Fundamental MAUI XAML Tags

## **Pages**
- `<ContentPage>` - Basic page container
- `<NavigationPage>` - Page with navigation bar
- `<TabbedPage>` - Page with tabs
- `<FlyoutPage>` - Page with flyout menu

## **Layouts**
- `<Grid>` - Grid-based layout (rows/columns)
- `<VerticalStackLayout>` - Vertical stacking layout
- `<HorizontalStackLayout>` - Horizontal stacking layout
- `<FlexLayout>` - Flexible layout
- `<AbsoluteLayout>` - Absolute positioning layout

## **Controls**
- `<Label>` - Text display
- `<Button>` - Clickable button
- `<Entry>` - Single-line text input
- `<Editor>` - Multi-line text input
- `<Image>` - Image display
- `<Border>` - Bordered container (replaces deprecated `<Frame>`)
- `<CheckBox>` - Checkbox input
- `<RadioButton>` - Radio button input
- `<Switch>` - Toggle switch
- `<Slider>` - Value slider
- `<Stepper>` - Increment/decrement control
- `<Picker>` - Selection dropdown
- `<DatePicker>` - Date selection
- `<TimePicker>` - Time selection

## **Containers & Views**
- `<ScrollView>` - Scrollable content
- `<StackLayout>` - Legacy vertical/horizontal stack (use VerticalStackLayout instead)
- `<ContentView>` - Custom content container

## **Data & Binding**
- `<CollectionView>` - List/data display
- `<CarouselView>` - Carousel of items

## **Update Note**
- `<Frame>` is deprecated in recent MAUI versions; use `<Border>` for framed content.
- This list reflects .NET MAUI 8+ recommendations.



![[Pasted image 20251016110443.png]]
# Imp

# Recreating the UI Based on Fundamental MAUI Tags

Assuming the uploaded image matches the AboutUsPage structure from your earlier XAML (custom navigation, app info, interactive rows, and a modal popup), I'll recreate it using the updated fundamental tags. I've used `<Border>` instead of the deprecated `<Frame>` and stuck to core elements like `<ContentPage>`, `<Grid>`, `<VerticalStackLayout>`, `<Image>`, `<Label>`, `<Button>`, and `<ContentView>`.

## **Recreated XAML Structure**

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="NICVC.AboutUsPage"
             BackgroundColor="White"
             Title="About Us">

    <!-- Custom Navigation -->
    <NavigationPage.TitleView>
        <VerticalStackLayout Orientation="Horizontal" 
                             HorizontalOptions="FillAndExpand" 
                             VerticalOptions="CenterAndExpand">
            <Image Source="ic_launcher.png" 
                   HeightRequest="40" 
                   VerticalOptions="CenterAndExpand"/>
            <VerticalStackLayout Orientation="Vertical" 
                                 VerticalOptions="CenterAndExpand" 
                                 HorizontalOptions="CenterAndExpand" 
                                 Spacing="0">
                <Label Text="NIC Video Conferencing" 
                       FontSize="20" 
                       FontAttributes="Bold" 
                       HorizontalTextAlignment="Center"
                       VerticalTextAlignment="Center" />
            </VerticalStackLayout>
        </VerticalStackLayout>
    </NavigationPage.TitleView>

    <!-- Main Content -->
    <Grid>
        <ScrollView VerticalOptions="FillAndExpand">
            <VerticalStackLayout Spacing="10" Margin="0">

                <!-- App Icon and Name -->
                <Image Source="ic_launcher" 
                       HorizontalOptions="Center" 
                       WidthRequest="130" 
                       HeightRequest="100" />
                <Label Text="NICVC" 
                       FontSize="Large" 
                       TextColor="Navy" 
                       HorizontalOptions="CenterAndExpand" 
                       HorizontalTextAlignment="Center" 
                       FontAttributes="Bold"/>
                <Label TextColor="Black" 
                       HorizontalOptions="Center" 
                       HorizontalTextAlignment="Center" 
                       IsVisible="false"/>

                <!-- Department Info -->
                <VerticalStackLayout HorizontalOptions="Center">
                    <Label Text="VC Division, New Delhi" 
                           TextDecorations="Underline" 
                           FontSize="18" 
                           TextColor="Navy" 
                           FontAttributes="Bold" 
                           HorizontalOptions="FillAndExpand" 
                           HorizontalTextAlignment="Center" />
                </VerticalStackLayout>

                <!-- Interactive Rows -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Call" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_phone" HeightRequest="30"/>
                    <Label Text="Call Us" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_WebSite" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_website" HeightRequest="30"/>
                    <Label Text="Website" 
                           TextColor="Black" 
                           FontSize="16"/>
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Email" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_email" HeightRequest="30"/>
                    <Label Text="Email" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Preferences" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_setting" HeightRequest="30"/>
                    <Label Text="Preferences" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="PersonalInfo_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_profile" HeightRequest="30"/>
                    <Label Text="Update Personal Info" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="DeleteProfile_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_delete" HeightRequest="30"/>
                    <Label Text="Delete Profile" 
                           TextColor="Red" 
                           FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Logout" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_logout" HeightRequest="30" />
                    <Label Text="Logout" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>

                <!-- NIC Logo -->
                <Image Source="ic_niclogo" 
                       HorizontalOptions="Center" 
                       WidthRequest="150" 
                       HeightRequest="100"/>

            </VerticalStackLayout>
        </ScrollView>

        <!-- Modal Popup (using Border) -->
        <ContentView IsVisible="false" BackgroundColor="#C0808080" Padding="10">
            <Border Stroke="Gold" 
                    StrokeThickness="2" 
                    Background="White" 
                    HorizontalOptions="FillAndExpand" 
                    VerticalOptions="FillAndExpand">
                <VerticalStackLayout>
                    <Label Text="How to Logout" 
                           HorizontalOptions="CenterAndExpand" 
                           FontAttributes="Bold" 
                           FontSize="16"/>
                    <Grid>
                        <Grid.RowDefinitions>
                            <RowDefinition Height="*"/>
                            <RowDefinition Height="Auto"/>
                        </Grid.RowDefinitions>
                        <Image Source="l3.png" 
                               VerticalOptions="Fill" 
                               HorizontalOptions="FillAndExpand" 
                               Grid.Row="0"/>
                        <Label Text="Click On Menu Icon (1) and choose Logout (2) option." 
                               TextColor="Red" 
                               HorizontalTextAlignment="Center" 
                               VerticalTextAlignment="Center" 
                               FontAttributes="Bold" 
                               Grid.Row="1"/>
                    </Grid>
                    <Button Text="Continue to Logout" 
                            Clicked="Btn_CloseThisHelp_Clicked" 
                            BackgroundColor="Navy" 
                            TextColor="White"/>
                </VerticalStackLayout>
            </Border>
        </ContentView>
    </Grid>
</ContentPage>
```

## **Corresponding C# Code-Behind (AboutUsPage.xaml.cs)**

```csharp
using Microsoft.Maui.Controls;

namespace NICVC
{
    public partial class AboutUsPage : ContentPage
    {
        public AboutUsPage()
        {
            InitializeComponent();
        }

        private void Deptt_Call(object sender, EventArgs e)
        {
            // Handle call action
        }

        private void Deptt_WebSite(object sender, EventArgs e)
        {
            // Handle website navigation
        }

        private void Deptt_Email(object sender, EventArgs e)
        {
            // Handle email action
        }

        private void Preferences(object sender, EventArgs e)
        {
            // Handle preferences navigation
        }

        private void PersonalInfo_Tapped(object sender, EventArgs e)
        {
            // Handle personal info update
        }

        private void DeleteProfile_Tapped(object sender, EventArgs e)
        {
            // Handle profile deletion
        }

        private void Logout(object sender, EventArgs e)
        {
            // Handle logout
        }

        private void Btn_CloseThisHelp_Clicked(object sender, EventArgs e)
        {
            // Close modal
        }
    }
}
```

This recreates the UI using modern MAUI tags. Adjust properties (e.g., colors, images) to match your exact design. If the image differs, provide more details for refinements!