---
title: How to Scale an App in an App Service Environment
description: Scaling an app in an App Service Environment
services: app-service
documentationcenter: ''
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: d04a5fce920dae25507cdf2f64832574e24c51dd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865158"
---
# <a name="scaling-apps-in-an-app-service-environment"></a><span data-ttu-id="8835d-103">Scaling apps in an App Service Environment</span><span class="sxs-lookup"><span data-stu-id="8835d-103">Scaling apps in an App Service Environment</span></span>
<span data-ttu-id="8835d-104">In the Azure App Service there are normally three things you can scale:</span><span class="sxs-lookup"><span data-stu-id="8835d-104">In the Azure App Service there are normally three things you can scale:</span></span>

* <span data-ttu-id="8835d-105">pricing plan</span><span class="sxs-lookup"><span data-stu-id="8835d-105">pricing plan</span></span>
* <span data-ttu-id="8835d-106">worker size</span><span class="sxs-lookup"><span data-stu-id="8835d-106">worker size</span></span> 
* <span data-ttu-id="8835d-107">number of instances.</span><span class="sxs-lookup"><span data-stu-id="8835d-107">number of instances.</span></span>

<span data-ttu-id="8835d-108">In an ASE there is no need to select or change the pricing plan.</span><span class="sxs-lookup"><span data-stu-id="8835d-108">In an ASE there is no need to select or change the pricing plan.</span></span>  <span data-ttu-id="8835d-109">In terms of capabilities it is already at a Premium pricing capability level.</span><span class="sxs-lookup"><span data-stu-id="8835d-109">In terms of capabilities it is already at a Premium pricing capability level.</span></span>  

<span data-ttu-id="8835d-110">With respect to worker sizes, the ASE admin can assign the size of the compute resource to be used for each worker pool.</span><span class="sxs-lookup"><span data-stu-id="8835d-110">With respect to worker sizes, the ASE admin can assign the size of the compute resource to be used for each worker pool.</span></span>  <span data-ttu-id="8835d-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span><span class="sxs-lookup"><span data-stu-id="8835d-111">That means you can have Worker Pool 1 with P4 compute resources and Worker Pool 2 with P1 compute resources, if desired.</span></span>  <span data-ttu-id="8835d-112">They do not have to be in size order.</span><span class="sxs-lookup"><span data-stu-id="8835d-112">They do not have to be in size order.</span></span>  <span data-ttu-id="8835d-113">For details around the sizes and their pricing see the document here [Azure App Service Pricing][AppServicePricing].</span><span class="sxs-lookup"><span data-stu-id="8835d-113">For details around the sizes and their pricing see the document here [Azure App Service Pricing][AppServicePricing].</span></span>  <span data-ttu-id="8835d-114">This leaves the scaling options for web apps and App Service Plans in an App Service Environment to be:</span><span class="sxs-lookup"><span data-stu-id="8835d-114">This leaves the scaling options for web apps and App Service Plans in an App Service Environment to be:</span></span>

* <span data-ttu-id="8835d-115">worker pool selection</span><span class="sxs-lookup"><span data-stu-id="8835d-115">worker pool selection</span></span>
* <span data-ttu-id="8835d-116">number of instances</span><span class="sxs-lookup"><span data-stu-id="8835d-116">number of instances</span></span>

<span data-ttu-id="8835d-117">Changing either item is done through the appropriate UI shown for your ASE hosted App Service Plans.</span><span class="sxs-lookup"><span data-stu-id="8835d-117">Changing either item is done through the appropriate UI shown for your ASE hosted App Service Plans.</span></span>  

![][1]

<span data-ttu-id="8835d-118">You can't scale up your ASP beyond the number of available compute resources in the worker pool that your ASP is in.</span><span class="sxs-lookup"><span data-stu-id="8835d-118">You can't scale up your ASP beyond the number of available compute resources in the worker pool that your ASP is in.</span></span>  <span data-ttu-id="8835d-119">If you need compute resources in that worker pool you need to get your ASE administrator to add them.</span><span class="sxs-lookup"><span data-stu-id="8835d-119">If you need compute resources in that worker pool you need to get your ASE administrator to add them.</span></span>  <span data-ttu-id="8835d-120">For information around re-configuring your ASE read the information here: [How to Configure an App Service environment][HowtoConfigureASE].</span><span class="sxs-lookup"><span data-stu-id="8835d-120">For information around re-configuring your ASE read the information here: [How to Configure an App Service environment][HowtoConfigureASE].</span></span>  <span data-ttu-id="8835d-121">You may also want to take advantage of the ASE autoscale features to add capacity based on schedule or metrics.</span><span class="sxs-lookup"><span data-stu-id="8835d-121">You may also want to take advantage of the ASE autoscale features to add capacity based on schedule or metrics.</span></span>  <span data-ttu-id="8835d-122">To get more details on configuring autoscale for the ASE environment itself see [How to configure autoscale for an App Service Environment][ASEAutoscale].</span><span class="sxs-lookup"><span data-stu-id="8835d-122">To get more details on configuring autoscale for the ASE environment itself see [How to configure autoscale for an App Service Environment][ASEAutoscale].</span></span>

