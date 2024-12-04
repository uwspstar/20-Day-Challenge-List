
### **.NET Core Web API project** as a reverse proxy to bypass **Same-Origin Policy** (CORS) issues. 

Here’s how you can set this up:

---

### **Key Setup**
1. **Blazor App**:
   - Runs on `https://localhost:5001`.
   - Communicates with the Web API proxy for cross-origin requests.
2. **Web API Proxy**:
   - Runs on a separate port (e.g., `https://localhost:7001`).
   - Acts as a reverse proxy, fetching content from external sources and returning it to the Blazor app.

---

### **Step-by-Step Guide**

#### **1. Create a New .NET Core Web API Project**

1. Open a terminal and create a new Web API project:
   ```bash
   dotnet new webapi -n ReverseProxyAPI
   cd ReverseProxyAPI
   ```

2. Install required dependencies:
   ```bash
   dotnet add package Microsoft.AspNetCore.Cors
   ```

3. Open the `Program.cs` file and set up CORS:

   ```csharp
   var builder = WebApplication.CreateBuilder(args);

   // Add services to the container
   builder.Services.AddCors(options =>
   {
       options.AddPolicy("AllowBlazor", policy =>
       {
           policy.WithOrigins("https://localhost:5001")  // Blazor app origin
                 .AllowAnyHeader()
                 .AllowAnyMethod();
       });
   });

   builder.Services.AddControllers();
   builder.Services.AddHttpClient();  // Add HttpClient for proxy functionality

   var app = builder.Build();

   // Enable CORS for the Blazor app
   app.UseCors("AllowBlazor");

   // Configure the HTTP request pipeline
   app.UseHttpsRedirection();
   app.UseAuthorization();
   app.MapControllers();

   app.Run();
   ```

---

#### **2. Add the Proxy Logic**

1. Create a `ProxyController`:

   - Navigate to the `Controllers` folder.
   - Create a new file called `ProxyController.cs`.

   ```csharp
   using Microsoft.AspNetCore.Mvc;
   using System.Net.Http;
   using System.Threading.Tasks;

   namespace ReverseProxyAPI.Controllers
   {
       [ApiController]
       [Route("api/[controller]")]
       public class ProxyController : ControllerBase
       {
           private readonly HttpClient _httpClient;

           public ProxyController(HttpClient httpClient)
           {
               _httpClient = httpClient;
           }

           [HttpGet("fetch")]
           public async Task<IActionResult> Fetch([FromQuery] string url)
           {
               if (string.IsNullOrEmpty(url))
                   return BadRequest("URL is required.");

               try
               {
                   // Fetch the content from the external URL
                   var response = await _httpClient.GetAsync(url);
                   response.EnsureSuccessStatusCode();

                   // Read and return the response content
                   var content = await response.Content.ReadAsStringAsync();
                   return Content(content, response.Content.Headers.ContentType?.ToString() ?? "text/html");
               }
               catch (HttpRequestException ex)
               {
                   return BadRequest($"Error fetching the URL: {ex.Message}");
               }
           }
       }
   }
   ```

---

#### **3. Run the Web API Proxy**

1. Run the Web API project:
   ```bash
   dotnet run
   ```

2. Verify it runs on `https://localhost:7001` (or another port, as displayed in the terminal).

---

#### **4. Configure the Blazor App**

In your Blazor Server app:

1. **Set up the iframe** in a Razor page (e.g., `ProxyPage.razor`):

   ```razor
   @page "/proxy"
   <h3>Cross-Origin Proxy Example</h3>

   <!-- Use the proxy API to fetch external content -->
   <iframe src="https://localhost:7001/api/proxy/fetch?url=https://example.com" 
           width="800" 
           height="600" 
           style="border: 1px solid black;">
   </iframe>
   ```

2. **Run your Blazor app**:
   - The iframe will load content from the Web API proxy (`https://localhost:7001`), which in turn fetches content from `https://example.com`.

---

### **How It Works**
1. The Blazor app (`https://localhost:5001`) makes a request to the proxy (`https://localhost:7001`).
2. The proxy (`ProxyController`) fetches content from the external site (`https://example.com`).
3. The proxy returns the content to the Blazor app as if it originated from the proxy, bypassing Same-Origin Policy.

---

### **Important Notes**
1. **CORS Configuration**:
   - The Web API proxy explicitly allows the Blazor app’s origin (`https://localhost:5001`).
   - Adjust the `WithOrigins` value in `Program.cs` if your Blazor app uses a different URL in production.

2. **Security**:
   - Validate the incoming `url` parameter to prevent misuse of the proxy.
   - Add a whitelist for allowed domains to ensure only trusted sources can be proxied.

   Example:
   ```csharp
   private readonly List<string> _allowedDomains = new List<string>
   {
       "example.com",
       "another-domain.com"
   };

   private bool IsUrlAllowed(string url)
   {
       var uri = new Uri(url);
       return _allowedDomains.Contains(uri.Host);
   }
   ```

   Validate the URL in the `Fetch` method:
   ```csharp
   if (!IsUrlAllowed(url))
       return BadRequest("This URL is not allowed.");
   ```

3. **Performance**:
   - If the external content doesn’t change often, implement caching in the proxy to reduce load.

---

### **Summary**
This approach creates a secure and flexible reverse proxy with a separate .NET Core Web API project. The Web API handles the cross-origin communication, while the Blazor app focuses on rendering the content seamlessly.

If you have further questions or need adjustments, let me know!
