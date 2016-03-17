The transitions part of Material Design In XAML Toolkit seeks to make attractive animations easily achievable for any XAML programmer/designer.  They hide the complexities of storyboards, and wrap up some more complex animations, and are combinable, to help achieve a multitude of effects quickly.  For the adventurous, the API is extendible, and animations can still be combined with classic XAML storyboards/animations.

There are a couple of core classes which can be used from XAML.  The ```Transitioner``` and ```TransitioningContent```.  Use them, and combine them, setting effects on them, to piece together transitions as a user moves through the application.

# Transitioner

The transitioner is an ```ItemsControl```. Each item forms a slide.  The active slide is defined by the ```.SelectedIndex```

Imagine a simple wizard:

```
<materialDesign:Transitioner SelectedIndex="0">
    <WizardPageOne />
    <WizardPageTwo />
    <WizardPageThree />
</materialDesign:Transitioner>
```

The ```Transitioner``` will automatically wrap each wizard page in a ```TransitionerSlide``` Straight out of the box there will be a circle **wipe** going forwards through the wizard, and slide wipe going backwards.  You have more granular control by specifying the slide manually, where you can ass an additional opening **effect** (which will run in addition to the wipe):

```
<materialDesign:Transitioner SelectedIndex="0">
    <WizardPageOne />
    <materialDesign:TransitionerSlide OpeningEffect="{materialDesign:TransitionEffect FadeIn}">
        <WizardPageTwo />
    </materialDesign:TransitionerSlide>
    <materialDesign:TransitionerSlide OpeningEffect="{materialDesign:TransitionEffect FadeIn}">
        <WizardPageThree />
    </materialDesign:TransitionerSlide>
</materialDesign:Transitioner>
```

You can override wipes at the slide level:

```
<materialDesign:TransitionerSlide>
    <materialDesign:TransitionerSlide.BackwardWipe>
        <materialDesign:CircleWipe />
    </materialDesign:TransitionerSlide.BackwardWipe>
    <WizardPageTwo />
</materialDesign:TransitionerSlide>
```

## Navigation

Navigation is easy; as mentioned above you can change the ```Transitioner.SelectedIndex```, which may suit if you are using MVVM, or even code behind.  For convenience there are some routed commands available:

* Transitioner.MoveNextCommand
* Transitioner.MovePreviousCommand
* Transitioner.MoveFirstCommand
* Transitioner.MoveLastCommand

You could use these in your user control (e.g. inside WizardPageOne):

```
<Button Command="{x:Static materialDesign:Transitioner.MoveNextCommand}">
    NEXT
</Button>
```

# TransitioningContent

```TransitioningContent``` is a ```ContentControl``` enabling animations to be run on a UI element easily, typically when a control loads.  By combining with the ```Transitioner``` more complex animations can be created.  Usage is simple:

```
<materialDesign:TransitioningContent OpeningEffect="{materialDesign:TransitionEffect ExpandIn}">
    <TextBlock>Hello World</TextBlock>
</materialDesign:TransitioningContent>
```

Effects can be combined:
```
<materialDesign:TransitioningContent>
    <materialDesign:TransitioningContent.OpeningEffects>
        <materialDesign:TransitionEffect Kind="FadeIn" />
        <materialDesign:TransitionEffect Kind="SlideInFromBottom" />
    </materialDesign:TransitioningContent.OpeningEffects>
    <TextBlock>Hello World</TextBlock>
</materialDesign:TransitioningContent>
```

Effects can be delayed.  Using an items control, a great cascading effect can achieved but using a delay offset multiplier:

```
<ItemsControl>
    <materialDesign:TransitioningContent OpeningEffectsOffset="{materialDesign:IndexedItemOffsetMultiplier 0:0:0.05}">
        <materialDesign:TransitioningContent.OpeningEffects>
            <materialDesign:TransitionEffect Kind="SlideInFromLeft" />
        </materialDesign:TransitioningContent.OpeningEffects>
        <TextBlock>Hello World</TextBlock>
    </materialDesign:TransitioningContent>
    . . .
    <!-- more items using same multipler -->
    . . .
</ItemsControl>
```

