---
title: Archive the Azure Activity Log | Microsoft Docs
description: Learn how to archive your Azure Activity Log for long-term retention in a storage account.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d37d3fda-8ef1-477c-a360-a855b418de84
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2016
ms.author: johnkem
ms.openlocfilehash: 8076cb6e9ae4916ef93d3c8bbc1fe63e1d3a58a8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549695"
---
# <a name="archive-the-azure-activity-log"></a><span data-ttu-id="e98a3-103">Archive the Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="e98a3-103">Archive the Azure Activity Log</span></span>
<span data-ttu-id="e98a3-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span><span class="sxs-lookup"><span data-stu-id="e98a3-104">In this article, we show how you can use the Azure portal, PowerShell Cmdlets, or Cross-Platform CLI to archive your [**Azure Activity Log**](monitoring-overview-activity-logs.md) in a storage account.</span></span> <span data-ttu-id="e98a3-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span><span class="sxs-lookup"><span data-stu-id="e98a3-105">This option is useful if you would like to retain your Activity Log longer than 90 days (with full control over the retention policy) for audit, static analysis, or backup.</span></span> <span data-ttu-id="e98a3-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span><span class="sxs-lookup"><span data-stu-id="e98a3-106">If you only need to retain your events for 90 days or less you do not need to set up archival to a storage account, since Activity Log events are retained in the Azure platform for 90 days without enabling archival.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e98a3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e98a3-107">Prerequisites</span></span>
<span data-ttu-id="e98a3-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span><span class="sxs-lookup"><span data-stu-id="e98a3-108">Before you begin, you need to [create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) to which you can archive your Activity Log.</span></span> <span data-ttu-id="e98a3-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span><span class="sxs-lookup"><span data-stu-id="e98a3-109">We highly recommend that you do not use an existing storage account that has other, non-monitoring data stored in it so that you can better control access to monitoring data.</span></span> <span data-ttu-id="e98a3-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span><span class="sxs-lookup"><span data-stu-id="e98a3-110">However, if you are also archiving Diagnostic Logs and metrics to a storage account, it may make sense to use that storage account for your Activity Log as well to keep all monitoring data in a central location.</span></span> <span data-ttu-id="e98a3-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span><span class="sxs-lookup"><span data-stu-id="e98a3-111">The storage account you use must be a general purpose storage account, not a blob storage account.</span></span> <span data-ttu-id="e98a3-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="e98a3-112">The storage account does not have to be in the same subscription as the subscription emitting logs as long as the user who configures the setting has appropriate RBAC access to both subscriptions.</span></span>

## <a name="log-profile"></a><span data-ttu-id="e98a3-113">Log Profile</span><span class="sxs-lookup"><span data-stu-id="e98a3-113">Log Profile</span></span>
<span data-ttu-id="e98a3-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span><span class="sxs-lookup"><span data-stu-id="e98a3-114">To archive the Activity Log using any of the methods below, you set the **Log Profile** for a subscription.</span></span> <span data-ttu-id="e98a3-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span><span class="sxs-lookup"><span data-stu-id="e98a3-115">The Log Profile defines the type of events that are stored or streamed and the outputs—storage account and/or event hub.</span></span> <span data-ttu-id="e98a3-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span><span class="sxs-lookup"><span data-stu-id="e98a3-116">It also defines the retention policy (number of days to retain) for events stored in a storage account.</span></span> <span data-ttu-id="e98a3-117">If the retention policy is set to zero, events are stored indefinitely.</span><span class="sxs-lookup"><span data-stu-id="e98a3-117">If the retention policy is set to zero, events are stored indefinitely.</span></span> <span data-ttu-id="e98a3-118">Otherwise, this can be set to any value between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e98a3-118">Otherwise, this can be set to any value between 1 and 2147483647.</span></span> <span data-ttu-id="e98a3-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span><span class="sxs-lookup"><span data-stu-id="e98a3-119">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy will be deleted.</span></span> <span data-ttu-id="e98a3-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span><span class="sxs-lookup"><span data-stu-id="e98a3-120">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span> <span data-ttu-id="e98a3-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-log-profiles).</span><span class="sxs-lookup"><span data-stu-id="e98a3-121">[You can read more about log profiles here](monitoring-overview-activity-logs.md#export-the-activity-log-with-log-profiles).</span></span> 

