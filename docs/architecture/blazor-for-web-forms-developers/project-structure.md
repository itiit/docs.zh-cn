---
title: Blazor 应用的项目结构
description: 了解 ASP.NET Web 窗体和 Blazor 项目的项目结构比较。
author: danroth27
ms.author: daroth
ms.date: 09/11/2019
ms.openlocfilehash: 2c383e86ff22f5a3460476998992b66e9417cc11
ms.sourcegitcommit: 559fcfbe4871636494870a8b716bf7325df34ac5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/30/2019
ms.locfileid: "73841905"
---
# <a name="project-structure-for-blazor-apps"></a><span data-ttu-id="31f14-103">Blazor 应用的项目结构</span><span class="sxs-lookup"><span data-stu-id="31f14-103">Project structure for Blazor apps</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="31f14-104">尽管它们的项目结构明显不同，ASP.NET Web 窗体和 Blazor 也共享许多类似的概念。</span><span class="sxs-lookup"><span data-stu-id="31f14-104">Despite their significant project structure differences, ASP.NET Web Forms and Blazor share many similar concepts.</span></span> <span data-ttu-id="31f14-105">在这里，我们将查看 Blazor 项目的结构，并将其与 ASP.NET Web 窗体项目进行比较。</span><span class="sxs-lookup"><span data-stu-id="31f14-105">Here, we'll look at the structure of a Blazor project and compare it to an ASP.NET Web Forms project.</span></span>

<span data-ttu-id="31f14-106">若要创建第一个 Blazor 应用，请按照[Blazor 入门步骤](/aspnet/core/blazor/get-started)中的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="31f14-106">To create your first Blazor app, follow the instructions in the [Blazor getting started steps](/aspnet/core/blazor/get-started).</span></span> <span data-ttu-id="31f14-107">可以按照说明在 ASP.NET Core 中创建托管的 Blazor 服务器应用或 Blazor WebAssembly 应用。</span><span class="sxs-lookup"><span data-stu-id="31f14-107">You can follow the instructions to create either a Blazor Server app or a Blazor WebAssembly app hosted in ASP.NET Core.</span></span> <span data-ttu-id="31f14-108">除了托管模型特定的逻辑外，这两个项目中的大多数代码都是相同的。</span><span class="sxs-lookup"><span data-stu-id="31f14-108">Except for the hosting model-specific logic, most of the code in both projects is the same.</span></span>

## <a name="project-file"></a><span data-ttu-id="31f14-109">项目文件</span><span class="sxs-lookup"><span data-stu-id="31f14-109">Project file</span></span>

<span data-ttu-id="31f14-110">Blazor 服务器应用程序是 .NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="31f14-110">Blazor Server apps are .NET Core projects.</span></span> <span data-ttu-id="31f14-111">Blazor 服务器应用程序的项目文件与它一样简单：</span><span class="sxs-lookup"><span data-stu-id="31f14-111">The project file for the Blazor Server app is about as simple as it can get:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netcoreapp3.0</TargetFramework>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="31f14-112">Blazor WebAssembly 应用程序的项目文件看起来稍微更多（具体版本号可能会有所不同）：</span><span class="sxs-lookup"><span data-stu-id="31f14-112">The project file for a Blazor WebAssembly app looks slightly more involved (exact version numbers may vary):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk.Web">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <RazorLangVersion>3.0</RazorLangVersion>
  </PropertyGroup>

  <ItemGroup>
    <PackageReference Include="Microsoft.AspNetCore.Blazor" Version="3.1.0" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.Build" Version="3.1.0" PrivateAssets="all" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.HttpClient" Version="3.1.0" />
    <PackageReference Include="Microsoft.AspNetCore.Blazor.DevServer" Version="3.1.0" PrivateAssets="all" />
  </ItemGroup>

  <ItemGroup>
    <ProjectReference Include="..\Shared\BlazorWebAssemblyApp1.Shared.csproj" />
  </ItemGroup>

