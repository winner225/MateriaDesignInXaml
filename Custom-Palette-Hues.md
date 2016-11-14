Illustration of advanced configuration of App.xaml which allows individual palette hues to be specified.

```xml
<Application x:Class="MaterialDesignColors.WpfExample.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:dragablz="clr-namespace:Dragablz;assembly=Dragablz"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <!-- primary color -->
                <ResourceDictionary>
                    <!-- include your primary palette -->
                    <ResourceDictionary.MergedDictionaries>
                        <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Indigo.Named.xaml" />
                    </ResourceDictionary.MergedDictionaries>
                    <!--
                            include three hues from the primary palette (and the associated forecolours).
                            Do not rename, keep in sequence; light to dark.
                        -->
                    <SolidColorBrush x:Key="PrimaryHueLightBrush" Color="{StaticResource Primary200}"/>
                    <SolidColorBrush x:Key="PrimaryHueLightForegroundBrush" Color="{StaticResource Primary200Foreground}"/>
                    <SolidColorBrush x:Key="PrimaryHueMidBrush" Color="{StaticResource Primary500}"/>
                    <SolidColorBrush x:Key="PrimaryHueMidForegroundBrush" Color="{StaticResource Primary500Foreground}"/>
                    <SolidColorBrush x:Key="PrimaryHueDarkBrush" Color="{StaticResource Primary700}"/>
                    <SolidColorBrush x:Key="PrimaryHueDarkForegroundBrush" Color="{StaticResource Primary700Foreground}"/>
                </ResourceDictionary>

                <!-- secondary colour -->
                <ResourceDictionary>
                    <!-- include your secondary pallette -->
                    <ResourceDictionary.MergedDictionaries>
                        <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Yellow.Named.xaml" />
                    </ResourceDictionary.MergedDictionaries>

                    <!-- include a single secondary accent color (and the associated forecolour) -->
                    <SolidColorBrush x:Key="SecondaryAccentBrush" Color="{StaticResource Accent200}"/>
                    <SolidColorBrush x:Key="SecondaryAccentForegroundBrush" Color="{StaticResource Accent200Foreground}"/>
                </ResourceDictionary>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

## Custom Colours

If you want to use completely non-standard brushes, just define them manually:

```xml
<Application x:Class="MaterialDesignColors.WpfExample.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:dragablz="clr-namespace:Dragablz;assembly=Dragablz"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
        	<!-- primary -->
            <SolidColorBrush x:Key="PrimaryHueLightBrush" Color="#744CE0"/>
            <SolidColorBrush x:Key="PrimaryHueLightForegroundBrush" Color="#FFFFFF"/>
            <SolidColorBrush x:Key="PrimaryHueMidBrush" Color="#6134D9"/>
            <SolidColorBrush x:Key="PrimaryHueMidForegroundBrush" Color="#FFFFFF"/>
            <SolidColorBrush x:Key="PrimaryHueDarkBrush" Color="#4D1DCF"/>
            <SolidColorBrush x:Key="PrimaryHueDarkForegroundBrush" Color="#FFFFFF"/>
            <!-- accent -->
            <SolidColorBrush x:Key="SecondaryAccentBrush" Color="#5C5B5E"/>
            <SolidColorBrush x:Key="SecondaryAccentForegroundBrush" Color="#FFFFFF"/>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

