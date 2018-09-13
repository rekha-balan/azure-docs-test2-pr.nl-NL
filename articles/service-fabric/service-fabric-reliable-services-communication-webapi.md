---
title: Service communication with the ASP.NET Web API | Microsoft Docs
description: Learn how to implement service communication step-by-step by using the ASP.NET Web API with OWIN self-hosting in the Reliable Services API.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: 8aa4668d-cbb6-4225-bd2d-ab5925a868f2
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 02/10/2017
ms.author: vturecek
redirect_url: /azure/service-fabric/service-fabric-reliable-services-communication-aspnetcore
ms.openlocfilehash: 3c29b4e5ba5ac821c3a0b0a03de2108814c9b14f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555375"
---
# <a name="get-started-service-fabric-web-api-services-with-owin-self-hosting"></a><span data-ttu-id="e839d-103">Get started: Service Fabric Web API services with OWIN self-hosting</span><span class="sxs-lookup"><span data-stu-id="e839d-103">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>
<span data-ttu-id="e839d-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span><span class="sxs-lookup"><span data-stu-id="e839d-104">Azure Service Fabric puts the power in your hands when you're deciding how you want your services to communicate with users and with each other.</span></span> <span data-ttu-id="e839d-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span><span class="sxs-lookup"><span data-stu-id="e839d-105">This tutorial focuses on implementing service communication using ASP.NET Web API with Open Web Interface for .NET (OWIN) self-hosting in Service Fabric's Reliable Services API.</span></span> <span data-ttu-id="e839d-106">We'll delve deeply into the Reliable Services pluggable communication API.</span><span class="sxs-lookup"><span data-stu-id="e839d-106">We'll delve deeply into the Reliable Services pluggable communication API.</span></span> <span data-ttu-id="e839d-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span><span class="sxs-lookup"><span data-stu-id="e839d-107">We'll also use Web API in a step-by-step example to show you how to set up a custom communication listener.</span></span>

## <a name="introduction-to-web-api-in-service-fabric"></a><span data-ttu-id="e839d-108">Introduction to Web API in Service Fabric</span><span class="sxs-lookup"><span data-stu-id="e839d-108">Introduction to Web API in Service Fabric</span></span>
<span data-ttu-id="e839d-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="e839d-109">ASP.NET Web API is a popular and powerful framework for building HTTP APIs on top of the .NET Framework.</span></span> <span data-ttu-id="e839d-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span><span class="sxs-lookup"><span data-stu-id="e839d-110">If you're not already familiar with the framework, see [Getting started with ASP.NET Web API 2](http://www.asp.net/web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api) to learn more.</span></span>

<span data-ttu-id="e839d-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span><span class="sxs-lookup"><span data-stu-id="e839d-111">Web API in Service Fabric is the same ASP.NET Web API you know and love.</span></span> <span data-ttu-id="e839d-112">The difference is in how you *host* a Web API application.</span><span class="sxs-lookup"><span data-stu-id="e839d-112">The difference is in how you *host* a Web API application.</span></span> <span data-ttu-id="e839d-113">You won't be using Microsoft Internet Information Services (IIS).</span><span class="sxs-lookup"><span data-stu-id="e839d-113">You won't be using Microsoft Internet Information Services (IIS).</span></span> <span data-ttu-id="e839d-114">To better understand the difference, let's break it into two parts:</span><span class="sxs-lookup"><span data-stu-id="e839d-114">To better understand the difference, let's break it into two parts:</span></span>

1. <span data-ttu-id="e839d-115">The Web API application (including controllers and models)</span><span class="sxs-lookup"><span data-stu-id="e839d-115">The Web API application (including controllers and models)</span></span>
2. <span data-ttu-id="e839d-116">The host (the web server, usually IIS)</span><span class="sxs-lookup"><span data-stu-id="e839d-116">The host (the web server, usually IIS)</span></span>

<span data-ttu-id="e839d-117">A Web API application itself doesn't change.</span><span class="sxs-lookup"><span data-stu-id="e839d-117">A Web API application itself doesn't change.</span></span> <span data-ttu-id="e839d-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span><span class="sxs-lookup"><span data-stu-id="e839d-118">It's no different from Web API applications you may have written in the past, and you should be able to simply move over most of your application code.</span></span> <span data-ttu-id="e839d-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span><span class="sxs-lookup"><span data-stu-id="e839d-119">But if you've been hosting on IIS, where you host the application may be a little different from what you're used to.</span></span> <span data-ttu-id="e839d-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span><span class="sxs-lookup"><span data-stu-id="e839d-120">Before we get to the hosting part, let's start with something more familiar: the Web API application.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="e839d-121">Create the application</span><span class="sxs-lookup"><span data-stu-id="e839d-121">Create the application</span></span>
<span data-ttu-id="e839d-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="e839d-122">Start by creating a new Service Fabric application with a single stateless service in Visual Studio 2015.</span></span>

<span data-ttu-id="e839d-123">A Visual Studio template for a stateless service using Web API is available to you.</span><span class="sxs-lookup"><span data-stu-id="e839d-123">A Visual Studio template for a stateless service using Web API is available to you.</span></span> <span data-ttu-id="e839d-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span><span class="sxs-lookup"><span data-stu-id="e839d-124">In this tutorial, we'll build a Web API project from scratch that results in what you'd get if you selected this template.</span></span>

