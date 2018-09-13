---
title: Monitoring usage and estimated costs in Azure Monitor
description: Overview of the process of using Azure Monitor usage and estimated costs page
author: dalekoetke
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 08/11/2018
ms.author: mbullwin
ms.reviewer: Dale.Koetke
ms.component: ''
ms.openlocfilehash: 35e7d36043defd236252f86facf4b9e2ed945d67
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869930"
---
# <a name="monitoring-usage-and-estimated-costs"></a><span data-ttu-id="9e1d7-103">Monitoring usage and estimated costs</span><span class="sxs-lookup"><span data-stu-id="9e1d7-103">Monitoring usage and estimated costs</span></span>

> [!NOTE]
> <span data-ttu-id="9e1d7-104">This article describes how to view usage and estimated costs across multiple Azure monitoring features for different pricing models.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-104">This article describes how to view usage and estimated costs across multiple Azure monitoring features for different pricing models.</span></span>  <span data-ttu-id="9e1d7-105">Refer to the following articles for related information.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-105">Refer to the following articles for related information.</span></span>
> - <span data-ttu-id="9e1d7-106">[Manage cost by controlling data volume and retention in Log Analytics](../log-analytics/log-analytics-manage-cost-storage.md) describes how to control your costs by changing your data retention period.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-106">[Manage cost by controlling data volume and retention in Log Analytics](../log-analytics/log-analytics-manage-cost-storage.md) describes how to control your costs by changing your data retention period.</span></span>
> - <span data-ttu-id="9e1d7-107">[Analyze data usage in Log Analytics](../log-analytics/log-analytics-usage.md) describes how to analyze and alert on your data usage.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-107">[Analyze data usage in Log Analytics](../log-analytics/log-analytics-usage.md) describes how to analyze and alert on your data usage.</span></span>
> - <span data-ttu-id="9e1d7-108">[Manage pricing and data volume in Application Insights](../application-insights/app-insights-pricing.md) describes how to analyze data usage in Application Insights.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-108">[Manage pricing and data volume in Application Insights](../application-insights/app-insights-pricing.md) describes how to analyze data usage in Application Insights.</span></span>

