---
title: Archive Azure Diagnostic Logs | Microsoft Docs
description: Learn how to archive your Azure Diagnostic Logs for long-term retention in a storage account.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 3a55c73f-2ef3-45f3-8956-bcf9c0cb7e05
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/26/2016
ms.author: johnkem
ms.openlocfilehash: 27461dbc898c6a147c1a01219ca51d00dc89c8b4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564557"
---
# <a name="archive-azure-diagnostic-logs"></a><span data-ttu-id="2c3e8-103">Archive Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="2c3e8-103">Archive Azure Diagnostic Logs</span></span>
<span data-ttu-id="2c3e8-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, CLI, or REST API to archive your [Azure Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md) in a storage account.</span></span> <span data-ttu-id="2c3e8-105">This option is useful if you would like to retain your Diagnostic Logs with an optional retention policy for audit, static analysis, or backup.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-105">This option is useful if you would like to retain your Diagnostic Logs with an optional retention policy for audit, static analysis, or backup.</span></span> <span data-ttu-id="2c3e8-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-106">The storage account does not have to be in the same subscription as the resource emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2c3e8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2c3e8-107">Prerequisites</span></span>
<span data-ttu-id="2c3e8-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Diagnostic Logs.</span></span> <span data-ttu-id="2c3e8-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="2c3e8-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your Diagnostic Logs as well to keep all monitoring data in a central location.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-110">However, if you are also archiving your Activity Log and diagnostic metrics to a storage account, it may make sense to use that storage account for your Diagnostic Logs as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="2c3e8-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="2c3e8-112">Diagnostic Settings</span><span class="sxs-lookup"><span data-stu-id="2c3e8-112">Diagnostic Settings</span></span>
<span data-ttu-id="2c3e8-113">To archive your Diagnostic Logs using any of the methods below, you set a **Diagnostic Setting** for a particular resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-113">To archive your Diagnostic Logs using any of the methods below, you set a **Diagnostic Setting** for a particular resource.</span></span> <span data-ttu-id="2c3e8-114">A diagnostic setting for a resource defines the categories of logs that are that are stored or streamed and the outputs—storage account and/or event hub.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-114">A diagnostic setting for a resource defines the categories of logs that are that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="2c3e8-115">It also defines the retention policy (number of days to retain) for events of each log category stored in a storage account.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-115">It also defines the retention policy (number of days to retain) for events of each log category stored in a storage account.</span></span> <span data-ttu-id="2c3e8-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span><span class="sxs-lookup"><span data-stu-id="2c3e8-116">If a retention policy is set to zero, events for that log category are stored indefinitely (that is to say, forever).</span></span> <span data-ttu-id="2c3e8-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-117">A retention policy can otherwise be any number of days between 1 and 2147483647.</span></span> <span data-ttu-id="2c3e8-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="2c3e8-118">[You can read more about diagnostic settings here](monitoring-overview-of-diagnostic-logs.md#diagnostic-settings).</span></span> <span data-ttu-id="2c3e8-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="2c3e8-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span><span class="sxs-lookup"><span data-stu-id="2c3e8-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted</span></span>

## <a name="archive-diagnostic-logs-using-the-portal"></a><span data-ttu-id="2c3e8-121">Archive Diagnostic Logs using the portal</span><span class="sxs-lookup"><span data-stu-id="2c3e8-121">Archive Diagnostic Logs using the portal</span></span>
1. <span data-ttu-id="2c3e8-122">In the portal, click into the resource blade for the resource on which you would like to enable archival of Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-122">In the portal, click into the resource blade for the resource on which you would like to enable archival of Diagnostic Logs.</span></span>
2. <span data-ttu-id="2c3e8-123">In the **Monitoring** section of the resource settings menu, select **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-123">In the **Monitoring** section of the resource settings menu, select **Diagnostics**.</span></span>
   
    ![Monitoring section of resource menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-archive-diagnostic-logs/diag-log-monitoring-sec.png)