</Project>
```

<span data-ttu-id="31f14-113">Blazor WebAssembly 项目目标 .NET Standard 而不是 .NET Core，因为它们在基于 WebAssembly 的 .NET 运行时上的浏览器中运行。</span><span class="sxs-lookup"><span data-stu-id="31f14-113">Blazor WebAssembly projects target .NET Standard instead of .NET Core because they run in the browser on a WebAssembly-based .NET runtime.</span></span> <span data-ttu-id="31f14-114">不能像在服务器或开发人员计算机上那样将 .NET 安装到 web 浏览器中。</span><span class="sxs-lookup"><span data-stu-id="31f14-114">You can't install .NET into a web browser like you can on a server or developer machine.</span></span> <span data-ttu-id="31f14-115">因此，该项目使用单独的包引用来引用 Blazor framework。</span><span class="sxs-lookup"><span data-stu-id="31f14-115">Consequently, the project references the Blazor framework using individual package references.</span></span>

<span data-ttu-id="31f14-116">相比之下，默认的 ASP.NET Web 窗体项目在其 *.csproj*文件中包含将近300行的 XML，其中的大多数行都显式列出了项目中的各种代码和内容文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-116">By comparison, a default ASP.NET Web Forms project includes almost 300 lines of XML in its *.csproj* file, most of which is explicitly listing the various code and content files in the project.</span></span> <span data-ttu-id="31f14-117">基于 .NET Core 和 .NET Standard 的项目中的许多简化来自通过引用 `Microsoft.NET.Sdk.Web` SDK 导入的默认目标和属性，通常称为 Web SDK。</span><span class="sxs-lookup"><span data-stu-id="31f14-117">Many of the simplifications in the .NET Core- and .NET Standard-based projects come from the default targets and properties imported by referencing the `Microsoft.NET.Sdk.Web` SDK, often referred to as simply the Web SDK.</span></span> <span data-ttu-id="31f14-118">Web SDK 包括通配符和其他很便利，用于简化在项目中包含的代码和内容文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-118">The Web SDK includes wildcards and other conveniences that simplify inclusion of code and content files in the project.</span></span> <span data-ttu-id="31f14-119">无需显式列出文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-119">You don't need to list the files explicitly.</span></span> <span data-ttu-id="31f14-120">面向 .NET Core 时，Web SDK 还添加了对 .NET Core 和 ASP.NET Core 共享框架的框架引用。</span><span class="sxs-lookup"><span data-stu-id="31f14-120">When targeting .NET Core, the Web SDK also adds framework references to both the .NET Core and ASP.NET Core shared frameworks.</span></span> <span data-ttu-id="31f14-121">可以从 "**解决方案资源管理器**" 窗口中的 "**依赖关系** > **框架**" 节点中查看框架。</span><span class="sxs-lookup"><span data-stu-id="31f14-121">The frameworks are visible from the **Dependencies** > **Frameworks** node in the **Solution Explorer** window.</span></span> <span data-ttu-id="31f14-122">共享框架是安装 .NET Core 时计算机上安装的程序集的集合。</span><span class="sxs-lookup"><span data-stu-id="31f14-122">The shared frameworks are collections of assemblies that were installed on the machine when installing .NET Core.</span></span>

<span data-ttu-id="31f14-123">尽管它们受支持，但在 .NET Core 项目中，各个程序集引用不太常见。</span><span class="sxs-lookup"><span data-stu-id="31f14-123">Although they're supported, individual assembly references are less common in .NET Core projects.</span></span> <span data-ttu-id="31f14-124">大多数项目依赖项都作为 NuGet 包引用处理。</span><span class="sxs-lookup"><span data-stu-id="31f14-124">Most project dependencies are handled as NuGet package references.</span></span> <span data-ttu-id="31f14-125">只需引用 .NET Core 项目中的顶级包依赖项。</span><span class="sxs-lookup"><span data-stu-id="31f14-125">You only need to reference top-level package dependencies in .NET Core projects.</span></span> <span data-ttu-id="31f14-126">自动包含可传递的依赖项。</span><span class="sxs-lookup"><span data-stu-id="31f14-126">Transitive dependencies are included automatically.</span></span> <span data-ttu-id="31f14-127">包引用会使用 `<PackageReference>` 元素添加到项目文件中，而不是使用 ASP.NET Web 窗体项目中常见的*包 .config*文件来引用包。</span><span class="sxs-lookup"><span data-stu-id="31f14-127">Instead of using the *packages.config* file commonly found in ASP.NET Web Forms projects to reference packages, package references are added to the project file using the `<PackageReference>` element.</span></span>

```xml
<ItemGroup>
  <PackageReference Include="Newtonsoft.Json" Version="12.0.2" />
