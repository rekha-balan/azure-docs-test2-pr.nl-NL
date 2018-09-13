---
title: Azure App Service plans in-depth overview | Microsoft Docs
description: Learn how App Service plans for Azure App Service work, and how they benefit your management experience.
keywords: app service, azure app service, scale, scalable, app service plan, app service cost
services: app-service
documentationcenter: ''
author: btardif
manager: erikre
editor: ''
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: eae59562bfb2892da2c37fce1d108b32c2ebfbcf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552305"
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="c3564-104">Azure App Service plans in-depth overview</span><span class="sxs-lookup"><span data-stu-id="c3564-104">Azure App Service plans in-depth overview</span></span>
<span data-ttu-id="c3564-105">App Service plans represent the collection of physical resources used to host your apps.</span><span class="sxs-lookup"><span data-stu-id="c3564-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="c3564-106">App Service plans define:</span><span class="sxs-lookup"><span data-stu-id="c3564-106">App Service plans define:</span></span>

- <span data-ttu-id="c3564-107">Region (West US, East US, etc.)</span><span class="sxs-lookup"><span data-stu-id="c3564-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="c3564-108">Scale count (one, two, three instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="c3564-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="c3564-109">Instance size (Small, Medium, Large)</span><span class="sxs-lookup"><span data-stu-id="c3564-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="c3564-110">SKU (Free, Shared, Basic, Standard, Premium)</span><span class="sxs-lookup"><span data-stu-id="c3564-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="c3564-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="c3564-112">Apps in the same subscription, region, and resource group can share an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-112">Apps in the same subscription, region, and resource group can share an App Service plan.</span></span> 

<span data-ttu-id="c3564-113">All applications assigned to an **App Service plan** share the resources defined by it.</span><span class="sxs-lookup"><span data-stu-id="c3564-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="c3564-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="c3564-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span><span class="sxs-lookup"><span data-stu-id="c3564-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span> 

<span data-ttu-id="c3564-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span><span class="sxs-lookup"><span data-stu-id="c3564-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="c3564-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span><span class="sxs-lookup"><span data-stu-id="c3564-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="c3564-118">Apps also have access to the standard service tier features.</span><span class="sxs-lookup"><span data-stu-id="c3564-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="c3564-119">Plan instances on which apps are running are fully managed and highly available.</span><span class="sxs-lookup"><span data-stu-id="c3564-119">Plan instances on which apps are running are fully managed and highly available.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c3564-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span><span class="sxs-lookup"><span data-stu-id="c3564-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="c3564-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span><span class="sxs-lookup"><span data-stu-id="c3564-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="c3564-122">Apps and App Service plans</span><span class="sxs-lookup"><span data-stu-id="c3564-122">Apps and App Service plans</span></span>
<span data-ttu-id="c3564-123">An app in App Service can be associated with only one App Service plan at any given time.</span><span class="sxs-lookup"><span data-stu-id="c3564-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="c3564-124">Both apps and plans are contained in a **resource group**.</span><span class="sxs-lookup"><span data-stu-id="c3564-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="c3564-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span><span class="sxs-lookup"><span data-stu-id="c3564-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="c3564-126">You can use resource groups to manage all the pieces of an application together.</span><span class="sxs-lookup"><span data-stu-id="c3564-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="c3564-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span><span class="sxs-lookup"><span data-stu-id="c3564-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span> 

<span data-ttu-id="c3564-128">For example, you can separate resources among dev, test, and production environments.</span><span class="sxs-lookup"><span data-stu-id="c3564-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="c3564-129">Having separate environments for production and dev/test lets you isolate resources.</span><span class="sxs-lookup"><span data-stu-id="c3564-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="c3564-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span><span class="sxs-lookup"><span data-stu-id="c3564-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="c3564-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span><span class="sxs-lookup"><span data-stu-id="c3564-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span> 

<span data-ttu-id="c3564-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="c3564-133">In such a situation, all the copies of the app are then contained in a single resource group.</span><span class="sxs-lookup"><span data-stu-id="c3564-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="c3564-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span><span class="sxs-lookup"><span data-stu-id="c3564-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="c3564-135">Create an App Service plan or use existing one</span><span class="sxs-lookup"><span data-stu-id="c3564-135">Create an App Service plan or use existing one</span></span>
<span data-ttu-id="c3564-136">When you create an app, you should consider creating a resource group.</span><span class="sxs-lookup"><span data-stu-id="c3564-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="c3564-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span><span class="sxs-lookup"><span data-stu-id="c3564-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="c3564-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span><span class="sxs-lookup"><span data-stu-id="c3564-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="c3564-139">This decision is more a question of capacity and expected load.</span><span class="sxs-lookup"><span data-stu-id="c3564-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="c3564-140">We recommend isolating your app into a new App Service plan when:</span><span class="sxs-lookup"><span data-stu-id="c3564-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="c3564-141">App is resource-intensive.</span><span class="sxs-lookup"><span data-stu-id="c3564-141">App is resource-intensive.</span></span> 
- <span data-ttu-id="c3564-142">App has different scaling factors from the other apps hosted in an existing plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="c3564-143">App needs resource in a different geographical region.</span><span class="sxs-lookup"><span data-stu-id="c3564-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="c3564-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span><span class="sxs-lookup"><span data-stu-id="c3564-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="c3564-145">Create an App Service plan</span><span class="sxs-lookup"><span data-stu-id="c3564-145">Create an App Service plan</span></span>
> [!TIP]
> <span data-ttu-id="c3564-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="c3564-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>
 

