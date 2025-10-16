# Natural Language Requirements: TmpPage.xaml (Complete Breakdown)

---

## ✅ 1. Define ContentPage Root with Namespaces

### **Natural-Language Instruction Breakdown**
Create a XAML file starting with XML declaration version 1.0 and UTF-8 encoding. Define the root element as ContentPage. Import the standard MAUI namespace (http://schemas.microsoft.com/dotnet/2021/maui) for accessing all MAUI controls like Label, Button, Image, Grid, ScrollView, etc. Import the x namespace (http://schemas.microsoft.com/winfx/2009/xaml) for XAML-specific features like x:Class, x:Name, and other XAML directives. Set the x:Class attribute to "NICVC.TmpPage" to connect this XAML file to the TmpPage.xaml.cs code-behind class. Configure the page with BackgroundColor set to "White" for a clean white background. Set the Title to "About Us" which will appear in the navigation bar.

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

## ✅ 2. Create Custom Navigation Header with App Icon and Title

### **Natural-Language Instruction Breakdown**
Override the default navigation bar by creating a custom NavigationPage.TitleView section. Inside the TitleView, use a VerticalStackLayout but set its Orientation to "Horizontal" to arrange child elements in a horizontal row. Set HorizontalOptions to "FillAndExpand" so it stretches across the full width of the navigation bar. Set VerticalOptions to "CenterAndExpand" to center content vertically in the navigation bar. Add an Image element with Source pointing to "ic_launcher.png" (the app icon) and HeightRequest of 40 pixels to keep the icon appropriately sized. Set VerticalOptions to "CenterAndExpand" to center the icon vertically. Next to the icon, add another VerticalStackLayout with Orientation set to "Vertical" for stacking the title text. Set VerticalOptions to "CenterAndExpand" and HorizontalOptions to "CenterAndExpand" to center the title. Set Spacing to 0 to remove any gaps. Inside this second VerticalStackLayout, add a Label with Text "NIC Video Conferencing" in FontSize 20, FontAttributes set to "Bold" for emphasis, and both HorizontalTextAlignment and VerticalTextAlignment set to "Center" to perfectly center the title text. This creates a professional branded navigation header.

### **The XAML Code**
```xml
    <!-- Custom Navigation Header -->
    <NavigationPage.TitleView>
        <VerticalStackLayout Orientation="Horizontal" 
                             HorizontalOptions="FillAndExpand" 
                             VerticalOptions="CenterAndExpand">
            
            <!-- App Icon in Navigation Bar -->
            <Image Source="ic_launcher.png" 
                   HeightRequest="40" 
                   VerticalOptions="CenterAndExpand"/>
            
            <!-- App Title Container -->
            <VerticalStackLayout Orientation="Vertical" 
                                 VerticalOptions="CenterAndExpand" 
                                 HorizontalOptions="CenterAndExpand" 
                                 Spacing="0">
                
                <!-- App Title Label -->
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

## ✅ 3. Create Main Content Grid and ScrollView Container

### **Natural-Language Instruction Breakdown**
Create a Grid element as the root layout container for all page content. The Grid will allow layering of the scrollable content and the modal overlay. Inside the Grid, add a ScrollView element with VerticalOptions set to "FillAndExpand" so it fills the entire vertical space available. The ScrollView enables scrolling when content exceeds the screen height. Inside the ScrollView, create a VerticalStackLayout which will contain all the visible page content stacked vertically. Set Spacing to 10 pixels to add consistent vertical spacing between child elements. Set Margin to 0 to ensure content starts at the edge without extra padding. This creates the foundation for the scrollable content area.

### **The XAML Code**
```xml
    <!-- Main Content Grid Container -->
    <Grid>
        
        <!-- Scrollable Content Area -->
        <ScrollView VerticalOptions="FillAndExpand">
            
            <!-- Vertical Stack for All Content -->
            <VerticalStackLayout Spacing="10" Margin="0">
```

---

## ✅ 4. Display App Icon at Top of Content

### **Natural-Language Instruction Breakdown**
Add an Image element at the top of the scrollable content to display the main app icon. Set the Source property to "ic_launcher" to load the icon image from the Resources/Images folder. Set HorizontalOptions to "Center" to center the icon horizontally on the screen. Set WidthRequest to 130 pixels and HeightRequest to 100 pixels to control the icon's display dimensions and maintain consistent sizing across different screen sizes. This creates a prominent app branding element at the top of the page.

### **The XAML Code**
```xml
                <!-- App Icon Display -->
                <Image Source="ic_launcher" 
                       HorizontalOptions="Center" 
                       WidthRequest="130" 
                       HeightRequest="100" />
```

---

## ✅ 5. Display App Name Label

### **Natural-Language Instruction Breakdown**
Below the app icon, add a Label element to display the app name "NICVC". Set the Text property to "NICVC". Set FontSize to "Large" to make the app name prominent. Set TextColor to "Navy" for a professional blue color that matches the app's branding. Set HorizontalOptions to "CenterAndExpand" to center the label horizontally and allow it to expand if needed. Set HorizontalTextAlignment to "Center" to ensure the text is centered within the label. Set FontAttributes to "Bold" to make the app name stand out prominently. This creates the main app name heading.

### **The XAML Code**
```xml
                <!-- App Name Label -->
                <Label Text="NICVC" 
                       FontSize="Large" 
                       TextColor="Navy" 
                       HorizontalOptions="CenterAndExpand" 
                       HorizontalTextAlignment="Center" 
                       FontAttributes="Bold"/>
```

---

## ✅ 6. Add Hidden Label for Future Use

### **Natural-Language Instruction Breakdown**
Add another Label element below the app name that is initially hidden. Set TextColor to "Black", HorizontalOptions to "Center", and HorizontalTextAlignment to "Center" for proper styling when it becomes visible. Set IsVisible to "false" to hide the label by default. This label can be used later to display additional information like version number, build number, or temporary messages by setting its Text property and IsVisible to true in the code-behind. This provides flexibility for future enhancements without modifying the XAML structure.

### **The XAML Code**
```xml
                <!-- Hidden Label for Additional Info (e.g., version) -->
                <Label TextColor="Black" 
                       HorizontalOptions="Center" 
                       HorizontalTextAlignment="Center" 
                       IsVisible="false"/>
```

---

## ✅ 7. Display Department Heading

### **Natural-Language Instruction Breakdown**
Create a VerticalStackLayout container with HorizontalOptions set to "Center" to center its content horizontally. Inside this container, add a Label element to display the department or organization name. Set the Text property to "VC Division, New Delhi". Add TextDecorations set to "Underline" to underline the text for emphasis. Set FontSize to 18 to make it prominent but smaller than the app name. Set TextColor to "Navy" to match the app's color scheme. Set FontAttributes to "Bold" to make it stand out. Set HorizontalOptions to "FillAndExpand" and HorizontalTextAlignment to "Center" to ensure the text is centered. This creates a clear identifier of which department or organization owns this app.

### **The XAML Code**
```xml
                <!-- Department/Organization Heading -->
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

## ✅ 8. Create Tappable "Call Us" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to initiate a phone call. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange the icon and text side by side. Add a GestureRecognizers section containing a TapGestureRecognizer with the Tapped event set to "Deptt_Call" which will trigger the Deptt_Call method in the code-behind when the row is tapped. Inside the layout, add an Image element with Source set to "ic_phone" to display a phone icon and HeightRequest set to 30 pixels for appropriate sizing. Next to the icon, add a Label with Text set to "Call Us", TextColor set to "Black", and FontSize set to 16 for readability. This creates a clickable row that users can tap to call the department.

### **The XAML Code**
```xml
                <!-- Call Us Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Call" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Phone Icon -->
                    <Image Source="ic_phone" HeightRequest="30"/>
                    
                    <!-- Call Us Label -->
                    <Label Text="Call Us" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 9. Create Tappable "Website" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to open the department website in a browser. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange content in a row. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "Deptt_WebSite" to trigger the website opening method in the code-behind. Inside the layout, add an Image element with Source set to "ic_website" to display a website/globe icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Website", TextColor set to "Black", and FontSize set to 16. This creates a tappable row that opens the department's website in the default browser when tapped.

### **The XAML Code**
```xml
                <!-- Website Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_WebSite" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Website Icon -->
                    <Image Source="ic_website" HeightRequest="30"/>
                    
                    <!-- Website Label -->
                    <Label Text="Website" 
                           TextColor="Black" 
                           FontSize="16"/>
                </VerticalStackLayout>
```

---

## ✅ 10. Create Tappable "Email" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to compose an email to the department. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange the icon and label horizontally. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "Deptt_Email" to trigger the email composition method in the code-behind. Inside the layout, add an Image element with Source set to "ic_email" to display an email/envelope icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Email", TextColor set to "Black", and FontSize set to 16. This creates a tappable row that opens the device's email app with the department email pre-filled when tapped.

### **The XAML Code**
```xml
                <!-- Email Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Email" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Email Icon -->
                    <Image Source="ic_email" HeightRequest="30"/>
                    
                    <!-- Email Label -->
                    <Label Text="Email" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 11. Create Tappable "Preferences" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to access app preferences or settings. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange content in a horizontal row. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "Preferences" to navigate to the preferences page when tapped. Inside the layout, add an Image element with Source set to "ic_setting" to display a settings/gear icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Preferences", TextColor set to "Black", and FontSize set to 16. This creates a tappable row that navigates users to the app settings page where they can configure various options.

### **The XAML Code**
```xml
                <!-- Preferences Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Preferences" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Settings Icon -->
                    <Image Source="ic_setting" HeightRequest="30"/>
                    
                    <!-- Preferences Label -->
                    <Label Text="Preferences" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 12. Create Tappable "Update Personal Info" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to update their personal information or profile. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange elements side by side. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "PersonalInfo_Tapped" to navigate to the personal information edit page. Inside the layout, add an Image element with Source set to "ic_profile" to display a profile/user icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Update Personal Info", TextColor set to "Black", and FontSize set to 16. This creates a tappable row that navigates users to a page where they can edit their profile details like name, email, phone number, etc.

### **The XAML Code**
```xml
                <!-- Update Personal Info Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="PersonalInfo_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Profile Icon -->
                    <Image Source="ic_profile" HeightRequest="30"/>
                    
                    <!-- Personal Info Label -->
                    <Label Text="Update Personal Info" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 13. Create Tappable "Delete Profile" Row with Icon and Red Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to permanently delete their account profile. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange elements in a row. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "DeleteProfile_Tapped" to trigger the profile deletion confirmation dialog. Inside the layout, add an Image element with Source set to "ic_delete" to display a delete/trash icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Delete Profile", TextColor set to "Red" (not Black) to indicate this is a destructive action that requires caution, and FontSize set to 16. The red color serves as a visual warning that this action is permanent and cannot be undone. This creates a tappable row that initiates the account deletion process with appropriate confirmation dialogs.

### **The XAML Code**
```xml
                <!-- Delete Profile Interactive Row (Destructive Action) -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="DeleteProfile_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Delete Icon -->
                    <Image Source="ic_delete" HeightRequest="30"/>
                    
                    <!-- Delete Profile Label (Red for Warning) -->
                    <Label Text="Delete Profile" 
                           TextColor="Red" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 14. Create Tappable "Logout" Row with Icon and Label

### **Natural-Language Instruction Breakdown**
Create an interactive row that users can tap to log out of the application. Use a VerticalStackLayout with Orientation set to "Horizontal" to arrange elements horizontally. Add a GestureRecognizers section with a TapGestureRecognizer that has the Tapped event set to "Logout" to trigger the logout confirmation and process. Inside the layout, add an Image element with Source set to "ic_logout" to display a logout/exit icon and HeightRequest set to 30 pixels. Next to the icon, add a Label with Text set to "Logout", TextColor set to "Black", and FontSize set to 16. This creates a tappable row that logs the user out of the app, clears their session data, and typically navigates them back to the login screen.

### **The XAML Code**
```xml
                <!-- Logout Interactive Row -->
                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Logout" />
                    </VerticalStackLayout.GestureRecognizers>
                    
                    <!-- Logout Icon -->
                    <Image Source="ic_logout" HeightRequest="30" />
                    
                    <!-- Logout Label -->
                    <Label Text="Logout" 
                           TextColor="Black" 
                           FontSize="16" />
                </VerticalStackLayout>
```

---

## ✅ 15. Display NIC Logo at Bottom of Scrollable Content

### **Natural-Language Instruction Breakdown**
At the bottom of all the interactive rows, add an Image element to display the NIC (National Informatics Centre) official logo. Set the Source property to "ic_niclogo" to load the NIC logo image from the Resources/Images folder. Set HorizontalOptions to "Center" to center the logo horizontally on the screen. Set WidthRequest to 150 pixels and HeightRequest to 100 pixels to control the logo's display size and maintain proper aspect ratio. This serves as official branding indicating the app is developed by or associated with the National Informatics Centre, adding credibility and government identity to the application. After this element, close the VerticalStackLayout and ScrollView tags to complete the scrollable content section.

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

## ✅ 16. Create Modal Popup Overlay for Logout Instructions

### **Natural-Language Instruction Breakdown**
Create a modal popup overlay that can be shown to help users understand how to logout. Use a ContentView element with IsVisible set to "false" so the modal is hidden by default and can be shown programmatically from the code-behind. Set BackgroundColor to "#C0808080" which is a semi-transparent gray (C0 = 75% opacity) to create an overlay effect that dims the background content. Set Padding to 10 pixels for spacing around the modal content. Inside the ContentView, create a Border element (instead of the deprecated Frame) with Stroke set to "Gold" for a distinctive golden border, StrokeThickness set to 2 pixels for a visible border, and Background set to "White" for a solid white modal background. Set both HorizontalOptions and VerticalOptions to "FillAndExpand" so the Border fills the available space in the ContentView. This creates the foundation for a modal dialog that overlays the main content.

### **The XAML Code**
```xml
        <!-- Modal Popup Overlay (Hidden by Default) -->
        <ContentView IsVisible="false" 
                     BackgroundColor="#C0808080" 
                     Padding="10">
            
            <!-- Modal Border Container -->
            <Border Stroke="Gold" 
                    StrokeThickness="2" 
                    Background="White" 
                    HorizontalOptions="FillAndExpand" 
                    VerticalOptions="FillAndExpand">
```

---

## ✅ 17. Add Modal Title and Instruction Content

### **Natural-Language Instruction Breakdown**
Inside the Border, create a VerticalStackLayout to stack the modal content vertically. First, add a Label element with Text set to "How to Logout" to serve as the modal title. Set HorizontalOptions to "CenterAndExpand" to center the title horizontally. Set FontAttributes to "Bold" and FontSize to 16 to make the title prominent. Below the title, create a Grid element to organize the instructional content. Define Grid.RowDefinitions with two rows: the first row with Height set to "*" (star sizing) to take up all available space, and the second row with Height set to "Auto" to size itself based on content. In the first row (Grid.Row="0"), add an Image element with Source set to "l3.png" which should contain a screenshot or diagram showing the logout steps. Set VerticalOptions to "Fill" and HorizontalOptions to "FillAndExpand" so the image fills the row space. In the second row (Grid.Row="1"), add a Label with Text explaining the logout steps: "Click On Menu Icon (1) and choose Logout (2) option." Set TextColor to "Red" for emphasis, HorizontalTextAlignment and VerticalTextAlignment to "Center" to center the text, and FontAttributes to "Bold" to make the instructions stand out. This creates clear visual and text instructions for users.

### **The XAML Code**
```xml
                <!-- Modal Content Stack -->
                <VerticalStackLayout>
                    
                    <!-- Modal Title -->
                    <Label Text="How to Logout" 
                           HorizontalOptions="CenterAndExpand" 
                           FontAttributes="Bold" 
                           FontSize="16"/>
                    
                    <!-- Instructions Grid with Image and Text -->
                    <Grid>
                        <Grid.RowDefinitions>
                            <RowDefinition Height="*"/>
                            <RowDefinition Height="Auto"/>
                        </Grid.RowDefinitions>
                        
                        <!-- Instructional Screenshot/Diagram -->
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
```

---

## ✅ 18. Add Continue Button and Close All Tags

### **Natural-Language Instruction Breakdown**
Below the Grid containing instructions, add a Button element to allow users to proceed after reading the instructions. Set the Text property to "Continue to Logout" to clearly indicate the action. Set the Clicked event to "Btn_CloseThisHelp_Clicked" which will close the modal and proceed with the logout process. Set BackgroundColor to "Navy" for a strong blue color and TextColor to "White" for high contrast and readability. This button gives users control to dismiss the help modal and continue with their intended action. After the Button, close the VerticalStackLayout tag to end the modal content stack, close the Border tag to end the modal container, close the ContentView tag to end the modal overlay, close the Grid tag to end the main page container, and finally close the ContentPage tag to complete the entire XAML file structure.

### **The XAML Code**
```xml
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
                       Horizont

# Complete TmpPage.xaml File

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ContentPage xmlns="http://schemas.microsoft.com/dotnet/2021/maui"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             x:Class="NICVC.TmpPage"
             BackgroundColor="White"
             Title="About Us">

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

    <Grid>
        <ScrollView VerticalOptions="FillAndExpand">
            <VerticalStackLayout Spacing="10" Margin="0">

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

                <VerticalStackLayout HorizontalOptions="Center">
                    <Label Text="VC Division, New Delhi" 
                           TextDecorations="Underline" 
                           FontSize="18" 
                           TextColor="Navy" 
                           FontAttributes="Bold" 
                           HorizontalOptions="FillAndExpand" 
                           HorizontalTextAlignment="Center" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Call" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_phone" HeightRequest="30"/>
                    <Label Text="Call Us" TextColor="Black" FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_WebSite" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_website" HeightRequest="30"/>
                    <Label Text="Website" TextColor="Black" FontSize="16"/>
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Deptt_Email" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_email" HeightRequest="30"/>
                    <Label Text="Email" TextColor="Black" FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Preferences" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_setting" HeightRequest="30"/>
                    <Label Text="Preferences" TextColor="Black" FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="PersonalInfo_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_profile" HeightRequest="30"/>
                    <Label Text="Update Personal Info" TextColor="Black" FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="DeleteProfile_Tapped" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_delete" HeightRequest="30"/>
                    <Label Text="Delete Profile" TextColor="Red" FontSize="16" />
                </VerticalStackLayout>

                <VerticalStackLayout Orientation="Horizontal">
                    <VerticalStackLayout.GestureRecognizers>
                        <TapGestureRecognizer Tapped="Logout" />
                    </VerticalStackLayout.GestureRecognizers>
                    <Image Source="ic_logout" HeightRequest="30" />
                    <Label Text="Logout" TextColor="Black" FontSize="16" />
                </VerticalStackLayout>

                <Image Source="ic_niclogo" 
                       HorizontalOptions="Center" 
                       WidthRequest="150" 
                       HeightRequest="100"/>

            </VerticalStackLayout>
        </ScrollView>

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

**Complete TmpPage.xaml includes:**
1. Custom NavigationPage.TitleView with app icon and title
2. ScrollView with VerticalStackLayout containing app branding
3. Seven interactive rows (Call, Website, Email, Preferences, Personal Info, Delete Profile, Logout)
4. NIC logo at bottom
5. Hidden modal popup for logout instructions

All interactive rows use TapGestureRecognizer to trigger code-behind event handlers.