# Caliburn.Micro
#### Project -> Quick Install Package -> 'n':
```Caliburn.Micro -Version 4.0.0-alpha.1```

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

---

<br>
<br>
<br>

## Databinding
Automatically bind ViewModel properties to properties on controls with naming convention.
```xaml
<TextBox x:Name="FirstName" />
```
This will cause the “Text” property of the TextBox to be bound to the “FirstName” property on the ViewModel.

Explicit:
```xaml
<TextBox Text="{Binding Path=FirstName, Mode=TwoWay}" />
```

---

<br>
<br>
<br>

## Actions
You can use anything that inherits from System.Windows.Interactivity.TriggerBase to trigger the sending of an ActionMessage. Perhaps the most common trigger is an EventTrigger, but you can create almost any kind of trigger imaginable or leverage some common triggers already created by the community.

#### ActionTrigger
When an ActionTrigger occurs, it executes the specified method by creating an ActionMessage.

#### Action guard
When a handler is found for the “SayHello” message, it will check to see if that class also has either a property or a method named “CanSayHello.” If you have a guard property and your class implements INotifyPropertyChanged, then the framework will observe changes in that property and re-evaluate the guard accordingly.

#### Wiring Events
To wire events on controls to call methods on the ViewModel, give them the same name.
```xaml
<Button x:Name="Save">
```
This will cause the Click event of the Button to call “Save” method on the ViewModel.

<br>

Different events can be used like this:
```xaml
<Button cal:Message.Attach="[Event MouseEnter] = [Action Save]">
```

Different parameters can be passed to the method like this:
```xaml
<Button cal:Message.Attach="[Event MouseEnter] = [Action Save($this)]"> 
```
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

This works well if you only want to bind to the default event but what if you wanted to bind to a different event or even pass parameters? All we have done here is explicitly say which event we are listening for and which function in the View Model should be called.

Next lets look at how we can pass parameters with the action message, modify ShellView as follows so that it passes a parameter when the button is clicked. Next edit the ChangeMessage function in ShellViewModel so that it takes an integer parameter. If you run the app again you should notice that the count is now increased by two, this is because when the button is clicked it sends the action message to the View Model with the specified parameter which is then added to the count.

<br>

What we have done here is used System.Windows.Interactivity triggers to hook up an event to a method. In the EventTrigger we can specify which event we want to listen to, and using the Caliburn Micro ActionMessage we can specify which method should be called. Using this approach you can include any number of event triggers to listen to other events on the same control. So you could listen to MouseEnter and MouseLeave to perform additional actions.

Next let’s look at event parameters. To demonstrate this, we will add another button that increments the count by 2. In AppViewModel.cs we need to modify the IncrementCount method to include an integer parameter. This parameter will be used to change the Count property.

Back in AppView.xaml, update the existing repeat button by adding a Caliburn Micro Parameter to the ActionMessage. The Value property of the Caliburn Micro Parameter is a dependency property, which means it also supports the usual WPF data binding.

Pro Tip: Because of the flexibity of using data binding to set the parameter value, it is possible to pass UI elements from the view into the view-model. You should try to avoid doing this as hard as you possibly can! UI elements in the view-model can fracture your MVVM archetecture and can cause maintenance issues in the future.

```xaml
cal:Message.Attach="[Event Click] = [Action IncrementCount]" />
```

All we have done this time is use one of Caliburn Micro’s attached properties (Message.Attach) to specify which event we are interested in, and which method to call.

Next we look at event parameters using this short syntax. Modify the IncrementCount method in same way we did for the long syntax. Including an event parameter using Message.Attach will look like this:
```xaml
cal:Message.Attach="[Event Click] = [Action IncrementCount(1)]"
```
The short syntax even supports a special form of data binding. To demonstrate this, let’s add a button that increments the count by the count value itself. In other words, a button that doubles the count value. You can remove the CanIncrementCount event guard mentioned in the previous blog post to make the value go higher than 100. The repeat button code would look something like this:
```xaml
<RepeatButton Content="Double" Margin="15" cal:Message.Attach="[Event Click] = [Action IncrementCount(Count.Text)]" />
```
Here I have set the parameter to be Count.Text. This sets up a binding to the Text property of the TextBlock (named Count) which is displaying the current value. Notice that Caliburn Micro automatically converts string values that we want to pass into a method that takes a numerical value. Another shortcut that Caliburn Micro provides here is that it will automatically use an appropriate property on a user control if we do not specify a property. In the example above, we could just write the name of the TextBlock (“Count”) as the parameter and Caliburn Micro will bind to the Text property by default.

#### Automatically Finding Parameters
To finish off this tutorial I’ll mention that Caliburn Micro even has conventions for automatically picking up parameters when you don’t explicitly set them. If you do not explicitly specify a parameter, Caliburn Micro will look at the parameter name in the method signiture and try find any user control in the view that matches this name (ignoring the case). If a matching user control is found, an appropriate property on the control will be used to provide the parameter. For example, if the user control is a TextBlock, the Text property value will be used as the parameter. Again, Caliburn Micro can automatically convert strings to ints and so on if necessary.

