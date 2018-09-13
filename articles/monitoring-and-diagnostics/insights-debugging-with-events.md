---
title: View events and activity(Audit) logs
description: Learn how to see all of the events that happen in your Azure subscription.
author: rboucher
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 60c38217-c3b5-4ef1-98ac-d045fdd5549b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/28/2015
ms.author: robb
ms.openlocfilehash: 2d6c759bd6a6180235bf757d01ad9c3e1d273aa0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556073"
---
# <a name="view-events-and-activity-logs"></a><span data-ttu-id="8573f-103">View events and activity logs</span><span class="sxs-lookup"><span data-stu-id="8573f-103">View events and activity logs</span></span>
<span data-ttu-id="8573f-104">All operations performed on Azure resources are fully audited by the Azure Resource Manager, from creation and deletions to granting or revoking access.</span><span class="sxs-lookup"><span data-stu-id="8573f-104">All operations performed on Azure resources are fully audited by the Azure Resource Manager, from creation and deletions to granting or revoking access.</span></span> <span data-ttu-id="8573f-105">You can browse these logs in the Azure portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931927.aspx) or [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) to access the full set of events programmatically.</span><span class="sxs-lookup"><span data-stu-id="8573f-105">You can browse these logs in the Azure portal, and you can also use the [REST API](https://msdn.microsoft.com/library/azure/dn931927.aspx) or [.NET SDK](https://www.nuget.org/packages/Microsoft.Azure.Insights/) to access the full set of events programmatically.</span></span>

## <a name="browse-the-events-impacting-your-azure-subscription"></a><span data-ttu-id="8573f-106">Browse the events impacting your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="8573f-106">Browse the events impacting your Azure subscription</span></span>
1. <span data-ttu-id="8573f-107">Sign in to the [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="8573f-107">Sign in to the [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="8573f-108">Click on the **Browse** and select **Audit logs**.</span><span class="sxs-lookup"><span data-stu-id="8573f-108">Click on the **Browse** and select **Audit logs**.</span></span>  
    <span data-ttu-id="8573f-109">![Browse Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_Browse.png)</span><span class="sxs-lookup"><span data-stu-id="8573f-109">![Browse Hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_Browse.png)</span></span>
3. <span data-ttu-id="8573f-110">This will open up a blade showing all of the events that have impacted any of your subscriptions for the past 7 days.</span><span class="sxs-lookup"><span data-stu-id="8573f-110">This will open up a blade showing all of the events that have impacted any of your subscriptions for the past 7 days.</span></span> <span data-ttu-id="8573f-111">At the top is a chart showing data by level, and below that is the full list of logs: ![All events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_AllEvents.png)</span><span class="sxs-lookup"><span data-stu-id="8573f-111">At the top is a chart showing data by level, and below that is the full list of logs: ![All events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_AllEvents.png)</span></span>

> [!NOTE]
> <span data-ttu-id="8573f-112">You can only view the 500 most recent events for a given subscription in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8573f-112">You can only view the 500 most recent events for a given subscription in the Azure portal.</span></span>
> 
> 

1. <span data-ttu-id="8573f-113">You can click on any log entry to see the events that made it up.</span><span class="sxs-lookup"><span data-stu-id="8573f-113">You can click on any log entry to see the events that made it up.</span></span> <span data-ttu-id="8573f-114">For example, when you deploy something to a resource group, many different resources may be created or modified.</span><span class="sxs-lookup"><span data-stu-id="8573f-114">For example, when you deploy something to a resource group, many different resources may be created or modified.</span></span> <span data-ttu-id="8573f-115">For each entry you can see:</span><span class="sxs-lookup"><span data-stu-id="8573f-115">For each entry you can see:</span></span>
   
   * <span data-ttu-id="8573f-116">The **Level** of the event - for example, it could be just something to track (**Informational**), or when something has gone wrong that you need to know about (**Error**).</span><span class="sxs-lookup"><span data-stu-id="8573f-116">The **Level** of the event - for example, it could be just something to track (**Informational**), or when something has gone wrong that you need to know about (**Error**).</span></span>
   * <span data-ttu-id="8573f-117">The **Status** - the final status will generally be **Succeeded** or **Failed**, but it may also be **Accepted** for long-running operations.</span><span class="sxs-lookup"><span data-stu-id="8573f-117">The **Status** - the final status will generally be **Succeeded** or **Failed**, but it may also be **Accepted** for long-running operations.</span></span>
   * <span data-ttu-id="8573f-118">*When* the event occurred.</span><span class="sxs-lookup"><span data-stu-id="8573f-118">*When* the event occurred.</span></span>
   * <span data-ttu-id="8573f-119">*Who* performed the operation, if anyone.</span><span class="sxs-lookup"><span data-stu-id="8573f-119">*Who* performed the operation, if anyone.</span></span> <span data-ttu-id="8573f-120">Not all operations are performed by users, some are performed by backend services so they would not have a **Caller**.</span><span class="sxs-lookup"><span data-stu-id="8573f-120">Not all operations are performed by users, some are performed by backend services so they would not have a **Caller**.</span></span>
   * <span data-ttu-id="8573f-121">The **Correlation ID** of the event - this is the unique identifier for this set of operations.</span><span class="sxs-lookup"><span data-stu-id="8573f-121">The **Correlation ID** of the event - this is the unique identifier for this set of operations.</span></span>
2. <span data-ttu-id="8573f-122">From there you can go to the details blade to see the specifics of the event.</span><span class="sxs-lookup"><span data-stu-id="8573f-122">From there you can go to the details blade to see the specifics of the event.</span></span>
   
    ![Resource groups](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_EventDetails.png)
   
    <span data-ttu-id="8573f-124">For **Failed** events, this page usually includes a **Substatus** and a **Properties** section that include useful details for debugging purposes.</span><span class="sxs-lookup"><span data-stu-id="8573f-124">For **Failed** events, this page usually includes a **Substatus** and a **Properties** section that include useful details for debugging purposes.</span></span>

## <a name="filter-to-specific-logs"></a><span data-ttu-id="8573f-125">Filter to specific logs</span><span class="sxs-lookup"><span data-stu-id="8573f-125">Filter to specific logs</span></span>
<span data-ttu-id="8573f-126">In order to see events that apply to a specific entity, or of a specific type, you can filter the Audit logs blade by clicking the **Filter** command.</span><span class="sxs-lookup"><span data-stu-id="8573f-126">In order to see events that apply to a specific entity, or of a specific type, you can filter the Audit logs blade by clicking the **Filter** command.</span></span> <span data-ttu-id="8573f-127">You also use the Filter blade to change the **Time span** of the Audit logs blade.</span><span class="sxs-lookup"><span data-stu-id="8573f-127">You also use the Filter blade to change the **Time span** of the Audit logs blade.</span></span>

<span data-ttu-id="8573f-128">Once you click this command, a new blade will open:</span><span class="sxs-lookup"><span data-stu-id="8573f-128">Once you click this command, a new blade will open:</span></span>

![Filter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_EventFilter.png)

<span data-ttu-id="8573f-130">There are four types of filters:</span><span class="sxs-lookup"><span data-stu-id="8573f-130">There are four types of filters:</span></span>

1. <span data-ttu-id="8573f-131">By subscription</span><span class="sxs-lookup"><span data-stu-id="8573f-131">By subscription</span></span>
2. <span data-ttu-id="8573f-132">By a **Resource group**</span><span class="sxs-lookup"><span data-stu-id="8573f-132">By a **Resource group**</span></span>
3. <span data-ttu-id="8573f-133">By a **Resource type**</span><span class="sxs-lookup"><span data-stu-id="8573f-133">By a **Resource type**</span></span>
4. <span data-ttu-id="8573f-134">By a particular **Resource** - for this you must past in the full *Resource ID* of the resource you are interested in</span><span class="sxs-lookup"><span data-stu-id="8573f-134">By a particular **Resource** - for this you must past in the full *Resource ID* of the resource you are interested in</span></span>

<span data-ttu-id="8573f-135">In addition, you can also filter events by who performed the event, or, by the level of the event.</span><span class="sxs-lookup"><span data-stu-id="8573f-135">In addition, you can also filter events by who performed the event, or, by the level of the event.</span></span>

<span data-ttu-id="8573f-136">Once you have finished choosing what you want to see, click the **Update** button at the bottom of the blade.</span><span class="sxs-lookup"><span data-stu-id="8573f-136">Once you have finished choosing what you want to see, click the **Update** button at the bottom of the blade.</span></span>

## <a name="monitor-events-impacting-specific-resources"></a><span data-ttu-id="8573f-137">Monitor events impacting specific resources</span><span class="sxs-lookup"><span data-stu-id="8573f-137">Monitor events impacting specific resources</span></span>
1. <span data-ttu-id="8573f-138">Click on **Browse** to find the resource you are interested in.</span><span class="sxs-lookup"><span data-stu-id="8573f-138">Click on **Browse** to find the resource you are interested in.</span></span> <span data-ttu-id="8573f-139">You can also see all of the logs for an entire **Resource group**.</span><span class="sxs-lookup"><span data-stu-id="8573f-139">You can also see all of the logs for an entire **Resource group**.</span></span>
2. <span data-ttu-id="8573f-140">On the resource's blade, scroll down until you find the **Events** tile.</span><span class="sxs-lookup"><span data-stu-id="8573f-140">On the resource's blade, scroll down until you find the **Events** tile.</span></span>  
    <span data-ttu-id="8573f-141">![Events tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_EventsTile.png)</span><span class="sxs-lookup"><span data-stu-id="8573f-141">![Events tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-debugging-with-events/Insights_EventsTile.png)</span></span>
3. <span data-ttu-id="8573f-142">Click on that tile to see events filtered to just the resource that you selected.</span><span class="sxs-lookup"><span data-stu-id="8573f-142">Click on that tile to see events filtered to just the resource that you selected.</span></span> <span data-ttu-id="8573f-143">You can use the **Filter** command to change the time range or apply more specific filters.</span><span class="sxs-lookup"><span data-stu-id="8573f-143">You can use the **Filter** command to change the time range or apply more specific filters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8573f-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="8573f-144">Next steps</span></span>
* <span data-ttu-id="8573f-145">[Receive alert notifications](insights-receive-alert-notifications.md) whenever an event happens.</span><span class="sxs-lookup"><span data-stu-id="8573f-145">[Receive alert notifications](insights-receive-alert-notifications.md) whenever an event happens.</span></span>
* <span data-ttu-id="8573f-146">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span><span class="sxs-lookup"><span data-stu-id="8573f-146">[Monitor service metrics](insights-how-to-customize-monitoring.md) to make sure your service is available and responsive.</span></span>
* <span data-ttu-id="8573f-147">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span><span class="sxs-lookup"><span data-stu-id="8573f-147">[Track service health](insights-service-health.md) to find out when Azure has experienced performance degradation or service interruptions.</span></span>  