<span data-ttu-id="e839d-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span><span class="sxs-lookup"><span data-stu-id="e839d-125">Select a blank Stateless Service project to learn how to build a Web API project from scratch, or you can start with the stateless service Web API template and simply follow along.</span></span>  

<span data-ttu-id="e839d-126">The first step is to pull in some NuGet packages for Web API.</span><span class="sxs-lookup"><span data-stu-id="e839d-126">The first step is to pull in some NuGet packages for Web API.</span></span> <span data-ttu-id="e839d-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span><span class="sxs-lookup"><span data-stu-id="e839d-127">The package we want to use is Microsoft.AspNet.WebApi.OwinSelfHost.</span></span> <span data-ttu-id="e839d-128">This package includes all the necessary Web API packages and the *host* packages.</span><span class="sxs-lookup"><span data-stu-id="e839d-128">This package includes all the necessary Web API packages and the *host* packages.</span></span> <span data-ttu-id="e839d-129">This will be important later.</span><span class="sxs-lookup"><span data-stu-id="e839d-129">This will be important later.</span></span>

<span data-ttu-id="e839d-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span><span class="sxs-lookup"><span data-stu-id="e839d-130">After the packages have been installed, you can begin building out the basic Web API project structure.</span></span> <span data-ttu-id="e839d-131">If you've used Web API, the project structure should look very familiar.</span><span class="sxs-lookup"><span data-stu-id="e839d-131">If you've used Web API, the project structure should look very familiar.</span></span> <span data-ttu-id="e839d-132">Start by adding a `Controllers` directory and a simple values controller:</span><span class="sxs-lookup"><span data-stu-id="e839d-132">Start by adding a `Controllers` directory and a simple values controller:</span></span>

<span data-ttu-id="e839d-133">**ValuesController.cs**</span><span class="sxs-lookup"><span data-stu-id="e839d-133">**ValuesController.cs**</span></span>

```csharp
using System.Collections.Generic;
using System.Web.Http;

namespace WebService.Controllers
{
    public class ValuesController : ApiController
    {
        // GET api/values 
        public IEnumerable<string> Get()
        {
            return new string[] { "value1", "value2" };
        }

        // GET api/values/5 
        public string Get(int id)
        {
            return "value";
        }

        // POST api/values 
        public void Post([FromBody]string value)
        {
        }

        // PUT api/values/5 
        public void Put(int id, [FromBody]string value)
        {
        }

        // DELETE api/values/5 
        public void Delete(int id)
        {
        }
    }
}

```

<span data-ttu-id="e839d-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span><span class="sxs-lookup"><span data-stu-id="e839d-134">Next, add a Startup class at the project root to register the routing, formatters, and any other configuration setup.</span></span> <span data-ttu-id="e839d-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span><span class="sxs-lookup"><span data-stu-id="e839d-135">This is also where Web API plugs in to the *host*, which will be revisited again later.</span></span> 

<span data-ttu-id="e839d-136">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="e839d-136">**Startup.cs**</span></span>

```csharp
using System.Web.Http;
using Owin;

namespace WebService
{
    public static class Startup
    {
        public static void ConfigureApp(IAppBuilder appBuilder)
        {
            // Configure Web API for self-host. 
            HttpConfiguration config = new HttpConfiguration();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            appBuilder.UseWebApi(config);
        }
    }
}
```

<span data-ttu-id="e839d-137">That's it for the application part.</span><span class="sxs-lookup"><span data-stu-id="e839d-137">That's it for the application part.</span></span> <span data-ttu-id="e839d-138">At this point, we've set up just the basic Web API project layout.</span><span class="sxs-lookup"><span data-stu-id="e839d-138">At this point, we've set up just the basic Web API project layout.</span></span> <span data-ttu-id="e839d-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span><span class="sxs-lookup"><span data-stu-id="e839d-139">So far, it shouldn't look much different from Web API projects you may have written in the past or from the basic Web API template.</span></span> <span data-ttu-id="e839d-140">Your business logic goes in the controllers and models as usual.</span><span class="sxs-lookup"><span data-stu-id="e839d-140">Your business logic goes in the controllers and models as usual.</span></span>

<span data-ttu-id="e839d-141">Now what do we do about hosting so that we can actually run it?</span><span class="sxs-lookup"><span data-stu-id="e839d-141">Now what do we do about hosting so that we can actually run it?</span></span>

## <a name="service-hosting"></a><span data-ttu-id="e839d-142">Service hosting</span><span class="sxs-lookup"><span data-stu-id="e839d-142">Service hosting</span></span>
<span data-ttu-id="e839d-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span><span class="sxs-lookup"><span data-stu-id="e839d-143">In Service Fabric, your service runs in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="e839d-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span><span class="sxs-lookup"><span data-stu-id="e839d-144">When you write a service by using the Reliable Services API, your service project just compiles to an executable file that registers your service type and runs your code.</span></span> <span data-ttu-id="e839d-145">This is true in most cases when you write a service on Service Fabric in .NET.</span><span class="sxs-lookup"><span data-stu-id="e839d-145">This is true in most cases when you write a service on Service Fabric in .NET.</span></span> <span data-ttu-id="e839d-146">When you open Program.cs in the stateless service project, you should see:</span><span class="sxs-lookup"><span data-stu-id="e839d-146">When you open Program.cs in the stateless service project, you should see:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Threading;
using Microsoft.ServiceFabric.Services.Runtime;