</ItemGroup>
```

## <a name="entry-point"></a><span data-ttu-id="31f14-128">入口点</span><span class="sxs-lookup"><span data-stu-id="31f14-128">Entry point</span></span>

<span data-ttu-id="31f14-129">Blazor 服务器应用程序的入口点是在*Program.cs*文件中定义的，如控制台应用程序中所示。</span><span class="sxs-lookup"><span data-stu-id="31f14-129">The Blazor Server app's entry point is defined in the *Program.cs* file, as you would see in a Console app.</span></span> <span data-ttu-id="31f14-130">当应用程序执行时，它将使用特定于 web 应用的默认值创建并运行 web 主机实例。</span><span class="sxs-lookup"><span data-stu-id="31f14-130">When the app executes, it creates and runs a web host instance using defaults specific to web apps.</span></span> <span data-ttu-id="31f14-131">Web 主机管理 Blazor 服务器应用程序的生命周期，并设置主机级服务。</span><span class="sxs-lookup"><span data-stu-id="31f14-131">The web host manages the Blazor Server app's lifecycle and sets up host-level services.</span></span> <span data-ttu-id="31f14-132">此类服务的示例包括配置、日志记录、依赖关系注入和 HTTP 服务器。</span><span class="sxs-lookup"><span data-stu-id="31f14-132">Examples of such services are configuration, logging, dependency injection, and the HTTP server.</span></span> <span data-ttu-id="31f14-133">此代码主要是样板化的，通常保持不变。</span><span class="sxs-lookup"><span data-stu-id="31f14-133">This code is mostly boilerplate and is often left unchanged.</span></span>

```csharp
public class Program
{
    public static void Main(string[] args)
    {
        CreateHostBuilder(args).Build().Run();
    }

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseStartup<Startup>();
            });
}
```

<span data-ttu-id="31f14-134">Blazor WebAssembly apps 还定义*Program.cs*中的入口点。</span><span class="sxs-lookup"><span data-stu-id="31f14-134">Blazor WebAssembly apps also define an entry point in *Program.cs*.</span></span> <span data-ttu-id="31f14-135">代码看起来略有不同。</span><span class="sxs-lookup"><span data-stu-id="31f14-135">The code looks slightly different.</span></span> <span data-ttu-id="31f14-136">此代码类似于设置应用程序主机以向应用程序提供相同的主机级服务。</span><span class="sxs-lookup"><span data-stu-id="31f14-136">The code is similar in that it's setting up the app host to provide the same host-level services to the app.</span></span> <span data-ttu-id="31f14-137">不过，WebAssembly 应用主机不会设置 HTTP 服务器，因为它是直接在浏览器中执行的。</span><span class="sxs-lookup"><span data-stu-id="31f14-137">The WebAssembly app host doesn't, however, set up an HTTP server because it executes directly in the browser.</span></span>

<span data-ttu-id="31f14-138">Blazor 应用具有一个 `Startup` 类，而不是一个*global.asax*文件，用于定义应用的启动逻辑。</span><span class="sxs-lookup"><span data-stu-id="31f14-138">Blazor apps have a `Startup` class instead of a *Global.asax* file to define the startup logic for the app.</span></span> <span data-ttu-id="31f14-139">`Startup` 类用于配置应用程序和任何特定于应用程序的服务。</span><span class="sxs-lookup"><span data-stu-id="31f14-139">The `Startup` class is used to configure the app and any app-specific services.</span></span> <span data-ttu-id="31f14-140">在 Blazor 服务器应用中，`Startup` 类用于为客户端浏览器和服务器之间的 Blazor 使用的实时连接设置终结点。</span><span class="sxs-lookup"><span data-stu-id="31f14-140">In the Blazor Server app, the `Startup` class is used to set up the endpoint for the real-time connection used by Blazor between the client browsers and the server.</span></span> <span data-ttu-id="31f14-141">在 Blazor WebAssembly 应用中，`Startup` 类定义应用的根组件及其呈现位置。</span><span class="sxs-lookup"><span data-stu-id="31f14-141">In the Blazor WebAssembly app, the `Startup` class defines the root components for the app and where they should be rendered.</span></span> <span data-ttu-id="31f14-142">我们将深入了解[应用程序启动](./app-startup.md)部分中的 `Startup` 类。</span><span class="sxs-lookup"><span data-stu-id="31f14-142">We'll take a deeper look at the `Startup` class in the [App startup](./app-startup.md) section.</span></span>

## <a name="static-files"></a><span data-ttu-id="31f14-143">静态文件</span><span class="sxs-lookup"><span data-stu-id="31f14-143">Static files</span></span>

<span data-ttu-id="31f14-144">与 ASP.NET Web 窗体项目不同，Blazor 项目中的所有文件都不能被请求为静态文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-144">Unlike ASP.NET Web Forms projects, not all files in a Blazor project can be requested as static files.</span></span> <span data-ttu-id="31f14-145">只有*wwwroot*文件夹中的文件可通过 web 寻址。</span><span class="sxs-lookup"><span data-stu-id="31f14-145">Only the files in the *wwwroot* folder are web-addressable.</span></span> <span data-ttu-id="31f14-146">此文件夹被称为应用程序的 "web 根目录"。</span><span class="sxs-lookup"><span data-stu-id="31f14-146">This folder is referred to the app's "web root".</span></span> <span data-ttu-id="31f14-147">应用程序的 web 根目录之外的任何内容都*无法*进行 web 寻址。</span><span class="sxs-lookup"><span data-stu-id="31f14-147">Anything outside of the app's web root *isn't* web-addressable.</span></span> <span data-ttu-id="31f14-148">此设置提供了额外的安全级别，可防止在 web 上意外公开项目文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-148">This setup provides an additional level of security that prevents accidental exposing of project files over the web.</span></span>

## <a name="configuration"></a><span data-ttu-id="31f14-149">配置</span><span class="sxs-lookup"><span data-stu-id="31f14-149">Configuration</span></span>

<span data-ttu-id="31f14-150">ASP.NET Web 窗体应用中的配置通常使用一个或多个*web.config*文件进行处理。</span><span class="sxs-lookup"><span data-stu-id="31f14-150">Configuration in ASP.NET Web Forms apps is typically handled using one or more *web.config* files.</span></span> <span data-ttu-id="31f14-151">Blazor apps 通常*不包含 web.config 文件。*</span><span class="sxs-lookup"><span data-stu-id="31f14-151">Blazor apps don't typically have *web.config* files.</span></span> <span data-ttu-id="31f14-152">如果是这样，则在 IIS 上承载时，该文件仅用于配置 IIS 特定的设置。</span><span class="sxs-lookup"><span data-stu-id="31f14-152">If they do, the file is only used to configure IIS-specific settings when hosted on IIS.</span></span> <span data-ttu-id="31f14-153">相反，Blazor Server apps 使用 ASP.NET Core 配置抽象（Blazor WebAssembly 应用程序当前不支持相同的配置抽象，但这可能是将来添加的一项功能）。</span><span class="sxs-lookup"><span data-stu-id="31f14-153">Instead, Blazor Server apps use the ASP.NET Core configuration abstractions (Blazor WebAssembly apps don't currently support the same configuration abstractions, but that may be a feature added in the future).</span></span> <span data-ttu-id="31f14-154">例如，默认的 Blazor 服务器应用将一些设置存储在*appsettings*中。</span><span class="sxs-lookup"><span data-stu-id="31f14-154">For example, the default Blazor Server app stores some settings in *appsettings.json*.</span></span>

```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information"
    }
  },
  "AllowedHosts": "*"
}
```

<span data-ttu-id="31f14-155">有关配置的详细信息，请参阅[配置](./config.md)节 ASP.NET Core 项目。</span><span class="sxs-lookup"><span data-stu-id="31f14-155">We'll learn more about configuration in ASP.NET Core projects in the [Configuration](./config.md) section.</span></span>

## <a name="razor-components"></a><span data-ttu-id="31f14-156">Razor 组件</span><span class="sxs-lookup"><span data-stu-id="31f14-156">Razor components</span></span>

<span data-ttu-id="31f14-157">Blazor 项目中的大多数文件都是*razor*文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-157">Most files in Blazor projects are *.razor* files.</span></span> <span data-ttu-id="31f14-158">Razor 是基于 HTML C#的模板化语言，用于动态生成 web UI。</span><span class="sxs-lookup"><span data-stu-id="31f14-158">Razor is a templating language based on HTML and C# that is used to dynamically generate web UI.</span></span> <span data-ttu-id="31f14-159">*Razor*文件定义构成应用程序的 UI 的组件。</span><span class="sxs-lookup"><span data-stu-id="31f14-159">The *.razor* files define components that make up the UI of the app.</span></span> <span data-ttu-id="31f14-160">大多数情况下，Blazor 服务器和 Blazor WebAssembly 应用程序的组件都是相同的。</span><span class="sxs-lookup"><span data-stu-id="31f14-160">For the most part, the components are identical for both the Blazor Server and Blazor WebAssembly apps.</span></span> <span data-ttu-id="31f14-161">Blazor 中的组件类似于 ASP.NET Web 窗体中的用户控件。</span><span class="sxs-lookup"><span data-stu-id="31f14-161">Components in Blazor are analogous to user controls in ASP.NET Web Forms.</span></span>

<span data-ttu-id="31f14-162">生成项目时，每个 Razor 组件文件都将编译为 .NET 类。</span><span class="sxs-lookup"><span data-stu-id="31f14-162">Each Razor component file is compiled into a .NET class when the project is built.</span></span> <span data-ttu-id="31f14-163">生成的类捕获组件的状态、呈现逻辑、生命周期方法、事件处理程序和其他逻辑。</span><span class="sxs-lookup"><span data-stu-id="31f14-163">The generated class captures the component's state, rendering logic, lifecycle methods, event handlers, and other logic.</span></span> <span data-ttu-id="31f14-164">我们将在[使用 Blazor 构建可重复使用的 UI 组件](./components.md)部分中了解如何创作组件。</span><span class="sxs-lookup"><span data-stu-id="31f14-164">We'll look at authoring components in the [Building reusable UI components with Blazor](./components.md) section.</span></span>

<span data-ttu-id="31f14-165">*_Imports*文件不是 razor 组件文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-165">The *_Imports.razor* files aren't Razor component files.</span></span> <span data-ttu-id="31f14-166">相反，它们定义一组 Razor 指令以导入到同一文件夹及其子文件夹中的其他*razor*文件中。</span><span class="sxs-lookup"><span data-stu-id="31f14-166">Instead, they define a set of Razor directives to import into other *.razor* files within the same folder and in its subfolders.</span></span> <span data-ttu-id="31f14-167">例如， *_Imports razor*文件是为常用命名空间添加 `using` 语句的常规方法：</span><span class="sxs-lookup"><span data-stu-id="31f14-167">For example, a *_Imports.razor* file is a conventional way to add `using` statements for commonly used namespaces:</span></span>

```razor
@using System.Net.Http
@using Microsoft.AspNetCore.Authorization
@using Microsoft.AspNetCore.Components.Authorization
@using Microsoft.AspNetCore.Components.Forms
@using Microsoft.AspNetCore.Components.Routing
@using Microsoft.AspNetCore.Components.Web
@using Microsoft.JSInterop
@using BlazorApp1
@using BlazorApp1.Shared
```

## <a name="pages"></a><span data-ttu-id="31f14-168">Pages</span><span class="sxs-lookup"><span data-stu-id="31f14-168">Pages</span></span>

<span data-ttu-id="31f14-169">Blazor 应用中的页面位于何处？</span><span class="sxs-lookup"><span data-stu-id="31f14-169">Where are the pages in the Blazor apps?</span></span> <span data-ttu-id="31f14-170">Blazor 不会为可寻址页面定义单独的文件扩展名，例如 ASP.NET Web Forms apps 中的 *.aspx*文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-170">Blazor doesn't define a separate file extension for addressable pages, like the *.aspx* files in ASP.NET Web Forms apps.</span></span> <span data-ttu-id="31f14-171">而是通过将路由分配给组件来定义页面。</span><span class="sxs-lookup"><span data-stu-id="31f14-171">Instead, pages are defined by assigning routes to components.</span></span> <span data-ttu-id="31f14-172">通常使用 `@page` Razor 指令分配路由。</span><span class="sxs-lookup"><span data-stu-id="31f14-172">A route is typically assigned using the `@page` Razor directive.</span></span> <span data-ttu-id="31f14-173">例如，在*Pages/Counter*文件中编写的 `Counter` 组件定义了以下路由：</span><span class="sxs-lookup"><span data-stu-id="31f14-173">For example, the `Counter` component authored in the *Pages/Counter.razor* file defines the following route:</span></span>

```razor
@page "/counter"
```

<span data-ttu-id="31f14-174">Blazor 中的路由在客户端（而不是在服务器上）进行处理。</span><span class="sxs-lookup"><span data-stu-id="31f14-174">Routing in Blazor is handled client-side, not on the server.</span></span> <span data-ttu-id="31f14-175">当用户在浏览器中导航时，Blazor 会截获导航，然后用匹配的路由呈现组件。</span><span class="sxs-lookup"><span data-stu-id="31f14-175">As the user navigates in the browser, Blazor intercepts the navigation and then renders the component with the matching route.</span></span>

<span data-ttu-id="31f14-176">组件的文件位置目前不会推理组件路由，就像 *.aspx*页面一样。</span><span class="sxs-lookup"><span data-stu-id="31f14-176">The component routes aren't currently inferred by the component's file location like they are with *.aspx* pages.</span></span> <span data-ttu-id="31f14-177">将来可能会添加此功能。</span><span class="sxs-lookup"><span data-stu-id="31f14-177">This feature may be added in the future.</span></span> <span data-ttu-id="31f14-178">必须在组件上显式指定每个路由。</span><span class="sxs-lookup"><span data-stu-id="31f14-178">Each route must be specified explicitly on the component.</span></span> <span data-ttu-id="31f14-179">在 "*页面*" 文件夹中存储可路由的组件无特殊含义，只是一种约定。</span><span class="sxs-lookup"><span data-stu-id="31f14-179">Storing routable components in a *Pages* folder has no special meaning and is purely a convention.</span></span>

<span data-ttu-id="31f14-180">我们将在 "[页面"、"路由" 和 "布局](./pages-routing-layouts.md)" 部分的 Blazor 中更详细地介绍。</span><span class="sxs-lookup"><span data-stu-id="31f14-180">We'll look in greater detail at routing in Blazor in the [Pages, routing, and layouts](./pages-routing-layouts.md) section.</span></span>

## <a name="layout"></a><span data-ttu-id="31f14-181">布局</span><span class="sxs-lookup"><span data-stu-id="31f14-181">Layout</span></span>

<span data-ttu-id="31f14-182">在 ASP.NET Web 窗体应用程序中，使用*母版页（master*）处理公用页面布局。</span><span class="sxs-lookup"><span data-stu-id="31f14-182">In ASP.NET Web Forms apps, common page layout is handled using master pages (*Site.Master*).</span></span> <span data-ttu-id="31f14-183">在 Blazor 应用中，使用布局组件（*Shared/MainLayout*）处理页面布局。</span><span class="sxs-lookup"><span data-stu-id="31f14-183">In Blazor apps, page layout is handled using layout components (*Shared/MainLayout.razor*).</span></span> <span data-ttu-id="31f14-184">"[页面"、"路由" 和 "布局"](./pages-routing-layouts.md)部分中将更详细地讨论布局组件。</span><span class="sxs-lookup"><span data-stu-id="31f14-184">Layout components will be discussed in more detail in [Page, routing, and layouts](./pages-routing-layouts.md) section.</span></span>

## <a name="bootstrap-blazor"></a><span data-ttu-id="31f14-185">启动 Blazor</span><span class="sxs-lookup"><span data-stu-id="31f14-185">Bootstrap Blazor</span></span>

<span data-ttu-id="31f14-186">若要启动 Blazor，应用必须：</span><span class="sxs-lookup"><span data-stu-id="31f14-186">To bootstrap Blazor, the app must:</span></span>

- <span data-ttu-id="31f14-187">指定根组件（*app.config*）在页面上的呈现位置。</span><span class="sxs-lookup"><span data-stu-id="31f14-187">Specify where on the page the root component (*App.Razor*) should be rendered.</span></span>
- <span data-ttu-id="31f14-188">添加相应的 Blazor 框架脚本。</span><span class="sxs-lookup"><span data-stu-id="31f14-188">Add the corresponding Blazor framework script.</span></span>

<span data-ttu-id="31f14-189">在 Blazor 服务器应用程序中，根组件的 "主机" 页在 *_Host.* # 文件中定义。</span><span class="sxs-lookup"><span data-stu-id="31f14-189">In the Blazor Server app, the root component's host page is defined in the *_Host.cshtml* file.</span></span> <span data-ttu-id="31f14-190">此文件定义了一个 Razor 页面，而不是一个组件。</span><span class="sxs-lookup"><span data-stu-id="31f14-190">This file defines a Razor Page, not a component.</span></span> <span data-ttu-id="31f14-191">Razor Pages 使用 Razor 语法来定义服务器可寻址页面，与 *.aspx*页面非常类似。</span><span class="sxs-lookup"><span data-stu-id="31f14-191">Razor Pages use Razor syntax to define a server-addressable page, very much like an *.aspx* page.</span></span> <span data-ttu-id="31f14-192">`Html.RenderComponentAsync<TComponent>(RenderMode)` 方法用于定义根级别组件的呈现位置。</span><span class="sxs-lookup"><span data-stu-id="31f14-192">The `Html.RenderComponentAsync<TComponent>(RenderMode)` method is used to define where a root-level component should be rendered.</span></span> <span data-ttu-id="31f14-193">`RenderMode` 选项指示组件的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="31f14-193">The `RenderMode` option indicates the manner in which the component should be rendered.</span></span> <span data-ttu-id="31f14-194">下表概述了支持的 `RenderMode` 选项。</span><span class="sxs-lookup"><span data-stu-id="31f14-194">The following table outlines the supported `RenderMode` options.</span></span>

|<span data-ttu-id="31f14-195">选项</span><span class="sxs-lookup"><span data-stu-id="31f14-195">Option</span></span>                        |<span data-ttu-id="31f14-196">说明</span><span class="sxs-lookup"><span data-stu-id="31f14-196">Description</span></span>       |
|------------------------------|------------------|
|`RenderMode.Server`           |<span data-ttu-id="31f14-197">建立与浏览器的连接后交互呈现</span><span class="sxs-lookup"><span data-stu-id="31f14-197">Rendered interactively once a connection with the browser is established</span></span>|
|`RenderMode.ServerPrerendered`|<span data-ttu-id="31f14-198">首先预呈现并以交互方式呈现</span><span class="sxs-lookup"><span data-stu-id="31f14-198">First prerendered and then rendered interactively</span></span>|
|`RenderMode.Static`           |<span data-ttu-id="31f14-199">呈现为静态内容</span><span class="sxs-lookup"><span data-stu-id="31f14-199">Rendered as static content</span></span>|

<span data-ttu-id="31f14-200">*_Framework/blazor.server.js*的脚本引用与服务器建立实时连接，并处理所有用户交互和 UI 更新。</span><span class="sxs-lookup"><span data-stu-id="31f14-200">The script reference to *_framework/blazor.server.js* establishes the real-time connection with the server and then deals with all user interactions and UI updates.</span></span>

```razor
@page "/"
@namespace BlazorApp1.Pages
@addTagHelper *, Microsoft.AspNetCore.Mvc.TagHelpers

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>BlazorApp1</title>
    <base href="~/" />
    <link rel="stylesheet" href="css/bootstrap/bootstrap.min.css" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>
        @(await Html.RenderComponentAsync<App>(RenderMode.ServerPrerendered))
    </app>

    <script src="_framework/blazor.server.js"></script>
