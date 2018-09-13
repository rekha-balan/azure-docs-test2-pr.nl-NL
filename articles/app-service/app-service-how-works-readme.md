---
title: How Azure App Service works
description: Learn how App Service works
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: yochay
manager: erikre
editor: ''
ms.assetid: ae74fc32-969e-4580-8d61-02c922f1f184
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 02/23/2017
ms.author: yochayk
ms.openlocfilehash: 2d830963d3d2adba71a6ca99f79eac0fc8cbfb12
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563755"
---
# <a name="how-app-service-works"></a><span data-ttu-id="b6009-104">How App Service works</span><span class="sxs-lookup"><span data-stu-id="b6009-104">How App Service works</span></span>
<span data-ttu-id="b6009-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span><span class="sxs-lookup"><span data-stu-id="b6009-105">Azure App Service is a cloud service that's designed to solve the practical problems that engineers face today.</span></span>
<span data-ttu-id="b6009-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="b6009-106">App Service focuses on providing superior developer productivity without compromising on the need to deliver applications at cloud scale.</span></span> 

<span data-ttu-id="b6009-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span><span class="sxs-lookup"><span data-stu-id="b6009-107">App Service also provides the features and frameworks that are necessary for creating enterprise line-of-business applications.</span></span> <span data-ttu-id="b6009-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span><span class="sxs-lookup"><span data-stu-id="b6009-108">App Service lets you develop apps in most popular development languages, including Java, PHP, Node.js, Python, and the Microsoft .NET languages.</span></span> <span data-ttu-id="b6009-109">With App Service, you can:</span><span class="sxs-lookup"><span data-stu-id="b6009-109">With App Service, you can:</span></span>

* <span data-ttu-id="b6009-110">Build highly scalable web apps.</span><span class="sxs-lookup"><span data-stu-id="b6009-110">Build highly scalable web apps.</span></span>
* <span data-ttu-id="b6009-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span><span class="sxs-lookup"><span data-stu-id="b6009-111">Quickly build Mobile Apps back ends with a set of easy-to-use mobile capabilities such as data back ends, user authentication, and push notifications.</span></span>
* <span data-ttu-id="b6009-112">Implement, deploy, and publish APIs with API Apps.</span><span class="sxs-lookup"><span data-stu-id="b6009-112">Implement, deploy, and publish APIs with API Apps.</span></span>
* <span data-ttu-id="b6009-113">Tie business applications together into workflows and transform data with Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b6009-113">Tie business applications together into workflows and transform data with Logic Apps.</span></span>

> [!INCLUDE [app-service-linux](../../includes/app-service-linux.md)]
> 
> 

<span data-ttu-id="b6009-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span><span class="sxs-lookup"><span data-stu-id="b6009-114">All app types rely on the scalable and flexible Web Apps platform, which enables developers to have an optimized full lifecycle experience from app design to app maintenance.</span></span> <span data-ttu-id="b6009-115">The lifecycle capabilities enable the following:</span><span class="sxs-lookup"><span data-stu-id="b6009-115">The lifecycle capabilities enable the following:</span></span>

* <span data-ttu-id="b6009-116">**Quick app creation**.</span><span class="sxs-lookup"><span data-stu-id="b6009-116">**Quick app creation**.</span></span> <span data-ttu-id="b6009-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="b6009-117">Start from scratch or pick an operational support system (OSS) package from the Azure Marketplace.</span></span>
* <span data-ttu-id="b6009-118">**Continuous deployment**.</span><span class="sxs-lookup"><span data-stu-id="b6009-118">**Continuous deployment**.</span></span> <span data-ttu-id="b6009-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span><span class="sxs-lookup"><span data-stu-id="b6009-119">Automatically deploy new code from popular source control solutions such as TFS, GitHub, and Bitbucket, and sync content from online storage services such as OneDrive and Dropbox.</span></span>
* <span data-ttu-id="b6009-120">**Test in production**.</span><span class="sxs-lookup"><span data-stu-id="b6009-120">**Test in production**.</span></span> <span data-ttu-id="b6009-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span><span class="sxs-lookup"><span data-stu-id="b6009-121">Smoothly create pre-production environments and manage the amount of traffic that's going to them.</span></span> <span data-ttu-id="b6009-122">Debug in the cloud when needed, and roll back when issues are found.</span><span class="sxs-lookup"><span data-stu-id="b6009-122">Debug in the cloud when needed, and roll back when issues are found.</span></span>
* <span data-ttu-id="b6009-123">**Running asynchronous tasks and batch jobs**.</span><span class="sxs-lookup"><span data-stu-id="b6009-123">**Running asynchronous tasks and batch jobs**.</span></span> <span data-ttu-id="b6009-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span><span class="sxs-lookup"><span data-stu-id="b6009-124">Run code in a background process or activate your code based on events (such as messages landing in an Azure Storage queue) and scheduled times (CRON).</span></span>
* <span data-ttu-id="b6009-125">**Scaling the app**.</span><span class="sxs-lookup"><span data-stu-id="b6009-125">**Scaling the app**.</span></span> <span data-ttu-id="b6009-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span><span class="sxs-lookup"><span data-stu-id="b6009-126">Use one of many options to automatically scale your service horizontally and vertically based on traffic and resource utilization.</span></span> <span data-ttu-id="b6009-127">Configure private environments that are dedicated to your apps.</span><span class="sxs-lookup"><span data-stu-id="b6009-127">Configure private environments that are dedicated to your apps.</span></span>   
* <span data-ttu-id="b6009-128">**Maintaining the app**.</span><span class="sxs-lookup"><span data-stu-id="b6009-128">**Maintaining the app**.</span></span> <span data-ttu-id="b6009-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span><span class="sxs-lookup"><span data-stu-id="b6009-129">Use many of the debugging and diagnostics features to stay ahead of problems and to efficiently resolve them either in real time (with features such as auto-healing and live debugging) or after the fact by analyzing logs and memory dumps.</span></span>

