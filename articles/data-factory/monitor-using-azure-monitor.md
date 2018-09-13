---
title: Monitor data factories using Azure Monitor | Microsoft Docs
description: Learn how to use Azure Monitor to monitor Data Factory pipelines by enabling diagnostic logs with information from Azure Data Factory.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/22/2018
ms.author: shlo
ms.openlocfilehash: d0f36551fb06e04b50af464bac6953dda64c6202
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870615"
---
# <a name="alert-and-monitor-data-factories-using-azure-monitor"></a><span data-ttu-id="4b197-103">Alert and Monitor data factories using Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4b197-103">Alert and Monitor data factories using Azure Monitor</span></span>
<span data-ttu-id="4b197-104">Cloud applications are complex with many moving parts.</span><span class="sxs-lookup"><span data-stu-id="4b197-104">Cloud applications are complex with many moving parts.</span></span> <span data-ttu-id="4b197-105">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span><span class="sxs-lookup"><span data-stu-id="4b197-105">Monitoring provides data to ensure that your application stays up and running in a healthy state.</span></span> <span data-ttu-id="4b197-106">It also helps you to stave off potential problems or troubleshoot past ones.</span><span class="sxs-lookup"><span data-stu-id="4b197-106">It also helps you to stave off potential problems or troubleshoot past ones.</span></span> <span data-ttu-id="4b197-107">In addition, you can use monitoring data to gain deep insights about your application.</span><span class="sxs-lookup"><span data-stu-id="4b197-107">In addition, you can use monitoring data to gain deep insights about your application.</span></span> <span data-ttu-id="4b197-108">This knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span><span class="sxs-lookup"><span data-stu-id="4b197-108">This knowledge can help you to improve application performance or maintainability, or automate actions that would otherwise require manual intervention.</span></span>