</body>
</html>
```

<span data-ttu-id="31f14-201">在 Blazor WebAssembly 应用中，"主机" 页是 " *wwwroot/index.html*" 下的简单静态 HTML 文件。</span><span class="sxs-lookup"><span data-stu-id="31f14-201">In the Blazor WebAssembly app, the host page is a simple static HTML file under *wwwroot/index.html*.</span></span> <span data-ttu-id="31f14-202">`<app>` 元素用来指示应呈现根组件的位置。</span><span class="sxs-lookup"><span data-stu-id="31f14-202">The `<app>` element is used to indicate where the root component should be rendered.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width" />
    <title>BlazorApp2</title>
    <base href="/" />
    <link href="css/bootstrap/bootstrap.min.css" rel="stylesheet" />
    <link href="css/site.css" rel="stylesheet" />
</head>
<body>
    <app>Loading...</app>

    <script src="_framework/blazor.webassembly.js"></script>
</body>
</html>
```

<span data-ttu-id="31f14-203">要呈现的特定组件在应用的 `Startup.Configure` 方法中进行配置，其中包含一个指示应在何处呈现组件的相应 CSS 选择器。</span><span class="sxs-lookup"><span data-stu-id="31f14-203">The specific component to render is configured in the app's `Startup.Configure` method with a corresponding CSS selector indicating where the component should be rendered.</span></span>

