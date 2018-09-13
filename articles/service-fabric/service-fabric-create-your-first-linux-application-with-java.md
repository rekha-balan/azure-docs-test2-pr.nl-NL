---
title: Create your first Azure microservices app on Linux using Java | Microsoft Docs
description: Create and deploy a Service Fabric application using Java
services: service-fabric
documentationcenter: java
author: seanmck
manager: timlt
editor: ''
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/05/2017
ms.author: seanmck
ms.openlocfilehash: 8f3abf3e228a33892bdcd3bb16c7515fa5a82925
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556456"
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="2ea0d-103">Create your first Azure Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="2ea0d-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="2ea0d-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="2ea0d-108">In this tutorial, we create an application for Linux and build a service using Java.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-108">In this tutorial, we create an application for Linux and build a service using Java.</span></span>  

> [!NOTE]
> Java as a first class built-in programming language is supported for the Linux preview only (Windows support is planned). However, any applications including Java applications can be run as guest executables or inside containers on Windows or Linux. For more information, see [Deploy an existing executable to Azure Service Fabric](service-fabric-deploy-existing-app.md) and [Deploy containers to Service Fabric](service-fabric-deploy-container.md).
>

## <a name="video-tutorial"></a><span data-ttu-id="2ea0d-112">Video tutorial</span><span class="sxs-lookup"><span data-stu-id="2ea0d-112">Video tutorial</span></span>

<span data-ttu-id="2ea0d-113">The following Microsoft Virtual Academy video walks you through the process of creating a Java app on Linux:</span><span class="sxs-lookup"><span data-stu-id="2ea0d-113">The following Microsoft Virtual Academy video walks you through the process of creating a Java app on Linux:</span></span>  
<center><a target="\_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965">  
<img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-java/LinuxVid.png" WIDTH="360" HEIGHT="244">  
</a></center>


## <a name="prerequisites"></a><span data-ttu-id="2ea0d-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2ea0d-114">Prerequisites</span></span>
<span data-ttu-id="2ea0d-115">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0d-115">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="2ea0d-116">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="2ea0d-116">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="2ea0d-117">Create the application</span><span class="sxs-lookup"><span data-stu-id="2ea0d-117">Create the application</span></span>
<span data-ttu-id="2ea0d-118">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-118">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="2ea0d-119">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your first service and to add more later.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-119">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="2ea0d-120">Let's use Yeoman to create an application with a single service.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-120">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="2ea0d-121">In a terminal, type ``yo azuresfjava``.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-121">In a terminal, type ``yo azuresfjava``.</span></span>
2. <span data-ttu-id="2ea0d-122">Name your application.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-122">Name your application.</span></span>
3. <span data-ttu-id="2ea0d-123">Choose the type of your first service and name it.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-123">Choose the type of your first service and name it.</span></span> <span data-ttu-id="2ea0d-124">For the purposes of this tutorial, we choose a Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-124">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Service Fabric Yeoman generator for Java][sf-yeoman]

> [!NOTE]
> For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).
>

