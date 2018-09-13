---
title: Overview of the Azure Activity Log | Microsoft Docs
description: Learn what the Azure Activity Log is and how you can use it to understand events occurring within your Azure subscription.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: c274782f-039d-4c28-9ddb-f89ce21052c7
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/02/2017
ms.author: johnkem
ms.openlocfilehash: 79bfab5eb964d5e6b7ba7afcd082436266712df1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563242"
---
# <a name="overview-of-the-azure-activity-log"></a><span data-ttu-id="8b5ce-103">Overview of the Azure Activity Log</span><span class="sxs-lookup"><span data-stu-id="8b5ce-103">Overview of the Azure Activity Log</span></span>
<span data-ttu-id="8b5ce-104">The **Azure Activity Log** is a log that provides insight into the operations that were performed on resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-104">The **Azure Activity Log** is a log that provides insight into the operations that were performed on resources in your subscription.</span></span> <span data-ttu-id="8b5ce-105">The Activity Log was previously known as “Audit Logs” or “Operational Logs,” since it reports control-plane events for your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-105">The Activity Log was previously known as “Audit Logs” or “Operational Logs,” since it reports control-plane events for your subscriptions.</span></span> <span data-ttu-id="8b5ce-106">Using the Activity Log, you can determine the ‘what, who, and when’ for any write operations (PUT, POST, DELETE) taken on the resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-106">Using the Activity Log, you can determine the ‘what, who, and when’ for any write operations (PUT, POST, DELETE) taken on the resources in your subscription.</span></span> <span data-ttu-id="8b5ce-107">You can also understand the status of the operation and other relevant properties.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-107">You can also understand the status of the operation and other relevant properties.</span></span> <span data-ttu-id="8b5ce-108">The Activity Log does not include read (GET) operations or operations for resources that use the Classic/"RDFE" model.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-108">The Activity Log does not include read (GET) operations or operations for resources that use the Classic/"RDFE" model.</span></span>

![<span data-ttu-id="8b5ce-109">Activity Logs vs other types of logs</span><span class="sxs-lookup"><span data-stu-id="8b5ce-109">Activity Logs vs other types of logs</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/Activity_Log_vs_other_logs_v5.png)

<span data-ttu-id="8b5ce-110">Figure 1: Activity Logs vs other types of logs</span><span class="sxs-lookup"><span data-stu-id="8b5ce-110">Figure 1: Activity Logs vs other types of logs</span></span>

