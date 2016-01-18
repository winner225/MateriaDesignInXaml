***

**Please Note:** *The MaterialDesignThemes.MahApps project is contained in [its own NuGet package](https://www.nuget.org/packages/MaterialDesignThemes.MahApps), which must be downloaded separatedly. (```Install-Package MaterialDesignThemes.MahApps```)*


***

While the Metro UI itself does not integrate nicely with Google's guidelines, MahApps.Metro contains the MetroWindow, which has new looks and functionality that can be quite handy for Material Design. The Toolkit has a built-in support for MahApps, which resides in the *MaterialDesignThemes.MahApps* project.

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

If you are using the Swatches or Recommended colors provided by the Toolkit, here are the proper substitutions:
* `HighlightColor` => `Primary700`
* `AccentColor` => `Primary500`
* `AccentColor2` => `Primary400`
* `AccentColor3` => `Primary300`
* `AccentColor4` => `Primary200`
* `IdealForegroundColor` => `Primary500Foreground`

Here's what the substitution looks like:
```xml
<SolidColorBrush x:Key="HighlightBrush" Color="{DynamicResource Primary700}"/>
<SolidColorBrush x:Key="AccentColorBrush" Color="{DynamicResource Primary500}"/>
<SolidColorBrush x:Key="AccentColorBrush2" Color="{DynamicResource Primary400}"/>
<SolidColorBrush x:Key="AccentColorBrush3" Color="{DynamicResource Primary300}"/>
<SolidColorBrush x:Key="AccentColorBrush4" Color="{DynamicResource Primary200}"/>
<SolidColorBrush x:Key="WindowTitleColorBrush" Color="{DynamicResource Primary700}"/>
<SolidColorBrush x:Key="AccentSelectedColorBrush" Color="{DynamicResource Primary500Foreground}"/>
<LinearGradientBrush x:Key="ProgressBrush" EndPoint="0.001,0.5" StartPoint="1.002,0.5">
    <GradientStop Color="{DynamicResource Primary700}" Offset="0"/>
    <GradientStop Color="{DynamicResource Primary300}" Offset="1"/>
</LinearGradientBrush>
<SolidColorBrush x:Key="CheckmarkFill" Color="{DynamicResource Primary500}"/>
<SolidColorBrush x:Key="RightArrowFill" Color="{DynamicResource Primary500}"/>
<SolidColorBrush x:Key="IdealForegroundColorBrush" Color="{DynamicResource Primary500Foreground}"/>
<SolidColorBrush x:Key="IdealForegroundDisabledBrush" Color="{DynamicResource Primary500}" Opacity="0.4"/>
```

## The Fonts
Metro uses Segoe UI, Material uses Roboto. To override MahApps' fonts with Roboto, import the following file:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.MahApps;component/Themes/MaterialDesignTheme.MahApps.Fonts.xaml" />
```

## The Dialogs
Using MetroWindow's dialogs with the Toolkit is very easy: the only difference is some extra settings to override the styles of the controls inside the dialog.

First, create a ResourceDictionary that points to the file designed to override dialogs' controls:

```C#
var dictionary = new ResourceDictionary();
dictionary.Source = new Uri("pack://application:,,,/MaterialDesignThemes.MahApps;component/Themes/MaterialDesignTheme.MahApps.Dialogs.xaml");
```

Then, just change the following properties in the `MetroDialogSettings` that will be sent to the dialog:

```C#
settings.SuppressDefaultResources = true;
settings.CustomResourceDictionary = dictionary;
```

### Known Issues
* **Progress Dialog:** The 'negative button' in this dialog cannot be styled, it will always use the default Metro style. This is most likely a bug in MahMapps itself.
* **Login Dialog:** `UsernameWatermark` and `PasswordWatermark` have no effect when Material Design styles are used. Setting `EnablePasswordPreview` to true reverts the Password Textbox back to the default Metro style.

## The Flyouts
Similar to the Dialogs, they work just like in MahApps, you just need to override their look. But this time, it's even easier! You just need to import the following dictionary in your app.xaml and all Flyouts will use the new Material look:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.MahApps;component/Themes/MaterialDesignTheme.MahApps.Flyout.xaml" />
```

### Known Issues

When using a custom background brush on a flyout where the close button and title are collapsed, you are limited to using a color from your Material Design palette.

The brush used for the `Background` property must be of the same color as the `ColorZoneMode` used for the header:

```
<Controls:Flyout Position="Bottom"
                 CloseButtonVisibility="Collapsed"
                 TitleVisibility="Collapsed"
                 Background="{DynamicResource PrimaryHueLightBrush"
                 mahApps:FlyoutAssist.HeaderColorMode="PrimaryLight"
                 >
                <TextBlock>Some content</TextBlock>
</Controls:Flyout>
```
## The Palette Helper

If you plan on using the Toolkit's Palette Helper to switch colors dynamically during run-time, you need to add an extra paremeter to every *ReplacePrimaryColor* call, to properly change MahApps' brushes. For example:

```C#
helper.ReplacePrimaryColor(swatch, true)
```

## The App.xaml
Here's an example app.xaml, using Blue as the primary color and Lime as the accent color:

```xml
<Application x:Class="MaterialMahApps.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>

            <ResourceDictionary.MergedDictionaries>

                <!-- MahApps -->
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Controls.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Fonts.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Colors.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MahApps.Metro;component/Styles/Accents/BaseLight.xaml" />

                <!-- Material Design -->
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Light.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Primary/MaterialDesignColor.DeepPurple.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Accent/MaterialDesignColor.Lime.xaml" />                

                <!-- Material Design: MahApps Compatibility -->
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.MahApps;component/Themes/MaterialDesignTheme.MahApps.Fonts.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.MahApps;component/Themes/MaterialDesignTheme.MahApps.Flyout.xaml" />

            </ResourceDictionary.MergedDictionaries>

            <!-- MahApps Brushes -->
            <SolidColorBrush x:Key="HighlightBrush" Color="{DynamicResource Primary700}"/>
            <SolidColorBrush x:Key="AccentColorBrush" Color="{DynamicResource Primary500}"/>
            <SolidColorBrush x:Key="AccentColorBrush2" Color="{DynamicResource Primary400}"/>
            <SolidColorBrush x:Key="AccentColorBrush3" Color="{DynamicResource Primary300}"/>
            <SolidColorBrush x:Key="AccentColorBrush4" Color="{DynamicResource Primary200}"/>
            <SolidColorBrush x:Key="WindowTitleColorBrush" Color="{DynamicResource Primary700}"/>
            <SolidColorBrush x:Key="AccentSelectedColorBrush" Color="{DynamicResource Primary500Foreground}"/>
            <LinearGradientBrush x:Key="ProgressBrush" EndPoint="0.001,0.5" StartPoint="1.002,0.5">
                <GradientStop Color="{DynamicResource Primary700}" Offset="0"/>
                <GradientStop Color="{DynamicResource Primary300}" Offset="1"/>
            </LinearGradientBrush>
            <SolidColorBrush x:Key="CheckmarkFill" Color="{DynamicResource Primary500}"/>
            <SolidColorBrush x:Key="RightArrowFill" Color="{DynamicResource Primary500}"/>
            <SolidColorBrush x:Key="IdealForegroundColorBrush" Color="{DynamicResource Primary500Foreground}"/>
            <SolidColorBrush x:Key="IdealForegroundDisabledBrush" Color="{DynamicResource Primary500}" Opacity="0.4"/>

        </ResourceDictionary>
    </Application.Resources>
</Application>
```