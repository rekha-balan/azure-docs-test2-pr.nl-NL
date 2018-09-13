---
title: Manage your applications in Visual Studio | Microsoft Docs
description: Use Visual Studio to create, develop, package, deploy, and debug your Service Fabric applications and services.
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: c317cb7e-7eae-466e-ba41-6aa2518be5cf
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/05/2017
ms.author: seanmck;mikhegn
ms.openlocfilehash: dba49f5ac0cfa3877c235a8451fbe6fbb37d98ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550731"
---
# <a name="use-visual-studio-to-simplify-writing-and-managing-your-service-fabric-applications"></a><span data-ttu-id="3ecd7-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span><span class="sxs-lookup"><span data-stu-id="3ecd7-103">Use Visual Studio to simplify writing and managing your Service Fabric applications</span></span>
<span data-ttu-id="3ecd7-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-104">You can manage your Azure Service Fabric applications and services through Visual Studio.</span></span> <span data-ttu-id="3ecd7-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-105">Once you've [set up your development environment](service-fabric-get-started.md), you can use Visual Studio to create Service Fabric applications, add services, or package, register, and deploy applications in your local development cluster.</span></span>

## <a name="deploy-your-service-fabric-application"></a><span data-ttu-id="3ecd7-106">Deploy your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="3ecd7-106">Deploy your Service Fabric application</span></span>
<span data-ttu-id="3ecd7-107">By default, deploying an application combines the following steps into one simple operation:</span><span class="sxs-lookup"><span data-stu-id="3ecd7-107">By default, deploying an application combines the following steps into one simple operation:</span></span>

1. <span data-ttu-id="3ecd7-108">Creating the application package</span><span class="sxs-lookup"><span data-stu-id="3ecd7-108">Creating the application package</span></span>
2. <span data-ttu-id="3ecd7-109">Uploading the application package to the image store</span><span class="sxs-lookup"><span data-stu-id="3ecd7-109">Uploading the application package to the image store</span></span>
3. <span data-ttu-id="3ecd7-110">Registering the application type</span><span class="sxs-lookup"><span data-stu-id="3ecd7-110">Registering the application type</span></span>
4. <span data-ttu-id="3ecd7-111">Removing any running application instances</span><span class="sxs-lookup"><span data-stu-id="3ecd7-111">Removing any running application instances</span></span>
5. <span data-ttu-id="3ecd7-112">Creating a new application instance</span><span class="sxs-lookup"><span data-stu-id="3ecd7-112">Creating a new application instance</span></span>

<span data-ttu-id="3ecd7-113">In Visual Studio, pressing **F5** will also deploy your application and attach the debugger to all application instances.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-113">In Visual Studio, pressing **F5** will also deploy your application and attach the debugger to all application instances.</span></span> <span data-ttu-id="3ecd7-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-114">You can use **Ctrl+F5** to deploy an application without debugging, or you can publish to a local or remote cluster by using the publish profile.</span></span> <span data-ttu-id="3ecd7-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd7-115">For more information, see [Publish an application to a remote cluster by using Visual Studio](service-fabric-publish-app-remote-cluster.md).</span></span>

### <a name="application-debug-mode"></a><span data-ttu-id="3ecd7-116">Application Debug Mode</span><span class="sxs-lookup"><span data-stu-id="3ecd7-116">Application Debug Mode</span></span>
<span data-ttu-id="3ecd7-117">By default, Visual Studio removes existing instances of your application type when you stop debugging or (if you deployed the app without attaching the debugger), when you redeploy the application.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-117">By default, Visual Studio removes existing instances of your application type when you stop debugging or (if you deployed the app without attaching the debugger), when you redeploy the application.</span></span> <span data-ttu-id="3ecd7-118">In that case, all the application's data is removed.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-118">In that case, all the application's data is removed.</span></span> <span data-ttu-id="3ecd7-119">While debugging locally, you may want to keep data that you've already created when testing a new version of the application, you want to keep the application running or you want subsequent debug sessions to upgrade the application.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-119">While debugging locally, you may want to keep data that you've already created when testing a new version of the application, you want to keep the application running or you want subsequent debug sessions to upgrade the application.</span></span> <span data-ttu-id="3ecd7-120">Visual Studio Service Fabric Tools provide a property called **Application Debug Mode**, which controls whether the **F5** should uninstall the application, keep the application running after a debug session ends or enable the application to be upgraded on subsequent debugging sessions, rather than removed and redeployed.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-120">Visual Studio Service Fabric Tools provide a property called **Application Debug Mode**, which controls whether the **F5** should uninstall the application, keep the application running after a debug session ends or enable the application to be upgraded on subsequent debugging sessions, rather than removed and redeployed.</span></span>