3. <span data-ttu-id="2c3e8-125">Check the box for **Export to Storage Account**, then select a storage account.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-125">Check the box for **Export to Storage Account**, then select a storage account.</span></span> <span data-ttu-id="2c3e8-126">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-126">Optionally, set a number of days to retain these logs by using the **Retention (days)** sliders.</span></span> <span data-ttu-id="2c3e8-127">A retention of zero days stores the logs indefinitely.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-127">A retention of zero days stores the logs indefinitely.</span></span>
   
    ![Diagnostic Logs blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-archive-diagnostic-logs/diag-log-monitoring-blade.png)
4. <span data-ttu-id="2c3e8-129">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-129">Click **Save**.</span></span>

<span data-ttu-id="2c3e8-130">Diagnostic Logs are archived to that storage account as soon as new event data is generated.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-130">Diagnostic Logs are archived to that storage account as soon as new event data is generated.</span></span>

## <a name="archive-diagnostic-logs-via-the-powershell-cmdlets"></a><span data-ttu-id="2c3e8-131">Archive Diagnostic Logs via the PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="2c3e8-131">Archive Diagnostic Logs via the PowerShell Cmdlets</span></span>
```
Set-AzureRmDiagnosticSetting -ResourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg -StorageAccountId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Categories networksecuritygroupevent,networksecuritygrouprulecounter -Enabled $true -RetentionEnabled $true -RetentionInDays 90
```

| <span data-ttu-id="2c3e8-132">Property</span><span class="sxs-lookup"><span data-stu-id="2c3e8-132">Property</span></span> | <span data-ttu-id="2c3e8-133">Required</span><span class="sxs-lookup"><span data-stu-id="2c3e8-133">Required</span></span> | <span data-ttu-id="2c3e8-134">Description</span><span class="sxs-lookup"><span data-stu-id="2c3e8-134">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c3e8-135">ResourceId</span><span class="sxs-lookup"><span data-stu-id="2c3e8-135">ResourceId</span></span> |<span data-ttu-id="2c3e8-136">Yes</span><span class="sxs-lookup"><span data-stu-id="2c3e8-136">Yes</span></span> |<span data-ttu-id="2c3e8-137">Resource ID of the resource on which you want to set a diagnostic setting.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-137">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="2c3e8-138">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="2c3e8-138">StorageAccountId</span></span> |<span data-ttu-id="2c3e8-139">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-139">No</span></span> |<span data-ttu-id="2c3e8-140">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-140">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="2c3e8-141">Categories</span><span class="sxs-lookup"><span data-stu-id="2c3e8-141">Categories</span></span> |<span data-ttu-id="2c3e8-142">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-142">No</span></span> |<span data-ttu-id="2c3e8-143">Comma-separated list of log categories to enable.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-143">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="2c3e8-144">Enabled</span><span class="sxs-lookup"><span data-stu-id="2c3e8-144">Enabled</span></span> |<span data-ttu-id="2c3e8-145">Yes</span><span class="sxs-lookup"><span data-stu-id="2c3e8-145">Yes</span></span> |<span data-ttu-id="2c3e8-146">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-146">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |
| <span data-ttu-id="2c3e8-147">RetentionEnabled</span><span class="sxs-lookup"><span data-stu-id="2c3e8-147">RetentionEnabled</span></span> |<span data-ttu-id="2c3e8-148">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-148">No</span></span> |<span data-ttu-id="2c3e8-149">Boolean indicating if a retention policy are enabled on this resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-149">Boolean indicating if a retention policy are enabled on this resource.</span></span> |
| <span data-ttu-id="2c3e8-150">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="2c3e8-150">RetentionInDays</span></span> |<span data-ttu-id="2c3e8-151">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-151">No</span></span> |<span data-ttu-id="2c3e8-152">Number of days for which events should be retained between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-152">Number of days for which events should be retained between 1 and 2147483647.</span></span> <span data-ttu-id="2c3e8-153">A value of zero stores the logs indefinitely.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-153">A value of zero stores the logs indefinitely.</span></span> |

