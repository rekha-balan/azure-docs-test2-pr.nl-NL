---
title: Use the Azure portal to create classic alerts for Azure services | Microsoft Docs
description: Trigger emails or notifications, or call website URLs (webhooks) or automation when the conditions that you specify are met.
author: rboucher
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 09/23/2016
ms.author: robb
ms.component: alerts
ms.openlocfilehash: d0e5512eb3f963898ded6d7155f8b75cfb6ef911
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805446"
---
# <a name="use-the-azure-portal-to-create-classic-metric-alerts-in-azure-monitor-for-azure-services"></a><span data-ttu-id="7ff93-103">Use the Azure portal to create classic metric alerts in Azure Monitor for Azure services</span><span class="sxs-lookup"><span data-stu-id="7ff93-103">Use the Azure portal to create classic metric alerts in Azure Monitor for Azure services</span></span> 

> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>

> [!NOTE]
> This article describes how to create older classic metric alerts. Azure Monitor now supports [newer metric alerts](monitoring-near-real-time-metric-alerts.md). 


<span data-ttu-id="7ff93-109">This article shows you how to set up classic Azure metric alerts by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7ff93-109">This article shows you how to set up classic Azure metric alerts by using the Azure portal.</span></span> 

<span data-ttu-id="7ff93-110">You can receive an alert based on  metrics for your Azure services, or you can receive alerts for events that occur in Azure.</span><span class="sxs-lookup"><span data-stu-id="7ff93-110">You can receive an alert based on  metrics for your Azure services, or you can receive alerts for events that occur in Azure.</span></span>

* <span data-ttu-id="7ff93-111">**Metric values**: The alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="7ff93-111">**Metric values**: The alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span></span> <span data-ttu-id="7ff93-112">That is, it triggers both when the condition is first met and then when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="7ff93-112">That is, it triggers both when the condition is first met and then when that condition is no longer being met.</span></span>    