#### <a name="to-set-the-application-debug-mode-property"></a><span data-ttu-id="3ecd7-121">To set the Application Debug Mode property</span><span class="sxs-lookup"><span data-stu-id="3ecd7-121">To set the Application Debug Mode property</span></span>
1. <span data-ttu-id="3ecd7-122">On the application project's shortcut menu, choose **Properties** (or press the **F4** key).</span><span class="sxs-lookup"><span data-stu-id="3ecd7-122">On the application project's shortcut menu, choose **Properties** (or press the **F4** key).</span></span>
2. <span data-ttu-id="3ecd7-123">In the **Properties** window, set the **Application Debug Mode** property.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-123">In the **Properties** window, set the **Application Debug Mode** property.</span></span>

    ![Set Application Debug Mode Property][debugmodeproperty]

<span data-ttu-id="3ecd7-125">These are the **Application Debug Mode** options available.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-125">These are the **Application Debug Mode** options available.</span></span>

1. <span data-ttu-id="3ecd7-126">**Auto Upgrade**: The application continues to run when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-126">**Auto Upgrade**: The application continues to run when the debug session ends.</span></span> <span data-ttu-id="3ecd7-127">The next **F5** will treat the deployment as an upgrade by using unmonitored auto mode to quickly upgrade the application to a newer version with a date string appended.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-127">The next **F5** will treat the deployment as an upgrade by using unmonitored auto mode to quickly upgrade the application to a newer version with a date string appended.</span></span> <span data-ttu-id="3ecd7-128">The upgrade process preserves any data that you entered in a previous debug session.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-128">The upgrade process preserves any data that you entered in a previous debug session.</span></span>
2. <span data-ttu-id="3ecd7-129">**Keep Application**: The application keeps running in the cluster when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-129">**Keep Application**: The application keeps running in the cluster when the debug session ends.</span></span> <span data-ttu-id="3ecd7-130">On the next **F5** the application will be removed and the newly built application will be deployed to the cluster.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-130">On the next **F5** the application will be removed and the newly built application will be deployed to the cluster.</span></span>
3. <span data-ttu-id="3ecd7-131">**Remove Application** causes the application to be removed when the debug session ends.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-131">**Remove Application** causes the application to be removed when the debug session ends.</span></span>

<span data-ttu-id="3ecd7-132">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric, but it is tuned to optimize for performance rather than safety.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-132">For **Auto Upgrade** data is preserved by applying the application upgrade capabilities of Service Fabric, but it is tuned to optimize for performance rather than safety.</span></span> <span data-ttu-id="3ecd7-133">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd7-133">For more information about upgrading applications and how you might perform an upgrade in a real environment, see [Service Fabric application upgrade](service-fabric-application-upgrade.md).</span></span>

![Example of new application version with date appended][preservedata]

> [!NOTE]
> <span data-ttu-id="3ecd7-135">This property doesn't exist prior to version 1.1 of the Service Fabric Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-135">This property doesn't exist prior to version 1.1 of the Service Fabric Tools for Visual Studio.</span></span> <span data-ttu-id="3ecd7-136">Prior to 1.1, please use the **Preserve Data On Start** property to achieve the same behavior.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-136">Prior to 1.1, please use the **Preserve Data On Start** property to achieve the same behavior.</span></span> <span data-ttu-id="3ecd7-137">The "Keep Application" option was introduced in version 1.2 of the Service Fabric Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-137">The "Keep Application" option was introduced in version 1.2 of the Service Fabric Tools for Visual Studio.</span></span>
>
>

## <a name="add-a-service-to-your-service-fabric-application"></a><span data-ttu-id="3ecd7-138">Add a service to your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="3ecd7-138">Add a service to your Service Fabric application</span></span>
<span data-ttu-id="3ecd7-139">You can add new services to your application to extend its functionality.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-139">You can add new services to your application to extend its functionality.</span></span>  <span data-ttu-id="3ecd7-140">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-140">To ensure that the service is included in your application package, add the service through the **New Fabric Service...** menu item.</span></span>

![Add a new fabric service to your application][newservice]