<span data-ttu-id="4b197-109">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="4b197-109">Azure Monitor provides base level infrastructure metrics and logs for most services in Microsoft Azure.</span></span> <span data-ttu-id="4b197-110">For details, see [monitoring overview](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span><span class="sxs-lookup"><span data-stu-id="4b197-110">For details, see [monitoring overview](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor).</span></span> <span data-ttu-id="4b197-111">Azure Diagnostic logs are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span><span class="sxs-lookup"><span data-stu-id="4b197-111">Azure Diagnostic logs are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="4b197-112">Data Factory outputs diagnostic logs in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4b197-112">Data Factory outputs diagnostic logs in Azure Monitor.</span></span>

## <a name="persist-data-factory-data"></a><span data-ttu-id="4b197-113">Persist Data Factory Data</span><span class="sxs-lookup"><span data-stu-id="4b197-113">Persist Data Factory Data</span></span>
<span data-ttu-id="4b197-114">Data Factory only stores pipeline run data for 45 days.</span><span class="sxs-lookup"><span data-stu-id="4b197-114">Data Factory only stores pipeline run data for 45 days.</span></span> <span data-ttu-id="4b197-115">If you want to persist pipeline run data for more than 45 days, using Azure Monitor, you can not only route diagnostic logs for analysis, you can persist them into a storage account so you have factory information for the duration of your choosing.</span><span class="sxs-lookup"><span data-stu-id="4b197-115">If you want to persist pipeline run data for more than 45 days, using Azure Monitor, you can not only route diagnostic logs for analysis, you can persist them into a storage account so you have factory information for the duration of your choosing.</span></span>

## <a name="diagnostic-logs"></a><span data-ttu-id="4b197-116">Diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="4b197-116">Diagnostic logs</span></span>

* <span data-ttu-id="4b197-117">Save them to a **Storage Account** for auditing or manual inspection.</span><span class="sxs-lookup"><span data-stu-id="4b197-117">Save them to a **Storage Account** for auditing or manual inspection.</span></span> <span data-ttu-id="4b197-118">You can specify the retention time (in days) using the diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="4b197-118">You can specify the retention time (in days) using the diagnostic settings.</span></span>
* <span data-ttu-id="4b197-119">Stream them to **Event Hubs** for ingestion by a third-party service or custom analytics solution such as PowerBI.</span><span class="sxs-lookup"><span data-stu-id="4b197-119">Stream them to **Event Hubs** for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="4b197-120">Analyze them with **Log Analytics**</span><span class="sxs-lookup"><span data-stu-id="4b197-120">Analyze them with **Log Analytics**</span></span>

<span data-ttu-id="4b197-121">You can use a storage account or event hub namespace that is not in the same subscription as the resource that is emitting logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-121">You can use a storage account or event hub namespace that is not in the same subscription as the resource that is emitting logs.</span></span> <span data-ttu-id="4b197-122">The user who configures the setting must have the appropriate role-based access control (RBAC) access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="4b197-122">The user who configures the setting must have the appropriate role-based access control (RBAC) access to both subscriptions.</span></span>

## <a name="set-up-diagnostic-logs"></a><span data-ttu-id="4b197-123">Set up diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="4b197-123">Set up diagnostic logs</span></span>

### <a name="diagnostic-settings"></a><span data-ttu-id="4b197-124">Diagnostic Settings</span><span class="sxs-lookup"><span data-stu-id="4b197-124">Diagnostic Settings</span></span>
<span data-ttu-id="4b197-125">Diagnostic Logs for non-compute resources are configured using diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="4b197-125">Diagnostic Logs for non-compute resources are configured using diagnostic settings.</span></span> <span data-ttu-id="4b197-126">Diagnostic settings for a resource control:</span><span class="sxs-lookup"><span data-stu-id="4b197-126">Diagnostic settings for a resource control:</span></span>

* <span data-ttu-id="4b197-127">Where diagnostic logs are sent (Storage Account, Event Hubs, and/or Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="4b197-127">Where diagnostic logs are sent (Storage Account, Event Hubs, and/or Log Analytics).</span></span>
* <span data-ttu-id="4b197-128">Which log categories are sent.</span><span class="sxs-lookup"><span data-stu-id="4b197-128">Which log categories are sent.</span></span>
* <span data-ttu-id="4b197-129">How long each log category should be retained in a storage account</span><span class="sxs-lookup"><span data-stu-id="4b197-129">How long each log category should be retained in a storage account</span></span>
* <span data-ttu-id="4b197-130">A retention of zero days means logs are kept forever.</span><span class="sxs-lookup"><span data-stu-id="4b197-130">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="4b197-131">Otherwise, the value can be any number of days between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="4b197-131">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
* <span data-ttu-id="4b197-132">If retention policies are set but storing logs in a storage account is disabled (for example, only Event Hubs or Log Analytics options are selected), the retention policies have no effect.</span><span class="sxs-lookup"><span data-stu-id="4b197-132">If retention policies are set but storing logs in a storage account is disabled (for example, only Event Hubs or Log Analytics options are selected), the retention policies have no effect.</span></span>
* <span data-ttu-id="4b197-133">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span><span class="sxs-lookup"><span data-stu-id="4b197-133">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="4b197-134">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span><span class="sxs-lookup"><span data-stu-id="4b197-134">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

### <a name="enable-diagnostic-logs-via-rest-apis"></a><span data-ttu-id="4b197-135">Enable diagnostic logs via REST APIs</span><span class="sxs-lookup"><span data-stu-id="4b197-135">Enable diagnostic logs via REST APIs</span></span>

<span data-ttu-id="4b197-136">Create or update a diagnostics setting in Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="4b197-136">Create or update a diagnostics setting in Azure Monitor REST API</span></span>

<span data-ttu-id="4b197-137">**Request**</span><span class="sxs-lookup"><span data-stu-id="4b197-137">**Request**</span></span>
```
PUT
https://management.azure.com/{resource-id}/providers/microsoft.insights/diagnosticSettings/service?api-version={api-version}
```

<span data-ttu-id="4b197-138">**Headers**</span><span class="sxs-lookup"><span data-stu-id="4b197-138">**Headers**</span></span>
* <span data-ttu-id="4b197-139">Replace `{api-version}` with `2016-09-01`.</span><span class="sxs-lookup"><span data-stu-id="4b197-139">Replace `{api-version}` with `2016-09-01`.</span></span>
* <span data-ttu-id="4b197-140">Replace `{resource-id}` with the resource ID of the resource for which you would like to edit diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="4b197-140">Replace `{resource-id}` with the resource ID of the resource for which you would like to edit diagnostic settings.</span></span> <span data-ttu-id="4b197-141">For more information [Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b197-141">For more information [Using Resource groups to manage your Azure resources](../azure-resource-manager/resource-group-portal.md).</span></span>
* <span data-ttu-id="4b197-142">Set the `Content-Type` header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="4b197-142">Set the `Content-Type` header to `application/json`.</span></span>
* <span data-ttu-id="4b197-143">Set the authorization header to a JSON web token that you obtain from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b197-143">Set the authorization header to a JSON web token that you obtain from Azure Active Directory.</span></span> <span data-ttu-id="4b197-144">For more information, see [Authenticating requests](../active-directory/develop/authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="4b197-144">For more information, see [Authenticating requests](../active-directory/develop/authentication-scenarios.md).</span></span>

<span data-ttu-id="4b197-145">**Body**</span><span class="sxs-lookup"><span data-stu-id="4b197-145">**Body**</span></span>
```json
{
    "properties": {
        "storageAccountId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Storage/storageAccounts/<storageAccountName>",
        "serviceBusRuleId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>/providers/Microsoft.EventHub/namespaces/<eventHubName>/authorizationrules/RootManageSharedAccessKey",
        "workspaceId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>/providers/Microsoft.OperationalInsights/workspaces/<LogAnalyticsName>",
        "metrics": [
        ],
        "logs": [
                {
                    "category": "PipelineRuns",
                    "enabled": true,
                    "retentionPolicy": {
                        "enabled": false,
                        "days": 0
                    }
                },
                {
                    "category": "TriggerRuns",
                    "enabled": true,
                    "retentionPolicy": {
                        "enabled": false,
                        "days": 0
                    }
                },
                {
                    "category": "ActivityRuns",
                    "enabled": true,
                    "retentionPolicy": {
                        "enabled": false,
                        "days": 0
                    }
                }
            ]
    },
    "location": ""
}
```

| <span data-ttu-id="4b197-146">Property</span><span class="sxs-lookup"><span data-stu-id="4b197-146">Property</span></span> | <span data-ttu-id="4b197-147">Type</span><span class="sxs-lookup"><span data-stu-id="4b197-147">Type</span></span> | <span data-ttu-id="4b197-148">Description</span><span class="sxs-lookup"><span data-stu-id="4b197-148">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b197-149">storageAccountId</span><span class="sxs-lookup"><span data-stu-id="4b197-149">storageAccountId</span></span> |<span data-ttu-id="4b197-150">String</span><span class="sxs-lookup"><span data-stu-id="4b197-150">String</span></span> | <span data-ttu-id="4b197-151">The resource ID of the storage account to which you would like to send Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="4b197-151">The resource ID of the storage account to which you would like to send Diagnostic Logs</span></span> |
| <span data-ttu-id="4b197-152">serviceBusRuleId</span><span class="sxs-lookup"><span data-stu-id="4b197-152">serviceBusRuleId</span></span> |<span data-ttu-id="4b197-153">String</span><span class="sxs-lookup"><span data-stu-id="4b197-153">String</span></span> | <span data-ttu-id="4b197-154">The service bus rule ID of the service bus namespace in which you would like to have Event Hubs created for streaming Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-154">The service bus rule ID of the service bus namespace in which you would like to have Event Hubs created for streaming Diagnostic Logs.</span></span> <span data-ttu-id="4b197-155">The rule ID is of the format: "{service bus resource ID}/authorizationrules/{key name}".</span><span class="sxs-lookup"><span data-stu-id="4b197-155">The rule ID is of the format: "{service bus resource ID}/authorizationrules/{key name}".</span></span>|
| <span data-ttu-id="4b197-156">workspaceId</span><span class="sxs-lookup"><span data-stu-id="4b197-156">workspaceId</span></span> | <span data-ttu-id="4b197-157">Complex Type</span><span class="sxs-lookup"><span data-stu-id="4b197-157">Complex Type</span></span> | <span data-ttu-id="4b197-158">Array of metric time grains and their retention policies.</span><span class="sxs-lookup"><span data-stu-id="4b197-158">Array of metric time grains and their retention policies.</span></span> <span data-ttu-id="4b197-159">Currently, this property is empty.</span><span class="sxs-lookup"><span data-stu-id="4b197-159">Currently, this property is empty.</span></span> |
|<span data-ttu-id="4b197-160">metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-160">metrics</span></span>| <span data-ttu-id="4b197-161">Parameter values of the pipeline run to be passed to the invoked pipeline</span><span class="sxs-lookup"><span data-stu-id="4b197-161">Parameter values of the pipeline run to be passed to the invoked pipeline</span></span>| <span data-ttu-id="4b197-162">A JSON object mapping parameter names to argument values</span><span class="sxs-lookup"><span data-stu-id="4b197-162">A JSON object mapping parameter names to argument values</span></span> |
| <span data-ttu-id="4b197-163">logs</span><span class="sxs-lookup"><span data-stu-id="4b197-163">logs</span></span>| <span data-ttu-id="4b197-164">Complex Type</span><span class="sxs-lookup"><span data-stu-id="4b197-164">Complex Type</span></span>| <span data-ttu-id="4b197-165">Name of a Diagnostic Log category for a resource type.</span><span class="sxs-lookup"><span data-stu-id="4b197-165">Name of a Diagnostic Log category for a resource type.</span></span> <span data-ttu-id="4b197-166">To obtain the list of Diagnostic Log categories for a resource, first perform a GET diagnostic settings operation.</span><span class="sxs-lookup"><span data-stu-id="4b197-166">To obtain the list of Diagnostic Log categories for a resource, first perform a GET diagnostic settings operation.</span></span> |
| <span data-ttu-id="4b197-167">category</span><span class="sxs-lookup"><span data-stu-id="4b197-167">category</span></span>| <span data-ttu-id="4b197-168">String</span><span class="sxs-lookup"><span data-stu-id="4b197-168">String</span></span>| <span data-ttu-id="4b197-169">Array of log categories and their retention policies</span><span class="sxs-lookup"><span data-stu-id="4b197-169">Array of log categories and their retention policies</span></span> |
| <span data-ttu-id="4b197-170">timeGrain</span><span class="sxs-lookup"><span data-stu-id="4b197-170">timeGrain</span></span> | <span data-ttu-id="4b197-171">String</span><span class="sxs-lookup"><span data-stu-id="4b197-171">String</span></span> | <span data-ttu-id="4b197-172">The granularity of metrics that are captured in ISO 8601 duration format.</span><span class="sxs-lookup"><span data-stu-id="4b197-172">The granularity of metrics that are captured in ISO 8601 duration format.</span></span> <span data-ttu-id="4b197-173">Must be PT1M (one minute)</span><span class="sxs-lookup"><span data-stu-id="4b197-173">Must be PT1M (one minute)</span></span>|
| <span data-ttu-id="4b197-174">enabled</span><span class="sxs-lookup"><span data-stu-id="4b197-174">enabled</span></span>| <span data-ttu-id="4b197-175">Boolean</span><span class="sxs-lookup"><span data-stu-id="4b197-175">Boolean</span></span> | <span data-ttu-id="4b197-176">Specifies whether collection of that metric or log category is enabled for this resource</span><span class="sxs-lookup"><span data-stu-id="4b197-176">Specifies whether collection of that metric or log category is enabled for this resource</span></span>|
| <span data-ttu-id="4b197-177">retentionPolicy</span><span class="sxs-lookup"><span data-stu-id="4b197-177">retentionPolicy</span></span>| <span data-ttu-id="4b197-178">Complex Type</span><span class="sxs-lookup"><span data-stu-id="4b197-178">Complex Type</span></span>| <span data-ttu-id="4b197-179">Describes the retention policy for a metric or log category.</span><span class="sxs-lookup"><span data-stu-id="4b197-179">Describes the retention policy for a metric or log category.</span></span> <span data-ttu-id="4b197-180">Used for storage account option only.</span><span class="sxs-lookup"><span data-stu-id="4b197-180">Used for storage account option only.</span></span>|
| <span data-ttu-id="4b197-181">days</span><span class="sxs-lookup"><span data-stu-id="4b197-181">days</span></span>| <span data-ttu-id="4b197-182">Int</span><span class="sxs-lookup"><span data-stu-id="4b197-182">Int</span></span>| <span data-ttu-id="4b197-183">Number of days to retain the metrics or logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-183">Number of days to retain the metrics or logs.</span></span> <span data-ttu-id="4b197-184">A value of 0 retains the logs indefinitely.</span><span class="sxs-lookup"><span data-stu-id="4b197-184">A value of 0 retains the logs indefinitely.</span></span> <span data-ttu-id="4b197-185">Used for storage account option only.</span><span class="sxs-lookup"><span data-stu-id="4b197-185">Used for storage account option only.</span></span> |

<span data-ttu-id="4b197-186">**Response**</span><span class="sxs-lookup"><span data-stu-id="4b197-186">**Response**</span></span>

<span data-ttu-id="4b197-187">200 OK</span><span class="sxs-lookup"><span data-stu-id="4b197-187">200 OK</span></span>


```json
{
    "id": "/subscriptions/<subID>/resourcegroups/adf/providers/microsoft.datafactory/factories/shloadobetest2/providers/microsoft.insights/diagnosticSettings/service",
    "type": null,
    "name": "service",
    "location": null,
    "kind": null,
    "tags": null,
    "properties": {
        "storageAccountId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>//providers/Microsoft.Storage/storageAccounts/<storageAccountName>",
        "serviceBusRuleId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>//providers/Microsoft.EventHub/namespaces/<eventHubName>/authorizationrules/RootManageSharedAccessKey",
        "workspaceId": "/subscriptions/<subID>/resourceGroups/<resourceGroupName>//providers/Microsoft.OperationalInsights/workspaces/<LogAnalyticsName>",
        "eventHubAuthorizationRuleId": null,
        "eventHubName": null,
        "metrics": [],
        "logs": [
            {
                "category": "PipelineRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            },
            {
                "category": "TriggerRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            },
            {
                "category": "ActivityRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            }
        ]
    },
    "identity": null
}
```

<span data-ttu-id="4b197-188">Get information about diagnostics setting in Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="4b197-188">Get information about diagnostics setting in Azure Monitor REST API</span></span>

<span data-ttu-id="4b197-189">**Request**</span><span class="sxs-lookup"><span data-stu-id="4b197-189">**Request**</span></span>
```
GET
https://management.azure.com/{resource-id}/providers/microsoft.insights/diagnosticSettings/service?api-version={api-version}
```

<span data-ttu-id="4b197-190">**Headers**</span><span class="sxs-lookup"><span data-stu-id="4b197-190">**Headers**</span></span>
* <span data-ttu-id="4b197-191">Replace `{api-version}` with `2016-09-01`.</span><span class="sxs-lookup"><span data-stu-id="4b197-191">Replace `{api-version}` with `2016-09-01`.</span></span>
* <span data-ttu-id="4b197-192">Replace `{resource-id}` with the resource ID of the resource for which you would like to edit diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="4b197-192">Replace `{resource-id}` with the resource ID of the resource for which you would like to edit diagnostic settings.</span></span> <span data-ttu-id="4b197-193">For more information Using Resource groups to manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4b197-193">For more information Using Resource groups to manage your Azure resources.</span></span>
* <span data-ttu-id="4b197-194">Set the `Content-Type` header to `application/json`.</span><span class="sxs-lookup"><span data-stu-id="4b197-194">Set the `Content-Type` header to `application/json`.</span></span>
* <span data-ttu-id="4b197-195">Set the authorization header to a JSON Web Token that you obtain from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b197-195">Set the authorization header to a JSON Web Token that you obtain from Azure Active Directory.</span></span> <span data-ttu-id="4b197-196">For more information, see Authenticating requests.</span><span class="sxs-lookup"><span data-stu-id="4b197-196">For more information, see Authenticating requests.</span></span>

<span data-ttu-id="4b197-197">**Response**</span><span class="sxs-lookup"><span data-stu-id="4b197-197">**Response**</span></span>

<span data-ttu-id="4b197-198">200 OK</span><span class="sxs-lookup"><span data-stu-id="4b197-198">200 OK</span></span>

```json
{
    "id": "/subscriptions/<subID>/resourcegroups/adf/providers/microsoft.datafactory/factories/shloadobetest2/providers/microsoft.insights/diagnosticSettings/service",
    "type": null,
    "name": "service",
    "location": null,
    "kind": null,
    "tags": null,
    "properties": {
        "storageAccountId": "/subscriptions/<subID>/resourceGroups/shloprivate/providers/Microsoft.Storage/storageAccounts/azmonlogs",
        "serviceBusRuleId": "/subscriptions/<subID>/resourceGroups/shloprivate/providers/Microsoft.EventHub/namespaces/shloeventhub/authorizationrules/RootManageSharedAccessKey",
        "workspaceId": "/subscriptions/<subID>/resourceGroups/ADF/providers/Microsoft.OperationalInsights/workspaces/mihaipie",
        "eventHubAuthorizationRuleId": null,
        "eventHubName": null,
        "metrics": [],
        "logs": [
            {
                "category": "PipelineRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            },
            {
                "category": "TriggerRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            },
            {
                "category": "ActivityRuns",
                "enabled": true,
                "retentionPolicy": {
                    "enabled": false,
                    "days": 0
                }
            }
        ]
    },
    "identity": null
}
```
[<span data-ttu-id="4b197-199">More info here</span><span class="sxs-lookup"><span data-stu-id="4b197-199">More info here</span></span>](https://docs.microsoft.com/en-us/rest/api/monitor/diagnosticsettings)

## <a name="schema-of-logs--events"></a><span data-ttu-id="4b197-200">Schema of Logs & Events</span><span class="sxs-lookup"><span data-stu-id="4b197-200">Schema of Logs & Events</span></span>

### <a name="activity-run-logs-attributes"></a><span data-ttu-id="4b197-201">Activity Run Logs Attributes</span><span class="sxs-lookup"><span data-stu-id="4b197-201">Activity Run Logs Attributes</span></span>

```json
{
   "Level": "",
   "correlationId":"",
   "time":"",
   "activityRunId":"",
   "pipelineRunId":"",
   "resourceId":"",
   "category":"ActivityRuns",
   "level":"Informational",
   "operationName":"",
   "pipelineName":"",
   "activityName":"",
   "start":"",
   "end":"",
   "properties:"
       {
          "Input": "{
              "source": {
                "type": "BlobSource"
              },
              "sink": {
                "type": "BlobSink"
              }
           }",
          "Output": "{"dataRead":121,"dataWritten":121,"copyDuration":5,
               "throughput":0.0236328132,"errors":[]}",
          "Error": "{
              "errorCode": "null",
              "message": "null",
              "failureType": "null",
              "target": "CopyBlobtoBlob"
        }
    }
}
```

| <span data-ttu-id="4b197-202">Property</span><span class="sxs-lookup"><span data-stu-id="4b197-202">Property</span></span> | <span data-ttu-id="4b197-203">Type</span><span class="sxs-lookup"><span data-stu-id="4b197-203">Type</span></span> | <span data-ttu-id="4b197-204">Description</span><span class="sxs-lookup"><span data-stu-id="4b197-204">Description</span></span> | <span data-ttu-id="4b197-205">Example</span><span class="sxs-lookup"><span data-stu-id="4b197-205">Example</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b197-206">Level</span><span class="sxs-lookup"><span data-stu-id="4b197-206">Level</span></span> |<span data-ttu-id="4b197-207">String</span><span class="sxs-lookup"><span data-stu-id="4b197-207">String</span></span> | <span data-ttu-id="4b197-208">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-208">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-209">Level 4 always is the case for activity run logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-209">Level 4 always is the case for activity run logs.</span></span> | `4`  |
| <span data-ttu-id="4b197-210">correlationId</span><span class="sxs-lookup"><span data-stu-id="4b197-210">correlationId</span></span> |<span data-ttu-id="4b197-211">String</span><span class="sxs-lookup"><span data-stu-id="4b197-211">String</span></span> | <span data-ttu-id="4b197-212">Unique ID to track a particular request end-to-end</span><span class="sxs-lookup"><span data-stu-id="4b197-212">Unique ID to track a particular request end-to-end</span></span> | `319dc6b4-f348-405e-b8d7-aafc77b73e77` |
| <span data-ttu-id="4b197-213">time</span><span class="sxs-lookup"><span data-stu-id="4b197-213">time</span></span> | <span data-ttu-id="4b197-214">String</span><span class="sxs-lookup"><span data-stu-id="4b197-214">String</span></span> | <span data-ttu-id="4b197-215">Time of the event in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-215">Time of the event in timespan, UTC format</span></span> | `YYYY-MM-DDTHH:MM:SS.00000Z` | `2017-06-28T21:00:27.3534352Z` |
|<span data-ttu-id="4b197-216">activityRunId</span><span class="sxs-lookup"><span data-stu-id="4b197-216">activityRunId</span></span>| <span data-ttu-id="4b197-217">String</span><span class="sxs-lookup"><span data-stu-id="4b197-217">String</span></span>| <span data-ttu-id="4b197-218">ID of the activity run</span><span class="sxs-lookup"><span data-stu-id="4b197-218">ID of the activity run</span></span> | `3a171e1f-b36e-4b80-8a54-5625394f4354` |
|<span data-ttu-id="4b197-219">pipelineRunId</span><span class="sxs-lookup"><span data-stu-id="4b197-219">pipelineRunId</span></span>| <span data-ttu-id="4b197-220">String</span><span class="sxs-lookup"><span data-stu-id="4b197-220">String</span></span>| <span data-ttu-id="4b197-221">ID of the pipeline run</span><span class="sxs-lookup"><span data-stu-id="4b197-221">ID of the pipeline run</span></span> | `9f6069d6-e522-4608-9f99-21807bfc3c70` |
|<span data-ttu-id="4b197-222">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b197-222">resourceId</span></span>| <span data-ttu-id="4b197-223">String</span><span class="sxs-lookup"><span data-stu-id="4b197-223">String</span></span> | <span data-ttu-id="4b197-224">Associated resource ID for the data factory resource</span><span class="sxs-lookup"><span data-stu-id="4b197-224">Associated resource ID for the data factory resource</span></span> | `/SUBSCRIPTIONS/<subID>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/FACTORIES/<dataFactoryName>` |
|<span data-ttu-id="4b197-225">category</span><span class="sxs-lookup"><span data-stu-id="4b197-225">category</span></span>| <span data-ttu-id="4b197-226">String</span><span class="sxs-lookup"><span data-stu-id="4b197-226">String</span></span> | <span data-ttu-id="4b197-227">Category of Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-227">Category of Diagnostic Logs.</span></span> <span data-ttu-id="4b197-228">Set this property to "ActivityRuns"</span><span class="sxs-lookup"><span data-stu-id="4b197-228">Set this property to "ActivityRuns"</span></span> | `ActivityRuns` |
|<span data-ttu-id="4b197-229">level</span><span class="sxs-lookup"><span data-stu-id="4b197-229">level</span></span>| <span data-ttu-id="4b197-230">String</span><span class="sxs-lookup"><span data-stu-id="4b197-230">String</span></span> | <span data-ttu-id="4b197-231">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-231">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-232">Set this property to "Informational"</span><span class="sxs-lookup"><span data-stu-id="4b197-232">Set this property to "Informational"</span></span> | `Informational` |
|<span data-ttu-id="4b197-233">operationName</span><span class="sxs-lookup"><span data-stu-id="4b197-233">operationName</span></span>| <span data-ttu-id="4b197-234">String</span><span class="sxs-lookup"><span data-stu-id="4b197-234">String</span></span> |<span data-ttu-id="4b197-235">Name of the activity with status.</span><span class="sxs-lookup"><span data-stu-id="4b197-235">Name of the activity with status.</span></span> <span data-ttu-id="4b197-236">If the status is the start heartbeat, it is `MyActivity -`.</span><span class="sxs-lookup"><span data-stu-id="4b197-236">If the status is the start heartbeat, it is `MyActivity -`.</span></span> <span data-ttu-id="4b197-237">If the status is the end heartbeat, it is `MyActivity - Succeeded` with final status</span><span class="sxs-lookup"><span data-stu-id="4b197-237">If the status is the end heartbeat, it is `MyActivity - Succeeded` with final status</span></span> | `MyActivity - Succeeded` |
|<span data-ttu-id="4b197-238">pipelineName</span><span class="sxs-lookup"><span data-stu-id="4b197-238">pipelineName</span></span>| <span data-ttu-id="4b197-239">String</span><span class="sxs-lookup"><span data-stu-id="4b197-239">String</span></span> | <span data-ttu-id="4b197-240">Name of the pipeline</span><span class="sxs-lookup"><span data-stu-id="4b197-240">Name of the pipeline</span></span> | `MyPipeline` |
|<span data-ttu-id="4b197-241">activityName</span><span class="sxs-lookup"><span data-stu-id="4b197-241">activityName</span></span>| <span data-ttu-id="4b197-242">String</span><span class="sxs-lookup"><span data-stu-id="4b197-242">String</span></span> | <span data-ttu-id="4b197-243">Name of the activity</span><span class="sxs-lookup"><span data-stu-id="4b197-243">Name of the activity</span></span> | `MyActivity` |
|<span data-ttu-id="4b197-244">start</span><span class="sxs-lookup"><span data-stu-id="4b197-244">start</span></span>| <span data-ttu-id="4b197-245">String</span><span class="sxs-lookup"><span data-stu-id="4b197-245">String</span></span> | <span data-ttu-id="4b197-246">Start of the activity run in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-246">Start of the activity run in timespan, UTC format</span></span> | `2017-06-26T20:55:29.5007959Z`|
|<span data-ttu-id="4b197-247">end</span><span class="sxs-lookup"><span data-stu-id="4b197-247">end</span></span>| <span data-ttu-id="4b197-248">String</span><span class="sxs-lookup"><span data-stu-id="4b197-248">String</span></span> | <span data-ttu-id="4b197-249">Ends of the activity run in timespan, UTC format.</span><span class="sxs-lookup"><span data-stu-id="4b197-249">Ends of the activity run in timespan, UTC format.</span></span> <span data-ttu-id="4b197-250">If the activity has not ended yet (diagnostic log for an activity starting), a default value of `1601-01-01T00:00:00Z` is set.</span><span class="sxs-lookup"><span data-stu-id="4b197-250">If the activity has not ended yet (diagnostic log for an activity starting), a default value of `1601-01-01T00:00:00Z` is set.</span></span>  | `2017-06-26T20:55:29.5007959Z` |


### <a name="pipeline-run-logs-attributes"></a><span data-ttu-id="4b197-251">Pipeline Run Logs Attributes</span><span class="sxs-lookup"><span data-stu-id="4b197-251">Pipeline Run Logs Attributes</span></span>

```json
{
   "Level": "",
   "correlationId":"",
   "time":"",
   "runId":"",
   "resourceId":"",
   "category":"PipelineRuns",
   "level":"Informational",
   "operationName":"",
   "pipelineName":"",
   "start":"",
   "end":"",
   "status":"",
   "properties":
    {
      "Parameters": {
        "<parameter1Name>": "<parameter1Value>"
      },
      "SystemParameters": {
        "ExecutionStart": "",
        "TriggerId": "",
        "SubscriptionId": ""
      }
    }
}
```

| <span data-ttu-id="4b197-252">Property</span><span class="sxs-lookup"><span data-stu-id="4b197-252">Property</span></span> | <span data-ttu-id="4b197-253">Type</span><span class="sxs-lookup"><span data-stu-id="4b197-253">Type</span></span> | <span data-ttu-id="4b197-254">Description</span><span class="sxs-lookup"><span data-stu-id="4b197-254">Description</span></span> | <span data-ttu-id="4b197-255">Example</span><span class="sxs-lookup"><span data-stu-id="4b197-255">Example</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b197-256">Level</span><span class="sxs-lookup"><span data-stu-id="4b197-256">Level</span></span> |<span data-ttu-id="4b197-257">String</span><span class="sxs-lookup"><span data-stu-id="4b197-257">String</span></span> | <span data-ttu-id="4b197-258">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-258">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-259">Level 4 is the case for activity run logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-259">Level 4 is the case for activity run logs.</span></span> | `4`  |
| <span data-ttu-id="4b197-260">correlationId</span><span class="sxs-lookup"><span data-stu-id="4b197-260">correlationId</span></span> |<span data-ttu-id="4b197-261">String</span><span class="sxs-lookup"><span data-stu-id="4b197-261">String</span></span> | <span data-ttu-id="4b197-262">Unique ID to track a particular request end-to-end</span><span class="sxs-lookup"><span data-stu-id="4b197-262">Unique ID to track a particular request end-to-end</span></span> | `319dc6b4-f348-405e-b8d7-aafc77b73e77` |
| <span data-ttu-id="4b197-263">time</span><span class="sxs-lookup"><span data-stu-id="4b197-263">time</span></span> | <span data-ttu-id="4b197-264">String</span><span class="sxs-lookup"><span data-stu-id="4b197-264">String</span></span> | <span data-ttu-id="4b197-265">Time of the event in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-265">Time of the event in timespan, UTC format</span></span> | `YYYY-MM-DDTHH:MM:SS.00000Z` | `2017-06-28T21:00:27.3534352Z` |
|<span data-ttu-id="4b197-266">runId</span><span class="sxs-lookup"><span data-stu-id="4b197-266">runId</span></span>| <span data-ttu-id="4b197-267">String</span><span class="sxs-lookup"><span data-stu-id="4b197-267">String</span></span>| <span data-ttu-id="4b197-268">ID of the pipeline run</span><span class="sxs-lookup"><span data-stu-id="4b197-268">ID of the pipeline run</span></span> | `9f6069d6-e522-4608-9f99-21807bfc3c70` |
|<span data-ttu-id="4b197-269">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b197-269">resourceId</span></span>| <span data-ttu-id="4b197-270">String</span><span class="sxs-lookup"><span data-stu-id="4b197-270">String</span></span> | <span data-ttu-id="4b197-271">Associated resource ID for the data factory resource</span><span class="sxs-lookup"><span data-stu-id="4b197-271">Associated resource ID for the data factory resource</span></span> | `/SUBSCRIPTIONS/<subID>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/FACTORIES/<dataFactoryName>` |
|<span data-ttu-id="4b197-272">category</span><span class="sxs-lookup"><span data-stu-id="4b197-272">category</span></span>| <span data-ttu-id="4b197-273">String</span><span class="sxs-lookup"><span data-stu-id="4b197-273">String</span></span> | <span data-ttu-id="4b197-274">Category of Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-274">Category of Diagnostic Logs.</span></span> <span data-ttu-id="4b197-275">Set this property to "PipelineRuns"</span><span class="sxs-lookup"><span data-stu-id="4b197-275">Set this property to "PipelineRuns"</span></span> | `PipelineRuns` |
|<span data-ttu-id="4b197-276">level</span><span class="sxs-lookup"><span data-stu-id="4b197-276">level</span></span>| <span data-ttu-id="4b197-277">String</span><span class="sxs-lookup"><span data-stu-id="4b197-277">String</span></span> | <span data-ttu-id="4b197-278">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-278">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-279">Set this property to  "Informational"</span><span class="sxs-lookup"><span data-stu-id="4b197-279">Set this property to  "Informational"</span></span> | `Informational` |
|<span data-ttu-id="4b197-280">operationName</span><span class="sxs-lookup"><span data-stu-id="4b197-280">operationName</span></span>| <span data-ttu-id="4b197-281">String</span><span class="sxs-lookup"><span data-stu-id="4b197-281">String</span></span> |<span data-ttu-id="4b197-282">Name of the pipeline with status.</span><span class="sxs-lookup"><span data-stu-id="4b197-282">Name of the pipeline with status.</span></span> <span data-ttu-id="4b197-283">"Pipeline - Succeeded" with final status when pipeline run is completed</span><span class="sxs-lookup"><span data-stu-id="4b197-283">"Pipeline - Succeeded" with final status when pipeline run is completed</span></span>| `MyPipeline - Succeeded` |
|<span data-ttu-id="4b197-284">pipelineName</span><span class="sxs-lookup"><span data-stu-id="4b197-284">pipelineName</span></span>| <span data-ttu-id="4b197-285">String</span><span class="sxs-lookup"><span data-stu-id="4b197-285">String</span></span> | <span data-ttu-id="4b197-286">Name of the pipeline</span><span class="sxs-lookup"><span data-stu-id="4b197-286">Name of the pipeline</span></span> | `MyPipeline` |
|<span data-ttu-id="4b197-287">start</span><span class="sxs-lookup"><span data-stu-id="4b197-287">start</span></span>| <span data-ttu-id="4b197-288">String</span><span class="sxs-lookup"><span data-stu-id="4b197-288">String</span></span> | <span data-ttu-id="4b197-289">Start of the activity run in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-289">Start of the activity run in timespan, UTC format</span></span> | `2017-06-26T20:55:29.5007959Z`|
|<span data-ttu-id="4b197-290">end</span><span class="sxs-lookup"><span data-stu-id="4b197-290">end</span></span>| <span data-ttu-id="4b197-291">String</span><span class="sxs-lookup"><span data-stu-id="4b197-291">String</span></span> | <span data-ttu-id="4b197-292">End of the activity runs in timespan, UTC format.</span><span class="sxs-lookup"><span data-stu-id="4b197-292">End of the activity runs in timespan, UTC format.</span></span> <span data-ttu-id="4b197-293">If the activity has not ended yet (diagnostic log for an activity starting), a default value of `1601-01-01T00:00:00Z` is set.</span><span class="sxs-lookup"><span data-stu-id="4b197-293">If the activity has not ended yet (diagnostic log for an activity starting), a default value of `1601-01-01T00:00:00Z` is set.</span></span>  | `2017-06-26T20:55:29.5007959Z` |
|<span data-ttu-id="4b197-294">status</span><span class="sxs-lookup"><span data-stu-id="4b197-294">status</span></span>| <span data-ttu-id="4b197-295">String</span><span class="sxs-lookup"><span data-stu-id="4b197-295">String</span></span> | <span data-ttu-id="4b197-296">Final status of the pipeline run (Succeeded or Failed)</span><span class="sxs-lookup"><span data-stu-id="4b197-296">Final status of the pipeline run (Succeeded or Failed)</span></span> | `Succeeded`|


### <a name="trigger-run-logs-attributes"></a><span data-ttu-id="4b197-297">Trigger Run Logs Attributes</span><span class="sxs-lookup"><span data-stu-id="4b197-297">Trigger Run Logs Attributes</span></span>

```json
{
   "Level": "",
   "correlationId":"",
   "time":"",
   "triggerId":"",
   "resourceId":"",
   "category":"TriggerRuns",
   "level":"Informational",
   "operationName":"",
   "triggerName":"",
   "triggerType":"",
   "triggerEvent":"",
   "start":"",
   "status":"",
   "properties":
   {
      "Parameters": {
        "TriggerTime": "",
       "ScheduleTime": ""
      },
      "SystemParameters": {}
    }
}

```

| <span data-ttu-id="4b197-298">Property</span><span class="sxs-lookup"><span data-stu-id="4b197-298">Property</span></span> | <span data-ttu-id="4b197-299">Type</span><span class="sxs-lookup"><span data-stu-id="4b197-299">Type</span></span> | <span data-ttu-id="4b197-300">Description</span><span class="sxs-lookup"><span data-stu-id="4b197-300">Description</span></span> | <span data-ttu-id="4b197-301">Example</span><span class="sxs-lookup"><span data-stu-id="4b197-301">Example</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b197-302">Level</span><span class="sxs-lookup"><span data-stu-id="4b197-302">Level</span></span> |<span data-ttu-id="4b197-303">String</span><span class="sxs-lookup"><span data-stu-id="4b197-303">String</span></span> | <span data-ttu-id="4b197-304">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-304">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-305">Set to level 4 for activity run logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-305">Set to level 4 for activity run logs.</span></span> | `4`  |
| <span data-ttu-id="4b197-306">correlationId</span><span class="sxs-lookup"><span data-stu-id="4b197-306">correlationId</span></span> |<span data-ttu-id="4b197-307">String</span><span class="sxs-lookup"><span data-stu-id="4b197-307">String</span></span> | <span data-ttu-id="4b197-308">Unique ID to track a particular request end-to-end</span><span class="sxs-lookup"><span data-stu-id="4b197-308">Unique ID to track a particular request end-to-end</span></span> | `319dc6b4-f348-405e-b8d7-aafc77b73e77` |
| <span data-ttu-id="4b197-309">time</span><span class="sxs-lookup"><span data-stu-id="4b197-309">time</span></span> | <span data-ttu-id="4b197-310">String</span><span class="sxs-lookup"><span data-stu-id="4b197-310">String</span></span> | <span data-ttu-id="4b197-311">Time of the event in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-311">Time of the event in timespan, UTC format</span></span> | `YYYY-MM-DDTHH:MM:SS.00000Z` | `2017-06-28T21:00:27.3534352Z` |
|<span data-ttu-id="4b197-312">triggerId</span><span class="sxs-lookup"><span data-stu-id="4b197-312">triggerId</span></span>| <span data-ttu-id="4b197-313">String</span><span class="sxs-lookup"><span data-stu-id="4b197-313">String</span></span>| <span data-ttu-id="4b197-314">ID of the trigger run</span><span class="sxs-lookup"><span data-stu-id="4b197-314">ID of the trigger run</span></span> | `08587023010602533858661257311` |
|<span data-ttu-id="4b197-315">resourceId</span><span class="sxs-lookup"><span data-stu-id="4b197-315">resourceId</span></span>| <span data-ttu-id="4b197-316">String</span><span class="sxs-lookup"><span data-stu-id="4b197-316">String</span></span> | <span data-ttu-id="4b197-317">Associated resource ID for the data factory resource</span><span class="sxs-lookup"><span data-stu-id="4b197-317">Associated resource ID for the data factory resource</span></span> | `/SUBSCRIPTIONS/<subID>/RESOURCEGROUPS/<resourceGroupName>/PROVIDERS/MICROSOFT.DATAFACTORY/FACTORIES/<dataFactoryName>` |
|<span data-ttu-id="4b197-318">category</span><span class="sxs-lookup"><span data-stu-id="4b197-318">category</span></span>| <span data-ttu-id="4b197-319">String</span><span class="sxs-lookup"><span data-stu-id="4b197-319">String</span></span> | <span data-ttu-id="4b197-320">Category of Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-320">Category of Diagnostic Logs.</span></span> <span data-ttu-id="4b197-321">Set this property to "PipelineRuns"</span><span class="sxs-lookup"><span data-stu-id="4b197-321">Set this property to "PipelineRuns"</span></span> | `PipelineRuns` |
|<span data-ttu-id="4b197-322">level</span><span class="sxs-lookup"><span data-stu-id="4b197-322">level</span></span>| <span data-ttu-id="4b197-323">String</span><span class="sxs-lookup"><span data-stu-id="4b197-323">String</span></span> | <span data-ttu-id="4b197-324">Level of the diagnostic logs.</span><span class="sxs-lookup"><span data-stu-id="4b197-324">Level of the diagnostic logs.</span></span> <span data-ttu-id="4b197-325">Set this property to "Informational"</span><span class="sxs-lookup"><span data-stu-id="4b197-325">Set this property to "Informational"</span></span> | `Informational` |
|<span data-ttu-id="4b197-326">operationName</span><span class="sxs-lookup"><span data-stu-id="4b197-326">operationName</span></span>| <span data-ttu-id="4b197-327">String</span><span class="sxs-lookup"><span data-stu-id="4b197-327">String</span></span> |<span data-ttu-id="4b197-328">Name of the trigger with final status whether it successfully fired.</span><span class="sxs-lookup"><span data-stu-id="4b197-328">Name of the trigger with final status whether it successfully fired.</span></span> <span data-ttu-id="4b197-329">"MyTrigger - Succeeded" if the heartbeat was successful</span><span class="sxs-lookup"><span data-stu-id="4b197-329">"MyTrigger - Succeeded" if the heartbeat was successful</span></span>| `MyTrigger - Succeeded` |
|<span data-ttu-id="4b197-330">triggerName</span><span class="sxs-lookup"><span data-stu-id="4b197-330">triggerName</span></span>| <span data-ttu-id="4b197-331">String</span><span class="sxs-lookup"><span data-stu-id="4b197-331">String</span></span> | <span data-ttu-id="4b197-332">Name of the trigger</span><span class="sxs-lookup"><span data-stu-id="4b197-332">Name of the trigger</span></span> | `MyTrigger` |
|<span data-ttu-id="4b197-333">triggerType</span><span class="sxs-lookup"><span data-stu-id="4b197-333">triggerType</span></span>| <span data-ttu-id="4b197-334">String</span><span class="sxs-lookup"><span data-stu-id="4b197-334">String</span></span> | <span data-ttu-id="4b197-335">Type of the trigger (Manual trigger or Schedule Trigger)</span><span class="sxs-lookup"><span data-stu-id="4b197-335">Type of the trigger (Manual trigger or Schedule Trigger)</span></span> | `ScheduleTrigger` |
|<span data-ttu-id="4b197-336">triggerEvent</span><span class="sxs-lookup"><span data-stu-id="4b197-336">triggerEvent</span></span>| <span data-ttu-id="4b197-337">String</span><span class="sxs-lookup"><span data-stu-id="4b197-337">String</span></span> | <span data-ttu-id="4b197-338">Event of the trigger</span><span class="sxs-lookup"><span data-stu-id="4b197-338">Event of the trigger</span></span> | `ScheduleTime - 2017-07-06T01:50:25Z` |
|<span data-ttu-id="4b197-339">start</span><span class="sxs-lookup"><span data-stu-id="4b197-339">start</span></span>| <span data-ttu-id="4b197-340">String</span><span class="sxs-lookup"><span data-stu-id="4b197-340">String</span></span> | <span data-ttu-id="4b197-341">Start of trigger fire in timespan, UTC format</span><span class="sxs-lookup"><span data-stu-id="4b197-341">Start of trigger fire in timespan, UTC format</span></span> | `2017-06-26T20:55:29.5007959Z`|
|<span data-ttu-id="4b197-342">status</span><span class="sxs-lookup"><span data-stu-id="4b197-342">status</span></span>| <span data-ttu-id="4b197-343">String</span><span class="sxs-lookup"><span data-stu-id="4b197-343">String</span></span> | <span data-ttu-id="4b197-344">Final status of whether trigger successfully fired (Succeeded or Failed)</span><span class="sxs-lookup"><span data-stu-id="4b197-344">Final status of whether trigger successfully fired (Succeeded or Failed)</span></span> | `Succeeded`|

## <a name="metrics"></a><span data-ttu-id="4b197-345">Metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-345">Metrics</span></span>

<span data-ttu-id="4b197-346">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span><span class="sxs-lookup"><span data-stu-id="4b197-346">Azure Monitor enables you to consume telemetry to gain visibility into the performance and health of your workloads on Azure.</span></span> <span data-ttu-id="4b197-347">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span><span class="sxs-lookup"><span data-stu-id="4b197-347">The most important type of Azure telemetry data is the metrics (also called performance counters) emitted by most Azure resources.</span></span> <span data-ttu-id="4b197-348">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span><span class="sxs-lookup"><span data-stu-id="4b197-348">Azure Monitor provides several ways to configure and consume these metrics for monitoring and troubleshooting.</span></span>

<span data-ttu-id="4b197-349">ADFV2 emits the following metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-349">ADFV2 emits the following metrics</span></span>

| <span data-ttu-id="4b197-350">**Metric**</span><span class="sxs-lookup"><span data-stu-id="4b197-350">**Metric**</span></span>           | <span data-ttu-id="4b197-351">**Metric Display Name**</span><span class="sxs-lookup"><span data-stu-id="4b197-351">**Metric Display Name**</span></span>         | <span data-ttu-id="4b197-352">**Unit**</span><span class="sxs-lookup"><span data-stu-id="4b197-352">**Unit**</span></span> | <span data-ttu-id="4b197-353">**Aggregation Type**</span><span class="sxs-lookup"><span data-stu-id="4b197-353">**Aggregation Type**</span></span> | <span data-ttu-id="4b197-354">**Description**</span><span class="sxs-lookup"><span data-stu-id="4b197-354">**Description**</span></span>                                       |
|----------------------|---------------------------------|----------|----------------------|-------------------------------------------------------|
| <span data-ttu-id="4b197-355">PipelineSucceededRun</span><span class="sxs-lookup"><span data-stu-id="4b197-355">PipelineSucceededRun</span></span> | <span data-ttu-id="4b197-356">Succeeded pipeline runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-356">Succeeded pipeline runs metrics</span></span> | <span data-ttu-id="4b197-357">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-357">Count</span></span>    | <span data-ttu-id="4b197-358">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-358">Total</span></span>                | <span data-ttu-id="4b197-359">Total pipelines runs succeeded within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-359">Total pipelines runs succeeded within a minute window</span></span> |
| <span data-ttu-id="4b197-360">PipelineFailedRuns</span><span class="sxs-lookup"><span data-stu-id="4b197-360">PipelineFailedRuns</span></span>   | <span data-ttu-id="4b197-361">Failed pipeline runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-361">Failed pipeline runs metrics</span></span>    | <span data-ttu-id="4b197-362">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-362">Count</span></span>    | <span data-ttu-id="4b197-363">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-363">Total</span></span>                | <span data-ttu-id="4b197-364">Total pipelines runs failed within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-364">Total pipelines runs failed within a minute window</span></span>    |
| <span data-ttu-id="4b197-365">ActivitySucceededRuns</span><span class="sxs-lookup"><span data-stu-id="4b197-365">ActivitySucceededRuns</span></span> | <span data-ttu-id="4b197-366">Succeeded activity runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-366">Succeeded activity runs metrics</span></span> | <span data-ttu-id="4b197-367">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-367">Count</span></span>    | <span data-ttu-id="4b197-368">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-368">Total</span></span>                | <span data-ttu-id="4b197-369">Total activity runs succeeded within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-369">Total activity runs succeeded within a minute window</span></span>  |
| <span data-ttu-id="4b197-370">ActivityFailedRuns</span><span class="sxs-lookup"><span data-stu-id="4b197-370">ActivityFailedRuns</span></span>   | <span data-ttu-id="4b197-371">Failed activity runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-371">Failed activity runs metrics</span></span>    | <span data-ttu-id="4b197-372">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-372">Count</span></span>    | <span data-ttu-id="4b197-373">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-373">Total</span></span>                | <span data-ttu-id="4b197-374">Total activity runs failed within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-374">Total activity runs failed within a minute window</span></span>     |
| <span data-ttu-id="4b197-375">TriggerSucceededRuns</span><span class="sxs-lookup"><span data-stu-id="4b197-375">TriggerSucceededRuns</span></span> | <span data-ttu-id="4b197-376">Succeeded trigger runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-376">Succeeded trigger runs metrics</span></span>  | <span data-ttu-id="4b197-377">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-377">Count</span></span>    | <span data-ttu-id="4b197-378">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-378">Total</span></span>                | <span data-ttu-id="4b197-379">Total trigger runs succeeded within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-379">Total trigger runs succeeded within a minute window</span></span>   |
| <span data-ttu-id="4b197-380">TriggerFailedRuns</span><span class="sxs-lookup"><span data-stu-id="4b197-380">TriggerFailedRuns</span></span>    | <span data-ttu-id="4b197-381">Failed trigger runs metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-381">Failed trigger runs metrics</span></span>     | <span data-ttu-id="4b197-382">Count</span><span class="sxs-lookup"><span data-stu-id="4b197-382">Count</span></span>    | <span data-ttu-id="4b197-383">Total</span><span class="sxs-lookup"><span data-stu-id="4b197-383">Total</span></span>                | <span data-ttu-id="4b197-384">Total trigger runs failed within a minute window</span><span class="sxs-lookup"><span data-stu-id="4b197-384">Total trigger runs failed within a minute window</span></span>      |

<span data-ttu-id="4b197-385">To access the metrics, follow the instructions in the article - https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-385">To access the metrics, follow the instructions in the article - https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics</span></span>

## <a name="monitor-data-factory-metrics-with-azure-monitor"></a><span data-ttu-id="4b197-386">Monitor Data Factory Metrics with Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4b197-386">Monitor Data Factory Metrics with Azure Monitor</span></span>

<span data-ttu-id="4b197-387">You can use Azure Data Factory integration with Azure Monitor to route data to Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4b197-387">You can use Azure Data Factory integration with Azure Monitor to route data to Azure Monitor.</span></span> <span data-ttu-id="4b197-388">This integration is useful in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="4b197-388">This integration is useful in the following scenarios:</span></span>

1.  <span data-ttu-id="4b197-389">You want to write complex queries on a rich set of metrics that is published by Data Factory to Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4b197-389">You want to write complex queries on a rich set of metrics that is published by Data Factory to Azure Monitor.</span></span> <span data-ttu-id="4b197-390">You can also create custom alerts on these queries via Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="4b197-390">You can also create custom alerts on these queries via Azure Monitor.</span></span>

2.  <span data-ttu-id="4b197-391">You want to monitor across data factories.</span><span class="sxs-lookup"><span data-stu-id="4b197-391">You want to monitor across data factories.</span></span> <span data-ttu-id="4b197-392">You can route data from multiple data factories to a single Azure Monitor workspace.</span><span class="sxs-lookup"><span data-stu-id="4b197-392">You can route data from multiple data factories to a single Azure Monitor workspace.</span></span>

<span data-ttu-id="4b197-393">For a seven-minute introduction and demonstration of this feature, watch the following video:</span><span class="sxs-lookup"><span data-stu-id="4b197-393">For a seven-minute introduction and demonstration of this feature, watch the following video:</span></span>

> [!VIDEO https://channel9.msdn.com/Shows/Azure-Friday/Monitor-Data-Factory-pipelines-using-Operations-Management-Suite-OMS/player]

### <a name="configure-diagnostic-settings-and-workspace"></a><span data-ttu-id="4b197-394">Configure Diagnostic Settings and Workspace</span><span class="sxs-lookup"><span data-stu-id="4b197-394">Configure Diagnostic Settings and Workspace</span></span>

<span data-ttu-id="4b197-395">Enable Diagnostic Settings for your data factory.</span><span class="sxs-lookup"><span data-stu-id="4b197-395">Enable Diagnostic Settings for your data factory.</span></span>

1.  <span data-ttu-id="4b197-396">Select **Azure Monitor** -> **Diagnostics settings** -> Select the data factory -> Turn on diagnostics.</span><span class="sxs-lookup"><span data-stu-id="4b197-396">Select **Azure Monitor** -> **Diagnostics settings** -> Select the data factory -> Turn on diagnostics.</span></span>

    ![monitor-oms-image1.png](media/data-factory-monitor-oms/monitor-oms-image1.png)

2.  <span data-ttu-id="4b197-398">Provide diagnostic settings including configuration of the workspace.</span><span class="sxs-lookup"><span data-stu-id="4b197-398">Provide diagnostic settings including configuration of the workspace.</span></span>

    ![monitor-oms-image2.png](media/data-factory-monitor-oms/monitor-oms-image2.png)

### <a name="install-azure-data-factory-analytics-from-azure-marketplace"></a><span data-ttu-id="4b197-400">Install Azure Data Factory Analytics from Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="4b197-400">Install Azure Data Factory Analytics from Azure Marketplace</span></span>

![monitor-oms-image3.png](media/data-factory-monitor-oms/monitor-oms-image3.png)

![monitor-oms-image4.png](media/data-factory-monitor-oms/monitor-oms-image4.png)

<span data-ttu-id="4b197-403">Click **Create** and select the Workspace and Workspace settings.</span><span class="sxs-lookup"><span data-stu-id="4b197-403">Click **Create** and select the Workspace and Workspace settings.</span></span>

![monitor-oms-image5.png](media/data-factory-monitor-oms/monitor-oms-image5.png)

### <a name="monitor-data-factory-metrics"></a><span data-ttu-id="4b197-405">Monitor Data Factory Metrics</span><span class="sxs-lookup"><span data-stu-id="4b197-405">Monitor Data Factory Metrics</span></span>

<span data-ttu-id="4b197-406">Installing **Azure Data Factory Analytics** creates a default set of views that enables the following metrics:</span><span class="sxs-lookup"><span data-stu-id="4b197-406">Installing **Azure Data Factory Analytics** creates a default set of views that enables the following metrics:</span></span>

- <span data-ttu-id="4b197-407">ADF Runs- 1) Pipeline Runs by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-407">ADF Runs- 1) Pipeline Runs by Data Factory</span></span>

- <span data-ttu-id="4b197-408">ADF Runs- 2) Activity Runs by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-408">ADF Runs- 2) Activity Runs by Data Factory</span></span>

- <span data-ttu-id="4b197-409">ADF Runs- 3) Trigger Runs by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-409">ADF Runs- 3) Trigger Runs by Data Factory</span></span>

- <span data-ttu-id="4b197-410">ADF Errors- 1) Top 10 Pipeline Errors by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-410">ADF Errors- 1) Top 10 Pipeline Errors by Data Factory</span></span>

- <span data-ttu-id="4b197-411">ADF Errors- 2) Top 10 Activity Runs by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-411">ADF Errors- 2) Top 10 Activity Runs by Data Factory</span></span>

