---
title: Set up staging environments for web apps in Azure App Service | Microsoft Docs
description: Learn how to use staged publishing for web apps in Azure App Service.
services: app-service
documentationcenter: ''
author: cephalin
writer: cephalin
manager: erikre
editor: mollybos
ms.assetid: e224fc4f-800d-469a-8d6a-72bcde612450
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: cephalin
ms.openlocfilehash: 2fabf0d61ffd2f526fab49816eab36a86497a358
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967841"
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="f676b-103">Set up staging environments in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f676b-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="f676b-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan tier.</span><span class="sxs-lookup"><span data-stu-id="f676b-104">When you deploy your web app, web app on Linux, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan tier.</span></span> <span data-ttu-id="f676b-105">Deployment slots are actually live apps with their own hostnames.</span><span class="sxs-lookup"><span data-stu-id="f676b-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="f676b-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="f676b-107">Deploying your application to a deployment slot has the following benefits:</span><span class="sxs-lookup"><span data-stu-id="f676b-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="f676b-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="f676b-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span><span class="sxs-lookup"><span data-stu-id="f676b-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="f676b-110">This eliminates downtime when you deploy your app.</span><span class="sxs-lookup"><span data-stu-id="f676b-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="f676b-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span><span class="sxs-lookup"><span data-stu-id="f676b-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="f676b-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span><span class="sxs-lookup"><span data-stu-id="f676b-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="f676b-113">After a swap, the slot with previously staged app now has the previous production app.</span><span class="sxs-lookup"><span data-stu-id="f676b-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="f676b-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span><span class="sxs-lookup"><span data-stu-id="f676b-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="f676b-115">Each App Service plan tier supports a different number of deployment slots.</span><span class="sxs-lookup"><span data-stu-id="f676b-115">Each App Service plan tier supports a different number of deployment slots.</span></span> <span data-ttu-id="f676b-116">To find out the number of slots your app's tier supports, see [App Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits#app-service-limits).</span><span class="sxs-lookup"><span data-stu-id="f676b-116">To find out the number of slots your app's tier supports, see [App Service Limits](https://docs.microsoft.com/azure/azure-subscription-service-limits#app-service-limits).</span></span> <span data-ttu-id="f676b-117">To scale your app to a different tier, the target tier must support the number of slots your app already uses.</span><span class="sxs-lookup"><span data-stu-id="f676b-117">To scale your app to a different tier, the target tier must support the number of slots your app already uses.</span></span> <span data-ttu-id="f676b-118">For example, if your app has more than 5 slots, you cannot scale it down to **Standard** tier, because **Standard** tier only supports 5 deployment slots.</span><span class="sxs-lookup"><span data-stu-id="f676b-118">For example, if your app has more than 5 slots, you cannot scale it down to **Standard** tier, because **Standard** tier only supports 5 deployment slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="f676b-119">Add a deployment slot</span><span class="sxs-lookup"><span data-stu-id="f676b-119">Add a deployment slot</span></span>
<span data-ttu-id="f676b-120">The app must be running in the **Standard** or **Premium** tier in order for you to enable multiple deployment slots.</span><span class="sxs-lookup"><span data-stu-id="f676b-120">The app must be running in the **Standard** or **Premium** tier in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="f676b-121">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="f676b-121">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="f676b-122">Choose the **Deployment slots** option, then click **Add Slot**.</span><span class="sxs-lookup"><span data-stu-id="f676b-122">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Add a new deployment slot][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="f676b-124">If the app is not already in the **Standard** or **Premium** tier, you will receive a message indicating the supported tiers for enabling staged publishing.</span><span class="sxs-lookup"><span data-stu-id="f676b-124">If the app is not already in the **Standard** or **Premium** tier, you will receive a message indicating the supported tiers for enabling staged publishing.</span></span> <span data-ttu-id="f676b-125">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span><span class="sxs-lookup"><span data-stu-id="f676b-125">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="f676b-126">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-126">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="f676b-127">Click the check mark to continue.</span><span class="sxs-lookup"><span data-stu-id="f676b-127">Click the check mark to continue.</span></span>
   
    ![Configuration Source][ConfigurationSource1]
   
    <span data-ttu-id="f676b-129">The first time you add a slot, you only have two choices: clone configuration from the default slot in production or not at all.</span><span class="sxs-lookup"><span data-stu-id="f676b-129">The first time you add a slot, you only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="f676b-130">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span><span class="sxs-lookup"><span data-stu-id="f676b-130">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Configuration sources][MultipleConfigurationSources]
