---
title: Overview of Alerts in Microsoft Azure and Azure Monitor | Microsoft Docs
description: Alerts enable you to monitor Azure resource metrics, events, or logs and be notified when a condition you specify is met.
author: rboucher
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb13cb84b742e9ba646811d5ff041fc8ba8cc60c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556005"
---
# <a name="what-are-alerts-in-microsoft-azure"></a><span data-ttu-id="72bee-103">What are alerts in Microsoft Azure?</span><span class="sxs-lookup"><span data-stu-id="72bee-103">What are alerts in Microsoft Azure?</span></span>
<span data-ttu-id="72bee-104">This article describes what alerts are, their benefits, and how to get started with using them.</span><span class="sxs-lookup"><span data-stu-id="72bee-104">This article describes what alerts are, their benefits, and how to get started with using them.</span></span> <span data-ttu-id="72bee-105">It specifically applies to Azure Monitor, but provides pointers to other services.</span><span class="sxs-lookup"><span data-stu-id="72bee-105">It specifically applies to Azure Monitor, but provides pointers to other services.</span></span>  

<span data-ttu-id="72bee-106">Alerts are a method of monitoring Azure resource metrics, events, or logs and being notified when a condition you specify is met.</span><span class="sxs-lookup"><span data-stu-id="72bee-106">Alerts are a method of monitoring Azure resource metrics, events, or logs and being notified when a condition you specify is met.</span></span>  

## <a name="alerts-in-different-azure-services"></a><span data-ttu-id="72bee-107">Alerts in different Azure services</span><span class="sxs-lookup"><span data-stu-id="72bee-107">Alerts in different Azure services</span></span>
<span data-ttu-id="72bee-108">Alerts are available across different services, including:</span><span class="sxs-lookup"><span data-stu-id="72bee-108">Alerts are available across different services, including:</span></span>

