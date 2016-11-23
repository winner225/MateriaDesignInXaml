- Start new WPF project
- Install _MaterialDesignThemes_ nuget: ``` Install-Package MaterialDesignThemes ```
- Edit App.xaml to following:

```
<Application . . . >
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

- Edit MainWindow.xaml to following:
```
<Window . . .
        xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes"
        TextElement.Foreground="{DynamicResource MaterialDesignBody}"
        TextElement.FontWeight="Regular"
        TextElement.FontSize="13"
        TextOptions.TextFormattingMode="Ideal" 
        TextOptions.TextRenderingMode="Auto"        
        Background="{DynamicResource MaterialDesignPaper}"
        FontFamily="{DynamicResource MaterialDesignFont}">
    <Grid>
        <materialDesign:Card Padding="32" Margin="16">
            <TextBlock Style="{DynamicResource MaterialDesignTitleTextBlock}">My First Material Design App</TextBlock>
        </materialDesign:Card>
    </Grid>
</Window>
```
- Hit F5, voila!

![](https://raw.githubusercontent.com/ButchersBoy/MaterialDesignInXamlToolkit/master/web/images/wikiscreen-quickstart.png)