<span data-ttu-id="8835d-123">You can create multiple app service plans using compute resources from different worker pools, or you can use the same worker pool.</span><span class="sxs-lookup"><span data-stu-id="8835d-123">You can create multiple app service plans using compute resources from different worker pools, or you can use the same worker pool.</span></span>  <span data-ttu-id="8835d-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose to create one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span><span class="sxs-lookup"><span data-stu-id="8835d-124">For example if you have (10) available compute resources in Worker Pool 1, you can choose to create one app service plan using (6) compute resources, and a second app service plan that uses (4) compute resources.</span></span>

### <a name="scaling-the-number-of-instances"></a><span data-ttu-id="8835d-125">Scaling the number of instances</span><span class="sxs-lookup"><span data-stu-id="8835d-125">Scaling the number of instances</span></span>
<span data-ttu-id="8835d-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span><span class="sxs-lookup"><span data-stu-id="8835d-126">When you first create your web app in an App Service Environment it starts with 1 instance.</span></span>  <span data-ttu-id="8835d-127">You can then scale out to additional instances to provide additional compute resources for your app.</span><span class="sxs-lookup"><span data-stu-id="8835d-127">You can then scale out to additional instances to provide additional compute resources for your app.</span></span>   

<span data-ttu-id="8835d-128">If your ASE has enough capacity then this is pretty simple.</span><span class="sxs-lookup"><span data-stu-id="8835d-128">If your ASE has enough capacity then this is pretty simple.</span></span>  <span data-ttu-id="8835d-129">You go to your App Service Plan that holds the sites you want to scale up and select Scale.</span><span class="sxs-lookup"><span data-stu-id="8835d-129">You go to your App Service Plan that holds the sites you want to scale up and select Scale.</span></span>  <span data-ttu-id="8835d-130">This opens the UI where you can manually set the scale for your ASP or configure autoscale rules for your ASP.</span><span class="sxs-lookup"><span data-stu-id="8835d-130">This opens the UI where you can manually set the scale for your ASP or configure autoscale rules for your ASP.</span></span>  <span data-ttu-id="8835d-131">To manually scale your app simply set ***Scale by*** to ***an instance count that I enter manually***.</span><span class="sxs-lookup"><span data-stu-id="8835d-131">To manually scale your app simply set ***Scale by*** to ***an instance count that I enter manually***.</span></span>  <span data-ttu-id="8835d-132">From here either drag the slider to the desired quantity or enter it in the box next to the slider.</span><span class="sxs-lookup"><span data-stu-id="8835d-132">From here either drag the slider to the desired quantity or enter it in the box next to the slider.</span></span>  

![][2] 

<span data-ttu-id="8835d-133">The autoscale rules for an ASP in an ASE work the same as they do normally.</span><span class="sxs-lookup"><span data-stu-id="8835d-133">The autoscale rules for an ASP in an ASE work the same as they do normally.</span></span>  <span data-ttu-id="8835d-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span><span class="sxs-lookup"><span data-stu-id="8835d-134">You can select ***CPU Percentage*** under ***Scale by*** and create autoscale rules for your ASP based on CPU Percentage or you can create more complex rules using ***schedule and performance rules***.</span></span>  <span data-ttu-id="8835d-135">To see more complete details on configuring autoscale use the guide here [Scale an app in Azure App Service][AppScale].</span><span class="sxs-lookup"><span data-stu-id="8835d-135">To see more complete details on configuring autoscale use the guide here [Scale an app in Azure App Service][AppScale].</span></span> 

