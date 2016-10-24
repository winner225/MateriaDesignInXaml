# SNACKBAR NOT YET AVAILABLE,  COMING SOON!
The simplest forms of snackbar usage are:

```
<materialDesign:Snackbar Message="Hello World" IsActive="True" />

<materialDesign:Snackbar IsActive="{Binding IsActive}">
    <materialDesign:SnackbarMessage Content="Deleted Item" ActionContent="UNDO" ActionCommand="{Binding UndoCommand}" />
</materialDesign:Snackbar>
```
However, in a real world scenario this usage isn't going to work.  With a visual notification system such as the snackbar various things have to be taken into account:

* Displaying messages for a set period
* Having different callbacks (or commands) for different messages
* Queuing messages, and receiving from different threads
* Discarding duplicates received in quick succession
* Keeping messages active due to events such as mouse over or dialog displaying over the top

To assist with all of the above challenges a ``` SnackbarMessageQueue ``` is provided. 

There is shorthand to setup a message queue, typically if you are a using code-behind development style you might use this syntax:

```
<materialDesign:Snackbar MessageQueue="{materialDesign:MessageQueue}" />
```
Or in an MVVM scenario you might use a binding:
```
<materialDesign:Snackbar MessageQueue="{Binding MyMessageQueue}" />
```
The ``` SnackbarMessageQueue ``` implements ``` ISnackbarMessageQueue ``` so you could create the queue near application startup and inject down into your view models via the interface.

You can queue messages **from any thread**:
```
snackbarMessageQueue.Enqueue("Wow, easy!");
```
And you can arrange for action callbacks:
```
snackbarMessageQueue.Enqueue("Item 1 Deleted", "UNDO", () => HandleUndoMethod());
snackbarMessageQueue.Enqueue($"Item {id} Deleted", "UNDO", undoId => HandleUndoMethod(undoId), id);
```

**Note** that although you can queue messages from any thread, you can only access ``` Snackbar.MessageQueue ``` from the Dispatcher.

If you assign a message queue to a DialogHost, if a snackbar notification displays whilst a dialog is being shown, the display period will extend so the user does not miss the notification.  So a basic application setup might look like:
```
<materialDesign:DialogHost SnackbarMessageQueue="{Binding ElementName=MySnackbar, Path=MessageQueue}">
    <Grid>
        <!-- app content here -->
        <materialDesign:Snackbar x:Name="MySnackbar" MessageQueue="{materialDesign:MessageQueue}" />
    </Grid>
</materialDesign:DialogHost>
```

