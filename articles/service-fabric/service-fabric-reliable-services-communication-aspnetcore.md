---
title: Service communication with the ASP.NET Core | Microsoft Docs
description: Learn how to use ASP.NET Core in stateless and stateful Reliable Services.
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
ms.date: 03/22/2017
ms.author: vturecek
ms.openlocfilehash: 541a1efd9950e36860d161298d8b9d5c4f178d57
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551864"
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="5a801-103">ASP.NET Core in Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5a801-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="5a801-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span><span class="sxs-lookup"><span data-stu-id="5a801-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> <span data-ttu-id="5a801-105">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5a801-105">While ASP.NET Core apps can run on .NET Core or on the full .NET Framework, Service Fabric services currently can only run on the full .NET Framework.</span></span> <span data-ttu-id="5a801-106">This means when you build an ASP.NET Core Service Fabric service, you must still target the full .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5a801-106">This means when you build an ASP.NET Core Service Fabric service, you must still target the full .NET Framework.</span></span>

<span data-ttu-id="5a801-107">ASP.NET Core can be used in two different ways in Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="5a801-107">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="5a801-108">**Hosted as a guest executable**.</span><span class="sxs-lookup"><span data-stu-id="5a801-108">**Hosted as a guest executable**.</span></span> <span data-ttu-id="5a801-109">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span><span class="sxs-lookup"><span data-stu-id="5a801-109">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="5a801-110">**Run inside a Reliable Service**.</span><span class="sxs-lookup"><span data-stu-id="5a801-110">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="5a801-111">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span><span class="sxs-lookup"><span data-stu-id="5a801-111">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="5a801-112">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="5a801-112">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

> [!NOTE]
><span data-ttu-id="5a801-113">The rest of this article assumes you are familiar with hosting in ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="5a801-113">The rest of this article assumes you are familiar with hosting in ASP.NET Core.</span></span> <span data-ttu-id="5a801-114">To learn more about hosting in ASP.NET Core, see: [Introduction to hosting in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/hosting).</span><span class="sxs-lookup"><span data-stu-id="5a801-114">To learn more about hosting in ASP.NET Core, see: [Introduction to hosting in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/hosting).</span></span>

> [!NOTE]
> <span data-ttu-id="5a801-115">To develop Reliable Services with ASP.NET Core in Visual Studio 2015, you will need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span><span class="sxs-lookup"><span data-stu-id="5a801-115">To develop Reliable Services with ASP.NET Core in Visual Studio 2015, you will need to have [.NET Core VS 2015 Tooling Preview 2](https://www.microsoft.com/net/download/core) installed.</span></span>

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="5a801-116">Service Fabric service hosting</span><span class="sxs-lookup"><span data-stu-id="5a801-116">Service Fabric service hosting</span></span>
<span data-ttu-id="5a801-117">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span><span class="sxs-lookup"><span data-stu-id="5a801-117">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="5a801-118">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span><span class="sxs-lookup"><span data-stu-id="5a801-118">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="5a801-119">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="5a801-119">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="5a801-120">ASP.NET Core provides a separation between the web server and your web application.</span><span class="sxs-lookup"><span data-stu-id="5a801-120">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="5a801-121">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span><span class="sxs-lookup"><span data-stu-id="5a801-121">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="5a801-122">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span><span class="sxs-lookup"><span data-stu-id="5a801-122">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="5a801-123">ASP.NET Core self-hosting allows you to do this.</span><span class="sxs-lookup"><span data-stu-id="5a801-123">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="5a801-124">Hosting ASP.NET Core in a Reliable Service</span><span class="sxs-lookup"><span data-stu-id="5a801-124">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="5a801-125">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="5a801-125">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="5a801-126">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span><span class="sxs-lookup"><span data-stu-id="5a801-126">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Hosting ASP.NET Core in a process][0]

<span data-ttu-id="5a801-128">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span><span class="sxs-lookup"><span data-stu-id="5a801-128">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="5a801-129">The WebHost should be created in a Reliable Service itself.</span><span class="sxs-lookup"><span data-stu-id="5a801-129">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="5a801-130">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span><span class="sxs-lookup"><span data-stu-id="5a801-130">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="5a801-131">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="5a801-131">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="5a801-132">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span><span class="sxs-lookup"><span data-stu-id="5a801-132">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="5a801-133">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span><span class="sxs-lookup"><span data-stu-id="5a801-133">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or WebListener in a Reliable Service.</span></span>

