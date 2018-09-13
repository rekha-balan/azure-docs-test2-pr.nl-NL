---
title: Create an Azure Service Fabric reliable actors Java application on Linux | Microsoft Docs
description: Learn how to create and deploy a Java Service Fabric reliable actors application in five minutes.
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: ''
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/18/2018
ms.author: ryanwi
ms.openlocfilehash: 57f781b045b53bf7a17461f78b2f04005567115a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776405"
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a><span data-ttu-id="ee148-103">Create your first Java Service Fabric Reliable Actors application on Linux</span><span class="sxs-lookup"><span data-stu-id="ee148-103">Create your first Java Service Fabric Reliable Actors application on Linux</span></span>
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="ee148-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span><span class="sxs-lookup"><span data-stu-id="ee148-107">This quick-start helps you create your first Azure Service Fabric Java application in a Linux development environment in just a few minutes.</span></span>  <span data-ttu-id="ee148-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span><span class="sxs-lookup"><span data-stu-id="ee148-108">When you are finished, you'll have a simple Java single-service application running on the local development cluster.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ee148-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ee148-109">Prerequisites</span></span>
<span data-ttu-id="ee148-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, Yeoman, setup the Java development environment, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ee148-110">Before you get started, install the Service Fabric SDK, the Service Fabric CLI, Yeoman, setup the Java development environment, and setup a development cluster in your [Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="ee148-111">If you are using Mac OS X, you can [Set up a development environment on Mac using Docker](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="ee148-111">If you are using Mac OS X, you can [Set up a development environment on Mac using Docker](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="ee148-112">Also install the [Service Fabric CLI](service-fabric-cli.md).</span><span class="sxs-lookup"><span data-stu-id="ee148-112">Also install the [Service Fabric CLI](service-fabric-cli.md).</span></span>

### <a name="install-and-set-up-the-generators-for-java"></a><span data-ttu-id="ee148-113">Install and set up the generators for Java</span><span class="sxs-lookup"><span data-stu-id="ee148-113">Install and set up the generators for Java</span></span>
<span data-ttu-id="ee148-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span><span class="sxs-lookup"><span data-stu-id="ee148-114">Service Fabric provides scaffolding tools which will help you create a Service Fabric Java application from terminal using Yeoman template generator.</span></span>  <span data-ttu-id="ee148-115">If Yeoman isn't already installed, see [Service Fabric getting started with Linux](service-fabric-get-started-linux.md#set-up-yeoman-generators-for-containers-and-guest-executables) for instructions on setting up Yeoman.</span><span class="sxs-lookup"><span data-stu-id="ee148-115">If Yeoman isn't already installed, see [Service Fabric getting started with Linux](service-fabric-get-started-linux.md#set-up-yeoman-generators-for-containers-and-guest-executables) for instructions on setting up Yeoman.</span></span> <span data-ttu-id="ee148-116">Run the following command to install the Service Fabric Yeoman template generator for Java.</span><span class="sxs-lookup"><span data-stu-id="ee148-116">Run the following command to install the Service Fabric Yeoman template generator for Java.</span></span>

  ```bash
  npm install -g generator-azuresfjava
  ```

## <a name="basic-concepts"></a><span data-ttu-id="ee148-117">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="ee148-117">Basic concepts</span></span>
<span data-ttu-id="ee148-118">To get started with Reliable Actors, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="ee148-118">To get started with Reliable Actors, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="ee148-119">**Actor service**.</span><span class="sxs-lookup"><span data-stu-id="ee148-119">**Actor service**.</span></span> <span data-ttu-id="ee148-120">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ee148-120">Reliable Actors are packaged in Reliable Services that can be deployed in the Service Fabric infrastructure.</span></span> <span data-ttu-id="ee148-121">Actor instances are activated in a named service instance.</span><span class="sxs-lookup"><span data-stu-id="ee148-121">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="ee148-122">**Actor registration**.</span><span class="sxs-lookup"><span data-stu-id="ee148-122">**Actor registration**.</span></span> <span data-ttu-id="ee148-123">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="ee148-123">As with Reliable Services, a Reliable Actor service needs to be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="ee148-124">In addition, the actor type needs to be registered with the Actor runtime.</span><span class="sxs-lookup"><span data-stu-id="ee148-124">In addition, the actor type needs to be registered with the Actor runtime.</span></span>
* <span data-ttu-id="ee148-125">**Actor interface**.</span><span class="sxs-lookup"><span data-stu-id="ee148-125">**Actor interface**.</span></span> <span data-ttu-id="ee148-126">The actor interface is used to define a strongly typed public interface of an actor.</span><span class="sxs-lookup"><span data-stu-id="ee148-126">The actor interface is used to define a strongly typed public interface of an actor.</span></span> <span data-ttu-id="ee148-127">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span><span class="sxs-lookup"><span data-stu-id="ee148-127">In the Reliable Actor model terminology, the actor interface defines the types of messages that the actor can understand and process.</span></span> <span data-ttu-id="ee148-128">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span><span class="sxs-lookup"><span data-stu-id="ee148-128">The actor interface is used by other actors and client applications to "send" (asynchronously) messages to the actor.</span></span> <span data-ttu-id="ee148-129">Reliable Actors can implement multiple interfaces.</span><span class="sxs-lookup"><span data-stu-id="ee148-129">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="ee148-130">**ActorProxy class**.</span><span class="sxs-lookup"><span data-stu-id="ee148-130">**ActorProxy class**.</span></span> <span data-ttu-id="ee148-131">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span><span class="sxs-lookup"><span data-stu-id="ee148-131">The ActorProxy class is used by client applications to invoke the methods exposed through the actor interface.</span></span> <span data-ttu-id="ee148-132">The ActorProxy class provides two important functionalities:</span><span class="sxs-lookup"><span data-stu-id="ee148-132">The ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="ee148-133">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span><span class="sxs-lookup"><span data-stu-id="ee148-133">Name resolution: It is able to locate the actor in the cluster (find the node of the cluster where it is hosted).</span></span>
  * <span data-ttu-id="ee148-134">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="ee148-134">Failure handling: It can retry method invocations and re-resolve the actor location after, for example, a failure that requires the actor to be relocated to another node in the cluster.</span></span>

<span data-ttu-id="ee148-135">The following rules that pertain to actor interfaces are worth mentioning:</span><span class="sxs-lookup"><span data-stu-id="ee148-135">The following rules that pertain to actor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="ee148-136">Actor interface methods cannot be overloaded.</span><span class="sxs-lookup"><span data-stu-id="ee148-136">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="ee148-137">Actor interface methods must not have out, ref, or optional parameters.</span><span class="sxs-lookup"><span data-stu-id="ee148-137">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="ee148-138">Generic interfaces are not supported.</span><span class="sxs-lookup"><span data-stu-id="ee148-138">Generic interfaces are not supported.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="ee148-139">Create the application</span><span class="sxs-lookup"><span data-stu-id="ee148-139">Create the application</span></span>
<span data-ttu-id="ee148-140">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="ee148-140">A Service Fabric application contains one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="ee148-141">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span><span class="sxs-lookup"><span data-stu-id="ee148-141">The generator you installed in the last section, makes it easy to create your first service and to add more later.</span></span>  <span data-ttu-id="ee148-142">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span><span class="sxs-lookup"><span data-stu-id="ee148-142">You can also create, build, and deploy Service Fabric Java applications using a plugin for Eclipse.</span></span> <span data-ttu-id="ee148-143">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="ee148-143">See [Create and deploy your first Java application using Eclipse](service-fabric-get-started-eclipse.md).</span></span> <span data-ttu-id="ee148-144">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span><span class="sxs-lookup"><span data-stu-id="ee148-144">For this quick start, use Yeoman to create an application with a single service that stores and gets a counter value.</span></span>

1. <span data-ttu-id="ee148-145">In a terminal, type ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="ee148-145">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="ee148-146">Name your application.</span><span class="sxs-lookup"><span data-stu-id="ee148-146">Name your application.</span></span>
3. <span data-ttu-id="ee148-147">Choose the type of your first service and name it.</span><span class="sxs-lookup"><span data-stu-id="ee148-147">Choose the type of your first service and name it.</span></span> <span data-ttu-id="ee148-148">For this tutorial, choose a Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="ee148-148">For this tutorial, choose a Reliable Actor Service.</span></span> <span data-ttu-id="ee148-149">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span><span class="sxs-lookup"><span data-stu-id="ee148-149">For more information about the other types of services, see [Service Fabric programming model overview](service-fabric-choose-framework.md).</span></span>
   <span data-ttu-id="ee148-150">![Service Fabric Yeoman generator for Java][sf-yeoman]</span><span class="sxs-lookup"><span data-stu-id="ee148-150">![Service Fabric Yeoman generator for Java][sf-yeoman]</span></span>

<span data-ttu-id="ee148-151">If you name the application "HelloWorldActorApplication" and the actor "HelloWorldActor", the following scaffolding is created:</span><span class="sxs-lookup"><span data-stu-id="ee148-151">If you name the application "HelloWorldActorApplication" and the actor "HelloWorldActor", the following scaffolding is created:</span></span>

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
## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="ee148-152">Reliable Actors basic building blocks</span><span class="sxs-lookup"><span data-stu-id="ee148-152">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="ee148-153">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span><span class="sxs-lookup"><span data-stu-id="ee148-153">The basic concepts described earlier translate into the basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="ee148-154">Actor interface</span><span class="sxs-lookup"><span data-stu-id="ee148-154">Actor interface</span></span>
<span data-ttu-id="ee148-155">This contains the interface definition for the actor.</span><span class="sxs-lookup"><span data-stu-id="ee148-155">This contains the interface definition for the actor.</span></span> <span data-ttu-id="ee148-156">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span><span class="sxs-lookup"><span data-stu-id="ee148-156">This interface defines the actor contract that is shared by the actor implementation and the clients calling the actor, so it typically makes sense to define it in a place that is separate from the actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="ee148-157">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="ee148-157">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="ee148-158">Actor service</span><span class="sxs-lookup"><span data-stu-id="ee148-158">Actor service</span></span>
<span data-ttu-id="ee148-159">This contains your actor implementation and actor registration code.</span><span class="sxs-lookup"><span data-stu-id="ee148-159">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="ee148-160">The actor class implements the actor interface.</span><span class="sxs-lookup"><span data-stu-id="ee148-160">The actor class implements the actor interface.</span></span> <span data-ttu-id="ee148-161">This is where your actor does its work.</span><span class="sxs-lookup"><span data-stu-id="ee148-161">This is where your actor does its work.</span></span>

<span data-ttu-id="ee148-162">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="ee148-162">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends FabricActor implements HelloWorldActor {
    private Logger logger = Logger.getLogger(this.getClass().getName());

    public HelloWorldActorImpl(FabricActorService actorService, ActorId actorId){
        super(actorService, actorId);
    }

    @Override
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

### <a name="actor-registration"></a><span data-ttu-id="ee148-163">Actor registration</span><span class="sxs-lookup"><span data-stu-id="ee148-163">Actor registration</span></span>
<span data-ttu-id="ee148-164">The actor service must be registered with a service type in the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="ee148-164">The actor service must be registered with a service type in the Service Fabric runtime.</span></span> <span data-ttu-id="ee148-165">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span><span class="sxs-lookup"><span data-stu-id="ee148-165">In order for the Actor Service to run your actor instances, your actor type must also be registered with the Actor Service.</span></span> <span data-ttu-id="ee148-166">The `ActorRuntime` registration method performs this work for actors.</span><span class="sxs-lookup"><span data-stu-id="ee148-166">The `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="ee148-167">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="ee148-167">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

private static final Logger logger = Logger.getLogger(HelloWorldActorHost.class.getName());
    
public static void main(String[] args) throws Exception {
        
        try {

            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new FabricActorService(context, actorType, (a,b)-> new HelloWorldActorImpl(a,b)), Duration.ofSeconds(10));
            Thread.sleep(Long.MAX_VALUE);
        } catch (Exception e) {
            logger.log(Level.SEVERE, "Exception occured", e);
            throw e;
        }
    }
}
```

## <a name="build-the-application"></a><span data-ttu-id="ee148-168">Build the application</span><span class="sxs-lookup"><span data-stu-id="ee148-168">Build the application</span></span>
<span data-ttu-id="ee148-169">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span><span class="sxs-lookup"><span data-stu-id="ee148-169">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the application from the terminal.</span></span>
<span data-ttu-id="ee148-170">Service Fabric Java dependencies get fetched from Maven.</span><span class="sxs-lookup"><span data-stu-id="ee148-170">Service Fabric Java dependencies get fetched from Maven.</span></span> <span data-ttu-id="ee148-171">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span><span class="sxs-lookup"><span data-stu-id="ee148-171">To build and work on the Service Fabric Java applications, you need to ensure that you have JDK and Gradle installed.</span></span> <span data-ttu-id="ee148-172">If they are not installed, see [Service Fabric getting started with Linux](service-fabric-get-started-linux.md#set-up-java-development) for instructions on installing JDK and Gradle.</span><span class="sxs-lookup"><span data-stu-id="ee148-172">If they are not installed, see [Service Fabric getting started with Linux](service-fabric-get-started-linux.md#set-up-java-development) for instructions on installing JDK and Gradle.</span></span>

<span data-ttu-id="ee148-173">To build and package the application, run the following:</span><span class="sxs-lookup"><span data-stu-id="ee148-173">To build and package the application, run the following:</span></span>

  ```bash
  cd HelloWorldActorApplication
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="ee148-174">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="ee148-174">Deploy the application</span></span>
<span data-ttu-id="ee148-175">Once the application is built, you can deploy it to the local cluster.</span><span class="sxs-lookup"><span data-stu-id="ee148-175">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="ee148-176">Connect to the local Service Fabric cluster (the cluster must be [setup and running](service-fabric-get-started-linux.md#set-up-a-local-cluster)).</span><span class="sxs-lookup"><span data-stu-id="ee148-176">Connect to the local Service Fabric cluster (the cluster must be [setup and running](service-fabric-get-started-linux.md#set-up-a-local-cluster)).</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="ee148-177">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="ee148-177">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="ee148-178">Deploying the built application is the same as any other Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="ee148-178">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="ee148-179">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="ee148-179">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="ee148-180">Parameters to these commands can be found in the generated manifests inside the application package.</span><span class="sxs-lookup"><span data-stu-id="ee148-180">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="ee148-181">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="ee148-181">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span>
<span data-ttu-id="ee148-182">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="ee148-182">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

> [!IMPORTANT]
> To deploy the application to a secure Linux cluster in Azure, you need to configure a certificate to validate your application with the Service Fabric runtime. Doing so enables your Reliable Actors services to communicate with the underlying Service Fabric runtime APIs. To learn more, see [Configure a Reliable Services app to run on Linux clusters](./service-fabric-configure-certificates-linux.md#configure-a-reliable-services-app-to-run-on-linux-clusters).  
>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="ee148-186">Start the test client and perform a failover</span><span class="sxs-lookup"><span data-stu-id="ee148-186">Start the test client and perform a failover</span></span>
<span data-ttu-id="ee148-187">Actors do not do anything on their own, they require another service or client to send them messages.</span><span class="sxs-lookup"><span data-stu-id="ee148-187">Actors do not do anything on their own, they require another service or client to send them messages.</span></span> <span data-ttu-id="ee148-188">The actor template includes a simple test script that you can use to interact with the actor service.</span><span class="sxs-lookup"><span data-stu-id="ee148-188">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

> [!Note]
> The test client uses the ActorProxy class to communicate with actors, which must run within the same cluster as the actor service or share the same IP address space.  You can run the test client on the same computer as the local development cluster.  To communicate with actors in a remote cluster, however, you must deploy a gateway on the cluster that handles external communication with the actors.

1. <span data-ttu-id="ee148-192">Run the script using the watch utility to see the output of the actor service.</span><span class="sxs-lookup"><span data-stu-id="ee148-192">Run the script using the watch utility to see the output of the actor service.</span></span>  <span data-ttu-id="ee148-193">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span><span class="sxs-lookup"><span data-stu-id="ee148-193">The test script calls the `setCountAsync()` method on the actor to increment a counter, calls the `getCountAsync()` method on the actor to get the new counter value, and displays that value to the console.</span></span>

   <span data-ttu-id="ee148-194">In case of MAC OS X, you need to copy the HelloWorldTestClient folder into the some location inside the container by running the following additional commands.</span><span class="sxs-lookup"><span data-stu-id="ee148-194">In case of MAC OS X, you need to copy the HelloWorldTestClient folder into the some location inside the container by running the following additional commands.</span></span>    
    
    ```bash
     docker cp HelloWorldTestClient [first-four-digits-of-container-ID]:/home
     docker exec -it [first-four-digits-of-container-ID] /bin/bash
     cd /home
     ```

    ```bash
    cd HelloWorldActorTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="ee148-195">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span><span class="sxs-lookup"><span data-stu-id="ee148-195">In Service Fabric Explorer, locate the node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="ee148-196">In the screenshot below, it is node 3.</span><span class="sxs-lookup"><span data-stu-id="ee148-196">In the screenshot below, it is node 3.</span></span> <span data-ttu-id="ee148-197">The primary service replica handles read and write operations.</span><span class="sxs-lookup"><span data-stu-id="ee148-197">The primary service replica handles read and write operations.</span></span>  <span data-ttu-id="ee148-198">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span><span class="sxs-lookup"><span data-stu-id="ee148-198">Changes in service state are then replicated out to the secondary replicas, running on nodes 0 and 1 in the screen shot below.</span></span>

    ![Finding the primary replica in Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="ee148-200">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span><span class="sxs-lookup"><span data-stu-id="ee148-200">In **Nodes**, click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="ee148-201">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span><span class="sxs-lookup"><span data-stu-id="ee148-201">This action restarts the node running the primary service replica and forces a failover to one of the secondary replicas running on another node.</span></span>  <span data-ttu-id="ee148-202">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span><span class="sxs-lookup"><span data-stu-id="ee148-202">That secondary replica is promoted to primary, another secondary replica is created on a different node, and the primary replica begins to take read/write operations.</span></span> <span data-ttu-id="ee148-203">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span><span class="sxs-lookup"><span data-stu-id="ee148-203">As the node restarts, watch the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="remove-the-application"></a><span data-ttu-id="ee148-204">Remove the application</span><span class="sxs-lookup"><span data-stu-id="ee148-204">Remove the application</span></span>
<span data-ttu-id="ee148-205">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span><span class="sxs-lookup"><span data-stu-id="ee148-205">Use the uninstall script provided in the template to delete the application instance, unregister the application package, and remove the application package from the cluster's image store.</span></span>

```bash
./uninstall.sh
```

<span data-ttu-id="ee148-206">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span><span class="sxs-lookup"><span data-stu-id="ee148-206">In Service Fabric explorer you see that the application and application type no longer appear in the **Applications** node.</span></span>

## <a name="service-fabric-java-libraries-on-maven"></a><span data-ttu-id="ee148-207">Service Fabric Java libraries on Maven</span><span class="sxs-lookup"><span data-stu-id="ee148-207">Service Fabric Java libraries on Maven</span></span>
<span data-ttu-id="ee148-208">Service Fabric Java libraries have been hosted in Maven.</span><span class="sxs-lookup"><span data-stu-id="ee148-208">Service Fabric Java libraries have been hosted in Maven.</span></span> <span data-ttu-id="ee148-209">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span><span class="sxs-lookup"><span data-stu-id="ee148-209">You can add the dependencies in the ``pom.xml`` or ``build.gradle`` of your projects to use Service Fabric Java libraries from **mavenCentral**.</span></span> 

### <a name="actors"></a><span data-ttu-id="ee148-210">Actors</span><span class="sxs-lookup"><span data-stu-id="ee148-210">Actors</span></span>

<span data-ttu-id="ee148-211">Service Fabric Reliable Actor support for your application.</span><span class="sxs-lookup"><span data-stu-id="ee148-211">Service Fabric Reliable Actor support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors:1.0.0'
  }
  ```

### <a name="services"></a><span data-ttu-id="ee148-212">Services</span><span class="sxs-lookup"><span data-stu-id="ee148-212">Services</span></span>

<span data-ttu-id="ee148-213">Service Fabric Reliable Services support for your application.</span><span class="sxs-lookup"><span data-stu-id="ee148-213">Service Fabric Reliable Services support for your application.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services:1.0.0'
  }
  ```

### <a name="others"></a><span data-ttu-id="ee148-214">Others</span><span class="sxs-lookup"><span data-stu-id="ee148-214">Others</span></span>
#### <a name="transport"></a><span data-ttu-id="ee148-215">Transport</span><span class="sxs-lookup"><span data-stu-id="ee148-215">Transport</span></span>

<span data-ttu-id="ee148-216">Transport layer support for Service Fabric Java application.</span><span class="sxs-lookup"><span data-stu-id="ee148-216">Transport layer support for Service Fabric Java application.</span></span> <span data-ttu-id="ee148-217">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span><span class="sxs-lookup"><span data-stu-id="ee148-217">You do not need to explicitly add this dependency to your Reliable Actor or Service applications, unless you program at the transport layer.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport:1.0.0'
  }
  ```

#### <a name="fabric-support"></a><span data-ttu-id="ee148-218">Fabric support</span><span class="sxs-lookup"><span data-stu-id="ee148-218">Fabric support</span></span>

<span data-ttu-id="ee148-219">System level support for Service Fabric, which talks to native Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="ee148-219">System level support for Service Fabric, which talks to native Service Fabric runtime.</span></span> <span data-ttu-id="ee148-220">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span><span class="sxs-lookup"><span data-stu-id="ee148-220">You do not need to explicitly add this dependency to your Reliable Actor or Service applications.</span></span> <span data-ttu-id="ee148-221">This gets fetched automatically from Maven, when you include the other dependencies above.</span><span class="sxs-lookup"><span data-stu-id="ee148-221">This gets fetched automatically from Maven, when you include the other dependencies above.</span></span>

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf</artifactId>
      <version>1.0.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf:1.0.0'
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="ee148-222">Next steps</span><span class="sxs-lookup"><span data-stu-id="ee148-222">Next steps</span></span>

* [<span data-ttu-id="ee148-223">Create your first Service Fabric Java application on Linux using Eclipse</span><span class="sxs-lookup"><span data-stu-id="ee148-223">Create your first Service Fabric Java application on Linux using Eclipse</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="ee148-224">Learn more about Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="ee148-224">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="ee148-225">Interact with Service Fabric clusters using the Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="ee148-225">Interact with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="ee148-226">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="ee148-226">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="ee148-227">Getting started with Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="ee148-227">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