4. <span data-ttu-id="f676b-132">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span><span class="sxs-lookup"><span data-stu-id="f676b-132">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="f676b-133">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-133">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Deployment Slot Title][StagingTitle]
5. <span data-ttu-id="f676b-135">Click the app URL in the slot's blade.</span><span class="sxs-lookup"><span data-stu-id="f676b-135">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="f676b-136">Notice the deployment slot has its own hostname and is also a live app.</span><span class="sxs-lookup"><span data-stu-id="f676b-136">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="f676b-137">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="f676b-137">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="f676b-138">There is no content after deployment slot creation.</span><span class="sxs-lookup"><span data-stu-id="f676b-138">There is no content after deployment slot creation.</span></span> <span data-ttu-id="f676b-139">You can deploy to the slot from a different repository branch, or an altogether different repository.</span><span class="sxs-lookup"><span data-stu-id="f676b-139">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="f676b-140">You can also change the slot's configuration.</span><span class="sxs-lookup"><span data-stu-id="f676b-140">You can also change the slot's configuration.</span></span> <span data-ttu-id="f676b-141">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span><span class="sxs-lookup"><span data-stu-id="f676b-141">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="f676b-142">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="f676b-142">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="which-settings-are-swapped"></a><span data-ttu-id="f676b-143">Which settings are swapped?</span><span class="sxs-lookup"><span data-stu-id="f676b-143">Which settings are swapped?</span></span>
<span data-ttu-id="f676b-144">When you clone configuration from another deployment slot, the cloned configuration is editable.</span><span class="sxs-lookup"><span data-stu-id="f676b-144">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="f676b-145">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span><span class="sxs-lookup"><span data-stu-id="f676b-145">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="f676b-146">The following lists show the settings that change when you swap slots.</span><span class="sxs-lookup"><span data-stu-id="f676b-146">The following lists show the settings that change when you swap slots.</span></span>

<span data-ttu-id="f676b-147">**Settings that are swapped**:</span><span class="sxs-lookup"><span data-stu-id="f676b-147">**Settings that are swapped**:</span></span>

* <span data-ttu-id="f676b-148">General settings - such as framework version, 32/64-bit, Web sockets</span><span class="sxs-lookup"><span data-stu-id="f676b-148">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="f676b-149">App settings (can be configured to stick to a slot)</span><span class="sxs-lookup"><span data-stu-id="f676b-149">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="f676b-150">Connection strings (can be configured to stick to a slot)</span><span class="sxs-lookup"><span data-stu-id="f676b-150">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="f676b-151">Handler mappings</span><span class="sxs-lookup"><span data-stu-id="f676b-151">Handler mappings</span></span>
* <span data-ttu-id="f676b-152">Monitoring and diagnostic settings</span><span class="sxs-lookup"><span data-stu-id="f676b-152">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="f676b-153">WebJobs content</span><span class="sxs-lookup"><span data-stu-id="f676b-153">WebJobs content</span></span>

