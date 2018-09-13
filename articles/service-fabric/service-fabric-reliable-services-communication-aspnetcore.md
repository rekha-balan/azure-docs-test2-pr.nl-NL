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
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 08/29/2018
ms.author: vturecek
ms.openlocfilehash: 439f02d5d62489a02473805d1223362cfff36eaf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44823958"
---
# <a name="aspnet-core-in-service-fabric-reliable-services"></a><span data-ttu-id="bbe6a-103">ASP.NET Core in Service Fabric Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bbe6a-103">ASP.NET Core in Service Fabric Reliable Services</span></span>

<span data-ttu-id="bbe6a-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-104">ASP.NET Core is a new open-source and cross-platform framework for building modern cloud-based Internet-connected applications, such as web apps, IoT apps, and mobile backends.</span></span> 

<span data-ttu-id="bbe6a-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.**\* set of NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-105">This article is an in-depth guide to hosting ASP.NET Core services in Service Fabric Reliable Services using the **Microsoft.ServiceFabric.AspNetCore.**\* set of NuGet packages.</span></span>

<span data-ttu-id="bbe6a-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment setup, see [Create a .NET application](service-fabric-tutorial-create-dotnet-app.md).</span><span class="sxs-lookup"><span data-stu-id="bbe6a-106">For an introductory tutorial on ASP.NET Core in Service Fabric and instructions on getting your development environment setup, see [Create a .NET application](service-fabric-tutorial-create-dotnet-app.md).</span></span>

<span data-ttu-id="bbe6a-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-107">The rest of this article assumes you are already familiar with ASP.NET Core.</span></span> <span data-ttu-id="bbe6a-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span><span class="sxs-lookup"><span data-stu-id="bbe6a-108">If not, we recommend reading through the [ASP.NET Core fundamentals](https://docs.microsoft.com/aspnet/core/fundamentals/index).</span></span>

## <a name="aspnet-core-in-the-service-fabric-environment"></a><span data-ttu-id="bbe6a-109">ASP.NET Core in the Service Fabric environment</span><span class="sxs-lookup"><span data-stu-id="bbe6a-109">ASP.NET Core in the Service Fabric environment</span></span>

<span data-ttu-id="bbe6a-110">Both ASP.NET Core and Service Fabric apps can run on .NET Core as well as full .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-110">Both ASP.NET Core and Service Fabric apps can run on .NET Core as well as full .NET Framework.</span></span> <span data-ttu-id="bbe6a-111">ASP.NET Core can be used in two different ways in Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-111">ASP.NET Core can be used in two different ways in Service Fabric:</span></span>
 - <span data-ttu-id="bbe6a-112">**Hosted as a guest executable**.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-112">**Hosted as a guest executable**.</span></span> <span data-ttu-id="bbe6a-113">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-113">This is primarily used to run existing ASP.NET Core applications on Service Fabric with no code changes.</span></span>
 - <span data-ttu-id="bbe6a-114">**Run inside a Reliable Service**.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-114">**Run inside a Reliable Service**.</span></span> <span data-ttu-id="bbe6a-115">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-115">This allows better integration with the Service Fabric runtime and allows stateful ASP.NET Core services.</span></span>

<span data-ttu-id="bbe6a-116">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-116">The rest of this article explains how to use ASP.NET Core inside a Reliable Service using the ASP.NET Core integration components that ship with the Service Fabric SDK.</span></span> 

## <a name="service-fabric-service-hosting"></a><span data-ttu-id="bbe6a-117">Service Fabric service hosting</span><span class="sxs-lookup"><span data-stu-id="bbe6a-117">Service Fabric service hosting</span></span>

<span data-ttu-id="bbe6a-118">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-118">In Service Fabric, one or more instances and/or replicas of your service run in a *service host process*, an executable file that runs your service code.</span></span> <span data-ttu-id="bbe6a-119">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-119">You, as a service author, own the service host process and Service Fabric activates and monitors it for you.</span></span>

<span data-ttu-id="bbe6a-120">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-120">Traditional ASP.NET (up to MVC 5) is tightly coupled to IIS through System.Web.dll.</span></span> <span data-ttu-id="bbe6a-121">ASP.NET Core provides a separation between the web server and your web application.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-121">ASP.NET Core provides a separation between the web server and your web application.</span></span> <span data-ttu-id="bbe6a-122">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-122">This allows web applications to be portable between different web servers and also allows web servers to be *self-hosted*, which means you can start a web server in your own process, as opposed to a process that is owned by dedicated web server software such as IIS.</span></span> 

<span data-ttu-id="bbe6a-123">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-123">In order to combine a Service Fabric service and ASP.NET, either as a guest executable or in a Reliable Service, you must be able to start ASP.NET inside your service host process.</span></span> <span data-ttu-id="bbe6a-124">ASP.NET Core self-hosting allows you to do this.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-124">ASP.NET Core self-hosting allows you to do this.</span></span>

