# Getting Started

**Material Design in XAML Toolkit** consists of Material styles for existing components and completly new components that follow the Material Design logic. This article will guide you through the steps necessary to set-up Material Design in XAML Toolkit in your project.
 
## Installing the Toolkit

Before anything else, you must install the Toolkit. This can be done either manually or through the [NuGet package](https://www.nuget.org/packages/MaterialDesignThemes/) (```Install-Package MaterialDesignThemes```).
 
## Configuring your App.xaml

### The basics

Like any other XAML library, the Toolkit needs to be imported and configured through your project's App.xaml to function properly. First of all, you'll need to merge one of the themes (Dark or Light) into your resource dictionary. This can be accomplished by adding the following line inside your Resource Dictionary's Merged Dictionaries:
 
 * For the Light theme:
 ```xml
 <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Light.xaml" />
 ```
 
 * For the Dark theme:
 ```xml
 <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Dark.xaml" />
 ```


Then, you'll need to load the ```MaterialDesignTheme.Defaults.xaml``` file, which contains all of the component styles, with the following line:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" /> 
```

If you have chosen the Light theme, your App.xaml should be looking something like this for now:
```xml
<Application x:Class="MaterialTest.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             xmlns:local="clr-namespace:MaterialTest"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Dark.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" />                
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

If you open your project now, you'll notice the components work but lack color. This will be remedied in the next section,

### The Colors

Unlike other toolkits, Material Design in XAML leaves the color definitions up to its user. Eight SolidColorBrushes need to be defined: PrimaryHueLightBrush, PrimaryHueLightForegroundBrush, PrimaryHueMidBrush, PrimaryHueMidForegroundBrush, PrimaryHueDarkBrush, PrimaryHueDarkForegroundBrush, SecondaryAccentBrush, and SecondaryAccentForegroundBrush.

To make your life easier, the Toolkit includes several *Swatches*, which are collections of pre-designed color shades that can be used for your brushes. They come in two varieties and can be imported with the following lines:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.COLOR_NAME.xaml" />
```

Or

```xml
 <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.COLOR_NAME.Named.xaml" />
 ```
 
Where *COLOR_NAME* represents the name of the color swatch you want to import. For a list of all color names, check the [repository's Theme folder on GitHub](https://github.com/ButchersBoy/MaterialDesignInXamlToolkit/tree/master/Themes). Those swatches are based on [Google's Material Design style guide](http://www.google.com.br/design/spec/style/color.html#color-color-palette), and contain four 'sets' of StaticResource colors each: 
 
 * For the common swatches: PrimaryXXX, PrimaryXXXForeground, AccentXXX, AccentXXXForeground
 * For the named swatches: COLOR_NAMEPrimaryXXX, COLOR_NAMEPrimaryXXXForeground, COLOR_NAMEAccentXXX, COLOR_NAMEAccentXXXForeground.

Where XXX represents the intensity of the color, as displayed on [Google's guide](http://www.google.com.br/design/spec/style/color.html#color-color-palette). (*Note:* The Toolkit's swatches only contain intesities 50 through 900 for Primary colors and 100, 200, 400, and 700 for Accent/Secondary colors.). Notice how unnamed swatches will be ovewritten if multiple colors are imported, while named swatches won't.

When defining the necessary color brushes with swatches, it is customary to use intensity 200 for Primary Light, 500 for Primary Mid, 700 for Primary Dark, and 700 for Accent/Secondary. For example, if you wanted to use Deep Purple as your primary color and Lime as your accent color, you'd do the following:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.DeepPurple.Named.xaml" />
 <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/MaterialDesignColor.Lime.Named.xaml" />
                
 <ResourceDictionary>
     <SolidColorBrush x:Key="PrimaryHueLightBrush" Color="{StaticResource DeepPurplePrimary200}"/>
      <SolidColorBrush x:Key="PrimaryHueLightForegroundBrush" Color="{StaticResource DeepPurplePrimary200Foreground}"/>
      <SolidColorBrush x:Key="PrimaryHueMidBrush" Color="{StaticResource DeepPurplePrimary500}"/>
      <SolidColorBrush x:Key="PrimaryHueMidForegroundBrush" Color="{StaticResource DeepPurplePrimary500Foreground}"/>
      <SolidColorBrush x:Key="PrimaryHueDarkBrush" Color="{StaticResource DeepPurplePrimary700}"/>
      <SolidColorBrush x:Key="PrimaryHueDarkForegroundBrush" Color="{StaticResource DeepPurplePrimary700Foreground}"/>
      
      <SolidColorBrush x:Key="SecondaryAccentBrush" Color="{StaticResource LimeAccent700}"/>
      <SolidColorBrush x:Key="SecondaryAccentForegroundBrush" Color="{StaticResource LimeAccent700Foreground}"/>                    
  </ResourceDictionary>  
```

Please note that the usage of Swatches for the brushes is optional. They can be defined with custom colors if you wish to do so.

## Configuring your Window(s)
We're almost there! Now, all we need to do is configure our window to have Material Designs's look. There are no secrets here, you just need to add a few parameters to your Window's opening tag. The basic ones are:

```xml
<Window [...]
        TextElement.Foreground="{DynamicResource MaterialDesignBody}"
        Background="{DynamicResource MaterialDesignPaper}"
        [...] >
```

These will ensure the window uses Material Design colors, blending in nicely with the Toolkit's styles and components. However, for the full Material Design experience, you should use:

```xml
<Window [...]
        TextElement.Foreground="{DynamicResource MaterialDesignBody}"
        Background="{DynamicResource MaterialDesignPaper}"
        TextElement.FontWeight="Medium"
        TextElement.FontSize="14"
        FontFamily="pack://application:,,,/MaterialDesignThemes.Wpf;component/Resources/Roboto/#Roboto"
        [...] >
```

Now your window's text will also blend in nicely with Material Design.

## Summary
To use Material Design in XAML Toolkit, you'll need to install the package manually or through NuGet, import either the Light or Dark theme, import the Default file that contains all of the component's themes, define Eight SolidColorBrushes with colors of your preference, and configure your window to use Material Design's looks.

# Using the Toolkit with MahApps
This section is not complete yet. Please check later for progress.

# Aftermath
Now that you're all set to stun your users with modern and beautiful applications, you should take a look at the [Toolkit's Demo](https://github.com/ButchersBoy/MaterialDesignInXamlToolkit/tree/master/MainDemo.Wpf) to learn how to properly use components and styles, or at the [Mash Up Demo](https://github.com/ButchersBoy/MaterialDesignInXamlToolkit/tree/master/MahMaterialDragablzMashUp) to see how to integrate Material Design, MahApps, and Dragablz for a truly modern application.