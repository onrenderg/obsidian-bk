# Natural Language Requirements: TmpPage.xaml (Complete Breakdown)

---

## ✅ 1. Define ContentPage Root with Namespaces

### **Natural-Language Instruction Breakdown**
Create a XAML file starting with XML declaration and ContentPage root element. Import the standard MAUI namespace for controls like Label, Button, Image, and Grid. Import the x namespace for XAML-specific features like x:Class and x:Name. Set the x:Class attribute to connect this XAML file to the TmpPage.xaml.cs code-behind class. Configure the page with a white background color and title "About Us".

### **The XAML Code**
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="NICVC.TmpPage"
             BackgroundColor="White"
             Title="About Us">
```

---

## ✅ 2. Create Custom Navigation Header (TitleView)

### **Natural-Language Instruction Breakdown**
Override the default navigation bar by creating a custom NavigationPage.TitleView. Inside the TitleView, use a VerticalStackLayout with horizontal orientation to arrange elements in a row. Add an app icon Image on the left with 40 pixels height, centered vertically. Next to it, add another VerticalStackLayout containing a Label that displays "NIC Video Conferencing" in bold 20-point font, centered both horizontally and vertically. This creates a branded navigation header with logo and app name.

### **The XAML Code**
```xml
    <!-- Custom Navigation Header -->
    <NavigationPage.TitleView>
        <VerticalStackLayout Orientation="Horizontal" 
                             HorizontalOptions="FillAndExpand" 
                             VerticalOptions="CenterAndExpand">
            <!-- App Icon -->
            <Image Source="ic_launcher.png" 
                   HeightRequest="40" 
                   VerticalOptions="CenterAndExpand"/>
            
            <!-- App Title -->
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
```

---

## ✅ 3. Create Main Content Grid Container

### **Natural-Language Instruction Breakdown**
Create a Grid as the root layout container for the page content. Inside the Grid, add a ScrollView that fills the entire vertical space to enable scrolling when content exceeds screen height. Inside the ScrollView, create a VerticalStackLayout with 10 pixels spacing between elements and zero margin. This VerticalStackLayout will hold all the page's content sections stacked vertically.

### **The XAML Code**
```xml
    <!-- Main Content Grid -->
    <Grid>
        <ScrollView VerticalOptions="FillAndExpand">
            <VerticalStackLayout Spacing="10" Margin="0">
```

---

## ✅ 4. Display App Icon and App Name

### **Natural-Language Instruction Breakdown**
At the top of the scrollable content, display the app icon as an Image centered horizontally with dimensions 130 pixels wide by 100 pixels tall. Below it, add a Label displaying "NICVC" in large navy blue bold text, centered horizontally. Add another Label below that is initially hidden (IsVisible="false") for displaying additional information later if needed. This creates the app branding section at the top of the page.

### **The XAML Code**
```xml
                <!-- App Icon and Name Section -->
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
```

---

## ✅ 5. Display Department/Organization Info

### **Natural-Language Instruction Breakdown**
Create a section displaying the department name by wrapping a Label inside a VerticalStackLayout centered horizontally. The Label displays "VC Division, New Delhi" in navy blue 18-point bold font with underline decoration, centered horizontally. This section identifies which department or organization the app belongs to.

### **The XAML Code**
```xml
                <!-- Department Information -->
                <VerticalStackLayout HorizontalOptions="Center">
                    <Label Text="VC Division, New Delhi" 
                           TextDecorations="Underline" 
                           FontSize="18" 
                           TextColor="Navy" 
                           FontAttributes="Bold" 
                           HorizontalOptions="FillAndExpand" 
                           HorizontalTextAlignment="Center" />
                </VerticalStackLayout>
```

---

## ✅ 6. Create Tappable "Call Us" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for calling the department by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer to make the entire row tappable, triggering the Deptt_Call event handler when clicked. Inside the layout, display a phone icon Image with 30 pixels height, followed by a Label displaying "Call Us" in black 16-point font. This row allows users to initiate a phone call when tapped.

### **The XAML Code**
```xml
                <!-- Call Us Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Call" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_phone" HeightRequest="30"/>
                    <Label Text="Call Us" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 7. Create Tappable "Website" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for opening the department website by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the Deptt_WebSite event handler when the row is tapped. Display a website icon Image with 30 pixels height, followed by a Label showing "Website" in black 16-point font. This row allows users to open the department's website in a browser when tapped.

### **The XAML Code**
```xml
                <!-- Website Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_WebSite" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_website" HeightRequest="30"/>
                    <Label Text="Website" 
                           TextColor="Black" 
                           FontSize="16"/>
                </VerticalStackLayout>
```

---

## ✅ 8. Create Tappable "Email" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for sending email to the department by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the Deptt_Email event handler when tapped. Display an email icon Image with 30 pixels height, followed by a Label showing "Email" in black 16-point font. This row allows users to compose and send an email when tapped.

### **The XAML Code**
```xml
                <!-- Email Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Email" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_email" HeightRequest="30"/>
                    <Label Text="Email" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 9. Create Tappable "Preferences" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for opening app preferences/settings by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the Preferences event handler when tapped. Display a settings icon Image with 30 pixels height, followed by a Label showing "Preferences" in black 16-point font. This row navigates users to the app settings page when tapped.

### **The XAML Code**
```xml
                <!-- Preferences Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Preferences" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_setting" HeightRequest="30"/>
                    <Label Text="Preferences" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 10. Create Tappable "Update Personal Info" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for updating user's personal information by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the PersonalInfo_Tapped event handler when tapped. Display a profile icon Image with 30 pixels height, followed by a Label showing "Update Personal Info" in black 16-point font. This row navigates users to a page where they can edit their profile information when tapped.