- <span data-ttu-id="4b197-412">ADF Errors- 3) Top 10 Trigger Errors by Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b197-412">ADF Errors- 3) Top 10 Trigger Errors by Data Factory</span></span>

- <span data-ttu-id="4b197-413">ADF Statistics- 1) Activity Runs by Type</span><span class="sxs-lookup"><span data-stu-id="4b197-413">ADF Statistics- 1) Activity Runs by Type</span></span>

- <span data-ttu-id="4b197-414">ADF Statistics- 2) Trigger Runs by Type</span><span class="sxs-lookup"><span data-stu-id="4b197-414">ADF Statistics- 2) Trigger Runs by Type</span></span>

- <span data-ttu-id="4b197-415">ADF Statistics- 3) Max Pipeline Runs Duration</span><span class="sxs-lookup"><span data-stu-id="4b197-415">ADF Statistics- 3) Max Pipeline Runs Duration</span></span>

![monitor-oms-image6.png](media/data-factory-monitor-oms/monitor-oms-image6.png)

![monitor-oms-image7.png](media/data-factory-monitor-oms/monitor-oms-image7.png)

<span data-ttu-id="4b197-418">You can visualize the above metrics, look at the queries behind these metrics, edit the queries, create alerts, and so forth.</span><span class="sxs-lookup"><span data-stu-id="4b197-418">You can visualize the above metrics, look at the queries behind these metrics, edit the queries, create alerts, and so forth.</span></span>