<span data-ttu-id="3ecd7-142">Select a Service Fabric project type to add to your application, and specify a name for the service.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-142">Select a Service Fabric project type to add to your application, and specify a name for the service.</span></span>  <span data-ttu-id="3ecd7-143">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-143">See [Choosing a framework for your service](service-fabric-choose-framework.md) to help you decide which service type to use.</span></span>

![Select a Fabric Service project type to add to your application][addserviceproject]

<span data-ttu-id="3ecd7-145">The new service will be added to your solution and existing application package.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-145">The new service will be added to your solution and existing application package.</span></span> <span data-ttu-id="3ecd7-146">The service references and a default service instance will be added to the application manifest.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-146">The service references and a default service instance will be added to the application manifest.</span></span> <span data-ttu-id="3ecd7-147">The service will be created and started the next time you deploy the application.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-147">The service will be created and started the next time you deploy the application.</span></span>

![The new service will be added to your application manifest][newserviceapplicationmanifest]

## <a name="package-your-service-fabric-application"></a><span data-ttu-id="3ecd7-149">Package your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="3ecd7-149">Package your Service Fabric application</span></span>
<span data-ttu-id="3ecd7-150">To deploy the application and its services to a cluster, you need to create an application package.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-150">To deploy the application and its services to a cluster, you need to create an application package.</span></span>  <span data-ttu-id="3ecd7-151">The package organizes the application manifest, service manifest(s), and other necessary files in a specific layout.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-151">The package organizes the application manifest, service manifest(s), and other necessary files in a specific layout.</span></span>  <span data-ttu-id="3ecd7-152">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-152">Visual Studio sets up and manages the package in the application project's folder, in the 'pkg' directory.</span></span>  <span data-ttu-id="3ecd7-153">Clicking **Package** from the **Application** context menu creates or updates the application package.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-153">Clicking **Package** from the **Application** context menu creates or updates the application package.</span></span>  <span data-ttu-id="3ecd7-154">You may want to do this if you deploy the application by using custom PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-154">You may want to do this if you deploy the application by using custom PowerShell scripts.</span></span>

## <a name="remove-applications-and-application-types-using-cloud-explorer"></a><span data-ttu-id="3ecd7-155">Remove applications and application types using Cloud Explorer</span><span class="sxs-lookup"><span data-stu-id="3ecd7-155">Remove applications and application types using Cloud Explorer</span></span>
<span data-ttu-id="3ecd7-156">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-156">You can perform basic cluster management operations from within Visual Studio using Cloud Explorer, which you can launch from the **View** menu.</span></span> <span data-ttu-id="3ecd7-157">For instance, you can delete applications and unprovision application types on local or remote clusters.</span><span class="sxs-lookup"><span data-stu-id="3ecd7-157">For instance, you can delete applications and unprovision application types on local or remote clusters.</span></span>

![Remove an application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/removeapplication.png)

> [!TIP]
> <span data-ttu-id="3ecd7-159">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="3ecd7-159">For richer cluster management functionality, see [Visualizing your cluster with Service Fabric Explorer](service-fabric-visualizing-your-cluster.md).</span></span>
>
>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="3ecd7-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="3ecd7-160">Next steps</span></span>
* [<span data-ttu-id="3ecd7-161">Service Fabric application model</span><span class="sxs-lookup"><span data-stu-id="3ecd7-161">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="3ecd7-162">Service Fabric application deployment</span><span class="sxs-lookup"><span data-stu-id="3ecd7-162">Service Fabric application deployment</span></span>](service-fabric-deploy-remove-applications.md)
* [<span data-ttu-id="3ecd7-163">Managing application parameters for multiple environments</span><span class="sxs-lookup"><span data-stu-id="3ecd7-163">Managing application parameters for multiple environments</span></span>](service-fabric-manage-multiple-environment-app-configuration.md)
* [<span data-ttu-id="3ecd7-164">Debugging your Service Fabric application</span><span class="sxs-lookup"><span data-stu-id="3ecd7-164">Debugging your Service Fabric application</span></span>](service-fabric-debugging-your-application.md)
* [<span data-ttu-id="3ecd7-165">Visualizing your cluster by using Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="3ecd7-165">Visualizing your cluster by using Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

<!--Image references-->
[addserviceproject]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/addserviceproject.png
[manageservicefabric]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/manageservicefabric.png
[newservice]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/newservice.png
[newserviceapplicationmanifest]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/newserviceapplicationmanifest.png
[preservedata]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/preservedata.png
[debugmodeproperty]:https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-manage-application-in-visual-studio/debugmodeproperty.png