## <a name="archive-the-activity-log-using-the-portal"></a><span data-ttu-id="e98a3-122">Archive the Activity Log using the portal</span><span class="sxs-lookup"><span data-stu-id="e98a3-122">Archive the Activity Log using the portal</span></span>
1. <span data-ttu-id="e98a3-123">In the portal, click the **Activity Log** link on the left-side navigation.</span><span class="sxs-lookup"><span data-stu-id="e98a3-123">In the portal, click the **Activity Log** link on the left-side navigation.</span></span> <span data-ttu-id="e98a3-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span><span class="sxs-lookup"><span data-stu-id="e98a3-124">If you don’t see a link for the Activity Log, click the **More Services** link first.</span></span>
   
    ![Navigate to Activity Log blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-archive-activity-log/act-log-portal-navigate.png)
2. <span data-ttu-id="e98a3-126">At the top of the blade, click **Export**.</span><span class="sxs-lookup"><span data-stu-id="e98a3-126">At the top of the blade, click **Export**.</span></span>
   
    ![Click the Export button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-archive-activity-log/act-log-portal-export-button.png)
3. <span data-ttu-id="e98a3-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span><span class="sxs-lookup"><span data-stu-id="e98a3-128">In the blade that appears, check the box for **Export to a storage account** and select a storage account.</span></span>
   
    ![Set a storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-archive-activity-log/act-log-portal-export-blade.png)
4. <span data-ttu-id="e98a3-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span><span class="sxs-lookup"><span data-stu-id="e98a3-130">Using the slider or text box, define a number of days for which Activity Log events should be kept in your storage account.</span></span> <span data-ttu-id="e98a3-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span><span class="sxs-lookup"><span data-stu-id="e98a3-131">If you prefer to have your data persisted in the storage account indefinitely, set this number to zero.</span></span>
5. <span data-ttu-id="e98a3-132">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e98a3-132">Click **Save**.</span></span>

## <a name="archive-the-activity-log-via-powershell"></a><span data-ttu-id="e98a3-133">Archive the Activity Log via PowerShell</span><span class="sxs-lookup"><span data-stu-id="e98a3-133">Archive the Activity Log via PowerShell</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -Locations global,westus,eastus -RetentionInDays 180 -Categories Write,Delete,Action
```

| <span data-ttu-id="e98a3-134">Property</span><span class="sxs-lookup"><span data-stu-id="e98a3-134">Property</span></span> | <span data-ttu-id="e98a3-135">Required</span><span class="sxs-lookup"><span data-stu-id="e98a3-135">Required</span></span> | <span data-ttu-id="e98a3-136">Description</span><span class="sxs-lookup"><span data-stu-id="e98a3-136">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e98a3-137">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="e98a3-137">StorageAccountId</span></span> |<span data-ttu-id="e98a3-138">No</span><span class="sxs-lookup"><span data-stu-id="e98a3-138">No</span></span> |<span data-ttu-id="e98a3-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span><span class="sxs-lookup"><span data-stu-id="e98a3-139">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="e98a3-140">Locations</span><span class="sxs-lookup"><span data-stu-id="e98a3-140">Locations</span></span> |<span data-ttu-id="e98a3-141">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-141">Yes</span></span> |<span data-ttu-id="e98a3-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span><span class="sxs-lookup"><span data-stu-id="e98a3-142">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="e98a3-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="e98a3-143">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="e98a3-144">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="e98a3-144">RetentionInDays</span></span> |<span data-ttu-id="e98a3-145">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-145">Yes</span></span> |<span data-ttu-id="e98a3-146">Number of days for which events should be retained, between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e98a3-146">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="e98a3-147">A value of zero stores the logs indefinitely (forever).</span><span class="sxs-lookup"><span data-stu-id="e98a3-147">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="e98a3-148">Categories</span><span class="sxs-lookup"><span data-stu-id="e98a3-148">Categories</span></span> |<span data-ttu-id="e98a3-149">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-149">Yes</span></span> |<span data-ttu-id="e98a3-150">Comma-separated list of event categories that should be collected.</span><span class="sxs-lookup"><span data-stu-id="e98a3-150">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="e98a3-151">Possible values are Write, Delete, and Action.</span><span class="sxs-lookup"><span data-stu-id="e98a3-151">Possible values are Write, Delete, and Action.</span></span> |

## <a name="archive-the-activity-log-via-cli"></a><span data-ttu-id="e98a3-152">Archive the Activity Log via CLI</span><span class="sxs-lookup"><span data-stu-id="e98a3-152">Archive the Activity Log via CLI</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --locations global,westus,eastus,northeurope --retentionInDays 180 –categories Write,Delete,Action
```

