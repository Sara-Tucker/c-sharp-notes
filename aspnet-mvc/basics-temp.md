# ASP.NET MVC

ASP.NET MVC 4 is a web framework.

MVC is an architectural pattern for implementing user interfaces. MVC allows for: Separation of concerns and More maintainable applications.


ViewModel:  
A Model specifically built for a View. It contains the data for that View.


Controller:
Responsible for handing a HTTP request.  
The methods of a Controller are called Actions.

Example:  
If a user requests http://vid.io/movies, a Controller will be selected to handle their request. The Controller will get all the movies from the database (Model), put them in a View, and return the View to the user's browser.

#### Attribute Routing:
Add ```routes.MapMvcAttributeRoutes();``` to RouteConfig.

```c#
[Route("movies/released/{year}/{month:regex(\\d{2}):range(1, 12)}")]
public ActionResult ByReleaseDate(int year, int month)
{
}
```


Controllers return the type ActionResponse.

#### ActionResult Sub-Types:
Type | Return Method | Returns
--- | --- | ---
ViewResult | View() | View
PartialViewResult | PartialView() | Partial View
ContentResult | Content() | Text / SQL text
RedirectResult | Redirect() | Redirect to a URL
RedirectToRouteResult | RedirectToAction() | Redirect to an Action
JsonResult | Json() | Serialized JSON object
FileResult | File() | File
HttpNotFoundResult | HttpNotFound() | 404
EmptyResult | new EmptyResult() | Void

#### Action Parameters
Parameter Binding:  
Request -> ASP.NET Framework -> Action

When a request is made ASP.NET automatically passes request data as arguments to Action methods.

Parameter Sources:
- URL: /movies/edit/**1**
- Query string: /movies/edit **?id=1**
- Form data: **id=1**

Optional parameters:  
Add a ? at the end of a type to make it nullable. Strings are nullable by default.
```c#
public ActionResult Index(int? pageIndex, string sortBy)
{
    // We want the pageIndex to be optional, because if no argument is passed we will show page 1.
}
```


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




