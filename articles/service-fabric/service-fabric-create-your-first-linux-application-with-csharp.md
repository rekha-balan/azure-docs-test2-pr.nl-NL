---
title: Create your first Azure microservices app on Linux using C#| Microsoft Docs
description: Create and deploy a Service Fabric application using C#
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/02/2017
ms.author: subramar
ms.openlocfilehash: 2c60b874e2e7bc476ec7f16b05e354fac34c739b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555530"
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="99be1-103">Create your first Azure Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="99be1-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
> 
> 

<span data-ttu-id="99be1-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span><span class="sxs-lookup"><span data-stu-id="99be1-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="99be1-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span><span class="sxs-lookup"><span data-stu-id="99be1-108">In this tutorial, we look at how to create an application for Linux and build a service using C# (.NET Core).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99be1-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="99be1-109">Prerequisites</span></span>
<span data-ttu-id="99be1-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="99be1-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="99be1-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="99be1-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

## <a name="create-the-application"></a><span data-ttu-id="99be1-112">Create the application</span><span class="sxs-lookup"><span data-stu-id="99be1-112">Create the application</span></span>
<span data-ttu-id="99be1-113">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="99be1-113">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="99be1-114">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your first service and to add more later.</span><span class="sxs-lookup"><span data-stu-id="99be1-114">The Service Fabric SDK for Linux includes a [Yeoman](http://yeoman.io/) generator that makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="99be1-115">Let's use Yeoman to create an application with a single service.</span><span class="sxs-lookup"><span data-stu-id="99be1-115">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="99be1-116">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="99be1-116">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="99be1-117">Name your application.</span><span class="sxs-lookup"><span data-stu-id="99be1-117">Name your application.</span></span>
3. <span data-ttu-id="99be1-118">Choose the type of your first service and name it.</span><span class="sxs-lookup"><span data-stu-id="99be1-118">Choose the type of your first service and name it.</span></span> <span data-ttu-id="99be1-119">For the purposes of this tutorial, we choose a Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="99be1-119">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>
   
   ![Service Fabric Yeoman generator for C#][sf-yeoman]

> [!NOTE]
> For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).
> 
> 

## <a name="build-the-application"></a><span data-ttu-id="99be1-122">Build the application</span><span class="sxs-lookup"><span data-stu-id="99be1-122">Build the application</span></span>
<span data-ttu-id="99be1-123">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span><span class="sxs-lookup"><span data-stu-id="99be1-123">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp 
 ./build.sh 
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="99be1-124">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="99be1-124">Deploy the application</span></span>
<span data-ttu-id="99be1-125">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="99be1-125">Once the application is built, you can deploy it to the local cluster using the Azure CLI.</span></span>

1. <span data-ttu-id="99be1-126">Connect to the local Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="99be1-126">Connect to the local Service Fabric cluster.</span></span>
   
    ```sh
    azure servicefabric cluster connect
    ```
2. <span data-ttu-id="99be1-127">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="99be1-127">Use the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>
   
    ```bash
    ./install.sh
    ```
3. <span data-ttu-id="99be1-128">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span><span class="sxs-lookup"><span data-stu-id="99be1-128">Open a browser and navigate to Service Fabric Explorer at http://localhost:19080/Explorer (replace localhost with the private IP of the VM if using Vagrant on Mac OS X).</span></span>
4. <span data-ttu-id="99be1-129">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="99be1-129">Expand the Applications node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="99be1-130">Start the test client and perform a failover</span><span class="sxs-lookup"><span data-stu-id="99be1-130">Start the test client and perform a failover</span></span>
<span data-ttu-id="99be1-131">Actor projects do not do anything on their own.</span><span class="sxs-lookup"><span data-stu-id="99be1-131">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="99be1-132">They require another service or client to send them messages.</span><span class="sxs-lookup"><span data-stu-id="99be1-132">They require another service or client to send them messages.</span></span> <span data-ttu-id="99be1-133">The actor template includes a simple test script that you can use to interact with the actor service.</span><span class="sxs-lookup"><span data-stu-id="99be1-133">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="99be1-134">Run the script using the watch utility to see the output of the actor service.</span><span class="sxs-lookup"><span data-stu-id="99be1-134">Run the script using the watch utility to see the output of the actor service.</span></span>
   
    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="99be1-135">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span><span class="sxs-lookup"><span data-stu-id="99be1-135">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="99be1-136">In the screenshot below, it is node 3.</span><span class="sxs-lookup"><span data-stu-id="99be1-136">In the screenshot below, it is node 3.</span></span>
   
    ![Finding the primary replica in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="99be1-138">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span><span class="sxs-lookup"><span data-stu-id="99be1-138">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="99be1-139">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span><span class="sxs-lookup"><span data-stu-id="99be1-139">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="99be1-140">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span><span class="sxs-lookup"><span data-stu-id="99be1-140">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="99be1-141">Adding more services to an existing application</span><span class="sxs-lookup"><span data-stu-id="99be1-141">Adding more services to an existing application</span></span>

<span data-ttu-id="99be1-142">To add another service to an application already created using `yo`, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="99be1-142">To add another service to an application already created using `yo`, perform the following steps:</span></span> 
1. <span data-ttu-id="99be1-143">Change directory to the root of the existing application.</span><span class="sxs-lookup"><span data-stu-id="99be1-143">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="99be1-144">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span><span class="sxs-lookup"><span data-stu-id="99be1-144">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="99be1-145">Run `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="99be1-145">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="next-steps"></a><span data-ttu-id="99be1-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="99be1-146">Next steps</span></span>
* [<span data-ttu-id="99be1-147">Learn more about Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="99be1-147">Learn more about Reliable Actors</span></span>](service-fabric-reliable-actors-introduction.md)
* [<span data-ttu-id="99be1-148">Interacting with Service Fabric clusters using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="99be1-148">Interacting with Service Fabric clusters using the Azure CLI</span></span>](service-fabric-azure-cli.md)
* <span data-ttu-id="99be1-149">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="99be1-149">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>

<!-- Images -->
[sf-yeoman]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png


