# ASP.NET MVC

MVC Architectural Pattern
Model View Controller

An architectural pattern for implementing user interfaces.


Model:
Application data and behaviour in terms of its problem domain, and independent of the UI.

Domain Model of the movie app: classes will be:
- Movie
- Customer
- Rental
- Transaction

These classes have properties and methods which represent the application state and rules. They are not tied to the user interface, meaning they could be used the same for a desktop or mobile app.


View:
HTML markup displayed to the user.


Controller:
Responsible for handing a http request.


Example:
if a user requests http://vidly.com/movies, a Controller will be selected to handle their request. The Controller will get all the movies from the database (Model) and put them in a View and return the View to the user's browser.


Router:
Almost always part of MVC but not in the acronym. Selects the right Controller to handle a request. The Router knows that the request for http://vidly.com/movies should be handled by the MoviesController class Controller, (or more accurately the request should be handled by a method of that class). The methods of a controller are called Actions. So techincally an Action (method) of the class will handle the request.


MVC allows for:
Separation of concerns
More maintainable applications


#### Project solution explorer:
- App_Data - where the database file will be stored
- App_Start - classes that are called when the application is started
    - RouteConfig - the configuration of the routing rules
        - url: "{controller}/{action}/{id}"
            - the controller used, the Action of that controller, id is an argument passed to that Action
            - Example: request to /movies/popular
            - {controller} = MoviesController
            - {action} = Popular()
            - Example: request to /movies/edit/351
            - {controller} = MoviesController
            - {action} = Edit(int id)
        - defaults: new { controller = "Home", action = "Index", id = UrlParameter.Optional }
            - Example: if url doesn't have anything in the url ^ thing above -> passed to HomeController
            - Example: /movies -> handled by the MoviesController.Index() Action
            - id is an optional parameter
- Content - store client side assets (.css, images)
- Controllers
    - AccountController - Actions for sign in, log out, etc
    - HomeController - homepage
    - ManageController - Actions for users to manage their profiles
- Models - all the domain classes will be here
- Scripts - JS files
- Views
- Startup.cs (old ver is Global.asax) - provides hooks for various events in the application's life cycle. Contains method that is called when app is started. It registers a few things, like the routes.
packages.config - used by NuGet package manager. Package managers manage the dependencies of the app.
    - Example: if app has dependencies on 5 external libraries. instead of going to 5 different sites and downloading them, NuGet gets all the packages for you.
- Web.config - xml doc of the apps config. <connectionStrings> and <appSettings> are most used.
