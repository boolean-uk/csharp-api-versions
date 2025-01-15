# C# WebApi's

This solution contains a couple of webapi's from different versions 7 & 8,

The classic Controller method of building API's is still used but a default now in version 8, you get a minimal api approach.  This is the way we will build our api's but as a developer you should have experience of the previous versions.

## Learning Objectives

- Setting up a webapi project
- Understand the different C# webapi project types
## Setup

This soluion was setup with the following commands in GitBash:  
```
dotnet new sln --name workshop
dotnet new webapi --name workshop.wwwapi7 -f net7.0
dotnet new webapi --name workshop.wwwapi8 
dotnet add **/*.csproj
```

**NOTE**  when you fork / clone this repository, you will need to create an appsettings.json AND appsettings.Development.json file in the root of each project.  This is excluded in the gitignore file, so look in there at the last few lines and  you will see the relevant script to exclude.  That should prevent the files from uploading to github.  The contents of your settings files should be:
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}

```

## workshop.wwwapi7

- ```dotnet new webapi -n workshop.wwwapi7 -f net7.0```
- Examine the WeatherForecastController class

## workshop.wwwapi8

- ```dotnet new webapi -n workshop.wwwapi8 -f net8.0```
- Everything is mapped in the Program.cs file.  

## workshop.wwwapi9

- Everything is mapped in the Program.cs file.  
- Swagger no longer included - do have the open api spec: [https://localhost:7199/openapi/v1.json](https://localhost:7199/openapi/v1.json)

## Install Swagger

- Can install Swagger with Swashbuckle.AspNetCore the Program.cs should look like this (the only modification in the app.Environment.IsDevelopment() if statement):
- Visit [https://localhost:7199/swagger](https://localhost:7199/swagger)

```cs
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
// Learn more about configuring OpenAPI at https://aka.ms/aspnet/openapi
builder.Services.AddOpenApi();


var app = builder.Build();

// Configure the HTTP request pipeline.
if (app.Environment.IsDevelopment())
{
    app.MapOpenApi();
    app.UseSwaggerUI(options =>
    {
        options.SwaggerEndpoint("/openapi/v1.json", "Demo API");
    });
}

app.UseHttpsRedirection();

var summaries = new[]
{
    "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
};

app.MapGet("/weatherforecast", () =>
{
    var forecast =  Enumerable.Range(1, 5).Select(index =>
        new WeatherForecast
        (
            DateOnly.FromDateTime(DateTime.Now.AddDays(index)),
            Random.Shared.Next(-20, 55),
            summaries[Random.Shared.Next(summaries.Length)]
        ))
        .ToArray();
    return forecast;
})
.WithName("GetWeatherForecast");

app.Run();

record WeatherForecast(DateOnly Date, int TemperatureC, string? Summary)
{
    public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
}

```

## Install Scalar

- install-package Scalar.AspNetCore
- Change the Program.cs and add app.MapScalarApiReference(); in the if statement:
  
```cs
if (app.Environment.IsDevelopment())
{
    app.MapOpenApi();
    app.UseSwaggerUI(options =>
    {
        options.SwaggerEndpoint("/openapi/v1.json", "Demo API");
    });
    app.MapScalarApiReference();
}
```
- visit: [https://localhost:7199/scalar/v1](https://localhost:7199/scalar/v1)


## Useful Resources

- Microsoft provide some further reading on the subject [here](https://learn.microsoft.com/en-us/aspnet/core/fundamentals/apis?view=aspnetcore-8.0)
- Verb definitions [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)