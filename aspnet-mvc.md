# C# Notes

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