| <span data-ttu-id="e98a3-153">Property</span><span class="sxs-lookup"><span data-stu-id="e98a3-153">Property</span></span> | <span data-ttu-id="e98a3-154">Required</span><span class="sxs-lookup"><span data-stu-id="e98a3-154">Required</span></span> | <span data-ttu-id="e98a3-155">Description</span><span class="sxs-lookup"><span data-stu-id="e98a3-155">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e98a3-156">name</span><span class="sxs-lookup"><span data-stu-id="e98a3-156">name</span></span> |<span data-ttu-id="e98a3-157">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-157">Yes</span></span> |<span data-ttu-id="e98a3-158">Name of your log profile.</span><span class="sxs-lookup"><span data-stu-id="e98a3-158">Name of your log profile.</span></span> |
| <span data-ttu-id="e98a3-159">storageId</span><span class="sxs-lookup"><span data-stu-id="e98a3-159">storageId</span></span> |<span data-ttu-id="e98a3-160">No</span><span class="sxs-lookup"><span data-stu-id="e98a3-160">No</span></span> |<span data-ttu-id="e98a3-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span><span class="sxs-lookup"><span data-stu-id="e98a3-161">Resource ID of the Storage Account to which Activity Logs should be saved.</span></span> |
| <span data-ttu-id="e98a3-162">locations</span><span class="sxs-lookup"><span data-stu-id="e98a3-162">locations</span></span> |<span data-ttu-id="e98a3-163">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-163">Yes</span></span> |<span data-ttu-id="e98a3-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span><span class="sxs-lookup"><span data-stu-id="e98a3-164">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> <span data-ttu-id="e98a3-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span><span class="sxs-lookup"><span data-stu-id="e98a3-165">You can view a list of all regions [by visiting this page](https://azure.microsoft.com/en-us/regions) or by using [the Azure Management REST API](https://msdn.microsoft.com/library/azure/gg441293.aspx).</span></span> |
| <span data-ttu-id="e98a3-166">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="e98a3-166">retentionInDays</span></span> |<span data-ttu-id="e98a3-167">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-167">Yes</span></span> |<span data-ttu-id="e98a3-168">Number of days for which events should be retained, between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="e98a3-168">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="e98a3-169">A value of zero will store the logs indefinitely (forever).</span><span class="sxs-lookup"><span data-stu-id="e98a3-169">A value of zero will store the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="e98a3-170">categories</span><span class="sxs-lookup"><span data-stu-id="e98a3-170">categories</span></span> |<span data-ttu-id="e98a3-171">Yes</span><span class="sxs-lookup"><span data-stu-id="e98a3-171">Yes</span></span> |<span data-ttu-id="e98a3-172">Comma-separated list of event categories that should be collected.</span><span class="sxs-lookup"><span data-stu-id="e98a3-172">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="e98a3-173">Possible values are Write, Delete, and Action.</span><span class="sxs-lookup"><span data-stu-id="e98a3-173">Possible values are Write, Delete, and Action.</span></span> |

## <a name="storage-schema-of-the-activity-log"></a><span data-ttu-id="e98a3-174">Storage schema of the Activity Log</span><span class="sxs-lookup"><span data-stu-id="e98a3-174">Storage schema of the Activity Log</span></span>
<span data-ttu-id="e98a3-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span><span class="sxs-lookup"><span data-stu-id="e98a3-175">Once you have set up archival, a storage container will be created in the storage account as soon as an Activity Log event occurs.</span></span> <span data-ttu-id="e98a3-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="e98a3-176">The blobs within the container follow the same format across the Activity Log and Diagnostic Logs.</span></span> <span data-ttu-id="e98a3-177">The structure of these blobs is:</span><span class="sxs-lookup"><span data-stu-id="e98a3-177">The structure of these blobs is:</span></span>

> <span data-ttu-id="e98a3-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e98a3-178">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/{subscription ID}/y={four-digit numeric year}/m={two-digit numeric month}/d={two-digit numeric day}/h={two-digit 24-hour clock hour}/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="e98a3-179">For example, a blob name might be:</span><span class="sxs-lookup"><span data-stu-id="e98a3-179">For example, a blob name might be:</span></span>

