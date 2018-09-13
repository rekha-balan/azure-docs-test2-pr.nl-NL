---
title: Manage your Azure Servic Fabric applications in Visual Studio | Microsoft Docs
description: Use Visual Studio to create, develop, package, deploy, and debug your Azure Service Fabric applications and services.
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: ''
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.custom: vs-azure
ms.workload: azure-vs
ms.date: 03/26/2018
ms.author: mikhegn
ms.openlocfilehash: 6b8c5bf156c9eb4a408f7589e9a6131918eb4d93
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818927"
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="1ac05-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="1ac05-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="1ac05-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1ac05-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="1ac05-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span><span class="sxs-lookup"><span data-stu-id="1ac05-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="1ac05-106">Deploy your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="1ac05-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="1ac05-107">By default, deploying an application combines the following steps into one simple operation:</span><span class="sxs-lookup"><span data-stu-id="1ac05-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="1ac05-108">Creating the application package</span><span class="sxs-lookup"><span data-stu-id="1ac05-108">Creating the application package</span></span>
2. <span data-ttu-id="1ac05-109">Uploading the application package to the image store</span><span class="sxs-lookup"><span data-stu-id="1ac05-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="1ac05-110">Registering the application type</span><span class="sxs-lookup"><span data-stu-id="1ac05-110">Registering the application type</span></span>
4. <span data-ttu-id="1ac05-111">Removing any running application instances</span><span class="sxs-lookup"><span data-stu-id="1ac05-111">Removing any running application instances</span></span>
5. <span data-ttu-id="1ac05-112">Creating an application instance</span><span class="sxs-lookup"><span data-stu-id="1ac05-112">Creating an application instance</span></span>

<span data-ttu-id="1ac05-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span><span class="sxs-lookup"><span data-stu-id="1ac05-113">In Visual Studio, pressing **F5** deploys your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="1ac05-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span><span class="sxs-lookup"><span data-stu-id="1ac05-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="1ac05-115">Application Debug Mode</span><span class="sxs-lookup"><span data-stu-id="1ac05-115">Application Debug Mode</span></span>
<span data-ttu-id="1ac05-116">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span><span class="sxs-lookup"><span data-stu-id="1ac05-116">Visual Studio provide a property called **Application Debug Mode**, which controls how you want Visual Studios to handle Application deployment as part of debugging.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="1ac05-117">To set the Application Debug Mode property</span><span class="sxs-lookup"><span data-stu-id="1ac05-117">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="1ac05-118">On the Service Fabric application project's (\*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span><span class="sxs-lookup"><span data-stu-id="1ac05-118">On the Service Fabric application project's (\*.sfproj) shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="1ac05-119">In the **Properties** window, set the **Application Debug Mode** property.</span><span class="sxs-lookup"><span data-stu-id="1ac05-119">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

![Set Application Debug Mode Property][debugmodeproperty]

#### <a name="application-debug-modes"></a><span data-ttu-id="1ac05-121">Application Debug Modes</span><span class="sxs-lookup"><span data-stu-id="1ac05-121">Application Debug Modes</span></span>

