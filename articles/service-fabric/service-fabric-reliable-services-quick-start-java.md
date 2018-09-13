---
title: Create your first Azure Service Fabric reliable service in Java | Microsoft Docs
description: Introduction to creating a Microsoft Azure Service Fabric application with stateless and stateful services.
services: service-fabric
documentationcenter: java
author: suhuruli
manager: timlt
editor: ''
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/02/2017
ms.author: suhuruli
ms.openlocfilehash: 44b8e632984a240ae137e5b52ba96f292e2aa0fd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44811745"
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="751c3-103">Get started with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="751c3-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-quick-start.md)
> * [Java on Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="751c3-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span><span class="sxs-lookup"><span data-stu-id="751c3-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="751c3-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="751c3-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="751c3-108">Installation and setup</span><span class="sxs-lookup"><span data-stu-id="751c3-108">Installation and setup</span></span>
<span data-ttu-id="751c3-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span><span class="sxs-lookup"><span data-stu-id="751c3-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="751c3-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="751c3-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="751c3-111">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="751c3-111">Basic concepts</span></span>
<span data-ttu-id="751c3-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="751c3-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="751c3-113">**Service type**: This is your service implementation.</span><span class="sxs-lookup"><span data-stu-id="751c3-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="751c3-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span><span class="sxs-lookup"><span data-stu-id="751c3-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="751c3-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span><span class="sxs-lookup"><span data-stu-id="751c3-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="751c3-116">Service instances are in fact object instantiations of your service class that you write.</span><span class="sxs-lookup"><span data-stu-id="751c3-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="751c3-117">**Service host**: The named service instances you create need to run inside a host.</span><span class="sxs-lookup"><span data-stu-id="751c3-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="751c3-118">The service host is just a process where instances of your service can run.</span><span class="sxs-lookup"><span data-stu-id="751c3-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="751c3-119">**Service registration**: Registration brings everything together.</span><span class="sxs-lookup"><span data-stu-id="751c3-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="751c3-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span><span class="sxs-lookup"><span data-stu-id="751c3-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="751c3-121">Create a stateless service</span><span class="sxs-lookup"><span data-stu-id="751c3-121">Create a stateless service</span></span>
<span data-ttu-id="751c3-122">Start by creating a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="751c3-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="751c3-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span><span class="sxs-lookup"><span data-stu-id="751c3-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="751c3-124">Start by running the following Yeoman command:</span><span class="sxs-lookup"><span data-stu-id="751c3-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="751c3-125">Follow the instructions to create a **Reliable Stateless Service**.</span><span class="sxs-lookup"><span data-stu-id="751c3-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="751c3-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="751c3-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="751c3-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="751c3-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```
### <a name="service-registration"></a><span data-ttu-id="751c3-128">Service registration</span><span class="sxs-lookup"><span data-stu-id="751c3-128">Service registration</span></span>
<span data-ttu-id="751c3-129">Service types must be registered with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="751c3-129">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="751c3-130">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="751c3-130">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="751c3-131">Service registration is performed in the process main entry point.</span><span class="sxs-lookup"><span data-stu-id="751c3-131">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="751c3-132">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="751c3-132">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="implement-the-service"></a><span data-ttu-id="751c3-133">Implement the service</span><span class="sxs-lookup"><span data-stu-id="751c3-133">Implement the service</span></span>

<span data-ttu-id="751c3-134">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="751c3-134">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="751c3-135">This class defines the service type, and can run any code.</span><span class="sxs-lookup"><span data-stu-id="751c3-135">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="751c3-136">The service API provides two entry points for your code:</span><span class="sxs-lookup"><span data-stu-id="751c3-136">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="751c3-137">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span><span class="sxs-lookup"><span data-stu-id="751c3-137">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="751c3-138">A communication entry point where you can plug in your communication stack of choice.</span><span class="sxs-lookup"><span data-stu-id="751c3-138">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="751c3-139">This is where you can start receiving requests from users and other services.</span><span class="sxs-lookup"><span data-stu-id="751c3-139">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="751c3-140">This tutorial focuses on the `runAsync()` entry point method.</span><span class="sxs-lookup"><span data-stu-id="751c3-140">This tutorial focuses on the `runAsync()` entry point method.</span></span> <span data-ttu-id="751c3-141">This is where you can immediately start running your code.</span><span class="sxs-lookup"><span data-stu-id="751c3-141">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="751c3-142">RunAsync</span><span class="sxs-lookup"><span data-stu-id="751c3-142">RunAsync</span></span>
<span data-ttu-id="751c3-143">The platform calls this method when an instance of a service is placed and ready to execute.</span><span class="sxs-lookup"><span data-stu-id="751c3-143">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="751c3-144">For a stateless service, that means when the service instance is opened.</span><span class="sxs-lookup"><span data-stu-id="751c3-144">For a stateless service, that means when the service instance is opened.</span></span> <span data-ttu-id="751c3-145">A cancellation token is provided to coordinate when your service instance needs to be closed.</span><span class="sxs-lookup"><span data-stu-id="751c3-145">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="751c3-146">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span><span class="sxs-lookup"><span data-stu-id="751c3-146">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="751c3-147">This can happen for various reasons, including:</span><span class="sxs-lookup"><span data-stu-id="751c3-147">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="751c3-148">The system moves your service instances for resource balancing.</span><span class="sxs-lookup"><span data-stu-id="751c3-148">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="751c3-149">Faults occur in your code.</span><span class="sxs-lookup"><span data-stu-id="751c3-149">Faults occur in your code.</span></span>
* <span data-ttu-id="751c3-150">The application or system is upgraded.</span><span class="sxs-lookup"><span data-stu-id="751c3-150">The application or system is upgraded.</span></span>
* <span data-ttu-id="751c3-151">The underlying hardware experiences an outage.</span><span class="sxs-lookup"><span data-stu-id="751c3-151">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="751c3-152">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span><span class="sxs-lookup"><span data-stu-id="751c3-152">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="751c3-153">`runAsync()` should not block synchronously.</span><span class="sxs-lookup"><span data-stu-id="751c3-153">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="751c3-154">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span><span class="sxs-lookup"><span data-stu-id="751c3-154">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="751c3-155">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="751c3-155">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="751c3-156">Cancellation</span><span class="sxs-lookup"><span data-stu-id="751c3-156">Cancellation</span></span>
<span data-ttu-id="751c3-157">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span><span class="sxs-lookup"><span data-stu-id="751c3-157">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="751c3-158">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span><span class="sxs-lookup"><span data-stu-id="751c3-158">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="751c3-159">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span><span class="sxs-lookup"><span data-stu-id="751c3-159">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="751c3-160">The following example demonstrates how to handle a cancellation event:</span><span class="sxs-lookup"><span data-stu-id="751c3-160">The following example demonstrates how to handle a cancellation event:</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

    // TODO: Replace the following sample code with your own logic
    // or remove this runAsync override if it's not needed in your service.

    return CompletableFuture.runAsync(() -> {
        long iterations = 0;
        while(true)
        {
        cancellationToken.throwIfCancellationRequested();
        logger.log(Level.INFO, "Working-{0}", ++iterations);

        try {
            Thread.sleep(1000);
        } catch (InterruptedException ex){}
        }
    });
}
```

<span data-ttu-id="751c3-161">In this stateless service example, the count is stored in a local variable.</span><span class="sxs-lookup"><span data-stu-id="751c3-161">In this stateless service example, the count is stored in a local variable.</span></span> <span data-ttu-id="751c3-162">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span><span class="sxs-lookup"><span data-stu-id="751c3-162">But because this is a stateless service, the value that's stored exists only for the current lifecycle of its service instance.</span></span> <span data-ttu-id="751c3-163">When the service moves or restarts, the value is lost.</span><span class="sxs-lookup"><span data-stu-id="751c3-163">When the service moves or restarts, the value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="751c3-164">Create a stateful service</span><span class="sxs-lookup"><span data-stu-id="751c3-164">Create a stateful service</span></span>
<span data-ttu-id="751c3-165">Service Fabric introduces a new kind of service that is stateful.</span><span class="sxs-lookup"><span data-stu-id="751c3-165">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="751c3-166">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span><span class="sxs-lookup"><span data-stu-id="751c3-166">A stateful service can maintain state reliably within the service itself, co-located with the code that's using it.</span></span> <span data-ttu-id="751c3-167">State is made highly available by Service Fabric without the need to persist state to an external store.</span><span class="sxs-lookup"><span data-stu-id="751c3-167">State is made highly available by Service Fabric without the need to persist state to an external store.</span></span>

<span data-ttu-id="751c3-168">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span><span class="sxs-lookup"><span data-stu-id="751c3-168">To convert a counter value from stateless to highly available and persistent, even when the service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="751c3-169">In the same directory as the HelloWorld application, you can add a new service by running the `yo azuresfjava:AddService` command.</span><span class="sxs-lookup"><span data-stu-id="751c3-169">In the same directory as the HelloWorld application, you can add a new service by running the `yo azuresfjava:AddService` command.</span></span> <span data-ttu-id="751c3-170">Choose the "Reliable Stateful Service" for your framework and name the service "HelloWorldStateful".</span><span class="sxs-lookup"><span data-stu-id="751c3-170">Choose the "Reliable Stateful Service" for your framework and name the service "HelloWorldStateful".</span></span> 

<span data-ttu-id="751c3-171">Your application should now have two services: the stateless service HelloWorld and the stateful service HelloWorldStateful.</span><span class="sxs-lookup"><span data-stu-id="751c3-171">Your application should now have two services: the stateless service HelloWorld and the stateful service HelloWorldStateful.</span></span>

<span data-ttu-id="751c3-172">A stateful service has the same entry points as a stateless service.</span><span class="sxs-lookup"><span data-stu-id="751c3-172">A stateful service has the same entry points as a stateless service.</span></span> <span data-ttu-id="751c3-173">The main difference is the availability of a state provider that can store state reliably.</span><span class="sxs-lookup"><span data-stu-id="751c3-173">The main difference is the availability of a state provider that can store state reliably.</span></span> <span data-ttu-id="751c3-174">Service Fabric comes with a state provider implementation called Reliable Collections, which lets you create replicated data structures through the Reliable State Manager.</span><span class="sxs-lookup"><span data-stu-id="751c3-174">Service Fabric comes with a state provider implementation called Reliable Collections, which lets you create replicated data structures through the Reliable State Manager.</span></span> <span data-ttu-id="751c3-175">A stateful Reliable Service uses this state provider by default.</span><span class="sxs-lookup"><span data-stu-id="751c3-175">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="751c3-176">Open HelloWorldStateful.java in **HelloWorldStateful -> src**, which contains the following RunAsync method:</span><span class="sxs-lookup"><span data-stu-id="751c3-176">Open HelloWorldStateful.java in **HelloWorldStateful -> src**, which contains the following RunAsync method:</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    Transaction tx = stateManager.createTransaction();
    return this.stateManager.<String, Long>getOrAddReliableHashMapAsync("myHashMap").thenCompose((map) -> {
        return map.computeAsync(tx, "counter", (k, v) -> {
            if (v == null)
                return 1L;
            else
                return ++v;
            }, Duration.ofSeconds(4), cancellationToken)
                .thenCompose((r) -> tx.commitAsync())
                .whenComplete((r, e) -> {
            try {
                tx.close();
            } catch (Exception e) {
                logger.log(Level.SEVERE, e.getMessage());
            }
        });
    });
}
```

