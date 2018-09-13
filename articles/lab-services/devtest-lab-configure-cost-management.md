---
title: View the monthly estimated lab cost trend in Azure DevTest Labs | Microsoft Docs
description: Learn about the Azure DevTest Labs monthly estimated cost trend chart.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
editor: ''
ms.assetid: 1f46fdc5-d917-46e3-a1ea-f6dd41212ba4
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/05/2018
ms.author: spelluru
ms.openlocfilehash: 13535dae82ef2c8896dad7d6221553d15e4e6a95
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865438"
---
# <a name="view-the-monthly-estimated-lab-cost-trend-in-azure-devtest-labs"></a><span data-ttu-id="82cfb-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82cfb-103">View the monthly estimated lab cost trend in Azure DevTest Labs</span></span>
<span data-ttu-id="82cfb-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span><span class="sxs-lookup"><span data-stu-id="82cfb-104">The Cost Management feature of DevTest Labs helps you track the cost of your lab.</span></span> <span data-ttu-id="82cfb-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span><span class="sxs-lookup"><span data-stu-id="82cfb-105">This article illustrates how to use the **Monthly Estimated Cost Trend** chart to view the current calendar month's estimated cost-to-date and the projected end-of-month cost for the current calendar month.</span></span> <span data-ttu-id="82cfb-106">This article also shows you how to better manage lab costs by setting spending targets and thresholds that, when reached, trigger DevTest Labs to report the results to you.</span><span class="sxs-lookup"><span data-stu-id="82cfb-106">This article also shows you how to better manage lab costs by setting spending targets and thresholds that, when reached, trigger DevTest Labs to report the results to you.</span></span>

## <a name="viewing-the-monthly-estimated-cost-trend-chart"></a><span data-ttu-id="82cfb-107">Viewing the Monthly Estimated Cost Trend chart</span><span class="sxs-lookup"><span data-stu-id="82cfb-107">Viewing the Monthly Estimated Cost Trend chart</span></span>
<span data-ttu-id="82cfb-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="82cfb-108">To view the Monthly Estimated Cost Trend chart, follow these steps:</span></span> 

1. <span data-ttu-id="82cfb-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="82cfb-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>
1. <span data-ttu-id="82cfb-110">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span><span class="sxs-lookup"><span data-stu-id="82cfb-110">If necessary, select **All Services**, and then select **DevTest Labs** from the list.</span></span> <span data-ttu-id="82cfb-111">(Your lab might already be shown on the Dashboard under **All Resources**).</span><span class="sxs-lookup"><span data-stu-id="82cfb-111">(Your lab might already be shown on the Dashboard under **All Resources**).</span></span>
1. <span data-ttu-id="82cfb-112">From the list of labs, select the desired lab.</span><span class="sxs-lookup"><span data-stu-id="82cfb-112">From the list of labs, select the desired lab.</span></span>  
1. <span data-ttu-id="82cfb-113">On the lab's **Overview** area, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-113">On the lab's **Overview** area, select **Configuration and policies**.</span></span>   
1. <span data-ttu-id="82cfb-114">On the left under **COST TRACKING**, select **Cost trend**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-114">On the left under **COST TRACKING**, select **Cost trend**.</span></span>

   <span data-ttu-id="82cfb-115">The following screen shot shows an example of a cost chart.</span><span class="sxs-lookup"><span data-stu-id="82cfb-115">The following screen shot shows an example of a cost chart.</span></span> 
   
    ![Cost chart](./media/devtest-lab-configure-cost-management/graph.png)

<span data-ttu-id="82cfb-117">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span><span class="sxs-lookup"><span data-stu-id="82cfb-117">The **Estimated cost** value is the current calendar month's estimated cost-to-date.</span></span> <span data-ttu-id="82cfb-118">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span><span class="sxs-lookup"><span data-stu-id="82cfb-118">The **Projected cost** is the estimated cost for the entire current calendar month, calculated using the lab cost for the previous five days.</span></span>

<span data-ttu-id="82cfb-119">The cost amounts are rounded up to the next whole number.</span><span class="sxs-lookup"><span data-stu-id="82cfb-119">The cost amounts are rounded up to the next whole number.</span></span> <span data-ttu-id="82cfb-120">For example:</span><span class="sxs-lookup"><span data-stu-id="82cfb-120">For example:</span></span> 

