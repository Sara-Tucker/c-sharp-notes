# Caliburn.Micro
#### View -> Package Manager:
```Install-Package Caliburn.Micro```

<br>

#### Solution Explorer:
Delete MainWindow.  
Create folders: Models, Views, ViewModels

<br>

#### App.xaml.cs - need this??? don't do unless error.
```c#
public App()
{
    InitializeComponent();
}
```

<br>

#### App.xaml
```xaml
The app starts at App.xaml, App.xaml uses Bootstrapper for startup.
Remove StartupUri

    <Application.Resources>
        <ResourceDictionary>
            <ResourceDictionary.MergedDictionaries>
                <ResourceDictionary>
                    <local:Bootstrapper x:Key="Bootstrapper" />
                </ResourceDictionary>
            </ResourceDictionary.MergedDictionaries>
        </ResourceDictionary>
    </Application.Resources>
</Application>
```

<br>

#### Bootstrapper.cs
```c#
using Namespace.ViewModels;


    public class Bootstrapper : BootstrapperBase
    {
        public Bootstrapper()
        {
            Initialize();
        }

        // Overriding the OnStartup method from BootstrapperBase
        protected override void OnStartup(object sender, StartupEventArgs e)
        {
            // The startup View for the app will be the View for the specified ViewModel
            DisplayRootViewFor<ShellViewModel>();
        }
    }
```

<br>

#### Create your startup ViewModel and View - inherit from PropertyChangedBase??
```c#
// Inherit from Screen class which gives more control for opening/closing app
public class ShellViewModel : Screen
{
}
```

<br>
<br>
<br>
<br>
<br>

## Databinding
Automatically bind ViewModel properties to properties on controls with naming convention.

This will cause the “Text” property of the TextBox to be bound to the “FirstName” property on the ViewModel:
```xaml
<TextBox x:Name="FirstName" />

<!-- Explicitly -->
<TextBox Text="{Binding Path=FirstName, Mode=TwoWay}" />

<!-- Traditional way -->
<TextBlock Text="{Binding PROPERTYNAME}" />
```

<br>

Mode:
- OneWayToSource - data goes from the form to the property

<br>

NotifyOfPropertyChange:
```c#
set
{
    NotifyOfPropertyChange(() => Property/ControlName)
}
```
Rather than implementing INotifyPropertyChanged in all of your models, you can simply call the NotifyOfPropertyChange method within the setter of your properties.

<br>
<br>
<br>
<br>
<br>

