# How to customize header icon in Xamarin.Forms Expander (SfExpander)?

You can customize the Xamarin.Forms [SfExpander](https://help.syncfusion.com/xamarin/expander/getting-started?) header icon in the SfExpander.Header elements using the [converter](https://docs.microsoft.com/en-us/xamarin/xamarin-forms/app-fundamentals/data-binding/converters).

You can also refer the following article.

https://www.syncfusion.com/kb/11378/how-to-customize-header-icon-in-xamarin-forms-expander-sfexpander

**XAML**

Binding the [IsExpanded](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Expander.SfExpander~IsExpanded.html?) property to show different icons to expand and collapse. Set [HeaderIconPosition](https://help.syncfusion.com/cr/cref_files/xamarin/Syncfusion.Expander.XForms~Syncfusion.XForms.Expander.SfExpander~HeaderIconPosition.html?) to None to hide the default header icon.

``` xml
<ContentPage xmlns="http://xamarin.com/schemas/2014/forms"
             xmlns:x="http://schemas.microsoft.com/winfx/2009/xaml"
             xmlns:local="clr-namespace:ExpanderXamarin"
             xmlns:syncfusion="clr-namespace:Syncfusion.XForms.Expander;assembly=Syncfusion.Expander.XForms"
             x:Class="ExpanderXamarin.MainPage">
 
    <ContentPage.Resources>
        <ResourceDictionary>
            <local:ExpanderIconConverter x:Key="ExpanderIconConverter"/>
        </ResourceDictionary>
    </ContentPage.Resources>
    
    <ContentPage.Content>
        <ScrollView BackgroundColor="#EDF2F5">
            <StackLayout>
                <syncfusion:SfExpander x:Name="expander1" HeaderIconPosition="None">
                    <syncfusion:SfExpander.Header>
                        <Grid HeightRequest="50">
                            <Label Text="Veg Pizza" TextColor="#495F6E" VerticalTextAlignment="Center" Margin="10,0,0,0"/>
                            <Image Margin="10" HorizontalOptions="End" Source="{Binding IsExpanded,Source={x:Reference expander1},Converter={StaticResource ExpanderIconConverter}}"/>
                        </Grid>
                    </syncfusion:SfExpander.Header>
                    <syncfusion:SfExpander.Content>
                        <Grid Padding="10,10,10,10" BackgroundColor="#FFFFFF">
                            <Label BackgroundColor="#FFFFFF" HeightRequest="50" Text="Veg pizza is prepared with the items that meet vegetarian standards by not including any meat or animal tissue products." TextColor="#303030" VerticalTextAlignment="Center"/>
                        </Grid>
                    </syncfusion:SfExpander.Content>
                </syncfusion:SfExpander>
            </StackLayout>
        </ScrollView>
    </ContentPage.Content>
</ContentPage>
```

**C#**

Return image based on the **IsExpanded** property value.

``` c#
namespace ExpanderXamarin
{
    public class ExpanderIconConverter : IValueConverter
    {
        public object Convert(object value, Type targetType, object parameter, CultureInfo culture)
        {
            if ((bool)value)
                return ImageSource.FromResource("ExpanderXamarin.Images.ArrowDown.png");
            else
                return ImageSource.FromResource("ExpanderXamarin.Images.ArrowUp.png");
        }
 
        public object ConvertBack(object value, Type targetType, object parameter, CultureInfo culture)
        {
            throw new NotImplementedException();
        }
    }
}
```

**Output**

![HeaderIconCustomization](https://github.com/SyncfusionExamples/expander-header-icon-customization-xamarin/blob/master/ScreenShots/HeaderIconCustomization.png)
