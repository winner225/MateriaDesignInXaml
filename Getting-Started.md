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

Your App.xaml should be looking something like this for now:
```xml
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
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

If you open your project now, you'll notice the components work but lack color. This will be remedied in the next section,

### The Colors

In Material Design, two 'palettes' need to be defined: Primary and Accent. To make your life easier, the Toolkit includes all of [Google's swatches](https://www.google.com/design/spec/style/color.html#color-color-palette) and their recommended palettes built in and ready to be used! They are contained in the MaterialDesignColors project, which is imported automatically as a dependency when you install the main NuGet package. 

In this section, we'll use the recommended palettes to define our application's colors, since they're the easiest way to do it and also the most common. If you'd like to hear more about Swatches, how they work, and how to define your own, head over to the [[Swatches]] page.

The recommended palettes live in ```/Themes/Recommended/Accent/MaterialDesignColor.COLOR_NAME.xaml``` and ```/Themes/Recommended/Primary/MaterialDesignColor.COLOR_NAME.xaml```, inside the *MaterialDesignColors* project, where *COLOR_NAME* is the name of the color swatch as defined in [Google's guide](https://www.google.com/design/spec/style/color.html#color-color-palette), without spaces (So *Deep Purple* becomes *DeepPurple*). Please note that not all swatches have Primary and Accent colors. So see which ones are available, consult Google's guide or the project's [Accent](/tree/master/MaterialDesignColors.Wpf/Themes/Recommended/Accent) and [Primary](/tree/master/MaterialDesignColors.Wpf/Themes/Recommended/Primary) folders.

Now, let's get to the code. Importing them is very similar to how you imported other resources earlier, just with a change to the project:

```xml
<ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Primary/MaterialDesignColor.COLOR_NAME.xaml" />
<ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Accent/MaterialDesignColor.COLOR_NAME.xaml" />
```

So, if you wanted to use Deep Purple as your primary color and Lime as your secondary, your app.xaml would look something like this right now:

```xml
<Application x:Class="MaterialTest.App"
             xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
             xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
             StartupUri="MainWindow.xaml">
    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>

                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Light.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignThemes.Wpf;component/Themes/MaterialDesignTheme.Defaults.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Primary/MaterialDesignColor.DeepPurple.xaml" />
                <ResourceDictionary Source="pack://application:,,,/MaterialDesignColors;component/Themes/Recommended/Accent/MaterialDesignColor.Lime.xaml" />

            </ResourceDictionary.MergedDictionaries>            
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

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
If you also want to use MahApps.Metro in your project, check out the [[MahApps.Metro integration]] page.

# Aftermath
Now that you're all set to stun your users with modern and beautiful applications, you should take a look at the [Toolkit's Demo](https://github.com/ButchersBoy/MaterialDesignInXamlToolkit/tree/master/MainDemo.Wpf) to learn how to properly use components and styles, or at the [Mash Up Demo](https://github.com/ButchersBoy/MaterialDesignInXamlToolkit/tree/master/MahMaterialDragablzMashUp) to see how to integrate Material Design, MahApps, and Dragablz for a truly modern application.