* <span data-ttu-id="7ff93-113">**Activity log events**: An alert can trigger on *every* event or when certain events occur.</span><span class="sxs-lookup"><span data-stu-id="7ff93-113">**Activity log events**: An alert can trigger on *every* event or when certain events occur.</span></span> <span data-ttu-id="7ff93-114">Learn more about [activity log alerts](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7ff93-114">Learn more about [activity log alerts](monitoring-activity-log-alerts.md).</span></span>

<span data-ttu-id="7ff93-115">You can configure a classic metric alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="7ff93-115">You can configure a classic metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="7ff93-116">Send email notifications to the service administrator and co-administrators.</span><span class="sxs-lookup"><span data-stu-id="7ff93-116">Send email notifications to the service administrator and co-administrators.</span></span>
* <span data-ttu-id="7ff93-117">Send email to additional email addresses that you specify.</span><span class="sxs-lookup"><span data-stu-id="7ff93-117">Send email to additional email addresses that you specify.</span></span>
* <span data-ttu-id="7ff93-118">Call a webhook.</span><span class="sxs-lookup"><span data-stu-id="7ff93-118">Call a webhook.</span></span>
* <span data-ttu-id="7ff93-119">Start execution of an Azure runbook (only from the Azure portal).</span><span class="sxs-lookup"><span data-stu-id="7ff93-119">Start execution of an Azure runbook (only from the Azure portal).</span></span>

<span data-ttu-id="7ff93-120">You can configure and get information about classic metric alert rules from the following locations:</span><span class="sxs-lookup"><span data-stu-id="7ff93-120">You can configure and get information about classic metric alert rules from the following locations:</span></span> 

* [<span data-ttu-id="7ff93-121">Azure portal</span><span class="sxs-lookup"><span data-stu-id="7ff93-121">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="7ff93-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ff93-122">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="7ff93-123">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="7ff93-123">Azure CLI</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="7ff93-124">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="7ff93-124">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="7ff93-125">Create an alert rule on a metric with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7ff93-125">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="7ff93-126">In the [portal](https://portal.azure.com/), locate the resource that you want to monitor, and then select it.</span><span class="sxs-lookup"><span data-stu-id="7ff93-126">In the [portal](https://portal.azure.com/), locate the resource that you want to monitor, and then select it.</span></span>

2. <span data-ttu-id="7ff93-127">In the **MONITORING** section, select **Alerts (Classic)**.</span><span class="sxs-lookup"><span data-stu-id="7ff93-127">In the **MONITORING** section, select **Alerts (Classic)**.</span></span> <span data-ttu-id="7ff93-128">The text and icon might vary slightly for different resources.</span><span class="sxs-lookup"><span data-stu-id="7ff93-128">The text and icon might vary slightly for different resources.</span></span> <span data-ttu-id="7ff93-129">If you don't find **Alerts (Classic)** here, you might find it in **Alerts** or **Alert Rules**.</span><span class="sxs-lookup"><span data-stu-id="7ff93-129">If you don't find **Alerts (Classic)** here, you might find it in **Alerts** or **Alert Rules**.</span></span>

    ![Monitoring](./media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="7ff93-131">Select the **Add metric alert (classic)** command, and then fill in the fields.</span><span class="sxs-lookup"><span data-stu-id="7ff93-131">Select the **Add metric alert (classic)** command, and then fill in the fields.</span></span>

    ![Add Alert](./media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="7ff93-133">**Name** your alert rule.</span><span class="sxs-lookup"><span data-stu-id="7ff93-133">**Name** your alert rule.</span></span> <span data-ttu-id="7ff93-134">Then choose a **Description**, which also appears in notification emails.</span><span class="sxs-lookup"><span data-stu-id="7ff93-134">Then choose a **Description**, which also appears in notification emails.</span></span>

5. <span data-ttu-id="7ff93-135">Select the **Metric** that you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="7ff93-135">Select the **Metric** that you want to monitor.</span></span> <span data-ttu-id="7ff93-136">Then choose a **Condition** and **Threshold** value for the metric.</span><span class="sxs-lookup"><span data-stu-id="7ff93-136">Then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="7ff93-137">Also choose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="7ff93-137">Also choose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="7ff93-138">For example, if you use the period "Over the last 5 minutes" and your alert looks for a CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="7ff93-138">For example, if you use the period "Over the last 5 minutes" and your alert looks for a CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="7ff93-139">After the first trigger occurs, it triggers again when the CPU stays below 80% for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="7ff93-139">After the first trigger occurs, it triggers again when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="7ff93-140">The CPU metric measurement happens every minute.</span><span class="sxs-lookup"><span data-stu-id="7ff93-140">The CPU metric measurement happens every minute.</span></span>

6. <span data-ttu-id="7ff93-141">Select **Email owners...** if you want administrators and co-administrators to receive email notifications when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="7ff93-141">Select **Email owners...** if you want administrators and co-administrators to receive email notifications when the alert fires.</span></span>

7. <span data-ttu-id="7ff93-142">If you want to send notifications to additional email addresses when the alert fires, add them in the **Additional Administrator email(s)** field.</span><span class="sxs-lookup"><span data-stu-id="7ff93-142">If you want to send notifications to additional email addresses when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="7ff93-143">Separate multiple emails with semicolons, in the following format: *email@contoso.com; email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="7ff93-143">Separate multiple emails with semicolons, in the following format: *email@contoso.com; email2@contoso.com*</span></span>

8. <span data-ttu-id="7ff93-144">Put in a valid URI in the **Webhook** field if you want it to be called when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="7ff93-144">Put in a valid URI in the **Webhook** field if you want it to be called when the alert fires.</span></span>

9. <span data-ttu-id="7ff93-145">If you use Azure Automation, you can select a runbook to be run when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="7ff93-145">If you use Azure Automation, you can select a runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="7ff93-146">Select **OK** to create the alert.</span><span class="sxs-lookup"><span data-stu-id="7ff93-146">Select **OK** to create the alert.</span></span>   

<span data-ttu-id="7ff93-147">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="7ff93-147">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="manage-your-alerts"></a><span data-ttu-id="7ff93-148">Manage your alerts</span><span class="sxs-lookup"><span data-stu-id="7ff93-148">Manage your alerts</span></span>
<span data-ttu-id="7ff93-149">After you create an alert, you can select it and do one of the following tasks:</span><span class="sxs-lookup"><span data-stu-id="7ff93-149">After you create an alert, you can select it and do one of the following tasks:</span></span>

* <span data-ttu-id="7ff93-150">View a graph that shows the metric threshold and the actual values from the previous day.</span><span class="sxs-lookup"><span data-stu-id="7ff93-150">View a graph that shows the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="7ff93-151">Edit or delete it.</span><span class="sxs-lookup"><span data-stu-id="7ff93-151">Edit or delete it.</span></span>
* <span data-ttu-id="7ff93-152">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span><span class="sxs-lookup"><span data-stu-id="7ff93-152">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7ff93-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ff93-153">Next steps</span></span>
* <span data-ttu-id="7ff93-154">[Get an overview of Azure monitoring](monitoring-overview.md), including the types of information you can collect and monitor.</span><span class="sxs-lookup"><span data-stu-id="7ff93-154">[Get an overview of Azure monitoring](monitoring-overview.md), including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="7ff93-155">Learn more about the [newer metric alerts](monitoring-near-real-time-metric-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7ff93-155">Learn more about the [newer metric alerts](monitoring-near-real-time-metric-alerts.md).</span></span>
* <span data-ttu-id="7ff93-156">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7ff93-156">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="7ff93-157">Learn more about [configuring alerts on activity log events](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="7ff93-157">Learn more about [configuring alerts on activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="7ff93-158">Learn more about [Azure Automation runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="7ff93-158">Learn more about [Azure Automation runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="7ff93-159">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md), and collect detailed high-frequency metrics on your service.</span><span class="sxs-lookup"><span data-stu-id="7ff93-159">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md), and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="7ff93-160">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure that your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="7ff93-160">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure that your service is available and responsive.</span></span>