## Bind events on controls to call methods on the ViewModel
Actions allow you to “bind” UI EventTriggers (like a Button's "Click" event) to methods on your View-Model.

When an EventTrigger occurs, it executes the specified method by creating, then sending, an ActionMessage.

You use a set of binding conventions around the ActionMessage feature. These conventions are based on x:Name. So, if you have a method called “Save” on your ViewModel and a Button named “Save” in your UI, we will automatically create an EventTrigger for the “Click” event and assign an ActionMessage for the “Save” method. Furthermore, we will inspect the method’s signature and properly construct the ActionMessage parameters.

<br>

#### Wiring Events
To wire events on controls to call methods on the ViewModel, give them the same name.

This will cause the Click event of the Button to call “Save” method on the ViewModel:
```xaml
<Button x:Name="Save">
```

<br>

#### cal:Message.Attach=""
Use the Message.Attach property to specify which event(s) to listen for, and which method should be called.
```xaml
<Button cal:Message.Attach="[Event Click] = [Action SayHello(Name.Text)]" />
```

<br>

If you leave out the event the parser will determine the default event to use for the trigger, for example a Button's Click. You can always be explicit of course.
```xaml
<Button cal:Message.Attach="SayHello(Name)" />
```
<br>
<br>
<br>

### Parameters
You can also pass parameters to the method as well. All parameters are automatically type converted.
```xaml
<Button cal:Message.Attach="[Event Click] = [Action IncrementCount(1)]" />
```

<br>

The short syntax even supports a special form of data binding. To demonstrate this, let’s increments the count by the count value itself (a button that doubles the count value).
```xaml
<Button cal:Message.Attach="[Event Click] = [Action IncrementCount(Count.Text)]" />
```
Here I have set the parameter to be Count.Text. This sets up a binding to the Text property of the TextBlock (named Count) which is displaying the current value. Caliburn Micro will automatically use an appropriate property on a user control if we do not specify a property. In the example above, we could just write the name of the TextBlock (“Count”) as the parameter and Caliburn Micro will bind to the Text property by default.

<br>

#### Automatically Finding Parameters
If you do not explicitly specify a parameter, Caliburn Micro will look at the parameter name in the method signiture and try find any user control in the view that matches this name (ignoring the case). If a matching user control is found, an appropriate property on the control will be used to provide the parameter. For example, if the user control is a TextBlock, the Text property value will be used as the parameter.

<br>

#### Warning
Because of the flexibity of using data binding to set the parameter value, it is possible to pass UI elements from the view into the view-model. You should try to avoid doing this as hard as you possibly can! UI elements in the ViewModel can fracture your MVVM archetecture and cause issues.

<br>

#### Special parameters
- $eventArgs
  - Passes the EventArgs or input parameter to your Action. Note: This will be null for guard methods since the trigger hasn’t actually occurred.
- $dataContext
  - Passes the DataContext of the element that the ActionMessage is attached to. This is very useful in Master/Detail scenarios where the ActionMessage may bubble to a parent VM but needs to carry with it the child instance to be acted upon.
- $source
  - The actual FrameworkElement that triggered the ActionMessage to be sent.
- $view
  - The view (usually a UserControl or Window) that is bound to the ViewModel.
- $this
  - The actual UI element to which the action is attached. In this case, the element itself won't be passed as a parameter, but rather its default property.

<br>
<br>
<br>

### Event guards
Every time Caliburn Micro hooks up an event is also looks for a boolean property or method with the same name plus the word Can before it. It then uses the boolean result to determine whether the event should be handled or not. If not, Caliburn Micro automatically disables the control.

```xaml
<StackPanel>
    <TextBox x:Name="Username" />
    <PasswordBox x:Name="Password" />
    <Button x:Name="Login" Content="Log in" />
</StackPanel>
```
```c#
public bool CanLogin(string username, string password)
{
    return !String.IsNullOrEmpty(username) && !String.IsNullOrEmpty(password);
}

public string Login(string username, string password)
{
    ...
}
```

<br>
<br>
<br>

#### Master/Detail stuff
```c#
public class ShellViewModel : IShell
{
    public BindableCollection<Model> Items { get; private set; }

    public ShellViewModel()
    {
        Items = new BindableCollection<Model>{
            new Model { Id = Guid.NewGuid() },
            new Model { Id = Guid.NewGuid() },
            new Model { Id = Guid.NewGuid() },
            new Model { Id = Guid.NewGuid() }
        };
    }

    public void Add()
    {
        Items.Add(new Model { Id = Guid.NewGuid() });
    }

    public void Remove(Model child)
    {
        Items.Remove(child);
    }
}
```
```xaml
    <StackPanel>
        <ItemsControl x:Name="Items">
            <ItemsControl.ItemTemplate>
                <DataTemplate>
                    <StackPanel Orientation="Horizontal">
                        <Button Content="Remove" cal:Message.Attach="Remove($dataContext)" />
                        <TextBlock Text="{Binding Id}" />
                    </StackPanel>
                </DataTemplate>
            </ItemsControl.ItemTemplate>
        </ItemsControl>
        <Button Content="Add" cal:Message.Attach="Add" />
    </StackPanel>
```

<br>
<br>
<br>
<br>
<br>

## Screens, Conductors, and Composition
Screen = subsection of a page, like github edit window. could kinda say it's only one page

Conductor = only one child page

Inherit from Screen if only one page, Inherit from Conductor<object> if multiple.

https://caliburnmicro.com/documentation/composition

<br>

#### Screen
Often times a screen has a lifecycle associated with it which allows the screen to perform custom activation and deactivation logic. This is the ScreenActivator. For example, take the Visual Studio code editor window. If you are editing a C# code file in one tab, then you switch to a tab containing an XML document, you will notice that the toolbar icons change. Each one of those screens has custom activation/deactivation logic that enables it to setup/teardown the application toolbars such that they provide the appropriate icons based on the active screen. In simple scenarios, the ScreenActivator is often the same class as the Screen. However, you should remember that these are two separate roles. If a particular screen has complex activation logic, it may be necessary to factor the ScreenActivator into its own class in order to reduce the complexity of the Screen. This is particularly important if you have an application with many different screens, but all with the same activation/deactivation logic.

<br>

#### Screen Conductor
Once you introduce the notion of a Screen Activation Lifecycle into your application, you need some way to enforce it. This is the role of the ScreenConductor. When you show a screen, the conductor makes sure it is properly activated. If you are transitioning away from a screen, it makes sure it gets deactivated.

<br>

#### Screen Collection
In an application like Visual Studio, you would not only have a ScreenConductor managing activation and deactivation but would also have a ScreenCollection maintaining the list of currently opened screens or documents. Anything that is in the ScreenCollection remains open, but only one of those items is active at a time. In an MDI-style application like VS, the conductor would manage switching the active screen between members of the ScreenCollection. Opening a new document would add it to the ScreenCollection and switch it to the active screen. Closing a document would not only deactivate it, but would remove it from the ScreenCollection. All that would be dependent on whether or not it answers the question “Can you close?” positively. Of course, after the document is closed, the conductor needs to decide which of the other items in the ScreenCollection should become the next active document.

<br>
<br>
<br>
<br>

#### Decouple ViewModels with built in composition patterns and event aggregation
```c#
public class DocumentTabsViewModel : Conductor<TabViewModel>.Collection.OneActive
{
	...
}

public class CartSummaryViewModel : IHandle<CartChangedMessage>
{
	...
}
```

<br>

#### PropertyChangedBase and BindableCollection
Use BindableCollection<> instead of List<>

<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>

# MVVM
- ViewModel = Program logic
- The way the View and ViewModel talk to each other is databinding with XAML

<br>
<br>
<br>

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

