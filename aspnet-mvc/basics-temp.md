# ASP.NET MVC

ASP.NET MVC 4 is a web framework.

MVC is an architectural pattern for implementing user interfaces. MVC allows for: Separation of concerns and More maintainable applications.


Model:  
Application data and behaviour in terms of its problem domain, and independent of the UI.

Domain Model of the movie app (classes):
- Movie
- Customer
- Rental
- Transaction

These classes have properties and methods which represent the application state and rules. They are not tied to the user interface, meaning they could be used the same for a desktop or mobile app.


View:  
HTML displayed to the user.

Partial View - not a complete page. A widget that can be used on different Views.  
Layout page - a template or master page. if you want all your pages to have the same look and feel use a layout.

```
@model VidIO.Models.Movie

<h2>@Model.<h2
```
Every View has a property called Model which gives access to the Model that was passed to the View by the Controller.

Controller:
Responsible for handing a HTTP request.  
The methods of a Controller are called Actions.

Example:  
If a user requests http://vid.io/movies, a Controller will be selected to handle their request. The Controller will get all the movies from the database (Model), put them in a View, and return the View to the user's browser.

Router:  
Selects the right Controller to handle a request. The Router knows that the request for http://vid.io/movies should be handled by the MoviesController class Controller, or more accurately, the request should be handled by a method of that class. The methods of a controller are called Actions. So techincally an Action (method) of the class will handle the request.

<br>
<br>
<br>

File or folder | Purpose
--- | ---
App_Data | database file
App_Start | classes that are called when the app is started
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;BundleConfig | Set Bootstrap style
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;RouteConfig | URL patterns
Content | stores static assets (.css, images)
Models | stores domain classes
Scripts | JS files
Global.asax | provides hooks for various events in the application's life cycle
packages.config | used by NuGet; package managers manage the dependencies of the app
Web.config | xml doc of the apps config; \<connectionStrings\> and \<appSettings\> are used most

<br>

#### RouteConfig
RouteConfig - URL patterns
```c#
routes.MapRoute(
    name: "Default",
    url: "{controller}/{action}/{id}",
    defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional });
```
- url - {The controller used}/{a method of that controller}/{an ID passed as an argument to that method}
  - /movies/popular
    - Controller = MoviesController, Method = Popular()
  - /movies/edit/351
    - Controller = MoviesController, Method = Edit(int id)
- defaults - Where it redirects to if a {} wasn't given.

<br>
<br>



- .csproj - dependencies for libraries and frameworks
- Startup.cs - the Startup class configures your application
    - Configure() method - where you build your HTTP processing pipeline.



Middleware - software components that are assembled into an application pipeline to handle requests and responses.

Middleware in ASP.NET Core controls how our application responds to HTTP requests. It can also control how our application looks when there is an error, and it is a key piece in how we authenticate and authorize a user to perform specific actions.

Each component chooses whether to pass the request on to the next component in the pipeline, and can perform certain actions before and after the next component is invoked in the pipeline.

Request delegates are used to build the request pipeline. The request delegates handle each HTTP request.

Each piece of middleware in ASP.NET Core is an object, and each piece has a very specific, focused, and limited role.


Logging middleware component:
This logger can see everything about the incoming request, but chances are a logger is simply going to record some information and then pass along this request to the next piece of middleware.


wwwroot (web root) folder - files served over an http request


An ASP.NET Core web application is actually a console project which starts executing from Main() in the Program class where we can create a host for the web application. 
Every ASP.NET Core web application requires a host to be executed. A host must implement IWebHost interface.