## <a name="hosting-aspnet-core-in-a-reliable-service"></a><span data-ttu-id="bbe6a-125">Hosting ASP.NET Core in a Reliable Service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-125">Hosting ASP.NET Core in a Reliable Service</span></span>
<span data-ttu-id="bbe6a-126">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-126">Typically, self-hosted ASP.NET Core applications create a WebHost in an application's entry point, such as the `static void Main()` method in `Program.cs`.</span></span> <span data-ttu-id="bbe6a-127">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-127">In this case, the lifecycle of the WebHost is bound to the lifecycle of the process.</span></span>

![Hosting ASP.NET Core in a process][0]

<span data-ttu-id="bbe6a-129">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-129">However, the application entry point is not the right place to create a WebHost in a Reliable Service, because the application entry point is only used to register a service type with the Service Fabric runtime, so that it may create instances of that service type.</span></span> <span data-ttu-id="bbe6a-130">The WebHost should be created in a Reliable Service itself.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-130">The WebHost should be created in a Reliable Service itself.</span></span> <span data-ttu-id="bbe6a-131">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-131">Within the service host process, service instances and/or replicas can go through multiple lifecycles.</span></span> 

<span data-ttu-id="bbe6a-132">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-132">A Reliable Service instance is represented by your service class deriving from `StatelessService` or `StatefulService`.</span></span> <span data-ttu-id="bbe6a-133">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-133">The communication stack for a service is contained in an `ICommunicationListener` implementation in your service class.</span></span> <span data-ttu-id="bbe6a-134">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or HttpSys in a Reliable Service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-134">The `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages contain implementations of `ICommunicationListener` that start and manage the ASP.NET Core WebHost for either Kestrel or HttpSys in a Reliable Service.</span></span>

![Hosting ASP.NET Core in a Reliable Service][1]

## <a name="aspnet-core-icommunicationlisteners"></a><span data-ttu-id="bbe6a-136">ASP.NET Core ICommunicationListeners</span><span class="sxs-lookup"><span data-stu-id="bbe6a-136">ASP.NET Core ICommunicationListeners</span></span>
<span data-ttu-id="bbe6a-137">The `ICommunicationListener` implementations for Kestrel and HttpSys in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-137">The `ICommunicationListener` implementations for Kestrel and HttpSys in the  `Microsoft.ServiceFabric.Services.AspNetCore.*` NuGet packages have similar use patterns but perform slightly different actions specific to each web server.</span></span> 

<span data-ttu-id="bbe6a-138">Both communication listeners provide a constructor that takes the following arguments:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-138">Both communication listeners provide a constructor that takes the following arguments:</span></span>
 - <span data-ttu-id="bbe6a-139">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-139">**`ServiceContext serviceContext`**: The `ServiceContext` object that contains information about the running service.</span></span>
 - <span data-ttu-id="bbe6a-140">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-140">**`string endpointName`**: the name of an `Endpoint` configuration in ServiceManifest.xml.</span></span> <span data-ttu-id="bbe6a-141">This is primarily where the two communication listeners differ: HttpSys **requires** an `Endpoint` configuration, while Kestrel does not.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-141">This is primarily where the two communication listeners differ: HttpSys **requires** an `Endpoint` configuration, while Kestrel does not.</span></span>
 - <span data-ttu-id="bbe6a-142">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-142">**`Func<string, AspNetCoreCommunicationListener, IWebHost> build`**: a lambda that you implement in which you create and return an `IWebHost`.</span></span> <span data-ttu-id="bbe6a-143">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-143">This allows you to configure `IWebHost` the way you normally would in an ASP.NET Core application.</span></span> <span data-ttu-id="bbe6a-144">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-144">The lambda provides a URL which is generated for you depending on the Service Fabric integration options you use and the `Endpoint` configuration you provide.</span></span> <span data-ttu-id="bbe6a-145">That URL can then be modified or used as-is to start the web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-145">That URL can then be modified or used as-is to start the web server.</span></span>

## <a name="service-fabric-integration-middleware"></a><span data-ttu-id="bbe6a-146">Service Fabric integration middleware</span><span class="sxs-lookup"><span data-stu-id="bbe6a-146">Service Fabric integration middleware</span></span>
<span data-ttu-id="bbe6a-147">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-147">The `Microsoft.ServiceFabric.Services.AspNetCore` NuGet package includes the `UseServiceFabricIntegration` extension method on `IWebHostBuilder` that adds Service Fabric-aware middleware.</span></span> <span data-ttu-id="bbe6a-148">This middleware configures the Kestrel or HttpSys `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-148">This middleware configures the Kestrel or HttpSys `ICommunicationListener` to register a unique service URL with the Service Fabric Naming Service and then validates client requests to ensure clients are connecting to the right service.</span></span> <span data-ttu-id="bbe6a-149">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-149">This is necessary in a shared-host environment such as Service Fabric, where multiple web applications can run on the same physical or virtual machine but do not use unique host names, to prevent clients from mistakenly connecting to the wrong service.</span></span> <span data-ttu-id="bbe6a-150">This scenario is described in more detail in the next section.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-150">This scenario is described in more detail in the next section.</span></span>