internal static class Program
{
    private static void Main()
    {
        try
        {
            ServiceRuntime.RegisterServiceAsync("WebServiceType",
                context => new WebService(context)).GetAwaiter().GetResult();

            ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(WebService).Name);

            // Prevents this host process from terminating so services keeps running. 
            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ServiceEventSource.Current.ServiceHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="e839d-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span><span class="sxs-lookup"><span data-stu-id="e839d-147">If that looks suspiciously like the entry point to a console application, that's because it is.</span></span>

<span data-ttu-id="e839d-148">Further details about the service host process and service registration are beyond the scope of this article.</span><span class="sxs-lookup"><span data-stu-id="e839d-148">Further details about the service host process and service registration are beyond the scope of this article.</span></span> <span data-ttu-id="e839d-149">But it's important to know for now that *your service code is running in its own process*.</span><span class="sxs-lookup"><span data-stu-id="e839d-149">But it's important to know for now that *your service code is running in its own process*.</span></span>

## <a name="self-host-web-api-with-an-owin-host"></a><span data-ttu-id="e839d-150">Self-host Web API with an OWIN host</span><span class="sxs-lookup"><span data-stu-id="e839d-150">Self-host Web API with an OWIN host</span></span>
<span data-ttu-id="e839d-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span><span class="sxs-lookup"><span data-stu-id="e839d-151">Given that your Web API application code is hosted in its own process, how do you hook it up to a web server?</span></span> <span data-ttu-id="e839d-152">Enter [OWIN](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="e839d-152">Enter [OWIN](http://owin.org/).</span></span> <span data-ttu-id="e839d-153">OWIN is simply a contract between .NET web applications and web servers.</span><span class="sxs-lookup"><span data-stu-id="e839d-153">OWIN is simply a contract between .NET web applications and web servers.</span></span> <span data-ttu-id="e839d-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span><span class="sxs-lookup"><span data-stu-id="e839d-154">Traditionally when ASP.NET (up to MVC 5) is used, the web application is tightly coupled to IIS through System.Web.</span></span> <span data-ttu-id="e839d-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span><span class="sxs-lookup"><span data-stu-id="e839d-155">However, Web API implements OWIN, so you can write a web application that is decoupled from the web server that hosts it.</span></span> <span data-ttu-id="e839d-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span><span class="sxs-lookup"><span data-stu-id="e839d-156">Because of this, you can use a *self-hosted* OWIN web server that you can start in your own process.</span></span> <span data-ttu-id="e839d-157">This fits perfectly with the Service Fabric hosting model we just described.</span><span class="sxs-lookup"><span data-stu-id="e839d-157">This fits perfectly with the Service Fabric hosting model we just described.</span></span>

<span data-ttu-id="e839d-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span><span class="sxs-lookup"><span data-stu-id="e839d-158">In this article, we'll use Katana as the OWIN host for the Web API application.</span></span> <span data-ttu-id="e839d-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span><span class="sxs-lookup"><span data-stu-id="e839d-159">Katana is an open-source OWIN host implementation built on [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx) and the Windows [HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="e839d-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span><span class="sxs-lookup"><span data-stu-id="e839d-160">To learn more about Katana, go to the [Katana site](http://www.asp.net/aspnet/overview/owin-and-katana/an-overview-of-project-katana).</span></span> <span data-ttu-id="e839d-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span><span class="sxs-lookup"><span data-stu-id="e839d-161">For a quick overview of how to use Katana to self-host Web API, see [Use OWIN to Self-Host ASP.NET Web API 2](http://www.asp.net/web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api).</span></span>
> 
> 

## <a name="set-up-the-web-server"></a><span data-ttu-id="e839d-162">Set up the web server</span><span class="sxs-lookup"><span data-stu-id="e839d-162">Set up the web server</span></span>
<span data-ttu-id="e839d-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span><span class="sxs-lookup"><span data-stu-id="e839d-163">The Reliable Services API provides a communication entry point where you can plug in communication stacks that allow users and clients to connect to the service:</span></span>

```csharp

protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}

```

<span data-ttu-id="e839d-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span><span class="sxs-lookup"><span data-stu-id="e839d-164">The web server (and any other communication stack you use in the future, such as WebSockets) should use the ICommunicationListener interface to integrate correctly with the system.</span></span> <span data-ttu-id="e839d-165">The reasons for this will become more apparent in the following steps.</span><span class="sxs-lookup"><span data-stu-id="e839d-165">The reasons for this will become more apparent in the following steps.</span></span>

<span data-ttu-id="e839d-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span><span class="sxs-lookup"><span data-stu-id="e839d-166">First, create a class called OwinCommunicationListener that implements ICommunicationListener:</span></span>

<span data-ttu-id="e839d-167">**OwinCommunicationListener.cs**</span><span class="sxs-lookup"><span data-stu-id="e839d-167">**OwinCommunicationListener.cs**</span></span>

```csharp
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;
using System;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        public void Abort()
        {
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
        }
    }
}
```

<span data-ttu-id="e839d-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span><span class="sxs-lookup"><span data-stu-id="e839d-168">The ICommunicationListener interface provides three methods to manage a communication listener for your service:</span></span>

* <span data-ttu-id="e839d-169">*OpenAsync*.</span><span class="sxs-lookup"><span data-stu-id="e839d-169">*OpenAsync*.</span></span> <span data-ttu-id="e839d-170">Start listening for requests.</span><span class="sxs-lookup"><span data-stu-id="e839d-170">Start listening for requests.</span></span>
* <span data-ttu-id="e839d-171">*CloseAsync*.</span><span class="sxs-lookup"><span data-stu-id="e839d-171">*CloseAsync*.</span></span> <span data-ttu-id="e839d-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span><span class="sxs-lookup"><span data-stu-id="e839d-172">Stop listening for requests, finish any in-flight requests, and shut down gracefully.</span></span>
* <span data-ttu-id="e839d-173">*Abort*.</span><span class="sxs-lookup"><span data-stu-id="e839d-173">*Abort*.</span></span> <span data-ttu-id="e839d-174">Cancel everything and stop immediately.</span><span class="sxs-lookup"><span data-stu-id="e839d-174">Cancel everything and stop immediately.</span></span>

<span data-ttu-id="e839d-175">To get started, add private class members for things the listener will need to function.</span><span class="sxs-lookup"><span data-stu-id="e839d-175">To get started, add private class members for things the listener will need to function.</span></span> <span data-ttu-id="e839d-176">These will be initialized through the constructor and used later when you set up the listening URL.</span><span class="sxs-lookup"><span data-stu-id="e839d-176">These will be initialized through the constructor and used later when you set up the listening URL.</span></span>

```csharp
internal class OwinCommunicationListener : ICommunicationListener
{
    private readonly ServiceEventSource eventSource;
    private readonly Action<IAppBuilder> startup;
    private readonly ServiceContext serviceContext;
    private readonly string endpointName;
    private readonly string appRoot;

    private IDisposable webApp;
    private string publishAddress;
    private string listeningAddress;

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
        : this(startup, serviceContext, eventSource, endpointName, null)
    {
    }

    public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
    {
        if (startup == null)
        {
            throw new ArgumentNullException(nameof(startup));
        }

        if (serviceContext == null)
        {
            throw new ArgumentNullException(nameof(serviceContext));
        }

        if (endpointName == null)
        {
            throw new ArgumentNullException(nameof(endpointName));
        }

        if (eventSource == null)
        {
            throw new ArgumentNullException(nameof(eventSource));
        }

        this.startup = startup;
        this.serviceContext = serviceContext;
        this.endpointName = endpointName;
        this.eventSource = eventSource;
        this.appRoot = appRoot;
    }


    ...

```

## <a name="implement-openasync"></a><span data-ttu-id="e839d-177">Implement OpenAsync</span><span class="sxs-lookup"><span data-stu-id="e839d-177">Implement OpenAsync</span></span>
<span data-ttu-id="e839d-178">To set up the web server, you need two pieces of information:</span><span class="sxs-lookup"><span data-stu-id="e839d-178">To set up the web server, you need two pieces of information:</span></span>

* <span data-ttu-id="e839d-179">*A URL path prefix*.</span><span class="sxs-lookup"><span data-stu-id="e839d-179">*A URL path prefix*.</span></span> <span data-ttu-id="e839d-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span><span class="sxs-lookup"><span data-stu-id="e839d-180">Although this is optional, it's good for you to set this up now so that you can safely host multiple web services in your application.</span></span>
* <span data-ttu-id="e839d-181">*A port*.</span><span class="sxs-lookup"><span data-stu-id="e839d-181">*A port*.</span></span>

<span data-ttu-id="e839d-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span><span class="sxs-lookup"><span data-stu-id="e839d-182">Before you get a port for the web server, it's important that you understand that Service Fabric provides an application layer that acts as a buffer between your application and the underlying operating system that it runs on.</span></span> <span data-ttu-id="e839d-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span><span class="sxs-lookup"><span data-stu-id="e839d-183">As such, Service Fabric provides a way to configure *endpoints* for your services.</span></span> <span data-ttu-id="e839d-184">Service Fabric ensures that endpoints are available for your service to use.</span><span class="sxs-lookup"><span data-stu-id="e839d-184">Service Fabric ensures that endpoints are available for your service to use.</span></span> <span data-ttu-id="e839d-185">This way, you don't have to configure them yourself in the underlying OS environment.</span><span class="sxs-lookup"><span data-stu-id="e839d-185">This way, you don't have to configure them yourself in the underlying OS environment.</span></span> <span data-ttu-id="e839d-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span><span class="sxs-lookup"><span data-stu-id="e839d-186">You can easily host your Service Fabric application in different environments without having to make any changes to your application.</span></span> <span data-ttu-id="e839d-187">(For example, you can host the same application in Azure or in your own datacenter.)</span><span class="sxs-lookup"><span data-stu-id="e839d-187">(For example, you can host the same application in Azure or in your own datacenter.)</span></span>

<span data-ttu-id="e839d-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="e839d-188">Configure an HTTP endpoint in PackageRoot\ServiceManifest.xml:</span></span>

```xml
<Resources>
    <Endpoints>
        <Endpoint Name="ServiceEndpoint" Type="Input" Protocol="http" Port="8281" />
    </Endpoints>
</Resources>

```

<span data-ttu-id="e839d-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span><span class="sxs-lookup"><span data-stu-id="e839d-189">This step is important because the service host process runs under restricted credentials (Network Service on Windows).</span></span> <span data-ttu-id="e839d-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span><span class="sxs-lookup"><span data-stu-id="e839d-190">This means that your service won't have access to set up an HTTP endpoint on its own.</span></span> <span data-ttu-id="e839d-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span><span class="sxs-lookup"><span data-stu-id="e839d-191">By using the endpoint configuration, Service Fabric knows to set up the proper access control list (ACL) for the URL that the service will listen on.</span></span> <span data-ttu-id="e839d-192">Service Fabric also provides a standard place to configure endpoints.</span><span class="sxs-lookup"><span data-stu-id="e839d-192">Service Fabric also provides a standard place to configure endpoints.</span></span>

<span data-ttu-id="e839d-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="e839d-193">Back in OwinCommunicationListener.cs, you can start implementing OpenAsync.</span></span> <span data-ttu-id="e839d-194">This is where you start the web server.</span><span class="sxs-lookup"><span data-stu-id="e839d-194">This is where you start the web server.</span></span> <span data-ttu-id="e839d-195">First, get the endpoint information and create the URL that the service will listen on.</span><span class="sxs-lookup"><span data-stu-id="e839d-195">First, get the endpoint information and create the URL that the service will listen on.</span></span> <span data-ttu-id="e839d-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span><span class="sxs-lookup"><span data-stu-id="e839d-196">The URL will be different depending on whether the listener is used in a stateless service or a stateful service.</span></span> <span data-ttu-id="e839d-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span><span class="sxs-lookup"><span data-stu-id="e839d-197">For a stateful service, the listener needs to create a unique address for every stateful service replica it listens on.</span></span> <span data-ttu-id="e839d-198">For stateless services, the address can be much simpler.</span><span class="sxs-lookup"><span data-stu-id="e839d-198">For stateless services, the address can be much simpler.</span></span> 

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
    var protocol = serviceEndpoint.Protocol;
    int port = serviceEndpoint.Port;

    if (this.serviceContext is StatefulServiceContext)
    {
        StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}{3}/{4}/{5}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/',
            statefulServiceContext.PartitionId,
            statefulServiceContext.ReplicaId,
            Guid.NewGuid());
    }
    else if (this.serviceContext is StatelessServiceContext)
    {
        this.listeningAddress = string.Format(
            CultureInfo.InvariantCulture,
            "{0}://+:{1}/{2}",
            protocol,
            port,
            string.IsNullOrWhiteSpace(this.appRoot)
                ? string.Empty
                : this.appRoot.TrimEnd('/') + '/');
    }
    else
    {
        throw new InvalidOperationException();
    }

    ...

```

<span data-ttu-id="e839d-199">Note that "http://+" is used here.</span><span class="sxs-lookup"><span data-stu-id="e839d-199">Note that "http://+" is used here.</span></span> <span data-ttu-id="e839d-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span><span class="sxs-lookup"><span data-stu-id="e839d-200">This is to make sure that the web server is listening on all available addresses, including localhost, FQDN, and the machine IP.</span></span>

<span data-ttu-id="e839d-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span><span class="sxs-lookup"><span data-stu-id="e839d-201">The OpenAsync implementation is one of the most important reasons why the web server (or any communication stack) is implemented as an ICommunicationListener, rather than just having it open directly from `RunAsync()` in the service.</span></span> <span data-ttu-id="e839d-202">The return value from OpenAsync is the address that the web server is listening on.</span><span class="sxs-lookup"><span data-stu-id="e839d-202">The return value from OpenAsync is the address that the web server is listening on.</span></span> <span data-ttu-id="e839d-203">When this address is returned to the system, it registers the address with the service.</span><span class="sxs-lookup"><span data-stu-id="e839d-203">When this address is returned to the system, it registers the address with the service.</span></span> <span data-ttu-id="e839d-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span><span class="sxs-lookup"><span data-stu-id="e839d-204">Service Fabric provides an API that allows clients and other services to then ask for this address by service name.</span></span> <span data-ttu-id="e839d-205">This is important because the service address is not static.</span><span class="sxs-lookup"><span data-stu-id="e839d-205">This is important because the service address is not static.</span></span> <span data-ttu-id="e839d-206">Services are moved around in the cluster for resource balancing and availability purposes.</span><span class="sxs-lookup"><span data-stu-id="e839d-206">Services are moved around in the cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="e839d-207">This is the mechanism that allows clients to resolve the listening address for a service.</span><span class="sxs-lookup"><span data-stu-id="e839d-207">This is the mechanism that allows clients to resolve the listening address for a service.</span></span>

<span data-ttu-id="e839d-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span><span class="sxs-lookup"><span data-stu-id="e839d-208">With that in mind, OpenAsync starts the web server and returns the address that it's listening on.</span></span> <span data-ttu-id="e839d-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span><span class="sxs-lookup"><span data-stu-id="e839d-209">Note that it listens on "http://+", but before OpenAsync returns the address, the "+" is replaced with the IP or FQDN of the node it is currently on.</span></span> <span data-ttu-id="e839d-210">The address that is returned by this method is what's registered with the system.</span><span class="sxs-lookup"><span data-stu-id="e839d-210">The address that is returned by this method is what's registered with the system.</span></span> <span data-ttu-id="e839d-211">It's also what clients and other services see when they ask for a service's address.</span><span class="sxs-lookup"><span data-stu-id="e839d-211">It's also what clients and other services see when they ask for a service's address.</span></span> <span data-ttu-id="e839d-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span><span class="sxs-lookup"><span data-stu-id="e839d-212">For clients to correctly connect to it, they need an actual IP or FQDN in the address.</span></span>

```csharp
    ...

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    try
    {
        this.eventSource.Message("Starting web server on " + this.listeningAddress);

        this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

        this.eventSource.Message("Listening on " + this.publishAddress);

        return Task.FromResult(this.publishAddress);
    }
    catch (Exception ex)
    {
        this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

        this.StopWebServer();

        throw;
    }
}

```

<span data-ttu-id="e839d-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span><span class="sxs-lookup"><span data-stu-id="e839d-213">Note that this references the Startup class that was passed in to the OwinCommunicationListener in the constructor.</span></span> <span data-ttu-id="e839d-214">This startup instance is used by the web server to bootstrap the Web API application.</span><span class="sxs-lookup"><span data-stu-id="e839d-214">This startup instance is used by the web server to bootstrap the Web API application.</span></span>

<span data-ttu-id="e839d-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span><span class="sxs-lookup"><span data-stu-id="e839d-215">The `ServiceEventSource.Current.Message()` line will appear in the Diagnostic Events window later, when you run the application to confirm that the web server has started successfully.</span></span>

## <a name="implement-closeasync-and-abort"></a><span data-ttu-id="e839d-216">Implement CloseAsync and Abort</span><span class="sxs-lookup"><span data-stu-id="e839d-216">Implement CloseAsync and Abort</span></span>
<span data-ttu-id="e839d-217">Finally, implement both CloseAsync and Abort to stop the web server.</span><span class="sxs-lookup"><span data-stu-id="e839d-217">Finally, implement both CloseAsync and Abort to stop the web server.</span></span> <span data-ttu-id="e839d-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span><span class="sxs-lookup"><span data-stu-id="e839d-218">The web server can be stopped by disposing the server handle that was created during OpenAsync.</span></span>

```csharp
public Task CloseAsync(CancellationToken cancellationToken)
{
    this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

    this.StopWebServer();

    return Task.FromResult(true);
}

public void Abort()
{
    this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

    this.StopWebServer();
}

private void StopWebServer()
{
    if (this.webApp != null)
    {
        try
        {
            this.webApp.Dispose();
        }
        catch (ObjectDisposedException)
        {
            // no-op
        }
    }
}
```

<span data-ttu-id="e839d-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span><span class="sxs-lookup"><span data-stu-id="e839d-219">In this implementation example, both CloseAsync and Abort simply stop the web server.</span></span> <span data-ttu-id="e839d-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span><span class="sxs-lookup"><span data-stu-id="e839d-220">You may opt to perform a more gracefully coordinated shutdown of the web server in CloseAsync.</span></span> <span data-ttu-id="e839d-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span><span class="sxs-lookup"><span data-stu-id="e839d-221">For example, the shutdown could wait for in-flight requests to be completed before the return.</span></span>

## <a name="start-the-web-server"></a><span data-ttu-id="e839d-222">Start the web server</span><span class="sxs-lookup"><span data-stu-id="e839d-222">Start the web server</span></span>
<span data-ttu-id="e839d-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span><span class="sxs-lookup"><span data-stu-id="e839d-223">You're now ready to create and return an instance of OwinCommunicationListener to start the web server.</span></span> <span data-ttu-id="e839d-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span><span class="sxs-lookup"><span data-stu-id="e839d-224">Back in the Service class (WebService.cs), override the `CreateServiceInstanceListeners()` method:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                           .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                           .Select(endpoint => endpoint.Name);

    return endpoints.Select(endpoint => new ServiceInstanceListener(
        serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
}
```

<span data-ttu-id="e839d-225">This is where the Web API *application* and the OWIN *host* finally meet.</span><span class="sxs-lookup"><span data-stu-id="e839d-225">This is where the Web API *application* and the OWIN *host* finally meet.</span></span> <span data-ttu-id="e839d-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span><span class="sxs-lookup"><span data-stu-id="e839d-226">The host (OwinCommunicationListener) is given an instance of the *application* (Web API) via the Startup class.</span></span> <span data-ttu-id="e839d-227">Service Fabric then manages its lifecycle.</span><span class="sxs-lookup"><span data-stu-id="e839d-227">Service Fabric then manages its lifecycle.</span></span> <span data-ttu-id="e839d-228">This same pattern can typically be followed with any communication stack.</span><span class="sxs-lookup"><span data-stu-id="e839d-228">This same pattern can typically be followed with any communication stack.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="e839d-229">Put it all together</span><span class="sxs-lookup"><span data-stu-id="e839d-229">Put it all together</span></span>
<span data-ttu-id="e839d-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span><span class="sxs-lookup"><span data-stu-id="e839d-230">In this example, you don't need to do anything in the `RunAsync()` method, so that override can simply be removed.</span></span>

<span data-ttu-id="e839d-231">The final service implementation should be very simple.</span><span class="sxs-lookup"><span data-stu-id="e839d-231">The final service implementation should be very simple.</span></span> <span data-ttu-id="e839d-232">It only needs to create the communication listener:</span><span class="sxs-lookup"><span data-stu-id="e839d-232">It only needs to create the communication listener:</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Fabric;
using System.Fabric.Description;
using System.Linq;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace WebService
{
    internal sealed class WebService : StatelessService
    {
        public WebService(StatelessServiceContext context)
            : base(context)
        { }

        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
            var endpoints = Context.CodePackageActivationContext.GetEndpoints()
                                   .Where(endpoint => endpoint.Protocol == EndpointProtocol.Http || endpoint.Protocol == EndpointProtocol.Https)
                                   .Select(endpoint => endpoint.Name);

            return endpoints.Select(endpoint => new ServiceInstanceListener(
                serviceContext => new OwinCommunicationListener(Startup.ConfigureApp, serviceContext, ServiceEventSource.Current, endpoint), endpoint));
        }
    }
}
```

<span data-ttu-id="e839d-233">The complete `OwinCommunicationListener` class:</span><span class="sxs-lookup"><span data-stu-id="e839d-233">The complete `OwinCommunicationListener` class:</span></span>

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Globalization;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Owin.Hosting;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Owin;

namespace WebService
{
    internal class OwinCommunicationListener : ICommunicationListener
    {
        private readonly ServiceEventSource eventSource;
        private readonly Action<IAppBuilder> startup;
        private readonly ServiceContext serviceContext;
        private readonly string endpointName;
        private readonly string appRoot;

        private IDisposable webApp;
        private string publishAddress;
        private string listeningAddress;

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName)
            : this(startup, serviceContext, eventSource, endpointName, null)
        {
        }

        public OwinCommunicationListener(Action<IAppBuilder> startup, ServiceContext serviceContext, ServiceEventSource eventSource, string endpointName, string appRoot)
        {
            if (startup == null)
            {
                throw new ArgumentNullException(nameof(startup));
            }

            if (serviceContext == null)
            {
                throw new ArgumentNullException(nameof(serviceContext));
            }

            if (endpointName == null)
            {
                throw new ArgumentNullException(nameof(endpointName));
            }

            if (eventSource == null)
            {
                throw new ArgumentNullException(nameof(eventSource));
            }

            this.startup = startup;
            this.serviceContext = serviceContext;
            this.endpointName = endpointName;
            this.eventSource = eventSource;
            this.appRoot = appRoot;
        }

        public Task<string> OpenAsync(CancellationToken cancellationToken)
        {
            var serviceEndpoint = this.serviceContext.CodePackageActivationContext.GetEndpoint(this.endpointName);
            var protocol = serviceEndpoint.Protocol;
            int port = serviceEndpoint.Port;

            if (this.serviceContext is StatefulServiceContext)
            {
                StatefulServiceContext statefulServiceContext = this.serviceContext as StatefulServiceContext;

                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}{3}/{4}/{5}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/',
                    statefulServiceContext.PartitionId,
                    statefulServiceContext.ReplicaId,
                    Guid.NewGuid());
            }
            else if (this.serviceContext is StatelessServiceContext)
            {
                this.listeningAddress = string.Format(
                    CultureInfo.InvariantCulture,
                    "{0}://+:{1}/{2}",
                    protocol,
                    port,
                    string.IsNullOrWhiteSpace(this.appRoot)
                        ? string.Empty
                        : this.appRoot.TrimEnd('/') + '/');
            }
            else
            {
                throw new InvalidOperationException();
            }

            this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

            try
            {
                this.eventSource.Message("Starting web server on " + this.listeningAddress);

                this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

                this.eventSource.Message("Listening on " + this.publishAddress);

                return Task.FromResult(this.publishAddress);
            }
            catch (Exception ex)
            {
                this.eventSource.Message("Web server failed to open endpoint {0}. {1}", this.endpointName, ex.ToString());

                this.StopWebServer();

                throw;
            }
        }

        public Task CloseAsync(CancellationToken cancellationToken)
        {
            this.eventSource.Message("Closing web server on endpoint {0}", this.endpointName);

            this.StopWebServer();

            return Task.FromResult(true);
        }

        public void Abort()
        {
            this.eventSource.Message("Aborting web server on endpoint {0}", this.endpointName);

            this.StopWebServer();
        }

        private void StopWebServer()
        {
            if (this.webApp != null)
            {
                try
                {
                    this.webApp.Dispose();
                }
                catch (ObjectDisposedException)
                {
                    // no-op
                }
            }
        }
    }
}
```

