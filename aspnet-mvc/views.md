# View

HTML displayed to the user.

<br>

Views for a Controller are put in a folder with the same name.

- Controllers
  - AccountController
  - HomeController
  - ManageController
- Views
  - Account
  - Home
  - Manage
  - Shared = Views used across different Controllers

<br>

Partial View - not a complete page. A widget that can be used on different Views.  
Layout page - a template or master page. if you want all your pages to have the same look and feel use a layout.

```
@model VidIO.Models.Movie

<h2>@Model.<h2
```
Every View has a property called Model which gives access to the Model that was passed to the View by the Controller.
