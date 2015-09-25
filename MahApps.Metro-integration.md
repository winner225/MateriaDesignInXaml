# MahApps.Metro integration
While the Metro UI itself does not integrate nicely with Google's guidelines, MahApps.Metro contains the MetroWindow, which has new looks and functionality that can be quite handy for Material Design.

## The Basics
First, you'll need to import MahApps.Metro into your project. A more detailed guide can be found in [MahApps' repository](https://github.com/MahApps/MahApps.Metro), but we will provide a quick overview as reference.

1. Install the [NuGet Package](https://www.nuget.org/packages/MahApps.Metro)
2. Merge the dictionaries in your App.xaml (Choose either BaseLight or BaseDark, accent color will be overwritten by Material Design's later, so it does not matter)

    ```xml
    <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Controls.xaml" />
    <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Fonts.xaml" />
    <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Colors.xaml" />
    <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Accents/BaseLight.xaml" />
    ```
3. Change all your windows to MetroWindows, with your preferred settings

    ```xml
    <metro:MetroWindow [...]
                       xmlns:metro="http://metro.mahapps.com/winfx/xaml/controls"
                       GlowBrush="{DynamicResource AccentColorBrush}"
                       BorderThickness="1"
                       [...]>
    ```

## The Colors
First of all, remove any Accent **Color** you've imported from MahApps' ```Styles/Accents/``` folder (*Not the BaseLight/BaseDark file!*), because it will be completly overwritten. If you look into one of those files, you'll see that 24 items are defined: 6  'helper' colors and 18 brushes. Although all brushes are defined in function of the colors, XAML doesn't have support for 'resource copying': you can't just redefine the 'helper' colors as previously defined Material Design colors and be done with it, you'll need to manually substitute the 'Color' attribute of each Brush.

If you are using the Swatches provided by the Toolkit, here are the recommended substitutions:
* `HighlightColor`: Primary 700
* `AccentColor`: Primary 500
* `AccentColor2`: Primary 400
* `AccentColor3`: Primary 300
* `AccentColor4`: Primary 200
* `IdealForegroundColor`: Primary 500 Foreground

Here's what the substitution looks like using non-named Swatches:
```xml
<SolidColorBrush x:Key="HighlightBrush" Color="{StaticResource Primary700}" />
<SolidColorBrush x:Key="AccentColorBrush" Color="{StaticResource Primary500}" />
<SolidColorBrush x:Key="AccentColorBrush2" Color="{StaticResource Primary400}" />
<SolidColorBrush x:Key="AccentColorBrush3" Color="{StaticResource Primary300}" />
<SolidColorBrush x:Key="AccentColorBrush4" Color="{StaticResource Primary200}" />
<SolidColorBrush x:Key="WindowTitleColorBrush" Color="{StaticResource Primary700}" />
<SolidColorBrush x:Key="AccentSelectedColorBrush" Color="{StaticResource Primary500Foreground}" />
<LinearGradientBrush x:Key="ProgressBrush" EndPoint="0.001,0.5" StartPoint="1.002,0.5" >
    <GradientStop Color="{StaticResource Primary700}" Offset="0" />
    <GradientStop Color="{StaticResource Primary300}" Offset="1" />
</LinearGradientBrush>
<SolidColorBrush x:Key="CheckmarkFill" Color="{StaticResource Primary500}" />
<SolidColorBrush x:Key="RightArrowFill" Color="{StaticResource Primary500}" />
<SolidColorBrush x:Key="IdealForegroundColorBrush" Color="{StaticResource Primary500Foreground}" />
<SolidColorBrush x:Key="IdealForegroundDisabledBrush" Color="{StaticResource Primary500}" Opacity="0.4" />
```

## The Fonts
By default Metro uses Segoe UI for all its controls. If you want to make them look more consistent, you'll need to override the Font Families defined in `/Styles/Fonts.xaml` with the direct path to the Roboto font file. 
(*Note*: Unlike the Accent colors, Font.xaml contains extra definitions that do not need to be overwritten. As such, don't remove its merged resource dictionary.)

```xml
<FontFamily x:Key="DefaultFont">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
<FontFamily x:Key="HeaderFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
<FontFamily x:Key="ContentFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
<FontFamily x:Key="ToggleSwitchFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
<FontFamily x:Key="ToggleSwitchHeaderFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
```

## The Dialogs
Using MetroWindow's dialogs with the Toolkit is very easy: the only difference is some extra settings to override the styles of the controls inside the dialog.

First, create a ResourceDictionary that points to the file designed to override dialogs' controls:

```C#
var dictionary = new ResourceDictionary();
dictionary.Source = new System.Uri(@"pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.MahApps.Dialogs.xaml");
```

Then, just change the following properties in the `MetroDialogSettings` that will be sent to the dialog:
```C#
settings.SuppressDefaultResources = true;
settings.CustomResourceDictionary = dictionary;
```

### Known Issues
* **Progress Dialog:** The 'negative button' in this dialog cannot be styled, it will always use the default Metro style. This is most likely a bug in MahMapps itself.
* **Login Dialog:** `UsernameWatermark` and `PasswordWatermark` have no effect when Material Design styles are used. Setting `EnablePasswordPreview` to true reverts the Password Textbox back to the default Metro style.

## App.xaml example
Here's an example app.xaml, using Blue as the primary color and Lime as the accent color:

```xml
<Application x:Class="MaterialTest.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:MaterialTest"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            
            <ResourceDictionary.MergedDictionaries>
                
                <!-- MahApps -->
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Controls.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Fonts.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Colors.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Accents/BaseLight.xaml" />

                <!-- Material -->
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Light.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Blue.Named.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Lime.Named.xaml" />
                
            </ResourceDictionary.MergedDictionaries>

            <!-- Material Brushes -->
            <SolidColorBrush x:Key="PrimaryHueLightBrush" Color="{StaticResource BluePrimary200}"/>
            <SolidColorBrush x:Key="PrimaryHueLightForegroundBrush" Color="{StaticResource BluePrimary200Foreground}"/>
            <SolidColorBrush x:Key="PrimaryHueMidBrush" Color="{StaticResource BluePrimary500}"/>
            <SolidColorBrush x:Key="PrimaryHueMidForegroundBrush" Color="{StaticResource BluePrimary500Foreground}"/>
            <SolidColorBrush x:Key="PrimaryHueDarkBrush" Color="{StaticResource BluePrimary700}"/>
            <SolidColorBrush x:Key="PrimaryHueDarkForegroundBrush" Color="{StaticResource BluePrimary700Foreground}"/>
            <SolidColorBrush x:Key="SecondaryAccentBrush" Color="{StaticResource LimeAccent700}"/>
            <SolidColorBrush x:Key="SecondaryAccentForegroundBrush" Color="{StaticResource LimeAccent700Foreground}"/>

            <!-- MahApps Brushes -->
            <SolidColorBrush x:Key="HighlightBrush" Color="{StaticResource BluePrimary700}"/>            
            <SolidColorBrush x:Key="AccentColorBrush" Color="{StaticResource BluePrimary500}"/>
            <SolidColorBrush x:Key="AccentColorBrush2" Color="{StaticResource BluePrimary400}"/>
            <SolidColorBrush x:Key="AccentColorBrush3" Color="{StaticResource BluePrimary300}"/>
            <SolidColorBrush x:Key="AccentColorBrush4" Color="{StaticResource BluePrimary200}"/>            
            <SolidColorBrush x:Key="WindowTitleColorBrush" Color="{StaticResource BluePrimary700}"/>
            <SolidColorBrush x:Key="AccentSelectedColorBrush" Color="{StaticResource BluePrimary500Foreground}"/>
            <LinearGradientBrush x:Key="ProgressBrush" EndPoint="0.001,0.5" StartPoint="1.002,0.5">
                <GradientStop Color="{StaticResource BluePrimary700}" Offset="0"/>
                <GradientStop Color="{StaticResource BluePrimary300}" Offset="1"/>
            </LinearGradientBrush>
            <SolidColorBrush x:Key="CheckmarkFill" Color="{StaticResource BluePrimary500}"/>
            <SolidColorBrush x:Key="RightArrowFill" Color="{StaticResource BluePrimary500}"/>            
            <SolidColorBrush x:Key="IdealForegroundColorBrush" Color="{StaticResource BluePrimary500Foreground}"/>
            <SolidColorBrush x:Key="IdealForegroundDisabledBrush" Color="{StaticResource BluePrimary500}" Opacity="0.4"/>

            <!-- MahApps Fonts -->
            <FontFamily x:Key="DefaultFont">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
            <FontFamily x:Key="HeaderFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
            <FontFamily x:Key="ContentFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
            <FontFamily x:Key="ToggleSwitchFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>
            <FontFamily x:Key="ToggleSwitchHeaderFontFamily">pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto</FontFamily>

        </ResourceDictionary>
    </Application.Resources>
</Application>
```