### <a name="a-case-of-mistaken-identity"></a><span data-ttu-id="bbe6a-151">A case of mistaken identity</span><span class="sxs-lookup"><span data-stu-id="bbe6a-151">A case of mistaken identity</span></span>
<span data-ttu-id="bbe6a-152">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-152">Service replicas, regardless of protocol, listen on a unique IP:port combination.</span></span> <span data-ttu-id="bbe6a-153">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-153">Once a service replica has started listening on an IP:port endpoint, it reports that endpoint address to the Service Fabric Naming Service where it can be discovered by clients or other services.</span></span> <span data-ttu-id="bbe6a-154">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-154">If services use dynamically-assigned application ports, a service replica may coincidentally use the same IP:port endpoint of another service that was previously on the same physical or virtual machine.</span></span> <span data-ttu-id="bbe6a-155">This can cause a client to mistakely connect to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-155">This can cause a client to mistakely connect to the wrong service.</span></span> <span data-ttu-id="bbe6a-156">This can happen if the following sequence of events occurs:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-156">This can happen if the following sequence of events occurs:</span></span>

 1. <span data-ttu-id="bbe6a-157">Service A listens on 10.0.0.1:30000 over HTTP.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-157">Service A listens on 10.0.0.1:30000 over HTTP.</span></span> 
 2. <span data-ttu-id="bbe6a-158">Client resolves Service A and gets address 10.0.0.1:30000</span><span class="sxs-lookup"><span data-stu-id="bbe6a-158">Client resolves Service A and gets address 10.0.0.1:30000</span></span>
 3. <span data-ttu-id="bbe6a-159">Service A moves to a different node.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-159">Service A moves to a different node.</span></span>
 4. <span data-ttu-id="bbe6a-160">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-160">Service B is placed on 10.0.0.1 and coincidentally uses the same port 30000.</span></span>
 5. <span data-ttu-id="bbe6a-161">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-161">Client attempts to connect to service A with cached address 10.0.0.1:30000.</span></span>
 6. <span data-ttu-id="bbe6a-162">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-162">Client is now successfully connected to service B not realizing it is connected to the wrong service.</span></span>

<span data-ttu-id="bbe6a-163">This can cause bugs at random times that can be difficult to diagnose.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-163">This can cause bugs at random times that can be difficult to diagnose.</span></span> 

### <a name="using-unique-service-urls"></a><span data-ttu-id="bbe6a-164">Using unique service URLs</span><span class="sxs-lookup"><span data-stu-id="bbe6a-164">Using unique service URLs</span></span>
<span data-ttu-id="bbe6a-165">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-165">To prevent this, services can post an endpoint to the Naming Service with a unique identifier, and then validate that unique identifier during client requests.</span></span> <span data-ttu-id="bbe6a-166">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-166">This is a cooperative action between services in a non-hostile-tenant trusted environment.</span></span> <span data-ttu-id="bbe6a-167">This does not provide secure service authentication in a hostile-tenant environment.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-167">This does not provide secure service authentication in a hostile-tenant environment.</span></span>

<span data-ttu-id="bbe6a-168">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-168">In a trusted environment, the middleware that's added by the `UseServiceFabricIntegration` method automatically appends a unique identifier to the address that is posted to the Naming Service and validates that identifier on each request.</span></span> <span data-ttu-id="bbe6a-169">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-169">If the identifier does not match, the middleware immediately returns an HTTP 410 Gone response.</span></span>

<span data-ttu-id="bbe6a-170">Services that use a dynamically assigned port should make use of this middleware.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-170">Services that use a dynamically assigned port should make use of this middleware.</span></span>

<span data-ttu-id="bbe6a-171">Services that use a fixed unique port do not have this problem in a cooperative environment.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-171">Services that use a fixed unique port do not have this problem in a cooperative environment.</span></span> <span data-ttu-id="bbe6a-172">A fixed unique port is typically used for externally facing services that need a well-known port for client applications to connect to.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-172">A fixed unique port is typically used for externally facing services that need a well-known port for client applications to connect to.</span></span> <span data-ttu-id="bbe6a-173">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-173">For example, most Internet-facing web applications will use port 80 or 443 for web browser connections.</span></span> <span data-ttu-id="bbe6a-174">In this case, the unique identifier should not be enabled.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-174">In this case, the unique identifier should not be enabled.</span></span>

<span data-ttu-id="bbe6a-175">The following diagram shows the request flow with the middleware enabled:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-175">The following diagram shows the request flow with the middleware enabled:</span></span>

![Service Fabric ASP.NET Core integration][2]

<span data-ttu-id="bbe6a-177">Both Kestrel and HttpSys `ICommunicationListener` implementations use this mechanism in exactly the same way.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-177">Both Kestrel and HttpSys `ICommunicationListener` implementations use this mechanism in exactly the same way.</span></span> <span data-ttu-id="bbe6a-178">Although HttpSys can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the HttpSys `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-178">Although HttpSys can internally differentiate requests based on unique URL paths using the underlying *http.sys* port sharing feature, that functionality is *not* used by the HttpSys `ICommunicationListener` implementation because that will result in HTTP 503 and HTTP 404 error status codes in the scenario described earlier.</span></span> <span data-ttu-id="bbe6a-179">That in turn makes it difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-179">That in turn makes it difficult for clients to determine the intent of the error, as HTTP 503 and HTTP 404 are already commonly used to indicate other errors.</span></span> <span data-ttu-id="bbe6a-180">Thus, both Kestrel and HttpSys `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-180">Thus, both Kestrel and HttpSys `ICommunicationListener` implementations standardize on the middleware provided by the `UseServiceFabricIntegration` extension method so that clients only need to perform a service endpoint re-resolve action on HTTP 410 responses.</span></span>

## <a name="httpsys-in-reliable-services"></a><span data-ttu-id="bbe6a-181">HttpSys in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bbe6a-181">HttpSys in Reliable Services</span></span>
<span data-ttu-id="bbe6a-182">HttpSys can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.HttpSys** NuGet package.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-182">HttpSys can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.HttpSys** NuGet package.</span></span> <span data-ttu-id="bbe6a-183">This package contains `HttpSysCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using HttpSys as the web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-183">This package contains `HttpSysCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using HttpSys as the web server.</span></span>

<span data-ttu-id="bbe6a-184">HttpSys is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span><span class="sxs-lookup"><span data-stu-id="bbe6a-184">HttpSys is built on the [Windows HTTP Server API](https://msdn.microsoft.com/library/windows/desktop/aa364510(v=vs.85).aspx).</span></span> <span data-ttu-id="bbe6a-185">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-185">This uses the *http.sys* kernel driver used by IIS to process HTTP requests and route them to processes running web applications.</span></span> <span data-ttu-id="bbe6a-186">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-186">This allows multiple processes on the same physical or virtual machine to host web applications on the same port, disambiguated by either a unique URL path or hostname.</span></span> <span data-ttu-id="bbe6a-187">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-187">These features are useful in Service Fabric for hosting multiple websites in the same cluster.</span></span>

>[!NOTE]
><span data-ttu-id="bbe6a-188">HttpSys implementation works only on Windows platform.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-188">HttpSys implementation works only on Windows platform.</span></span>

<span data-ttu-id="bbe6a-189">The following diagram illustrates how HttpSys uses the *http.sys* kernel driver on Windows for port sharing:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-189">The following diagram illustrates how HttpSys uses the *http.sys* kernel driver on Windows for port sharing:</span></span>

![http.sys][3]

### <a name="httpsys-in-a-stateless-service"></a><span data-ttu-id="bbe6a-191">HttpSys in a stateless service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-191">HttpSys in a stateless service</span></span>
<span data-ttu-id="bbe6a-192">To use `HttpSys` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `HttpSysCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-192">To use `HttpSys` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `HttpSysCommunicationListener` instance:</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    return new ServiceInstanceListener[]
    {
        new ServiceInstanceListener(serviceContext =>
            new HttpSysCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
                new WebHostBuilder()
                    .UseHttpSys()
                    .ConfigureServices(
                        services => services
                            .AddSingleton<StatelessServiceContext>(serviceContext))
                    .UseContentRoot(Directory.GetCurrentDirectory())
                    .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
                    .UseStartup<Startup>()
                    .UseUrls(url)
                    .Build()))
    };
}
```

### <a name="httpsys-in-a-stateful-service"></a><span data-ttu-id="bbe6a-193">HttpSys in a stateful service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-193">HttpSys in a stateful service</span></span>

<span data-ttu-id="bbe6a-194">`HttpSysCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-194">`HttpSysCommunicationListener` is currently not designed for use in stateful services due to complications with the underlying *http.sys* port sharing feature.</span></span> <span data-ttu-id="bbe6a-195">For more information, see the following section on dynamic port allocation with HttpSys.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-195">For more information, see the following section on dynamic port allocation with HttpSys.</span></span> <span data-ttu-id="bbe6a-196">For stateful services, Kestrel is the recommended web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-196">For stateful services, Kestrel is the recommended web server.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="bbe6a-197">Endpoint configuration</span><span class="sxs-lookup"><span data-stu-id="bbe6a-197">Endpoint configuration</span></span>

<span data-ttu-id="bbe6a-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including HttpSys.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-198">An `Endpoint` configuration is required for web servers that use the Windows HTTP Server API, including HttpSys.</span></span> <span data-ttu-id="bbe6a-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span><span class="sxs-lookup"><span data-stu-id="bbe6a-199">Web servers that use the Windows HTTP Server API must first reserve their URL with *http.sys* (this is normally accomplished with the [netsh](https://msdn.microsoft.com/library/windows/desktop/cc307236(v=vs.85).aspx) tool).</span></span> <span data-ttu-id="bbe6a-200">This action requires elevated privileges that your services by default do not have.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-200">This action requires elevated privileges that your services by default do not have.</span></span> <span data-ttu-id="bbe6a-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-201">The "http" or "https" options for the `Protocol` property of the `Endpoint` configuration in *ServiceManifest.xml* are used specifically to instruct the Service Fabric runtime to register a URL with *http.sys* on your behalf using the [*strong wildcard*](https://msdn.microsoft.com/library/windows/desktop/aa364698(v=vs.85).aspx) URL prefix.</span></span>

<span data-ttu-id="bbe6a-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-202">For example, to reserve `http://+:80` for a service, the following configuration should be used in ServiceManifest.xml:</span></span>

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

<span data-ttu-id="bbe6a-203">And the endpoint name must be passed to the `HttpSysCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-203">And the endpoint name must be passed to the `HttpSysCommunicationListener` constructor:</span></span>

```csharp
 new HttpSysCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     return new WebHostBuilder()
         .UseHttpSys()
         .UseServiceFabricIntegration(listener, ServiceFabricIntegrationOptions.None)
         .UseUrls(url)
         .Build();
 })
```

#### <a name="use-httpsys-with-a-static-port"></a><span data-ttu-id="bbe6a-204">Use HttpSys with a static port</span><span class="sxs-lookup"><span data-stu-id="bbe6a-204">Use HttpSys with a static port</span></span>
<span data-ttu-id="bbe6a-205">To use a static port with HttpSys, provide the port number in the `Endpoint` configuration:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-205">To use a static port with HttpSys, provide the port number in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

#### <a name="use-httpsys-with-a-dynamic-port"></a><span data-ttu-id="bbe6a-206">Use HttpSys with a dynamic port</span><span class="sxs-lookup"><span data-stu-id="bbe6a-206">Use HttpSys with a dynamic port</span></span>
<span data-ttu-id="bbe6a-207">To use a dynamically assigned port with HttpSys, omit the `Port` property in the `Endpoint` configuration:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-207">To use a dynamically assigned port with HttpSys, omit the `Port` property in the `Endpoint` configuration:</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bbe6a-208">A dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-208">A dynamic port allocated by an `Endpoint` configuration only provides one port *per host process*.</span></span> <span data-ttu-id="bbe6a-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-209">The current Service Fabric hosting model allows multiple service instances and/or replicas to be hosted in the same process, meaning that each one will share the same port when allocated through the `Endpoint` configuration.</span></span> <span data-ttu-id="bbe6a-210">Multiple HttpSys instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `HttpSysCommunicationListener` due to the complications it introduces for client requests.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-210">Multiple HttpSys instances can share a port using the underlying *http.sys* port sharing feature, but that is not supported by `HttpSysCommunicationListener` due to the complications it introduces for client requests.</span></span> <span data-ttu-id="bbe6a-211">For dynamic port usage, Kestrel is the recommended web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-211">For dynamic port usage, Kestrel is the recommended web server.</span></span>

## <a name="kestrel-in-reliable-services"></a><span data-ttu-id="bbe6a-212">Kestrel in Reliable Services</span><span class="sxs-lookup"><span data-stu-id="bbe6a-212">Kestrel in Reliable Services</span></span>
<span data-ttu-id="bbe6a-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-213">Kestrel can be used in a Reliable Service by importing the **Microsoft.ServiceFabric.AspNetCore.Kestrel** NuGet package.</span></span> <span data-ttu-id="bbe6a-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-214">This package contains `KestrelCommunicationListener`, an implementation of `ICommunicationListener`, that allows you to create an ASP.NET Core WebHost inside a Reliable Service using Kestrel as the web server.</span></span>

<span data-ttu-id="bbe6a-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-215">Kestrel is a cross-platform web server for ASP.NET Core based on libuv, a cross-platform asynchronous I/O library.</span></span> <span data-ttu-id="bbe6a-216">Unlike HttpSys, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-216">Unlike HttpSys, Kestrel does not use a centralized endpoint manager such as *http.sys*.</span></span> <span data-ttu-id="bbe6a-217">And unlike HttpSys, Kestrel does not support port sharing between multiple processes.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-217">And unlike HttpSys, Kestrel does not support port sharing between multiple processes.</span></span> <span data-ttu-id="bbe6a-218">Each instance of Kestrel must use a unique port.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-218">Each instance of Kestrel must use a unique port.</span></span>

![kestrel][4]

### <a name="kestrel-in-a-stateless-service"></a><span data-ttu-id="bbe6a-220">Kestrel in a stateless service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-220">Kestrel in a stateless service</span></span>
<span data-ttu-id="bbe6a-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-221">To use `Kestrel` in a stateless service, override the `CreateServiceInstanceListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

### <a name="kestrel-in-a-stateful-service"></a><span data-ttu-id="bbe6a-222">Kestrel in a stateful service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-222">Kestrel in a stateful service</span></span>
<span data-ttu-id="bbe6a-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-223">To use `Kestrel` in a stateful service, override the `CreateServiceReplicaListeners` method and return a `KestrelCommunicationListener` instance:</span></span>

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

<span data-ttu-id="bbe6a-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-224">In this example, a singleton instance of `IReliableStateManager` is provided to the WebHost dependency injection container.</span></span> <span data-ttu-id="bbe6a-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-225">This is not strictly necessary, but it allows you to use `IReliableStateManager` and Reliable Collections in your MVC controller action methods.</span></span>

