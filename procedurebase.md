
expressive syntax common english

select * from db.schemna.table a
left join(db.schema.table) b  b.coulmname = left(a.coluname, 4)






Perfect! ✅ I've successfully updated the loading popup in **ObserverViewExpenditureDetailsPage.xaml**.

## ✅ **Changes Applied:**

### **What Was Changed:**

**Before (Xamarin/Old):**
```xaml
<ContentView x:Name="Loading_activity" ... AbsoluteLayout.LayoutBounds="..." AbsoluteLayout.LayoutFlags="...">
    <Frame Style="{StaticResource FrameLoadingStyle}">
        <StackLayout Orientation="Horizontal">
            <ActivityIndicator/>
            <Label/>
        </StackLayout>
    </Frame>
</ContentView>
```

**After (Modern MAUI):**
```xaml
<Grid x:Name="Loading_activity" ZIndex="1000">
    <Border BackgroundColor="White">
        <HorizontalStackLayout Spacing="10">
            <ActivityIndicator Color="Navy"/>
            <Label TextColor="Black" FontAttributes="Bold"/>
        </HorizontalStackLayout>
    </Border>
</Grid>
```

### **Key Improvements:**

1. ✅ **Grid with ZIndex="1000"** - Ensures popup appears on top of all content
2. ✅ **Border instead of Frame** - Modern MAUI control
3. ✅ **HorizontalStackLayout** - Modern MAUI layout
4. ✅ **Navy ActivityIndicator** - Visible spinner
5. ✅ **Removed AbsoluteLayout properties** - Not needed in MAUI

### **Result:**

The "Please Wait..." popup will now display correctly when you click the **Observer Remarks** button! 🎉