<span data-ttu-id="f676b-154">**Settings that are not swapped**:</span><span class="sxs-lookup"><span data-stu-id="f676b-154">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="f676b-155">Publishing endpoints</span><span class="sxs-lookup"><span data-stu-id="f676b-155">Publishing endpoints</span></span>
* <span data-ttu-id="f676b-156">Custom Domain Names</span><span class="sxs-lookup"><span data-stu-id="f676b-156">Custom Domain Names</span></span>
* <span data-ttu-id="f676b-157">SSL certificates and bindings</span><span class="sxs-lookup"><span data-stu-id="f676b-157">SSL certificates and bindings</span></span>
* <span data-ttu-id="f676b-158">Scale settings</span><span class="sxs-lookup"><span data-stu-id="f676b-158">Scale settings</span></span>
* <span data-ttu-id="f676b-159">WebJobs schedulers</span><span class="sxs-lookup"><span data-stu-id="f676b-159">WebJobs schedulers</span></span>

<span data-ttu-id="f676b-160">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-160">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="f676b-161">Marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span><span class="sxs-lookup"><span data-stu-id="f676b-161">Marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Slot settings][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="f676b-163">Swap deployment slots</span><span class="sxs-lookup"><span data-stu-id="f676b-163">Swap deployment slots</span></span> 
<span data-ttu-id="f676b-164">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span><span class="sxs-lookup"><span data-stu-id="f676b-164">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f676b-165">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span><span class="sxs-lookup"><span data-stu-id="f676b-165">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="f676b-166">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-166">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Swap Button][SwapButtonBar]

2. <span data-ttu-id="f676b-168">Make sure that the swap source and swap target are set properly.</span><span class="sxs-lookup"><span data-stu-id="f676b-168">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="f676b-169">Usually, the swap target is the production slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-169">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="f676b-170">Click **OK** to complete the operation.</span><span class="sxs-lookup"><span data-stu-id="f676b-170">Click **OK** to complete the operation.</span></span> <span data-ttu-id="f676b-171">When the operation finishes, the deployment slots have been swapped.</span><span class="sxs-lookup"><span data-stu-id="f676b-171">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Complete swap](./media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="f676b-173">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="f676b-173">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="f676b-174">Swap with preview (multi-phase swap)</span><span class="sxs-lookup"><span data-stu-id="f676b-174">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="f676b-175">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span><span class="sxs-lookup"><span data-stu-id="f676b-175">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="f676b-176">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span><span class="sxs-lookup"><span data-stu-id="f676b-176">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="f676b-177">Swap with preview is what you need.</span><span class="sxs-lookup"><span data-stu-id="f676b-177">Swap with preview is what you need.</span></span>

> [!NOTE]
> <span data-ttu-id="f676b-178">Swap with preview is not supported in web apps on Linux.</span><span class="sxs-lookup"><span data-stu-id="f676b-178">Swap with preview is not supported in web apps on Linux.</span></span>

<span data-ttu-id="f676b-179">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span><span class="sxs-lookup"><span data-stu-id="f676b-179">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="f676b-180">Keeps the destination slot unchanged so existing workload on that slot (such as production) is not impacted.</span><span class="sxs-lookup"><span data-stu-id="f676b-180">Keeps the destination slot unchanged so existing workload on that slot (such as production) is not impacted.</span></span>
- <span data-ttu-id="f676b-181">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span><span class="sxs-lookup"><span data-stu-id="f676b-181">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="f676b-182">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span><span class="sxs-lookup"><span data-stu-id="f676b-182">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="f676b-183">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-183">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="f676b-184">The destination slot is moved into the source slot as in a manual swap.</span><span class="sxs-lookup"><span data-stu-id="f676b-184">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="f676b-185">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-185">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="f676b-186">You can preview exactly how the app will behave with the destination slot's configuration.</span><span class="sxs-lookup"><span data-stu-id="f676b-186">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="f676b-187">Once you complete validation, you complete the swap in a separate step.</span><span class="sxs-lookup"><span data-stu-id="f676b-187">Once you complete validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="f676b-188">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients don't experience any downtime.</span><span class="sxs-lookup"><span data-stu-id="f676b-188">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients don't experience any downtime.</span></span>  