<span data-ttu-id="c3564-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span><span class="sxs-lookup"><span data-stu-id="c3564-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="c3564-148">In the [Azure portal](https://portal.azure.com), click **New** > 
**Web + mobile**, and then select **Web App** or other App Service app kind.</span><span class="sxs-lookup"><span data-stu-id="c3564-148">In the [Azure portal](https://portal.azure.com), click **New** > 
**Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>
<span data-ttu-id="c3564-149">![Create an app in the Azure portal.][createWebApp]</span><span class="sxs-lookup"><span data-stu-id="c3564-149">![Create an app in the Azure portal.][createWebApp]</span></span>

<span data-ttu-id="c3564-150">You can then select or create the App Service plan for the new app.</span><span class="sxs-lookup"><span data-stu-id="c3564-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Create an App Service plan.][createASP]

<span data-ttu-id="c3564-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span><span class="sxs-lookup"><span data-stu-id="c3564-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="c3564-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span><span class="sxs-lookup"><span data-stu-id="c3564-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="c3564-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span><span class="sxs-lookup"><span data-stu-id="c3564-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="c3564-155">After you have selected the pricing tier, click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="c3564-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="c3564-156">Move an app to a different App Service plan</span><span class="sxs-lookup"><span data-stu-id="c3564-156">Move an app to a different App Service plan</span></span>
<span data-ttu-id="c3564-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c3564-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c3564-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span><span class="sxs-lookup"><span data-stu-id="c3564-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="c3564-159">To move an app to another plan:</span><span class="sxs-lookup"><span data-stu-id="c3564-159">To move an app to another plan:</span></span>

- <span data-ttu-id="c3564-160">Navigate to the app that you want to move.</span><span class="sxs-lookup"><span data-stu-id="c3564-160">Navigate to the app that you want to move.</span></span> 
- <span data-ttu-id="c3564-161">In the **Menu**, look for the **App Service Plan** section.</span><span class="sxs-lookup"><span data-stu-id="c3564-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="c3564-162">Select **Change App Service plan** to start the process.</span><span class="sxs-lookup"><span data-stu-id="c3564-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="c3564-163">**Change App Service plan** opens the **App Service plan** selector.</span><span class="sxs-lookup"><span data-stu-id="c3564-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="c3564-164">At this point, you can pick an existing plan to move this app into.</span><span class="sxs-lookup"><span data-stu-id="c3564-164">At this point, you can pick an existing plan to move this app into.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="c3564-165">Only valid plans (in the same resource group and geographical location) are shown.</span><span class="sxs-lookup"><span data-stu-id="c3564-165">Only valid plans (in the same resource group and geographical location) are shown.</span></span>

![App Service plan selector.][change]

<span data-ttu-id="c3564-167">Each plan has its own pricing tier.</span><span class="sxs-lookup"><span data-stu-id="c3564-167">Each plan has its own pricing tier.</span></span> <span data-ttu-id="c3564-168">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span><span class="sxs-lookup"><span data-stu-id="c3564-168">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="c3564-169">Clone an app to a different App Service plan</span><span class="sxs-lookup"><span data-stu-id="c3564-169">Clone an app to a different App Service plan</span></span>
<span data-ttu-id="c3564-170">If you want to move the app to a different region, one alternative is app cloning.</span><span class="sxs-lookup"><span data-stu-id="c3564-170">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="c3564-171">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span><span class="sxs-lookup"><span data-stu-id="c3564-171">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="c3564-172">You can find **Clone App** in the **Development Tools** section of the menu.</span><span class="sxs-lookup"><span data-stu-id="c3564-172">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3564-173">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c3564-173">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="c3564-174">Scale an App Service plan</span><span class="sxs-lookup"><span data-stu-id="c3564-174">Scale an App Service plan</span></span>
<span data-ttu-id="c3564-175">There are three ways to scale a plan:</span><span class="sxs-lookup"><span data-stu-id="c3564-175">There are three ways to scale a plan:</span></span>

* <span data-ttu-id="c3564-176">**Change the plan’s pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="c3564-176">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="c3564-177">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span><span class="sxs-lookup"><span data-stu-id="c3564-177">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
* <span data-ttu-id="c3564-178">**Change the plan’s instance size**.</span><span class="sxs-lookup"><span data-stu-id="c3564-178">**Change the plan’s instance size**.</span></span> <span data-ttu-id="c3564-179">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span><span class="sxs-lookup"><span data-stu-id="c3564-179">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="c3564-180">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span><span class="sxs-lookup"><span data-stu-id="c3564-180">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
* <span data-ttu-id="c3564-181">**Change the plan’s instance count**.</span><span class="sxs-lookup"><span data-stu-id="c3564-181">**Change the plan’s instance count**.</span></span> <span data-ttu-id="c3564-182">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span><span class="sxs-lookup"><span data-stu-id="c3564-182">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="c3564-183">A Premium plan can be scaled out to 20 instances (subject to availability).</span><span class="sxs-lookup"><span data-stu-id="c3564-183">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="c3564-184">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span><span class="sxs-lookup"><span data-stu-id="c3564-184">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="c3564-185">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="c3564-185">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="c3564-186">Changes apply to the App Service plan and affect all apps that it hosts.</span><span class="sxs-lookup"><span data-stu-id="c3564-186">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Set values to scale up an app.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="c3564-188">App Service plan cleanup</span><span class="sxs-lookup"><span data-stu-id="c3564-188">App Service plan cleanup</span></span>
> [!IMPORTANT]
><span data-ttu-id="c3564-189">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span><span class="sxs-lookup"><span data-stu-id="c3564-189">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="c3564-190">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span><span class="sxs-lookup"><span data-stu-id="c3564-190">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="c3564-191">Summary</span><span class="sxs-lookup"><span data-stu-id="c3564-191">Summary</span></span>
<span data-ttu-id="c3564-192">App Service plans represent a set of features and capacity that you can share across your apps.</span><span class="sxs-lookup"><span data-stu-id="c3564-192">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="c3564-193">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span><span class="sxs-lookup"><span data-stu-id="c3564-193">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="c3564-194">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span><span class="sxs-lookup"><span data-stu-id="c3564-194">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="c3564-195">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span><span class="sxs-lookup"><span data-stu-id="c3564-195">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="c3564-196">What's changed</span><span class="sxs-lookup"><span data-stu-id="c3564-196">What's changed</span></span>
* <span data-ttu-id="c3564-197">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="c3564-197">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service/media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png




