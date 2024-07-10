# Demo ASP.NET MVC Application

This repository contains a demo ASP.NET MVC application, showcasing the core components and features of the ASP.NET MVC framework.

## Project Overview

The main objective of this project is to demonstrate the development of a functional web application using the ASP.NET MVC framework. The application highlights the separation of concerns principle by dividing the application into Models, Views, and Controllers.

## Project Structure

- **Models**: Defines the data structures used in the application.
- **Views**: Handles the presentation logic and renders the user interface.
- **Controllers**: Manages the flow of the application, handles user input, and updates the views and models accordingly.

## Getting Started

### Prerequisites

Before you begin, ensure you have the following installed on your machine:

- .NET SDK
- Visual Studio or Visual Studio Code

### Installation

1. **Clone the repository**:
   ```sh
   git clone https://github.com/Aditiighosh/demo-asp.net-app.git
   ```
2. **Navigate to the project directory**:
   ```sh
   cd demo-asp.net-app
   ```
3. **Restore the dependencies**:
   ```sh
   dotnet restore
   ```
4. **Run the application**:
   ```sh
   dotnet run
   ```

### Project Files

#### Models/WeatherForecast.cs

```csharp
using System;

namespace DemoApp.Models
{
    public class WeatherForecast
    {
        public DateTime Date { get; set; }
        public int TemperatureC { get; set; }
        public string Summary { get; set; }

        public int TemperatureF => 32 + (int)(TemperatureC / 0.5556);
    }
}
```

#### Controllers/HomeController.cs

```csharp
using Microsoft.AspNetCore.Mvc;
using DemoApp.Models;
using System;
using System.Collections.Generic;
using System.Linq;

namespace DemoApp.Controllers
{
    public class HomeController : Controller
    {
        private static readonly string[] Summaries = new[]
        {
            "Freezing", "Bracing", "Chilly", "Cool", "Mild", "Warm", "Balmy", "Hot", "Sweltering", "Scorching"
        };

        public IActionResult Index()
        {
            var rng = new Random();
            var forecasts = Enumerable.Range(1, 5).Select(index => new WeatherForecast
            {
                Date = DateTime.Now.AddDays(index),
                TemperatureC = rng.Next(-20, 55),
                Summary = Summaries[rng.Next(Summaries.Length)]
            })
            .ToArray();
            return View(forecasts);
        }

        public IActionResult Privacy()
        {
            return View();
        }
    }
}
```

#### Views/Home/Index.cshtml

```html
@model IEnumerable<DemoApp.Models.WeatherForecast>

@{
    ViewData["Title"] = "Home Page";
}

<div class="text-center">
    <h1 class="display-4">Welcome</h1>
    <p>ASP.NET Core MVC Application</p>
    <table class="table">
        <thead>
            <tr>
                <th>Date</th>
                <th>TemperatureC</th>
                <th>TemperatureF</th>
                <th>Summary</th>
            </tr>
        </thead>
        <tbody>
            @foreach (var forecast in Model)
            {
                <tr>
                    <td>@forecast.Date.ToShortDateString()</td>
                    <td>@forecast.TemperatureC</td>
                    <td>@forecast.TemperatureF</td>
                    <td>@forecast.Summary</td>
                </tr>
            }
        </tbody>
    </table>
</div>
```

#### Views/Home/Privacy.cshtml

```html
@{
    ViewData["Title"] = "Privacy Policy";
}

<h1>@ViewData["Title"]</h1>
<p>Use this page to detail your site's privacy policy.</p>
```

#### Views/Shared/_Layout.cshtml

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - DemoApp</title>
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css" />
</head>
<body>
    <header>
        <nav class="navbar navbar-expand-sm navbar-light bg-light">
            <a class="navbar-brand" href="/">DemoApp</a>
            <div class="collapse navbar-collapse">
                <ul class="navbar-nav">
                    <li class="nav-item">
                        <a class="nav-link" href="/">Home</a>
                    </li>
                    <li class="nav-item">
                        <a class="nav-link" href="/Home/Privacy">Privacy</a>
                    </li>
                </ul>
            </div>
        </nav>
    </header>
    <div class="container">
        <main role="main" class="pb-3">
            @RenderBody()
        </main>
    </div>
    <footer class="border-top footer text-muted">
        <div class="container">
            &copy; 2024 - DemoApp - <a href="/Home/Privacy">Privacy</a>
        </div>
    </footer>
</body>
</html>
```

### GitHub Repository

For more information and to access the complete codebase, visit the [GitHub repository](https://github.com/Aditiighosh/demo-asp.net-app).

### Performance Analysis

In-depth performance analysis of the application revealed satisfactory response times and efficient utilization of resources in typical usage scenarios. Through profiling tools and performance metrics within Visual Studio, any bottlenecks were identified and addressed to ensure optimal application responsiveness and scalability.
