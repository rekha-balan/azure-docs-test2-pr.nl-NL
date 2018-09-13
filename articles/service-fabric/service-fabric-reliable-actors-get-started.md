---
title: Create an actor-based service on Azure Service Fabric | Microsoft Docs
description: Learn how to create, debug, and deploy your first actor-based service in C# using Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/16/2018
ms.author: vturecek
ms.openlocfilehash: 14fd73d6ff50e297c40ae34d0501c7a3185a468e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780603"
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="8f431-103">Getting started with Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="8f431-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-actors-get-started.md)
> * [Java on Linux](service-fabric-reliable-actors-get-started-java.md)

<span data-ttu-id="8f431-106">This article walks through creating and debugging a simple Reliable Actor application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f431-106">This article walks through creating and debugging a simple Reliable Actor application in Visual Studio.</span></span> <span data-ttu-id="8f431-107">For more information on Reliable Actors, see [Introduction to Service Fabric Reliable Actors](service-fabric-reliable-actors-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="8f431-107">For more information on Reliable Actors, see [Introduction to Service Fabric Reliable Actors](service-fabric-reliable-actors-introduction.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f431-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8f431-108">Prerequisites</span></span>

<span data-ttu-id="8f431-109">Before you start, ensure that you have the Service Fabric development environment, including Visual Studio, set up on your machine.</span><span class="sxs-lookup"><span data-stu-id="8f431-109">Before you start, ensure that you have the Service Fabric development environment, including Visual Studio, set up on your machine.</span></span> <span data-ttu-id="8f431-110">For details, see [how to set up the development environment](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f431-110">For details, see [how to set up the development environment](service-fabric-get-started.md).</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="8f431-111">Create a new project in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f431-111">Create a new project in Visual Studio</span></span>

<span data-ttu-id="8f431-112">Launch Visual Studio 2015 or later as an administrator, and then create a new **Service Fabric Application** project:</span><span class="sxs-lookup"><span data-stu-id="8f431-112">Launch Visual Studio 2015 or later as an administrator, and then create a new **Service Fabric Application** project:</span></span>

![Service Fabric tools for Visual Studio - new project][1]

<span data-ttu-id="8f431-114">In the next dialog box, choose **Actor Service** under **.Net Core 2.0** and enter a name for the service.</span><span class="sxs-lookup"><span data-stu-id="8f431-114">In the next dialog box, choose **Actor Service** under **.Net Core 2.0** and enter a name for the service.</span></span>

![Service Fabric project templates][5]

<span data-ttu-id="8f431-116">The created project shows the following structure:</span><span class="sxs-lookup"><span data-stu-id="8f431-116">The created project shows the following structure:</span></span>

![Service Fabric project structure][2]

## <a name="examine-the-solution"></a><span data-ttu-id="8f431-118">Examine the solution</span><span class="sxs-lookup"><span data-stu-id="8f431-118">Examine the solution</span></span>

<span data-ttu-id="8f431-119">The solution contains three projects:</span><span class="sxs-lookup"><span data-stu-id="8f431-119">The solution contains three projects:</span></span>

* <span data-ttu-id="8f431-120">**The application project (MyApplication)**.</span><span class="sxs-lookup"><span data-stu-id="8f431-120">**The application project (MyApplication)**.</span></span> <span data-ttu-id="8f431-121">This project packages all of the services together for deployment.</span><span class="sxs-lookup"><span data-stu-id="8f431-121">This project packages all of the services together for deployment.</span></span> <span data-ttu-id="8f431-122">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span><span class="sxs-lookup"><span data-stu-id="8f431-122">It contains the *ApplicationManifest.xml* and PowerShell scripts for managing the application.</span></span>

* <span data-ttu-id="8f431-123">**The interface project (HelloWorld.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="8f431-123">**The interface project (HelloWorld.Interfaces)**.</span></span> <span data-ttu-id="8f431-124">This project contains the interface definition for the actor.</span><span class="sxs-lookup"><span data-stu-id="8f431-124">This project contains the interface definition for the actor.</span></span> <span data-ttu-id="8f431-125">Actor interfaces can be defined in any project with any name.</span><span class="sxs-lookup"><span data-stu-id="8f431-125">Actor interfaces can be defined in any project with any name.</span></span>  <span data-ttu-id="8f431-126">The interface defines the actor contract that is shared by the actor implementation and the clients calling the actor.</span><span class="sxs-lookup"><span data-stu-id="8f431-126">The interface defines the actor contract that is shared by the actor implementation and the clients calling the actor.</span></span>  <span data-ttu-id="8f431-127">Because client projects may depend on it, it typically makes sense to define it in an assembly that is separate from the actor implementation.</span><span class="sxs-lookup"><span data-stu-id="8f431-127">Because client projects may depend on it, it typically makes sense to define it in an assembly that is separate from the actor implementation.</span></span>

* <span data-ttu-id="8f431-128">**The actor service project (HelloWorld)**.</span><span class="sxs-lookup"><span data-stu-id="8f431-128">**The actor service project (HelloWorld)**.</span></span> <span data-ttu-id="8f431-129">This project defines the Service Fabric service that is going to host the actor.</span><span class="sxs-lookup"><span data-stu-id="8f431-129">This project defines the Service Fabric service that is going to host the actor.</span></span> <span data-ttu-id="8f431-130">It contains the implementation of the actor, *HellowWorld.cs*.</span><span class="sxs-lookup"><span data-stu-id="8f431-130">It contains the implementation of the actor, *HellowWorld.cs*.</span></span> <span data-ttu-id="8f431-131">An actor implementation is a class that derives from the base type `Actor` and implements the interfaces defined in the *MyActor.Interfaces* project.</span><span class="sxs-lookup"><span data-stu-id="8f431-131">An actor implementation is a class that derives from the base type `Actor` and implements the interfaces defined in the *MyActor.Interfaces* project.</span></span> <span data-ttu-id="8f431-132">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span><span class="sxs-lookup"><span data-stu-id="8f431-132">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them to the base `Actor` class.</span></span>
    
    <span data-ttu-id="8f431-133">This project also contains *Program.cs*, which registers actor classes with the Service Fabric runtime using `ActorRuntime.RegisterActorAsync<T>()`.</span><span class="sxs-lookup"><span data-stu-id="8f431-133">This project also contains *Program.cs*, which registers actor classes with the Service Fabric runtime using `ActorRuntime.RegisterActorAsync<T>()`.</span></span> <span data-ttu-id="8f431-134">The `HelloWorld` class is already registered.</span><span class="sxs-lookup"><span data-stu-id="8f431-134">The `HelloWorld` class is already registered.</span></span> <span data-ttu-id="8f431-135">Any additional actor implementations added to the project must also be registered in the `Main()` method.</span><span class="sxs-lookup"><span data-stu-id="8f431-135">Any additional actor implementations added to the project must also be registered in the `Main()` method.</span></span>

## <a name="customize-the-helloworld-actor"></a><span data-ttu-id="8f431-136">Customize the HelloWorld actor</span><span class="sxs-lookup"><span data-stu-id="8f431-136">Customize the HelloWorld actor</span></span>

<span data-ttu-id="8f431-137">The project template defines some methods in the `IHelloWorld` interface and implements them in the `HelloWorld` actor implementation.</span><span class="sxs-lookup"><span data-stu-id="8f431-137">The project template defines some methods in the `IHelloWorld` interface and implements them in the `HelloWorld` actor implementation.</span></span>  <span data-ttu-id="8f431-138">Replace those methods so the actor service returns a simple "Hello World" string.</span><span class="sxs-lookup"><span data-stu-id="8f431-138">Replace those methods so the actor service returns a simple "Hello World" string.</span></span>

<span data-ttu-id="8f431-139">In the *HelloWorld.Interfaces* project, in the *IHelloWorld.cs* file, replace the interface definition as follows:</span><span class="sxs-lookup"><span data-stu-id="8f431-139">In the *HelloWorld.Interfaces* project, in the *IHelloWorld.cs* file, replace the interface definition as follows:</span></span>

```csharp
public interface IHelloWorld : IActor
{
    Task<string> GetHelloWorldAsync();
}
```

<span data-ttu-id="8f431-140">In the **HelloWorld** project, in **HelloWorld.cs**, replace the entire class definition as follows:</span><span class="sxs-lookup"><span data-stu-id="8f431-140">In the **HelloWorld** project, in **HelloWorld.cs**, replace the entire class definition as follows:</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
internal class HelloWorld : Actor, IHelloWorld
{
    public HelloWorld(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> GetHelloWorldAsync()
    {
        return Task.FromResult("Hello from my reliable actor!");
    }
}
```

<span data-ttu-id="8f431-141">Press **Ctrl-Shift-B** to build the project and make sure everything compiles.</span><span class="sxs-lookup"><span data-stu-id="8f431-141">Press **Ctrl-Shift-B** to build the project and make sure everything compiles.</span></span>

## <a name="add-a-client"></a><span data-ttu-id="8f431-142">Add a client</span><span class="sxs-lookup"><span data-stu-id="8f431-142">Add a client</span></span>

<span data-ttu-id="8f431-143">Create a simple console application to call the actor service.</span><span class="sxs-lookup"><span data-stu-id="8f431-143">Create a simple console application to call the actor service.</span></span>

1. <span data-ttu-id="8f431-144">Right-click on the solution in Solution Explorer > **Add** > **New Project...**.</span><span class="sxs-lookup"><span data-stu-id="8f431-144">Right-click on the solution in Solution Explorer > **Add** > **New Project...**.</span></span>

2. <span data-ttu-id="8f431-145">Under the **.NET Core** project types, choose **Console App (.NET Core)**.</span><span class="sxs-lookup"><span data-stu-id="8f431-145">Under the **.NET Core** project types, choose **Console App (.NET Core)**.</span></span>  <span data-ttu-id="8f431-146">Name the project *ActorClient*.</span><span class="sxs-lookup"><span data-stu-id="8f431-146">Name the project *ActorClient*.</span></span>
    
    ![Add New Project dialog][6]    
    
    > [!NOTE]
    > A console application is not the type of app you would typically use as a client in Service Fabric, but it makes a convenient example for debugging and testing using the local Service Fabric cluster.

3. <span data-ttu-id="8f431-149">The console application must be a 64-bit application to maintain compatibility with the interface project and other dependencies.</span><span class="sxs-lookup"><span data-stu-id="8f431-149">The console application must be a 64-bit application to maintain compatibility with the interface project and other dependencies.</span></span>  <span data-ttu-id="8f431-150">In Solution Explorer, right-click the **ActorClient** project, and then click **Properties**.</span><span class="sxs-lookup"><span data-stu-id="8f431-150">In Solution Explorer, right-click the **ActorClient** project, and then click **Properties**.</span></span>  <span data-ttu-id="8f431-151">On the **Build** tab, set **Platform target** to **x64**.</span><span class="sxs-lookup"><span data-stu-id="8f431-151">On the **Build** tab, set **Platform target** to **x64**.</span></span>
    
    ![Build properties][8]

4. <span data-ttu-id="8f431-153">The client project requires the reliable actors NuGet package.</span><span class="sxs-lookup"><span data-stu-id="8f431-153">The client project requires the reliable actors NuGet package.</span></span>  <span data-ttu-id="8f431-154">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="8f431-154">Click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>  <span data-ttu-id="8f431-155">In the Package Manager Console, enter the following command:</span><span class="sxs-lookup"><span data-stu-id="8f431-155">In the Package Manager Console, enter the following command:</span></span>
    
    ```powershell
    Install-Package Microsoft.ServiceFabric.Actors -IncludePrerelease -ProjectName ActorClient
    ```

    <span data-ttu-id="8f431-156">The NuGet package and all its dependencies are installed in the ActorClient project.</span><span class="sxs-lookup"><span data-stu-id="8f431-156">The NuGet package and all its dependencies are installed in the ActorClient project.</span></span>

5. <span data-ttu-id="8f431-157">The client project also requires a reference to the interfaces project.</span><span class="sxs-lookup"><span data-stu-id="8f431-157">The client project also requires a reference to the interfaces project.</span></span>  <span data-ttu-id="8f431-158">In the ActorClient project, right-click **Dependencies** and then click **Add reference...**.  Select **Projects > Solution** (if not already selected), and then tick the checkbox next to **HelloWorld.Interfaces**.</span><span class="sxs-lookup"><span data-stu-id="8f431-158">In the ActorClient project, right-click **Dependencies** and then click **Add reference...**.  Select **Projects > Solution** (if not already selected), and then tick the checkbox next to **HelloWorld.Interfaces**.</span></span>  <span data-ttu-id="8f431-159">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="8f431-159">Click **OK**.</span></span>
    
    ![Add reference dialog][7]

6. <span data-ttu-id="8f431-161">In the ActorClient project, replace the entire contents of *Program.cs* with the following code:</span><span class="sxs-lookup"><span data-stu-id="8f431-161">In the ActorClient project, replace the entire contents of *Program.cs* with the following code:</span></span>
    
    ```csharp
    using System;
    using System.Threading.Tasks;
    using Microsoft.ServiceFabric.Actors;
    using Microsoft.ServiceFabric.Actors.Client;
    using HelloWorld.Interfaces;
    
    namespace ActorClient
    {
        class Program
        {
            static void Main(string[] args)
            {
                IHelloWorld actor = ActorProxy.Create<IHelloWorld>(ActorId.CreateRandom(), new Uri("fabric:/MyApplication/HelloWorldActorService"));
                Task<string> retval = actor.GetHelloWorldAsync();
                Console.Write(retval.Result);
                Console.ReadLine();
            }
        }
    }
    ```

## <a name="running-and-debugging"></a><span data-ttu-id="8f431-162">Running and debugging</span><span class="sxs-lookup"><span data-stu-id="8f431-162">Running and debugging</span></span>

<span data-ttu-id="8f431-163">Press **F5** to build, deploy, and run the application locally in the Service Fabric development cluster.</span><span class="sxs-lookup"><span data-stu-id="8f431-163">Press **F5** to build, deploy, and run the application locally in the Service Fabric development cluster.</span></span>  <span data-ttu-id="8f431-164">During the deployment process, you can see the progress in the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="8f431-164">During the deployment process, you can see the progress in the **Output** window.</span></span>

![Service Fabric debugging output window][3]

<span data-ttu-id="8f431-166">When the output contains the text, *The application is ready*, it's possible to test the service using the ActorClient application.</span><span class="sxs-lookup"><span data-stu-id="8f431-166">When the output contains the text, *The application is ready*, it's possible to test the service using the ActorClient application.</span></span>  <span data-ttu-id="8f431-167">In Solution Explorer, right-click on the **ActorClient** project, then click **Debug** > **Start new instance**.</span><span class="sxs-lookup"><span data-stu-id="8f431-167">In Solution Explorer, right-click on the **ActorClient** project, then click **Debug** > **Start new instance**.</span></span>  <span data-ttu-id="8f431-168">The command line application should display the output from the actor service.</span><span class="sxs-lookup"><span data-stu-id="8f431-168">The command line application should display the output from the actor service.</span></span>

![Application output][9]

> [!TIP]
> The Service Fabric Actors runtime emits some [events and performance counters related to actor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters). They are useful in diagnostics and performance monitoring.

## <a name="next-steps"></a><span data-ttu-id="8f431-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="8f431-172">Next steps</span></span>
<span data-ttu-id="8f431-173">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="8f431-173">Learn more about [how Reliable Actors use the Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>


[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
[6]: ./media/service-fabric-reliable-actors-get-started/new-console-app.png
[7]: ./media/service-fabric-reliable-actors-get-started/add-reference.png
[8]: ./media/service-fabric-reliable-actors-get-started/build-props.png
[9]: ./media/service-fabric-reliable-actors-get-started/app-output.png