```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
    }

    public void Configure(IComponentsApplicationBuilder app)
    {
        app.AddComponent<App>("app");
    }
}
```

## <a name="build-output"></a><span data-ttu-id="31f14-204">生成输出</span><span class="sxs-lookup"><span data-stu-id="31f14-204">Build output</span></span>

<span data-ttu-id="31f14-205">生成 Blazor 项目时，所有 Razor 组件和代码文件都将编译为一个程序集。</span><span class="sxs-lookup"><span data-stu-id="31f14-205">When a Blazor project is built, all Razor component and code files are compiled into a single assembly.</span></span> <span data-ttu-id="31f14-206">与 ASP.NET Web 窗体项目不同，Blazor 不支持 UI 逻辑的运行时编译。</span><span class="sxs-lookup"><span data-stu-id="31f14-206">Unlike ASP.NET Web Forms projects, Blazor doesn't support runtime compilation of the UI logic.</span></span>

## <a name="run-the-app"></a><span data-ttu-id="31f14-207">运行应用</span><span class="sxs-lookup"><span data-stu-id="31f14-207">Run the app</span></span>

<span data-ttu-id="31f14-208">若要运行 Blazor 服务器应用，请在 Visual Studio 中按 `F5`。</span><span class="sxs-lookup"><span data-stu-id="31f14-208">To run the Blazor Server app, press `F5` in Visual Studio.</span></span> <span data-ttu-id="31f14-209">Blazor apps 不支持运行时编译。</span><span class="sxs-lookup"><span data-stu-id="31f14-209">Blazor apps don't support runtime compilation.</span></span> <span data-ttu-id="31f14-210">若要查看代码和组件标记更改的结果，请在附加调试器的情况下重新生成并重新启动应用。</span><span class="sxs-lookup"><span data-stu-id="31f14-210">To see the results of code and component markup changes, rebuild and restart the app with the debugger attached.</span></span> <span data-ttu-id="31f14-211">如果在未附加调试器的情况下运行（`Ctrl+F5`），则 Visual Studio 会监视文件更改，并在进行更改后重新启动应用。</span><span class="sxs-lookup"><span data-stu-id="31f14-211">If you run without the debugger attached (`Ctrl+F5`), Visual Studio watches for file changes and restarts the app as changes are made.</span></span> <span data-ttu-id="31f14-212">进行更改后，手动刷新浏览器。</span><span class="sxs-lookup"><span data-stu-id="31f14-212">You manually refresh the browser as changes are made.</span></span>

