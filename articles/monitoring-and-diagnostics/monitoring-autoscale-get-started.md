---
title: Get started with autoscale in Azure
description: Learn how to scale your resource Web App, Cloud Service, Virtual Machine or Virtual Machine Scale set in Azure.
author: rajram
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 07/07/2017
ms.author: rajram
ms.component: autoscale
ms.openlocfilehash: b303632c236e492bbf57ee60d5e7b0cc7b2f9e5c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855725"
---
# <a name="get-started-with-autoscale-in-azure"></a><span data-ttu-id="c8d20-103">Get started with Autoscale in Azure</span><span class="sxs-lookup"><span data-stu-id="c8d20-103">Get started with Autoscale in Azure</span></span>
<span data-ttu-id="c8d20-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c8d20-104">This article describes how to set up your Autoscale settings for your resource in the Microsoft Azure portal.</span></span>

<span data-ttu-id="c8d20-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span><span class="sxs-lookup"><span data-stu-id="c8d20-105">Azure Monitor Autoscale applies only to virtual machine scale sets, cloud services, Azure App Service plans, and App Service environments.</span></span> 

## <a name="discover-the-autoscale-settings-in-your-subscription"></a><span data-ttu-id="c8d20-106">Discover the Autoscale settings in your subscription</span><span class="sxs-lookup"><span data-stu-id="c8d20-106">Discover the Autoscale settings in your subscription</span></span>
<span data-ttu-id="c8d20-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="c8d20-107">You can discover all the resources for which Autoscale is applicable in Azure Monitor.</span></span> <span data-ttu-id="c8d20-108">Use the following steps for a step-by-step walkthrough:</span><span class="sxs-lookup"><span data-stu-id="c8d20-108">Use the following steps for a step-by-step walkthrough:</span></span>

1. <span data-ttu-id="c8d20-109">Open the [Azure portal.][1]</span><span class="sxs-lookup"><span data-stu-id="c8d20-109">Open the [Azure portal.][1]</span></span>
1. <span data-ttu-id="c8d20-110">Click the Azure Monitor icon in the left pane.</span><span class="sxs-lookup"><span data-stu-id="c8d20-110">Click the Azure Monitor icon in the left pane.</span></span>
  <span data-ttu-id="c8d20-111">![Open Azure Monitor][2]</span><span class="sxs-lookup"><span data-stu-id="c8d20-111">![Open Azure Monitor][2]</span></span>
1. <span data-ttu-id="c8d20-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span><span class="sxs-lookup"><span data-stu-id="c8d20-112">Click **Autoscale** to view all the resources for which Autoscale is applicable, along with their current Autoscale status.</span></span>
  <span data-ttu-id="c8d20-113">![Discover Autoscale in Azure Monitor][3]</span><span class="sxs-lookup"><span data-stu-id="c8d20-113">![Discover Autoscale in Azure Monitor][3]</span></span>

<span data-ttu-id="c8d20-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-114">You can use the filter pane at the top to scope down the list to select resources in a specific resource group, specific resource types, or a specific resource.</span></span>

<span data-ttu-id="c8d20-115">For each resource, you will find the current instance count and the Autoscale status.</span><span class="sxs-lookup"><span data-stu-id="c8d20-115">For each resource, you will find the current instance count and the Autoscale status.</span></span> <span data-ttu-id="c8d20-116">The Autoscale status can be:</span><span class="sxs-lookup"><span data-stu-id="c8d20-116">The Autoscale status can be:</span></span>

- <span data-ttu-id="c8d20-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-117">**Not configured**: You have not enabled Autoscale yet for this resource.</span></span>
- <span data-ttu-id="c8d20-118">**Enabled**: You have enabled Autoscale for this resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-118">**Enabled**: You have enabled Autoscale for this resource.</span></span>
- <span data-ttu-id="c8d20-119">**Disabled**: You have disabled Autoscale for this resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-119">**Disabled**: You have disabled Autoscale for this resource.</span></span>

## <a name="create-your-first-autoscale-setting"></a><span data-ttu-id="c8d20-120">Create your first Autoscale setting</span><span class="sxs-lookup"><span data-stu-id="c8d20-120">Create your first Autoscale setting</span></span>

<span data-ttu-id="c8d20-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="c8d20-121">Let's now go through a simple step-by-step walkthrough to create your first Autoscale setting.</span></span>

