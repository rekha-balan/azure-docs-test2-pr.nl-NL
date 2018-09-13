---
title: Create your first actor-based Azure microservice in C# | Microsoft Docs
description: This tutorial walks you through the steps of creating, debugging, and deploying a simple actor-based service using Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: d90b881ef1afbdec52874df0d4f3708c9f7ff95d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660917"
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="1be90-103">Getting started with Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="1be90-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-actors-get-started.md)
> * [Java on Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="1be90-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1be90-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="1be90-107">Installation and setup</span><span class="sxs-lookup"><span data-stu-id="1be90-107">Installation and setup</span></span>
<span data-ttu-id="1be90-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span><span class="sxs-lookup"><span data-stu-id="1be90-108">Before you start, ensure that you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="1be90-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1be90-109">If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="1be90-110">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="1be90-110">Basic concepts</span></span>
<span data-ttu-id="1be90-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="1be90-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="1be90-112">**Actor service**.</span><span class="sxs-lookup"><span data-stu-id="1be90-112">**Actor service**.</span></span> <span data-ttu-id="1be90-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span><span class="sxs-lookup"><span data-stu-id="1be90-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="1be90-114">Actor instances are activated in a named service instance.</span><span class="sxs-lookup"><span data-stu-id="1be90-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="1be90-115">**Actor registration**.</span><span class="sxs-lookup"><span data-stu-id="1be90-115">**Actor registration**.</span></span> <span data-ttu-id="1be90-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="1be90-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="1be90-117">In addition, the actor type needs to be registered with the Actor runtime.</span><span class="sxs-lookup"><span data-stu-id="1be90-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="1be90-118">**Actor interface**.</span><span class="sxs-lookup"><span data-stu-id="1be90-118">**Actor interface**.</span></span> <span data-ttu-id="1be90-119">The actor interface is used to define a strongly typed public interface of an actor.</span><span class="sxs-lookup"><span data-stu-id="1be90-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="1be90-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span><span class="sxs-lookup"><span data-stu-id="1be90-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="1be90-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span><span class="sxs-lookup"><span data-stu-id="1be90-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="1be90-122">Reliable Actors can implement multiple interfaces.</span><span class="sxs-lookup"><span data-stu-id="1be90-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="1be90-123">**ActorProxy class**.</span><span class="sxs-lookup"><span data-stu-id="1be90-123">**ActorProxy class**.</span></span> <span data-ttu-id="1be90-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span><span class="sxs-lookup"><span data-stu-id="1be90-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="1be90-125">The ActorProxy class provides two important functionalities:</span><span class="sxs-lookup"><span data-stu-id="1be90-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="1be90-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span><span class="sxs-lookup"><span data-stu-id="1be90-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="1be90-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1be90-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="1be90-128">The following rules that pertain to actor interfaces are worth mentioning:</span><span class="sxs-lookup"><span data-stu-id="1be90-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="1be90-129">Actor interface methods cannot be overloaded.</span><span class="sxs-lookup"><span data-stu-id="1be90-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="1be90-130">Actor interface methods must not have out, ref, or optional parameters.</span><span class="sxs-lookup"><span data-stu-id="1be90-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="1be90-131">Generic interfaces are not supported.</span><span class="sxs-lookup"><span data-stu-id="1be90-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="1be90-132">Create a new project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1be90-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="1be90-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span><span class="sxs-lookup"><span data-stu-id="1be90-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Service Fabric tools for Visual Studio - new project][1]

<span data-ttu-id="1be90-135">In the next dialog box, you can choose the type of project that you want to create.</span><span class="sxs-lookup"><span data-stu-id="1be90-135">In the next dialog box, you can choose the type of project that you want to create.</span></span>

![Service Fabric project templates][5]

<span data-ttu-id="1be90-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span><span class="sxs-lookup"><span data-stu-id="1be90-137">For the HelloWorld project, let's use the Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="1be90-138">After you have created the solution, you should see the following structure:</span><span class="sxs-lookup"><span data-stu-id="1be90-138">After you have created the solution, you should see the following structure:</span></span>

