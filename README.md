# Basic API Caching App

Welcome to this basic example of caching with ASP.NET Core and Redis. This application features the ability to request weather forecasts from the [National Weather Service(NWS)](https://www.weather.gov/documentation/services-web-api) for weather forecasts in the United States. Given that in order to perform a weather forecast for any lat/lon point in the US you need to send 2 API requests, and because those values do not update more than once an hour, this application uses a Redis cache to short-circut those API requests, and build a more performant API.

## How It Works

This is a simple API application with 1 endpoint `/WeatherForecast` which is a GET request - you pass in a latitude and longitude as query parameters, and the application will check to see if the latitude and longitude have already been saved in redis, if they have, just pull it out of the cache, otherwise query the NWS's weather API for the correct office and grid points for the given lat/lon, and then query the NWS API for the forecast for the given location. It will then save the result in redis reply with a strongly typed response for the given location.

## Prerequistes

* IDE to write C# code - Visual Studio, Rider, VS Code, etc. . .
* [.NET 6 SDK](https://dotnet.microsoft.com/en-us/download/dotnet/6.0)
* [Docker](https://www.docker.com/products/docker-desktop)

## How to Run

* Start out by starting docker (if you are going to production you may want to consider using the [Redis Cloud](https://app.redislabs.com/)) `docker run -p 6379:6379 redis`
* Run the app with `dotnet run`
* Open the swagger GUI at [https://localhost:7045/swagger/index.html](https://localhost:7045/swagger/index.html)