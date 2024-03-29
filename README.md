# What is This?

`BenMakesGames.MiniProfilerForBlazor` adds a service & component for displaying MiniProfiler results on a Blazor WebAssembly front-end.

[![Buy Me a Coffee at ko-fi.com](https://raw.githubusercontent.com/BenMakesGames/AssetsForNuGet/main/buymeacoffee.png)](https://ko-fi.com/A0A12KQ16)

# Installation & Configuration

## API Back-end Project

### Install MiniProfiler in API Project

Install & configure MiniProfiler: https://miniprofiler.com/dotnet/AspDotNetCore

* DON'T follow instructions for setting up `.cshtml` files; these do not apply to a Blazor WebAssembly project

### Validate Installation

1. Run the project, and view the website in your browser of choice
2. In the browser's developer tools, view the details for any XHR request
3. Verify that the response headers contains an `x-miniprofiler-ids` header
   * If the `x-miniprofiler-ids` header is not present, MiniProfiler has not been configured, and `MiniProfilerForBlazor` will not work

## WebAssembly Front-end Project

### Install this Package

Add `BenMakesGames.MiniProfilerForBlazor` to your Blazor WebAssembly project.

### Register Service

In your WebAssembly's `Program.cs`:

```c#
services.AddMiniProfilerForBlazor();
```

### Register Handler

#### Refit Client

```c#
services.AddRefitClient<...>() // <-- your refit client registration
    .AddMiniProfilerHandler(); // <-- add this
```

#### Standard HttpClient

```c#
services.AddHttpClient<...>() // <-- your http client registration
    .AddMiniProfilerHandler(); // <-- add this
```

### Add MiniProfiler to UI

In your `App.razor`, main layout, or wherever you want MiniProfiler to appear, add:

```html
@using BenMakesGames.MiniProfilerForBlazor.Components // or add this to your _Imports.razor; up to you

...

<MiniProfiler />
```

#### Component Options

* `int ZIndex` z-index to display the MiniProfiler button & panel; defaults to 9999
  * Example: `<MiniProfiler ZIndex="39" />`
