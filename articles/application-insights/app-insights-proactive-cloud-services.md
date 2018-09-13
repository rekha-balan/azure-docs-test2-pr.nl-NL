---
title: Alert on issues in Azure Cloud Services using the Azure Diagnostics integration with Azure Application Insights | Microsoft Docs
description: Monitor for issues like startup failures, crashes, and role recycle loops in Azure Cloud Services with Azure Application Insights
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.assetid: ea2a28ed-4cd9-4006-bd5a-d4c76f4ec20b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 06/07/2018
ms.reviewer: harelbr
ms.author: mbullwin
ms.openlocfilehash: cdb395a590fb200a24c68e56728a270b968e53b5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870436"
---
# <a name="alert-on-issues-in-azure-cloud-services-using-the-azure-diagnostics-integration-with-azure-application-insights"></a><span data-ttu-id="cc95e-103">Alert on issues in Azure Cloud Services using the Azure diagnostics integration with Azure Application Insights</span><span class="sxs-lookup"><span data-stu-id="cc95e-103">Alert on issues in Azure Cloud Services using the Azure diagnostics integration with Azure Application Insights</span></span>

<span data-ttu-id="cc95e-104">In this article, we will describe how to set up alert rules that monitor for issues like startup failures, crashes, and role recycle loops in Azure Cloud Services (web and worker roles).</span><span class="sxs-lookup"><span data-stu-id="cc95e-104">In this article, we will describe how to set up alert rules that monitor for issues like startup failures, crashes, and role recycle loops in Azure Cloud Services (web and worker roles).</span></span>