<span data-ttu-id="b6009-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span><span class="sxs-lookup"><span data-stu-id="b6009-130">As a whole, App Service capabilities enable developers to focus on their code and quickly reach a stable and highly scalable production state.</span></span> <span data-ttu-id="b6009-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span><span class="sxs-lookup"><span data-stu-id="b6009-131">With the API Apps and Logic Apps features, developers can build real-world enterprise applications that bridge barriers between business solutions and on-premises to cloud integration.</span></span> 

## <a name="videos"></a><span data-ttu-id="b6009-132">Videos</span><span class="sxs-lookup"><span data-stu-id="b6009-132">Videos</span></span>
* [<span data-ttu-id="b6009-133">Azure App Service Architecture</span><span class="sxs-lookup"><span data-stu-id="b6009-133">Azure App Service Architecture</span></span>](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/)

## <a name="next-steps"></a><span data-ttu-id="b6009-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="b6009-134">Next steps</span></span>

<span data-ttu-id="b6009-135">Learn more about App Service in one of the following topics:</span><span class="sxs-lookup"><span data-stu-id="b6009-135">Learn more about App Service in one of the following topics:</span></span>

* [<span data-ttu-id="b6009-136">What is Azure App Service?</span><span class="sxs-lookup"><span data-stu-id="b6009-136">What is Azure App Service?</span></span>](app-service-value-prop-what-is.md)
  * [<span data-ttu-id="b6009-137">Web App</span><span class="sxs-lookup"><span data-stu-id="b6009-137">Web App</span></span>](../app-service-web/app-service-web-overview.md)
  * [<span data-ttu-id="b6009-138">Mobile App</span><span class="sxs-lookup"><span data-stu-id="b6009-138">Mobile App</span></span>](../app-service-mobile/app-service-mobile-value-prop.md)
  * [<span data-ttu-id="b6009-139">API App</span><span class="sxs-lookup"><span data-stu-id="b6009-139">API App</span></span>](../app-service-api/app-service-api-apps-why-best-platform.md)
* [<span data-ttu-id="b6009-140">Azure App Service Architecture (presentation)</span><span class="sxs-lookup"><span data-stu-id="b6009-140">Azure App Service Architecture (presentation)</span></span>](http://www.slideshare.net/maartenba/windows-azure-web-sites-things-they-dont-teach-kids-in-school-comunity-day-2013)
* [<span data-ttu-id="b6009-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span><span class="sxs-lookup"><span data-stu-id="b6009-141">Azure App Service, Cloud Services, and Virtual Machines comparison</span></span>](../app-service-web/choose-web-site-cloud-service-vm.md)
* [<span data-ttu-id="b6009-142">Understanding App Service Plans</span><span class="sxs-lookup"><span data-stu-id="b6009-142">Understanding App Service Plans</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
* [<span data-ttu-id="b6009-143">Introduction to App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b6009-143">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
  * [<span data-ttu-id="b6009-144">Exercise: Create an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="b6009-144">Exercise: Create an App Service Environment</span></span>](../app-service-web/app-service-web-how-to-create-an-app-service-environment.md)
* [<span data-ttu-id="b6009-145">Azure App Service Development Stacks Support</span><span class="sxs-lookup"><span data-stu-id="b6009-145">Azure App Service Development Stacks Support</span></span>](https://azure.microsoft.com/blog/windows-azure-websites-development-stacks-support/)



