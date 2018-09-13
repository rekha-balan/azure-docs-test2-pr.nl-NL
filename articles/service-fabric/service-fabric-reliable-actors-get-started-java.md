---
title: Create your first actor-based Azure microservice in Java | Microsoft Docs
description: This tutorial walks you through the steps of creating, debugging, and deploying a simple actor-based service using Service Fabric Reliable Actors.
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: ''
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: d09f3b55b1cd125d872ee44104cce987e9ee09cc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555279"
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="23a2e-103">Getting started with Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="23a2e-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-actors-get-started.md)
> * [Java on Linux](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="23a2e-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span><span class="sxs-lookup"><span data-stu-id="23a2e-106">This article explains the basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="23a2e-107">Installation and setup</span><span class="sxs-lookup"><span data-stu-id="23a2e-107">Installation and setup</span></span>
<span data-ttu-id="23a2e-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span><span class="sxs-lookup"><span data-stu-id="23a2e-108">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="23a2e-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="23a2e-109">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="23a2e-110">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="23a2e-110">Basic concepts</span></span>
<span data-ttu-id="23a2e-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="23a2e-111">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="23a2e-112">**Actor service**.</span><span class="sxs-lookup"><span data-stu-id="23a2e-112">**Actor service**.</span></span> <span data-ttu-id="23a2e-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span><span class="sxs-lookup"><span data-stu-id="23a2e-113">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="23a2e-114">Actor instances are activated in a named service instance.</span><span class="sxs-lookup"><span data-stu-id="23a2e-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="23a2e-115">**Actor registration**.</span><span class="sxs-lookup"><span data-stu-id="23a2e-115">**Actor registration**.</span></span> <span data-ttu-id="23a2e-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="23a2e-116">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="23a2e-117">In addition, the actor type needs to be registered with the Actor runtime.</span><span class="sxs-lookup"><span data-stu-id="23a2e-117">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="23a2e-118">**Actor interface**.</span><span class="sxs-lookup"><span data-stu-id="23a2e-118">**Actor interface**.</span></span> <span data-ttu-id="23a2e-119">The actor interface is used to define a strongly typed public interface of an actor.</span><span class="sxs-lookup"><span data-stu-id="23a2e-119">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="23a2e-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span><span class="sxs-lookup"><span data-stu-id="23a2e-120">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="23a2e-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span><span class="sxs-lookup"><span data-stu-id="23a2e-121">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="23a2e-122">Reliable Actors can implement multiple interfaces.</span><span class="sxs-lookup"><span data-stu-id="23a2e-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="23a2e-123">**ActorProxy class**.</span><span class="sxs-lookup"><span data-stu-id="23a2e-123">**ActorProxy class**.</span></span> <span data-ttu-id="23a2e-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span><span class="sxs-lookup"><span data-stu-id="23a2e-124">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="23a2e-125">The ActorProxy class provides two important functionalities:</span><span class="sxs-lookup"><span data-stu-id="23a2e-125">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="23a2e-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span><span class="sxs-lookup"><span data-stu-id="23a2e-126">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="23a2e-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="23a2e-127">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="23a2e-128">The following rules that pertain to actor interfaces are worth mentioning:</span><span class="sxs-lookup"><span data-stu-id="23a2e-128">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="23a2e-129">Actor interface methods cannot be overloaded.</span><span class="sxs-lookup"><span data-stu-id="23a2e-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="23a2e-130">Actor interface methods must not have out, ref, or optional parameters.</span><span class="sxs-lookup"><span data-stu-id="23a2e-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="23a2e-131">Generic interfaces are not supported.</span><span class="sxs-lookup"><span data-stu-id="23a2e-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="23a2e-132">Create an actor service</span><span class="sxs-lookup"><span data-stu-id="23a2e-132">Create an actor service</span></span>
<span data-ttu-id="23a2e-133">Start by creating a new Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="23a2e-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="23a2e-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span><span class="sxs-lookup"><span data-stu-id="23a2e-134">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="23a2e-135">Start by running the following Yeoman command:</span><span class="sxs-lookup"><span data-stu-id="23a2e-135">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="23a2e-136">Follow the instructions to create a **Reliable Actor Service**.</span><span class="sxs-lookup"><span data-stu-id="23a2e-136">Follow the instructions to create a **Reliable Actor Service**.</span></span> <span data-ttu-id="23a2e-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="23a2e-137">For this tutorial, name the application "HelloWorldActorApplication" and the actor "HelloWorldActor."</span></span> <span data-ttu-id="23a2e-138">The following scaffolding will be created:</span><span class="sxs-lookup"><span data-stu-id="23a2e-138">The following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="23a2e-139">Reliable Actors basic building blocks</span><span class="sxs-lookup"><span data-stu-id="23a2e-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="23a2e-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span><span class="sxs-lookup"><span data-stu-id="23a2e-140">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="23a2e-141">Actor interface</span><span class="sxs-lookup"><span data-stu-id="23a2e-141">Actor interface</span></span>
<span data-ttu-id="23a2e-142">This contains the interface definition for the actor.</span><span class="sxs-lookup"><span data-stu-id="23a2e-142">This contains the interface definition for the actor.</span></span> <span data-ttu-id="23a2e-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span><span class="sxs-lookup"><span data-stu-id="23a2e-143">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="23a2e-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="23a2e-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="23a2e-145">Actor service</span><span class="sxs-lookup"><span data-stu-id="23a2e-145">Actor service</span></span>
<span data-ttu-id="23a2e-146">This contains your actor implementation and actor registration code.</span><span class="sxs-lookup"><span data-stu-id="23a2e-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="23a2e-147">The actor class implements the actor interface.</span><span class="sxs-lookup"><span data-stu-id="23a2e-147">The actor class implements the actor interface.</span></span> <span data-ttu-id="23a2e-148">This is where your actor does its work.</span><span class="sxs-lookup"><span data-stu-id="23a2e-148">This is where your actor does its work.</span></span>

<span data-ttu-id="23a2e-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="23a2e-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="23a2e-150">Actor registration</span><span class="sxs-lookup"><span data-stu-id="23a2e-150">Actor registration</span></span>
<span data-ttu-id="23a2e-151">The actor service must be registered with a service type in the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="23a2e-151">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="23a2e-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span><span class="sxs-lookup"><span data-stu-id="23a2e-152">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="23a2e-153">The `ActorRuntime` registration method performs this work for actors.</span><span class="sxs-lookup"><span data-stu-id="23a2e-153">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="23a2e-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="23a2e-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="23a2e-155">Test client</span><span class="sxs-lookup"><span data-stu-id="23a2e-155">Test client</span></span>
<span data-ttu-id="23a2e-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span><span class="sxs-lookup"><span data-stu-id="23a2e-156">This is a simple test client application you can run separately from the Service Fabric application to test your actor service.</span></span> <span data-ttu-id="23a2e-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span><span class="sxs-lookup"><span data-stu-id="23a2e-157">This is an example of where the ActorProxy can be used to activate and communicate with actor instances.</span></span> <span data-ttu-id="23a2e-158">It does not get deployed with your service.</span><span class="sxs-lookup"><span data-stu-id="23a2e-158">It does not get deployed with your service.</span></span>

### <a name="the-application"></a><span data-ttu-id="23a2e-159">The application</span><span class="sxs-lookup"><span data-stu-id="23a2e-159">The application</span></span>
<span data-ttu-id="23a2e-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span><span class="sxs-lookup"><span data-stu-id="23a2e-160">Finally, the application packages the actor service and any other services you might add in the future together for deployment.</span></span> <span data-ttu-id="23a2e-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span><span class="sxs-lookup"><span data-stu-id="23a2e-161">It contains the *ApplicationManifest.xml* and place holders for the actor service package.</span></span>

## <a name="run-the-application"></a><span data-ttu-id="23a2e-162">Run the application</span><span class="sxs-lookup"><span data-stu-id="23a2e-162">Run the application</span></span>
<span data-ttu-id="23a2e-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and un-deploy the application.</span><span class="sxs-lookup"><span data-stu-id="23a2e-163">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and un-deploy the application.</span></span> <span data-ttu-id="23a2e-164">To run the application, first build the application with gradle:</span><span class="sxs-lookup"><span data-stu-id="23a2e-164">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="23a2e-165">This will produce a Service Fabric application package that can be deployed using Service Fabric Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="23a2e-165">This will produce a Service Fabric application package that can be deployed using Service Fabric Azure CLI.</span></span> <span data-ttu-id="23a2e-166">The install.sh script contains the necessary Azure CLI commands to deploy the application package.</span><span class="sxs-lookup"><span data-stu-id="23a2e-166">The install.sh script contains the necessary Azure CLI commands to deploy the application package.</span></span> <span data-ttu-id="23a2e-167">Simply run the install.sh script to deploy:</span><span class="sxs-lookup"><span data-stu-id="23a2e-167">Simply run the install.sh script to deploy:</span></span>

```bask
$ ./install.sh
```
