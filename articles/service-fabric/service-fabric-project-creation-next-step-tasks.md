---
title: Service Fabric project creation next steps | Microsoft Docs
description: This article contains links to a set of core development tasks for Service Fabric
services: service-fabric
documentationcenter: .net
author: seanmck
manager: timlt
editor: ''
ms.assetid: 299d1f97-1ca9-440d-9f81-d1d0dd2bf4df
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/28/2017
ms.author: seanmck
ms.openlocfilehash: 8208a1a41388a8cc36f3702bd0cad2bb82e16403
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563113"
---
# <a name="your-service-fabric-application-and-next-steps"></a><span data-ttu-id="071ec-103">Your Service Fabric application and next steps</span><span class="sxs-lookup"><span data-stu-id="071ec-103">Your Service Fabric application and next steps</span></span>
<span data-ttu-id="071ec-104">Your Azure Service Fabric application has been created.</span><span class="sxs-lookup"><span data-stu-id="071ec-104">Your Azure Service Fabric application has been created.</span></span> <span data-ttu-id="071ec-105">This article describes the makeup of your project and some potential next steps.</span><span class="sxs-lookup"><span data-stu-id="071ec-105">This article describes the makeup of your project and some potential next steps.</span></span>

## <a name="your-application"></a><span data-ttu-id="071ec-106">Your application</span><span class="sxs-lookup"><span data-stu-id="071ec-106">Your application</span></span>
<span data-ttu-id="071ec-107">Every new application includes an application project.</span><span class="sxs-lookup"><span data-stu-id="071ec-107">Every new application includes an application project.</span></span> <span data-ttu-id="071ec-108">There may be one or two additional projects, depending on the type of service chosen.</span><span class="sxs-lookup"><span data-stu-id="071ec-108">There may be one or two additional projects, depending on the type of service chosen.</span></span>

### <a name="the-application-project"></a><span data-ttu-id="071ec-109">The application project</span><span class="sxs-lookup"><span data-stu-id="071ec-109">The application project</span></span>
<span data-ttu-id="071ec-110">The application project consists of:</span><span class="sxs-lookup"><span data-stu-id="071ec-110">The application project consists of:</span></span>

* <span data-ttu-id="071ec-111">A set of references to the services that make up your application.</span><span class="sxs-lookup"><span data-stu-id="071ec-111">A set of references to the services that make up your application.</span></span>
* <span data-ttu-id="071ec-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span><span class="sxs-lookup"><span data-stu-id="071ec-112">Three publish profiles (1-Node Local, 5-Node Local, and Cloud) that you can use to maintain preferences for working with different environments--such as preferences related to a cluster endpoint and whether to perform upgrade deployments by default.</span></span>
* <span data-ttu-id="071ec-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span><span class="sxs-lookup"><span data-stu-id="071ec-113">Three application parameter files (same as above) that you can use to maintain environment-specific application configurations, such as the number of partitions to create for a service.</span></span>
* <span data-ttu-id="071ec-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span><span class="sxs-lookup"><span data-stu-id="071ec-114">A deployment script that you can use to deploy your application from the command line or as part of an automated continuous integration and deployment pipeline.</span></span>
* <span data-ttu-id="071ec-115">The application manifest, which describes the application.</span><span class="sxs-lookup"><span data-stu-id="071ec-115">The application manifest, which describes the application.</span></span> <span data-ttu-id="071ec-116">You can find the manifest under the ApplicationPackageRoot folder.</span><span class="sxs-lookup"><span data-stu-id="071ec-116">You can find the manifest under the ApplicationPackageRoot folder.</span></span>

### <a name="stateless-service"></a><span data-ttu-id="071ec-117">Stateless service</span><span class="sxs-lookup"><span data-stu-id="071ec-117">Stateless service</span></span>
<span data-ttu-id="071ec-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="071ec-118">When you add a new stateless service, Visual Studio adds a service project to your solution that includes a type descended from `StatelessService`.</span></span> <span data-ttu-id="071ec-119">The service increments a local variable in a counter.</span><span class="sxs-lookup"><span data-stu-id="071ec-119">The service increments a local variable in a counter.</span></span>

