# ASP.NET Core

Show/Hide console: ```Ctrl + ` ```  
Create new project: ```dotnet new angular```  
Start server: ```dotnet run```  

<br>

Kestrel - in-process HTTP server implementation

ASP.NET Core is a web framework. An ASP.NET Core application is a console app that creates a web server in its Main method.

File or folder | Purpose
--- | ---
wwwroot | Contains static assets.
Pages | Folder for Razor Pages.
appsettings.json | Configuration
Program.cs | Configures the host of the ASP.NET Core app.
Startup.cs | Configures services and the request pipeline (middleware).


The Main method invokes WebHost.CreateDefaultBuilder, which follows the builder pattern to create a web application host. The builder has methods that define the web server (for example, UseKestrel) and the startup class (UseStartup).

WebHost.CreateDefaultBuilder returns the type IWebHostBuilder, which provides many optional methods. Some of these methods include UseHttpSys for hosting the app in HTTP.sys and UseContentRoot for specifying the root content directory. The Build and Run methods build the IWebHost object that hosts the app and begins listening for HTTP requests.

<br>

## Startup
The Startup class is where you define the app's request handling pipeline (Middleware) and where any services needed by the app are configured. The Startup class must be public and contain the following methods:
```c#
public class Startup
{
    // Use this method to add services to the container.
    public void ConfigureServices(IServiceCollection services)
    {
    }

    // Use this method to configure the HTTP request pipeline. (Add Middleware here)
    public void Configure(IApplicationBuilder app)
    {
    }
}
```

<br>

Content root:  
The content root is the base path to any content used by the app, such as views, Razor Pages, and static assets. By default, the content root is the same as application base path for the executable hosting the app.

Web root:  
The web root of an app is the directory in the project containing public, static resources, such as CSS, JavaScript, and image files.

<br>

## Middleware:
https://docs.microsoft.com/en-us/aspnet/core/fundamentals/middleware/?view=aspnetcore-2.1&tabs=aspnetcore2x

In ASP.NET Core, you compose your request pipeline using middleware. ASP.NET Core middleware performs logic on an HttpContext and then either invokes the next middleware in the sequence or terminates the request directly. A middleware component called "XYZ" is added by invoking an UseXYZ extension method in the Configure method.



- .csproj - dependencies for libraries and frameworks
- Startup.cs - the Startup class configures your application
    - Configure() method - where you build your HTTP processing pipeline.
