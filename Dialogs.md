Dialogs in WPF have always been somewhat tricky.  The Material Design In XAML Toolkit's dialogs implementation is designed to:

* Provide correct styling
* Allow any dialog to be constructed
* Compatible with code-behind
* Compatible with MVVM
* Compatible with pure XAML
* Work in applications with multiple windows

Dialogs _are asynchronous_ so at some point you will have to deal with that in your code.

The cornerstone of dialogs the DialogHost control.  It’s a content control, meaning the underlying content over which the popup dialog will be displayed can be targeted; to a specific area of your app, or the entire Window content.

```
<md:DialogHost>
    <md:DialogHost.DialogContent>
        <dialogContent />
    </md:DialogHost.DialogContent>
    <mainContent />
</md:DialogHost>
```

When the dialog is open, the underlying content will be dimmed and disabled.

![](https://dragablz.files.wordpress.com/2015/10/materialdesigndialogs.png)

DialogHost.DialogContent (associated with DialogHost.DialogContentTemplate) is your typical XAML content object property for setting the content of your dialog.  You can infer from this that you can use MVVM to bind content, but **there are multiple ways of populating the content, showing the dialog, closing the dialog, and processing responses**, so here’s a list of all the strategies for using the dialog (after the gif):

![](https://dragablz.files.wordpress.com/2015/10/materialdesigndialog_s.gif)

# Open Dialog Strategies

## DialogHost.OpenDialogCommand

```
<Button Command="{x:Static md:DialogHost.OpenDialogCommand}" />
```

RoutedCommand typically used from a button where optional content can be provided via the CommandParameter.

## DialogHost.IsOpen

```
<md:DialogHost IsOpen="True" />
```

Dependency property, to be triggered from XAML, set from code-behind or via a binding.  Content must be set in DialogHost.DialogContent.

## DialogHost.Show

```
DialogHost.Show(viewOrModel);
```

Async/await based static API which can be used purely in code (for example from in a view model).  Content can be passed directly to the dialog.  Note that if you have multiple windows and multiple ``` DialogHost ``` instances you can set the ``` DialogHost.Identifier ``` property, and provide the identifier to the ``` .Show(...) ``` method to help find the required DialogHost.  

Where there are multiple possible dialog host instances, and alternative method to show the dialog at the correct window is to use the extension method:

## .Show() extension method

Extending both Window and DepedencyObject this method will try and locate the most apt DialogHost to display the dialog.

# Close Dialog Strategies

## DialogSession.Close()

Via any of the methods for handling the opened event, you can get hold of the dialog session.  This cn be used to close a dialog via code:

```
var result = await nearTo.ShowDialog(myControl, delegate(object sender, DialogOpenedEventArgs args)
{
    args.Session.Close(false);
});
```

## DialogHost.CloseDialogCommand

```
<Button Command="{x:Static md:DialogHost.CloseDialogCommand}" />
```

RoutedCommand, typically used on buttons inside the dialog, where the command parameter will be passed along to the dialog response.

## DialogHost.IsOpen

```
<md:DialogHost IsOpen="False" />
```

Dependency property, to be triggered from XAML, set from code-behind or via a binding.

# Handle Closing Event Strategies

The DialogClosingEventHandler delegate is key.  It provides the parameter provided to DialogHost.CloseDialogCommand, and allows the pending close to be cancelled.

The following mechanisms allow handling of this event, via code-behind, MVVM practices, or just from the code API:

## DialogHost.DialogClosing

```
<md:DialogHost DialogClosing="DialogHost_OnDialogClosing" />
```

Bubbling RoutedEvent, which could be used in code-behind.

## DialogHost.DialogClosingAttached

```
<Button Command="{x:Static wpf:DialogHost.OpenDialogCommand}" md:DialogHost.DialogClosingAttached="DialogHost_OnDialogClosing" />
```

Attached property, which accepts a DialogClosingEventHandler which makes it easy to subscribe to the closing event in a more localized area of XAML.

## DialogClosing.DialogClosingCallback

```
<md:DialogHost DialogClosingCallback="{Binding DialogClosingHandler}" />
```

Standard dependency property which enables the a DialogClosingEventHandler implementation to be bound in, typically from a view model.

## DialogHost.Show

```
var result = await DialogHost.Show(viewOrModel, ClosingEventHandler);
```

The async response from this method returns the parameter provided when DialogHost.CloseDialogCommand was executed.  As part of the Show() signature a DialogClosingEventHandler delegate can be provided to intercept the on-closing event, just prior to the close.

# More Examples

More complete usage examples can be found in MainDemo.Wpf which is part of the Toolkit solution, primarily in MainDemo.Wpf/Dialogs.xaml.