### <a name="stateful-service"></a><span data-ttu-id="071ec-120">Stateful service</span><span class="sxs-lookup"><span data-stu-id="071ec-120">Stateful service</span></span>
<span data-ttu-id="071ec-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span><span class="sxs-lookup"><span data-stu-id="071ec-121">When you add a new stateful service, Visual Studio adds a service project to your solution that includes a type descended from `StatefulService`.</span></span> <span data-ttu-id="071ec-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span><span class="sxs-lookup"><span data-stu-id="071ec-122">The service increments a counter in its `RunAsync` method and stores the result in a `ReliableDictionary`.</span></span>

### <a name="actor-service"></a><span data-ttu-id="071ec-123">Actor service</span><span class="sxs-lookup"><span data-stu-id="071ec-123">Actor service</span></span>
<span data-ttu-id="071ec-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span><span class="sxs-lookup"><span data-stu-id="071ec-124">When you add a new reliable actor, Visual Studio adds two projects to your solution: an actor project and an interface project.</span></span>

<span data-ttu-id="071ec-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span><span class="sxs-lookup"><span data-stu-id="071ec-125">The actor project provides methods for setting and getting the value of a counter that is reliably persisted within the actor's state.</span></span> <span data-ttu-id="071ec-126">The interface project provides an interface that other services can use to invoke the actor.</span><span class="sxs-lookup"><span data-stu-id="071ec-126">The interface project provides an interface that other services can use to invoke the actor.</span></span>

### <a name="stateless-web-api"></a><span data-ttu-id="071ec-127">Stateless Web API</span><span class="sxs-lookup"><span data-stu-id="071ec-127">Stateless Web API</span></span>
<span data-ttu-id="071ec-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span><span class="sxs-lookup"><span data-stu-id="071ec-128">The stateless Web API project provides a basic web service that you can use to open your application to external clients.</span></span> <span data-ttu-id="071ec-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span><span class="sxs-lookup"><span data-stu-id="071ec-129">For more information about how the project structured, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md).</span></span>


### <a name="aspnet-core"></a><span data-ttu-id="071ec-130">ASP.NET core</span><span class="sxs-lookup"><span data-stu-id="071ec-130">ASP.NET core</span></span>
<span data-ttu-id="071ec-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span><span class="sxs-lookup"><span data-stu-id="071ec-131">The Service Fabric SDK provides the same set of ASP.NET Core templates that are available for standalone ASP.NET Core projects: empty, [Web API][aspnet-webapi], and [Web Application][aspnet-webapp].</span></span>

### <a name="guest-executables-and-guest-containers"></a><span data-ttu-id="071ec-132">Guest executables and guest containers</span><span class="sxs-lookup"><span data-stu-id="071ec-132">Guest executables and guest containers</span></span>

<span data-ttu-id="071ec-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span><span class="sxs-lookup"><span data-stu-id="071ec-133">A Service Fabric 'guest' is a service that is not built with the platform's programming models.</span></span> <span data-ttu-id="071ec-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span><span class="sxs-lookup"><span data-stu-id="071ec-134">You can package the binaries for a guest either [directly in the application package](service-fabric-deploy-existing-app.md) or [through a container image](service-fabric-deploy-container.md).</span></span> <span data-ttu-id="071ec-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span><span class="sxs-lookup"><span data-stu-id="071ec-135">In both cases, Visual Studio creates the necessary artifacts in the **ApplicationPackageRoot** folder of the application project.</span></span> <span data-ttu-id="071ec-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span><span class="sxs-lookup"><span data-stu-id="071ec-136">Visual Studio will not create a new service project because the code already exists elsewhere.</span></span> <span data-ttu-id="071ec-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="071ec-137">If you would like to manage your guest projects alongside the Service Fabric application project, you can add them to the same Visual Studio solution.</span></span>

