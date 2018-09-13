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
# <a name="getting-started-with-reliable-actors"></a>Getting started with Reliable Actors
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-actors-get-started.md)
> * [Java on Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.

## <a name="installation-and-setup"></a>Installation and setup
Before you start, ensure that you have the Service Fabric development environment set up on your machine.
If you need to set it up, see detailed instructions on [how to set up the development environment](service-fabric-get-started.md).

## <a name="basic-concepts"></a>Basic concepts
To get started with Reliable Actors, you only need to understand a few basic concepts:

* **Actor service**. Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure. Actor instances are activated in a named service instance.
* **Actor registration**. As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime. In addition, the actor type needs to be registered with the Actor runtime.
* **Actor interface**. The actor interface is used to define a strongly typed public interface of an actor. In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process. The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor. Reliable Actors can implement multiple interfaces.
* **ActorProxy class**. The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface. The ActorProxy class provides two important functionalities:
  
  * Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).
  * Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.

The following rules that pertain to actor interfaces are worth mentioning:

* Actor interface methods cannot be overloaded.
* Actor interface methods must not have out, ref, or optional parameters.
* Generic interfaces are not supported.

## <a name="create-a-new-project-in-visual-studio"></a>Create a new project in Visual Studio
Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:

![Service Fabric tools for Visual Studio - new project][1]

In the next dialog box, you can choose the type of project that you want to create.

![Service Fabric project templates][5]

For the HelloWorld project, let's use the Service Fabric Reliable Actors service.

After you have created the solution, you should see the following structure:

![Service Fabric project structure][2]

## <a name="reliable-actors-basic-building-blocks"></a>Reliable Actors basic building blocks
A typical Reliable Actors solution is composed of three projects:

* **The application project (MyActorApplication)**. This is the project that packages all of the services together for deployment. It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.
* **The interface project (MyActor.Interfaces)**. This is the project that contains the interface definition for the actor. In the MyActor.Interfaces project, you can define the interfaces that will be used by the actors in the solution. Your actor interfaces can be defined in any project with any name, however the interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in an assembly that is separate from the actor implementation and can be shared by multiple other projects.

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* **The actor service project (MyActor)**. This is the project used to define the Service Fabric service that is going to host the actor. It contains the implementation of the actor. An actor implementation is a class that derives from the base type `Actor` and implements the interface(s) that are defined in the MyActor.Interfaces project. An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class. This allows for constructor dependency injection of platform dependencies.

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

The actor service must be registered with a service type in the Service Fabric runtime. In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service. The `ActorRuntime` registration method performs this work for actors.

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

If you start from a new project in Visual Studio and you have only one actor definition, the registration is included by default in the code that Visual Studio generates. If you define other actors in the service, you need to add the actor registration by using:

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). They are useful in diagnostics and performance monitoring.
> 
> 

## <a name="debugging"></a>Debugging
The Service Fabric tools for Visual Studio support debugging on your local machine. You can start a debugging session by hitting the F5 key. Visual Studio builds (if necessary) packages. It also deploys the application on the local Service Fabric cluster and attaches the debugger.

During the deployment process, you can see the progress in the **Output** window.

![Service Fabric debugging output window][3]

## <a name="next-steps"></a>Next steps
* [How Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md)
* [Actor state management](service-fabric-reliable-actors-state-management.md)
* [Actor lifecycle and garbage collection](service-fabric-reliable-actors-lifecycle.md)
* [Actor API reference documentation](https://msdn.microsoft.com/library/azure/dn971626.aspx)
* [Sample code](https://github.com/Azure/servicefabric-samples)

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG





