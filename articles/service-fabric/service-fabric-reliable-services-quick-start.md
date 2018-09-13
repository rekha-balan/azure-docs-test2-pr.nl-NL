---
title: Create your first Service Fabric application in C# | Microsoft Docs
description: Introduction to creating a Microsoft Azure Service Fabric application with stateless and stateful services.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: 26e0e38b3c1c945ece09e6a602a60ca7866a8a09
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555311"
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="59df9-103">Get started with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="59df9-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-quick-start.md)
> * [Java on Linux](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="59df9-106">An Azure Service Fabric application contains one or more services that run your code.</span><span class="sxs-lookup"><span data-stu-id="59df9-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="59df9-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59df9-107">This guide shows you how to create both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="59df9-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="59df9-108">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="59df9-109">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="59df9-109">Basic concepts</span></span>
<span data-ttu-id="59df9-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="59df9-110">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="59df9-111">**Service type**: This is your service implementation.</span><span class="sxs-lookup"><span data-stu-id="59df9-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="59df9-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span><span class="sxs-lookup"><span data-stu-id="59df9-112">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="59df9-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span><span class="sxs-lookup"><span data-stu-id="59df9-113">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="59df9-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="59df9-114">A service instance has a name in the form of a URI using the "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="59df9-115">**Service host**: The named service instances you create need to run inside a host process.</span><span class="sxs-lookup"><span data-stu-id="59df9-115">**Service host**: The named service instances you create need to run inside a host process.</span></span> <span data-ttu-id="59df9-116">The service host is just a process where instances of your service can run.</span><span class="sxs-lookup"><span data-stu-id="59df9-116">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="59df9-117">**Service registration**: Registration brings everything together.</span><span class="sxs-lookup"><span data-stu-id="59df9-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="59df9-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span><span class="sxs-lookup"><span data-stu-id="59df9-118">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="59df9-119">Create a stateless service</span><span class="sxs-lookup"><span data-stu-id="59df9-119">Create a stateless service</span></span>
<span data-ttu-id="59df9-120">A stateless service is a type of service that is currently the norm in cloud applications.</span><span class="sxs-lookup"><span data-stu-id="59df9-120">A stateless service is a type of service that is currently the norm in cloud applications.</span></span> <span data-ttu-id="59df9-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span><span class="sxs-lookup"><span data-stu-id="59df9-121">It is considered stateless because the service itself does not contain data that needs to be stored reliably or made highly available.</span></span> <span data-ttu-id="59df9-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span><span class="sxs-lookup"><span data-stu-id="59df9-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="59df9-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span><span class="sxs-lookup"><span data-stu-id="59df9-123">In this type of service, state must be persisted to an external store, such as Azure Tables or a SQL database, for it to be made highly available and reliable.</span></span>

<span data-ttu-id="59df9-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span><span class="sxs-lookup"><span data-stu-id="59df9-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Use the New Project dialog box to create a new Service Fabric application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="59df9-126">Then create a stateless service project named *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="59df9-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![In the second dialog box, create a stateless service project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="59df9-128">Your solution now contains two projects:</span><span class="sxs-lookup"><span data-stu-id="59df9-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="59df9-129">*HelloWorld*.</span><span class="sxs-lookup"><span data-stu-id="59df9-129">*HelloWorld*.</span></span> <span data-ttu-id="59df9-130">This is the *application* project that contains your *services*.</span><span class="sxs-lookup"><span data-stu-id="59df9-130">This is the *application* project that contains your *services*.</span></span> <span data-ttu-id="59df9-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span><span class="sxs-lookup"><span data-stu-id="59df9-131">It also contains the application manifest that describes the application, as well as a number of PowerShell scripts that help you to deploy your application.</span></span>
* <span data-ttu-id="59df9-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="59df9-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="59df9-133">This is the service project.</span><span class="sxs-lookup"><span data-stu-id="59df9-133">This is the service project.</span></span> <span data-ttu-id="59df9-134">It contains the stateless service implementation.</span><span class="sxs-lookup"><span data-stu-id="59df9-134">It contains the stateless service implementation.</span></span>

## <a name="implement-the-service"></a><span data-ttu-id="59df9-135">Implement the service</span><span class="sxs-lookup"><span data-stu-id="59df9-135">Implement the service</span></span>
<span data-ttu-id="59df9-136">Open the **HelloWorldStateless.cs** file in the service project.</span><span class="sxs-lookup"><span data-stu-id="59df9-136">Open the **HelloWorldStateless.cs** file in the service project.</span></span> <span data-ttu-id="59df9-137">In Service Fabric, a service can run any business logic.</span><span class="sxs-lookup"><span data-stu-id="59df9-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="59df9-138">The service API provides two entry points for your code:</span><span class="sxs-lookup"><span data-stu-id="59df9-138">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="59df9-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span><span class="sxs-lookup"><span data-stu-id="59df9-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="59df9-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="59df9-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="59df9-141">This is where you can start receiving requests from users and other services.</span><span class="sxs-lookup"><span data-stu-id="59df9-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="59df9-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span><span class="sxs-lookup"><span data-stu-id="59df9-142">In this tutorial, we will focus on the `RunAsync()` entry point method.</span></span> <span data-ttu-id="59df9-143">This is where you can immediately start running your code.</span><span class="sxs-lookup"><span data-stu-id="59df9-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="59df9-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span><span class="sxs-lookup"><span data-stu-id="59df9-144">The project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> For details about how to work with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)
> 
> 

### <a name="runasync"></a><span data-ttu-id="59df9-146">RunAsync</span><span class="sxs-lookup"><span data-stu-id="59df9-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="59df9-147">The platform calls this method when an instance of a service is placed and ready to execute.</span><span class="sxs-lookup"><span data-stu-id="59df9-147">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="59df9-148">For a stateless service, that simply means when the service instance is opened.</span><span class="sxs-lookup"><span data-stu-id="59df9-148">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="59df9-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span><span class="sxs-lookup"><span data-stu-id="59df9-149">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="59df9-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span><span class="sxs-lookup"><span data-stu-id="59df9-150">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="59df9-151">This can happen for various reasons, including:</span><span class="sxs-lookup"><span data-stu-id="59df9-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="59df9-152">The system moves your service instances for resource balancing.</span><span class="sxs-lookup"><span data-stu-id="59df9-152">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="59df9-153">Faults occur in your code.</span><span class="sxs-lookup"><span data-stu-id="59df9-153">Faults occur in your code.</span></span>
* <span data-ttu-id="59df9-154">The application or system is upgraded.</span><span class="sxs-lookup"><span data-stu-id="59df9-154">The application or system is upgraded.</span></span>
* <span data-ttu-id="59df9-155">The underlying hardware experiences an outage.</span><span class="sxs-lookup"><span data-stu-id="59df9-155">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="59df9-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span><span class="sxs-lookup"><span data-stu-id="59df9-156">This orchestration is managed by the system to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="59df9-157">`RunAsync()` should not block synchronously.</span><span class="sxs-lookup"><span data-stu-id="59df9-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="59df9-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span><span class="sxs-lookup"><span data-stu-id="59df9-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations to allow the runtime to continue.</span></span> <span data-ttu-id="59df9-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span><span class="sxs-lookup"><span data-stu-id="59df9-159">Note in the `while(true)` loop in the previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="59df9-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span><span class="sxs-lookup"><span data-stu-id="59df9-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="59df9-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span><span class="sxs-lookup"><span data-stu-id="59df9-161">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="59df9-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span><span class="sxs-lookup"><span data-stu-id="59df9-162">The system will wait for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="59df9-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span><span class="sxs-lookup"><span data-stu-id="59df9-163">It is important to honor the cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when the system requests cancellation.</span></span>

<span data-ttu-id="59df9-164">In this stateless service example, the count is stored in a local variable.</span><span class="sxs-lookup"><span data-stu-id="59df9-164">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="59df9-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span><span class="sxs-lookup"><span data-stu-id="59df9-165">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="59df9-166">When the service moves or restarts, the value is lost.</span><span class="sxs-lookup"><span data-stu-id="59df9-166">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="59df9-167">Create a stateful service</span><span class="sxs-lookup"><span data-stu-id="59df9-167">Create a stateful service</span></span>
<span data-ttu-id="59df9-168">Service Fabric introduces a new kind of service that is stateful.</span><span class="sxs-lookup"><span data-stu-id="59df9-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="59df9-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span><span class="sxs-lookup"><span data-stu-id="59df9-169">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="59df9-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span><span class="sxs-lookup"><span data-stu-id="59df9-170">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="59df9-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span><span class="sxs-lookup"><span data-stu-id="59df9-171">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="59df9-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span><span class="sxs-lookup"><span data-stu-id="59df9-172">In the same *HelloWorld* application, you can add a new service by right-clicking on the Services references in the application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Add a service to your Service Fabric application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="59df9-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="59df9-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="59df9-175">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="59df9-175">Click **OK**.</span></span>

![Use the New Project dialog box to create a new Service Fabric stateful service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="59df9-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="59df9-177">Your application should now have two services: the stateless service *HelloWorldStateless* and the stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="59df9-178">A stateful service has the same entry points as a stateless service.</span><span class="sxs-lookup"><span data-stu-id="59df9-178">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="59df9-179">The main difference is the availability of a *state provider* that can store state reliably.</span><span class="sxs-lookup"><span data-stu-id="59df9-179">The main difference is the availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="59df9-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="59df9-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="59df9-181">A stateful Reliable Service uses this state provider by default.</span><span class="sxs-lookup"><span data-stu-id="59df9-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="59df9-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span><span class="sxs-lookup"><span data-stu-id="59df9-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains the following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace the following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, the transaction aborts, all changes are
            // discarded, and nothing is saved to the secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="59df9-183">RunAsync</span><span class="sxs-lookup"><span data-stu-id="59df9-183">RunAsync</span></span>
<span data-ttu-id="59df9-184">`RunAsync()` operates similarly in stateful and stateless services.</span><span class="sxs-lookup"><span data-stu-id="59df9-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="59df9-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="59df9-185">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="59df9-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span><span class="sxs-lookup"><span data-stu-id="59df9-186">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="59df9-187">Reliable Collections and the Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="59df9-187">Reliable Collections and the Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="59df9-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span><span class="sxs-lookup"><span data-stu-id="59df9-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="59df9-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span><span class="sxs-lookup"><span data-stu-id="59df9-189">With Service Fabric and Reliable Collections, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="59df9-190">Reliable Collections make your data highly available.</span><span class="sxs-lookup"><span data-stu-id="59df9-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="59df9-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span><span class="sxs-lookup"><span data-stu-id="59df9-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="59df9-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span><span class="sxs-lookup"><span data-stu-id="59df9-192">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="59df9-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span><span class="sxs-lookup"><span data-stu-id="59df9-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="59df9-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span><span class="sxs-lookup"><span data-stu-id="59df9-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data to local disk on each replica.</span></span> <span data-ttu-id="59df9-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span><span class="sxs-lookup"><span data-stu-id="59df9-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="59df9-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span><span class="sxs-lookup"><span data-stu-id="59df9-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important to make sure that your types are [supported by the Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use the default serializer.</span></span>
* <span data-ttu-id="59df9-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span><span class="sxs-lookup"><span data-stu-id="59df9-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="59df9-198">Objects stored in Reliable Collections are kept in local memory in your service.</span><span class="sxs-lookup"><span data-stu-id="59df9-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="59df9-199">This means that you have a local reference to the object.</span><span class="sxs-lookup"><span data-stu-id="59df9-199">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="59df9-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span><span class="sxs-lookup"><span data-stu-id="59df9-200">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="59df9-201">This is because changes to local instances of objects will not be replicated automatically.</span><span class="sxs-lookup"><span data-stu-id="59df9-201">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="59df9-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span><span class="sxs-lookup"><span data-stu-id="59df9-202">You must re-insert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="59df9-203">The Reliable State Manager manages Reliable Collections for you.</span><span class="sxs-lookup"><span data-stu-id="59df9-203">The Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="59df9-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span><span class="sxs-lookup"><span data-stu-id="59df9-204">You can simply ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="59df9-205">The Reliable State Manager ensures that you get a reference back.</span><span class="sxs-lookup"><span data-stu-id="59df9-205">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="59df9-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span><span class="sxs-lookup"><span data-stu-id="59df9-206">We don't recommended that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="59df9-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span><span class="sxs-lookup"><span data-stu-id="59df9-207">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="59df9-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span><span class="sxs-lookup"><span data-stu-id="59df9-208">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="59df9-209">Transactional and asynchronous operations</span><span class="sxs-lookup"><span data-stu-id="59df9-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="59df9-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span><span class="sxs-lookup"><span data-stu-id="59df9-210">Reliable Collections have many of the same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="59df9-211">Operations on Reliable Collections are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="59df9-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="59df9-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span><span class="sxs-lookup"><span data-stu-id="59df9-212">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="59df9-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span><span class="sxs-lookup"><span data-stu-id="59df9-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="59df9-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span><span class="sxs-lookup"><span data-stu-id="59df9-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save the result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="59df9-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span><span class="sxs-lookup"><span data-stu-id="59df9-215">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="59df9-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span><span class="sxs-lookup"><span data-stu-id="59df9-216">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="59df9-217">Run the application</span><span class="sxs-lookup"><span data-stu-id="59df9-217">Run the application</span></span>
<span data-ttu-id="59df9-218">We now return to the *HelloWorld* application.</span><span class="sxs-lookup"><span data-stu-id="59df9-218">We now return to the *HelloWorld* application.</span></span> <span data-ttu-id="59df9-219">You can now build and deploy your services.</span><span class="sxs-lookup"><span data-stu-id="59df9-219">You can now build and deploy your services.</span></span> <span data-ttu-id="59df9-220">When you press **F5**, your application will be built and deployed to your local cluster.</span><span class="sxs-lookup"><span data-stu-id="59df9-220">When you press **F5**, your application will be built and deployed to your local cluster.</span></span>

<span data-ttu-id="59df9-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span><span class="sxs-lookup"><span data-stu-id="59df9-221">After the services start running, you can view the generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="59df9-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span><span class="sxs-lookup"><span data-stu-id="59df9-222">Note that the events displayed are from both the stateless service and the stateful service in the application.</span></span> <span data-ttu-id="59df9-223">You can pause the stream by clicking the **Pause** button.</span><span class="sxs-lookup"><span data-stu-id="59df9-223">You can pause the stream by clicking the **Pause** button.</span></span> <span data-ttu-id="59df9-224">You can then examine the details of a message by expanding that message.</span><span class="sxs-lookup"><span data-stu-id="59df9-224">You can then examine the details of a message by expanding that message.</span></span>

> [!NOTE]
> Before you run the application, make sure that you have a local development cluster running. Check out the [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.
> 
> 

![View Diagnostic Events in Visual Studio](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="59df9-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="59df9-228">Next steps</span></span>
[<span data-ttu-id="59df9-229">Debug your Service Fabric application in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="59df9-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="59df9-230">Get started: Service Fabric Web API services with OWIN self-hosting</span><span class="sxs-lookup"><span data-stu-id="59df9-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="59df9-231">Learn more about Reliable Collections</span><span class="sxs-lookup"><span data-stu-id="59df9-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="59df9-232">Deploy an application</span><span class="sxs-lookup"><span data-stu-id="59df9-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="59df9-233">Application upgrade</span><span class="sxs-lookup"><span data-stu-id="59df9-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="59df9-234">Developer reference for Reliable Services</span><span class="sxs-lookup"><span data-stu-id="59df9-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)







