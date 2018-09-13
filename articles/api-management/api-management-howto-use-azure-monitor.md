---
title: Monitor API Management with Azure Monitor | Microsoft Docs
description: Learn how to monitor Azure API Management service using Azure Monitor.
services: api-management
documentationcenter: ''
author: miaojiang
manager: erikre
editor: ''
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: cff76aca09054a41b7e781e9bf0a942a23a02de2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540953"
---
# <a name="monitor-api-management-with-azure-monitor"></a><span data-ttu-id="f2a15-103">Monitor API Management with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="f2a15-103">Monitor API Management with Azure Monitor</span></span>
<span data-ttu-id="f2a15-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f2a15-104">Azure Monitor is an Azure service that provides a single source for monitoring all your Azure resources.</span></span> <span data-ttu-id="f2a15-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span><span class="sxs-lookup"><span data-stu-id="f2a15-105">With Azure Monitor, you can visualize, query, route, archive, and take actions on the metrics and logs coming from Azure resources such as API Management.</span></span> 

<span data-ttu-id="f2a15-106">The following video shows how to monitor API Management using Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="f2a15-106">The following video shows how to monitor API Management using Azure Monitor.</span></span> <span data-ttu-id="f2a15-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span><span class="sxs-lookup"><span data-stu-id="f2a15-107">For more information about Azure Monitor, see [Get Started with Azure Monitor].</span></span> 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a><span data-ttu-id="f2a15-108">Metrics</span><span class="sxs-lookup"><span data-stu-id="f2a15-108">Metrics</span></span>
<span data-ttu-id="f2a15-109">API Management currently emits five metrics and we plan to add more in the future.</span><span class="sxs-lookup"><span data-stu-id="f2a15-109">API Management currently emits five metrics and we plan to add more in the future.</span></span> <span data-ttu-id="f2a15-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span><span class="sxs-lookup"><span data-stu-id="f2a15-110">These metrics are emitted every minute, giving you near real-time visibility into the state and health of your APIs.</span></span> <span data-ttu-id="f2a15-111">Following is a summary of the metrics:</span><span class="sxs-lookup"><span data-stu-id="f2a15-111">Following is a summary of the metrics:</span></span>
* <span data-ttu-id="f2a15-112">Total Gateway Requests: the number of API requests in the period.</span><span class="sxs-lookup"><span data-stu-id="f2a15-112">Total Gateway Requests: the number of API requests in the period.</span></span> 
* <span data-ttu-id="f2a15-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span><span class="sxs-lookup"><span data-stu-id="f2a15-113">Successful Gateway Requests: the number of API requests that received successful HTTP response codes including 304, 307 and anything smaller than 301 (for example, 200).</span></span> 
* <span data-ttu-id="f2a15-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span><span class="sxs-lookup"><span data-stu-id="f2a15-114">Failed Gateway Requests: the number of API requests that received erroneous HTTP response codes including 400 and anything larger than 500.</span></span>
* <span data-ttu-id="f2a15-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span><span class="sxs-lookup"><span data-stu-id="f2a15-115">Unauthorized Gateway Requests: the number of API requests that received HTTP response codes including 401, 403, and 429.</span></span> 
* <span data-ttu-id="f2a15-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span><span class="sxs-lookup"><span data-stu-id="f2a15-116">Other Gateway Requests: the number of API requests that received HTTP response codes that do not belong to any of the preceding categories (for example, 418).</span></span>

<span data-ttu-id="f2a15-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="f2a15-117">You can access metrics in your API Management service, or access metrics of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="f2a15-118">To view metrics in your API Management service:</span><span class="sxs-lookup"><span data-stu-id="f2a15-118">To view metrics in your API Management service:</span></span>
1. <span data-ttu-id="f2a15-119">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2a15-119">Open the Azure portal.</span></span>
2. <span data-ttu-id="f2a15-120">Go to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="f2a15-120">Go to your API Management service.</span></span>
3. <span data-ttu-id="f2a15-121">Click **Metrics**.</span><span class="sxs-lookup"><span data-stu-id="f2a15-121">Click **Metrics**.</span></span>

![Metrics blade][metrics-blade]

<span data-ttu-id="f2a15-123">For more information about how to use Metrics, see [Overview of Metrics].</span><span class="sxs-lookup"><span data-stu-id="f2a15-123">For more information about how to use Metrics, see [Overview of Metrics].</span></span>

## <a name="activity-logs"></a><span data-ttu-id="f2a15-124">Activity Logs</span><span class="sxs-lookup"><span data-stu-id="f2a15-124">Activity Logs</span></span>
<span data-ttu-id="f2a15-125">Activity logs provide insight into the operations that were performed on your API Management services.</span><span class="sxs-lookup"><span data-stu-id="f2a15-125">Activity logs provide insight into the operations that were performed on your API Management services.</span></span> <span data-ttu-id="f2a15-126">It was previously known as "audit logs" or "operational logs".</span><span class="sxs-lookup"><span data-stu-id="f2a15-126">It was previously known as "audit logs" or "operational logs".</span></span> <span data-ttu-id="f2a15-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span><span class="sxs-lookup"><span data-stu-id="f2a15-127">Using activity logs, you can determine the "what, who, and when" for any write operations (PUT, POST, DELETE) taken on your API Management services.</span></span> 

> [!NOTE]
> <span data-ttu-id="f2a15-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span><span class="sxs-lookup"><span data-stu-id="f2a15-128">Activity logs do not include read (GET) operations or operations performed in the classic Publisher Portal or using the original Management APIs.</span></span>

<span data-ttu-id="f2a15-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="f2a15-129">You can access activity logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="f2a15-130">To view activity logs in your API Management service:</span><span class="sxs-lookup"><span data-stu-id="f2a15-130">To view activity logs in your API Management service:</span></span>
1. <span data-ttu-id="f2a15-131">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2a15-131">Open the Azure portal.</span></span>
2. <span data-ttu-id="f2a15-132">Go to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="f2a15-132">Go to your API Management service.</span></span>
3. <span data-ttu-id="f2a15-133">Click **Activity log**.</span><span class="sxs-lookup"><span data-stu-id="f2a15-133">Click **Activity log**.</span></span>

![Activity logs blade][activity-logs-blade]

<span data-ttu-id="f2a15-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span><span class="sxs-lookup"><span data-stu-id="f2a15-135">For more information about how to use Metrics, see [Overview of Activity Logs].</span></span>

## <a name="alerts"></a><span data-ttu-id="f2a15-136">Alerts</span><span class="sxs-lookup"><span data-stu-id="f2a15-136">Alerts</span></span>
<span data-ttu-id="f2a15-137">You can configure to receive alerts based on metrics and activity logs.</span><span class="sxs-lookup"><span data-stu-id="f2a15-137">You can configure to receive alerts based on metrics and activity logs.</span></span> <span data-ttu-id="f2a15-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span><span class="sxs-lookup"><span data-stu-id="f2a15-138">Azure Monitor allows you to configure an alert to do the following when it triggers:</span></span>

* <span data-ttu-id="f2a15-139">Send an email notification</span><span class="sxs-lookup"><span data-stu-id="f2a15-139">Send an email notification</span></span>
* <span data-ttu-id="f2a15-140">Call a webhook</span><span class="sxs-lookup"><span data-stu-id="f2a15-140">Call a webhook</span></span>
* <span data-ttu-id="f2a15-141">Invoke an Azure Logic App</span><span class="sxs-lookup"><span data-stu-id="f2a15-141">Invoke an Azure Logic App</span></span>

<span data-ttu-id="f2a15-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="f2a15-142">You can configure alert rules in your API Management service, or in Azure Monitor.</span></span> <span data-ttu-id="f2a15-143">To configure them in API Management:</span><span class="sxs-lookup"><span data-stu-id="f2a15-143">To configure them in API Management:</span></span> 
1. <span data-ttu-id="f2a15-144">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2a15-144">Open the Azure portal.</span></span>
2. <span data-ttu-id="f2a15-145">Go to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="f2a15-145">Go to your API Management service.</span></span>
3. <span data-ttu-id="f2a15-146">Click **Alert rules**.</span><span class="sxs-lookup"><span data-stu-id="f2a15-146">Click **Alert rules**.</span></span>

![Alert rules blade][alert-rules-blade]

<span data-ttu-id="f2a15-148">For more information about using Alerts, see [Overview of Alerts].</span><span class="sxs-lookup"><span data-stu-id="f2a15-148">For more information about using Alerts, see [Overview of Alerts].</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="f2a15-149">Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="f2a15-149">Diagnostic Logs</span></span>
<span data-ttu-id="f2a15-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="f2a15-150">Diagnostic logs provide rich information about operations and errors that are important for auditing as well as troubleshooting purposes.</span></span> <span data-ttu-id="f2a15-151">Diagnostics logs differ from activity logs.</span><span class="sxs-lookup"><span data-stu-id="f2a15-151">Diagnostics logs differ from activity logs.</span></span> <span data-ttu-id="f2a15-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="f2a15-152">Activity logs provide insights into the operations that were performed on your Azure resources.</span></span> <span data-ttu-id="f2a15-153">Diagnostics logs provide insight into operations that your resource performed itself.</span><span class="sxs-lookup"><span data-stu-id="f2a15-153">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="f2a15-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span><span class="sxs-lookup"><span data-stu-id="f2a15-154">API Management currently provides diagnostics logs (batched hourly) about individual API request with each entry having the following structure:</span></span>

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

<span data-ttu-id="f2a15-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="f2a15-155">You can access diagnostic logs in your API Management service, or access logs of all your Azure resources in Azure Monitor.</span></span> <span data-ttu-id="f2a15-156">To view diagnostic logs in your API Management service:</span><span class="sxs-lookup"><span data-stu-id="f2a15-156">To view diagnostic logs in your API Management service:</span></span>
1. <span data-ttu-id="f2a15-157">Open the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f2a15-157">Open the Azure portal.</span></span>
2. <span data-ttu-id="f2a15-158">Go to your API Management service.</span><span class="sxs-lookup"><span data-stu-id="f2a15-158">Go to your API Management service.</span></span>
3. <span data-ttu-id="f2a15-159">Click **Diagnostic log**.</span><span class="sxs-lookup"><span data-stu-id="f2a15-159">Click **Diagnostic log**.</span></span>

![Diagnostic logs blade][diagnostic-logs-blade]

<span data-ttu-id="f2a15-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span><span class="sxs-lookup"><span data-stu-id="f2a15-161">For more information about how to use Metrics, see [Overview of Diagnostic Logs].</span></span>

## <a name="next-step"></a><span data-ttu-id="f2a15-162">Next Step</span><span class="sxs-lookup"><span data-stu-id="f2a15-162">Next Step</span></span>

* <span data-ttu-id="f2a15-163">[Get Started with Azure Monitor]</span><span class="sxs-lookup"><span data-stu-id="f2a15-163">[Get Started with Azure Monitor]</span></span>
* <span data-ttu-id="f2a15-164">[Overview of Metrics]</span><span class="sxs-lookup"><span data-stu-id="f2a15-164">[Overview of Metrics]</span></span>
* <span data-ttu-id="f2a15-165">[Overview of Activity Logs]</span><span class="sxs-lookup"><span data-stu-id="f2a15-165">[Overview of Activity Logs]</span></span>
* <span data-ttu-id="f2a15-166">[Overview of Diagnostic Logs]</span><span class="sxs-lookup"><span data-stu-id="f2a15-166">[Overview of Diagnostic Logs]</span></span>
* <span data-ttu-id="f2a15-167">[Overview of Alerts]</span><span class="sxs-lookup"><span data-stu-id="f2a15-167">[Overview of Alerts]</span></span>

[Get Started with Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[Overview of Metrics]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[Overview of Activity Logs]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[Overview of Diagnostic Logs]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Overview of Alerts]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png




