---
title: Create alerts for Azure services - Azure portal | Microsoft Docs
description: Trigger emails, notifications, call websites URLs (webhooks), or automation when the conditions you specify are met.
author: rboucher
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: f7457655-ced6-4102-a9dd-7ddf2265c0e2
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/23/2016
ms.author: robb
ms.openlocfilehash: bf95afa203aed4693beb7028695183deb7870e6b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550599"
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---azure-portal"></a><span data-ttu-id="9a0b8-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a0b8-103">Create metric alerts in Azure Monitor for Azure services - Azure portal</span></span>
> [!div class="op_single_selector"]
> * [Portal](insights-alerts-portal.md)
> * [PowerShell](insights-alerts-powershell.md)
> * [CLI](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="9a0b8-107">Overview</span><span class="sxs-lookup"><span data-stu-id="9a0b8-107">Overview</span></span>
<span data-ttu-id="9a0b8-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-108">This article shows you how to set up Azure metric alerts using the Azure portal.</span></span>   

<span data-ttu-id="9a0b8-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="9a0b8-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-110">**Metric values** - The alert triggers when the value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="9a0b8-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-111">That is, it triggers both when the condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="9a0b8-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="9a0b8-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="9a0b8-113">To learn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="9a0b8-114">You can configure a metric alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="9a0b8-114">You can configure a metric alert to do the following when it triggers:</span></span>

* <span data-ttu-id="9a0b8-115">send email notifications to the service administrator and co-administrators</span><span class="sxs-lookup"><span data-stu-id="9a0b8-115">send email notifications to the service administrator and co-administrators</span></span>
* <span data-ttu-id="9a0b8-116">send email to additional emails that you specify.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-116">send email to additional emails that you specify.</span></span>
* <span data-ttu-id="9a0b8-117">call a webhook</span><span class="sxs-lookup"><span data-stu-id="9a0b8-117">call a webhook</span></span>
* <span data-ttu-id="9a0b8-118">start execution of an Azure runbook (only from the Azure portal)</span><span class="sxs-lookup"><span data-stu-id="9a0b8-118">start execution of an Azure runbook (only from the Azure portal)</span></span>

<span data-ttu-id="9a0b8-119">You can configure and get information about metric alert rules using</span><span class="sxs-lookup"><span data-stu-id="9a0b8-119">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="9a0b8-120">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a0b8-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="9a0b8-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a0b8-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="9a0b8-122">command-line interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="9a0b8-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="9a0b8-123">Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="9a0b8-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

## <a name="create-an-alert-rule-on-a-metric-with-the-azure-portal"></a><span data-ttu-id="9a0b8-124">Create an alert rule on a metric with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a0b8-124">Create an alert rule on a metric with the Azure portal</span></span>
1. <span data-ttu-id="9a0b8-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-125">In the [portal](https://portal.azure.com/), locate the resource you are interested in monitoring and select it.</span></span>

2. <span data-ttu-id="9a0b8-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-126">Select **Alerts** or **Alert rules** under the MONITORING section.</span></span> <span data-ttu-id="9a0b8-127">The text and icon may vary slightly for different resources.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-127">The text and icon may vary slightly for different resources.</span></span>  

    ![Monitoring](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-alerts-portal/AlertRulesButton.png)

3. <span data-ttu-id="9a0b8-129">Select the **Add alert** command and fill in the fields.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-129">Select the **Add alert** command and fill in the fields.</span></span>

    ![Add Alert](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-alerts-portal/AddAlertOnlyParamsPage.png)

4. <span data-ttu-id="9a0b8-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-131">**Name** your alert rule, and choose a **Description**, which also shows in notification emails.</span></span>

5. <span data-ttu-id="9a0b8-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-132">Select the **Metric** you want to monitor, then choose a **Condition** and **Threshold** value for the metric.</span></span> <span data-ttu-id="9a0b8-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-133">Also chose the **Period** of time that the metric rule must be satisfied before the alert triggers.</span></span> <span data-ttu-id="9a0b8-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-134">So for example, if you use the period "PT5M" and your alert looks for CPU above 80%, the alert triggers when the CPU has been consistently above 80% for 5 minutes.</span></span> <span data-ttu-id="9a0b8-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-135">Once the first trigger occurs, it again triggers when the CPU stays below 80% for 5 minutes.</span></span> <span data-ttu-id="9a0b8-136">The CPU measurement occurs every 1 minute.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-136">The CPU measurement occurs every 1 minute.</span></span>   

6. <span data-ttu-id="9a0b8-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-137">Check **Email owners...** if you want administrators and co-administrators to be emailed when the alert fires.</span></span>

7. <span data-ttu-id="9a0b8-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-138">If you want additional emails to receive a notification when the alert fires, add them in the **Additional Administrator email(s)** field.</span></span> <span data-ttu-id="9a0b8-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span><span class="sxs-lookup"><span data-stu-id="9a0b8-139">Separate multiple emails with semi-colons - *email@contoso.com;email2@contoso.com*</span></span>

8. <span data-ttu-id="9a0b8-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-140">Put in a valid URI in the **Webhook** field if you want it called when the alert fires.</span></span>

9. <span data-ttu-id="9a0b8-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-141">If you use Azure Automation, you can select a Runbook to be run when the alert fires.</span></span>

10. <span data-ttu-id="9a0b8-142">Select **OK** when done to create the alert.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-142">Select **OK** when done to create the alert.</span></span>   

<span data-ttu-id="9a0b8-143">Within a few minutes, the alert is active and triggers as previously described.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-143">Within a few minutes, the alert is active and triggers as previously described.</span></span>

## <a name="managing-your-alerts"></a><span data-ttu-id="9a0b8-144">Managing your alerts</span><span class="sxs-lookup"><span data-stu-id="9a0b8-144">Managing your alerts</span></span>
<span data-ttu-id="9a0b8-145">Once you have created an alert, you can select it and:</span><span class="sxs-lookup"><span data-stu-id="9a0b8-145">Once you have created an alert, you can select it and:</span></span>

* <span data-ttu-id="9a0b8-146">View a graph showing the metric threshold and the actual values from the previous day.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-146">View a graph showing the metric threshold and the actual values from the previous day.</span></span>
* <span data-ttu-id="9a0b8-147">Edit or delete it.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-147">Edit or delete it.</span></span>
* <span data-ttu-id="9a0b8-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-148">**Disable** or **Enable** it if you want to temporarily stop or resume receiving notifications for that alert.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9a0b8-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a0b8-149">Next steps</span></span>
* <span data-ttu-id="9a0b8-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-150">[Get an overview of Azure monitoring](monitoring-overview.md) including the types of information you can collect and monitor.</span></span>
* <span data-ttu-id="9a0b8-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b8-151">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="9a0b8-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b8-152">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="9a0b8-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="9a0b8-153">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="9a0b8-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-154">Get an [overview of diagnostic logs](monitoring-overview-of-diagnostic-logs.md) and collect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="9a0b8-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="9a0b8-155">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>