<span data-ttu-id="bbe6a-226">An `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-226">An `Endpoint` configuration name is **not** provided to `KestrelCommunicationListener` in a stateful service.</span></span> <span data-ttu-id="bbe6a-227">This is explained in more detail in the following section.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-227">This is explained in more detail in the following section.</span></span>

### <a name="endpoint-configuration"></a><span data-ttu-id="bbe6a-228">Endpoint configuration</span><span class="sxs-lookup"><span data-stu-id="bbe6a-228">Endpoint configuration</span></span>
<span data-ttu-id="bbe6a-229">An `Endpoint` configuration is not required to use Kestrel.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-229">An `Endpoint` configuration is not required to use Kestrel.</span></span> 

<span data-ttu-id="bbe6a-230">Kestrel is a simple stand-alone web server; unlike HttpSys (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-230">Kestrel is a simple stand-alone web server; unlike HttpSys (or HttpListener), it does not need an `Endpoint` configuration in *ServiceManifest.xml* because it does not require URL registration prior to starting.</span></span> 

#### <a name="use-kestrel-with-a-static-port"></a><span data-ttu-id="bbe6a-231">Use Kestrel with a static port</span><span class="sxs-lookup"><span data-stu-id="bbe6a-231">Use Kestrel with a static port</span></span>
<span data-ttu-id="bbe6a-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-232">A static port can be configured in the `Endpoint` configuration of ServiceManifest.xml for use with Kestrel.</span></span> <span data-ttu-id="bbe6a-233">Although this is not strictly necessary, it provides two potential benefits:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-233">Although this is not strictly necessary, it provides two potential benefits:</span></span>
 1. <span data-ttu-id="bbe6a-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-234">If the port does not fall in the application port range, it is opened through the OS firewall by Service Fabric.</span></span>
 2. <span data-ttu-id="bbe6a-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-235">The URL provided to you through `KestrelCommunicationListener` will use this port.</span></span>

```xml
  <Resources>
    <Endpoints>
      <Endpoint Protocol="http" Name="ServiceEndpoint" Port="80" />
    </Endpoints>
  </Resources>
