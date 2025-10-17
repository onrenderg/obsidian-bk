

Page  →  Layout(s)  →  Controls / Containers  →  Data Binding (optional)


Here’s a **complete list of all snippet names and prefixes** you can use (the exact text you type before pressing `Tab`) from the **MAUI Fundamental XAML Snippet Pack** I gave you.

Grouped by category 👇

---

### 📄 **Pages**

|Snippet Name|Prefix to Type|Purpose|
|---|---|---|
|Page: ContentPage|`pagContent`|Basic page container|
|Page: NavigationPage|`pagNav`|Page with navigation bar|
|Page: TabbedPage|`pagTabbed`|Page with tabs|
|Page: FlyoutPage|`pagFlyout`|Page with flyout menu|

---

### 🧱 **Layouts**

|Snippet Name|Prefix to Type|Purpose|
|---|---|---|
|Layout: Grid|`layGrid`|Grid-based layout|
|Layout: VerticalStackLayout|`layVStack`|Vertical stacking layout|
|Layout: HorizontalStackLayout|`layHStack`|Horizontal stacking layout|
|Layout: FlexLayout|`layFlex`|Flexible layout|
|Layout: AbsoluteLayout|`layAbsolute`|Absolute positioning layout|

---

### 🎛️ **Controls**

|Snippet Name|Prefix to Type|Purpose|
|---|---|---|
|Control: Label|`conLabel`|Text display|
|Control: Button|`conButton`|Clickable button|
|Control: Entry|`conEntry`|Single-line text input|
|Control: Editor|`conEditor`|Multi-line text input|
|Control: Image|`conImage`|Image display|
|Control: Border|`conBorder`|Bordered container (replaces Frame)|
|Control: CheckBox|`conCheck`|Checkbox input|
|Control: RadioButton|`conRadio`|Radio button input|
|Control: Switch|`conSwitch`|Toggle switch|
|Control: Slider|`conSlider`|Value slider|
|Control: Stepper|`conStepper`|Increment/decrement control|
|Control: Picker|`conPicker`|Selection dropdown|
|Control: DatePicker|`conDate`|Date selection|
|Control: TimePicker|`conTime`|Time selection|

---

### 🪟 **Containers & Views**

|Snippet Name|Prefix to Type|Purpose|
|---|---|---|
|Container: ScrollView|`cntScroll`|Scrollable content|
|Container: StackLayout|`cntStack`|Legacy stack layout|
|Container: ContentView|`cntContentView`|Custom content container|

---

### 🔗 **Data & Binding**

|Snippet Name|Prefix to Type|Purpose|
|---|---|---|
|Data: CollectionView|`dabCollection`|Data list view|
|Data: CarouselView|`dabCarousel`|Carousel of items|

---

### 🧠 **Summary of Prefix Patterns**

|Category|Prefix Pattern|Example|
|---|---|---|
|Pages|`pag`|`pagContent`|
|Layouts|`lay`|`layGrid`|
|Controls|`con`|`conButton`|
|Containers|`cnt`|`cntScroll`|
|Data & Binding|`dab`|`dabCollection`|

---

Would you like me to make a **cheat sheet markdown file** (`MAUI-XAML-Snippet-Guide.md`) that lists all these prefixes with short usage examples — so you can keep it inside your project or VS Code workspace for quick reference?



