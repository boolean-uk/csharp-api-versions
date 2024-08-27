# C# WebApi's

This solution contains a couple of webapi's from different versions 7 & 8,

The classic Controller method of building API's is still used but a default now in version 8, you get a minimal api approach.  This is the way we will build our api's but as a developer you should have experience of the previous versions.

## Setup

This soluion was setup with the following commands in GitBash:  
```
dotnet new sln --name workshop
dotnet new webapi --name workshop.wwwapi7 -f net7.0
dotnet new webapi --name workshop.wwwapi8 
dotnet add **/*.csproj
```

**NOTE**  you will need to create an appsettings.json AND appsettings.Development.json file in the root of each project.  This is excluded in the gitignore file, so look in there at the last few lines and  you will see the relevant script to exclude.  That should prevent the files from uploading to github.  The contents of your settings files should be:
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

Examine the WeatherForecastController class

## workshop.wwwapi8

Everything is mapped in the Program.cs file.  