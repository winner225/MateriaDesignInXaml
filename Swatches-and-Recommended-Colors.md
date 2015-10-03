All items here mentioned live in the *MaterialDesignColor* project(s).

**Naming Convetions:** 
* *LONG_COLOR_NAME* represents the color name as seen in [Google's guide][guide] (*Blue*, *Deep Purple*, *Red*, *Light Blue*, etc). 
* *SHORT_COLOR_NAME* represents the color name without spaces (*Blue*, *DeepPurple*, *Red*, *LightBlue*, etc).

## Essential Resources

First, we need to understand *Essential Resources*. They are a few resources that must be defined: The Toolkit will assume they always exist. They consist of 6 Primary Brushes, 2 Accent/Secondary Brushes, and a complete swatch set of Primary colors and Accent colors.

* **Primary Brushes:** ```PrimaryHueLightBrush```, ```PrimaryHueLightForegroundBrush```, ```PrimaryHueMidBrush```, ```PrimaryHueMidForegroundBrush```, ```PrimaryHueDarkBrush```, ```PrimaryHueDarkForegroundBrush```.
* **Accent Brushes:** ```SecondaryAccentBrush```, ```SecondaryAccentForegroundBrush```.
* **(Unnamed) Primary Swatch:** ```PrimaryXXX``` and ```PrimaryXXXForeground```, where XXX is the intensity as seen in [Google's guide][guide] (100 through 900 in increments of 100, plus 50).
* **(Unnamed) Accent Swatch:** ```AccentXXX``` and ```AccentXXXForeground```, where XXX is the intensity as seen in [Google's guide][guide], without the starting 'A' (100, 200, 400, and 700).


## Swatches

**Swatches** are collections of related colors hand-picked to look nice together. There are currently three types of swatches:

1. **Unnamed:** These contain unnamed color definitions that will be overwritten in case more than one swatch of the same type is imported. Primary swatches contain ```PrimaryXXX``` and```PrimaryXXXForeground```, Accent swatches contain ```AccentXXX``` and ```AccentXXXForeground```; Where XXX is the color intensity as seen in [Google's guide][guide]. They are:
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.Primary.xaml
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.Accent.xaml
2. **Named:** These contain named color definitions that allow multiple swatches to be imported without overwriting each other. Primary swatches contain ```LONG_COLOR_NAMEPrimaryXXX``` and```LONG_COLOR_NAMEPrimaryXXXForeground```, Accent swatches contain ```LONG_COLOR_NAMEAccentXXX``` and ```LONG_COLOR_NAMEAccentXXXForeground```; Where XXX is the color intensity as seen in [Google's guide][guide]. They are:
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.Named.Primary.xaml
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.Named.Accent.xaml
3. **Legacy:** These are only here for backwards compatibility and can be removed without warning at any moment. Do *not* use these swatches. They are:
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.xaml
    * Themes\MaterialDesignColor.SHORT_COLOR_NAME.Named.xaml


## Recommended Colors

Defining the essential resources manually would be tedious and repetitive hard work. As such, the Recommended Colors are there to save the developer from unnecessary effort: They define the necessary brushes and import the proper swatches to make everything work just fine. 

There are two types of Recommended Colors, and one of each must be imported to make them work properly:

1. **Primary:** These will define the Primary Brushes and Primary Swatch. They are:
    * Themes\Recommended\Primary\MaterialDesignColor.SHORT_COLOR_NAME.xaml
2. **Accent:** These will define the Accent/Secondary Brushes and Accent/Secondary Swatch. They are:
    * Themes\Recommended\Accent\MaterialDesignColor.SHORT_COLOR_NAME.xaml


 [guide]:https://www.google.com/design/spec/style/color.html#color-color-palette