## <a name="archive-diagnostic-logs-via-the-cross-platform-cli"></a><span data-ttu-id="2c3e8-154">Archive Diagnostic Logs via the Cross-Platform CLI</span><span class="sxs-lookup"><span data-stu-id="2c3e8-154">Archive Diagnostic Logs via the Cross-Platform CLI</span></span>
```
azure insights diagnostic set --resourceId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg --storageId /subscriptions/s1id1234-5679-0123-4567-890123456789/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage –categories networksecuritygroupevent,networksecuritygrouprulecounter --enabled true
```

| <span data-ttu-id="2c3e8-155">Property</span><span class="sxs-lookup"><span data-stu-id="2c3e8-155">Property</span></span> | <span data-ttu-id="2c3e8-156">Required</span><span class="sxs-lookup"><span data-stu-id="2c3e8-156">Required</span></span> | <span data-ttu-id="2c3e8-157">Description</span><span class="sxs-lookup"><span data-stu-id="2c3e8-157">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2c3e8-158">resourceId</span><span class="sxs-lookup"><span data-stu-id="2c3e8-158">resourceId</span></span> |<span data-ttu-id="2c3e8-159">Yes</span><span class="sxs-lookup"><span data-stu-id="2c3e8-159">Yes</span></span> |<span data-ttu-id="2c3e8-160">Resource ID of the resource on which you want to set a diagnostic setting.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-160">Resource ID of the resource on which you want to set a diagnostic setting.</span></span> |
| <span data-ttu-id="2c3e8-161">storageId</span><span class="sxs-lookup"><span data-stu-id="2c3e8-161">storageId</span></span> |<span data-ttu-id="2c3e8-162">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-162">No</span></span> |<span data-ttu-id="2c3e8-163">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-163">Resource ID of the Storage Account to which Diagnostic Logs should be saved.</span></span> |
| <span data-ttu-id="2c3e8-164">categories</span><span class="sxs-lookup"><span data-stu-id="2c3e8-164">categories</span></span> |<span data-ttu-id="2c3e8-165">No</span><span class="sxs-lookup"><span data-stu-id="2c3e8-165">No</span></span> |<span data-ttu-id="2c3e8-166">Comma-separated list of log categories to enable.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-166">Comma-separated list of log categories to enable.</span></span> |
| <span data-ttu-id="2c3e8-167">enabled</span><span class="sxs-lookup"><span data-stu-id="2c3e8-167">enabled</span></span> |<span data-ttu-id="2c3e8-168">Yes</span><span class="sxs-lookup"><span data-stu-id="2c3e8-168">Yes</span></span> |<span data-ttu-id="2c3e8-169">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-169">Boolean indicating whether diagnostics are enabled or disabled on this resource.</span></span> |