![monitor-oms-image8.png](media/data-factory-monitor-oms/monitor-oms-image8.png)

## <a name="alerts"></a><span data-ttu-id="4b197-420">Alerts</span><span class="sxs-lookup"><span data-stu-id="4b197-420">Alerts</span></span>

<span data-ttu-id="4b197-421">You can raise alerts on supported metrics in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4b197-421">You can raise alerts on supported metrics in Data Factory.</span></span> <span data-ttu-id="4b197-422">Click the **Alerts** button on the Data Factory **Monitor** page.</span><span class="sxs-lookup"><span data-stu-id="4b197-422">Click the **Alerts** button on the Data Factory **Monitor** page.</span></span>

![Alerts option](media/monitor-using-azure-monitor/alerts_image1.png)

<span data-ttu-id="4b197-424">This takes you to the **Alerts** page.</span><span class="sxs-lookup"><span data-stu-id="4b197-424">This takes you to the **Alerts** page.</span></span>

![Alerts page](media/monitor-using-azure-monitor/alerts_image2.png)

<span data-ttu-id="4b197-426">You can also log in to the Azure portal and click **Monitor -&gt; Alerts** to reach the **Alerts** page directly.</span><span class="sxs-lookup"><span data-stu-id="4b197-426">You can also log in to the Azure portal and click **Monitor -&gt; Alerts** to reach the **Alerts** page directly.</span></span>