1. <span data-ttu-id="c8d20-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span><span class="sxs-lookup"><span data-stu-id="c8d20-122">Open the **Autoscale** blade in Azure Monitor and select a resource that you want to scale.</span></span> <span data-ttu-id="c8d20-123">(The following steps use an App Service plan associated with a web app.</span><span class="sxs-lookup"><span data-stu-id="c8d20-123">(The following steps use an App Service plan associated with a web app.</span></span> <span data-ttu-id="c8d20-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span><span class="sxs-lookup"><span data-stu-id="c8d20-124">You can [create your first ASP.NET web app in Azure in 5 minutes.][4])</span></span>
1. <span data-ttu-id="c8d20-125">Note that the current instance count is 1.</span><span class="sxs-lookup"><span data-stu-id="c8d20-125">Note that the current instance count is 1.</span></span> <span data-ttu-id="c8d20-126">Click **Enable autoscale**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-126">Click **Enable autoscale**.</span></span>
  <span data-ttu-id="c8d20-127">![Scale setting for new web app][5]</span><span class="sxs-lookup"><span data-stu-id="c8d20-127">![Scale setting for new web app][5]</span></span>
1. <span data-ttu-id="c8d20-128">Provide a name for the scale setting, and then click **Add a rule**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-128">Provide a name for the scale setting, and then click **Add a rule**.</span></span> <span data-ttu-id="c8d20-129">Notice the scale rule options that open as a context pane on the right side.</span><span class="sxs-lookup"><span data-stu-id="c8d20-129">Notice the scale rule options that open as a context pane on the right side.</span></span> <span data-ttu-id="c8d20-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span><span class="sxs-lookup"><span data-stu-id="c8d20-130">By default, this sets the option to scale your instance count by 1 if the CPU percentage of the resource exceeds 70 percent.</span></span> <span data-ttu-id="c8d20-131">Leave it at its default values and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-131">Leave it at its default values and click **Add**.</span></span>
  <span data-ttu-id="c8d20-132">![Create scale setting for a web app][6]</span><span class="sxs-lookup"><span data-stu-id="c8d20-132">![Create scale setting for a web app][6]</span></span>
1. <span data-ttu-id="c8d20-133">You've now created your first scale rule.</span><span class="sxs-lookup"><span data-stu-id="c8d20-133">You've now created your first scale rule.</span></span> <span data-ttu-id="c8d20-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span><span class="sxs-lookup"><span data-stu-id="c8d20-134">Note that the UX recommends best practices and states that "It is recommended to have at least one scale in rule."</span></span> <span data-ttu-id="c8d20-135">To do so:</span><span class="sxs-lookup"><span data-stu-id="c8d20-135">To do so:</span></span>
  
    <span data-ttu-id="c8d20-136">a.</span><span class="sxs-lookup"><span data-stu-id="c8d20-136">a.</span></span> <span data-ttu-id="c8d20-137">Click **Add a rule**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-137">Click **Add a rule**.</span></span> 

    <span data-ttu-id="c8d20-138">b.</span><span class="sxs-lookup"><span data-stu-id="c8d20-138">b.</span></span> <span data-ttu-id="c8d20-139">Set **Operator** to **Less than**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-139">Set **Operator** to **Less than**.</span></span>

    <span data-ttu-id="c8d20-140">c.</span><span class="sxs-lookup"><span data-stu-id="c8d20-140">c.</span></span> <span data-ttu-id="c8d20-141">Set **Threshold** to **20**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-141">Set **Threshold** to **20**.</span></span>

    <span data-ttu-id="c8d20-142">d.</span><span class="sxs-lookup"><span data-stu-id="c8d20-142">d.</span></span> <span data-ttu-id="c8d20-143">Set **Operation** to **Decrease count by**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-143">Set **Operation** to **Decrease count by**.</span></span>

   <span data-ttu-id="c8d20-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span><span class="sxs-lookup"><span data-stu-id="c8d20-144">You should now have a scale setting that scales out/scales in based on CPU usage.</span></span>
   <span data-ttu-id="c8d20-145">![Scale based on CPU][8]</span><span class="sxs-lookup"><span data-stu-id="c8d20-145">![Scale based on CPU][8]</span></span>
1. <span data-ttu-id="c8d20-146">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-146">Click **Save**.</span></span>