> <span data-ttu-id="e98a3-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span><span class="sxs-lookup"><span data-stu-id="e98a3-180">insights-operational-logs/name=default/resourceId=/SUBSCRIPTIONS/s1id1234-5679-0123-4567-890123456789/y=2016/m=08/d=22/h=18/m=00/PT1H.json</span></span>
> 
> 

<span data-ttu-id="e98a3-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span><span class="sxs-lookup"><span data-stu-id="e98a3-181">Each PT1H.json blob contains a JSON blob of events that occurred within the hour specified in the blob URL (e.g. h=12).</span></span> <span data-ttu-id="e98a3-182">During the present hour, events are appended to the PT1H.json file as they occur.</span><span class="sxs-lookup"><span data-stu-id="e98a3-182">During the present hour, events are appended to the PT1H.json file as they occur.</span></span> <span data-ttu-id="e98a3-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span><span class="sxs-lookup"><span data-stu-id="e98a3-183">The minute value (m=00) is always 00, since Activity Log events are broken into individual blobs per hour.</span></span>

<span data-ttu-id="e98a3-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span><span class="sxs-lookup"><span data-stu-id="e98a3-184">Within the PT1H.json file, each event is stored in the “records” array, following this format:</span></span>

```
{
    "records": [
        {
            "time": "2015-01-21T22:14:26.9792776Z",
            "resourceId": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
            "operationName": "microsoft.support/supporttickets/write",
            "category": "Write",
            "resultType": "Success",
            "resultSignature": "Succeeded.Created",
            "durationMs": 2826,
            "callerIpAddress": "111.111.111.11",
            "correlationId": "c776f9f4-36e5-4e0e-809b-c9b3c3fb62a8",
            "identity": {
                "authorization": {
                    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
                    "action": "microsoft.support/supporttickets/write",
                    "evidence": {
                        "role": "Subscription Admin"
                    }
                },
                "claims": {
                    "aud": "https://management.core.windows.net/",
                    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
                    "iat": "1421876371",
                    "nbf": "1421876371",
                    "exp": "1421880271",
                    "ver": "1.0",
                    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
                    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
                    "puid": "20030000801A118C",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
                    "name": "John Smith",
                    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
                    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
                    "appidacr": "2",
                    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
                    "http://schemas.microsoft.com/claims/authnclassreference": "1"
                }
            },
            "level": "Information",
            "location": "global",
            "properties": {
                "statusCode": "Created",
                "serviceRequestId": "50d5cddb-8ca0-47ad-9b80-6cde2207f97c"
            }
        }
    ]
}
```