### <a name="worker-pool-selection"></a><span data-ttu-id="8835d-136">Worker Pool selection</span><span class="sxs-lookup"><span data-stu-id="8835d-136">Worker Pool selection</span></span>
<span data-ttu-id="8835d-137">As noted earlier, the worker pool selection is accessed from the ASP UI.</span><span class="sxs-lookup"><span data-stu-id="8835d-137">As noted earlier, the worker pool selection is accessed from the ASP UI.</span></span>  <span data-ttu-id="8835d-138">Open the blade for the ASP that you want to scale and select worker pool.</span><span class="sxs-lookup"><span data-stu-id="8835d-138">Open the blade for the ASP that you want to scale and select worker pool.</span></span>  <span data-ttu-id="8835d-139">You will see all of the worker pools which you have configured in your App Service Environment.</span><span class="sxs-lookup"><span data-stu-id="8835d-139">You will see all of the worker pools which you have configured in your App Service Environment.</span></span>  <span data-ttu-id="8835d-140">If you have only one worker pool then you will only see the one pool listed.</span><span class="sxs-lookup"><span data-stu-id="8835d-140">If you have only one worker pool then you will only see the one pool listed.</span></span>  <span data-ttu-id="8835d-141">To change what worker pool your ASP is in, you simply select the worker pool you want your App Service Plan to move to.</span><span class="sxs-lookup"><span data-stu-id="8835d-141">To change what worker pool your ASP is in, you simply select the worker pool you want your App Service Plan to move to.</span></span>  

![][3]

<span data-ttu-id="8835d-142">Before moving your ASP from one worker pool to another it is important to make sure you will have adequate capacity for your ASP.</span><span class="sxs-lookup"><span data-stu-id="8835d-142">Before moving your ASP from one worker pool to another it is important to make sure you will have adequate capacity for your ASP.</span></span>  <span data-ttu-id="8835d-143">In the list of worker pools, not only is the worker pool name listed but you can also see how many workers are available in that worker pool.</span><span class="sxs-lookup"><span data-stu-id="8835d-143">In the list of worker pools, not only is the worker pool name listed but you can also see how many workers are available in that worker pool.</span></span>  <span data-ttu-id="8835d-144">Make sure that there are enough instances available to contain your App Service Plan.</span><span class="sxs-lookup"><span data-stu-id="8835d-144">Make sure that there are enough instances available to contain your App Service Plan.</span></span>  <span data-ttu-id="8835d-145">If you need more compute resources in the worker pool you wish to move to, then get your ASE administrator to add them.</span><span class="sxs-lookup"><span data-stu-id="8835d-145">If you need more compute resources in the worker pool you wish to move to, then get your ASE administrator to add them.</span></span>  

> [!NOTE]
> <span data-ttu-id="8835d-146">Moving an ASP from one worker pool will cause cold starts of the apps in that ASP.</span><span class="sxs-lookup"><span data-stu-id="8835d-146">Moving an ASP from one worker pool will cause cold starts of the apps in that ASP.</span></span>  <span data-ttu-id="8835d-147">This can cause requests to run slowly as your app is cold started on the new compute resources.</span><span class="sxs-lookup"><span data-stu-id="8835d-147">This can cause requests to run slowly as your app is cold started on the new compute resources.</span></span>  <span data-ttu-id="8835d-148">The cold start can be avoided by using the [application warm up capability][AppWarmup] in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="8835d-148">The cold start can be avoided by using the [application warm up capability][AppWarmup] in Azure App Service.</span></span>  <span data-ttu-id="8835d-149">The Application Initialization module described in the article also works for cold starts because the initialization process is also invoked when apps are cold started on new compute resources.</span><span class="sxs-lookup"><span data-stu-id="8835d-149">The Application Initialization module described in the article also works for cold starts because the initialization process is also invoked when apps are cold started on new compute resources.</span></span> 
> 
> 

## <a name="getting-started"></a><span data-ttu-id="8835d-150">Getting started</span><span class="sxs-lookup"><span data-stu-id="8835d-150">Getting started</span></span>
<span data-ttu-id="8835d-151">To get started with App Service Environments, see [How To Create An App Service Environment][HowtoCreateASE]</span><span class="sxs-lookup"><span data-stu-id="8835d-151">To get started with App Service Environments, see [How To Create An App Service Environment][HowtoCreateASE]</span></span>

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: app-service-app-service-environment-intro.md
[ScaleWebapp]: ../web-sites-scale.md
[HowtoCreateASE]: app-service-web-how-to-create-an-app-service-environment.md
[HowtoConfigureASE]: app-service-web-configure-an-app-service-environment.md
[CreateWebappinASE]: app-service-web-how-to-create-a-web-app-in-an-ase.md
[Appserviceplans]: ../azure-web-sites-web-hosting-plans-in-depth-overview.md
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[ASEAutoscale]: app-service-environment-auto-scale.md
[AppScale]: ../web-sites-scale.md
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