```json
{
  // ===============================
  // 📄 PAGES
  // ===============================
  "Page: ContentPage": {
    "prefix": "pagContent",
    "body": [
      "<ContentPage xmlns=\"http://schemas.microsoft.com/dotnet/2021/maui\"",
      "             xmlns:x=\"http://schemas.microsoft.com/winfx/2009/xaml\"",
      "             x:Class=\"${1:YourNamespace.YourPage}\">",
      "    $0",
      "</ContentPage>"
    ],
    "description": "Create a ContentPage (basic page container)"
  },
  "Page: NavigationPage": {
    "prefix": "pagNav",
    "body": [
      "<NavigationPage>",
      "    <x:Arguments>",
      "        ${1:<ContentPage />}",
      "    </x:Arguments>",
      "</NavigationPage>"
    ],
    "description": "Create a NavigationPage (with navigation bar)"
  },
  "Page: TabbedPage": {
    "prefix": "pagTabbed",
    "body": [
      "<TabbedPage>",
      "    <ContentPage Title=\"${1:Tab 1}\">$0</ContentPage>",
      "</TabbedPage>"
    ],
    "description": "Create a TabbedPage (page with tabs)"
  },
  "Page: FlyoutPage": {
    "prefix": "pagFlyout",
    "body": [
      "<FlyoutPage>",
      "    <FlyoutPage.Flyout>",
      "        <ContentPage Title=\"Menu\" />",
      "    </FlyoutPage.Flyout>",
      "    <FlyoutPage.Detail>",
      "        <NavigationPage>",
      "            <x:Arguments>",
      "                <ContentPage Title=\"Detail\" />",
      "            </x:Arguments>",
      "        </NavigationPage>",
      "    </FlyoutPage.Detail>",
      "</FlyoutPage>"
    ],
    "description": "Create a FlyoutPage (page with flyout menu)"
  },

  // ===============================
  // 🧱 LAYOUTS
  // ===============================
  "Layout: Grid": {
    "prefix": "layGrid",
    "body": [
      "<Grid>",
      "    <Grid.RowDefinitions>",
      "        <RowDefinition Height=\"Auto\" />",
      "        <RowDefinition Height=\"*\" />",
      "    </Grid.RowDefinitions>",
      "    <Grid.ColumnDefinitions>",
      "        <ColumnDefinition Width=\"Auto\" />",
      "        <ColumnDefinition Width=\"*\" />",
      "    </Grid.ColumnDefinitions>",
      "    $0",
      "</Grid>"
    ],
    "description": "Create a Grid layout"
  },
  "Layout: VerticalStackLayout": {
    "prefix": "layVStack",
    "body": [
      "<VerticalStackLayout>",
      "    $0",
      "</VerticalStackLayout>"
    ],
    "description": "Create a VerticalStackLayout"
  },
  "Layout: HorizontalStackLayout": {
    "prefix": "layHStack",
    "body": [
      "<HorizontalStackLayout>",
      "    $0",
      "</HorizontalStackLayout>"
    ],
    "description": "Create a HorizontalStackLayout"
  },
  "Layout: FlexLayout": {
    "prefix": "layFlex",
    "body": [
      "<FlexLayout Direction=\"${1:Row}\" JustifyContent=\"${2:Start}\" AlignItems=\"${3:Center}\">$0</FlexLayout>"
    ],
    "description": "Create a FlexLayout"
  },
  "Layout: AbsoluteLayout": {
    "prefix": "layAbsolute",
    "body": [
      "<AbsoluteLayout>",
      "    $0",
      "</AbsoluteLayout>"
    ],
    "description": "Create an AbsoluteLayout"
  },

  // ===============================
  // 🎛️ CONTROLS
  // ===============================
  "Control: Label": {
    "prefix": "conLabel",
    "body": [
      "<Label Text=\"${1:Label Text}\" FontSize=\"${2:Medium}\" HorizontalOptions=\"${3:Center}\" />"
    ],
    "description": "Insert a Label (text display)"
  },
  "Control: Button": {
    "prefix": "conButton",
    "body": [
      "<Button Text=\"${1:Click Me}\" Clicked=\"${2:OnButtonClicked}\" />"
    ],
    "description": "Insert a Button (clickable control)"
  },
  "Control: Entry": {
    "prefix": "conEntry",
    "body": [
      "<Entry Placeholder=\"${1:Enter text}\" Text=\"{Binding ${2:InputText}}\" />"
    ],
    "description": "Insert an Entry (single-line input)"
  },
  "Control: Editor": {
    "prefix": "conEditor",
    "body": [
      "<Editor Placeholder=\"${1:Enter multi-line text}\" HeightRequest=\"${2:120}\" />"
    ],
    "description": "Insert an Editor (multi-line input)"
  },
  "Control: Image": {
    "prefix": "conImage",
    "body": [
      "<Image Source=\"${1:image.png}\" Aspect=\"${2:AspectFit}\" />"
    ],
    "description": "Insert an Image control"
  },
  "Control: Border": {
    "prefix": "conBorder",
    "body": [
      "<Border Stroke=\"${1:Gray}\" StrokeThickness=\"${2:1}\" Padding=\"${3:8}\">$0</Border>"
    ],
    "description": "Insert a Border (replaces Frame)"
  },
  "Control: CheckBox": {
    "prefix": "conCheck",
    "body": [
      "<CheckBox IsChecked=\"${1:False}\" />"
    ],
    "description": "Insert a CheckBox control"
  },
  "Control: RadioButton": {
    "prefix": "conRadio",
    "body": [
      "<RadioButton Content=\"${1:Option}\" GroupName=\"${2:Group1}\" />"
    ],
    "description": "Insert a RadioButton control"
  },
  "Control: Switch": {
    "prefix": "conSwitch",
    "body": [
      "<Switch IsToggled=\"${1:False}\" />"
    ],
    "description": "Insert a Switch (toggle control)"
  },
  "Control: Slider": {
    "prefix": "conSlider",
    "body": [
      "<Slider Minimum=\"${1:0}\" Maximum=\"${2:100}\" Value=\"${3:50}\" />"
    ],
    "description": "Insert a Slider control"
  },
  "Control: Stepper": {
    "prefix": "conStepper",
    "body": [
      "<Stepper Minimum=\"${1:0}\" Maximum=\"${2:10}\" Increment=\"${3:1}\" />"
    ],
    "description": "Insert a Stepper control"
  },
  "Control: Picker": {
    "prefix": "conPicker",
    "body": [
      "<Picker Title=\"${1:Select item}\">$0</Picker>"
    ],
    "description": "Insert a Picker (dropdown list)"
  },
  "Control: DatePicker": {
    "prefix": "conDate",
    "body": [
      "<DatePicker Date=\"${1:{x:Static sys:DateTime.Now}}\" />"
    ],
    "description": "Insert a DatePicker (date selector)"
  },
  "Control: TimePicker": {
    "prefix": "conTime",
    "body": [
      "<TimePicker Time=\"${1:00:00:00}\" />"
    ],
    "description": "Insert a TimePicker (time selector)"
  },

  // ===============================
  // 🪟 CONTAINERS & VIEWS
  // ===============================
  "Container: ScrollView": {
    "prefix": "cntScroll",
    "body": [
      "<ScrollView>",
      "    $0",
      "</ScrollView>"
    ],
    "description": "Insert a ScrollView (scrollable content)"
  },
  "Container: StackLayout": {
    "prefix": "cntStack",
    "body": [
      "<StackLayout Orientation=\"${1:Vertical}\">$0</StackLayout>"
    ],
    "description": "Insert a StackLayout (legacy)"
  },
  "Container: ContentView": {
    "prefix": "cntContentView",
    "body": [
      "<ContentView>",
      "    $0",
      "</ContentView>"
    ],
    "description": "Insert a ContentView (custom container)"
  },

  // ===============================
  // 🔗 DATA & BINDING
  // ===============================
  "Data: CollectionView": {
    "prefix": "dabCollection",
    "body": [
      "<CollectionView ItemsSource=\"{Binding ${1:Items}}\">",
      "    <CollectionView.ItemTemplate>",
      "        <DataTemplate>",
      "            ${2:<Label Text=\"{Binding Name}\" />}",
      "        </DataTemplate>",
      "    </CollectionView.ItemTemplate>",
      "</CollectionView>"
    ],
    "description": "Insert a CollectionView (data list)"
  },
  "Data: CarouselView": {
    "prefix": "dabCarousel",
    "body": [
      "<CarouselView ItemsSource=\"{Binding ${1:Items}}\">",
      "    <CarouselView.ItemTemplate>",
      "        <DataTemplate>",
      "            ${2:<Label Text=\"{Binding Title}\" />}",
      "        </DataTemplate>",
      "    </CarouselView.ItemTemplate>",
      "</CarouselView>"
    ],
    "description": "Insert a CarouselView (carousel of items)"
  }
}

```