1. <span data-ttu-id="1ac05-122">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span><span class="sxs-lookup"><span data-stu-id="1ac05-122">**Refresh Application** This mode enables you to quickly change and debug your code and supports editing static web files while debugging.</span></span> <span data-ttu-id="1ac05-123">This mode only works if your local development cluster is in [1-Node mode].</span><span class="sxs-lookup"><span data-stu-id="1ac05-123">This mode only works if your local development cluster is in [1-Node mode].</span></span> <span data-ttu-id="1ac05-124">This is the default Application Debug Mode.(/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span><span class="sxs-lookup"><span data-stu-id="1ac05-124">This is the default Application Debug Mode.(/service-fabric-get-started-with-a-local-cluster.md#one-node-and-five-node-cluster-mode).</span></span>
2. <span data-ttu-id="1ac05-125">**Remove Application** causes the application to be removed when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="1ac05-125">**Remove Application** causes the application to be removed when the debug session ends.</span></span>
3. <span data-ttu-id="1ac05-126">**Auto Upgrade** The application continues to run when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="1ac05-126">**Auto Upgrade** The application continues to run when the debug session ends.</span></span> <span data-ttu-id="1ac05-127">The next debug session will treat the deployment as an upgrade.</span><span class="sxs-lookup"><span data-stu-id="1ac05-127">The next debug session will treat the deployment as an upgrade.</span></span> <span data-ttu-id="1ac05-128">The upgrade process preserves any data that you entered in a previous debug session.</span><span class="sxs-lookup"><span data-stu-id="1ac05-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
4. <span data-ttu-id="1ac05-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="1ac05-129">**Keep Application** The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="1ac05-130">At the beginning of the next debug session, the application will be removed.</span><span class="sxs-lookup"><span data-stu-id="1ac05-130">At the beginning of the next debug session, the application will be removed.</span></span>

<span data-ttu-id="1ac05-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="1ac05-131">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric.</span></span> <span data-ttu-id="1ac05-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="1ac05-132">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="1ac05-133">Add a service to your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="1ac05-133">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="1ac05-134">You can add new services to your application to extend its functionality.</span><span class="sxs-lookup"><span data-stu-id="1ac05-134">You can add new services to your application to extend its functionality.</span></span> <span data-ttu-id="1ac05-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span><span class="sxs-lookup"><span data-stu-id="1ac05-135">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Add a new Service Fabric service][newservice]

<span data-ttu-id="1ac05-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span><span class="sxs-lookup"><span data-stu-id="1ac05-137">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="1ac05-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span><span class="sxs-lookup"><span data-stu-id="1ac05-138">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Select a Service Fabric service project type to add to your application][addserviceproject]

<span data-ttu-id="1ac05-140">The new service is added to your solution and existing application package.</span><span class="sxs-lookup"><span data-stu-id="1ac05-140">The new service is added to your solution and existing application package.</span></span> <span data-ttu-id="1ac05-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span><span class="sxs-lookup"><span data-stu-id="1ac05-141">The service references and a default service instance will be added to the application manifest, causing the service to be created and started the next time you deploy the application.</span></span>

![The new service is added to your application manifest][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="1ac05-143">Package your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="1ac05-143">Package your Service Fabric application</span></span>
<span data-ttu-id="1ac05-144">To deploy the application and its services to a cluster, you need to create an application package.</span><span class="sxs-lookup"><span data-stu-id="1ac05-144">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="1ac05-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span><span class="sxs-lookup"><span data-stu-id="1ac05-145">The package organizes the application manifest, service manifests, and other necessary files in a specific layout.</span></span>  <span data-ttu-id="1ac05-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span><span class="sxs-lookup"><span data-stu-id="1ac05-146">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="1ac05-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span><span class="sxs-lookup"><span data-stu-id="1ac05-147">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="1ac05-148">Remove applications and application types using Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="1ac05-148">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="1ac05-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span><span class="sxs-lookup"><span data-stu-id="1ac05-149">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="1ac05-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span><span class="sxs-lookup"><span data-stu-id="1ac05-150">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Remove an application][removeapplication]

> [!TIP]
> <span data-ttu-id="1ac05-152">For a richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="1ac05-152">For a richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="1ac05-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="1ac05-153">Next steps</span></span>
* [<span data-ttu-id="1ac05-154">Service Fabric application model</span><span class="sxs-lookup"><span data-stu-id="1ac05-154">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="1ac05-155">Service Fabric application deployment</span><span class="sxs-lookup"><span data-stu-id="1ac05-155">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="1ac05-156">Managing application parameters for multiple environments</span><span class="sxs-lookup"><span data-stu-id="1ac05-156">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="1ac05-157">Debugging your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="1ac05-157">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="1ac05-158">Visualizing your cluster by using Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="1ac05-158">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:./media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: ./media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:./media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:./media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[debugmodeproperty]:./media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png
[removeapplication]:./media/service-fabric-manage-application-in-visual-studio/removeapplication.png