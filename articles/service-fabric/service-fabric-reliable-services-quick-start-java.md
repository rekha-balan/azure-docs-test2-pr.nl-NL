---
title: Create your first reliable Azure microservice in Java | Microsoft Docs
description: Introduction to creating a Microsoft Azure Service Fabric application with stateless and stateful services.
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: ''
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/10/2017
ms.author: vturecek
ms.openlocfilehash: 3603e2fcd2fc56c2abab22f97f987ad89032a9c3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553269"
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="d3dc5-103">Get started with Reliable Services</span><span class="sxs-lookup"><span data-stu-id="d3dc5-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [C# on Windows](service-fabric-reliable-services-quick-start.md)
> * [Java on Linux](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="d3dc5-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-106">This article explains the basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="d3dc5-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="d3dc5-107">This Microsoft Virtual Academy video also shows you how to create a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="d3dc5-108">Installation and setup</span><span class="sxs-lookup"><span data-stu-id="d3dc5-108">Installation and setup</span></span>
<span data-ttu-id="d3dc5-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-109">Before you start, make sure you have the Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="d3dc5-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d3dc5-110">If you need to set it up, go to [getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="d3dc5-111">Basic concepts</span><span class="sxs-lookup"><span data-stu-id="d3dc5-111">Basic concepts</span></span>
<span data-ttu-id="d3dc5-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-112">To get started with Reliable Services, you only need to understand a few basic concepts:</span></span>

* <span data-ttu-id="d3dc5-113">**Service type**: This is your service implementation.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="d3dc5-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-114">It is defined by the class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="d3dc5-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-115">**Named service instance**: To run your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="d3dc5-116">Service instances are in fact object instantiations of your service class that you write.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="d3dc5-117">**Service host**: The named service instances you create need to run inside a host.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-117">**Service host**: The named service instances you create need to run inside a host.</span></span> <span data-ttu-id="d3dc5-118">The service host is just a process where instances of your service can run.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-118">The service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="d3dc5-119">**Service registration**: Registration brings everything together.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="d3dc5-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-120">The service type must be registered with the Service Fabric runtime in a service host to allow Service Fabric to create instances of it to run.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="d3dc5-121">Create a stateless service</span><span class="sxs-lookup"><span data-stu-id="d3dc5-121">Create a stateless service</span></span>
<span data-ttu-id="d3dc5-122">Start by creating a Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="d3dc5-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-123">The Service Fabric SDK for Linux includes a Yeoman generator to provide the scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="d3dc5-124">Start by running the following Yeoman command:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-124">Start by running the following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="d3dc5-125">Follow the instructions to create a **Reliable Stateless Service**.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-125">Follow the instructions to create a **Reliable Stateless Service**.</span></span> <span data-ttu-id="d3dc5-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span><span class="sxs-lookup"><span data-stu-id="d3dc5-126">For this tutorial, name the application "HelloWorldApplication" and the service "HelloWorld".</span></span> <span data-ttu-id="d3dc5-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-127">The result includes directories for the `HelloWorldApplication` and `HelloWorld`.</span></span>

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

## <a name="implement-the-service"></a><span data-ttu-id="d3dc5-128">Implement the service</span><span class="sxs-lookup"><span data-stu-id="d3dc5-128">Implement the service</span></span>
<span data-ttu-id="d3dc5-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="d3dc5-130">This class defines the service type, and can run any code.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-130">This class defines the service type, and can run any code.</span></span> <span data-ttu-id="d3dc5-131">The service API provides two entry points for your code:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-131">The service API provides two entry points for your code:</span></span>

* <span data-ttu-id="d3dc5-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="d3dc5-133">A communication entry point where you can plug in your communication stack of choice.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="d3dc5-134">This is where you can start receiving requests from users and other services.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="d3dc5-135">In this tutorial, we focus on the `runAsync()` entry point method.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-135">In this tutorial, we focus on the `runAsync()` entry point method.</span></span> <span data-ttu-id="d3dc5-136">This is where you can immediately start running your code.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="d3dc5-137">RunAsync</span><span class="sxs-lookup"><span data-stu-id="d3dc5-137">RunAsync</span></span>
<span data-ttu-id="d3dc5-138">The platform calls this method when an instance of a service is placed and ready to execute.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-138">The platform calls this method when an instance of a service is placed and ready to execute.</span></span> <span data-ttu-id="d3dc5-139">For a stateless service, that simply means when the service instance is opened.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-139">For a stateless service, that simply means when the service instance is opened.</span></span> <span data-ttu-id="d3dc5-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-140">A cancellation token is provided to coordinate when your service instance needs to be closed.</span></span> <span data-ttu-id="d3dc5-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-141">In Service Fabric, this open/close cycle of a service instance can occur many times over the lifetime of the service as a whole.</span></span> <span data-ttu-id="d3dc5-142">This can happen for various reasons, including:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="d3dc5-143">The system moves your service instances for resource balancing.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-143">The system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="d3dc5-144">Faults occur in your code.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-144">Faults occur in your code.</span></span>
* <span data-ttu-id="d3dc5-145">The application or system is upgraded.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-145">The application or system is upgraded.</span></span>
* <span data-ttu-id="d3dc5-146">The underlying hardware experiences an outage.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-146">The underlying hardware experiences an outage.</span></span>

<span data-ttu-id="d3dc5-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-147">This orchestration is managed by Service Fabric to keep your service highly available and properly balanced.</span></span>

<span data-ttu-id="d3dc5-148">`runAsync()` should not block synchronously.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="d3dc5-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-149">Your implementation of runAsync should return a CompletableFuture to allow the runtime to continue.</span></span> <span data-ttu-id="d3dc5-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-150">If your workload needs to implement a long running task that should be done inside the CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="d3dc5-151">Cancellation</span><span class="sxs-lookup"><span data-stu-id="d3dc5-151">Cancellation</span></span>
<span data-ttu-id="d3dc5-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-152">Cancellation of your workload is a cooperative effort orchestrated by the provided cancellation token.</span></span> <span data-ttu-id="d3dc5-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-153">The system waits for your task to end (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="d3dc5-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-154">It is important to honor the cancellation token, finish any work, and exit `runAsync()` as quickly as possible when the system requests cancellation.</span></span> <span data-ttu-id="d3dc5-155">The following example demonstrates how to handle a cancellation event:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-155">The following example demonstrates how to handle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace the following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="d3dc5-156">Service registration</span><span class="sxs-lookup"><span data-stu-id="d3dc5-156">Service registration</span></span>
<span data-ttu-id="d3dc5-157">Service types must be registered with the Service Fabric runtime.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-157">Service types must be registered with the Service Fabric runtime.</span></span> <span data-ttu-id="d3dc5-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-158">The service type is defined in the `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="d3dc5-159">Service registration is performed in the process main entry point.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-159">Service registration is performed in the process main entry point.</span></span> <span data-ttu-id="d3dc5-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-160">In this example, the process main entry point is `HelloWorldServiceHost.java`:</span></span>

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

## <a name="run-the-application"></a><span data-ttu-id="d3dc5-161">Run the application</span><span class="sxs-lookup"><span data-stu-id="d3dc5-161">Run the application</span></span>
<span data-ttu-id="d3dc5-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and undeploy the application.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-162">The Yeoman scaffolding includes a gradle script to build the application and bash scripts to deploy and undeploy the application.</span></span> <span data-ttu-id="d3dc5-163">To run the application, first build the application with gradle:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-163">To run the application, first build the application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="d3dc5-164">This produces a Service Fabric application package that can be deployed using Service Fabric Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-164">This produces a Service Fabric application package that can be deployed using Service Fabric Azure CLI.</span></span> <span data-ttu-id="d3dc5-165">The install.sh script contains the necessary Azure CLI commands to deploy the application package.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-165">The install.sh script contains the necessary Azure CLI commands to deploy the application package.</span></span> <span data-ttu-id="d3dc5-166">Run the install.sh script to deploy:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-166">Run the install.sh script to deploy:</span></span>

```bash
$ ./install.sh
```