<span data-ttu-id="8b5ce-111">The Activity Log differs from [Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-111">The Activity Log differs from [Diagnostic Logs](monitoring-overview-of-diagnostic-logs.md).</span></span> <span data-ttu-id="8b5ce-112">Activity Logs provide data about the operations on a resource from the outside.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-112">Activity Logs provide data about the operations on a resource from the outside.</span></span> <span data-ttu-id="8b5ce-113">Diagnostics Logs are emitted by a resource and provide information about the operation of that resource.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-113">Diagnostics Logs are emitted by a resource and provide information about the operation of that resource.</span></span>

<span data-ttu-id="8b5ce-114">You can retrieve events from your Activity Log using the Azure portal, CLI, PowerShell cmdlets, and Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-114">You can retrieve events from your Activity Log using the Azure portal, CLI, PowerShell cmdlets, and Azure Monitor REST API.</span></span>


> [!WARNING]
> <span data-ttu-id="8b5ce-115">The Azure Activity Log is primarily for activities that occur in Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-115">The Azure Activity Log is primarily for activities that occur in Azure Resource Manager.</span></span> <span data-ttu-id="8b5ce-116">It does not track resources using the Classic/RDFE model.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-116">It does not track resources using the Classic/RDFE model.</span></span> <span data-ttu-id="8b5ce-117">Some Classic resource types have a proxy resource provider in Azure Resource Manager (for example, Microsoft.ClassicCompute).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-117">Some Classic resource types have a proxy resource provider in Azure Resource Manager (for example, Microsoft.ClassicCompute).</span></span> <span data-ttu-id="8b5ce-118">If you interact with a Classic resource type through Azure Resource Manager using these proxy resource providers, the operations appear in the Activity Log.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-118">If you interact with a Classic resource type through Azure Resource Manager using these proxy resource providers, the operations appear in the Activity Log.</span></span> <span data-ttu-id="8b5ce-119">If you interact with a Classic resource type in the Classic portal or otherwise outside of the Azure Resource Manager proxies, your actions are only recorded in the Operation Log.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-119">If you interact with a Classic resource type in the Classic portal or otherwise outside of the Azure Resource Manager proxies, your actions are only recorded in the Operation Log.</span></span> <span data-ttu-id="8b5ce-120">The Operation Log is accessible only in the Classic portal.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-120">The Operation Log is accessible only in the Classic portal.</span></span>
>
>

<span data-ttu-id="8b5ce-121">View the following video introducing the Activity Log.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-121">View the following video introducing the Activity Log.</span></span>
[!VIDEO https://channel9.msdn.com/Blogs/Seth-Juarez/Logs-John-Kemnetz/player]

## <a name="what-you-can-do-with-the-activity-log"></a><span data-ttu-id="8b5ce-122">What you can do with the Activity Log</span><span class="sxs-lookup"><span data-stu-id="8b5ce-122">What you can do with the Activity Log</span></span>
<span data-ttu-id="8b5ce-123">Here are some of the things you can do with the Activity Log:</span><span class="sxs-lookup"><span data-stu-id="8b5ce-123">Here are some of the things you can do with the Activity Log:</span></span>

![Azure Activity log](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/Activity_Log_Overview_v3.png)


* [<span data-ttu-id="8b5ce-125">Create an alert that triggers off an Activity Log event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-125">Create an alert that triggers off an Activity Log event.</span></span>](monitoring-activity-log-alerts.md)
* <span data-ttu-id="8b5ce-126">[Stream it to an **Event Hub**](monitoring-stream-activity-logs-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-126">[Stream it to an **Event Hub**](monitoring-stream-activity-logs-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="8b5ce-127">Analyze it in PowerBI using the [**PowerBI content pack**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-127">Analyze it in PowerBI using the [**PowerBI content pack**](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/).</span></span>
* <span data-ttu-id="8b5ce-128">[Save it to a **Storage Account** for archival or manual inspection](monitoring-archive-activity-log.md).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-128">[Save it to a **Storage Account** for archival or manual inspection](monitoring-archive-activity-log.md).</span></span> <span data-ttu-id="8b5ce-129">You can specify the retention time (in days) using **Log Profiles**.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-129">You can specify the retention time (in days) using **Log Profiles**.</span></span>
* <span data-ttu-id="8b5ce-130">Query and view it in the **Azure portal**.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-130">Query and view it in the **Azure portal**.</span></span>
* <span data-ttu-id="8b5ce-131">Query it via PowerShell Cmdlet, CLI, or REST API.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-131">Query it via PowerShell Cmdlet, CLI, or REST API.</span></span>


<span data-ttu-id="8b5ce-132">You can use a storage account or event hub namespace that is not in the same subscription as the one emitting logs.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-132">You can use a storage account or event hub namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="8b5ce-133">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-133">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="export-the-activity-log-with-log-profiles"></a><span data-ttu-id="8b5ce-134">Export the Activity Log with Log Profiles</span><span class="sxs-lookup"><span data-stu-id="8b5ce-134">Export the Activity Log with Log Profiles</span></span>
<span data-ttu-id="8b5ce-135">A **Log Profile** controls how your Activity Log is exported.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-135">A **Log Profile** controls how your Activity Log is exported.</span></span> <span data-ttu-id="8b5ce-136">Using a Log Profile, you can configure:</span><span class="sxs-lookup"><span data-stu-id="8b5ce-136">Using a Log Profile, you can configure:</span></span>

* <span data-ttu-id="8b5ce-137">Where the Activity Log should be sent (Storage Account or Event Hubs)</span><span class="sxs-lookup"><span data-stu-id="8b5ce-137">Where the Activity Log should be sent (Storage Account or Event Hubs)</span></span>
* <span data-ttu-id="8b5ce-138">Which event categories (Write, Delete, Action) should be sent.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-138">Which event categories (Write, Delete, Action) should be sent.</span></span> <span data-ttu-id="8b5ce-139">*The meaning of "category" in Log Profiles and Activity Log events is different. In the Log Profile, "Category" represents the operation type (Write, Delete, Action). In an Activity Log event, the "category" property represents the source or type of event (for example, Administration, ServiceHealth, Alert, and more).*</span><span class="sxs-lookup"><span data-stu-id="8b5ce-139">*The meaning of "category" in Log Profiles and Activity Log events is different. In the Log Profile, "Category" represents the operation type (Write, Delete, Action). In an Activity Log event, the "category" property represents the source or type of event (for example, Administration, ServiceHealth, Alert, and more).*</span></span>
* <span data-ttu-id="8b5ce-140">Which regions (locations) should be exported</span><span class="sxs-lookup"><span data-stu-id="8b5ce-140">Which regions (locations) should be exported</span></span>
* <span data-ttu-id="8b5ce-141">How long the Activity Log should be retained in a Storage Account.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-141">How long the Activity Log should be retained in a Storage Account.</span></span>
    - <span data-ttu-id="8b5ce-142">A retention of zero days means logs are kept forever.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-142">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="8b5ce-143">Otherwise, the value can be any number of days between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-143">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="8b5ce-144">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-144">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="8b5ce-145">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-145">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="8b5ce-146">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-146">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="8b5ce-147">These settings can be configured via the “Export” option in the Activity Log blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-147">These settings can be configured via the “Export” option in the Activity Log blade in the portal.</span></span> <span data-ttu-id="8b5ce-148">They can also be configured programmatically [using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell cmdlets, or CLI.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-148">They can also be configured programmatically [using the Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931927.aspx), PowerShell cmdlets, or CLI.</span></span> <span data-ttu-id="8b5ce-149">A subscription can only have one log profile.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-149">A subscription can only have one log profile.</span></span>

### <a name="configure-log-profiles-using-the-azure-portal"></a><span data-ttu-id="8b5ce-150">Configure log profiles using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8b5ce-150">Configure log profiles using the Azure portal</span></span>
<span data-ttu-id="8b5ce-151">You can stream the Activity Log to an Event Hub or store them in a Storage Account by using the “Export” option in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-151">You can stream the Activity Log to an Event Hub or store them in a Storage Account by using the “Export” option in the Azure portal.</span></span>

1. <span data-ttu-id="8b5ce-152">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-152">Navigate to the **Activity Log** blade using the menu on the left side of the portal.</span></span>

    ![Navigate to Activity Log in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-navigate.png)
2. <span data-ttu-id="8b5ce-154">Click the **Export** button at the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-154">Click the **Export** button at the top of the blade.</span></span>

    ![Export button in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-export.png)
3. <span data-ttu-id="8b5ce-156">In the blade that appears, you can select:</span><span class="sxs-lookup"><span data-stu-id="8b5ce-156">In the blade that appears, you can select:</span></span>  
  * <span data-ttu-id="8b5ce-157">regions for which you would like to export events</span><span class="sxs-lookup"><span data-stu-id="8b5ce-157">regions for which you would like to export events</span></span>
  * <span data-ttu-id="8b5ce-158">the Storage Account to which you would like to save events</span><span class="sxs-lookup"><span data-stu-id="8b5ce-158">the Storage Account to which you would like to save events</span></span>
  * <span data-ttu-id="8b5ce-159">the number of days you want to retain these events in storage.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-159">the number of days you want to retain these events in storage.</span></span> <span data-ttu-id="8b5ce-160">A setting of 0 days retains the logs forever.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-160">A setting of 0 days retains the logs forever.</span></span>
  * <span data-ttu-id="8b5ce-161">the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-161">the Service Bus Namespace in which you would like an Event Hub to be created for streaming these events.</span></span>

     ![Export Activity Log blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-activity-logs/activity-logs-portal-export-blade.png)
4. <span data-ttu-id="8b5ce-163">Click **Save** to save these settings.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-163">Click **Save** to save these settings.</span></span> <span data-ttu-id="8b5ce-164">The settings are immediately be applied to your subscription.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-164">The settings are immediately be applied to your subscription.</span></span>

### <a name="configure-log-profiles-using-the-azure-powershell-cmdlets"></a><span data-ttu-id="8b5ce-165">Configure log profiles using the Azure PowerShell Cmdlets</span><span class="sxs-lookup"><span data-stu-id="8b5ce-165">Configure log profiles using the Azure PowerShell Cmdlets</span></span>
#### <a name="get-existing-log-profile"></a><span data-ttu-id="8b5ce-166">Get existing log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-166">Get existing log profile</span></span>
```
Get-AzureRmLogProfile
```

#### <a name="add-a-log-profile"></a><span data-ttu-id="8b5ce-167">Add a log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-167">Add a log profile</span></span>
```
Add-AzureRmLogProfile -Name my_log_profile -StorageAccountId /subscriptions/s1/resourceGroups/myrg1/providers/Microsoft.Storage/storageAccounts/my_storage -serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey -Locations global,westus,eastus -RetentionInDays 90 -Categories Write,Delete,Action
```

| <span data-ttu-id="8b5ce-168">Property</span><span class="sxs-lookup"><span data-stu-id="8b5ce-168">Property</span></span> | <span data-ttu-id="8b5ce-169">Required</span><span class="sxs-lookup"><span data-stu-id="8b5ce-169">Required</span></span> | <span data-ttu-id="8b5ce-170">Description</span><span class="sxs-lookup"><span data-stu-id="8b5ce-170">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b5ce-171">Name</span><span class="sxs-lookup"><span data-stu-id="8b5ce-171">Name</span></span> |<span data-ttu-id="8b5ce-172">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-172">Yes</span></span> |<span data-ttu-id="8b5ce-173">Name of your log profile.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-173">Name of your log profile.</span></span> |
| <span data-ttu-id="8b5ce-174">StorageAccountId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-174">StorageAccountId</span></span> |<span data-ttu-id="8b5ce-175">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-175">No</span></span> |<span data-ttu-id="8b5ce-176">Resource ID of the Storage Account to which the Activity Log should be saved.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-176">Resource ID of the Storage Account to which the Activity Log should be saved.</span></span> |
| <span data-ttu-id="8b5ce-177">serviceBusRuleId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-177">serviceBusRuleId</span></span> |<span data-ttu-id="8b5ce-178">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-178">No</span></span> |<span data-ttu-id="8b5ce-179">Service Bus Rule ID for the Service Bus namespace you would like to have event hubs created in.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-179">Service Bus Rule ID for the Service Bus namespace you would like to have event hubs created in.</span></span> <span data-ttu-id="8b5ce-180">Is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-180">Is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span> |
| <span data-ttu-id="8b5ce-181">Locations</span><span class="sxs-lookup"><span data-stu-id="8b5ce-181">Locations</span></span> |<span data-ttu-id="8b5ce-182">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-182">Yes</span></span> |<span data-ttu-id="8b5ce-183">Comma-separated list of regions for which you would like to collect Activity Log events.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-183">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> |
| <span data-ttu-id="8b5ce-184">RetentionInDays</span><span class="sxs-lookup"><span data-stu-id="8b5ce-184">RetentionInDays</span></span> |<span data-ttu-id="8b5ce-185">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-185">Yes</span></span> |<span data-ttu-id="8b5ce-186">Number of days for which events should be retained, between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-186">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="8b5ce-187">A value of zero stores the logs indefinitely (forever).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-187">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="8b5ce-188">Categories</span><span class="sxs-lookup"><span data-stu-id="8b5ce-188">Categories</span></span> |<span data-ttu-id="8b5ce-189">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-189">No</span></span> |<span data-ttu-id="8b5ce-190">Comma-separated list of event categories that should be collected.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-190">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="8b5ce-191">Possible values are Write, Delete, and Action.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-191">Possible values are Write, Delete, and Action.</span></span> |

#### <a name="remove-a-log-profile"></a><span data-ttu-id="8b5ce-192">Remove a log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-192">Remove a log profile</span></span>
```
Remove-AzureRmLogProfile -name my_log_profile
```

### <a name="configure-log-profiles-using-the-azure-cross-platform-cli"></a><span data-ttu-id="8b5ce-193">Configure log profiles Using the Azure Cross-Platform CLI</span><span class="sxs-lookup"><span data-stu-id="8b5ce-193">Configure log profiles Using the Azure Cross-Platform CLI</span></span>
#### <a name="get-existing-log-profile"></a><span data-ttu-id="8b5ce-194">Get existing log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-194">Get existing log profile</span></span>
```
azure insights logprofile list
```
```
azure insights logprofile get --name my_log_profile
```
<span data-ttu-id="8b5ce-195">The `name` property should be the name of your log profile.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-195">The `name` property should be the name of your log profile.</span></span>

#### <a name="add-a-log-profile"></a><span data-ttu-id="8b5ce-196">Add a log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-196">Add a log profile</span></span>
```
azure insights logprofile add --name my_log_profile --storageId /subscriptions/s1/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/my_storage --serviceBusRuleId /subscriptions/s1/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/mytestSB/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope --retentionInDays 90 –categories Write,Delete,Action
```

| <span data-ttu-id="8b5ce-197">Property</span><span class="sxs-lookup"><span data-stu-id="8b5ce-197">Property</span></span> | <span data-ttu-id="8b5ce-198">Required</span><span class="sxs-lookup"><span data-stu-id="8b5ce-198">Required</span></span> | <span data-ttu-id="8b5ce-199">Description</span><span class="sxs-lookup"><span data-stu-id="8b5ce-199">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8b5ce-200">name</span><span class="sxs-lookup"><span data-stu-id="8b5ce-200">name</span></span> |<span data-ttu-id="8b5ce-201">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-201">Yes</span></span> |<span data-ttu-id="8b5ce-202">Name of your log profile.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-202">Name of your log profile.</span></span> |
| <span data-ttu-id="8b5ce-203">storageId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-203">storageId</span></span> |<span data-ttu-id="8b5ce-204">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-204">No</span></span> |<span data-ttu-id="8b5ce-205">Resource ID of the Storage Account to which the Activity Log should be saved.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-205">Resource ID of the Storage Account to which the Activity Log should be saved.</span></span> |
| <span data-ttu-id="8b5ce-206">serviceBusRuleId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-206">serviceBusRuleId</span></span> |<span data-ttu-id="8b5ce-207">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-207">No</span></span> |<span data-ttu-id="8b5ce-208">Service Bus Rule ID for the Service Bus namespace you would like to have event hubs created in.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-208">Service Bus Rule ID for the Service Bus namespace you would like to have event hubs created in.</span></span> <span data-ttu-id="8b5ce-209">Is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-209">Is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span> |
| <span data-ttu-id="8b5ce-210">locations</span><span class="sxs-lookup"><span data-stu-id="8b5ce-210">locations</span></span> |<span data-ttu-id="8b5ce-211">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-211">Yes</span></span> |<span data-ttu-id="8b5ce-212">Comma-separated list of regions for which you would like to collect Activity Log events.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-212">Comma-separated list of regions for which you would like to collect Activity Log events.</span></span> |
| <span data-ttu-id="8b5ce-213">retentionInDays</span><span class="sxs-lookup"><span data-stu-id="8b5ce-213">retentionInDays</span></span> |<span data-ttu-id="8b5ce-214">Yes</span><span class="sxs-lookup"><span data-stu-id="8b5ce-214">Yes</span></span> |<span data-ttu-id="8b5ce-215">Number of days for which events should be retained, between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-215">Number of days for which events should be retained, between 1 and 2147483647.</span></span> <span data-ttu-id="8b5ce-216">A value of zero stores the logs indefinitely (forever).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-216">A value of zero stores the logs indefinitely (forever).</span></span> |
| <span data-ttu-id="8b5ce-217">categories</span><span class="sxs-lookup"><span data-stu-id="8b5ce-217">categories</span></span> |<span data-ttu-id="8b5ce-218">No</span><span class="sxs-lookup"><span data-stu-id="8b5ce-218">No</span></span> |<span data-ttu-id="8b5ce-219">Comma-separated list of event categories that should be collected.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-219">Comma-separated list of event categories that should be collected.</span></span> <span data-ttu-id="8b5ce-220">Possible values are Write, Delete, and Action.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-220">Possible values are Write, Delete, and Action.</span></span> |

#### <a name="remove-a-log-profile"></a><span data-ttu-id="8b5ce-221">Remove a log profile</span><span class="sxs-lookup"><span data-stu-id="8b5ce-221">Remove a log profile</span></span>
```
azure insights logprofile delete --name my_log_profile
```

## <a name="event-schema"></a><span data-ttu-id="8b5ce-222">Event schema</span><span class="sxs-lookup"><span data-stu-id="8b5ce-222">Event schema</span></span>
<span data-ttu-id="8b5ce-223">Each event in the Activity Log has a JSON blob similar to this example:</span><span class="sxs-lookup"><span data-stu-id="8b5ce-223">Each event in the Activity Log has a JSON blob similar to this example:</span></span>

```
{
  "value": [ {
    "authorization": {
      "action": "microsoft.support/supporttickets/write",
      "role": "Subscription Admin",
      "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
    },
    "caller": "admin@contoso.com",
    "channels": "Operation",
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
    },
    "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
    "description": "",
    "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
    "eventName": {
      "value": "EndRequest",
      "localizedValue": "End request"
    },
    "eventSource": {
      "value": "Microsoft.Resources",
      "localizedValue": "Microsoft Resources"
    },
    "httpRequest": {
      "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
      "clientIpAddress": "192.168.35.115",
      "method": "PUT"
    },
    "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
    "level": "Informational",
    "resourceGroupName": "MSSupportGroup",
    "resourceProviderName": {
      "value": "microsoft.support",
      "localizedValue": "microsoft.support"
    },
    "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
    "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
    "operationName": {
      "value": "microsoft.support/supporttickets/write",
      "localizedValue": "microsoft.support/supporttickets/write"
    },
    "properties": {
      "statusCode": "Created"
    },
    "status": {
      "value": "Succeeded",
      "localizedValue": "Succeeded"
    },
    "subStatus": {
      "value": "Created",
      "localizedValue": "Created (HTTP Status Code: 201)"
    },
    "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
    "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
    "subscriptionId": "s1"
  } ],
"nextLink": "https://management.azure.com/########-####-####-####-############$skiptoken=######"
}
```

| <span data-ttu-id="8b5ce-224">Element Name</span><span class="sxs-lookup"><span data-stu-id="8b5ce-224">Element Name</span></span> | <span data-ttu-id="8b5ce-225">Description</span><span class="sxs-lookup"><span data-stu-id="8b5ce-225">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8b5ce-226">authorization</span><span class="sxs-lookup"><span data-stu-id="8b5ce-226">authorization</span></span> |<span data-ttu-id="8b5ce-227">Blob of RBAC properties of the event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-227">Blob of RBAC properties of the event.</span></span> <span data-ttu-id="8b5ce-228">Usually includes the “action”, “role” and “scope” properties.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-228">Usually includes the “action”, “role” and “scope” properties.</span></span> |
| <span data-ttu-id="8b5ce-229">caller</span><span class="sxs-lookup"><span data-stu-id="8b5ce-229">caller</span></span> |<span data-ttu-id="8b5ce-230">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-230">Email address of the user who has performed the operation, UPN claim, or SPN claim based on availability.</span></span> |
| <span data-ttu-id="8b5ce-231">channels</span><span class="sxs-lookup"><span data-stu-id="8b5ce-231">channels</span></span> |<span data-ttu-id="8b5ce-232">One of the following values: “Admin”, “Operation”</span><span class="sxs-lookup"><span data-stu-id="8b5ce-232">One of the following values: “Admin”, “Operation”</span></span> |
| <span data-ttu-id="8b5ce-233">correlationId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-233">correlationId</span></span> |<span data-ttu-id="8b5ce-234">Usually a GUID in the string format.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-234">Usually a GUID in the string format.</span></span> <span data-ttu-id="8b5ce-235">Events that share a correlationId belong to the same uber action.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-235">Events that share a correlationId belong to the same uber action.</span></span> |
| <span data-ttu-id="8b5ce-236">description</span><span class="sxs-lookup"><span data-stu-id="8b5ce-236">description</span></span> |<span data-ttu-id="8b5ce-237">Static text description of an event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-237">Static text description of an event.</span></span> |
| <span data-ttu-id="8b5ce-238">eventDataId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-238">eventDataId</span></span> |<span data-ttu-id="8b5ce-239">Unique identifier of an event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-239">Unique identifier of an event.</span></span> |
| <span data-ttu-id="8b5ce-240">eventSource</span><span class="sxs-lookup"><span data-stu-id="8b5ce-240">eventSource</span></span> |<span data-ttu-id="8b5ce-241">Name of the Azure service or infrastructure that has generated this event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-241">Name of the Azure service or infrastructure that has generated this event.</span></span> |
| <span data-ttu-id="8b5ce-242">httpRequest</span><span class="sxs-lookup"><span data-stu-id="8b5ce-242">httpRequest</span></span> |<span data-ttu-id="8b5ce-243">Blob describing the Http Request.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-243">Blob describing the Http Request.</span></span> <span data-ttu-id="8b5ce-244">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-244">Usually includes the “clientRequestId”, “clientIpAddress” and “method” (HTTP method.</span></span> <span data-ttu-id="8b5ce-245">For example, PUT).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-245">For example, PUT).</span></span> |
| <span data-ttu-id="8b5ce-246">level</span><span class="sxs-lookup"><span data-stu-id="8b5ce-246">level</span></span> |<span data-ttu-id="8b5ce-247">Level of the event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-247">Level of the event.</span></span> <span data-ttu-id="8b5ce-248">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span><span class="sxs-lookup"><span data-stu-id="8b5ce-248">One of the following values: “Critical”, “Error”, “Warning”, “Informational” and “Verbose”</span></span> |
| <span data-ttu-id="8b5ce-249">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="8b5ce-249">resourceGroupName</span></span> |<span data-ttu-id="8b5ce-250">Name of the resource group for the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-250">Name of the resource group for the impacted resource.</span></span> |
| <span data-ttu-id="8b5ce-251">resourceProviderName</span><span class="sxs-lookup"><span data-stu-id="8b5ce-251">resourceProviderName</span></span> |<span data-ttu-id="8b5ce-252">Name of the resource provider for the impacted resource</span><span class="sxs-lookup"><span data-stu-id="8b5ce-252">Name of the resource provider for the impacted resource</span></span> |
| <span data-ttu-id="8b5ce-253">resourceUri</span><span class="sxs-lookup"><span data-stu-id="8b5ce-253">resourceUri</span></span> |<span data-ttu-id="8b5ce-254">Resource id of the impacted resource.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-254">Resource id of the impacted resource.</span></span> |
| <span data-ttu-id="8b5ce-255">operationId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-255">operationId</span></span> |<span data-ttu-id="8b5ce-256">A GUID shared among the events that correspond to a single operation.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-256">A GUID shared among the events that correspond to a single operation.</span></span> |
| <span data-ttu-id="8b5ce-257">operationName</span><span class="sxs-lookup"><span data-stu-id="8b5ce-257">operationName</span></span> |<span data-ttu-id="8b5ce-258">Name of the operation.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-258">Name of the operation.</span></span> |
| <span data-ttu-id="8b5ce-259">properties</span><span class="sxs-lookup"><span data-stu-id="8b5ce-259">properties</span></span> |<span data-ttu-id="8b5ce-260">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-260">Set of `<Key, Value>` pairs (that is, a Dictionary) describing the details of the event.</span></span> |
| <span data-ttu-id="8b5ce-261">status</span><span class="sxs-lookup"><span data-stu-id="8b5ce-261">status</span></span> |<span data-ttu-id="8b5ce-262">String describing the status of the operation.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-262">String describing the status of the operation.</span></span> <span data-ttu-id="8b5ce-263">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-263">Some common values are: Started, In Progress, Succeeded, Failed, Active, Resolved.</span></span> |
| <span data-ttu-id="8b5ce-264">subStatus</span><span class="sxs-lookup"><span data-stu-id="8b5ce-264">subStatus</span></span> |<span data-ttu-id="8b5ce-265">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span><span class="sxs-lookup"><span data-stu-id="8b5ce-265">Usually the HTTP status code of the corresponding REST call, but can also include other strings describing a substatus, such as these common values: OK (HTTP Status Code: 200), Created (HTTP Status Code: 201), Accepted (HTTP Status Code: 202), No Content (HTTP Status Code: 204), Bad Request (HTTP Status Code: 400), Not Found (HTTP Status Code: 404), Conflict (HTTP Status Code: 409), Internal Server Error (HTTP Status Code: 500), Service Unavailable (HTTP Status Code: 503), Gateway Timeout (HTTP Status Code: 504).</span></span> |
| <span data-ttu-id="8b5ce-266">eventTimestamp</span><span class="sxs-lookup"><span data-stu-id="8b5ce-266">eventTimestamp</span></span> |<span data-ttu-id="8b5ce-267">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-267">Timestamp when the event was generated by the Azure service processing the request corresponding the event.</span></span> |
| <span data-ttu-id="8b5ce-268">submissionTimestamp</span><span class="sxs-lookup"><span data-stu-id="8b5ce-268">submissionTimestamp</span></span> |<span data-ttu-id="8b5ce-269">Timestamp when the event became available for querying.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-269">Timestamp when the event became available for querying.</span></span> |
| <span data-ttu-id="8b5ce-270">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="8b5ce-270">subscriptionId</span></span> |<span data-ttu-id="8b5ce-271">Azure Subscription Id.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-271">Azure Subscription Id.</span></span> |
| <span data-ttu-id="8b5ce-272">nextLink</span><span class="sxs-lookup"><span data-stu-id="8b5ce-272">nextLink</span></span> |<span data-ttu-id="8b5ce-273">Continuation token to fetch the next set of results when they are broken up into multiple responses.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-273">Continuation token to fetch the next set of results when they are broken up into multiple responses.</span></span> <span data-ttu-id="8b5ce-274">Typically needed when there are more than 200 records.</span><span class="sxs-lookup"><span data-stu-id="8b5ce-274">Typically needed when there are more than 200 records.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8b5ce-275">Next Steps</span><span class="sxs-lookup"><span data-stu-id="8b5ce-275">Next Steps</span></span>
* [<span data-ttu-id="8b5ce-276">Learn more about the Activity Log (formerly Audit Logs)</span><span class="sxs-lookup"><span data-stu-id="8b5ce-276">Learn more about the Activity Log (formerly Audit Logs)</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="8b5ce-277">Stream the Azure Activity Log to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="8b5ce-277">Stream the Azure Activity Log to Event Hubs</span></span>](monitoring-stream-activity-logs-event-hubs.md)