<span data-ttu-id="31f14-213">若要运行 Blazor WebAssembly 应用，请选择以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="31f14-213">To run the Blazor WebAssembly app, choose one of the following approaches:</span></span>

- <span data-ttu-id="31f14-214">使用开发服务器直接运行客户端项目。</span><span class="sxs-lookup"><span data-stu-id="31f14-214">Run the client project directly using the development server.</span></span>
- <span data-ttu-id="31f14-215">在将应用程序托管到 ASP.NET Core 时运行服务器项目。</span><span class="sxs-lookup"><span data-stu-id="31f14-215">Run the server project when hosting the app with ASP.NET Core.</span></span>

<span data-ttu-id="31f14-216">Blazor WebAssembly apps 不支持使用 Visual Studio 进行调试。</span><span class="sxs-lookup"><span data-stu-id="31f14-216">Blazor WebAssembly apps don't support debugging using Visual Studio.</span></span> <span data-ttu-id="31f14-217">若要运行应用，请使用 `Ctrl+F5` 而不是 `F5`。</span><span class="sxs-lookup"><span data-stu-id="31f14-217">To run the app, use `Ctrl+F5` instead of `F5`.</span></span> <span data-ttu-id="31f14-218">您可以改为直接在浏览器中调试 Blazor WebAssembly 应用程序。</span><span class="sxs-lookup"><span data-stu-id="31f14-218">You can instead debug Blazor WebAssembly apps directly in the browser.</span></span> <span data-ttu-id="31f14-219">有关详细信息，请参阅[Debug ASP.NET Core Blazor](/aspnet/core/blazor/debug) 。</span><span class="sxs-lookup"><span data-stu-id="31f14-219">See [Debug ASP.NET Core Blazor](/aspnet/core/blazor/debug) for details.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="31f14-220">[上一页](hosting-models.md)
>[下一页](app-startup.md)</span><span class="sxs-lookup"><span data-stu-id="31f14-220">[Previous](hosting-models.md)
[Next](app-startup.md)</span></span>