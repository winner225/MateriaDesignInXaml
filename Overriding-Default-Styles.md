If you are not happy with the default styles you can easily override them. Just create a resource dictionary with a new style using the **same key** as the style you want to override. Make sure you put the original style in the `BaseOn` attribute. 

Example of `MaterialDesignThemes.Overrides.xaml`:

```
<ResourceDictionary xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
                    xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"                                     
                    xmlns:materialDesign="clr-namespace:MaterialDesignThemes.Wpf;assembly=MaterialDesignThemes.Wpf">
    
    <Style x:Key="MaterialDesignFloatingHintTextBox" BasedOn="{StaticResource MaterialDesignFloatingHintTextBox}" TargetType="{x:Type TextBox}">
        <Setter Property="FontSize" Value="24" />
        <Setter Property="materialDesign:HintAssist.FloatingScale" Value="0.6" />
        <Setter Property="materialDesign:HintAssist.FloatingOffset" Value="1,-20" />
    </Style>

</ResourceDictionary>     
```

As you are overriding default styles you probably want to merge your new default styles into your App.xaml resources. That would look something like this:

```
<Application x:Class="MaterialTest.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:MaterialTest"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Light.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" /> 

                <ResourceDictionary Source="pack://application:,,,/Your.Assembly;component/Themes/MaterialDesignTheme.Overrides.xaml" />
                                
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```
