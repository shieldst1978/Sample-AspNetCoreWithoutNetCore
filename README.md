# Sample-AspNetCoreWithoutNetCore
I wanted to test the theory that AspNetCore can run inside a standard csproj project. 

## Items Required to Run
Basic summary of how to bootstrap a Asp.Net Core MVC 6 application using csproj and standard VS15 tooling.

### Nuget Packages
```
Install-Package Microsoft.AspNetCore
Install-Package Microsoft.AspNetCore.Mvc
```

### Entry Point ( Console App Project )
It is important to add a link to libuv.dll of your processor type to be output to the /bin folder. .Net Core will not add this dll by default and it will cause you to get the error that libuv.dll is not found.

```
internal static class Program
{
    private static void Main()
    {
        new WebHostBuilder().UseKestrel().UseStartup<Startup>().Build().Run();
    }
}
```

### Startup and Configuration of MVC
```
internal class Startup
{
    public void Configure(IApplicationBuilder app, IHostingEnvironment env, ILoggerFactory loggerFactory)
    {
        app.UseMvcWithDefaultRoute();
    }

    public void ConfigureServices(IServiceCollection services)
    {
        services.AddMvc();
    }
}
```

### Basic Controller
```
[Route("/")] 
public class HomeController : Controller
{
    [HttpGet("")]
    public IActionResult Index()
    {
        return Ok("Hello World, From Asp.Net Core (MVC 6) in regular VS15 .Net Project!");
    }
}
```