![Alerts in the portal menu](media/monitor-using-azure-monitor/alerts_image3.png)

### <a name="create-alerts"></a><span data-ttu-id="4b197-428">Create Alerts</span><span class="sxs-lookup"><span data-stu-id="4b197-428">Create Alerts</span></span>

1.  <span data-ttu-id="4b197-429">Click **+ New Alert rule** to create a new alert.</span><span class="sxs-lookup"><span data-stu-id="4b197-429">Click **+ New Alert rule** to create a new alert.</span></span>

    ![New alert rule](media/monitor-using-azure-monitor/alerts_image4.png)

2.  <span data-ttu-id="4b197-431">Define the **Alert condition**.</span><span class="sxs-lookup"><span data-stu-id="4b197-431">Define the **Alert condition**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4b197-432">Make sure to select **All** in the **Filter by resource type**.</span><span class="sxs-lookup"><span data-stu-id="4b197-432">Make sure to select **All** in the **Filter by resource type**.</span></span>

    ![Alert condition, screen 1 of 3](media/monitor-using-azure-monitor/alerts_image5.png)

    ![Alert condition, screen 2 of 3](media/monitor-using-azure-monitor/alerts_image6.png)

    ![Alert condition, screen 3 of 3](media/monitor-using-azure-monitor/alerts_image7.png)

3.  <span data-ttu-id="4b197-436">Define the **Alert details**.</span><span class="sxs-lookup"><span data-stu-id="4b197-436">Define the **Alert details**.</span></span>

    ![Alert details](media/monitor-using-azure-monitor/alerts_image8.png)

4.  <span data-ttu-id="4b197-438">Define the **Action group**.</span><span class="sxs-lookup"><span data-stu-id="4b197-438">Define the **Action group**.</span></span>

    ![Action group, screen 1 of 4](media/monitor-using-azure-monitor/alerts_image9.png)

    ![Action group, screen 2 of 4](media/monitor-using-azure-monitor/alerts_image10.png)

    ![Action group, screen 3 of 4](media/monitor-using-azure-monitor/alerts_image11.png)

    ![Action group, screen 4 of 4](media/monitor-using-azure-monitor/alerts_image12.png)

## <a name="next-steps"></a><span data-ttu-id="4b197-443">Next steps</span><span class="sxs-lookup"><span data-stu-id="4b197-443">Next steps</span></span>
<span data-ttu-id="4b197-444">See [Monitor and manage pipelines programmatically](monitor-programmatically.md) article to learn about monitoring and managing pipelines by running .</span><span class="sxs-lookup"><span data-stu-id="4b197-444">See [Monitor and manage pipelines programmatically](monitor-programmatically.md) article to learn about monitoring and managing pipelines by running .</span></span>