## <a name="archive-diagnostic-logs-via-the-rest-api"></a><span data-ttu-id="2c3e8-170">Archive Diagnostic Logs via the REST API</span><span class="sxs-lookup"><span data-stu-id="2c3e8-170">Archive Diagnostic Logs via the REST API</span></span>
<span data-ttu-id="2c3e8-171">[See this document](https://msdn.microsoft.com/library/azure/dn931931.aspx) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-171">[See this document](https://msdn.microsoft.com/library/azure/dn931931.aspx) for information on how you can set up a diagnostic setting using the Azure Monitor REST API.</span></span>

## <a name="schema-of-diagnostic-logs-in-the-storage-account"></a><span data-ttu-id="2c3e8-172">Schema of Diagnostic Logs in the storage account</span><span class="sxs-lookup"><span data-stu-id="2c3e8-172">Schema of Diagnostic Logs in the storage account</span></span>
<span data-ttu-id="2c3e8-173">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-173">Once you have set up archival, a storage container is created in the storage account as soon as an event occurs in one of the log categories you have enabled.</span></span> <span data-ttu-id="2c3e8-174">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-174">The blobs within the container follow the same format across Diagnostic Logs and the Activity Log.</span></span> <span data-ttu-id="2c3e8-175">The structure of these blobs is:</span><span class="sxs-lookup"><span data-stu-id="2c3e8-175">The structure of these blobs is:</span></span>

> <span data-ttu-id="2c3e8-176">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2c3e8-176">insights-logs-{log category name}/resourceId=/SUBSCRIPTIONS/{subscription ID}/RESOURCEGROUPS/{resource group name}/PROVIDERS/{resource provider name}/{resource type}/{resource name}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2c3e8-177">Or, more simply,</span><span class="sxs-lookup"><span data-stu-id="2c3e8-177">Or, more simply,</span></span>

> <span data-ttu-id="2c3e8-178">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2c3e8-178">insights-logs-{log category name}/resourceId=/{resource Id}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2c3e8-179">For example, a blob name might be:</span><span class="sxs-lookup"><span data-stu-id="2c3e8-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="2c3e8-180">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="2c3e8-180">insights-logs-networksecuritygrouprulecounter/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUP/TESTNSG/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="2c3e8-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span><span class="sxs-lookup"><span data-stu-id="2c3e8-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (for example, h=12).</span></span> <span data-ttu-id="2c3e8-182">During the present hour, events are appended to the PT1H.json file as they occur.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="2c3e8-183">The minute value (m=00) is always 00, since Diagnostic Log events are broken into individual blobs per hour.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-183">The minute value (m=00) is always 00, since Diagnostic Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="2c3e8-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span><span class="sxs-lookup"><span data-stu-id="2c3e8-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2016-07-01T00:00:37.2040000Z",
            "systemId": "46cdbb41-cb9c-4f3d-a5b4-1d458d827ff1",
            "category": "NetworkSecurityGroupRuleCounter",
            "resourceId": "/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/RESOURCEGROUPS/TESTRESOURCEGROUP/PROVIDERS/MICROSOFT.NETWORK/NETWORKSECURITYGROUPS/TESTNSG",
            "operationName": "NetworkSecurityGroupCounters",
            "properties": {
                "vnetResourceGuid": "{12345678-9012-3456-7890-123456789012}",
                "subnetPrefix": "10.3.0.0/24",
                "macAddress": "000123456789",
                "ruleName": "/subscriptions/ s1id1234-5679-0123-4567-890123456789/resourceGroups/testresourcegroup/providers/Microsoft.Network/networkSecurityGroups/testnsg/securityRules/default-allow-rdp",
                "direction": "In",
                "type": "allow",
                "matchedConnections": 1988
            }
        }
    ]
}
```

| <span data-ttu-id="2c3e8-185">Element name</span><span class="sxs-lookup"><span data-stu-id="2c3e8-185">Element name</span></span> | <span data-ttu-id="2c3e8-186">Description</span><span class="sxs-lookup"><span data-stu-id="2c3e8-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2c3e8-187">time</span><span class="sxs-lookup"><span data-stu-id="2c3e8-187">time</span></span> |<span data-ttu-id="2c3e8-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="2c3e8-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="2c3e8-189">resourceId</span></span> |<span data-ttu-id="2c3e8-190">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="2c3e8-191">operationName</span><span class="sxs-lookup"><span data-stu-id="2c3e8-191">operationName</span></span> |<span data-ttu-id="2c3e8-192">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-192">Name of the operation.</span></span> |
| <span data-ttu-id="2c3e8-193">category</span><span class="sxs-lookup"><span data-stu-id="2c3e8-193">category</span></span> |<span data-ttu-id="2c3e8-194">Log category of the event.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-194">Log category of the event.</span></span> |
| <span data-ttu-id="2c3e8-195">properties</span><span class="sxs-lookup"><span data-stu-id="2c3e8-195">properties</span></span> |<span data-ttu-id="2c3e8-196">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-196">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="2c3e8-197">The properties and usage of those properties can vary depending on the resource.</span><span class="sxs-lookup"><span data-stu-id="2c3e8-197">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="2c3e8-198">Next Steps</span><span class="sxs-lookup"><span data-stu-id="2c3e8-198">Next Steps</span></span>
* [<span data-ttu-id="2c3e8-199">Download blobs for analysis</span><span class="sxs-lookup"><span data-stu-id="2c3e8-199">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="2c3e8-200">Stream Diagnostic Logs to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2c3e8-200">Stream Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="2c3e8-201">Read more about Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="2c3e8-201">Read more about Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)