<span data-ttu-id="e839d-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span><span class="sxs-lookup"><span data-stu-id="e839d-234">Now that you have put all the pieces in place, your project should look like a typical Web API application with Reliable Services API entry points and an OWIN host.</span></span>

## <a name="run-and-connect-through-a-web-browser"></a><span data-ttu-id="e839d-235">Run and connect through a web browser</span><span class="sxs-lookup"><span data-stu-id="e839d-235">Run and connect through a web browser</span></span>
<span data-ttu-id="e839d-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e839d-236">If you haven't done so, [set up your development environment](service-fabric-get-started.md).</span></span>

<span data-ttu-id="e839d-237">You can now build and deploy your service.</span><span class="sxs-lookup"><span data-stu-id="e839d-237">You can now build and deploy your service.</span></span> <span data-ttu-id="e839d-238">Press **F5** in Visual Studio to build and deploy the application.</span><span class="sxs-lookup"><span data-stu-id="e839d-238">Press **F5** in Visual Studio to build and deploy the application.</span></span> <span data-ttu-id="e839d-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span><span class="sxs-lookup"><span data-stu-id="e839d-239">In the Diagnostic Events window, you should see a message that indicates that the web server opened on http://localhost:8281/.</span></span>

> [!NOTE]
> <span data-ttu-id="e839d-240">If the port has already been opened by another process on your machine, you may see an error here.</span><span class="sxs-lookup"><span data-stu-id="e839d-240">If the port has already been opened by another process on your machine, you may see an error here.</span></span> <span data-ttu-id="e839d-241">This indicates that the listener couldn't be opened.</span><span class="sxs-lookup"><span data-stu-id="e839d-241">This indicates that the listener couldn't be opened.</span></span> <span data-ttu-id="e839d-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="e839d-242">If that's the case, try using a different port for the endpoint configuration in ServiceManifest.xml.</span></span>
> 
> 