| <span data-ttu-id="e98a3-185">Element name</span><span class="sxs-lookup"><span data-stu-id="e98a3-185">Element name</span></span> | <span data-ttu-id="e98a3-186">Description</span><span class="sxs-lookup"><span data-stu-id="e98a3-186">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e98a3-187">time</span><span class="sxs-lookup"><span data-stu-id="e98a3-187">time</span></span> |<span data-ttu-id="e98a3-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="e98a3-188">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="e98a3-189">resourceId</span><span class="sxs-lookup"><span data-stu-id="e98a3-189">resourceId</span></span> |<span data-ttu-id="e98a3-190">Resource ID of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="e98a3-190">Resource ID of the impacted resource.</span></span> |
| <span data-ttu-id="e98a3-191">operationName</span><span class="sxs-lookup"><span data-stu-id="e98a3-191">operationName</span></span> |<span data-ttu-id="e98a3-192">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="e98a3-192">Name of the operation.</span></span> |
| <span data-ttu-id="e98a3-193">category</span><span class="sxs-lookup"><span data-stu-id="e98a3-193">category</span></span> |<span data-ttu-id="e98a3-194">Category of the action, eg.</span><span class="sxs-lookup"><span data-stu-id="e98a3-194">Category of the action, eg.</span></span> <span data-ttu-id="e98a3-195">Write, Read, Action.</span><span class="sxs-lookup"><span data-stu-id="e98a3-195">Write, Read, Action.</span></span> |
| <span data-ttu-id="e98a3-196">resultType</span><span class="sxs-lookup"><span data-stu-id="e98a3-196">resultType</span></span> |<span data-ttu-id="e98a3-197">The type of the result, eg.</span><span class="sxs-lookup"><span data-stu-id="e98a3-197">The type of the result, eg.</span></span> <span data-ttu-id="e98a3-198">Success, Failure, Start</span><span class="sxs-lookup"><span data-stu-id="e98a3-198">Success, Failure, Start</span></span> |
| <span data-ttu-id="e98a3-199">resultSignature</span><span class="sxs-lookup"><span data-stu-id="e98a3-199">resultSignature</span></span> |<span data-ttu-id="e98a3-200">Depends on the resource type.</span><span class="sxs-lookup"><span data-stu-id="e98a3-200">Depends on the resource type.</span></span> |
| <span data-ttu-id="e98a3-201">durationMs</span><span class="sxs-lookup"><span data-stu-id="e98a3-201">durationMs</span></span> |<span data-ttu-id="e98a3-202">Duration of the operation in milliseconds</span><span class="sxs-lookup"><span data-stu-id="e98a3-202">Duration of the operation in milliseconds</span></span> |
| <span data-ttu-id="e98a3-203">callerIpAddress</span><span class="sxs-lookup"><span data-stu-id="e98a3-203">callerIpAddress</span></span> |<span data-ttu-id="e98a3-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="e98a3-204">IP address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="e98a3-205">correlationId</span><span class="sxs-lookup"><span data-stu-id="e98a3-205">correlationId</span></span> |<span data-ttu-id="e98a3-206">Usually a GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="e98a3-206">Usually a GUID in the string format.</span></span> <span data-ttu-id="e98a3-207">Events that share a correlationId belong to the same uber action.</span><span class="sxs-lookup"><span data-stu-id="e98a3-207">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="e98a3-208">identity</span><span class="sxs-lookup"><span data-stu-id="e98a3-208">identity</span></span> |<span data-ttu-id="e98a3-209">JSON blob describing the authorization and claims.</span><span class="sxs-lookup"><span data-stu-id="e98a3-209">JSON blob describing the authorization and claims.</span></span> |
| <span data-ttu-id="e98a3-210">authorization</span><span class="sxs-lookup"><span data-stu-id="e98a3-210">authorization</span></span> |<span data-ttu-id="e98a3-211">Blob of RBAC properties of the event.</span><span class="sxs-lookup"><span data-stu-id="e98a3-211">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="e98a3-212">Usually includes the “action”, “role” and “scope” properties.</span><span class="sxs-lookup"><span data-stu-id="e98a3-212">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="e98a3-213">level</span><span class="sxs-lookup"><span data-stu-id="e98a3-213">level</span></span> |<span data-ttu-id="e98a3-214">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="e98a3-214">Level of the event.</span></span> <span data-ttu-id="e98a3-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span><span class="sxs-lookup"><span data-stu-id="e98a3-215">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="e98a3-216">location</span><span class="sxs-lookup"><span data-stu-id="e98a3-216">location</span></span> |<span data-ttu-id="e98a3-217">Region in which the location occurred (or global).</span><span class="sxs-lookup"><span data-stu-id="e98a3-217">Region in which the location occurred (or global).</span></span> |
| <span data-ttu-id="e98a3-218">properties</span><span class="sxs-lookup"><span data-stu-id="e98a3-218">properties</span></span> |<span data-ttu-id="e98a3-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="e98a3-219">Set of `<Key, Value>` pairs (i.e. Dictionary) describing the details of the event.</span></span> |

> [!NOTE]
> <span data-ttu-id="e98a3-220">The properties and usage of those properties can vary depending on the resource.</span><span class="sxs-lookup"><span data-stu-id="e98a3-220">The properties and usage of those properties can vary depending on the resource.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="e98a3-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="e98a3-221">Next steps</span></span>
* [<span data-ttu-id="e98a3-222">Download blobs for analysis</span><span class="sxs-lookup"><span data-stu-id="e98a3-222">Download blobs for analysis</span></span>](../storage/storage-dotnet-how-to-use-blobs.md#download-blobs)
* [<span data-ttu-id="e98a3-223">Stream the Activity Log to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="e98a3-223">Stream the Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)
* [<span data-ttu-id="e98a3-224">Read more about the Activity Log</span><span class="sxs-lookup"><span data-stu-id="e98a3-224">Read more about the Activity Log</span></span>](monitoring-overview-activity-logs.md)




