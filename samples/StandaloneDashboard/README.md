---
languages:
- csharp
products:
- dotnet
- dotnet-aspire
page_type: sample
name: "Standalone Aspire dashboard sample app"
urlFragment: "aspire-standalone-dashboard"
description: "A sample of using the Aspire dashboard to view telemetry from non-Aspire apps."
---

# Standalone Aspire dashboard sample app

The Aspire dashboard can be used to view OpenTelemetry data from any app. The dashboard supports running standalone, and any app can send it open telemetry.

This is a simple .NET app that downloads data from [PokeAPI](https://pokeapi.co/). The app sends telemetry to the Aspire dashboard which can be viewed in the dashboard telemetry UI.

![Screenshot of the standalone .NET Aspire dashboard](./images/aspire-dashboard-screenshot.png)

## Demonstrates

- How to run the Aspire dashboard from a Docker container
- How to configure a .NET app to export telemetry to the dashboard
- How to view telemetry in the Aspire dashboard

## Sample prerequisites

This sample is written in C# and targets .NET 8.0. It requires the [.NET 8.0 SDK](https://dotnet.microsoft.com/download/dotnet/8.0) or later.

This sample runs the Aspire dashboard from a Docker container. It requires Docker to be installed.

## Start Aspire dashboard

The following command starts the Aspire dashboard in a Docker container:

``` bash
docker run --rm -it -p 18888:18888 -p 4317:18889 -d --name aspire-dashboard mcr.microsoft.com/dotnet/nightly/aspire-dashboard:8.0.0-preview.4
```

The docker command:

* Starts a container from the `mcr.microsoft.com/dotnet/nightly/aspire-dashboard` image.
* The container has two ports:
  * Port `4317` receives OpenTelemetry data from apps. Apps send data using [OpenTelemetry Protocol (OTLP)](https://opentelemetry.io/docs/specs/otlp/).
  * Port `18888` has the dashboard UI. Navigate to http://localhost:18888 in the browser to view the dashboard.

## Building the sample

To download and run the sample, follow these steps:

1. Clone the `dotnet/aspire-samples` repository.
2. In Visual Studio (2022 or later):
    1. On the menu bar, choose **File** > **Open** > **Project/Solution**.
    2. Navigate to the folder that holds the sample code, and open the solution (.sln) file.
    3. Choose the <kbd>F5</kbd> key to run with debugging, or <kbd>Ctrl</kbd>+<kbd>F5</kbd> keys to run the project without debugging.
3. From the command line:
   1. Navigate to the folder that holds the sample code.
   2. At the command line, type [`dotnet run`](https://docs.microsoft.com/dotnet/core/tools/dotnet-run).

Run the .NET app by executing the following at the command prompt (opened to the base directory of the sample):

``` bash
dotnet run --project ConsoleApp
```

1. The console app launches, downloads information about all Pokemon and then exits.
2. View the Aspire dashboard at http://localhost:18888 to see app telemetry.
  1. View structured logs to see the list of downloaded Pokemon.
  2. View traces to see HTTP requests made.
  3. View metrics to see numeric data about the app such as average HTTP request duration.