<span data-ttu-id="c8d20-147">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="c8d20-147">Congratulations!</span></span> <span data-ttu-id="c8d20-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span><span class="sxs-lookup"><span data-stu-id="c8d20-148">You've now successfully created your first scale setting to autoscale your web app based on CPU usage.</span></span>

> [!NOTE] 
> <span data-ttu-id="c8d20-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span><span class="sxs-lookup"><span data-stu-id="c8d20-149">The same steps are applicable to get started with a virtual machine scale set or cloud service role.</span></span>

## <a name="other-considerations"></a><span data-ttu-id="c8d20-150">Other considerations</span><span class="sxs-lookup"><span data-stu-id="c8d20-150">Other considerations</span></span>
### <a name="scale-based-on-a-schedule"></a><span data-ttu-id="c8d20-151">Scale based on a schedule</span><span class="sxs-lookup"><span data-stu-id="c8d20-151">Scale based on a schedule</span></span>
<span data-ttu-id="c8d20-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span><span class="sxs-lookup"><span data-stu-id="c8d20-152">In addition to scale based on CPU, you can set your scale differently for specific days of the week.</span></span>

1. <span data-ttu-id="c8d20-153">Click **Add a scale condition**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-153">Click **Add a scale condition**.</span></span>
1. <span data-ttu-id="c8d20-154">Setting the scale mode and the rules is the same as the default condition.</span><span class="sxs-lookup"><span data-stu-id="c8d20-154">Setting the scale mode and the rules is the same as the default condition.</span></span>
1. <span data-ttu-id="c8d20-155">Select **Repeat specific days** for the schedule.</span><span class="sxs-lookup"><span data-stu-id="c8d20-155">Select **Repeat specific days** for the schedule.</span></span>
1. <span data-ttu-id="c8d20-156">Select the days and the start/end time for when the scale condition should be applied.</span><span class="sxs-lookup"><span data-stu-id="c8d20-156">Select the days and the start/end time for when the scale condition should be applied.</span></span>

![Scale condition based on schedule][9]
### <a name="scale-differently-on-specific-dates"></a><span data-ttu-id="c8d20-158">Scale differently on specific dates</span><span class="sxs-lookup"><span data-stu-id="c8d20-158">Scale differently on specific dates</span></span>
<span data-ttu-id="c8d20-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span><span class="sxs-lookup"><span data-stu-id="c8d20-159">In addition to scale based on CPU, you can set your scale differently for specific dates.</span></span>

1. <span data-ttu-id="c8d20-160">Click **Add a scale condition**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-160">Click **Add a scale condition**.</span></span>
1. <span data-ttu-id="c8d20-161">Setting the scale mode and the rules is the same as the default condition.</span><span class="sxs-lookup"><span data-stu-id="c8d20-161">Setting the scale mode and the rules is the same as the default condition.</span></span>
1. <span data-ttu-id="c8d20-162">Select **Specify start/end dates** for the schedule.</span><span class="sxs-lookup"><span data-stu-id="c8d20-162">Select **Specify start/end dates** for the schedule.</span></span>
1. <span data-ttu-id="c8d20-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span><span class="sxs-lookup"><span data-stu-id="c8d20-163">Select the start/end dates and the start/end time for when the scale condition should be applied.</span></span>

![Scale condition based on dates][10]

### <a name="view-the-scale-history-of-your-resource"></a><span data-ttu-id="c8d20-165">View the scale history of your resource</span><span class="sxs-lookup"><span data-stu-id="c8d20-165">View the scale history of your resource</span></span>
<span data-ttu-id="c8d20-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span><span class="sxs-lookup"><span data-stu-id="c8d20-166">Whenever your resource is scaled up or down, an event is logged in the activity log.</span></span> <span data-ttu-id="c8d20-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span><span class="sxs-lookup"><span data-stu-id="c8d20-167">You can view the scale history of your resource for the past 24 hours by switching to the **Run history** tab.</span></span>

![Run history][11]

<span data-ttu-id="c8d20-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-169">If you want to view the complete scale history (for up to 90 days), select **Click here to see more details**.</span></span> <span data-ttu-id="c8d20-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span><span class="sxs-lookup"><span data-stu-id="c8d20-170">The activity log opens, with Autoscale pre-selected for your resource and category.</span></span>