![Service Fabric project structure][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="1be90-140">Reliable Actors basic building blocks</span><span class="sxs-lookup"><span data-stu-id="1be90-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="1be90-141">A typical Reliable Actors solution is composed of three projects:</span><span class="sxs-lookup"><span data-stu-id="1be90-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="1be90-142">**The application project (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="1be90-142">**The application project (MyActorApplication)**.</span></span> <span data-ttu-id="1be90-143">This is the project that packages all of the services together for deployment.</span><span class="sxs-lookup"><span data-stu-id="1be90-143">This is the project that packages all of the services together for deployment.</span></span> <span data-ttu-id="1be90-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span><span class="sxs-lookup"><span data-stu-id="1be90-144">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>
* <span data-ttu-id="1be90-145">**The interface project (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="1be90-145">**The interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="1be90-146">This is the project that contains the interface definition for the actor.</span><span class="sxs-lookup"><span data-stu-id="1be90-146">This is the project that contains the interface definition for the actor.</span></span> <span data-ttu-id="1be90-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span><span class="sxs-lookup"><span data-stu-id="1be90-147">In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution.</span></span> <span data-ttu-id="1be90-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span><span class="sxs-lookup"><span data-stu-id="1be90-148">Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="1be90-149">**The actor service project (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="1be90-149">**The actor service project (MyActor)**.</span></span> <span data-ttu-id="1be90-150">This is the project used to define the Service Fabric service that is going to host the actor.</span><span class="sxs-lookup"><span data-stu-id="1be90-150">This is the project used to define the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="1be90-151">It contains the implementation of the actor.</span><span class="sxs-lookup"><span data-stu-id="1be90-151">It contains the implementation of the actor.</span></span> <span data-ttu-id="1be90-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span><span class="sxs-lookup"><span data-stu-id="1be90-152">An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project.</span></span> <span data-ttu-id="1be90-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span><span class="sxs-lookup"><span data-stu-id="1be90-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span> <span data-ttu-id="1be90-154">This allows for constructor dependency injection of platform dependencies.</span><span class="sxs-lookup"><span data-stu-id="1be90-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="1be90-155">The actor service must be registered with a service type in the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="1be90-155">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="1be90-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span><span class="sxs-lookup"><span data-stu-id="1be90-156">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="1be90-157">The `ActorRuntime` registration method performs this work for actors.</span><span class="sxs-lookup"><span data-stu-id="1be90-157">The `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="1be90-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span><span class="sxs-lookup"><span data-stu-id="1be90-158">If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates.</span></span> <span data-ttu-id="1be90-159">If you define other actors in the service, you need to add the actor registration by using:</span><span class="sxs-lookup"><span data-stu-id="1be90-159">If you define other actors in the service, you need to add the actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). They are useful in diagnostics and performance monitoring.
> 
> 

## <a name="debugging"></a><span data-ttu-id="1be90-162">Debugging</span><span class="sxs-lookup"><span data-stu-id="1be90-162">Debugging</span></span>
<span data-ttu-id="1be90-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span><span class="sxs-lookup"><span data-stu-id="1be90-163">The Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="1be90-164">You can start a debugging session by hitting the F5 key.</span><span class="sxs-lookup"><span data-stu-id="1be90-164">You can start a debugging session by hitting the F5 key.</span></span> <span data-ttu-id="1be90-165">Visual Studio builds (if necessary) packages.</span><span class="sxs-lookup"><span data-stu-id="1be90-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="1be90-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span><span class="sxs-lookup"><span data-stu-id="1be90-166">It also deploys the application on the local Service Fabric cluster and attaches the debugger.</span></span>

<span data-ttu-id="1be90-167">During the deployment process, you can see the progress in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="1be90-167">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Service Fabric debugging output window][3]

## <a name="next-steps"></a><span data-ttu-id="1be90-169">Next steps</span><span class="sxs-lookup"><span data-stu-id="1be90-169">Next steps</span></span>
* [<span data-ttu-id="1be90-170">How Reliable Actors use the Service Fabric platform</span><span class="sxs-lookup"><span data-stu-id="1be90-170">How Reliable Actors use the Service Fabric platform</span></span>](service-fabric-reliable-actors-platform.md)
* [<span data-ttu-id="1be90-171">Actor state management</span><span class="sxs-lookup"><span data-stu-id="1be90-171">Actor state management</span></span>](service-fabric-reliable-actors-state-management.md)
* [<span data-ttu-id="1be90-172">Actor lifecycle and garbage collection</span><span class="sxs-lookup"><span data-stu-id="1be90-172">Actor lifecycle and garbage collection</span></span>](service-fabric-reliable-actors-lifecycle.md)
* [<span data-ttu-id="1be90-173">Actor API reference documentation</span><span class="sxs-lookup"><span data-stu-id="1be90-173">Actor API reference documentation</span></span>](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [<span data-ttu-id="1be90-174">Sample code</span><span class="sxs-lookup"><span data-stu-id="1be90-174">Sample code</span></span>](https://github.com/Azure/servicefabric-samples)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG





