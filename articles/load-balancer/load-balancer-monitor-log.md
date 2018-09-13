---
title: Monitor operations, events, and counters for Load Balancer | Microsoft Docs
description: Learn how to enable alert events, and probe health status logging for Azure Load Balancer
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: 56656d74-0241-4096-88c8-aa88515d676d
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 9c0e5f4765152204b0d1f9027b0ef03b9bcf5aa4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552806"
---
# <a name="log-analytics-for-azure-load-balancer"></a><span data-ttu-id="541b7-103">Log analytics for Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="541b7-103">Log analytics for Azure Load Balancer</span></span>

<span data-ttu-id="541b7-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span><span class="sxs-lookup"><span data-stu-id="541b7-104">You can use different types of logs in Azure to manage and troubleshoot load balancers.</span></span> <span data-ttu-id="541b7-105">Some of these logs can be accessed through the portal.</span><span class="sxs-lookup"><span data-stu-id="541b7-105">Some of these logs can be accessed through the portal.</span></span> <span data-ttu-id="541b7-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span><span class="sxs-lookup"><span data-stu-id="541b7-106">All logs can be extracted from Azure blob storage, and viewed in different tools, such as Excel and PowerBI.</span></span> <span data-ttu-id="541b7-107">You can learn more about the different types of logs from the list below.</span><span class="sxs-lookup"><span data-stu-id="541b7-107">You can learn more about the different types of logs from the list below.</span></span>

* <span data-ttu-id="541b7-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span><span class="sxs-lookup"><span data-stu-id="541b7-108">**Audit logs:** You can use [Azure Audit Logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) (formerly known as Operational Logs) to view all operations being submitted to your Azure subscription(s), and their status.</span></span> <span data-ttu-id="541b7-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="541b7-109">Audit logs are enabled by default, and can be viewed in the Azure portal.</span></span>
* <span data-ttu-id="541b7-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span><span class="sxs-lookup"><span data-stu-id="541b7-110">**Alert event logs:** You can use this log to view alerts rasied by the load balancer.</span></span> <span data-ttu-id="541b7-111">The status for the load balancer is collected every five minutes.</span><span class="sxs-lookup"><span data-stu-id="541b7-111">The status for the load balancer is collected every five minutes.</span></span> <span data-ttu-id="541b7-112">This log is only written if a load balancer alert event is raised.</span><span class="sxs-lookup"><span data-stu-id="541b7-112">This log is only written if a load balancer alert event is raised.</span></span>
* <span data-ttu-id="541b7-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span><span class="sxs-lookup"><span data-stu-id="541b7-113">**Health probe logs:** You can use this log to view problems detected by your health probe, such as the number of instances in your backend-pool that are not receiving requests from the load balancer because of health probe failures.</span></span> <span data-ttu-id="541b7-114">This log is written to when there is a change in the health probe status.</span><span class="sxs-lookup"><span data-stu-id="541b7-114">This log is written to when there is a change in the health probe status.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="541b7-115">Log analytics currently works only for Internet facing load balancers.</span><span class="sxs-lookup"><span data-stu-id="541b7-115">Log analytics currently works only for Internet facing load balancers.</span></span> <span data-ttu-id="541b7-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="541b7-116">Logs are only available for resources deployed in the Resource Manager deployment model.</span></span> <span data-ttu-id="541b7-117">You cannot use logs for resources in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="541b7-117">You cannot use logs for resources in the classic deployment model.</span></span> <span data-ttu-id="541b7-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="541b7-118">For more information about the deployment models, see [Understanding Resource Manager deployment and classic deployment](../azure-resource-manager/resource-manager-deployment-model.md).</span></span>

## <a name="enable-logging"></a><span data-ttu-id="541b7-119">Enable logging</span><span class="sxs-lookup"><span data-stu-id="541b7-119">Enable logging</span></span>

<span data-ttu-id="541b7-120">Audit logging is automatically enabled for every Resource Manager resource.</span><span class="sxs-lookup"><span data-stu-id="541b7-120">Audit logging is automatically enabled for every Resource Manager resource.</span></span> <span data-ttu-id="541b7-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span><span class="sxs-lookup"><span data-stu-id="541b7-121">You need to enable event and health probe logging to start collecting the data available through those logs.</span></span> <span data-ttu-id="541b7-122">Use the following steps to enable logging.</span><span class="sxs-lookup"><span data-stu-id="541b7-122">Use the following steps to enable logging.</span></span>

<span data-ttu-id="541b7-123">Sign-in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="541b7-123">Sign-in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="541b7-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span><span class="sxs-lookup"><span data-stu-id="541b7-124">If you don't already have a load balancer, [create a load balancer](load-balancer-get-started-internet-arm-ps.md) before you continue.</span></span>

1. <span data-ttu-id="541b7-125">In the portal, click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="541b7-125">In the portal, click **Browse**.</span></span>
2. <span data-ttu-id="541b7-126">Select **Load Balancers**.</span><span class="sxs-lookup"><span data-stu-id="541b7-126">Select **Load Balancers**.</span></span>

    ![portal - load-balancer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-monitor-log/load-balancer-browse.png)

3. <span data-ttu-id="541b7-128">Select an existing load balancer >> **All Settings**.</span><span class="sxs-lookup"><span data-stu-id="541b7-128">Select an existing load balancer >> **All Settings**.</span></span>
4. <span data-ttu-id="541b7-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="541b7-129">On the right side of the dialog under the name of the load balancer, scroll to **Monitoring**, click **Diagnostics**.</span></span>

    ![portal - load-balancer-settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-monitor-log/load-balancer-settings.png)

5. <span data-ttu-id="541b7-131">In the **Diagnostics** pane, under **Status**, select **On**.</span><span class="sxs-lookup"><span data-stu-id="541b7-131">In the **Diagnostics** pane, under **Status**, select **On**.</span></span>
6. <span data-ttu-id="541b7-132">Click **Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="541b7-132">Click **Storage Account**.</span></span>
7. <span data-ttu-id="541b7-133">Under **LOGS**, select an existing storage account, or create a new one.</span><span class="sxs-lookup"><span data-stu-id="541b7-133">Under **LOGS**, select an existing storage account, or create a new one.</span></span> <span data-ttu-id="541b7-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span><span class="sxs-lookup"><span data-stu-id="541b7-134">Use the slider to determine how many days worth of event data will be stored in the event logs.</span></span> 
8. <span data-ttu-id="541b7-135">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="541b7-135">Click **Save**.</span></span>

    ![Portal - Diagnostics logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-monitor-log/load-balancer-diagnostics.png)

> [!NOTE]
> <span data-ttu-id="541b7-137">Audit logs do not require a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="541b7-137">Audit logs do not require a separate storage account.</span></span> <span data-ttu-id="541b7-138">The use of storage for event and health probe logging will incur service charges.</span><span class="sxs-lookup"><span data-stu-id="541b7-138">The use of storage for event and health probe logging will incur service charges.</span></span>

## <a name="audit-log"></a><span data-ttu-id="541b7-139">Audit log</span><span class="sxs-lookup"><span data-stu-id="541b7-139">Audit log</span></span>

<span data-ttu-id="541b7-140">The audit log is generated by default.</span><span class="sxs-lookup"><span data-stu-id="541b7-140">The audit log is generated by default.</span></span> <span data-ttu-id="541b7-141">The logs are preserved for 90 days in Azure's Event Logs store.</span><span class="sxs-lookup"><span data-stu-id="541b7-141">The logs are preserved for 90 days in Azure's Event Logs store.</span></span> <span data-ttu-id="541b7-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span><span class="sxs-lookup"><span data-stu-id="541b7-142">Learn more about these logs by reading the [View events and audit logs](../monitoring-and-diagnostics/insights-debugging-with-events.md) article.</span></span>

## <a name="alert-event-log"></a><span data-ttu-id="541b7-143">Alert event log</span><span class="sxs-lookup"><span data-stu-id="541b7-143">Alert event log</span></span>

<span data-ttu-id="541b7-144">This log is only generated if you've enabled it on a per load balancer basis.</span><span class="sxs-lookup"><span data-stu-id="541b7-144">This log is only generated if you've enabled it on a per load balancer basis.</span></span> <span data-ttu-id="541b7-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span><span class="sxs-lookup"><span data-stu-id="541b7-145">The events are logged in JSON format and stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="541b7-146">The following is an example of an event.</span><span class="sxs-lookup"><span data-stu-id="541b7-146">The following is an example of an event.</span></span>

```json
{
    "time": "2016-01-26T10:37:46.6024215Z",
    "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
    "category": "LoadBalancerAlertEvent",
    "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
    "operationName": "LoadBalancerProbeHealthStatus",
    "properties": {
        "eventName": "Resource Limits Hit",
        "eventDescription": "Ports exhausted",
        "eventProperties": {
            "public ip address": "40.117.227.32"
        }
    }
}
```

<span data-ttu-id="541b7-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span><span class="sxs-lookup"><span data-stu-id="541b7-147">The JSON output shows the *eventname* property which will describe the reason for the load balancer created an alert.</span></span> <span data-ttu-id="541b7-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span><span class="sxs-lookup"><span data-stu-id="541b7-148">In this case, the alert generated was due to TCP port exhaustion caused by source IP NAT limits (SNAT).</span></span>

## <a name="health-probe-log"></a><span data-ttu-id="541b7-149">Health probe log</span><span class="sxs-lookup"><span data-stu-id="541b7-149">Health probe log</span></span>

<span data-ttu-id="541b7-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span><span class="sxs-lookup"><span data-stu-id="541b7-150">This log is only generated if you've enabled it on a per load balancer basis as detailed above.</span></span> <span data-ttu-id="541b7-151">The data is stored in the storage account you specified when you enabled the logging.</span><span class="sxs-lookup"><span data-stu-id="541b7-151">The data is stored in the storage account you specified when you enabled the logging.</span></span> <span data-ttu-id="541b7-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span><span class="sxs-lookup"><span data-stu-id="541b7-152">A container named 'insights-logs-loadbalancerprobehealthstatus' is created and the following data is logged:</span></span>

```json
{
    "records":[
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 1,
            "healthPercentage": 50.000000
        }
    },
    {
        "time": "2016-01-26T10:37:46.6024215Z",
        "systemId": "32077926-b9c4-42fb-94c1-762e528b5b27",
        "category": "LoadBalancerProbeHealthStatus",
        "resourceId": "/SUBSCRIPTIONS/XXXXXXXXXXXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXX/RESOURCEGROUPS/RG7/PROVIDERS/MICROSOFT.NETWORK/LOADBALANCERS/WWEBLB",
        "operationName": "LoadBalancerProbeHealthStatus",
        "properties": {
            "publicIpAddress": "40.83.190.158",
            "port": "81",
            "totalDipCount": 2,
            "dipDownCount": 0,
            "healthPercentage": 100.000000
        }
    }]
}
```

<span data-ttu-id="541b7-153">The JSON output shows in the properties field the basic information for the probe health status.</span><span class="sxs-lookup"><span data-stu-id="541b7-153">The JSON output shows in the properties field the basic information for the probe health status.</span></span> <span data-ttu-id="541b7-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span><span class="sxs-lookup"><span data-stu-id="541b7-154">The *dipDownCount* property shows the total number of instances on the back-end which are not receiving network traffic due to failed probe responses.</span></span>

## <a name="view-and-analyze-the-audit-log"></a><span data-ttu-id="541b7-155">View and analyze the audit log</span><span class="sxs-lookup"><span data-stu-id="541b7-155">View and analyze the audit log</span></span>

<span data-ttu-id="541b7-156">You can view and analyze audit log data using any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="541b7-156">You can view and analyze audit log data using any of the following methods:</span></span>

* <span data-ttu-id="541b7-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span><span class="sxs-lookup"><span data-stu-id="541b7-157">**Azure tools:** Retrieve information from the audit logs through Azure PowerShell, the Azure Command Line Interface (CLI), the Azure REST API, or the Azure preview portal.</span></span> <span data-ttu-id="541b7-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span><span class="sxs-lookup"><span data-stu-id="541b7-158">Step-by-step instructions for each method are detailed in the [Audit operations with Resource Manager](../azure-resource-manager/resource-group-audit.md) article.</span></span>
* <span data-ttu-id="541b7-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span><span class="sxs-lookup"><span data-stu-id="541b7-159">**Power BI:** If you do not already have a [Power BI](https://powerbi.microsoft.com/pricing) account, you can try it for free.</span></span> <span data-ttu-id="541b7-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span><span class="sxs-lookup"><span data-stu-id="541b7-160">Using the [Azure Audit Logs content pack for Power BI](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs), you can analyze your data with pre-configured dashboards, or you can customize views to suit your requirements.</span></span>

## <a name="view-and-analyze-the-health-probe-and-event-log"></a><span data-ttu-id="541b7-161">View and analyze the health probe and event log</span><span class="sxs-lookup"><span data-stu-id="541b7-161">View and analyze the health probe and event log</span></span>

<span data-ttu-id="541b7-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span><span class="sxs-lookup"><span data-stu-id="541b7-162">You need to connect to your storage account and retrieve the JSON log entries for event and health probe logs.</span></span> <span data-ttu-id="541b7-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span><span class="sxs-lookup"><span data-stu-id="541b7-163">Once you download the JSON files, you can convert them to CSV and view in Excel, PowerBI, or any other data visualization tool.</span></span>

> [!TIP]
> <span data-ttu-id="541b7-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span><span class="sxs-lookup"><span data-stu-id="541b7-164">If you are familiar with Visual Studio and basic concepts of changing values for constants and variables in C#, you can use the [log converter tools](https://github.com/Azure-Samples/networking-dotnet-log-converter) available from GitHub.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="541b7-165">Additional resources</span><span class="sxs-lookup"><span data-stu-id="541b7-165">Additional resources</span></span>

* <span data-ttu-id="541b7-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span><span class="sxs-lookup"><span data-stu-id="541b7-166">[Visualize your Azure Audit Logs with Power BI](http://blogs.msdn.com/b/powerbi/archive/2015/09/30/monitor-azure-audit-logs-with-power-bi.aspx) blog post.</span></span>
* <span data-ttu-id="541b7-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span><span class="sxs-lookup"><span data-stu-id="541b7-167">[View and analyze Azure Audit Logs in Power BI and more](https://azure.microsoft.com/blog/analyze-azure-audit-logs-in-powerbi-more/) blog post.</span></span>

## <a name="next-steps"></a><span data-ttu-id="541b7-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="541b7-168">Next steps</span></span>

[<span data-ttu-id="541b7-169">Understand load balancer probes</span><span class="sxs-lookup"><span data-stu-id="541b7-169">Understand load balancer probes</span></span>](load-balancer-custom-probe-overview.md)