### <a name="view-the-scale-definition-of-your-resource"></a><span data-ttu-id="c8d20-171">View the scale definition of your resource</span><span class="sxs-lookup"><span data-stu-id="c8d20-171">View the scale definition of your resource</span></span>
<span data-ttu-id="c8d20-172">Autoscale is an Azure Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-172">Autoscale is an Azure Resource Manager resource.</span></span> <span data-ttu-id="c8d20-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span><span class="sxs-lookup"><span data-stu-id="c8d20-173">You can view the scale definition in JSON by switching to the **JSON** tab.</span></span>

![Scale definition][12]

<span data-ttu-id="c8d20-175">You can make changes in JSON directly, if required.</span><span class="sxs-lookup"><span data-stu-id="c8d20-175">You can make changes in JSON directly, if required.</span></span> <span data-ttu-id="c8d20-176">These changes will be reflected after you save them.</span><span class="sxs-lookup"><span data-stu-id="c8d20-176">These changes will be reflected after you save them.</span></span>

### <a name="disable-autoscale-and-manually-scale-your-instances"></a><span data-ttu-id="c8d20-177">Disable Autoscale and manually scale your instances</span><span class="sxs-lookup"><span data-stu-id="c8d20-177">Disable Autoscale and manually scale your instances</span></span>
<span data-ttu-id="c8d20-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span><span class="sxs-lookup"><span data-stu-id="c8d20-178">There might be times when you want to disable your current scale setting and manually scale your resource.</span></span>

<span data-ttu-id="c8d20-179">Click the **Disable autoscale** button at the top.</span><span class="sxs-lookup"><span data-stu-id="c8d20-179">Click the **Disable autoscale** button at the top.</span></span>
<span data-ttu-id="c8d20-180">![Disable Autoscale][13]</span><span class="sxs-lookup"><span data-stu-id="c8d20-180">![Disable Autoscale][13]</span></span>

> [!NOTE] 
> <span data-ttu-id="c8d20-181">This option disables your configuration.</span><span class="sxs-lookup"><span data-stu-id="c8d20-181">This option disables your configuration.</span></span> <span data-ttu-id="c8d20-182">However, you can get back to it after you enable Autoscale again.</span><span class="sxs-lookup"><span data-stu-id="c8d20-182">However, you can get back to it after you enable Autoscale again.</span></span> 

<span data-ttu-id="c8d20-183">You can now set the number of instances that you want to scale to manually.</span><span class="sxs-lookup"><span data-stu-id="c8d20-183">You can now set the number of instances that you want to scale to manually.</span></span>

![Set manual scale][14]

<span data-ttu-id="c8d20-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span><span class="sxs-lookup"><span data-stu-id="c8d20-185">You can always return to Autoscale by clicking **Enable autoscale** and then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8d20-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8d20-186">Next steps</span></span>
- [<span data-ttu-id="c8d20-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span><span class="sxs-lookup"><span data-stu-id="c8d20-187">Create an Activity Log Alert to monitor all Autoscale engine operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert)
- [<span data-ttu-id="c8d20-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span><span class="sxs-lookup"><span data-stu-id="c8d20-188">Create an Activity Log Alert to monitor all failed Autoscale scale-in/scale-out operations on your subscription</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert)

<!--Reference-->
[1]:https://portal.azure.com
[2]: ./media/monitoring-autoscale-get-started/azure-monitor-launch.png
[3]: ./media/monitoring-autoscale-get-started/discover-autoscale-azure-monitor.png
[4]: https://docs.microsoft.com/azure/app-service/app-service-web-get-started-dotnet
[5]: ./media/monitoring-autoscale-get-started/scale-setting-new-web-app.png
[6]: ./media/monitoring-autoscale-get-started/create-scale-setting-web-app.png
[7]: ./media/monitoring-autoscale-get-started/scale-in-recommendation.png
[8]: ./media/monitoring-autoscale-get-started/scale-based-on-cpu.png
[9]: ./media/monitoring-autoscale-get-started/scale-condition-schedule.png
[10]: ./media/monitoring-autoscale-get-started/scale-condition-dates.png
[11]: ./media/monitoring-autoscale-get-started/scale-history.png
[12]: ./media/monitoring-autoscale-get-started/scale-definition-json.png
[13]: ./media/monitoring-autoscale-get-started/disable-autoscale.png
[14]: ./media/monitoring-autoscale-get-started/set-manualscale.png

