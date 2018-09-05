# WPF

[WPF Overview](https://docs.microsoft.com/en-us/visualstudio/designers/introduction-to-wpf?view=vs-2017)  
[Great YouTube series](https://www.youtube.com/watch?v=Vjldip84CXQ&list=PLrW43fNmjaQVYF4zgsD0oL9Iv6u23PI6M)

<br>

[Designer vs Blend](https://docs.microsoft.com/en-us/visualstudio/designers/designing-xaml-in-visual-studio?view=vs-2017)  
[XAML Overview](https://docs.microsoft.com/en-us/dotnet/framework/wpf/advanced/xaml-overview-wpf)  
[DataGrid (and use from SQL server)](https://docs.microsoft.com/en-us/dotnet/framework/wpf/controls/datagrid#related-topics)  
[WPF with EF](https://docs.microsoft.com/en-us/visualstudio/data-tools/create-a-simple-data-application-with-wpf-and-entity-framework-6?view=vs-2017)

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