### <a name="runasync"></a><span data-ttu-id="751c3-177">RunAsync</span><span class="sxs-lookup"><span data-stu-id="751c3-177">RunAsync</span></span>
<span data-ttu-id="751c3-178">`RunAsync()` operates similarly in stateful and stateless services.</span><span class="sxs-lookup"><span data-stu-id="751c3-178">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="751c3-179">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="751c3-179">However, in a stateful service, the platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="751c3-180">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span><span class="sxs-lookup"><span data-stu-id="751c3-180">This work can include ensuring that the Reliable State Manager and Reliable Collections are ready to use.</span></span>

### <a name="reliable-collections-and-the-reliable-state-manager"></a><span data-ttu-id="751c3-181">Reliable Collections and the Reliable State Manager</span><span class="sxs-lookup"><span data-stu-id="751c3-181">Reliable Collections and the Reliable State Manager</span></span>
```java
ReliableHashMap<String,Long> map = this.stateManager.<String, Long>getOrAddReliableHashMapAsync("myHashMap")
```

<span data-ttu-id="751c3-182">[ReliableHashMap](https://docs.microsoft.com/java/api/microsoft.servicefabric.data.collections._reliable_hash_map) is a dictionary implementation that you can use to reliably store state in the service.</span><span class="sxs-lookup"><span data-stu-id="751c3-182">[ReliableHashMap](https://docs.microsoft.com/java/api/microsoft.servicefabric.data.collections._reliable_hash_map) is a dictionary implementation that you can use to reliably store state in the service.</span></span> <span data-ttu-id="751c3-183">With Service Fabric and Reliable HashMaps, you can store data directly in your service without the need for an external persistent store.</span><span class="sxs-lookup"><span data-stu-id="751c3-183">With Service Fabric and Reliable HashMaps, you can store data directly in your service without the need for an external persistent store.</span></span> <span data-ttu-id="751c3-184">Reliable HashMaps make your data highly available.</span><span class="sxs-lookup"><span data-stu-id="751c3-184">Reliable HashMaps make your data highly available.</span></span> <span data-ttu-id="751c3-185">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span><span class="sxs-lookup"><span data-stu-id="751c3-185">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="751c3-186">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span><span class="sxs-lookup"><span data-stu-id="751c3-186">It also provides an API that abstracts away the complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="751c3-187">Reliable Collections can store any Java type, including your custom types, with a couple of caveats:</span><span class="sxs-lookup"><span data-stu-id="751c3-187">Reliable Collections can store any Java type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="751c3-188">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable HashMap stores your data to local disk on each replica.</span><span class="sxs-lookup"><span data-stu-id="751c3-188">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable HashMap stores your data to local disk on each replica.</span></span> <span data-ttu-id="751c3-189">This means that everything that is stored in Reliable HashMaps must be *serializable*.</span><span class="sxs-lookup"><span data-stu-id="751c3-189">This means that everything that is stored in Reliable HashMaps must be *serializable*.</span></span> 
* <span data-ttu-id="751c3-190">Objects are replicated for high availability when you commit transactions on Reliable HashMaps.</span><span class="sxs-lookup"><span data-stu-id="751c3-190">Objects are replicated for high availability when you commit transactions on Reliable HashMaps.</span></span> <span data-ttu-id="751c3-191">Objects stored in Reliable HashMaps are kept in local memory in your service.</span><span class="sxs-lookup"><span data-stu-id="751c3-191">Objects stored in Reliable HashMaps are kept in local memory in your service.</span></span> <span data-ttu-id="751c3-192">This means that you have a local reference to the object.</span><span class="sxs-lookup"><span data-stu-id="751c3-192">This means that you have a local reference to the object.</span></span>
  
   <span data-ttu-id="751c3-193">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span><span class="sxs-lookup"><span data-stu-id="751c3-193">It is important that you do not mutate local instances of those objects without performing an update operation on the reliable collection in a transaction.</span></span> <span data-ttu-id="751c3-194">This is because changes to local instances of objects will not be replicated automatically.</span><span class="sxs-lookup"><span data-stu-id="751c3-194">This is because changes to local instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="751c3-195">You must reinsert the object back into the dictionary or use one of the *update* methods on the dictionary.</span><span class="sxs-lookup"><span data-stu-id="751c3-195">You must reinsert the object back into the dictionary or use one of the *update* methods on the dictionary.</span></span>

<span data-ttu-id="751c3-196">The Reliable State Manager manages Reliable HashMaps for you.</span><span class="sxs-lookup"><span data-stu-id="751c3-196">The Reliable State Manager manages Reliable HashMaps for you.</span></span> <span data-ttu-id="751c3-197">You can ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span><span class="sxs-lookup"><span data-stu-id="751c3-197">You can ask the Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="751c3-198">The Reliable State Manager ensures that you get a reference back.</span><span class="sxs-lookup"><span data-stu-id="751c3-198">The Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="751c3-199">We don't recommend that you save references to reliable collection instances in class member variables or properties.</span><span class="sxs-lookup"><span data-stu-id="751c3-199">We don't recommend that you save references to reliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="751c3-200">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span><span class="sxs-lookup"><span data-stu-id="751c3-200">Special care must be taken to ensure that the reference is set to an instance at all times in the service lifecycle.</span></span> <span data-ttu-id="751c3-201">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span><span class="sxs-lookup"><span data-stu-id="751c3-201">The Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>


### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="751c3-202">Transactional and asynchronous operations</span><span class="sxs-lookup"><span data-stu-id="751c3-202">Transactional and asynchronous operations</span></span>
```java
return map.computeAsync(tx, "counter", (k, v) -> {
    if (v == null)
        return 1L;
    else
        return ++v;
    }, Duration.ofSeconds(4), cancellationToken)
        .thenCompose((r) -> tx.commitAsync())
        .whenComplete((r, e) -> {
    try {
        tx.close();
    } catch (Exception e) {
        logger.log(Level.SEVERE, e.getMessage());
    }
});
```

<span data-ttu-id="751c3-203">Operations on Reliable HashMaps are asynchronous.</span><span class="sxs-lookup"><span data-stu-id="751c3-203">Operations on Reliable HashMaps are asynchronous.</span></span> <span data-ttu-id="751c3-204">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span><span class="sxs-lookup"><span data-stu-id="751c3-204">This is because write operations with Reliable Collections perform I/O operations to replicate and persist data to disk.</span></span>

<span data-ttu-id="751c3-205">Reliable HashMap operations are *transactional*, so that you can keep state consistent across multiple Reliable HashMaps and operations.</span><span class="sxs-lookup"><span data-stu-id="751c3-205">Reliable HashMap operations are *transactional*, so that you can keep state consistent across multiple Reliable HashMaps and operations.</span></span> <span data-ttu-id="751c3-206">For example, you may get a work item from one Reliable Dictionary, perform an operation on it, and save the result in another Reliable HashMap, all within a single transaction.</span><span class="sxs-lookup"><span data-stu-id="751c3-206">For example, you may get a work item from one Reliable Dictionary, perform an operation on it, and save the result in another Reliable HashMap, all within a single transaction.</span></span> <span data-ttu-id="751c3-207">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span><span class="sxs-lookup"><span data-stu-id="751c3-207">This is treated as an atomic operation, and it guarantees that either the entire operation will succeed or the entire operation will roll back.</span></span> <span data-ttu-id="751c3-208">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span><span class="sxs-lookup"><span data-stu-id="751c3-208">If an error occurs after you dequeue the item but before you save the result, the entire transaction is rolled back and the item remains in the queue for processing.</span></span>


## <a name="build-the-application"></a><span data-ttu-id="751c3-209">Build the application</span><span class="sxs-lookup"><span data-stu-id="751c3-209">Build the application</span></span>

<span data-ttu-id="751c3-210">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span><span class="sxs-lookup"><span data-stu-id="751c3-210">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and remove the application.</span></span> <span data-ttu-id="751c3-211">To run the application, first build the application with gradle:</span><span class="sxs-lookup"><span data-stu-id="751c3-211">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="751c3-212">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span><span class="sxs-lookup"><span data-stu-id="751c3-212">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

## <a name="deploy-the-application"></a><span data-ttu-id="751c3-213">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="751c3-213">Deploy the application</span></span>

<span data-ttu-id="751c3-214">Once the application is built, you can deploy it to the local cluster.</span><span class="sxs-lookup"><span data-stu-id="751c3-214">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="751c3-215">Connect to the local Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="751c3-215">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="751c3-216">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="751c3-216">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="751c3-217">Deploying the built application is the same as any other Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="751c3-217">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="751c3-218">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="751c3-218">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="751c3-219">Parameters to these commands can be found in the generated manifests inside the application package.</span><span class="sxs-lookup"><span data-stu-id="751c3-219">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="751c3-220">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="751c3-220">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="751c3-221">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="751c3-221">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

> [!IMPORTANT]
> To deploy the application to a secure Linux cluster in Azure, you need to configure a certificate to validate your application with the Service Fabric runtime. Doing so enables your Reliable Services services to communicate with the underlying Service Fabric runtime APIs. To learn more, see [Configure a Reliable Services app to run on Linux clusters](./service-fabric-configure-certificates-linux.md#configure-a-reliable-services-app-to-run-on-linux-clusters).  
>

## <a name="next-steps"></a><span data-ttu-id="751c3-225">Next steps</span><span class="sxs-lookup"><span data-stu-id="751c3-225">Next steps</span></span>

* [<span data-ttu-id="751c3-226">Getting started with Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="751c3-226">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