<span data-ttu-id="f676b-189">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span><span class="sxs-lookup"><span data-stu-id="f676b-189">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="f676b-190">Configure Auto Swap</span><span class="sxs-lookup"><span data-stu-id="f676b-190">Configure Auto Swap</span></span>
<span data-ttu-id="f676b-191">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span><span class="sxs-lookup"><span data-stu-id="f676b-191">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="f676b-192">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-192">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f676b-193">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span><span class="sxs-lookup"><span data-stu-id="f676b-193">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

> [!NOTE]
> <span data-ttu-id="f676b-194">Auto Swap is not supported in web apps on Linux.</span><span class="sxs-lookup"><span data-stu-id="f676b-194">Auto Swap is not supported in web apps on Linux.</span></span>

<span data-ttu-id="f676b-195">Configuring Auto Swap for a slot is easy.</span><span class="sxs-lookup"><span data-stu-id="f676b-195">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="f676b-196">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="f676b-196">Follow these steps:</span></span>

1. <span data-ttu-id="f676b-197">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span><span class="sxs-lookup"><span data-stu-id="f676b-197">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="f676b-198">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="f676b-198">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="f676b-199">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-199">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="f676b-200">The **Notifications** tab flashes a green **SUCCESS** once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="f676b-200">The **Notifications** tab flashes a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="f676b-201">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span><span class="sxs-lookup"><span data-stu-id="f676b-201">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="f676b-202">Execute a code push to that deployment slot.</span><span class="sxs-lookup"><span data-stu-id="f676b-202">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="f676b-203">Auto Swap happens after a short time and the update is reflected at your target slot's URL.</span><span class="sxs-lookup"><span data-stu-id="f676b-203">Auto Swap happens after a short time and the update is reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="roll-back-a-production-app-after-swap"></a><span data-ttu-id="f676b-204">Roll back a production app after swap</span><span class="sxs-lookup"><span data-stu-id="f676b-204">Roll back a production app after swap</span></span>
<span data-ttu-id="f676b-205">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span><span class="sxs-lookup"><span data-stu-id="f676b-205">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="f676b-206">Custom warm-up before swap</span><span class="sxs-lookup"><span data-stu-id="f676b-206">Custom warm-up before swap</span></span>
<span data-ttu-id="f676b-207">Some apps may require custom warm-up actions.</span><span class="sxs-lookup"><span data-stu-id="f676b-207">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="f676b-208">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span><span class="sxs-lookup"><span data-stu-id="f676b-208">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="f676b-209">The swap operation waits for this custom warm-up to complete.</span><span class="sxs-lookup"><span data-stu-id="f676b-209">The swap operation waits for this custom warm-up to complete.</span></span> <span data-ttu-id="f676b-210">Here is a sample web.config fragment.</span><span class="sxs-lookup"><span data-stu-id="f676b-210">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

## <a name="monitor-swap-progress"></a><span data-ttu-id="f676b-211">Monitor swap progress</span><span class="sxs-lookup"><span data-stu-id="f676b-211">Monitor swap progress</span></span>