```

<span data-ttu-id="bbe6a-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-236">If an `Endpoint` is configured, its name must be passed into the `KestrelCommunicationListener` constructor:</span></span> 

```csharp
new KestrelCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) => ...
```

<span data-ttu-id="bbe6a-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-237">If an `Endpoint` configuration is not used, omit the name in the `KestrelCommunicationListener` constructor.</span></span> <span data-ttu-id="bbe6a-238">In this case, a dynamic port will be used.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-238">In this case, a dynamic port will be used.</span></span> <span data-ttu-id="bbe6a-239">See the next section for more information.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-239">See the next section for more information.</span></span>

#### <a name="use-kestrel-with-a-dynamic-port"></a><span data-ttu-id="bbe6a-240">Use Kestrel with a dynamic port</span><span class="sxs-lookup"><span data-stu-id="bbe6a-240">Use Kestrel with a dynamic port</span></span>
<span data-ttu-id="bbe6a-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-241">Kestrel cannot use the automatic port assignment from the `Endpoint` configuration in ServiceManifest.xml, because automatic port assignment from an `Endpoint` configuration assigns a unique port per *host process*, and a single host process can contain multiple Kestrel instances.</span></span> <span data-ttu-id="bbe6a-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-242">Since Kestrel does not support port sharing, this does not work as each Kestrel instance must be opened on a unique port.</span></span>

<span data-ttu-id="bbe6a-243">To use dynamic port assignment with Kestrel, omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-243">To use dynamic port assignment with Kestrel, omit the `Endpoint` configuration in ServiceManifest.xml entirely, and do not pass an endpoint name to the `KestrelCommunicationListener` constructor:</span></span>

```csharp
new KestrelCommunicationListener(serviceContext, (url, listener) => ...
```

<span data-ttu-id="bbe6a-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-244">In this configuration, `KestrelCommunicationListener` will automatically select an unused port from the application port range.</span></span>

## <a name="scenarios-and-configurations"></a><span data-ttu-id="bbe6a-245">Scenarios and configurations</span><span class="sxs-lookup"><span data-stu-id="bbe6a-245">Scenarios and configurations</span></span>
<span data-ttu-id="bbe6a-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-246">This section describes the following scenarios and provides the recommended combination of web server, port configuration, Service Fabric integration options, and miscellaneous settings to achieve a properly functioning service:</span></span>
 - <span data-ttu-id="bbe6a-247">Externally exposed ASP.NET Core stateless service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-247">Externally exposed ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="bbe6a-248">Internal-only ASP.NET Core stateless service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-248">Internal-only ASP.NET Core stateless service</span></span>
 - <span data-ttu-id="bbe6a-249">Internal-only ASP.NET Core stateful service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-249">Internal-only ASP.NET Core stateful service</span></span>

<span data-ttu-id="bbe6a-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-250">An **externally exposed** service is one that exposes an endpoint reachable from outside the cluster, usually through a load balancer.</span></span>

<span data-ttu-id="bbe6a-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-251">An **internal-only** service is one whose endpoint is only reachable from within the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="bbe6a-252">Stateful service endpoints generally should not be exposed to the Internet.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-252">Stateful service endpoints generally should not be exposed to the Internet.</span></span> <span data-ttu-id="bbe6a-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-253">Clusters that are behind load balancers that are unaware of Service Fabric service resolution, such as the Azure Load Balancer, will be unable to expose stateful services because the load balancer will not be able to locate and route traffic to the appropriate stateful service replica.</span></span> 

### <a name="externally-exposed-aspnet-core-stateless-services"></a><span data-ttu-id="bbe6a-254">Externally exposed ASP.NET Core stateless services</span><span class="sxs-lookup"><span data-stu-id="bbe6a-254">Externally exposed ASP.NET Core stateless services</span></span>
<span data-ttu-id="bbe6a-255">Kestrel is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-255">Kestrel is the recommended web server for front-end services that expose external, Internet-facing HTTP endpoints.</span></span> <span data-ttu-id="bbe6a-256">On Windows, HttpSys may be used to provide port sharing capability which allows you to host multiple web services on the same set of nodes using the same port, differentiated by hostname or path, without relying on a front-end proxy or gateway to provide HTTP routing.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-256">On Windows, HttpSys may be used to provide port sharing capability which allows you to host multiple web services on the same set of nodes using the same port, differentiated by hostname or path, without relying on a front-end proxy or gateway to provide HTTP routing.</span></span>
 
<span data-ttu-id="bbe6a-257">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-257">When exposed to the Internet, a stateless service should use a well-known and stable endpoint that is reachable through a load balancer.</span></span> <span data-ttu-id="bbe6a-258">This is the URL you will provide to users of your application.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-258">This is the URL you will provide to users of your application.</span></span> <span data-ttu-id="bbe6a-259">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-259">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bbe6a-260">**Notes**</span><span class="sxs-lookup"><span data-stu-id="bbe6a-260">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbe6a-261">Web server</span><span class="sxs-lookup"><span data-stu-id="bbe6a-261">Web server</span></span> | <span data-ttu-id="bbe6a-262">Kestrel</span><span class="sxs-lookup"><span data-stu-id="bbe6a-262">Kestrel</span></span> | <span data-ttu-id="bbe6a-263">Kestrel is the preferred web server as it is supported across Windows and Linux.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-263">Kestrel is the preferred web server as it is supported across Windows and Linux.</span></span> |
| <span data-ttu-id="bbe6a-264">Port configuration</span><span class="sxs-lookup"><span data-stu-id="bbe6a-264">Port configuration</span></span> | <span data-ttu-id="bbe6a-265">static</span><span class="sxs-lookup"><span data-stu-id="bbe6a-265">static</span></span> | <span data-ttu-id="bbe6a-266">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-266">A well-known static port should be configured in the `Endpoints` configuration of ServiceManifest.xml, such as 80 for HTTP or 443 for HTTPS.</span></span> |
| <span data-ttu-id="bbe6a-267">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bbe6a-267">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bbe6a-268">None</span><span class="sxs-lookup"><span data-stu-id="bbe6a-268">None</span></span> | <span data-ttu-id="bbe6a-269">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-269">The `ServiceFabricIntegrationOptions.None` option should be used when configuring Service Fabric integration middleware so that the service does not attempt to validate incoming requests for a unique identifier.</span></span> <span data-ttu-id="bbe6a-270">External users of your application will not know the unique identifying information used by the middleware.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-270">External users of your application will not know the unique identifying information used by the middleware.</span></span> |
| <span data-ttu-id="bbe6a-271">Instance Count</span><span class="sxs-lookup"><span data-stu-id="bbe6a-271">Instance Count</span></span> | <span data-ttu-id="bbe6a-272">-1</span><span class="sxs-lookup"><span data-stu-id="bbe6a-272">-1</span></span> | <span data-ttu-id="bbe6a-273">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-273">In typical use cases, the instance count setting should be set to "-1" so that an instance is available on all nodes that receive traffic from a load balancer.</span></span> |

<span data-ttu-id="bbe6a-274">If multiple externally exposed services share the same set of nodes, HttpSys can be used with a unique but stable URL path.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-274">If multiple externally exposed services share the same set of nodes, HttpSys can be used with a unique but stable URL path.</span></span> <span data-ttu-id="bbe6a-275">This can be accomplished by modifying the URL provided when configuring IWebHost.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-275">This can be accomplished by modifying the URL provided when configuring IWebHost.</span></span> <span data-ttu-id="bbe6a-276">Note this applies to HttpSys only.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-276">Note this applies to HttpSys only.</span></span>

 ```csharp
 new HttpSysCommunicationListener(serviceContext, "ServiceEndpoint", (url, listener) =>
 {
     url += "/MyUniqueServicePath";
 
     return new WebHostBuilder()
         .UseHttpSys()
         ...
         .UseUrls(url)
         .Build();
 })
 ```

### <a name="internal-only-stateless-aspnet-core-service"></a><span data-ttu-id="bbe6a-277">Internal-only stateless ASP.NET Core service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-277">Internal-only stateless ASP.NET Core service</span></span>
<span data-ttu-id="bbe6a-278">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-278">Stateless services that are only called from within the cluster should use unique URLs and dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="bbe6a-279">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-279">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bbe6a-280">**Notes**</span><span class="sxs-lookup"><span data-stu-id="bbe6a-280">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbe6a-281">Web server</span><span class="sxs-lookup"><span data-stu-id="bbe6a-281">Web server</span></span> | <span data-ttu-id="bbe6a-282">Kestrel</span><span class="sxs-lookup"><span data-stu-id="bbe6a-282">Kestrel</span></span> | <span data-ttu-id="bbe6a-283">Although HttpSys may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-283">Although HttpSys may be used for internal stateless services, Kestrel is the recommended server to allow multiple service instances to share a host.</span></span>  |
| <span data-ttu-id="bbe6a-284">Port configuration</span><span class="sxs-lookup"><span data-stu-id="bbe6a-284">Port configuration</span></span> | <span data-ttu-id="bbe6a-285">dynamically assigned</span><span class="sxs-lookup"><span data-stu-id="bbe6a-285">dynamically assigned</span></span> | <span data-ttu-id="bbe6a-286">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-286">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="bbe6a-287">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bbe6a-287">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bbe6a-288">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="bbe6a-288">UseUniqueServiceUrl</span></span> | <span data-ttu-id="bbe6a-289">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-289">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |
| <span data-ttu-id="bbe6a-290">InstanceCount</span><span class="sxs-lookup"><span data-stu-id="bbe6a-290">InstanceCount</span></span> | <span data-ttu-id="bbe6a-291">any</span><span class="sxs-lookup"><span data-stu-id="bbe6a-291">any</span></span> | <span data-ttu-id="bbe6a-292">The instance count setting can be set to any value necessary to operate the service.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-292">The instance count setting can be set to any value necessary to operate the service.</span></span> |

### <a name="internal-only-stateful-aspnet-core-service"></a><span data-ttu-id="bbe6a-293">Internal-only stateful ASP.NET Core service</span><span class="sxs-lookup"><span data-stu-id="bbe6a-293">Internal-only stateful ASP.NET Core service</span></span>
<span data-ttu-id="bbe6a-294">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-294">Stateful services that are only called from within the cluster should use dynamically assigned ports to ensure cooperation between multiple services.</span></span> <span data-ttu-id="bbe6a-295">The following configuration is recommended:</span><span class="sxs-lookup"><span data-stu-id="bbe6a-295">The following configuration is recommended:</span></span>

|  |  | <span data-ttu-id="bbe6a-296">**Notes**</span><span class="sxs-lookup"><span data-stu-id="bbe6a-296">**Notes**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="bbe6a-297">Web server</span><span class="sxs-lookup"><span data-stu-id="bbe6a-297">Web server</span></span> | <span data-ttu-id="bbe6a-298">Kestrel</span><span class="sxs-lookup"><span data-stu-id="bbe6a-298">Kestrel</span></span> | <span data-ttu-id="bbe6a-299">The `HttpSysCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-299">The `HttpSysCommunicationListener` is not designed for use by stateful services in which replicas share a host process.</span></span> |
| <span data-ttu-id="bbe6a-300">Port configuration</span><span class="sxs-lookup"><span data-stu-id="bbe6a-300">Port configuration</span></span> | <span data-ttu-id="bbe6a-301">dynamically assigned</span><span class="sxs-lookup"><span data-stu-id="bbe6a-301">dynamically assigned</span></span> | <span data-ttu-id="bbe6a-302">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-302">Multiple replicas of a stateful service may share a host process or host operating system and thus will need unique ports.</span></span> |
| <span data-ttu-id="bbe6a-303">ServiceFabricIntegrationOptions</span><span class="sxs-lookup"><span data-stu-id="bbe6a-303">ServiceFabricIntegrationOptions</span></span> | <span data-ttu-id="bbe6a-304">UseUniqueServiceUrl</span><span class="sxs-lookup"><span data-stu-id="bbe6a-304">UseUniqueServiceUrl</span></span> | <span data-ttu-id="bbe6a-305">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span><span class="sxs-lookup"><span data-stu-id="bbe6a-305">With dynamic port assignment, this setting prevents the mistaken identity issue described earlier.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="bbe6a-306">Next steps</span><span class="sxs-lookup"><span data-stu-id="bbe6a-306">Next steps</span></span>
[<span data-ttu-id="bbe6a-307">Debug your Service Fabric application by using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bbe6a-307">Debug your Service Fabric application by using Visual Studio</span></span>](service-fabric-debugging-your-application.md)

<!--Image references-->
[0]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-standalone.png
[1]:./media/service-fabric-reliable-services-communication-aspnetcore/webhost-servicefabric.png
[2]:./media/service-fabric-reliable-services-communication-aspnetcore/integration.png
[3]:./media/service-fabric-reliable-services-communication-aspnetcore/httpsys.png
[4]:./media/service-fabric-reliable-services-communication-aspnetcore/kestrel.png
