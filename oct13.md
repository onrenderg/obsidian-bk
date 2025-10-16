I see the issue! The problem is that the Grid inside the Frame only has 5 row definitions (rows 0-4), but the buttons are placed in Grid.Row="7" and Grid.Row="8". This means they're being placed in non-existent rows, which is causing layout issues.

Let me check the Grid row definitions:


##  **Simple Radio Button Dark Mode Fix:**

### **What I Changed:**

1. **Grid Background**: Added `BackgroundColor="{AppThemeBinding Light=Transparent, Dark=Transparent}"` to ensure no black bars
2. **Text Colors**: Changed `TextColor="Navy"` to `TextColor="{AppThemeBinding Light=Navy, Dark=LightBlue}"` for:
    - The label (`lbl_Type`)
    - Both radio buttons (`rb_exptype` and `rb_expdate`)

### **Why This Works:**

- **Light Mode**: Navy text on transparent background (same as before)
- **Dark Mode**: Light blue text on transparent background (visible and readable)
- **No black bars**: The transparent background prevents any unwanted dark bars
- **Minimal changes**: Only touched the radio button section, left everything else as-is




## **The XAML Solution Implemented:**

### **1. AppThemeBinding for Conditional Values:**

xaml

BackgroundColor="{AppThemeBinding Light=Transparent, Dark=Transparent}"

**Why this approach:**

- `AppThemeBinding` is MAUI's built-in mechanism for theme-aware styling
- It automatically switches values based on the device's light/dark mode setting
- `Light=Transparent, Dark=Transparent` ensures no background color in both modes
- This prevents the black bar appearance that was happening in dark mode