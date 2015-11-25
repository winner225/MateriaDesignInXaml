_[refers to pre-release version]_

This library relies heavily on animation but it may be necessary to reduce the animation burden, for example when running on resource constrained hardware.

These techniques can help:

#### Timeline.DesiredFrameRateProperty

WPF allows you reduce the Timeline (Storyboard) frame-rate (from the default of 60):

```Timeline.DesiredFrameRateProperty.OverrideMetadata(typeof(Timeline), new FrameworkPropertyMetadata { DefaultValue = 30 });```

#### TransitionAssist.DisableTransitions

The Material Design In XAML Toolkit library itself provides means to turn off transitions (where supported) via an attached property:

```materialDesign:TransitionAssist.DisableTransitions="True" ```

This is an inheriting property, so you could turn off all (supported) transitions at Window (or UserControl) level:

```
<Window xmlns:materialDesign="http://materialdesigninxaml.net/winfx/xaml/themes"
        materialDesign:TransitionAssist.DisableTransitions="True" />
```

Or you could manage this with more granularity on individual controls.

#### Current status of controls supporting ```.DisableTransitions```:

- [x] DialogHost
- [x] Drawer
- [ ] Clock
- [ ] Underline