### **The XAML Code**
```xml
                <!-- Update Personal Info Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="PersonalInfo_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_profile" HeightRequest="30"/>
                    <Label Text="Update Personal Info" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 11. Create Tappable "Delete Profile" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for deleting user's profile by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the DeleteProfile_Tapped event handler when tapped. Display a delete icon Image with 30 pixels height, followed by a Label showing "Delete Profile" in red 16-point font to indicate the destructive nature of this action. This row allows users to permanently delete their account when tapped, usually with a confirmation dialog.

### **The XAML Code**
```xml
                <!-- Delete Profile Row (Destructive Action) -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="DeleteProfile_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_delete" HeightRequest="30"/>
                    <Label Text="Delete Profile" 
                           TextColor="Red" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 12. Create Tappable "Logout" Row

### **Natural-Language Instruction Breakdown**
Create an interactive row for logging out of the app by using a VerticalStackLayout with horizontal orientation. Add a TapGestureRecognizer that triggers the Logout event handler when tapped. Display a logout icon Image with 30 pixels height, followed by a Label showing "Logout" in black 16-point font with vertical center alignment. This row logs the user out and typically returns them to the login screen when tapped.

### **The XAML Code**
```xml
                <!-- Logout Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Logout" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_logout" HeightRequest="30" />
                    <Label Text="Logout" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 13. Display NIC Logo at Bottom

### **Natural-Language Instruction Breakdown**
At the bottom of the scrollable content, display the NIC (National Informatics Centre) logo as an Image centered horizontally with dimensions 150 pixels wide by 100 pixels tall. This serves as official branding and indicates the app is developed by or associated with NIC. Close the VerticalStackLayout and ScrollView tags to complete the main content section.

### **The XAML Code**
```xml
                <!-- NIC Logo at Bottom -->
                <Image Source="ic_niclogo" 
                       HorizontalOptions="Center" 
                       WidthRequest="150" 
                       HeightRequest="100"/>

            </VerticalStackLayout>
        </ScrollView>
```

---

## ✅ 14. Create Modal Popup Overlay for Logout Help

### **Natural-Language Instruction Breakdown**
Create a modal popup overlay using a ContentView that is initially hidden (IsVisible="false") with a semi-transparent gray background (#C0808080) and 10 pixels padding. Inside, create a Border with gold stroke (2 pixels thick) and white background that fills the entire space. Inside the Border, use a VerticalStackLayout to stack content vertically. Add a Label displaying "How to Logout" as the title in bold 16-point font, centered horizontally. Below it, create a Grid with two rows - the first row (* height) displays an instructional image "l3.png" that fills the space, and the second row (Auto height) contains a Label with red text explaining "Click On Menu Icon (1) and choose Logout (2) option" in bold font, centered. At the bottom, add a Button labeled "Continue to Logout" with navy background and white text that triggers the Btn_CloseThisHelp_Clicked event handler. This modal can be shown programmatically to guide users through the logout process. Close the ContentView and Grid tags to complete the page.

### **The XAML Code**
```xml
        <!-- Modal Popup Overlay for Logout Instructions -->
        <ContentView IsVisible="false" 
                     BackgroundColor="#C0808080" 
                     Padding="10">
            <Border Stroke="Gold" 
                    StrokeThickness="2" 
                    Background="White" 
                    HorizontalOptions="FillAndExpand" 
                    VerticalOptions="FillAndExpand">
                <VerticalStackLayout>
                    <!-- Modal Title -->
                    <Label Text="How to Logout" 
                           HorizontalOptions="CenterAndExpand" 
                           FontAttributes="Bold" 
                           FontSize="16"/>
                    
                    <!-- Instructions Grid -->
                    <Grid>
                        <Grid.RowDefinitions>
                            <RowDefinition Height="*"/>
                            <RowDefinition Height="Auto"/>
                        </Grid.RowDefinitions>
                        
                        <!-- Instructional Image -->
                        <Image Source="l3.png" 
                               VerticalOptions="Fill" 
                               HorizontalOptions="FillAndExpand" 
                               Grid.Row="0"/>
                        
                        <!-- Instruction Text -->
                        <Label Text="Click On Menu Icon (1) and choose Logout (2) option." 
                               TextColor="Red" 
                               HorizontalTextAlignment="Center" 
                               VerticalTextAlignment="Center" 
                               FontAttributes="Bold" 
                               Grid.Row="1"/>
                    </Grid>
                    
                    <!-- Continue Button -->
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

---

## 📄 Complete TmpPage.xaml File

### **The Complete XAML Code**
```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="NICVC.TmpPage"
             BackgroundColor="White"
             Title="About Us">

    <!-- Custom Navigation Header -->
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

    <!-- Main Content Grid -->
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

        <!-- Modal Popup -->
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

---

## 📝 Summary

**What You Have in TmpPage.xaml (In Sequence):**

1. **ContentPage root** with namespaces and class name
2. **Custom NavigationPage.TitleView** with app icon and title
3. **Grid container** holding all content
4. **ScrollView** for scrollable content
5. **VerticalStackLayout** with app branding (icon, name, department)
6. **Seven interactive rows** (Call, Website, Email, Preferences, Personal Info, Delete Profile, Logout)
7. **NIC logo** at bottom
8. **Modal popup overlay** for logout instructions (hidden by default)

This XAML creates a complete "About Us" / "More" page with navigation and interactive menu options.