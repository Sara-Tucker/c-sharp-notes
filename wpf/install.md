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