* <span data-ttu-id="82cfb-121">5.01 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="82cfb-121">5.01 rounds up to 6</span></span> 
* <span data-ttu-id="82cfb-122">5.50 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="82cfb-122">5.50 rounds up to 6</span></span>
* <span data-ttu-id="82cfb-123">5.99 rounds up to 6</span><span class="sxs-lookup"><span data-stu-id="82cfb-123">5.99 rounds up to 6</span></span>

<span data-ttu-id="82cfb-124">As it states above the chart, the costs you see by default in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span><span class="sxs-lookup"><span data-stu-id="82cfb-124">As it states above the chart, the costs you see by default in the chart are *estimated* costs using [Pay-As-You-Go](https://azure.microsoft.com/offers/ms-azr-0003p/) offer rates.</span></span> <span data-ttu-id="82cfb-125">You can also set your own spending targets that are displayed in the charts by [managing the cost targets for your lab.](#managing-cost-targets-for-your-lab)</span><span class="sxs-lookup"><span data-stu-id="82cfb-125">You can also set your own spending targets that are displayed in the charts by [managing the cost targets for your lab.](#managing-cost-targets-for-your-lab)</span></span>

<span data-ttu-id="82cfb-126">Additionally, the following are *not* included in the cost calculation:</span><span class="sxs-lookup"><span data-stu-id="82cfb-126">Additionally, the following are *not* included in the cost calculation:</span></span>

* <span data-ttu-id="82cfb-127">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span><span class="sxs-lookup"><span data-stu-id="82cfb-127">CSP and Dreamspark subscriptions are currently not supported as Azure DevTest Labs uses the [Azure billing APIs](../billing/billing-usage-rate-card-overview.md) to calculate the lab cost, which does not support CSP or Dreamspark subscriptions.</span></span>
* <span data-ttu-id="82cfb-128">Your offer rates.</span><span class="sxs-lookup"><span data-stu-id="82cfb-128">Your offer rates.</span></span> <span data-ttu-id="82cfb-129">Currently, you can't use the offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span><span class="sxs-lookup"><span data-stu-id="82cfb-129">Currently, you can't use the offer rates (shown under your subscription) that you have negotiated with Microsoft or Microsoft partners.</span></span> <span data-ttu-id="82cfb-130">Only Pay-As-You-Go rates are used.</span><span class="sxs-lookup"><span data-stu-id="82cfb-130">Only Pay-As-You-Go rates are used.</span></span>
* <span data-ttu-id="82cfb-131">Your taxes</span><span class="sxs-lookup"><span data-stu-id="82cfb-131">Your taxes</span></span>
* <span data-ttu-id="82cfb-132">Your discounts</span><span class="sxs-lookup"><span data-stu-id="82cfb-132">Your discounts</span></span>
* <span data-ttu-id="82cfb-133">Your billing currency.</span><span class="sxs-lookup"><span data-stu-id="82cfb-133">Your billing currency.</span></span> <span data-ttu-id="82cfb-134">Currently, the lab cost is displayed only in USD currency.</span><span class="sxs-lookup"><span data-stu-id="82cfb-134">Currently, the lab cost is displayed only in USD currency.</span></span>

## <a name="managing-cost-targets-for-your-lab"></a><span data-ttu-id="82cfb-135">Managing cost targets for your lab</span><span class="sxs-lookup"><span data-stu-id="82cfb-135">Managing cost targets for your lab</span></span>
<span data-ttu-id="82cfb-136">DevTest Labs lets you better manage the costs in  your lab by setting a spending target that you can then view in the Monthly Estimated Cost Trend chart.</span><span class="sxs-lookup"><span data-stu-id="82cfb-136">DevTest Labs lets you better manage the costs in  your lab by setting a spending target that you can then view in the Monthly Estimated Cost Trend chart.</span></span> <span data-ttu-id="82cfb-137">DevTest Labs can also send you a notification when the specified target spending or threshold is reached.</span><span class="sxs-lookup"><span data-stu-id="82cfb-137">DevTest Labs can also send you a notification when the specified target spending or threshold is reached.</span></span> 

1. <span data-ttu-id="82cfb-138">On your lab's **Overview** pane, select **Configuration and policies**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-138">On your lab's **Overview** pane, select **Configuration and policies**.</span></span>
1. <span data-ttu-id="82cfb-139">On the left under **COST TRACKING**, select **Cost trend**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-139">On the left under **COST TRACKING**, select **Cost trend**.</span></span>

    ![Manage target button](./media/devtest-lab-configure-cost-management/cost-trend.png)

1. <span data-ttu-id="82cfb-141">In the **Cost trend** pane, select **Manage target**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-141">In the **Cost trend** pane, select **Manage target**.</span></span>

    ![Manage target button](./media/devtest-lab-configure-cost-management/cost-trend-manage-target.png)

1. <span data-ttu-id="82cfb-143">In the Manage target pane, specify your desired spending target and thresholds.</span><span class="sxs-lookup"><span data-stu-id="82cfb-143">In the Manage target pane, specify your desired spending target and thresholds.</span></span> <span data-ttu-id="82cfb-144">You can also set whether each selected threshold is reported on the cost trend chart or through a webhook notification.</span><span class="sxs-lookup"><span data-stu-id="82cfb-144">You can also set whether each selected threshold is reported on the cost trend chart or through a webhook notification.</span></span>

    ![Manage target pane](./media/devtest-lab-configure-cost-management/cost-trend-manage-target-pane.png)

   - <span data-ttu-id="82cfb-146">Select a time period during which you want cost targets tracked.</span><span class="sxs-lookup"><span data-stu-id="82cfb-146">Select a time period during which you want cost targets tracked.</span></span>
      - <span data-ttu-id="82cfb-147">**Monthly**: cost targets are tracked per month.</span><span class="sxs-lookup"><span data-stu-id="82cfb-147">**Monthly**: cost targets are tracked per month.</span></span>
      - <span data-ttu-id="82cfb-148">**Fixed**: cost targets are tracked for the date range you specify in the Start date and End date fields.</span><span class="sxs-lookup"><span data-stu-id="82cfb-148">**Fixed**: cost targets are tracked for the date range you specify in the Start date and End date fields.</span></span> <span data-ttu-id="82cfb-149">Typically, this might correspond with how long your project is scheduled to run.</span><span class="sxs-lookup"><span data-stu-id="82cfb-149">Typically, this might correspond with how long your project is scheduled to run.</span></span>
   - <span data-ttu-id="82cfb-150">Specify a **Target cost**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-150">Specify a **Target cost**.</span></span> <span data-ttu-id="82cfb-151">For example, this might be how much you plan to spend on this lab in the time period you defined.</span><span class="sxs-lookup"><span data-stu-id="82cfb-151">For example, this might be how much you plan to spend on this lab in the time period you defined.</span></span>
   - <span data-ttu-id="82cfb-152">Select to enable or disable any threshold you want reported – in increments of 25% – up to 125% of your specified **Target cost**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-152">Select to enable or disable any threshold you want reported – in increments of 25% – up to 125% of your specified **Target cost**.</span></span>
      - <span data-ttu-id="82cfb-153">**Notify**: When this threshold is met, you are notified by a webhook URL you specify.</span><span class="sxs-lookup"><span data-stu-id="82cfb-153">**Notify**: When this threshold is met, you are notified by a webhook URL you specify.</span></span>
      - <span data-ttu-id="82cfb-154">**Plot on chart**: When this threshold is met, the results are plotted on the cost trend graph that you can view, as described in [Viewing the Monthly Estimated Cost Trend chart](#viewing-the-monthly-estimated-cost-trend-chart).</span><span class="sxs-lookup"><span data-stu-id="82cfb-154">**Plot on chart**: When this threshold is met, the results are plotted on the cost trend graph that you can view, as described in [Viewing the Monthly Estimated Cost Trend chart](#viewing-the-monthly-estimated-cost-trend-chart).</span></span>
   - <span data-ttu-id="82cfb-155">If you choose to **Notify** when the threshold is met, you must specify a webhook URL.</span><span class="sxs-lookup"><span data-stu-id="82cfb-155">If you choose to **Notify** when the threshold is met, you must specify a webhook URL.</span></span> <span data-ttu-id="82cfb-156">In the Cost integrations area, select **Click here to add an integration**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-156">In the Cost integrations area, select **Click here to add an integration**.</span></span>

      <span data-ttu-id="82cfb-157">Enter a Webhook URL in the Configure notification pane and then select **OK**.</span><span class="sxs-lookup"><span data-stu-id="82cfb-157">Enter a Webhook URL in the Configure notification pane and then select **OK**.</span></span>

       ![Configure notification pane](./media/devtest-lab-configure-cost-management/configure-notification.png)

      - <span data-ttu-id="82cfb-159">If you specify **Notify**, you must define a webhook URL.</span><span class="sxs-lookup"><span data-stu-id="82cfb-159">If you specify **Notify**, you must define a webhook URL.</span></span>
      - <span data-ttu-id="82cfb-160">Likewise, if you define a webhook URL, you must set **Notification** to **On** in the Cost threshold pane.</span><span class="sxs-lookup"><span data-stu-id="82cfb-160">Likewise, if you define a webhook URL, you must set **Notification** to **On** in the Cost threshold pane.</span></span>
      - <span data-ttu-id="82cfb-161">You must create a webhook prior to entering it here.</span><span class="sxs-lookup"><span data-stu-id="82cfb-161">You must create a webhook prior to entering it here.</span></span>  

      <span data-ttu-id="82cfb-162">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span><span class="sxs-lookup"><span data-stu-id="82cfb-162">For more information about webhooks, see [Create a webhook or API Azure Function](../azure-functions/functions-create-a-web-hook-or-api-function.md).</span></span> 
 

[!INCLUDE [devtest-lab-try-it-out](../../includes/devtest-lab-try-it-out.md)]

## <a name="related-blog-posts"></a><span data-ttu-id="82cfb-163">Related blog posts</span><span class="sxs-lookup"><span data-stu-id="82cfb-163">Related blog posts</span></span>
* [<span data-ttu-id="82cfb-164">Two more things to keep your cost on track in DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="82cfb-164">Two more things to keep your cost on track in DevTest Labs</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/06/21/keep-your-cost-on-track/)
* [<span data-ttu-id="82cfb-165">Why Cost Thresholds?</span><span class="sxs-lookup"><span data-stu-id="82cfb-165">Why Cost Thresholds?</span></span>](https://blogs.msdn.microsoft.com/devtestlab/2016/04/11/why-cost-thresholds/)

## <a name="next-steps"></a><span data-ttu-id="82cfb-166">Next steps</span><span class="sxs-lookup"><span data-stu-id="82cfb-166">Next steps</span></span>
<span data-ttu-id="82cfb-167">Here are some things to try next:</span><span class="sxs-lookup"><span data-stu-id="82cfb-167">Here are some things to try next:</span></span>

* <span data-ttu-id="82cfb-168">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span><span class="sxs-lookup"><span data-stu-id="82cfb-168">[Define lab policies](devtest-lab-set-lab-policy.md) - Learn how to set the various policies used to govern how your lab and its VMs are used.</span></span> 
* <span data-ttu-id="82cfb-169">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span><span class="sxs-lookup"><span data-stu-id="82cfb-169">[Create custom image](devtest-lab-create-template.md) - When you create a VM, you specify a base, which can be either a custom image or a Marketplace image.</span></span> <span data-ttu-id="82cfb-170">This article illustrates how to create a custom image from a VHD file.</span><span class="sxs-lookup"><span data-stu-id="82cfb-170">This article illustrates how to create a custom image from a VHD file.</span></span>
* <span data-ttu-id="82cfb-171">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span><span class="sxs-lookup"><span data-stu-id="82cfb-171">[Configure Marketplace images](devtest-lab-configure-marketplace-images.md) - DevTest Labs supports creating VMs based on Azure Marketplace images.</span></span> <span data-ttu-id="82cfb-172">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span><span class="sxs-lookup"><span data-stu-id="82cfb-172">This article illustrates how to specify which, if any, Azure Marketplace images can be used when creating VMs in a lab.</span></span>
* <span data-ttu-id="82cfb-173">[Create a VM in a lab](devtest-lab-add-vm.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span><span class="sxs-lookup"><span data-stu-id="82cfb-173">[Create a VM in a lab](devtest-lab-add-vm.md) - Illustrates how to create a VM from a base image (either custom or Marketplace), and how to work with artifacts in your VM.</span></span>