<span data-ttu-id="cc95e-105">The method described in this article is based on the [Azure Diagnostics integration with Application Insights](https://azure.microsoft.com/blog/azure-diagnostics-integration-with-application-insights/), and the recently released [Log Alerts for Application Insights](https://azure.microsoft.com/blog/log-alerts-for-application-insights-preview/) capability.</span><span class="sxs-lookup"><span data-stu-id="cc95e-105">The method described in this article is based on the [Azure Diagnostics integration with Application Insights](https://azure.microsoft.com/blog/azure-diagnostics-integration-with-application-insights/), and the recently released [Log Alerts for Application Insights](https://azure.microsoft.com/blog/log-alerts-for-application-insights-preview/) capability.</span></span>

## <a name="define-a-base-query"></a><span data-ttu-id="cc95e-106">Define a base query</span><span class="sxs-lookup"><span data-stu-id="cc95e-106">Define a base query</span></span>

<span data-ttu-id="cc95e-107">To get started, we will define a base query that retrieves the Windows Event Log events from the Windows Azure channel, which are captured into Application Insights as trace records.</span><span class="sxs-lookup"><span data-stu-id="cc95e-107">To get started, we will define a base query that retrieves the Windows Event Log events from the Windows Azure channel, which are captured into Application Insights as trace records.</span></span>
<span data-ttu-id="cc95e-108">These records can be used for detecting a variety of issues in Azure Cloud Services, like startup failures, runtime failures and recycle loops.</span><span class="sxs-lookup"><span data-stu-id="cc95e-108">These records can be used for detecting a variety of issues in Azure Cloud Services, like startup failures, runtime failures and recycle loops.</span></span>

> [!NOTE]
> <span data-ttu-id="cc95e-109">The base query below checks for issues in a time window of 30 minutes, and assumes a 10 minutes latency in ingesting the telemetry records.</span><span class="sxs-lookup"><span data-stu-id="cc95e-109">The base query below checks for issues in a time window of 30 minutes, and assumes a 10 minutes latency in ingesting the telemetry records.</span></span> <span data-ttu-id="cc95e-110">These defaults can be configured as you see fit.</span><span class="sxs-lookup"><span data-stu-id="cc95e-110">These defaults can be configured as you see fit.</span></span>

```
let window = 30m;
let endTime = ago(10m);
let EventLogs = traces
| where timestamp > endTime - window and timestamp < endTime
| extend channel = tostring(customDimensions.Channel), eventId = tostring(customDimensions.EventId)
| where channel == 'Windows Azure' and isnotempty(eventId)
| where tostring(customDimensions.DeploymentName) !contains 'deployment' // discard records captured from local machines
| project timestamp, channel, eventId, message, cloud_RoleInstance, cloud_RoleName, itemCount;
```

## <a name="check-for-specific-event-ids"></a><span data-ttu-id="cc95e-111">Check for specific event IDs</span><span class="sxs-lookup"><span data-stu-id="cc95e-111">Check for specific event IDs</span></span>

<span data-ttu-id="cc95e-112">After retrieving the Windows Event Log events, specific issues can be detected by checking for their respective event ID and message properties (see examples below).</span><span class="sxs-lookup"><span data-stu-id="cc95e-112">After retrieving the Windows Event Log events, specific issues can be detected by checking for their respective event ID and message properties (see examples below).</span></span>
<span data-ttu-id="cc95e-113">Simply combine the base query above with one of the queries below, and used that combined query when defining the log alert rule.</span><span class="sxs-lookup"><span data-stu-id="cc95e-113">Simply combine the base query above with one of the queries below, and used that combined query when defining the log alert rule.</span></span>

> [!NOTE]
> <span data-ttu-id="cc95e-114">In the examples below, an issue will be detected if more than three events are found during the analyzed time window.</span><span class="sxs-lookup"><span data-stu-id="cc95e-114">In the examples below, an issue will be detected if more than three events are found during the analyzed time window.</span></span> <span data-ttu-id="cc95e-115">This default can be configured to change the sensitivity of the alert rule.</span><span class="sxs-lookup"><span data-stu-id="cc95e-115">This default can be configured to change the sensitivity of the alert rule.</span></span>

```
// Detect failures in the OnStart method
EventLogs
| where eventId == '2001'
| where message contains '.OnStart()'
| summarize Failures = sum(itemCount) by cloud_RoleInstance, cloud_RoleName
| where Failures > 3
```

```
// Detect failures during runtime
EventLogs
| where eventId == '2001'
| where message contains '.Run()'
| summarize Failures = sum(itemCount) by cloud_RoleInstance, cloud_RoleName
| where Failures > 3
```

```
// Detect failures when running a startup task
EventLogs
| where eventId == '1000'
| summarize Failures = sum(itemCount) by cloud_RoleInstance, cloud_RoleName
| where Failures > 3
```

```
// Detect recycle loops
EventLogs
| where eventId == '1006'
| summarize Failures = sum(itemCount) by cloud_RoleInstance, cloud_RoleName
| where Failures > 3
```

## <a name="create-an-alert"></a><span data-ttu-id="cc95e-116">Create an alert</span><span class="sxs-lookup"><span data-stu-id="cc95e-116">Create an alert</span></span>

<span data-ttu-id="cc95e-117">In the navigation menu within your Application Insights resource, go to **Alerts**, and then select **New Alert Rule**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-117">In the navigation menu within your Application Insights resource, go to **Alerts**, and then select **New Alert Rule**.</span></span>

![Screenshot of Create rule](./media/app-insights-proactive-cloud-services/001.png)

<span data-ttu-id="cc95e-119">In the **Create rule** window, under the **Define alert condition** section, click on **Add criteria**, and then select **Custom log search**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-119">In the **Create rule** window, under the **Define alert condition** section, click on **Add criteria**, and then select **Custom log search**.</span></span>

![Screenshot of define condition criteria for alert](./media/app-insights-proactive-cloud-services/002.png)

<span data-ttu-id="cc95e-121">In the **Search query** box, paste the combined query you prepared in the previous step.</span><span class="sxs-lookup"><span data-stu-id="cc95e-121">In the **Search query** box, paste the combined query you prepared in the previous step.</span></span>

<span data-ttu-id="cc95e-122">Then, continue to the **Threshold** box, and set its value to 0.</span><span class="sxs-lookup"><span data-stu-id="cc95e-122">Then, continue to the **Threshold** box, and set its value to 0.</span></span> <span data-ttu-id="cc95e-123">You may optionally tweak the **Period** and Frequency **fields**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-123">You may optionally tweak the **Period** and Frequency **fields**.</span></span>
<span data-ttu-id="cc95e-124">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-124">Click **Done**.</span></span>

![Screenshot of configure signal logic query](./media/app-insights-proactive-cloud-services/003.png)

<span data-ttu-id="cc95e-126">Under the **Define alert details** section, provide a **Name** and **Description** to the alert rule, and set its **Severity**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-126">Under the **Define alert details** section, provide a **Name** and **Description** to the alert rule, and set its **Severity**.</span></span>
<span data-ttu-id="cc95e-127">Also, make sure that the **Enable rule upon creation** button is set to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-127">Also, make sure that the **Enable rule upon creation** button is set to **Yes**.</span></span>

![Screenshot alert details](./media/app-insights-proactive-cloud-services/004.png)

<span data-ttu-id="cc95e-129">Under the **Define action group** section, you can select an existing **Action group** or create a new one.</span><span class="sxs-lookup"><span data-stu-id="cc95e-129">Under the **Define action group** section, you can select an existing **Action group** or create a new one.</span></span>
<span data-ttu-id="cc95e-130">You may choose to have the action group contain multiple actions of various types.</span><span class="sxs-lookup"><span data-stu-id="cc95e-130">You may choose to have the action group contain multiple actions of various types.</span></span>

![Screenshot action group](./media/app-insights-proactive-cloud-services/005.png)

<span data-ttu-id="cc95e-132">Once you've defined the Action group, confirm your changes and click **Create alert rule**.</span><span class="sxs-lookup"><span data-stu-id="cc95e-132">Once you've defined the Action group, confirm your changes and click **Create alert rule**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc95e-133">Next Steps</span><span class="sxs-lookup"><span data-stu-id="cc95e-133">Next Steps</span></span>

<span data-ttu-id="cc95e-134">Learn more about automatically detecting:</span><span class="sxs-lookup"><span data-stu-id="cc95e-134">Learn more about automatically detecting:</span></span>

<span data-ttu-id="cc95e-135">[Failure anomalies](app-insights-proactive-failure-diagnostics.md)
[Memory Leaks](app-insights-proactive-potential-memory-leak.md)
[Performance anomalies](app-insights-proactive-performance-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="cc95e-135">[Failure anomalies](app-insights-proactive-failure-diagnostics.md)
[Memory Leaks](app-insights-proactive-potential-memory-leak.md)
[Performance anomalies](app-insights-proactive-performance-diagnostics.md)</span></span>

