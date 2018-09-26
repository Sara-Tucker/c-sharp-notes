# WPF

[Great YouTube series](https://www.youtube.com/watch?v=Vjldip84CXQ&list=PLrW43fNmjaQVYF4zgsD0oL9Iv6u23PI6M)

<br>

[Designer vs Blend](https://docs.microsoft.com/en-us/visualstudio/designers/designing-xaml-in-visual-studio?view=vs-2017)  
[XAML Overview](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-overview-wpf)  
[DataGrid (and use from SQL server)](https://docs.microsoft.com/en-us/dotnet/framework/wpf/controls/datagrid#related-topics)  
[WPF with EF](https://docs.microsoft.com/en-us/visualstudio/data-tools/create-a-simple-data-application-with-wpf-and-entity-framework-6?view=vs-2017)

<br>

XAML is a markup language. You can create visible UI elements in the declarative XAML markup, and then separate the UI definition from the run-time logic by using code-behind files, joined to the markup through partial class definitions. XAML directly represents the instantiation of objects.

When you specify an object element tag, you create a new instance of that class. `<ObjectElement/>`

The location of the XAML code-behind file for a XAML file is identified by specifying a namespace and class as the x:Class attribute of the root element of the XAML.

<br>
<br>

#### Routed events
A particular event feature that is fundamental to WPF is a routed event. Routed events enable an element to handle an event that was raised by a different element, as long as the elements are connected through a tree relationship.

<br>

#### Naming "elements"
- Use the `Name=""` property
- If you cannot find a Name property use `x:Name=""` instead

<br>
<br>
<br>
<br>

Margin = Outside  
Padding = Inside

<br>

#### Border
Put everything inside a border with padding.
```xaml
<Border Padding ="10">

<Border/>
```

<br>

There are two main container controls used for layout: StackPanel and Grid.

<br>

#### Stack Panel
Arranges child elements vertically or horizontally into a single straight stack and automatically sizes controls so they use only the space that they need and no more.
```xaml
<Border Padding ="10">
    <StackPanel>

    <StackPanel/>
<Border/>
```

<br>

#### Grid
For layouts other than a straight stack, like two columns, use a Grid. Grids use ColumnDefinition and RowDefinition classes to define columns and rows. Then use the Grid.Column="#" and Grid.Row="#" properties for the child elements.
```xaml
<Border Padding ="10">
    <StackPanel>
        <!-- Buttons -->
        <Grid>
            <Grid.ColumnDefinitions>
                <ColumnDefinition Width="2*" />
                <ColumnDefinition Width="*" />
                <ColumnDefinition Width="*" />
            </Grid.ColumnDefinitions>

            <Button x:Name="ApplyButton" Click="ApplyButton_OnClick" Margin="0 0 10 0" Grid.Column="0" Content="Apply"/>
            <Button x:Name="ResetButton" Click="ResetButton_OnClick" Grid.Column="1" Content="Reset"/>
            <Button Margin="10 0 0 0" Grid.Column="2" Content="Refresh"/>
        </Grid>
    <StackPanel/>
<Border/>
```

<br>

#### Other
```xaml
<!-- TextBlock: Use for text. -->
<TextBlock Text="Part Properties" FontWeight="Bold" Margin="0 10"/>

<!-- TextBox: Use for input. -->
<TextBox x:Name="InputText" Padding="2"/>
```

<br>
<br>
<br>

## Open a Window
The first Window that is opened is the apps main window. The Startup event handler opens the main window.
```XAML
<Application
  xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
  xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
  x:Class="Sample.AppName" 
  Startup="App_Startup" />
```
```C#
using System.Windows;

namespace Sample
{
    public partial class AppName : Application
    {
        void App_Startup(object sender, StartupEventArgs e)
        {
            // Open a window
            MyWindow window = new MyWindow();
            window.Show();
        }
    }
}
```
The first Window to be instantiated in a standalone application becomes the main application window by default. This Window object is referenced by the Application.MainWindow property. The value of the MainWindow property can be changed programmatically if a different window than the first instantiated Window should be the main window.

<br>
<br>

## Window
The implementation of a typical window comprises both appearance and behavior, where appearance defines how a window looks to users and behavior defines the way a window functions as users interact with it.

<br>

#### Window Ownership
A window that is opened by using the Show method does not have an implicit relationship with the window that created it; users can interact with either window independently of the other.

Windows should always close, minimize, maximize, and restore in concert with the window that created them. Such a relationship can be established by making one window own another, and is achieved by setting the Owner property of the owned window with a reference to the owner window. This is shown in the following example.
```c#
// Create a window and make this window its owner
Window ownedWindow = new Window();
ownedWindow.Owner = this;
ownedWindow.Show();
```
 After ownership is established:
- The owned window can reference its owner window by inspecting the value of its Owner property.
- The owner window can discover all the windows it owns by inspecting the value of its OwnedWindows property.

<br>

#### Preventing Window Activation
There are scenarios where windows should not be brought to the front or the active Window when shown, such as conversation windows of a messenger app or notification windows of an email app.

If your application has a window that shouldn't be activated when shown, you can set its ShowActivated property to false before calling the Show method for the first time so that the currently activated window remains activated.

<br>

## Controls
Controls are common UI components such as Button, Label, TextBox, etc.  
[List of Controls](https://docs.microsoft.com/en-us/visualstudio/designers/introduction-to-wpf?view=vs-2017#wpf-controls-by-function)

Sender is the object that called the function.
```c#
void Control_Event(object sender, RoutedEventArgs e)
{
    this.Control.Property = ((ControlType)sender).Property;
}
```

<br>

## Data binding
https://docs.microsoft.com/en-us/dotnet/framework/wpf/data/data-binding-overview