<span data-ttu-id="f676b-212">Sometimes, the swap operation takes some time to complete, such as when the app that is swapped has a long warm-up time.</span><span class="sxs-lookup"><span data-stu-id="f676b-212">Sometimes, the swap operation takes some time to complete, such as when the app that is swapped has a long warm-up time.</span></span> <span data-ttu-id="f676b-213">You can get more information on swap operations in the [Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f676b-213">You can get more information on swap operations in the [Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) in the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="f676b-214">In your app page of the portal, in the left-hand navigation, select **Activity log**.</span><span class="sxs-lookup"><span data-stu-id="f676b-214">In your app page of the portal, in the left-hand navigation, select **Activity log**.</span></span>

<span data-ttu-id="f676b-215">A swap operation appears in the log query as `Slotsswap`.</span><span class="sxs-lookup"><span data-stu-id="f676b-215">A swap operation appears in the log query as `Slotsswap`.</span></span> <span data-ttu-id="f676b-216">You can expand it and select one of the suboperations or errors to see the details.</span><span class="sxs-lookup"><span data-stu-id="f676b-216">You can expand it and select one of the suboperations or errors to see the details.</span></span>

![Activity log for slot swap](media/web-sites-staged-publishing/activity-log.png)

<a name="Delete"></a>

## <a name="delete-a-deployment-slot"></a><span data-ttu-id="f676b-218">Delete a deployment slot</span><span class="sxs-lookup"><span data-stu-id="f676b-218">Delete a deployment slot</span></span>
<span data-ttu-id="f676b-219">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="f676b-219">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Delete a Deployment Slot][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="automate-with-azure-powershell"></a><span data-ttu-id="f676b-221">Automate with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f676b-221">Automate with Azure PowerShell</span></span>

<span data-ttu-id="f676b-222">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="f676b-222">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="f676b-223">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f676b-223">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azure/overview).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="f676b-224">Create a web app</span><span class="sxs-lookup"><span data-stu-id="f676b-224">Create a web app</span></span>
```PowerShell
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="f676b-225">Create a deployment slot</span><span class="sxs-lookup"><span data-stu-id="f676b-225">Create a deployment slot</span></span>
```PowerShell
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-preview-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="f676b-226">Initiate a swap with preview (multi-phase swap) and apply destination slot configuration to source slot</span><span class="sxs-lookup"><span data-stu-id="f676b-226">Initiate a swap with preview (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```PowerShell
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="f676b-227">Cancel a pending swap (swap with review) and restore source slot configuration</span><span class="sxs-lookup"><span data-stu-id="f676b-227">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```PowerShell
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="f676b-228">Swap deployment slots</span><span class="sxs-lookup"><span data-stu-id="f676b-228">Swap deployment slots</span></span>
```PowerShell
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

### <a name="monitor-swap-events-in-the-activity-log"></a><span data-ttu-id="f676b-229">Monitor swap events in the Activity Log</span><span class="sxs-lookup"><span data-stu-id="f676b-229">Monitor swap events in the Activity Log</span></span>
```PowerShell
Get-AzureRmLog -ResourceGroup [resource group name] -StartTime 2018-03-07 -Caller SlotSwapJobProcessor  
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="f676b-230">Delete deployment slot</span><span class="sxs-lookup"><span data-stu-id="f676b-230">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="automate-with-azure-cli"></a><span data-ttu-id="f676b-231">Automate with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f676b-231">Automate with Azure CLI</span></span>

<span data-ttu-id="f676b-232">For [Azure CLI](https://github.com/Azure/azure-cli) commands for deployment slots, see [az webapp deployment slot](/cli/azure/webapp/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="f676b-232">For [Azure CLI](https://github.com/Azure/azure-cli) commands for deployment slots, see [az webapp deployment slot](/cli/azure/webapp/deployment/slot).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f676b-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="f676b-233">Next steps</span></span>
[<span data-ttu-id="f676b-234">Azure App Service Web App – block web access to non-production deployment slots</span><span class="sxs-lookup"><span data-stu-id="f676b-234">Azure App Service Web App – block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)  
[<span data-ttu-id="f676b-235">Introduction to App Service on Linux</span><span class="sxs-lookup"><span data-stu-id="f676b-235">Introduction to App Service on Linux</span></span>](../app-service/containers/app-service-linux-intro.md)  
[<span data-ttu-id="f676b-236">Microsoft Azure Free Trial</span><span class="sxs-lookup"><span data-stu-id="f676b-236">Microsoft Azure Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  ./media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: ./media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: ./media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: ./media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: ./media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: ./media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: ./media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: ./media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: ./media/web-sites-staged-publishing/SlotSetting.png