## <a name="build-the-application"></a><span data-ttu-id="2ea0d-127">Build the application</span><span class="sxs-lookup"><span data-stu-id="2ea0d-127">Build the application</span></span>
<span data-ttu-id="2ea0d-128">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the app from the terminal.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-128">The Service Fabric Yeoman templates include a build script for [Gradle](https://gradle.org/), which you can use to build the app from the terminal.</span></span>

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="2ea0d-129">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="2ea0d-129">Deploy the application</span></span>
<span data-ttu-id="2ea0d-130">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-130">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="2ea0d-131">Connect to the local Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-131">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    azure servicefabric cluster connect
    ```

2. <span data-ttu-id="2ea0d-132">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-132">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

3. <span data-ttu-id="2ea0d-133">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="2ea0d-133">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>

4. <span data-ttu-id="2ea0d-134">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-134">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="2ea0d-135">Start the test client and perform a failover</span><span class="sxs-lookup"><span data-stu-id="2ea0d-135">Start the test client and perform a failover</span></span>
<span data-ttu-id="2ea0d-136">Actor projects do not do anything on their own.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-136">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="2ea0d-137">They require another service or client to send them messages.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-137">They require another service or client to send them messages.</span></span> <span data-ttu-id="2ea0d-138">The actor template includes a simple test script that you can use to interact with the actor service.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-138">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="2ea0d-139">Run the script using the watch utility to see the output of the actor service.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-139">Run the script using the watch utility to see the output of the actor service.</span></span>

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. <span data-ttu-id="2ea0d-140">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-140">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="2ea0d-141">In the screenshot below, it is node 3.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-141">In the screenshot below, it is node 3.</span></span>

    ![Finding the primary replica in Service Fabric Explorer][sfx-primary]

3. <span data-ttu-id="2ea0d-143">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-143">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="2ea0d-144">This action restarts one of the five nodes in your local cluster and force a failover to one of the secondary replicas running on another node.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-144">This action restarts one of the five nodes in your local cluster and force a failover to one of the secondary replicas running on another node.</span></span> <span data-ttu-id="2ea0d-145">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-145">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="create-and-deploy-an-application-with-the-eclipse-neon-plugin"></a><span data-ttu-id="2ea0d-146">Create and deploy an application with the Eclipse Neon plugin</span><span class="sxs-lookup"><span data-stu-id="2ea0d-146">Create and deploy an application with the Eclipse Neon plugin</span></span>

<span data-ttu-id="2ea0d-147">Service Fabric also gives you the provision to create, build and deploy Service Fabric Java application using Eclipse.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-147">Service Fabric also gives you the provision to create, build and deploy Service Fabric Java application using Eclipse.</span></span> <span data-ttu-id="2ea0d-148">When installing Eclipse, choose the **Eclipse IDE for Java developers**.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-148">When installing Eclipse, choose the **Eclipse IDE for Java developers**.</span></span> <span data-ttu-id="2ea0d-149">Also, Service Fabric currently supports the plugin for Eclipse **Neon**.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-149">Also, Service Fabric currently supports the plugin for Eclipse **Neon**.</span></span> <span data-ttu-id="2ea0d-150">Please refer to the detailed documentation - [Create and deploy your first Service Fabric Java application using Service Fabric Plugin for Eclipse on Linux](service-fabric-get-started-eclipse.md)</span><span class="sxs-lookup"><span data-stu-id="2ea0d-150">Please refer to the detailed documentation - [Create and deploy your first Service Fabric Java application using Service Fabric Plugin for Eclipse on Linux](service-fabric-get-started-eclipse.md)</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="2ea0d-151">Adding more services to an existing application</span><span class="sxs-lookup"><span data-stu-id="2ea0d-151">Adding more services to an existing application</span></span>

### <a name="using-command-line-utility"></a><span data-ttu-id="2ea0d-152">Using command line utility</span><span class="sxs-lookup"><span data-stu-id="2ea0d-152">Using command line utility</span></span>
<span data-ttu-id="2ea0d-153">To add another service to an application already created using `yo`, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="2ea0d-153">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="2ea0d-154">Change directory to the root of the existing application.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-154">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="2ea0d-155">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span><span class="sxs-lookup"><span data-stu-id="2ea0d-155">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="2ea0d-156">Run `yo azuresfjava:AddService`</span><span class="sxs-lookup"><span data-stu-id="2ea0d-156">Run `yo azuresfjava:AddService`</span></span>

### <a name="using-service-fabric-eclipse-plugin-for-java-on-linux"></a><span data-ttu-id="2ea0d-157">Using Service Fabric Eclipse plugin for Java on Linux</span><span class="sxs-lookup"><span data-stu-id="2ea0d-157">Using Service Fabric Eclipse plugin for Java on Linux</span></span>
<span data-ttu-id="2ea0d-158">To add service to an existing application created using Eclipse plugin for Service Fabric refer to documentation [here](service-fabric-get-started-eclipse.md#add-a-service-fabric-service-to-your-service-fabric-application).</span><span class="sxs-lookup"><span data-stu-id="2ea0d-158">To add service to an existing application created using Eclipse plugin for Service Fabric refer to documentation [here](service-fabric-get-started-eclipse.md#add-a-service-fabric-service-to-your-service-fabric-application).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2ea0d-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ea0d-159">Next steps</span></span>
* [<span data-ttu-id="2ea0d-160">Create and deploy your first Service Fabric Java application using Service Fabric Plugin for Eclipse on Linux</span><span class="sxs-lookup"><span data-stu-id="2ea0d-160">Create and deploy your first Service Fabric Java application using Service Fabric Plugin for Eclipse on Linux</span></span>](service-fabric-get-started-eclipse.md)
* [<span data-ttu-id="2ea0d-161">Learn more about Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="2ea0d-161">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="2ea0d-162">Interacting with Service Fabric clusters using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="2ea0d-162">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)
* [<span data-ttu-id="2ea0d-163">Troubleshooting deployment</span><span class="sxs-lookup"><span data-stu-id="2ea0d-163">Troubleshooting deployment</span></span>](service-fabric-azure-cli.md#troubleshooting)
* <span data-ttu-id="2ea0d-164">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="2ea0d-164">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<!-- Images -->
[sf-yeoman]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png




