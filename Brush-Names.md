Sometimes you may want to use the toolkit's brush names directly in your XAML.  Typically you'll use them as dynamic resources, so the update with the current material palette.

# Palette Brush Names

## Primary Colour

* PrimaryHueLightBrush
* PrimaryHueLightForegroundBrush
* PrimaryHueMidBrush
* PrimaryHueMidForegroundBrush
* PrimaryHueDarkBrush
* PrimaryHueDarkForegroundBrush

NB.  *[Light/Mid/Dark]Brush brushes define the different hues of the primary colour, and the *[Light/Mid/Dark]ForegroundBrush define a foreground colour which will show up clearly on that hue.

## Accent Colour

* SecondaryAccentBrush
* SecondaryAccentForegroundBrush

## Example Usage

```<TextBlock Foreground="{DynamicResource PrimaryHueMidBrush}" />```

# Light/Dark Specific Brush Names

* MaterialDesignBackground
* MaterialDesignPaper
* MaterialDesignBody
* MaterialDesignBodyLight
* MaterialDesignColumnHeader
* MaterialDesignCheckBoxOff
* MaterialDesignCheckBoxDisabled
* MaterialDesignTextBoxBorder
* MaterialDesignDivider
* MaterialDesignSelection
* MaterialDesignFlatButtonClick
* MaterialDesignFlatButtonRipple
* MaterialDesignToolTipBackground
* MaterialDesignChipBackground