* <span data-ttu-id="72bee-109">**Application Insights**: Enables web test and metric alerts.</span><span class="sxs-lookup"><span data-stu-id="72bee-109">**Application Insights**: Enables web test and metric alerts.</span></span> <span data-ttu-id="72bee-110">See [Set alerts in Application Insights](../application-insights/app-insights-alerts.md) and [Monitor availability and responsiveness of any website](../application-insights/app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="72bee-110">See [Set alerts in Application Insights](../application-insights/app-insights-alerts.md) and [Monitor availability and responsiveness of any website](../application-insights/app-insights-monitor-web-app-availability.md).</span></span>
* <span data-ttu-id="72bee-111">**Log Analytics (Operations Management Suite)**: Enables the routing of Activity and Diagnostic Logs to Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="72bee-111">**Log Analytics (Operations Management Suite)**: Enables the routing of Activity and Diagnostic Logs to Log Analytics.</span></span> <span data-ttu-id="72bee-112">Operations Management Suite allows metric, log, and other alert types.</span><span class="sxs-lookup"><span data-stu-id="72bee-112">Operations Management Suite allows metric, log, and other alert types.</span></span> <span data-ttu-id="72bee-113">For more information, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="72bee-113">For more information, see [Alerts in Log Analytics](../log-analytics/log-analytics-alerts.md).</span></span>  
* <span data-ttu-id="72bee-114">**Azure Monitor**: Enables alerts based on both metric values and activity log events.</span><span class="sxs-lookup"><span data-stu-id="72bee-114">**Azure Monitor**: Enables alerts based on both metric values and activity log events.</span></span> <span data-ttu-id="72bee-115">You can use the [Azure Monitor REST API](https://msdn.microsoft.com/library/dn931943.aspx) to manage alerts.</span><span class="sxs-lookup"><span data-stu-id="72bee-115">You can use the [Azure Monitor REST API](https://msdn.microsoft.com/library/dn931943.aspx) to manage alerts.</span></span>  <span data-ttu-id="72bee-116">For more information, see [Using the Azure portal, PowerShell, or the command-line interface to create alerts](insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="72bee-116">For more information, see [Using the Azure portal, PowerShell, or the command-line interface to create alerts](insights-alerts-portal.md).</span></span>

## <a name="visual-summary"></a><span data-ttu-id="72bee-117">Visual Summary</span><span class="sxs-lookup"><span data-stu-id="72bee-117">Visual Summary</span></span>
<span data-ttu-id="72bee-118">The following diagram summarizes alerts and what you can do with them specifically in "Azure Monitor".</span><span class="sxs-lookup"><span data-stu-id="72bee-118">The following diagram summarizes alerts and what you can do with them specifically in "Azure Monitor".</span></span> <span data-ttu-id="72bee-119">Other actions may be available for the services listed previously.</span><span class="sxs-lookup"><span data-stu-id="72bee-119">Other actions may be available for the services listed previously.</span></span> <span data-ttu-id="72bee-120">For example, currently alerts on Diagnostics Logs are only available in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="72bee-120">For example, currently alerts on Diagnostics Logs are only available in Log Analytics.</span></span>

![Alerts explained](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="what-can-trigger-alerts-in-azure-monitor"></a><span data-ttu-id="72bee-122">What can trigger alerts in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="72bee-122">What can trigger alerts in Azure Monitor</span></span>

<span data-ttu-id="72bee-123">You can receive alerts based on:</span><span class="sxs-lookup"><span data-stu-id="72bee-123">You can receive alerts based on:</span></span>

* <span data-ttu-id="72bee-124">**Metric values**: This alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span><span class="sxs-lookup"><span data-stu-id="72bee-124">**Metric values**: This alert triggers when the value of a specified metric crosses a threshold that you assign in either direction.</span></span> <span data-ttu-id="72bee-125">That is, it triggers both when the condition is first met and then afterward when that condition is no longer being met.</span><span class="sxs-lookup"><span data-stu-id="72bee-125">That is, it triggers both when the condition is first met and then afterward when that condition is no longer being met.</span></span> <span data-ttu-id="72bee-126">For a growing list of available metrics supported by Azure monitor, see [List of metrics supported on Azure Monitor](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="72bee-126">For a growing list of available metrics supported by Azure monitor, see [List of metrics supported on Azure Monitor](monitoring-supported-metrics.md).</span></span>
* <span data-ttu-id="72bee-127">**Activity log events**: This alert can trigger when a particular event occurs on a resource, or when a service notification is posted to your subscription.</span><span class="sxs-lookup"><span data-stu-id="72bee-127">**Activity log events**: This alert can trigger when a particular event occurs on a resource, or when a service notification is posted to your subscription.</span></span>

## <a name="what-can-metric-alerts-do"></a><span data-ttu-id="72bee-128">What can Metric Alerts do?</span><span class="sxs-lookup"><span data-stu-id="72bee-128">What can Metric Alerts do?</span></span>
<span data-ttu-id="72bee-129">You can configure an alert to do the following actions:</span><span class="sxs-lookup"><span data-stu-id="72bee-129">You can configure an alert to do the following actions:</span></span>

* <span data-ttu-id="72bee-130">Send email notifications to the service administrator, to co-administrators, or to additional email addresses that you specify.</span><span class="sxs-lookup"><span data-stu-id="72bee-130">Send email notifications to the service administrator, to co-administrators, or to additional email addresses that you specify.</span></span>
* <span data-ttu-id="72bee-131">Call a webhook, which enables you to launch additional automation actions.</span><span class="sxs-lookup"><span data-stu-id="72bee-131">Call a webhook, which enables you to launch additional automation actions.</span></span> <span data-ttu-id="72bee-132">Examples include calling:</span><span class="sxs-lookup"><span data-stu-id="72bee-132">Examples include calling:</span></span>
    - <span data-ttu-id="72bee-133">Azure Automation Runbook</span><span class="sxs-lookup"><span data-stu-id="72bee-133">Azure Automation Runbook</span></span>
    - <span data-ttu-id="72bee-134">Azure Function</span><span class="sxs-lookup"><span data-stu-id="72bee-134">Azure Function</span></span>
    - <span data-ttu-id="72bee-135">Azure Logic App</span><span class="sxs-lookup"><span data-stu-id="72bee-135">Azure Logic App</span></span>
    - <span data-ttu-id="72bee-136">a third-party service</span><span class="sxs-lookup"><span data-stu-id="72bee-136">a third-party service</span></span>

## <a name="what-can-activity-log-alerts-do"></a><span data-ttu-id="72bee-137">What can Activity Log Alerts do?</span><span class="sxs-lookup"><span data-stu-id="72bee-137">What can Activity Log Alerts do?</span></span>
<span data-ttu-id="72bee-138">You can configure an alert to do the following actions:</span><span class="sxs-lookup"><span data-stu-id="72bee-138">You can configure an alert to do the following actions:</span></span>
* <span data-ttu-id="72bee-139">Trigger whenever a specific event occurs one of the resources under your subscription</span><span class="sxs-lookup"><span data-stu-id="72bee-139">Trigger whenever a specific event occurs one of the resources under your subscription</span></span>
* <span data-ttu-id="72bee-140">Trigger whenever a service notification is posted to your subscription</span><span class="sxs-lookup"><span data-stu-id="72bee-140">Trigger whenever a service notification is posted to your subscription</span></span>
* <span data-ttu-id="72bee-141">Alert members of an action group via</span><span class="sxs-lookup"><span data-stu-id="72bee-141">Alert members of an action group via</span></span>
    * <span data-ttu-id="72bee-142">SMS</span><span class="sxs-lookup"><span data-stu-id="72bee-142">SMS</span></span>
    * <span data-ttu-id="72bee-143">Email</span><span class="sxs-lookup"><span data-stu-id="72bee-143">Email</span></span>
    * <span data-ttu-id="72bee-144">Webhook</span><span class="sxs-lookup"><span data-stu-id="72bee-144">Webhook</span></span>

## <a name="next-steps"></a><span data-ttu-id="72bee-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="72bee-145">Next steps</span></span>
<span data-ttu-id="72bee-146">Get information about alert rules and configuring them by using:</span><span class="sxs-lookup"><span data-stu-id="72bee-146">Get information about alert rules and configuring them by using:</span></span>

* <span data-ttu-id="72bee-147">Learn more about [Metrics](monitoring-overview-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-147">Learn more about [Metrics](monitoring-overview-metrics.md)</span></span>
* <span data-ttu-id="72bee-148">Configure [Metric Alerts via Azure portal](insights-alerts-portal.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-148">Configure [Metric Alerts via Azure portal](insights-alerts-portal.md)</span></span>
* <span data-ttu-id="72bee-149">Configure [Metric Alerts PowerShell](insights-alerts-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-149">Configure [Metric Alerts PowerShell](insights-alerts-powershell.md)</span></span>
* <span data-ttu-id="72bee-150">Configure [Metric Alerts Command-line interface (CLI)](insights-alerts-command-line-interface.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-150">Configure [Metric Alerts Command-line interface (CLI)](insights-alerts-command-line-interface.md)</span></span>
* <span data-ttu-id="72bee-151">Configure [Metric Alerts Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)</span><span class="sxs-lookup"><span data-stu-id="72bee-151">Configure [Metric Alerts Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)</span></span>
* <span data-ttu-id="72bee-152">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-152">Learn more about [Activity Log](monitoring-overview-activity-logs.md)</span></span>
* <span data-ttu-id="72bee-153">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-153">Configure [Activity Log Alerts via Azure portal](monitoring-activity-log-alerts.md)</span></span>
* <span data-ttu-id="72bee-154">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-154">Configure [Activity Log Alerts via Resource Manager](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
* <span data-ttu-id="72bee-155">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-155">Review the [activity log alert webhook schema](monitoring-activity-log-alerts-webhook.md)</span></span>
* <span data-ttu-id="72bee-156">Learn more about [Service Notifications](monitoring-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-156">Learn more about [Service Notifications](monitoring-service-notifications.md)</span></span>
* <span data-ttu-id="72bee-157">Learn more about [Action Groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="72bee-157">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>

