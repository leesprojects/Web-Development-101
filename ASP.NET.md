# ASP.NET
## [MVC Controllers](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs)

An <b>Action</b> is a controller's method which has been called from a particular URL address.
Actions cannot be overloaded or static
An action can return one of the following.

| Action Result| Return Method | Description |
| :-: | :-: | :-:|
| ViewResult | View  | Represents HTML and markup |
| EmptyResult |  N/A | Represents no result |
| RedirectResult | Redirect(), RedirectToAction(), RedirectToRoute()  | Represents a redirection to a new URL |
| JsonResult | Json() | Represents a JavaScript Object Notation for AJAX |
| JavaScriptResult  | JavaScriptResult() | Represents a JavaScript script
| ContentResult | Content() | Represents a text result |
| FileContentResult  | File() | Represents a downloadable file (with the binary - content) |
| FilePathResult | File() | Represents a downloadable file (with a path) |
| FileStreamResult | File() | Represents a downloadable file (with a file stream) |

## [MVC Default Route Maps](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-cs)
Default Map Routes
```C#
routes.MapRoute(
  "Default",                                              // Route name
  "{controller}/{action}/{id}",                           // URL with parameters
  new { controller = "Home", action = "Index", id = "" }  // Parameter defaults
  );
```

## [MVC Unit Testing](https://learn.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs)
```C#
namespace StoreTests.Controllers
{
  //TESTING TARGET
  public class ProductController : Controller
  {
    public ActionResult Index()
    {
      // Add action logic here
      throw new NotImplementedException();
    }

    public ActionResult Details(int Id)
    {
      return View("Details");
    }
  }

  //UNIT TESTING
  [TestClass]
  public class ProductControllerTest
  {
    [TestMethod] //Test if the view is called 'Details'
    public void TestDetailsView()
    {
      var controller = new ProductController();
      var result = controller.Details(2) as ViewResult;
      Assert.AreEqual("Details", result.ViewName);
    }

    [TestMethod] //Test if view data contains a product named 'Laptop'
    public void TestDetailsViewData()
    {
      var controller = new ProductController();
      var result = controller.Details(2) as ViewResult;
      var product = (Product) result.ViewData.Model;
      Assert.AreEqual("Laptop", product.Name);
    }

    [TestMethod] //Test the action results
    //if Index is invalid i.e. < -1 then redirect to Index() action
    //else, return the details view for the item
    public void TestDetailsRedirect()
    {
      var controller = new ProductController();
      var result = (RedirectToRouteResult) controller.Details(-1);
      Assert.AreEqual("Index", result.Values["action"]);
    }
  }
}
//result.ViewName will return 'Details' even if return View(); has no arguments since it will infer it
//Run all tests in solution for results
```

  
## [JSON Web Tokens](https://jwt.io/)
View Web Token content with [JWT.MS](https://jwt.ms/)
A data structure standard for creating data with a signature and payload with encrpytion.
E.g.
```JS
//HEADER.PAYLOAD.SIGNATURE
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

```

  | Component | Function |
  | - | - |
  | HEADER | Algorithm & Token Type |
  | PAYLOAD | Data |
  | SIGNATURE | Encodes the token for verifcation |
  
Benefits
- Dosent use cookies
- can be used across several backends
- fully self-contained
- one process for verification

[MVC Services](https://stackoverflow.com/questions/38138100/addtransient-addscoped-and-addsingleton-services-differences)
```C#
services.AddScoped<ITokenService, TokenService>();
//Same within a request, different across different requests

services.AddTransient<ITokenService, TokenService>();
//A new instance for every controller and service

services.AddSingleton<ITokenService, TokenService>();
//Same for every object and request
```

Encryption Key Types
| Key Type | Purpose |
| :-: | :-: |
| Symmetric | Server only |
| Asymmetric | Server and client need to decrpyt with a public key |

  

<br><br><br>