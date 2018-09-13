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
ms.openlocfilehash: 8249f3e8f3cf753818f12b20eeead697878c8225
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549261"
---
# <a name="set-up-staging-environments-in-azure-app-service"></a><span data-ttu-id="ef050-103">Set up staging environments in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="ef050-103">Set up staging environments in Azure App Service</span></span>
<a name="Overview"></a>

<span data-ttu-id="ef050-104">When you deploy your web app, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span><span class="sxs-lookup"><span data-stu-id="ef050-104">When you deploy your web app, mobile back end, and API app to [App Service](http://go.microsoft.com/fwlink/?LinkId=529714), you can deploy to a separate deployment slot instead of the default production slot when running in the **Standard** or **Premium** App Service plan mode.</span></span> <span data-ttu-id="ef050-105">Deployment slots are actually live apps with their own hostnames.</span><span class="sxs-lookup"><span data-stu-id="ef050-105">Deployment slots are actually live apps with their own hostnames.</span></span> <span data-ttu-id="ef050-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-106">App content and configurations elements can be swapped between two deployment slots, including the production slot.</span></span> <span data-ttu-id="ef050-107">Deploying your application to a deployment slot has the following benefits:</span><span class="sxs-lookup"><span data-stu-id="ef050-107">Deploying your application to a deployment slot has the following benefits:</span></span>

* <span data-ttu-id="ef050-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-108">You can validate app changes in a staging deployment slot before swapping it with the production slot.</span></span>
* <span data-ttu-id="ef050-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span><span class="sxs-lookup"><span data-stu-id="ef050-109">Deploying an app to a slot first and swapping it into production ensures that all instances of the slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="ef050-110">This eliminates downtime when you deploy your app.</span><span class="sxs-lookup"><span data-stu-id="ef050-110">This eliminates downtime when you deploy your app.</span></span> <span data-ttu-id="ef050-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span><span class="sxs-lookup"><span data-stu-id="ef050-111">The traffic redirection is seamless, and no requests are dropped as a result of swap operations.</span></span> <span data-ttu-id="ef050-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span><span class="sxs-lookup"><span data-stu-id="ef050-112">This entire workflow can be automated by configuring [Auto Swap](#Auto-Swap) when pre-swap validation is not needed.</span></span>
* <span data-ttu-id="ef050-113">After a swap, the slot with previously staged app now has the previous production app.</span><span class="sxs-lookup"><span data-stu-id="ef050-113">After a swap, the slot with previously staged app now has the previous production app.</span></span> <span data-ttu-id="ef050-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span><span class="sxs-lookup"><span data-stu-id="ef050-114">If the changes swapped into the production slot are not as you expected, you can perform the same swap immediately to get your "last known good site" back.</span></span>

<span data-ttu-id="ef050-115">Each App Service plan mode supports a different number of deployment slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-115">Each App Service plan mode supports a different number of deployment slots.</span></span> <span data-ttu-id="ef050-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="ef050-116">To find out the number of slots your app's mode supports, see [App Service Pricing](https://azure.microsoft.com/pricing/details/app-service/).</span></span>

* <span data-ttu-id="ef050-117">When your app has multiple slots, you cannot change the mode.</span><span class="sxs-lookup"><span data-stu-id="ef050-117">When your app has multiple slots, you cannot change the mode.</span></span>
* <span data-ttu-id="ef050-118">Scaling is not available for non-production slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-118">Scaling is not available for non-production slots.</span></span>
* <span data-ttu-id="ef050-119">Linked resource management is not supported for non-production slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-119">Linked resource management is not supported for non-production slots.</span></span> <span data-ttu-id="ef050-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span><span class="sxs-lookup"><span data-stu-id="ef050-120">In the [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715) only, you can avoid this potential impact on a production slot by temporarily moving the non-production slot to a different App Service plan mode.</span></span> <span data-ttu-id="ef050-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-121">Note that the non-production slot must once again share the same mode with the production slot before you can swap the two slots.</span></span>

<a name="Add"></a>

## <a name="add-a-deployment-slot"></a><span data-ttu-id="ef050-122">Add a deployment slot</span><span class="sxs-lookup"><span data-stu-id="ef050-122">Add a deployment slot</span></span>
<span data-ttu-id="ef050-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-123">The app must be running in the **Standard** or **Premium** mode in order for you to enable multiple deployment slots.</span></span>

1. <span data-ttu-id="ef050-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span><span class="sxs-lookup"><span data-stu-id="ef050-124">In the [Azure Portal](https://portal.azure.com/), open your app's [resource blade](../azure-resource-manager/resource-group-portal.md#manage-resources).</span></span>
2. <span data-ttu-id="ef050-125">Choose the **Deployment slots** option, then click **Add Slot**.</span><span class="sxs-lookup"><span data-stu-id="ef050-125">Choose the **Deployment slots** option, then click **Add Slot**.</span></span>
   
    ![Add a new deployment slot][QGAddNewDeploymentSlot]
   
   > [!NOTE]
   > <span data-ttu-id="ef050-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span><span class="sxs-lookup"><span data-stu-id="ef050-127">If the app is not already in the **Standard** or **Premium** mode, you will receive a message indicating the supported modes for enabling staged publishing.</span></span> <span data-ttu-id="ef050-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span><span class="sxs-lookup"><span data-stu-id="ef050-128">At this point, you have the option to select **Upgrade** and navigate to the **Scale** tab of your app before continuing.</span></span>
   > 
   > 
3. <span data-ttu-id="ef050-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-129">In the **Add a slot** blade, give the slot a name, and select whether to clone app configuration from another existing deployment slot.</span></span> <span data-ttu-id="ef050-130">Click the check mark to continue.</span><span class="sxs-lookup"><span data-stu-id="ef050-130">Click the check mark to continue.</span></span>
   
    ![Configuration Source][ConfigurationSource1]
   
    <span data-ttu-id="ef050-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span><span class="sxs-lookup"><span data-stu-id="ef050-132">The first time you add a slot, you will only have two choices: clone configuration from the default slot in production or not at all.</span></span>
    <span data-ttu-id="ef050-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span><span class="sxs-lookup"><span data-stu-id="ef050-133">After you have created several slots, you will be able to clone configuration from a slot other than the one in production:</span></span>
   
    ![Configuration sources][MultipleConfigurationSources]
4. <span data-ttu-id="ef050-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span><span class="sxs-lookup"><span data-stu-id="ef050-135">In your app's resource blade, click  **Deployment slots**, then click a deployment slot to open that slot's resource blade, with a set of metrics and configuration just like any other app.</span></span> <span data-ttu-id="ef050-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-136">The name of the slot is shown at the top of the blade to remind you that you are viewing the deployment slot.</span></span>
   
    ![Deployment Slot Title][StagingTitle]
5. <span data-ttu-id="ef050-138">Click the app URL in the slot's blade.</span><span class="sxs-lookup"><span data-stu-id="ef050-138">Click the app URL in the slot's blade.</span></span> <span data-ttu-id="ef050-139">Notice the deployment slot has its own hostname and is also a live app.</span><span class="sxs-lookup"><span data-stu-id="ef050-139">Notice the deployment slot has its own hostname and is also a live app.</span></span> <span data-ttu-id="ef050-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span><span class="sxs-lookup"><span data-stu-id="ef050-140">To limit public access to the deployment slot, see [App Service Web App – block web access to non-production deployment slots](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/).</span></span>

<span data-ttu-id="ef050-141">There is no content after deployment slot creation.</span><span class="sxs-lookup"><span data-stu-id="ef050-141">There is no content after deployment slot creation.</span></span> <span data-ttu-id="ef050-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span><span class="sxs-lookup"><span data-stu-id="ef050-142">You can deploy to the slot from a different repository branch, or an altogether different repository.</span></span> <span data-ttu-id="ef050-143">You can also change the slot's configuration.</span><span class="sxs-lookup"><span data-stu-id="ef050-143">You can also change the slot's configuration.</span></span> <span data-ttu-id="ef050-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span><span class="sxs-lookup"><span data-stu-id="ef050-144">Use the publish profile or deployment credentials associated with the deployment slot for content updates.</span></span>  <span data-ttu-id="ef050-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span><span class="sxs-lookup"><span data-stu-id="ef050-145">For example, you can [publish to this slot with git](app-service-deploy-local-git.md).</span></span>

<a name="AboutConfiguration"></a>

## <a name="configuration-for-deployment-slots"></a><span data-ttu-id="ef050-146">Configuration for deployment slots</span><span class="sxs-lookup"><span data-stu-id="ef050-146">Configuration for deployment slots</span></span>
<span data-ttu-id="ef050-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span><span class="sxs-lookup"><span data-stu-id="ef050-147">When you clone configuration from another deployment slot, the cloned configuration is editable.</span></span> <span data-ttu-id="ef050-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span><span class="sxs-lookup"><span data-stu-id="ef050-148">Furthermore, some configuration elements will follow the content across a swap (not slot specific) while other configuration elements will stay in the same slot after a swap (slot specific).</span></span> <span data-ttu-id="ef050-149">The following lists show the configuration that will change when you swap slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-149">The following lists show the configuration that will change when you swap slots.</span></span>

<span data-ttu-id="ef050-150">**Settings that are swapped**:</span><span class="sxs-lookup"><span data-stu-id="ef050-150">**Settings that are swapped**:</span></span>

* <span data-ttu-id="ef050-151">General settings - such as framework version, 32/64-bit, Web sockets</span><span class="sxs-lookup"><span data-stu-id="ef050-151">General settings - such as framework version, 32/64-bit, Web sockets</span></span>
* <span data-ttu-id="ef050-152">App settings (can be configured to stick to a slot)</span><span class="sxs-lookup"><span data-stu-id="ef050-152">App settings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="ef050-153">Connection strings (can be configured to stick to a slot)</span><span class="sxs-lookup"><span data-stu-id="ef050-153">Connection strings (can be configured to stick to a slot)</span></span>
* <span data-ttu-id="ef050-154">Handler mappings</span><span class="sxs-lookup"><span data-stu-id="ef050-154">Handler mappings</span></span>
* <span data-ttu-id="ef050-155">Monitoring and diagnostic settings</span><span class="sxs-lookup"><span data-stu-id="ef050-155">Monitoring and diagnostic settings</span></span>
* <span data-ttu-id="ef050-156">WebJobs content</span><span class="sxs-lookup"><span data-stu-id="ef050-156">WebJobs content</span></span>

<span data-ttu-id="ef050-157">**Settings that are not swapped**:</span><span class="sxs-lookup"><span data-stu-id="ef050-157">**Settings that are not swapped**:</span></span>

* <span data-ttu-id="ef050-158">Publishing endpoints</span><span class="sxs-lookup"><span data-stu-id="ef050-158">Publishing endpoints</span></span>
* <span data-ttu-id="ef050-159">Custom Domain Names</span><span class="sxs-lookup"><span data-stu-id="ef050-159">Custom Domain Names</span></span>
* <span data-ttu-id="ef050-160">SSL certificates and bindings</span><span class="sxs-lookup"><span data-stu-id="ef050-160">SSL certificates and bindings</span></span>
* <span data-ttu-id="ef050-161">Scale settings</span><span class="sxs-lookup"><span data-stu-id="ef050-161">Scale settings</span></span>
* <span data-ttu-id="ef050-162">WebJobs schedulers</span><span class="sxs-lookup"><span data-stu-id="ef050-162">WebJobs schedulers</span></span>

<span data-ttu-id="ef050-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-163">To configure an app setting or connection string to stick to a slot (not swapped), access the **Application Settings** blade for a specific slot, then select the **Slot Setting** box for the configuration elements that should stick the slot.</span></span> <span data-ttu-id="ef050-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span><span class="sxs-lookup"><span data-stu-id="ef050-164">Note that marking a configuration element as slot specific has the effect of establishing that element as not swappable across all the deployment slots associated with the app.</span></span>

![Slot settings][SlotSettings]

<a name="Swap"></a>

## <a name="swap-deployment-slots"></a><span data-ttu-id="ef050-166">Swap deployment slots</span><span class="sxs-lookup"><span data-stu-id="ef050-166">Swap deployment slots</span></span> 
<span data-ttu-id="ef050-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span><span class="sxs-lookup"><span data-stu-id="ef050-167">You can swap deployment slots in the **Overview** or **Deployment slots** view of your app's resource blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef050-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span><span class="sxs-lookup"><span data-stu-id="ef050-168">Before you swap an app from a deployment slot into production, make sure that all non-slot specific settings are configured exactly as you want to have it in the swap target.</span></span>
> 
> 

1. <span data-ttu-id="ef050-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-169">To swap deployment slots, click the **Swap** button in the command bar of the app or in the command bar of a deployment slot.</span></span>
   
    ![Swap Button][SwapButtonBar]

2. <span data-ttu-id="ef050-171">Make sure that the swap source and swap target are set properly.</span><span class="sxs-lookup"><span data-stu-id="ef050-171">Make sure that the swap source and swap target are set properly.</span></span> <span data-ttu-id="ef050-172">Usually, the swap target is the production slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-172">Usually, the swap target is the production slot.</span></span> <span data-ttu-id="ef050-173">Click **OK** to complete the operation.</span><span class="sxs-lookup"><span data-stu-id="ef050-173">Click **OK** to complete the operation.</span></span> <span data-ttu-id="ef050-174">When the operation finishes, the deployment slots have been swapped.</span><span class="sxs-lookup"><span data-stu-id="ef050-174">When the operation finishes, the deployment slots have been swapped.</span></span>

    ![Complete swap](https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/SwapImmediately.png)

    <span data-ttu-id="ef050-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span><span class="sxs-lookup"><span data-stu-id="ef050-176">For the **Swap with preview** swap type, see [Swap with preview (multi-phase swap)](#Multi-Phase).</span></span>  

<a name="Multi-Phase"></a>

## <a name="swap-with-preview-multi-phase-swap"></a><span data-ttu-id="ef050-177">Swap with preview (multi-phase swap)</span><span class="sxs-lookup"><span data-stu-id="ef050-177">Swap with preview (multi-phase swap)</span></span>

<span data-ttu-id="ef050-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span><span class="sxs-lookup"><span data-stu-id="ef050-178">Swap with preview, or multi-phase swap, simplify validation of slot-specific configuration elements, such as connection strings.</span></span>
<span data-ttu-id="ef050-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span><span class="sxs-lookup"><span data-stu-id="ef050-179">For mission-critical workloads, you want to validate that the app behaves as expected when the production slot's configuration is applied, and you must perform such validation *before* the app is swapped into production.</span></span> <span data-ttu-id="ef050-180">Swap with preview is what you need.</span><span class="sxs-lookup"><span data-stu-id="ef050-180">Swap with preview is what you need.</span></span>

<span data-ttu-id="ef050-181">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span><span class="sxs-lookup"><span data-stu-id="ef050-181">When you use the **Swap with preview** option (see [Swap deployment slots](#Swap)), App Service does the following:</span></span>

- <span data-ttu-id="ef050-182">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span><span class="sxs-lookup"><span data-stu-id="ef050-182">Keeps the destination slot unchanged so existing workload on that slot (e.g. production) is not impacted.</span></span>
- <span data-ttu-id="ef050-183">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span><span class="sxs-lookup"><span data-stu-id="ef050-183">Applies the configuration elements of the destination slot to the source slot, including the slot-specific connection strings and app settings.</span></span>
- <span data-ttu-id="ef050-184">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span><span class="sxs-lookup"><span data-stu-id="ef050-184">Restarts the worker processes on the source slot using these aforementioned configuration elements.</span></span>
- <span data-ttu-id="ef050-185">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-185">When you complete the swap: Moves the pre-warmed-up source slot into the destination slot.</span></span> <span data-ttu-id="ef050-186">The destination slot is moved into the source slot as in a manual swap.</span><span class="sxs-lookup"><span data-stu-id="ef050-186">The destination slot is moved into the source slot as in a manual swap.</span></span>
- <span data-ttu-id="ef050-187">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-187">When you cancel the swap: Reapplies the configuration elements of the source slot to the source slot.</span></span>

<span data-ttu-id="ef050-188">You can preview exactly how the app will behave with the destination slot's configuration.</span><span class="sxs-lookup"><span data-stu-id="ef050-188">You can preview exactly how the app will behave with the destination slot's configuration.</span></span> <span data-ttu-id="ef050-189">Once you completes validation, you complete the swap in a separate step.</span><span class="sxs-lookup"><span data-stu-id="ef050-189">Once you completes validation, you complete the swap in a separate step.</span></span> <span data-ttu-id="ef050-190">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span><span class="sxs-lookup"><span data-stu-id="ef050-190">This step has the added advantage that the source slot is already warmed up with the desired configuration, and clients will not experience any downtime.</span></span>  

<span data-ttu-id="ef050-191">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span><span class="sxs-lookup"><span data-stu-id="ef050-191">Samples for the Azure PowerShell cmdlets available for multi-phase swap are included in the Azure PowerShell cmdlets for deployment slots section.</span></span>

<a name="Auto-Swap"></a>

## <a name="configure-auto-swap"></a><span data-ttu-id="ef050-192">Configure Auto Swap</span><span class="sxs-lookup"><span data-stu-id="ef050-192">Configure Auto Swap</span></span>
<span data-ttu-id="ef050-193">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span><span class="sxs-lookup"><span data-stu-id="ef050-193">Auto Swap streamlines DevOps scenarios where you want to continuously deploy your app with zero cold start and zero downtime for end customers of the app.</span></span> <span data-ttu-id="ef050-194">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-194">When a deployment slot is configured for Auto Swap into production, every time you push your code update to that slot, App Service will automatically swap the app into production after it has already warmed up in the slot.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef050-195">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span><span class="sxs-lookup"><span data-stu-id="ef050-195">When you enable Auto Swap for a slot, make sure the slot configuration is exactly the configuration intended for the target slot (usually the production slot).</span></span>
> 
> 

<span data-ttu-id="ef050-196">Configuring Auto Swap for a slot is easy.</span><span class="sxs-lookup"><span data-stu-id="ef050-196">Configuring Auto Swap for a slot is easy.</span></span> <span data-ttu-id="ef050-197">Follow the steps below:</span><span class="sxs-lookup"><span data-stu-id="ef050-197">Follow the steps below:</span></span>

1. <span data-ttu-id="ef050-198">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span><span class="sxs-lookup"><span data-stu-id="ef050-198">In **Deployment Slots**, select a non-production slot, and choose **Application Settings** in that slot's resource blade.</span></span>  
   
    ![][Autoswap1]
2. <span data-ttu-id="ef050-199">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="ef050-199">Select **On** for **Auto Swap**, select the desired target slot in **Auto Swap Slot**, and click **Save** in the command bar.</span></span> <span data-ttu-id="ef050-200">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-200">Make sure configuration for the slot is exactly the configuration intended for the target slot.</span></span>
   
    <span data-ttu-id="ef050-201">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span><span class="sxs-lookup"><span data-stu-id="ef050-201">The **Notifications** tab will flash a green **SUCCESS** once the operation is complete.</span></span>
   
    ![][Autoswap2]
   
   > [!NOTE]
   > <span data-ttu-id="ef050-202">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span><span class="sxs-lookup"><span data-stu-id="ef050-202">To test Auto Swap for your app, you can first select a non-production target slot in **Auto Swap Slot** to become familiar with the feature.</span></span>  
   > 
   > 
3. <span data-ttu-id="ef050-203">Execute a code push to that deployment slot.</span><span class="sxs-lookup"><span data-stu-id="ef050-203">Execute a code push to that deployment slot.</span></span> <span data-ttu-id="ef050-204">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span><span class="sxs-lookup"><span data-stu-id="ef050-204">Auto Swap will happen after a short time and the update will be reflected at your target slot's URL.</span></span>

<a name="Rollback"></a>

## <a name="to-rollback-a-production-app-after-swap"></a><span data-ttu-id="ef050-205">To rollback a production app after swap</span><span class="sxs-lookup"><span data-stu-id="ef050-205">To rollback a production app after swap</span></span>
<span data-ttu-id="ef050-206">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span><span class="sxs-lookup"><span data-stu-id="ef050-206">If any errors are identified in production after a slot swap, roll the slots back to their pre-swap states by swapping the same two slots immediately.</span></span>

<a name="Warm-up"></a>

## <a name="custom-warm-up-before-swap"></a><span data-ttu-id="ef050-207">Custom warm-up before swap</span><span class="sxs-lookup"><span data-stu-id="ef050-207">Custom warm-up before swap</span></span>
<span data-ttu-id="ef050-208">Some apps may require custom warm-up actions.</span><span class="sxs-lookup"><span data-stu-id="ef050-208">Some apps may require custom warm-up actions.</span></span> <span data-ttu-id="ef050-209">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span><span class="sxs-lookup"><span data-stu-id="ef050-209">The `applicationInitialization` configuration element in web.config allows you to specify custom initialization actions to be performed before a request is received.</span></span> <span data-ttu-id="ef050-210">The swap operation will wait for this custom warm-up to complete.</span><span class="sxs-lookup"><span data-stu-id="ef050-210">The swap operation will wait for this custom warm-up to complete.</span></span> <span data-ttu-id="ef050-211">Here is a sample web.config fragment.</span><span class="sxs-lookup"><span data-stu-id="ef050-211">Here is a sample web.config fragment.</span></span>

    <applicationInitialization>
        <add initializationPage="/" hostName="[app hostname]" />
        <add initializationPage="/Home/About" hostname="[app hostname]" />
    </applicationInitialization>

<a name="Delete"></a>

## <a name="to-delete-a-deployment-slot"></a><span data-ttu-id="ef050-212">To delete a deployment slot</span><span class="sxs-lookup"><span data-stu-id="ef050-212">To delete a deployment slot</span></span>
<span data-ttu-id="ef050-213">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span><span class="sxs-lookup"><span data-stu-id="ef050-213">In the blade for a deployment slot, open the deployment slot's blade, click **Overview** (the default page), and click **Delete** in the command bar.</span></span>  

![Delete a Deployment Slot][DeleteStagingSiteButton]

<!-- ======== AZURE POWERSHELL CMDLETS =========== -->

<a name="PowerShell"></a>

## <a name="azure-powershell-cmdlets-for-deployment-slots"></a><span data-ttu-id="ef050-215">Azure PowerShell cmdlets for deployment slots</span><span class="sxs-lookup"><span data-stu-id="ef050-215">Azure PowerShell cmdlets for deployment slots</span></span>
<span data-ttu-id="ef050-216">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="ef050-216">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell, including support for managing deployment slots in Azure App Service.</span></span>

* <span data-ttu-id="ef050-217">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="ef050-217">For information on installing and configuring Azure PowerShell, and on authenticating Azure PowerShell with your Azure subscription, see [How to install and configure Microsoft Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>  

- - -
### <a name="create-a-web-app"></a><span data-ttu-id="ef050-218">Create a web app</span><span class="sxs-lookup"><span data-stu-id="ef050-218">Create a web app</span></span>
```
New-AzureRmWebApp -ResourceGroupName [resource group name] -Name [app name] -Location [location] -AppServicePlan [app service plan name]
```

- - -
### <a name="create-a-deployment-slot"></a><span data-ttu-id="ef050-219">Create a deployment slot</span><span class="sxs-lookup"><span data-stu-id="ef050-219">Create a deployment slot</span></span>
```
New-AzureRmWebAppSlot -ResourceGroupName [resource group name] -Name [app name] -Slot [deployment slot name] -AppServicePlan [app service plan name]
```

- - -
### <a name="initiate-a-swap-with-review-multi-phase-swap-and-apply-destination-slot-configuration-to-source-slot"></a><span data-ttu-id="ef050-220">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span><span class="sxs-lookup"><span data-stu-id="ef050-220">Initiate a swap with review (multi-phase swap) and apply destination slot configuration to source slot</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action applySlotConfig -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="cancel-a-pending-swap-swap-with-review-and-restore-source-slot-configuration"></a><span data-ttu-id="ef050-221">Cancel a pending swap (swap with review) and restore source slot configuration</span><span class="sxs-lookup"><span data-stu-id="ef050-221">Cancel a pending swap (swap with review) and restore source slot configuration</span></span>
```
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action resetSlotConfig -ApiVersion 2015-07-01
```

- - -
### <a name="swap-deployment-slots"></a><span data-ttu-id="ef050-222">Swap deployment slots</span><span class="sxs-lookup"><span data-stu-id="ef050-222">Swap deployment slots</span></span>
```
$ParametersObject = @{targetSlot  = "[slot name – e.g. “production”]"}
Invoke-AzureRmResourceAction -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots -ResourceName [app name]/[slot name] -Action slotsswap -Parameters $ParametersObject -ApiVersion 2015-07-01
```

- - -
### <a name="delete-deployment-slot"></a><span data-ttu-id="ef050-223">Delete deployment slot</span><span class="sxs-lookup"><span data-stu-id="ef050-223">Delete deployment slot</span></span>
```
Remove-AzureRmResource -ResourceGroupName [resource group name] -ResourceType Microsoft.Web/sites/slots –Name [app name]/[slot name] -ApiVersion 2015-07-01
```

- - -
<!-- ======== Azure CLI =========== -->

<a name="CLI"></a>

## <a name="azure-command-line-interface-azure-cli-commands-for-deployment-slots"></a><span data-ttu-id="ef050-224">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span><span class="sxs-lookup"><span data-stu-id="ef050-224">Azure Command-Line Interface (Azure CLI) commands for Deployment Slots</span></span>
<span data-ttu-id="ef050-225">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span><span class="sxs-lookup"><span data-stu-id="ef050-225">The Azure CLI provides cross-platform commands for working with Azure, including support for managing App Service deployment slots.</span></span>

* <span data-ttu-id="ef050-226">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="ef050-226">For instructions on installing and configuring the Azure CLI, including information on how to connect Azure CLI to your Azure subscription, see [Install and Configure the Azure CLI](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="ef050-227">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span><span class="sxs-lookup"><span data-stu-id="ef050-227">To list the commands available for Azure App Service in the Azure CLI, call `azure site -h`.</span></span>

> [!NOTE] 
> <span data-ttu-id="ef050-228">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span><span class="sxs-lookup"><span data-stu-id="ef050-228">For [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands for deployment slots, see [az appservice web deployment slot](/cli/azure/appservice/web/deployment/slot).</span></span>

- - -
### <a name="azure-site-list"></a><span data-ttu-id="ef050-229">azure site list</span><span class="sxs-lookup"><span data-stu-id="ef050-229">azure site list</span></span>
<span data-ttu-id="ef050-230">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="ef050-230">For information about the apps in the current subscription, call **azure site list**, as in the following example.</span></span>

`azure site list webappslotstest`

- - -
### <a name="azure-site-create"></a><span data-ttu-id="ef050-231">azure site create</span><span class="sxs-lookup"><span data-stu-id="ef050-231">azure site create</span></span>
<span data-ttu-id="ef050-232">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="ef050-232">To create a deployment slot, call **azure site create** and specify the name of an existing app and the name of the slot to create, as in the following example.</span></span>

`azure site create webappslotstest --slot staging`

<span data-ttu-id="ef050-233">To enable source control for the new slot, use the **--git** option, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="ef050-233">To enable source control for the new slot, use the **--git** option, as in the following example.</span></span>

`azure site create --git webappslotstest --slot staging`

- - -
### <a name="azure-site-swap"></a><span data-ttu-id="ef050-234">azure site swap</span><span class="sxs-lookup"><span data-stu-id="ef050-234">azure site swap</span></span>
<span data-ttu-id="ef050-235">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="ef050-235">To make the updated deployment slot the production app, use the **azure site swap** command to perform a swap operation, as in the following example.</span></span> <span data-ttu-id="ef050-236">The production app will not experience any down time, nor will it undergo a cold start.</span><span class="sxs-lookup"><span data-stu-id="ef050-236">The production app will not experience any down time, nor will it undergo a cold start.</span></span>

`azure site swap webappslotstest`

- - -
### <a name="azure-site-delete"></a><span data-ttu-id="ef050-237">azure site delete</span><span class="sxs-lookup"><span data-stu-id="ef050-237">azure site delete</span></span>
<span data-ttu-id="ef050-238">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span><span class="sxs-lookup"><span data-stu-id="ef050-238">To delete a deployment slot that is no longer needed, use the **azure site delete** command, as in the following example.</span></span>

`azure site delete webappslotstest --slot staging`

- - -
> [!NOTE]
> <span data-ttu-id="ef050-239">See a web app in action.</span><span class="sxs-lookup"><span data-stu-id="ef050-239">See a web app in action.</span></span> <span data-ttu-id="ef050-240">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span><span class="sxs-lookup"><span data-stu-id="ef050-240">[Try App Service](https://azure.microsoft.com/try/app-service/) immediately and create a short-lived starter app—no credit card required, no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="ef050-241">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ef050-241">Next Steps</span></span>
[<span data-ttu-id="ef050-242">Azure App Service Web App – block web access to non-production deployment slots</span><span class="sxs-lookup"><span data-stu-id="ef050-242">Azure App Service Web App – block web access to non-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)

[<span data-ttu-id="ef050-243">Microsoft Azure Free Trial</span><span class="sxs-lookup"><span data-stu-id="ef050-243">Microsoft Azure Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

<!-- IMAGES -->
[QGAddNewDeploymentSlot]:  https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/QGAddNewDeploymentSlot.png
[AddNewDeploymentSlotDialog]: ./media/web-sites-staged-publishing/AddNewDeploymentSlotDialog.png
[ConfigurationSource1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/ConfigurationSource1.png
[MultipleConfigurationSources]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/MultipleConfigurationSources.png
[SiteListWithStagedSite]: ./media/web-sites-staged-publishing/SiteListWithStagedSite.png
[StagingTitle]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/StagingTitle.png
[SwapButtonBar]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/SwapButtonBar.png
[SwapConfirmationDialog]:  ./media/web-sites-staged-publishing/SwapConfirmationDialog.png
[DeleteStagingSiteButton]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/DeleteStagingSiteButton.png
[SwapDeploymentsDialog]: ./media/web-sites-staged-publishing/SwapDeploymentsDialog.png
[Autoswap1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/AutoSwap01.png
[Autoswap2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/AutoSwap02.png
[SlotSettings]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-web/media/web-sites-staged-publishing/SlotSetting.png