![Hosting ASP.NET Core in a Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="5a801-135">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="5a801-135">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="5a801-136">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-136">The `ICommunicationListener` implementations for Kestrel and WebListener in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="5a801-137">Both communication listeners provide a constructor that takes the following arguments:</span><span class="sxs-lookup"><span data-stu-id="5a801-137">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="5a801-138">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span><span class="sxs-lookup"><span data-stu-id="5a801-138">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="5a801-139">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="5a801-139">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="5a801-140">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span><span class="sxs-lookup"><span data-stu-id="5a801-140">This is primarily where the two communication listeners differ: WebListener **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="5a801-141">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="5a801-141">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="5a801-142">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span><span class="sxs-lookup"><span data-stu-id="5a801-142">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="5a801-143">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span><span class="sxs-lookup"><span data-stu-id="5a801-143">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="5a801-144">That URL can then be modified or used as-is to start the web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-144">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="5a801-145">Service Fabric integration middleware</span><span class="sxs-lookup"><span data-stu-id="5a801-145">Service Fabric integration middleware</span></span>
<span data-ttu-id="5a801-146">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span><span class="sxs-lookup"><span data-stu-id="5a801-146">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="5a801-147">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span><span class="sxs-lookup"><span data-stu-id="5a801-147">This middleware configures the Kestrel or WebListener `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="5a801-148">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="5a801-148">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="5a801-149">This scenario is described in more detail in the next section.</span><span class="sxs-lookup"><span data-stu-id="5a801-149">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="5a801-150">A case of mistaken identity</span><span class="sxs-lookup"><span data-stu-id="5a801-150">A case of mistaken identity</span></span>
<span data-ttu-id="5a801-151">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span><span class="sxs-lookup"><span data-stu-id="5a801-151">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="5a801-152">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span><span class="sxs-lookup"><span data-stu-id="5a801-152">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="5a801-153">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a801-153">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="5a801-154">This can cause a client to mistakely connect to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="5a801-154">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="5a801-155">This can happen if the following sequence of events occur:</span><span class="sxs-lookup"><span data-stu-id="5a801-155">This can happen if the following sequence of events occur:</span></span>

 1. <span data-ttu-id="5a801-156">Service A listens on 10.0.0.1:30000 over HTTP.</span><span class="sxs-lookup"><span data-stu-id="5a801-156">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="5a801-157">Client resolves Service A and gets address 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="5a801-157">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="5a801-158">Service A moves to a different node.</span><span class="sxs-lookup"><span data-stu-id="5a801-158">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="5a801-159">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span><span class="sxs-lookup"><span data-stu-id="5a801-159">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="5a801-160">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="5a801-160">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="5a801-161">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="5a801-161">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="5a801-162">This can cause bugs at random times that can be difficult to diagnose.</span><span class="sxs-lookup"><span data-stu-id="5a801-162">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="5a801-163">Using unique service URLs</span><span class="sxs-lookup"><span data-stu-id="5a801-163">Using unique service URLs</span></span>
<span data-ttu-id="5a801-164">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span><span class="sxs-lookup"><span data-stu-id="5a801-164">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="5a801-165">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span><span class="sxs-lookup"><span data-stu-id="5a801-165">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="5a801-166">This does not provide secure service authentication in a hostile-tenant environment.</span><span class="sxs-lookup"><span data-stu-id="5a801-166">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="5a801-167">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span><span class="sxs-lookup"><span data-stu-id="5a801-167">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="5a801-168">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span><span class="sxs-lookup"><span data-stu-id="5a801-168">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="5a801-169">Services that use a dynamically-assigned port should make use of this middleware.</span><span class="sxs-lookup"><span data-stu-id="5a801-169">Services that use a dynamically-assigned port should make use of this middleware.</span></span>

<span data-ttu-id="5a801-170">Services that use a fixed unique port do not have this problem in a cooperative environment.</span><span class="sxs-lookup"><span data-stu-id="5a801-170">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="5a801-171">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span><span class="sxs-lookup"><span data-stu-id="5a801-171">A fixed unique port is typically used for externally-facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="5a801-172">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span><span class="sxs-lookup"><span data-stu-id="5a801-172">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="5a801-173">In this case, the unique identifier should not be enabled.</span><span class="sxs-lookup"><span data-stu-id="5a801-173">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="5a801-174">The following diagram shows the request flow with the middleware enabled:</span><span class="sxs-lookup"><span data-stu-id="5a801-174">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core integration][2]

<span data-ttu-id="5a801-176">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span><span class="sxs-lookup"><span data-stu-id="5a801-176">Both Kestrel and WebListener `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="5a801-177">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span><span class="sxs-lookup"><span data-stu-id="5a801-177">Although WebListener can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the WebListener `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="5a801-178">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span><span class="sxs-lookup"><span data-stu-id="5a801-178">That in turn makes it very difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="5a801-179">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span><span class="sxs-lookup"><span data-stu-id="5a801-179">Thus, both Kestrel and WebListener `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="weblistener-in-reliable-services"></a><span data-ttu-id="5a801-180">WebListener in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5a801-180">WebListener in Reliable Services</span></span>
<span data-ttu-id="5a801-181">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span><span class="sxs-lookup"><span data-stu-id="5a801-181">WebListener can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.WebListener** NuGet package.</span></span> <span data-ttu-id="5a801-182">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-182">This package contains `WebListenerCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using WebListener as the web server.</span></span>

<span data-ttu-id="5a801-183">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="5a801-183">WebListener is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="5a801-184">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span><span class="sxs-lookup"><span data-stu-id="5a801-184">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="5a801-185">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span><span class="sxs-lookup"><span data-stu-id="5a801-185">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="5a801-186">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="5a801-186">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

<span data-ttu-id="5a801-187">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span><span class="sxs-lookup"><span data-stu-id="5a801-187">The following diagram illustrates how WebListener uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="weblistener-in-a-stateless-service"></a><span data-ttu-id="5a801-189">WebListener in a stateless service</span><span class="sxs-lookup"><span data-stu-id="5a801-189">WebListener in a stateless service</span></span>
<span data-ttu-id="5a801-190">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="5a801-190">To use `WebListener` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `WebListenerCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseWebListener()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="weblistener-in-a-stateful-service"></a><span data-ttu-id="5a801-191">WebListener in a stateful service</span><span class="sxs-lookup"><span data-stu-id="5a801-191">WebListener in a stateful service</span></span>

<span data-ttu-id="5a801-192">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span><span class="sxs-lookup"><span data-stu-id="5a801-192">`WebListenerCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="5a801-193">For more information, see the following section on dynamic port allocation with WebListener.</span><span class="sxs-lookup"><span data-stu-id="5a801-193">For more information, see the following section on dynamic port allocation with WebListener.</span></span> <span data-ttu-id="5a801-194">For stateful services, Kestrel is the recommended web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-194">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="5a801-195">Endpoint configuration</span><span class="sxs-lookup"><span data-stu-id="5a801-195">Endpoint configuration</span></span>

<span data-ttu-id="5a801-196">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span><span class="sxs-lookup"><span data-stu-id="5a801-196">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including WebListener.</span></span> <span data-ttu-id="5a801-197">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span><span class="sxs-lookup"><span data-stu-id="5a801-197">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="5a801-198">This action requires elevated privileges that your services by default do not have.</span><span class="sxs-lookup"><span data-stu-id="5a801-198">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="5a801-199">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span><span class="sxs-lookup"><span data-stu-id="5a801-199">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="5a801-200">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="5a801-200">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

```xml
<ServiceManifest ... >
    ...
    <Resources>
        <Endpoints>
            <Endpoint Name="ServiceEndpoint" Protocol="http" Port="80" />
        </Endpoints>
    </Resources>

</ServiceManifest>
```

<span data-ttu-id="5a801-201">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="5a801-201">And the endpoint name must be passed to the `WebListenerCommunicationListener` constructor:</span></span>

```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseWebListener()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-weblistener-with-a-static-port"></a><span data-ttu-id="5a801-202">Use WebListener with a static port</span><span class="sxs-lookup"><span data-stu-id="5a801-202">Use WebListener with a static port</span></span>
<span data-ttu-id="5a801-203">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span><span class="sxs-lookup"><span data-stu-id="5a801-203">To use a static port with WebListener, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-weblistener-with-a-dynamic-port"></a><span data-ttu-id="5a801-204">Use WebListener with a dynamic port</span><span class="sxs-lookup"><span data-stu-id="5a801-204">Use WebListener with a dynamic port</span></span>
<span data-ttu-id="5a801-205">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span><span class="sxs-lookup"><span data-stu-id="5a801-205">To use a dynamically assigned port with WebListener, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="5a801-206">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span><span class="sxs-lookup"><span data-stu-id="5a801-206">Note that a dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="5a801-207">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span><span class="sxs-lookup"><span data-stu-id="5a801-207">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="5a801-208">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span><span class="sxs-lookup"><span data-stu-id="5a801-208">Multiple WebListener instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `WebListenerCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="5a801-209">For dynamic port usage, Kestrel is the recommended web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-209">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="5a801-210">Kestrel in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="5a801-210">Kestrel in Reliable Services</span></span>
<span data-ttu-id="5a801-211">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span><span class="sxs-lookup"><span data-stu-id="5a801-211">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="5a801-212">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span><span class="sxs-lookup"><span data-stu-id="5a801-212">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="5a801-213">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span><span class="sxs-lookup"><span data-stu-id="5a801-213">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="5a801-214">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="5a801-214">Unlike WebListener, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="5a801-215">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span><span class="sxs-lookup"><span data-stu-id="5a801-215">And unlike WebListener, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="5a801-216">Each instance of Kestrel must use a unique port.</span><span class="sxs-lookup"><span data-stu-id="5a801-216">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="5a801-218">Kestrel in a stateless service</span><span class="sxs-lookup"><span data-stu-id="5a801-218">Kestrel in a stateless service</span></span>
<span data-ttu-id="5a801-219">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="5a801-219">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="5a801-220">Kestrel in a stateful service</span><span class="sxs-lookup"><span data-stu-id="5a801-220">Kestrel in a stateful service</span></span>
<span data-ttu-id="5a801-221">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="5a801-221">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new ServiceReplicaListener[]
    {
        new ServiceReplicaListener(serviceContext =>
            new KestrelCommunicationListener(serviceContext, (url, listener) =>
                new WebHostBuilder()
                    .UseKestrel()
                    .ConfigureServices(
                         services => services
                             .AddSingleton<StatefulServiceContext>(serviceContext)
                             .AddSingleton<IReliableStateManager>(this.StateManager))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.UseUniqueServiceUrl)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build();
            ))
    };
}
```

<span data-ttu-id="5a801-222">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span><span class="sxs-lookup"><span data-stu-id="5a801-222">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="5a801-223">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span><span class="sxs-lookup"><span data-stu-id="5a801-223">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="5a801-224">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span><span class="sxs-lookup"><span data-stu-id="5a801-224">Note that an `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="5a801-225">This is explained in more detail in the following section.</span><span class="sxs-lookup"><span data-stu-id="5a801-225">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="5a801-226">Endpoint configuration</span><span class="sxs-lookup"><span data-stu-id="5a801-226">Endpoint configuration</span></span>
<span data-ttu-id="5a801-227">An `Endpoint` configuration is not required to use Kestrel.</span><span class="sxs-lookup"><span data-stu-id="5a801-227">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="5a801-228">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span><span class="sxs-lookup"><span data-stu-id="5a801-228">Kestrel is a simple stand-alone web server; unlike WebListener (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="5a801-229">Use Kestrel with a static port</span><span class="sxs-lookup"><span data-stu-id="5a801-229">Use Kestrel with a static port</span></span>
<span data-ttu-id="5a801-230">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span><span class="sxs-lookup"><span data-stu-id="5a801-230">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="5a801-231">Although this is not strictly necessary, it provides two potential benefits:</span><span class="sxs-lookup"><span data-stu-id="5a801-231">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="5a801-232">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="5a801-232">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="5a801-233">The URL provided to you through `KestrelCommunicationListener` will use this port.</span><span class="sxs-lookup"><span data-stu-id="5a801-233">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="5a801-234">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="5a801-234">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="5a801-235">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span><span class="sxs-lookup"><span data-stu-id="5a801-235">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="5a801-236">In this case, a dynamic port will be used.</span><span class="sxs-lookup"><span data-stu-id="5a801-236">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="5a801-237">See the next section for more information.</span><span class="sxs-lookup"><span data-stu-id="5a801-237">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="5a801-238">Use Kestrel with a dynamic port</span><span class="sxs-lookup"><span data-stu-id="5a801-238">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="5a801-239">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span><span class="sxs-lookup"><span data-stu-id="5a801-239">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="5a801-240">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span><span class="sxs-lookup"><span data-stu-id="5a801-240">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="5a801-241">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="5a801-241">To use dynamic port assignment with Kestrel, simply omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="5a801-242">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span><span class="sxs-lookup"><span data-stu-id="5a801-242">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="5a801-243">Scenarios and configurations</span><span class="sxs-lookup"><span data-stu-id="5a801-243">Scenarios and configurations</span></span>
<span data-ttu-id="5a801-244">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span><span class="sxs-lookup"><span data-stu-id="5a801-244">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="5a801-245">Externally exposed ASP.NET Core stateless service</span><span class="sxs-lookup"><span data-stu-id="5a801-245">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="5a801-246">Internal-only ASP.NET Core stateless service</span><span class="sxs-lookup"><span data-stu-id="5a801-246">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="5a801-247">Internal-only ASP.NET Core stateful service</span><span class="sxs-lookup"><span data-stu-id="5a801-247">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="5a801-248">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span><span class="sxs-lookup"><span data-stu-id="5a801-248">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="5a801-249">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a801-249">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="5a801-250">Stateful service endpoints generally should not be exposed to the Internet.</span><span class="sxs-lookup"><span data-stu-id="5a801-250">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="5a801-251">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span><span class="sxs-lookup"><span data-stu-id="5a801-251">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="5a801-252">Externally exposed ASP.NET Core stateless services</span><span class="sxs-lookup"><span data-stu-id="5a801-252">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="5a801-253">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span><span class="sxs-lookup"><span data-stu-id="5a801-253">WebListener is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints on Windows.</span></span> <span data-ttu-id="5a801-254">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span><span class="sxs-lookup"><span data-stu-id="5a801-254">It provides better protection against attacks and supports features that Kestrel does not, such as Windows Authentication and port sharing.</span></span> 

<span data-ttu-id="5a801-255">Kestrel is not supported as an edge (Internet-facing) server at this time.</span><span class="sxs-lookup"><span data-stu-id="5a801-255">Kestrel is not supported as an edge (Internet-facing) server at this time.</span></span> <span data-ttu-id="5a801-256">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span><span class="sxs-lookup"><span data-stu-id="5a801-256">A reverse proxy server such as IIS or Nginx must be used to handle traffic from the public Internet.</span></span>
 
<span data-ttu-id="5a801-257">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span><span class="sxs-lookup"><span data-stu-id="5a801-257">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="5a801-258">This is the URL you will provide to users of your application.</span><span class="sxs-lookup"><span data-stu-id="5a801-258">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="5a801-259">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="5a801-259">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="5a801-260">**Notes**</span><span class="sxs-lookup"><span data-stu-id="5a801-260">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a801-261">Web server</span><span class="sxs-lookup"><span data-stu-id="5a801-261">Web server</span></span> | <span data-ttu-id="5a801-262">WebListener</span><span class="sxs-lookup"><span data-stu-id="5a801-262">WebListener</span></span> | <span data-ttu-id="5a801-263">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span><span class="sxs-lookup"><span data-stu-id="5a801-263">If the service is only exposed to a trusted network, such an intranet, Kestrel may be used.</span></span> <span data-ttu-id="5a801-264">Otherwise, WebListener is the preferred option.</span><span class="sxs-lookup"><span data-stu-id="5a801-264">Otherwise, WebListener is the preferred option.</span></span> |
| <span data-ttu-id="5a801-265">Port configuration</span><span class="sxs-lookup"><span data-stu-id="5a801-265">Port configuration</span></span> | <span data-ttu-id="5a801-266">static</span><span class="sxs-lookup"><span data-stu-id="5a801-266">static</span></span> | <span data-ttu-id="5a801-267">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5a801-267">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="5a801-268">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="5a801-268">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="5a801-269">None</span><span class="sxs-lookup"><span data-stu-id="5a801-269">None</span></span> | <span data-ttu-id="5a801-270">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span><span class="sxs-lookup"><span data-stu-id="5a801-270">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="5a801-271">External users of your application will not know the unique identifying information used by the middleware.</span><span class="sxs-lookup"><span data-stu-id="5a801-271">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="5a801-272">Instance Count</span><span class="sxs-lookup"><span data-stu-id="5a801-272">Instance Count</span></span> | <span data-ttu-id="5a801-273">-1</span><span class="sxs-lookup"><span data-stu-id="5a801-273">-1</span></span> | <span data-ttu-id="5a801-274">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span><span class="sxs-lookup"><span data-stu-id="5a801-274">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="5a801-275">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span><span class="sxs-lookup"><span data-stu-id="5a801-275">If multiple externally exposed services share the same set of nodes, a unique but stable URL path should be used.</span></span> <span data-ttu-id="5a801-276">This can be accomplished by modifying the URL provided when configuring IWebHost.</span><span class="sxs-lookup"><span data-stu-id="5a801-276">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="5a801-277">Note this applies to WebListener only.</span><span class="sxs-lookup"><span data-stu-id="5a801-277">Note this applies to WebListener only.</span></span>

 ```csharp
 new WebListenerCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseWebListener()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="5a801-278">Internal-only stateless ASP.NET Core service</span><span class="sxs-lookup"><span data-stu-id="5a801-278">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="5a801-279">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span><span class="sxs-lookup"><span data-stu-id="5a801-279">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="5a801-280">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="5a801-280">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="5a801-281">**Notes**</span><span class="sxs-lookup"><span data-stu-id="5a801-281">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a801-282">Web server</span><span class="sxs-lookup"><span data-stu-id="5a801-282">Web server</span></span> | <span data-ttu-id="5a801-283">Kestrel</span><span class="sxs-lookup"><span data-stu-id="5a801-283">Kestrel</span></span> | <span data-ttu-id="5a801-284">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span><span class="sxs-lookup"><span data-stu-id="5a801-284">Although WebListener may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="5a801-285">Port configuration</span><span class="sxs-lookup"><span data-stu-id="5a801-285">Port configuration</span></span> | <span data-ttu-id="5a801-286">dynamically assigned</span><span class="sxs-lookup"><span data-stu-id="5a801-286">dynamically assigned</span></span> | <span data-ttu-id="5a801-287">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span><span class="sxs-lookup"><span data-stu-id="5a801-287">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="5a801-288">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="5a801-288">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="5a801-289">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="5a801-289">UseUniqueServiceUrl</span></span> | <span data-ttu-id="5a801-290">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span><span class="sxs-lookup"><span data-stu-id="5a801-290">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="5a801-291">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="5a801-291">InstanceCount</span></span> | <span data-ttu-id="5a801-292">any</span><span class="sxs-lookup"><span data-stu-id="5a801-292">any</span></span> | <span data-ttu-id="5a801-293">The instance count setting can be set to any value necessary to operate the service.</span><span class="sxs-lookup"><span data-stu-id="5a801-293">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="5a801-294">Internal-only stateful ASP.NET Core service</span><span class="sxs-lookup"><span data-stu-id="5a801-294">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="5a801-295">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span><span class="sxs-lookup"><span data-stu-id="5a801-295">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="5a801-296">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="5a801-296">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="5a801-297">**Notes**</span><span class="sxs-lookup"><span data-stu-id="5a801-297">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a801-298">Web server</span><span class="sxs-lookup"><span data-stu-id="5a801-298">Web server</span></span> | <span data-ttu-id="5a801-299">Kestrel</span><span class="sxs-lookup"><span data-stu-id="5a801-299">Kestrel</span></span> | <span data-ttu-id="5a801-300">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span><span class="sxs-lookup"><span data-stu-id="5a801-300">The `WebListenerCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="5a801-301">Port configuration</span><span class="sxs-lookup"><span data-stu-id="5a801-301">Port configuration</span></span> | <span data-ttu-id="5a801-302">dynamically assigned</span><span class="sxs-lookup"><span data-stu-id="5a801-302">dynamically assigned</span></span> | <span data-ttu-id="5a801-303">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span><span class="sxs-lookup"><span data-stu-id="5a801-303">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="5a801-304">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="5a801-304">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="5a801-305">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="5a801-305">UseUniqueServiceUrl</span></span> | <span data-ttu-id="5a801-306">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span><span class="sxs-lookup"><span data-stu-id="5a801-306">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5a801-307">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a801-307">Next steps</span></span>
[<span data-ttu-id="5a801-308">Debug your Service Fabric application by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a801-308">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png