<span data-ttu-id="e839d-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span><span class="sxs-lookup"><span data-stu-id="e839d-243">Once the service is running, open a browser and navigate to [http://localhost:8281/api/values](http://localhost:8281/api/values) to test it.</span></span>

## <a name="scale-it-out"></a><span data-ttu-id="e839d-244">Scale it out</span><span class="sxs-lookup"><span data-stu-id="e839d-244">Scale it out</span></span>
<span data-ttu-id="e839d-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span><span class="sxs-lookup"><span data-stu-id="e839d-245">Scaling out stateless web apps typically means adding more machines and spinning up the web apps on them.</span></span> <span data-ttu-id="e839d-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span><span class="sxs-lookup"><span data-stu-id="e839d-246">Service Fabric's orchestration engine can do this for you whenever new nodes are added to a cluster.</span></span> <span data-ttu-id="e839d-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span><span class="sxs-lookup"><span data-stu-id="e839d-247">When you create instances of a stateless service, you can specify the number of instances you want to create.</span></span> <span data-ttu-id="e839d-248">Service Fabric places that number of instances on nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="e839d-248">Service Fabric places that number of instances on nodes in the cluster.</span></span> <span data-ttu-id="e839d-249">And it makes sure not to create more than one instance on any one node.</span><span class="sxs-lookup"><span data-stu-id="e839d-249">And it makes sure not to create more than one instance on any one node.</span></span> <span data-ttu-id="e839d-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span><span class="sxs-lookup"><span data-stu-id="e839d-250">You can also instruct Service Fabric to always create an instance on every node by specifying **-1** for the instance count.</span></span> <span data-ttu-id="e839d-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span><span class="sxs-lookup"><span data-stu-id="e839d-251">This guarantees that whenever you add nodes to scale out your cluster, an instance of your stateless service will be created on the new nodes.</span></span> <span data-ttu-id="e839d-252">This value is a property of the service instance, so it is set when you create a service instance.</span><span class="sxs-lookup"><span data-stu-id="e839d-252">This value is a property of the service instance, so it is set when you create a service instance.</span></span> <span data-ttu-id="e839d-253">You can do this through PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e839d-253">You can do this through PowerShell:</span></span>

```powershell

New-ServiceFabricService -ApplicationName "fabric:/WebServiceApplication" -ServiceName "fabric:/WebServiceApplication/WebService" -ServiceTypeName "WebServiceType" -Stateless -PartitionSchemeSingleton -InstanceCount -1

```

<span data-ttu-id="e839d-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span><span class="sxs-lookup"><span data-stu-id="e839d-254">You can also do this when you define a default service in a Visual Studio stateless service project:</span></span>

```xml

<DefaultServices>
  <Service Name="WebService">
    <StatelessService ServiceTypeName="WebServiceType" InstanceCount="-1">
      <SingletonPartition />
    </StatelessService>
  </Service>
</DefaultServices>

```

<span data-ttu-id="e839d-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span><span class="sxs-lookup"><span data-stu-id="e839d-255">For more information on how to create application and service instances, see [Deploy an application](service-fabric-deploy-remove-applications.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e839d-256">Next steps</span><span class="sxs-lookup"><span data-stu-id="e839d-256">Next steps</span></span>
[<span data-ttu-id="e839d-257">Debug your Service Fabric application by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e839d-257">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

