### What is an Action Filter in ASP.NET MVC?

An **Action Filter** in ASP.NET MVC is a specialized filter that allows you to inject custom logic **before** or **after** the execution of an action method. Action filters are part of the **MVC filters** framework, which includes several types of filters, such as authentication, authorization, and result filters. **Action filters** are specifically used to manipulate the execution flow of action methods and can be applied globally, at the controller level, or on specific action methods.

### Why Use Action Filters?

Action filters are used when you need to execute logic that applies to multiple actions or controllers without repeating the same code. This includes scenarios like:
- Logging
- Caching
- Performance monitoring
- Validating input
- Exception handling
- Modifying the result returned by the action method

By using action filters, you adhere to the **DRY** (Don't Repeat Yourself) principle, since the filter logic is centralized and applied across multiple controllers or actions.

### Types of Filters in MVC

To understand action filters, it's helpful to know the other types of filters available in ASP.NET MVC:

1. **Authentication Filters**: Validate user credentials.
2. **Authorization Filters**: Verify if the user is authorized to execute the action.
3. **Action Filters**: Inject logic before or after the execution of action methods.
4. **Result Filters**: Modify the result before it is rendered to the view.
5. **Exception Filters**: Handle exceptions thrown during action execution.

Among these, **action filters** focus on action execution and are triggered at specific points in the request processing pipeline.

### How Action Filters Work

Action filters are typically implemented by overriding one or more methods of the `ActionFilterAttribute` class. These methods define where the custom logic should be injected into the action execution process:

- **OnActionExecuting**: Runs **before** the action method is executed.
- **OnActionExecuted**: Runs **after** the action method is executed but **before** the result is returned.
- **OnResultExecuting**: Runs **before** the result (such as a view) is processed.
- **OnResultExecuted**: Runs **after** the result is processed.

### Example of Creating and Using an Action Filter

#### 1. Create a Custom Action Filter

Let’s create a simple action filter that logs the execution time of an action method.

```csharp
using System.Diagnostics;
using System.Web.Mvc;

public class LogExecutionTimeAttribute : ActionFilterAttribute
{
    private Stopwatch _stopwatch;

    // Runs before the action method executes
    public override void OnActionExecuting(ActionExecutingContext filterContext)
    {
        _stopwatch = Stopwatch.StartNew();
        base.OnActionExecuting(filterContext);
    }

    // Runs after the action method executes
    public override void OnActionExecuted(ActionExecutedContext filterContext)
    {
        _stopwatch.Stop();
        var executionTime = _stopwatch.ElapsedMilliseconds;
        filterContext.HttpContext.Response.Write($"<p>Action executed in {executionTime} ms</p>");
        base.OnActionExecuted(filterContext);
    }
}
```

#### 2. Apply the Action Filter

Once you create the custom filter, you can apply it in different ways:

##### a. **Apply to an Action Method**

```csharp
public class HomeController : Controller
{
    [LogExecutionTime]
    public ActionResult Index()
    {
        return View();
    }
}
```

##### b. **Apply to a Controller**

```csharp
[LogExecutionTime]
public class HomeController : Controller
{
    public ActionResult Index()
    {
        return View();
    }

    public ActionResult About()
    {
        return View();
    }
}
```

##### c. **Apply Globally (for all controllers and actions)**

To apply the action filter globally, modify `Global.asax.cs`:

```csharp
public class MvcApplication : System.Web.HttpApplication
{
    protected void Application_Start()
    {
        GlobalFilters.Filters.Add(new LogExecutionTimeAttribute());
    }
}
```

#### 3. Result in Action

When you apply the `LogExecutionTimeAttribute` to an action, it calculates and logs the time taken for the action method to execute, then writes the result to the HTTP response. The time will appear on the rendered page as something like:

```html
<p>Action executed in 150 ms</p>
```

### Action Filter Methods

Here are the important methods you can override when creating an action filter:

1. **OnActionExecuting(ActionExecutingContext filterContext)**  
   This method is called **before** the action method is executed. You can use it to perform logic such as logging, validation, or setting parameters.

2. **OnActionExecuted(ActionExecutedContext filterContext)**  
   This method is called **after** the action method executes but **before** the result is returned to the view. You can use this to log the results, catch any errors, or clean up resources.

3. **OnResultExecuting(ResultExecutingContext filterContext)**  
   This method runs **before** the action result (such as a view) is processed. It’s typically used for modifying the result before rendering.

4. **OnResultExecuted(ResultExecutedContext filterContext)**  
   This method runs **after** the action result has been processed and rendered to the view.

### Example of Using `OnResultExecuting` and `OnResultExecuted`

```csharp
public class ModifyResultFilter : ActionFilterAttribute
{
    public override void OnResultExecuting(ResultExecutingContext filterContext)
    {
        // This runs before the result is rendered to the view
        filterContext.HttpContext.Response.Write("<p>Before rendering the result</p>");
    }

    public override void OnResultExecuted(ResultExecutedContext filterContext)
    {
        // This runs after the result is rendered to the view
        filterContext.HttpContext.Response.Write("<p>After rendering the result</p>");
    }
}
```

### Practical Use Cases of Action Filters

1. **Logging**: Log the details of each request, including the action name, parameters, and execution time.
2. **Caching**: Cache the result of an action method to improve performance.
3. **Input Validation**: Validate input data before the action is executed.
4. **Performance Monitoring**: Measure and log the performance of action methods.
5. **Authorization**: Implement custom authorization logic before the action is executed.
6. **Error Handling**: Handle exceptions raised during action execution or log errors in a centralized way.

### Built-In Action Filters in ASP.NET MVC

ASP.NET MVC provides several built-in action filters that are commonly used:

1. **[Authorize]**: Ensures the user is authorized to access the action.
   
   ```csharp
   [Authorize]
   public ActionResult Dashboard()
   {
       return View();
   }
   ```

2. **[HandleError]**: Catches exceptions thrown by the action method and displays a custom error page.

   ```csharp
   [HandleError]
   public ActionResult ErrorProneAction()
   {
       throw new Exception("An error occurred!");
   }
   ```

3. **[OutputCache]**: Caches the output of an action method for a specified duration.

   ```csharp
   [OutputCache(Duration = 60)]
   public ActionResult CachedAction()
   {
       return View();
   }
   ```

### Summary

- **What**: Action filters in ASP.NET MVC are used to inject custom logic before or after the execution of action methods.
- **Why**: To handle cross-cutting concerns like logging, validation, error handling, performance monitoring, and caching without repeating code.
- **When**: Action filters are applied at various stages in the action execution pipeline, depending on the methods you override.
- **Where**: Filters can be applied globally, at the controller level, or on individual actions.
- **Who**: Developers use action filters to centralize and apply common functionality across multiple actions or controllers.

### Comparison of Action Filters vs Other Filters

| Filter Type            | Purpose                                | When it Executes                                                   |
|------------------------|----------------------------------------|--------------------------------------------------------------------|
| **Authentication**      | Validates user credentials             | Before action method execution                                     |
| **Authorization**       | Verifies user authorization            | Before action method execution                                     |
| **Action**              | Custom logic before/after action method| Before and after action method execution                           |
| **Result**              | Custom logic before/after result       | Before and after the result is executed (e.g., view rendering)      |
| **Exception**           | Handles exceptions                     | When an exception occurs during action or result execution          |

### Tips:
1. **Reusable Logic**: Use action filters to avoid duplicating common logic like logging or performance monitoring across multiple actions.
2. **Global Filters**: You can apply action filters globally using the `GlobalFilters` collection.
3. **Custom Filters**: Implement custom filters by inheriting from `ActionFilterAttribute` and overriding the appropriate methods.

### Warning:
- Be cautious of overusing filters, as it can make the control flow hard to follow, especially if multiple filters are applied on the same action.

This should give you a clear understanding of action filters in ASP.NET MVC. Let me know if you’d like to explore other types of filters or advanced topics!