To understand this convention more easily, lets try this out in the application. Add a slider to the application and call it “Delta”. Then add another button called “IncrementCount”. As explained in the previous blog post, the button is going to automatically call the IncrementCount method when it is clicked. This time however, the method has a parameter, but we havn’t specified what value the button should use. Notice that the slider we added is the same name as the parameter (delta). Thus Caliburn Micro will automatically use the Value property of the slider as the parameter to the method whenever the button is clicked. Here is all the code we needed to add to do this:

<UniformGrid Columns="2" VerticalAlignment="Bottom">
  <Slider Name="Delta" Minimum="0" Maximum="5" Margin="15" />
  <Button Name="IncrementCount" Content="Increment" Margin="15" />
</UniformGrid>

<br>
<br>

#### Apply methods between your View and ViewModel automatically with parameters and guard methods
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

#### Event guards
Event guards are used to only allow the handling of an event if a certain condition is met. To demonstrate this we will prevent the user from pressing the button more than 10 times. Add a new property to ShellViewModel called CanChangeMessage and also add a new NotifyOfPropertyChange to the Message setter.

Every time Caliburn Micro hooks up an event is also looks for a boolean property with the same name plus the word Can before it. It then uses the result of that property to determine whether the event should be handled or not. If not, Caliburn Micro automatically disables the control.

<br>

#### Action Messages
The Action mechanism allows you to “bind” UI triggers, such as a Button’s “Click” event, to methods on your View-Model. The mechanism allows for passing parameters to the method as well. Parameters can be databound to other FrameworkElements or can pass special values, such as the DataContext or EventArgs. All parameters are automatically type converted to the method’s signature. This mechanism also allows the “Action.Target” to vary independently of the DataContext and enables it to be declared at different points in the UI from the trigger. When a trigger occurs, the “message” bubbles through the element tree looking for an Action.Target (handler) that is capable of invoking the specified method. This is why we call them messages. The “bubbling” nature of Action Messages is extremely powerful and very helpful especially in master/detail scenarios. In addition to invocation, the mechanism supports a “CanExecute” guard. If the Action has a corresponding Property or Method with the same name, but preceded by the word “Can,” the invocation of the Action will be blocked and the UI will be disabled.

<br>

#### Action Conventions
Out of the box, we support a set of binding conventions around the ActionMessage feature. These conventions are based on x:Name. So, if you have a method called “Save” on your ViewModel and a Button named “Save” in your UI, we will automatically create an EventTrigger for the “Click” event and assign an ActionMessage for the “Save” method. Furthermore, we will inspect the method’s signature and properly construct the ActionMessage parameters.

Example
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

Message.Attach

The first thing to notice is that we are using a more Xaml-developer-friendly mechanism for declaring our ActionMessages. The Message.Attach property is backed by a simple parser which takes its textual input and transforms it into the full Interaction.Trigger/ActionMessage that you’ve seen previously. If you work primarily in the Xaml editor and not in the designer, you’re going to like Message.Attach. Notice that neither Message.Attach declarations specify which event should send the message. If you leave off the event, the parser will use the ConventionManager to determine the default event to use for the trigger. In the case of Button, it’s Click. You can always be explicit of coarse. Here’s what the full syntax for our Remove message would look like if we were declaring everything:

<Button Content="Remove" cal:Message.Attach="[Event Click] = [Action Remove($dataContext)]" />

Suppose we were to re-write our parameterized SayHello action with the Message.Attach syntax. It would look like this:

<Button Content="Click Me" cal:Message.Attach="[Event Click] = [Action SayHello(Name.Text)]" />

But we could also leverage some smart defaults of the parser and do it like this:

<Button Content="Click Me" cal:Message.Attach="SayHello(Name)" />

---

<br>
<br>
<br>

NotifyOfPropertyChange:
```c#
set
{
    NotifyOfPropertyChange(() => Property/ControlName)
}
```
Rather than implementing INotifyPropertyChanged in all of your models, you can simply call the NotifyOfPropertyChange method within the setter of your properties.

Traditional way:
```xaml
<TextBlock Text="{Binding PROPERTYNAME}" />
```

<br>

Use BindableCollection<> instead of List<>

Mode:
OneWayToSource - data goes from the form to the property

Inherit from Screen if only one page, Inherit from Conductor<object> if multiple.

screen = only one page

Conductor = only one child page

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
What self respecting WPF/SL framework could go without a base implementation of INotifyPropertyChanged? The Caliburn.Micro implementation enables string and lambda-based change notification. It also ensures that all events are raised on the UI thread. BindableCollection is a simple collection that inherits from ObservableCollection, but that ensures that all its events are raised on the UI thread as well.

<br>
<br>
<br>
<br>

# MVVM

- ViewModel = Program logic
- View is not connected and knows nothing about the Model or ViewModel
- ViewModel is not connected and knows nothing about the View
- The way the View and ViewModel talk to each other is databinding with XAML

#### Instructions
1. Create new project, create Models, Views, ViewModels folders

<br>
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

