Illustration of how to configure your App.xaml in version 1.0 of the toolkit.  A simpler mechanism is available for 1.1, but 1.1 is currently under development.

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
                        <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Indigo.xaml" />
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
                        <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Yellow.xaml" />
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