## <a name="next-steps"></a><span data-ttu-id="071ec-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="071ec-138">Next steps</span></span>
### <a name="create-an-azure-cluster"></a><span data-ttu-id="071ec-139">Create an Azure cluster</span><span class="sxs-lookup"><span data-stu-id="071ec-139">Create an Azure cluster</span></span>
<span data-ttu-id="071ec-140">The Service Fabric SDK provides a local cluster for development and testing.</span><span class="sxs-lookup"><span data-stu-id="071ec-140">The Service Fabric SDK provides a local cluster for development and testing.</span></span> <span data-ttu-id="071ec-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span><span class="sxs-lookup"><span data-stu-id="071ec-141">To create a cluster in Azure, see [Setting up a Service Fabric cluster from the Azure portal][create-cluster-in-portal].</span></span>

### <a name="publish-your-application-to-azure"></a><span data-ttu-id="071ec-142">Publish your application to Azure</span><span class="sxs-lookup"><span data-stu-id="071ec-142">Publish your application to Azure</span></span>
<span data-ttu-id="071ec-143">You can publish your application directly from Visual Studio to an Azure cluster.</span><span class="sxs-lookup"><span data-stu-id="071ec-143">You can publish your application directly from Visual Studio to an Azure cluster.</span></span> <span data-ttu-id="071ec-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span><span class="sxs-lookup"><span data-stu-id="071ec-144">To learn how, see [Publishing your application to Azure][publish-app-to-azure].</span></span>

### <a name="use-service-fabric-explorer-to-visualize-your-cluster"></a><span data-ttu-id="071ec-145">Use Service Fabric Explorer to visualize your cluster</span><span class="sxs-lookup"><span data-stu-id="071ec-145">Use Service Fabric Explorer to visualize your cluster</span></span>
<span data-ttu-id="071ec-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span><span class="sxs-lookup"><span data-stu-id="071ec-146">Service Fabric Explorer offers an easy way to visualize your cluster, including deployed applications and physical layout.</span></span> <span data-ttu-id="071ec-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span><span class="sxs-lookup"><span data-stu-id="071ec-147">To learn more, see [Visualizing your cluster by using Service Fabric Explorer][visualize-with-sfx].</span></span>

### <a name="version-and-upgrade-your-services"></a><span data-ttu-id="071ec-148">Version and upgrade your services</span><span class="sxs-lookup"><span data-stu-id="071ec-148">Version and upgrade your services</span></span>
<span data-ttu-id="071ec-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span><span class="sxs-lookup"><span data-stu-id="071ec-149">Service Fabric enables independent versioning and upgrading of independent services in an application.</span></span> <span data-ttu-id="071ec-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span><span class="sxs-lookup"><span data-stu-id="071ec-150">To learn more, see [Versioning and upgrading your services][app-upgrade-tutorial].</span></span>

### <a name="configure-continuous-integration-with-visual-studio-team-services"></a><span data-ttu-id="071ec-151">Configure continuous integration with Visual Studio Team Services</span><span class="sxs-lookup"><span data-stu-id="071ec-151">Configure continuous integration with Visual Studio Team Services</span></span>
<span data-ttu-id="071ec-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span><span class="sxs-lookup"><span data-stu-id="071ec-152">To learn how you can set up a continuous integration process for your Service Fabric application, see [Configure continuous integration with Visual Studio Team Services][ci-with-vso].</span></span>

<!-- Links -->
[add-web-frontend]: service-fabric-add-a-web-frontend.md
[create-cluster-in-portal]: service-fabric-cluster-creation-via-portal.md
[publish-app-to-azure]: service-fabric-publish-app-remote-cluster.md
[visualize-with-sfx]: service-fabric-visualizing-your-cluster.md
[ci-with-vso]: service-fabric-set-up-continuous-integration.md
[reliable-services-webapi]: service-fabric-reliable-services-communication-webapi.md
[app-upgrade-tutorial]: service-fabric-application-upgrade-tutorial.md
[aspnet-webapi]: https://docs.asp.net/en/latest/tutorials/first-web-api.html
[aspnet-webapp]: https://docs.asp.net/en/latest/tutorials/first-mvc-app/index.html
