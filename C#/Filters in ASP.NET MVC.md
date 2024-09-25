### What are Filters in ASP.NET MVC?

In ASP.NET MVC, **filters** are attributes that provide a way to execute code **before** or **after** certain stages of request processing in the MVC pipeline. Filters allow you to run custom logic at specific points during the request's lifecycle, such as before an action method is executed or after the result has been rendered.

### Types of Filters in ASP.NET MVC

There are **five types of filters** available in ASP.NET MVC:

1. **Authentication Filters**  
   These filters are used to authenticate users before the request reaches the controller. They are typically used to validate user credentials and identity.
   
2. **Authorization Filters**  
   These filters handle authorization logic, determining whether the current user has the necessary permissions to execute a specific action method.
   
3. **Action Filters**  
   These filters allow custom logic to be run **before** and **after** an action method is executed. For example, you might use an action filter to log execution time or validate input data.
   
4. **Result Filters**  
   These filters run **before** and **after** the action result is executed. They are often used for modifying or processing the result data before it is returned to the client.
   
5. **Exception Filters**  
   These filters handle exceptions that are thrown during the execution of the action method or other filters. They are often used to log errors or display custom error messages.

### How Filters Work in MVC Request Lifecycle

When a request is made, ASP.NET MVC processes filters in a specific order:

1. **Authentication**: Filters determine the identity of the user.
2. **Authorization**: Filters determine if the user is authorized to access the resource.
3. **Action Execution**: Action filters are applied before and after the controller's action method is invoked.
4. **Result Execution**: Result filters are applied before and after the result (like a view or JSON response) is processed.
5. **Exception Handling**: If an exception occurs at any point, exception filters come into play.

### Example of Using Filters

Let's see an example using an **Action Filter** to log the execution time of an action method:

#### Creating a Custom Action Filter:

```csharp
using System;
using System.Diagnostics;
using System.Web.Mvc;

public class LogExecutionTimeFilter : ActionFilterAttribute
{
    private Stopwatch _stopwatch;

    // Runs before the action method starts executing
    public override void OnActionExecuting(ActionExecutingContext filterContext)
    {
        _stopwatch = Stopwatch.StartNew();
        base.OnActionExecuting(filterContext);
    }

    // Runs after the action method finishes executing
    public override void OnActionExecuted(ActionExecutedContext filterContext)
    {
        _stopwatch.Stop();
        var executionTime = _stopwatch.ElapsedMilliseconds;
        filterContext.HttpContext.Response.Write($"<p>Action executed in {executionTime} ms</p>");
        base.OnActionExecuted(filterContext);
    }
}
```

#### Applying the Action Filter to a Controller or Action:

```csharp
// Apply the filter globally to the entire controller
[LogExecutionTimeFilter]
public class HomeController : Controller
{
    public ActionResult Index()
    {
        return View();
    }

    // Apply the filter to a specific action method
    [LogExecutionTimeFilter]
    public ActionResult About()
    {
        return View();
    }
}
```

In this example:
- The `LogExecutionTimeFilter` action filter calculates the time taken for the action method to execute and writes it to the response.
- The filter is applied to the controller or a specific action, so the logic runs before and after the method is executed.

### Built-in Filters in ASP.NET MVC

There are some built-in filters in ASP.NET MVC that you can use out of the box:

1. **[Authorize]**: Ensures that the user is authorized to access the action or controller.
   
   ```csharp
   [Authorize]
   public ActionResult Dashboard() 
   {
       return View();
   }
   ```

2. **[HandleError]**: Provides a way to handle exceptions thrown by action methods.
   
   ```csharp
   [HandleError]
   public ActionResult ErrorProneAction()
   {
       throw new Exception("This is an error!");
   }
   ```

3. **[OutputCache]**: Caches the output of an action for a specified amount of time, improving performance by reducing unnecessary processing.
   
   ```csharp
   [OutputCache(Duration = 60)]
   public ActionResult CachedAction()
   {
       return View();
   }
   ```

### How to Apply Filters
1. **Global Filters**: Applied to all actions across all controllers in the application.
   - In `Global.asax.cs`:

   ```csharp
   protected void Application_Start()
   {
       GlobalFilters.Filters.Add(new HandleErrorAttribute());
   }
   ```

2. **Controller-Level Filters**: Applied to all actions in a specific controller.
   - On the controller:

   ```csharp
   [Authorize]
   public class AccountController : Controller
   {
       // All actions in this controller require authorization
   }
   ```

3. **Action-Level Filters**: Applied to specific action methods.
   - On a specific action method:

   ```csharp
   public class AccountController : Controller
   {
       [Authorize]
       public ActionResult Dashboard()
       {
           return View();
       }
   }
   ```

### Summary

- **What**: Filters allow you to run custom code before or after specific stages of the MVC request pipeline (e.g., before or after an action is executed).
- **Why**: Filters are useful for tasks like authentication, authorization, logging, error handling, or modifying the result.
- **When**: Filters run in a predefined order, helping to enforce security, validation, and other cross-cutting concerns.
- **Where**: Filters can be applied globally, at the controller level, or on specific actions.
- **Who**: Developers apply filters when there's a need to handle cross-cutting concerns (such as logging, security, or caching) in a DRY (Don’t Repeat Yourself) manner.

### Tips:
1. Use filters to avoid repetitive code.
2. Choose the correct filter type for the task at hand.
3. Apply filters at the appropriate level (globally, per controller, or per action).

### Warning:
- Overusing filters can lead to complex and hard-to-debug code, especially when multiple filters interact with each other.

This covers an overview of filters in ASP.NET MVC. Let me know if you'd like to explore a specific filter type further!