<span data-ttu-id="9e1d7-109">In the Monitor hub of the Azure portal, the **Usage and estimated costs** page explains the usage of core monitoring features such as [alerting, metrics, notifications](https://azure.microsoft.com/pricing/details/monitor/), [Azure Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/), and [Azure Application Insights](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-109">In the Monitor hub of the Azure portal, the **Usage and estimated costs** page explains the usage of core monitoring features such as [alerting, metrics, notifications](https://azure.microsoft.com/pricing/details/monitor/), [Azure Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/), and [Azure Application Insights](https://azure.microsoft.com/pricing/details/application-insights/).</span></span> <span data-ttu-id="9e1d7-110">For customers on the pricing plans available before April 2018, this also includes Log Analytics usage purchased through the Insights and Analytics offer.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-110">For customers on the pricing plans available before April 2018, this also includes Log Analytics usage purchased through the Insights and Analytics offer.</span></span>

<span data-ttu-id="9e1d7-111">On this page, users can view their resource usage for the past 31 days, aggregated per subscription.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-111">On this page, users can view their resource usage for the past 31 days, aggregated per subscription.</span></span> <span data-ttu-id="9e1d7-112">Drill-ins show usage trends over the 31-day period.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-112">Drill-ins show usage trends over the 31-day period.</span></span> <span data-ttu-id="9e1d7-113">A lot of data needs to come together for this estimate, so please be patient as the page loads.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-113">A lot of data needs to come together for this estimate, so please be patient as the page loads.</span></span>

<span data-ttu-id="9e1d7-114">This example shows monitoring usage and an estimate of the resulting costs:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-114">This example shows monitoring usage and an estimate of the resulting costs:</span></span>

![Usage and estimated costs portal screenshot](./media/monitoring-usage-and-estimated-costs/001.png)

<span data-ttu-id="9e1d7-116">Select the link in the monthly usage column to open a chart that shows usage trends over the last 31-day period:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-116">Select the link in the monthly usage column to open a chart that shows usage trends over the last 31-day period:</span></span>

![Included per node bar chart screenshot](./media/monitoring-usage-and-estimated-costs/002.png)

<span data-ttu-id="9e1d7-118">Here’s another similar usage and cost summary.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-118">Here’s another similar usage and cost summary.</span></span> <span data-ttu-id="9e1d7-119">This example shows a subscription in the new April 2018 consumption-based pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-119">This example shows a subscription in the new April 2018 consumption-based pricing model.</span></span> <span data-ttu-id="9e1d7-120">Note the lack of any node-based billing.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-120">Note the lack of any node-based billing.</span></span> <span data-ttu-id="9e1d7-121">Data ingestion and retention for Log Analytics and Application Insights are now reported on a new common meter.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-121">Data ingestion and retention for Log Analytics and Application Insights are now reported on a new common meter.</span></span>

![Usage and estimated costs portal screenshot - April 2018 pricing](./media/monitoring-usage-and-estimated-costs/003.png)

## <a name="new-pricing-model"></a><span data-ttu-id="9e1d7-123">New pricing model</span><span class="sxs-lookup"><span data-stu-id="9e1d7-123">New pricing model</span></span>

<span data-ttu-id="9e1d7-124">In April 2018, a [new monitoring pricing model was released](https://azure.microsoft.com/blog/introducing-a-new-way-to-purchase-azure-monitoring-services/).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-124">In April 2018, a [new monitoring pricing model was released](https://azure.microsoft.com/blog/introducing-a-new-way-to-purchase-azure-monitoring-services/).</span></span>  <span data-ttu-id="9e1d7-125">This features cloud-friendly, consumption-based pricing.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-125">This features cloud-friendly, consumption-based pricing.</span></span> <span data-ttu-id="9e1d7-126">You only pay for what you use, without node-based commitments.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-126">You only pay for what you use, without node-based commitments.</span></span> <span data-ttu-id="9e1d7-127">Details of the new pricing model are available for [alerting, metrics, notifications](https://azure.microsoft.com/pricing/details/monitor/), [Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/) and [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-127">Details of the new pricing model are available for [alerting, metrics, notifications](https://azure.microsoft.com/pricing/details/monitor/), [Log Analytics](https://azure.microsoft.com/pricing/details/log-analytics/) and [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/).</span></span> 

<span data-ttu-id="9e1d7-128">For customers onboarding to Log Analytics or Application Insights after April 2, 2018, the new pricing model is the only option.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-128">For customers onboarding to Log Analytics or Application Insights after April 2, 2018, the new pricing model is the only option.</span></span> <span data-ttu-id="9e1d7-129">For customers who already use these services, moving to the new pricing model is optional.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-129">For customers who already use these services, moving to the new pricing model is optional.</span></span>

## <a name="assessing-the-impact-of-the-new-pricing-model"></a><span data-ttu-id="9e1d7-130">Assessing the impact of the new pricing model</span><span class="sxs-lookup"><span data-stu-id="9e1d7-130">Assessing the impact of the new pricing model</span></span>
<span data-ttu-id="9e1d7-131">The new pricing model will have different impacts on each customer based on their monitoring usage patterns.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-131">The new pricing model will have different impacts on each customer based on their monitoring usage patterns.</span></span> <span data-ttu-id="9e1d7-132">For customers who were using Log Analytics or Application Insights before April 2, 2018, the **Usage and estimated cost** page in Azure Monitor estimates any change in costs if they move to the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-132">For customers who were using Log Analytics or Application Insights before April 2, 2018, the **Usage and estimated cost** page in Azure Monitor estimates any change in costs if they move to the new pricing model.</span></span> <span data-ttu-id="9e1d7-133">It provides the way to move a subscription into the new model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-133">It provides the way to move a subscription into the new model.</span></span> <span data-ttu-id="9e1d7-134">For most customers, the new pricing model will be advantageous.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-134">For most customers, the new pricing model will be advantageous.</span></span> <span data-ttu-id="9e1d7-135">For customers with especially high data usage patterns or in higher-cost regions, this may not be the case.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-135">For customers with especially high data usage patterns or in higher-cost regions, this may not be the case.</span></span>

<span data-ttu-id="9e1d7-136">To see an estimate of your costs for the subscriptions that you chose on the **Usage and estimated costs** page, select the blue banner near the top of the page.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-136">To see an estimate of your costs for the subscriptions that you chose on the **Usage and estimated costs** page, select the blue banner near the top of the page.</span></span> <span data-ttu-id="9e1d7-137">It’s best to do this one subscription at a time, because that's the level at which the new pricing model can be adopted.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-137">It’s best to do this one subscription at a time, because that's the level at which the new pricing model can be adopted.</span></span>

![Monitor usage and estimated costs in new pricing model screenshot](./media/monitoring-usage-and-estimated-costs/004.png)

<span data-ttu-id="9e1d7-139">The new page shows a similar version of the prior page with a green banner:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-139">The new page shows a similar version of the prior page with a green banner:</span></span>

![Monitor usage and estimated costs in current pricing model screenshot](./media/monitoring-usage-and-estimated-costs/005.png)

<span data-ttu-id="9e1d7-141">The page also shows a different set of meters that correspond to the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-141">The page also shows a different set of meters that correspond to the new pricing model.</span></span> <span data-ttu-id="9e1d7-142">This list is an example:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-142">This list is an example:</span></span>

- <span data-ttu-id="9e1d7-143">Insight and Analytics\Overage per Node</span><span class="sxs-lookup"><span data-stu-id="9e1d7-143">Insight and Analytics\Overage per Node</span></span>
- <span data-ttu-id="9e1d7-144">Insight and Analytics\Included per Node</span><span class="sxs-lookup"><span data-stu-id="9e1d7-144">Insight and Analytics\Included per Node</span></span>
- <span data-ttu-id="9e1d7-145">Application Insights\Basic Overage Data</span><span class="sxs-lookup"><span data-stu-id="9e1d7-145">Application Insights\Basic Overage Data</span></span>
- <span data-ttu-id="9e1d7-146">Application Insights\Included Data</span><span class="sxs-lookup"><span data-stu-id="9e1d7-146">Application Insights\Included Data</span></span>

<span data-ttu-id="9e1d7-147">The new pricing model doesn't have node-based included data allocations.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-147">The new pricing model doesn't have node-based included data allocations.</span></span> <span data-ttu-id="9e1d7-148">Therefore, these data ingestion meters are combined into a new common data ingestion meter called **Shared Services\Data Ingestion**.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-148">Therefore, these data ingestion meters are combined into a new common data ingestion meter called **Shared Services\Data Ingestion**.</span></span> 

<span data-ttu-id="9e1d7-149">There's another change to data ingested into Log Analytics or Application Insights in regions with higher costs.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-149">There's another change to data ingested into Log Analytics or Application Insights in regions with higher costs.</span></span> <span data-ttu-id="9e1d7-150">Data for these high-cost regions will be shown with the new regional meters.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-150">Data for these high-cost regions will be shown with the new regional meters.</span></span> <span data-ttu-id="9e1d7-151">An example is **Data Ingestion (US West Central)**.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-151">An example is **Data Ingestion (US West Central)**.</span></span>

> [!NOTE]
> <span data-ttu-id="9e1d7-152">The per subscription estimated costs do not factor into the account-level per node entitlements of the Operations Management Suite (OMS) subscription.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-152">The per subscription estimated costs do not factor into the account-level per node entitlements of the Operations Management Suite (OMS) subscription.</span></span> <span data-ttu-id="9e1d7-153">Consult your account representative for a more in-depth discussion of the new pricing model in this case.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-153">Consult your account representative for a more in-depth discussion of the new pricing model in this case.</span></span>

## <a name="new-pricing-model-and-operations-management-suite-subscription-entitlements"></a><span data-ttu-id="9e1d7-154">New pricing model and Operations Management Suite subscription entitlements</span><span class="sxs-lookup"><span data-stu-id="9e1d7-154">New pricing model and Operations Management Suite subscription entitlements</span></span>

<span data-ttu-id="9e1d7-155">Customers who purchased Microsoft Operations Management Suite E1 and E2 are eligible for per-node data ingestion entitlements for [Log Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite) and [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-pricing#the-price-plans).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-155">Customers who purchased Microsoft Operations Management Suite E1 and E2 are eligible for per-node data ingestion entitlements for [Log Analytics](https://www.microsoft.com/cloud-platform/operations-management-suite) and [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-pricing#the-price-plans).</span></span> <span data-ttu-id="9e1d7-156">To receive these entitlements for Log Analytics workspaces or Application Insights resources in a given subscription:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-156">To receive these entitlements for Log Analytics workspaces or Application Insights resources in a given subscription:</span></span> 

- <span data-ttu-id="9e1d7-157">The subscription's pricing model must remain in the pre-April 2018 model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-157">The subscription's pricing model must remain in the pre-April 2018 model.</span></span>
- <span data-ttu-id="9e1d7-158">Log Analytics workspaces should use the "Per-node (OMS)" pricing tier.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-158">Log Analytics workspaces should use the "Per-node (OMS)" pricing tier.</span></span>
- <span data-ttu-id="9e1d7-159">Application Insights resources should use the "Enterprise" pricing plan.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-159">Application Insights resources should use the "Enterprise" pricing plan.</span></span>

<span data-ttu-id="9e1d7-160">Depending on the number of nodes of the suite that your organization purchased, moving some subscriptions to the new pricing model could be advantageous, but this requires careful consideration.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-160">Depending on the number of nodes of the suite that your organization purchased, moving some subscriptions to the new pricing model could be advantageous, but this requires careful consideration.</span></span> <span data-ttu-id="9e1d7-161">In general, it is advisable simply to stay in the pre-April 2018 model as described above.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-161">In general, it is advisable simply to stay in the pre-April 2018 model as described above.</span></span>

> [!WARNING]
> <span data-ttu-id="9e1d7-162">If your organization has purchased the Microsoft Operations Management Suite E1 and E2, it is usually best to keep your subscriptions in the pre-April 2018 pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-162">If your organization has purchased the Microsoft Operations Management Suite E1 and E2, it is usually best to keep your subscriptions in the pre-April 2018 pricing model.</span></span> 
>

## <a name="changes-when-youre-moving-to-the-new-pricing-model"></a><span data-ttu-id="9e1d7-163">Changes when you're moving to the new pricing model</span><span class="sxs-lookup"><span data-stu-id="9e1d7-163">Changes when you're moving to the new pricing model</span></span>

<span data-ttu-id="9e1d7-164">The new pricing model simplifies Log Analytics and Application Insights pricing options to only a single tier (or plan).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-164">The new pricing model simplifies Log Analytics and Application Insights pricing options to only a single tier (or plan).</span></span> <span data-ttu-id="9e1d7-165">Moving a subscription into the new pricing model will:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-165">Moving a subscription into the new pricing model will:</span></span>

- <span data-ttu-id="9e1d7-166">Change the pricing tier for each Log Analytics to a new Per-GB tier (called “pergb2018” in Azure Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="9e1d7-166">Change the pricing tier for each Log Analytics to a new Per-GB tier (called “pergb2018” in Azure Resource Manager)</span></span>
- <span data-ttu-id="9e1d7-167">Any Application Insights resources in the Enterprise plan is changed to the Basic plan.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-167">Any Application Insights resources in the Enterprise plan is changed to the Basic plan.</span></span>

<span data-ttu-id="9e1d7-168">The cost estimation shows the effects of these changes.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-168">The cost estimation shows the effects of these changes.</span></span>

> [!WARNING]
> <span data-ttu-id="9e1d7-169">Here an important note if you use Azure Resource Manager or PowerShell to deploy [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-template-workspace-configuration) or [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-powershell) in a subscription you have moved to the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-169">Here an important note if you use Azure Resource Manager or PowerShell to deploy [Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-template-workspace-configuration) or [Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-powershell) in a subscription you have moved to the new pricing model.</span></span> <span data-ttu-id="9e1d7-170">If you specify a pricing tier/plan other than the “pergb2018” for Log Analytics or “Basic” for Application Insights, rather than failing the deployment due to specifying an invalid pricing tier/plan, it will succeed **but it will use only the valid pricing tier/plan** (This does not apply to the Log Analytics Free tier where an invalid pricing tier message is generated).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-170">If you specify a pricing tier/plan other than the “pergb2018” for Log Analytics or “Basic” for Application Insights, rather than failing the deployment due to specifying an invalid pricing tier/plan, it will succeed **but it will use only the valid pricing tier/plan** (This does not apply to the Log Analytics Free tier where an invalid pricing tier message is generated).</span></span>
>

## <a name="moving-to-the-new-pricing-model"></a><span data-ttu-id="9e1d7-171">Moving to the new pricing model</span><span class="sxs-lookup"><span data-stu-id="9e1d7-171">Moving to the new pricing model</span></span>

<span data-ttu-id="9e1d7-172">If you’ve decided to adopt the new pricing model for a subscription, select the **Pricing model selection** option at the top of the **Usage and estimated costs** page:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-172">If you’ve decided to adopt the new pricing model for a subscription, select the **Pricing model selection** option at the top of the **Usage and estimated costs** page:</span></span>

![Monitor usage and estimated costs in new pricing model screenshot](./media/monitoring-usage-and-estimated-costs/006.png)

<span data-ttu-id="9e1d7-174">The **Pricing model selection** page will open.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-174">The **Pricing model selection** page will open.</span></span> <span data-ttu-id="9e1d7-175">It shows a list of each of the subscriptions that you viewed on the prior page:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-175">It shows a list of each of the subscriptions that you viewed on the prior page:</span></span>

![Pricing model selection screenshot](./media/monitoring-usage-and-estimated-costs/007.png)

<span data-ttu-id="9e1d7-177">To move a subscription to the new pricing model, just select the box and then select **Save**.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-177">To move a subscription to the new pricing model, just select the box and then select **Save**.</span></span> <span data-ttu-id="9e1d7-178">You can move back to the older pricing model in the same way.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-178">You can move back to the older pricing model in the same way.</span></span> <span data-ttu-id="9e1d7-179">Keep in mind that subscription owner or contributor permissions are required to change the pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-179">Keep in mind that subscription owner or contributor permissions are required to change the pricing model.</span></span>

## <a name="automate-moving-to-the-new-pricing-model"></a><span data-ttu-id="9e1d7-180">Automate moving to the new pricing model</span><span class="sxs-lookup"><span data-stu-id="9e1d7-180">Automate moving to the new pricing model</span></span>

<span data-ttu-id="9e1d7-181">The scripts below require the Azure PowerShell Module.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-181">The scripts below require the Azure PowerShell Module.</span></span> <span data-ttu-id="9e1d7-182">To check if you have the latest version see [Install Azure PowerShell module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.1.0).</span><span class="sxs-lookup"><span data-stu-id="9e1d7-182">To check if you have the latest version see [Install Azure PowerShell module](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.1.0).</span></span>

<span data-ttu-id="9e1d7-183">Once you have the latest version of Azure PowerShell, you would first need to run ``Connect-AzureRmAccount``.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-183">Once you have the latest version of Azure PowerShell, you would first need to run ``Connect-AzureRmAccount``.</span></span>

``` PowerShell
# To check if your subscription is eligible to adjust pricing models.
$ResourceID ="/subscriptions/<Subscription-ID-Here>/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action listmigrationdate `
 -Force
```

<span data-ttu-id="9e1d7-184">A result of True under isGrandFatherableSubscription indicates that this subscription's pricing model can be moved between pricing models.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-184">A result of True under isGrandFatherableSubscription indicates that this subscription's pricing model can be moved between pricing models.</span></span> <span data-ttu-id="9e1d7-185">The lack of a value under optedInDate means this subscription is currently set to the old pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-185">The lack of a value under optedInDate means this subscription is currently set to the old pricing model.</span></span>

```
isGrandFatherableSubscription optedInDate
----------------------------- -----------
                         True            
```

<span data-ttu-id="9e1d7-186">To migrate this subscription to the new pricing model run:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-186">To migrate this subscription to the new pricing model run:</span></span>

```PowerShell
$ResourceID ="/subscriptions/<Subscription-ID-Here>/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action migratetonewpricingmodel `
 -Force
```

<span data-ttu-id="9e1d7-187">To confirm that the change was successful rerun:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-187">To confirm that the change was successful rerun:</span></span>

```PowerShell
$ResourceID ="/subscriptions/<Subscription-ID-Here>/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action listmigrationdate `
 -Force
```

<span data-ttu-id="9e1d7-188">If the migration was successful, your result should now look like:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-188">If the migration was successful, your result should now look like:</span></span>

```
isGrandFatherableSubscription optedInDate                      
----------------------------- -----------                      
                         True 2018-05-31T13:52:43.3592081+00:00
```

<span data-ttu-id="9e1d7-189">The optInDate now contains a timestamp of when this subscription opted in to the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-189">The optInDate now contains a timestamp of when this subscription opted in to the new pricing model.</span></span>

<span data-ttu-id="9e1d7-190">If you need to revert back to the old pricing model, you would run:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-190">If you need to revert back to the old pricing model, you would run:</span></span>

```PowerShell
 $ResourceID ="/subscriptions/<Subscription-ID-Here>/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action rollbacktolegacypricingmodel `
 -Force
```

<span data-ttu-id="9e1d7-191">If you then rerun the previous script that has ``-Action listmigrationdate``, you should now see an empty optedInDate value indicating your subscription has been returned to the legacy pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-191">If you then rerun the previous script that has ``-Action listmigrationdate``, you should now see an empty optedInDate value indicating your subscription has been returned to the legacy pricing model.</span></span>

<span data-ttu-id="9e1d7-192">If you have multiple subscriptions, that you wish to migrate which are hosted under the same tenant you could create your own variant using pieces of the following scripts:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-192">If you have multiple subscriptions, that you wish to migrate which are hosted under the same tenant you could create your own variant using pieces of the following scripts:</span></span>

```PowerShell
#Query tenant and create an array comprised of all of your tenants subscription ids
$TenantId = <Your-tenant-id>
$Tenant =Get-AzureRMSubscription -TenantId $TenantId
$Subscriptions = $Tenant.Id
```

<span data-ttu-id="9e1d7-193">To check to see if all the subscriptions in your tenant are eligible for the new pricing model, you can run:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-193">To check to see if all the subscriptions in your tenant are eligible for the new pricing model, you can run:</span></span>

```PowerShell
Foreach ($id in $Subscriptions)
{
$ResourceID ="/subscriptions/$id/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action listmigrationdate `
 -Force
}
```

<span data-ttu-id="9e1d7-194">The script could be refined further by creating a script that generates three arrays.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-194">The script could be refined further by creating a script that generates three arrays.</span></span> <span data-ttu-id="9e1d7-195">One array will consist of all subscription id's that have ```isGrandFatherableSubscription``` set to True and optedInDate does not currently have a value.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-195">One array will consist of all subscription id's that have ```isGrandFatherableSubscription``` set to True and optedInDate does not currently have a value.</span></span> <span data-ttu-id="9e1d7-196">A second array of any subscriptions currently on the new pricing model.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-196">A second array of any subscriptions currently on the new pricing model.</span></span> <span data-ttu-id="9e1d7-197">And a third array populated only with subscription ids in your tenant that are not eligible for the new pricing model:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-197">And a third array populated only with subscription ids in your tenant that are not eligible for the new pricing model:</span></span>

```PowerShell
[System.Collections.ArrayList]$Eligible= @{}
[System.Collections.ArrayList]$NewPricingEnabled = @{}
[System.Collections.ArrayList]$NotEligible = @{}

Foreach ($id in $Subscriptions)
{
$ResourceID ="/subscriptions/$id/providers/microsoft.insights"
$Result= Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action listmigrationdate `
 -Force

     if ($Result.isGrandFatherableSubscription -eq $True -and [bool]$Result.optedInDate -eq $False)
     {
     $Eligible.Add($id)
     }

     elseif ($Result.isGrandFatherableSubscription -eq $True -and [bool]$Result.optedInDate -eq $True)
     {
     $NewPricingEnabled.Add($id)
     }

     elseif ($Result.isGrandFatherableSubscription -eq $False)
     {
     $NotEligible.add($id)
     }
}
```

> [!NOTE]
> <span data-ttu-id="9e1d7-198">Depending on the number of subscriptions the above script may take some time to run.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-198">Depending on the number of subscriptions the above script may take some time to run.</span></span> <span data-ttu-id="9e1d7-199">Due to the use of the .add() method the PowerShell window will echo incrementing values as items are added to each array.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-199">Due to the use of the .add() method the PowerShell window will echo incrementing values as items are added to each array.</span></span>

<span data-ttu-id="9e1d7-200">Now that you have your subscriptions divided into the three arrays you should carefully review your results.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-200">Now that you have your subscriptions divided into the three arrays you should carefully review your results.</span></span> <span data-ttu-id="9e1d7-201">You may want to make a backup copy of the contents of the arrays so that you can easily revert your changes should you need to in the future.</span><span class="sxs-lookup"><span data-stu-id="9e1d7-201">You may want to make a backup copy of the contents of the arrays so that you can easily revert your changes should you need to in the future.</span></span> <span data-ttu-id="9e1d7-202">If you decided, you wanted to convert all the eligible subscriptions that are currently on the old pricing model to the new pricing model this task could now be accomplished with:</span><span class="sxs-lookup"><span data-stu-id="9e1d7-202">If you decided, you wanted to convert all the eligible subscriptions that are currently on the old pricing model to the new pricing model this task could now be accomplished with:</span></span>

```PowerShell
Foreach ($id in $Eligible)
{
$ResourceID ="/subscriptions/$id/providers/microsoft.insights"
Invoke-AzureRmResourceAction `
 -ResourceId $ResourceID `
 -ApiVersion "2017-10-01" `
 -Action migratetonewpricingmodel `
 -Force
}

```