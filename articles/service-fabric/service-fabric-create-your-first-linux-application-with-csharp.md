---
title: Create your first Azure Service Fabric app on Linux using C#| Microsoft Docs
description: Learn how to create and deploy a Service Fabric application using C# and .NET Core 2.0.
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: ''
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: conceptual
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/11/2018
ms.author: subramar
ms.openlocfilehash: 5c1804f3b72f7a79b134419aefbfa46ab65206c3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44814748"
---
# <a name="create-your-first-azure-service-fabric-application"></a><span data-ttu-id="1edf8-103">Create your first Azure Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="1edf8-103">Create your first Azure Service Fabric application</span></span>
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux (Preview)](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux (Preview)](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

<span data-ttu-id="1edf8-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span><span class="sxs-lookup"><span data-stu-id="1edf8-107">Service Fabric provides SDKs for building services on Linux in both .NET Core and Java.</span></span> <span data-ttu-id="1edf8-108">In this tutorial, we look at how to create an application for Linux and build a service using C# on .NET Core 2.0.</span><span class="sxs-lookup"><span data-stu-id="1edf8-108">In this tutorial, we look at how to create an application for Linux and build a service using C# on .NET Core 2.0.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1edf8-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1edf8-109">Prerequisites</span></span>
<span data-ttu-id="1edf8-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1edf8-110">Before you get started, make sure that you have [set up your Linux development environment](service-fabric-get-started-linux.md).</span></span> <span data-ttu-id="1edf8-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span><span class="sxs-lookup"><span data-stu-id="1edf8-111">If you are using Mac OS X, you can [set up a Linux one-box environment in a virtual machine using Vagrant](service-fabric-get-started-mac.md).</span></span>

<span data-ttu-id="1edf8-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span><span class="sxs-lookup"><span data-stu-id="1edf8-112">You will also want to install the [Service Fabric CLI](service-fabric-cli.md)</span></span>

### <a name="install-and-set-up-the-generators-for-c"></a><span data-ttu-id="1edf8-113">Install and set up the generators for C#</span><span class="sxs-lookup"><span data-stu-id="1edf8-113">Install and set up the generators for C#</span></span>
<span data-ttu-id="1edf8-114">Service Fabric provides scaffolding tools which help you create Service Fabric applications from a terminal using Yeoman template generators.</span><span class="sxs-lookup"><span data-stu-id="1edf8-114">Service Fabric provides scaffolding tools which help you create Service Fabric applications from a terminal using Yeoman template generators.</span></span> <span data-ttu-id="1edf8-115">Follow these steps to set up the Service Fabric Yeoman template generators for C#:</span><span class="sxs-lookup"><span data-stu-id="1edf8-115">Follow these steps to set up the Service Fabric Yeoman template generators for C#:</span></span>

1. <span data-ttu-id="1edf8-116">Install nodejs and NPM on your machine</span><span class="sxs-lookup"><span data-stu-id="1edf8-116">Install nodejs and NPM on your machine</span></span>

   ```bash
   curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.0/install.sh | bash 
   nvm install node 
   ```
2. <span data-ttu-id="1edf8-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span><span class="sxs-lookup"><span data-stu-id="1edf8-117">Install [Yeoman](http://yeoman.io/) template generator on your machine from NPM</span></span>

  ```bash
  npm install -g yo
  ```
3. <span data-ttu-id="1edf8-118">Install the Service Fabric Yeoman C# application generator from NPM</span><span class="sxs-lookup"><span data-stu-id="1edf8-118">Install the Service Fabric Yeoman C# application generator from NPM</span></span>

  ```bash
  npm install -g generator-azuresfcsharp
  ```

## <a name="create-the-application"></a><span data-ttu-id="1edf8-119">Create the application</span><span class="sxs-lookup"><span data-stu-id="1edf8-119">Create the application</span></span>
<span data-ttu-id="1edf8-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span><span class="sxs-lookup"><span data-stu-id="1edf8-120">A Service Fabric application can contain one or more services, each with a specific role in delivering the application's functionality.</span></span> <span data-ttu-id="1edf8-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for C#, which you installed in last step, makes it easy to create your first service and to add more later.</span><span class="sxs-lookup"><span data-stu-id="1edf8-121">The Service Fabric [Yeoman](http://yeoman.io/) generator for C#, which you installed in last step, makes it easy to create your first service and to add more later.</span></span> <span data-ttu-id="1edf8-122">Let's use Yeoman to create an application with a single service.</span><span class="sxs-lookup"><span data-stu-id="1edf8-122">Let's use Yeoman to create an application with a single service.</span></span>

1. <span data-ttu-id="1edf8-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span><span class="sxs-lookup"><span data-stu-id="1edf8-123">In a terminal, type the following command to start building the scaffolding: `yo azuresfcsharp`</span></span>
2. <span data-ttu-id="1edf8-124">Name your application.</span><span class="sxs-lookup"><span data-stu-id="1edf8-124">Name your application.</span></span>
3. <span data-ttu-id="1edf8-125">Choose the type of your first service and name it.</span><span class="sxs-lookup"><span data-stu-id="1edf8-125">Choose the type of your first service and name it.</span></span> <span data-ttu-id="1edf8-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span><span class="sxs-lookup"><span data-stu-id="1edf8-126">For the purposes of this tutorial, we choose a Reliable Actor Service.</span></span>

   ![Service Fabric Yeoman generator for C#][sf-yeoman]

> [!NOTE]
> For more information about the options, see [Service Fabric programming model overview](service-fabric-choose-framework.md).
>
>

## <a name="build-the-application"></a><span data-ttu-id="1edf8-129">Build the application</span><span class="sxs-lookup"><span data-stu-id="1edf8-129">Build the application</span></span>
<span data-ttu-id="1edf8-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span><span class="sxs-lookup"><span data-stu-id="1edf8-130">The Service Fabric Yeoman templates include a build script that you can use to build the app from the terminal (after navigating to the application folder).</span></span>

  ```sh
 cd myapp
 ./build.sh
  ```

## <a name="deploy-the-application"></a><span data-ttu-id="1edf8-131">Deploy the application</span><span class="sxs-lookup"><span data-stu-id="1edf8-131">Deploy the application</span></span>

<span data-ttu-id="1edf8-132">Once the application is built, you can deploy it to the local cluster.</span><span class="sxs-lookup"><span data-stu-id="1edf8-132">Once the application is built, you can deploy it to the local cluster.</span></span>

1. <span data-ttu-id="1edf8-133">Connect to the local Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="1edf8-133">Connect to the local Service Fabric cluster.</span></span>

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. <span data-ttu-id="1edf8-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span><span class="sxs-lookup"><span data-stu-id="1edf8-134">Run the install script provided in the template to copy the application package to the cluster's image store, register the application type, and create an instance of the application.</span></span>

    ```bash
    ./install.sh
    ```

<span data-ttu-id="1edf8-135">Deploying the built application is the same as any other Service Fabric application.</span><span class="sxs-lookup"><span data-stu-id="1edf8-135">Deploying the built application is the same as any other Service Fabric application.</span></span> <span data-ttu-id="1edf8-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span><span class="sxs-lookup"><span data-stu-id="1edf8-136">See the documentation on [managing a Service Fabric application with the Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) for detailed instructions.</span></span>

<span data-ttu-id="1edf8-137">Parameters to these commands can be found in the generated manifests inside the application package.</span><span class="sxs-lookup"><span data-stu-id="1edf8-137">Parameters to these commands can be found in the generated manifests inside the application package.</span></span>

<span data-ttu-id="1edf8-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span><span class="sxs-lookup"><span data-stu-id="1edf8-138">Once the application has been deployed, open a browser and navigate to [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) at [http://localhost:19080/Explorer](http://localhost:19080/Explorer).</span></span> <span data-ttu-id="1edf8-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span><span class="sxs-lookup"><span data-stu-id="1edf8-139">Then, expand the **Applications** node and note that there is now an entry for your application type and another for the first instance of that type.</span></span>

> [!IMPORTANT]
> To deploy the application to a secure Linux cluster in Azure, you need to configure a certificate to validate your application with the Service Fabric runtime. Doing so enables your Reliable Services services to communicate with the underlying Service Fabric runtime APIs. To learn more, see [Configure a Reliable Services app to run on Linux clusters](./service-fabric-configure-certificates-linux.md#configure-a-reliable-services-app-to-run-on-linux-clusters).  
>

## <a name="start-the-test-client-and-perform-a-failover"></a><span data-ttu-id="1edf8-143">Start the test client and perform a failover</span><span class="sxs-lookup"><span data-stu-id="1edf8-143">Start the test client and perform a failover</span></span>
<span data-ttu-id="1edf8-144">Actor projects do not do anything on their own.</span><span class="sxs-lookup"><span data-stu-id="1edf8-144">Actor projects do not do anything on their own.</span></span> <span data-ttu-id="1edf8-145">They require another service or client to send them messages.</span><span class="sxs-lookup"><span data-stu-id="1edf8-145">They require another service or client to send them messages.</span></span> <span data-ttu-id="1edf8-146">The actor template includes a simple test script that you can use to interact with the actor service.</span><span class="sxs-lookup"><span data-stu-id="1edf8-146">The actor template includes a simple test script that you can use to interact with the actor service.</span></span>

1. <span data-ttu-id="1edf8-147">Run the script using the watch utility to see the output of the actor service.</span><span class="sxs-lookup"><span data-stu-id="1edf8-147">Run the script using the watch utility to see the output of the actor service.</span></span>

   <span data-ttu-id="1edf8-148">In case of MAC OS X, you need to copy the myactorsvcTestClient folder into the some location inside the container by running the following additional commands.</span><span class="sxs-lookup"><span data-stu-id="1edf8-148">In case of MAC OS X, you need to copy the myactorsvcTestClient folder into the some location inside the container by running the following additional commands.</span></span>
    
    ```bash
    docker cp  [first-four-digits-of-container-ID]:/home
    docker exec -it [first-four-digits-of-container-ID] /bin/bash
    cd /home
    ```
    
    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. <span data-ttu-id="1edf8-149">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span><span class="sxs-lookup"><span data-stu-id="1edf8-149">In Service Fabric Explorer, locate node hosting the primary replica for the actor service.</span></span> <span data-ttu-id="1edf8-150">In the screenshot below, it is node 3.</span><span class="sxs-lookup"><span data-stu-id="1edf8-150">In the screenshot below, it is node 3.</span></span>

    ![Finding the primary replica in Service Fabric Explorer][sfx-primary]
3. <span data-ttu-id="1edf8-152">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span><span class="sxs-lookup"><span data-stu-id="1edf8-152">Click the node you found in the previous step, then select **Deactivate (restart)** from the Actions menu.</span></span> <span data-ttu-id="1edf8-153">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span><span class="sxs-lookup"><span data-stu-id="1edf8-153">This action restarts one node in your local cluster forcing a failover to a secondary replica running on another node.</span></span> <span data-ttu-id="1edf8-154">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span><span class="sxs-lookup"><span data-stu-id="1edf8-154">As you perform this action, pay attention to the output from the test client and note that the counter continues to increment despite the failover.</span></span>

## <a name="adding-more-services-to-an-existing-application"></a><span data-ttu-id="1edf8-155">Adding more services to an existing application</span><span class="sxs-lookup"><span data-stu-id="1edf8-155">Adding more services to an existing application</span></span>

<span data-ttu-id="1edf8-156">To add another service to an application already created using `yo`, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="1edf8-156">To add another service to an application already created using `yo`, perform the following steps:</span></span>
1. <span data-ttu-id="1edf8-157">Change directory to the root of the existing application.</span><span class="sxs-lookup"><span data-stu-id="1edf8-157">Change directory to the root of the existing application.</span></span>  <span data-ttu-id="1edf8-158">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span><span class="sxs-lookup"><span data-stu-id="1edf8-158">For example, `cd ~/YeomanSamples/MyApplication`, if `MyApplication` is the application created by Yeoman.</span></span>
2. <span data-ttu-id="1edf8-159">Run `yo azuresfcsharp:AddService`</span><span class="sxs-lookup"><span data-stu-id="1edf8-159">Run `yo azuresfcsharp:AddService`</span></span>

## <a name="next-steps"></a><span data-ttu-id="1edf8-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="1edf8-160">Next steps</span></span>

* [<span data-ttu-id="1edf8-161">Interacting with Service Fabric clusters using the Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="1edf8-161">Interacting with Service Fabric clusters using the Service Fabric CLI</span></span>](service-fabric-cli.md)
* <span data-ttu-id="1edf8-162">Learn about [Service Fabric support options](service-fabric-support.md)</span><span class="sxs-lookup"><span data-stu-id="1edf8-162">Learn about [Service Fabric support options](service-fabric-support.md)</span></span>
* [<span data-ttu-id="1edf8-163">Getting started with Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="1edf8-163">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
