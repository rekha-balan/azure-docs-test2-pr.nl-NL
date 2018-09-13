---
title: Overview of Azure Diagnostic Logs | Microsoft Docs
description: Learn what Azure Diagnostic Logs are and how you can use them to understand events occurring within an Azure resource.
author: johnkemnetz
manager: rboucher
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: fa4895ca74fda086c754b6e61db781bec92e231d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669754"
---
# <a name="collect-and-consume-diagnostic-data-from-your-azure-resources"></a><span data-ttu-id="97d2a-103">Collect and consume diagnostic data from your Azure resources</span><span class="sxs-lookup"><span data-stu-id="97d2a-103">Collect and consume diagnostic data from your Azure resources</span></span>

## <a name="what-are-azure-diagnostic-logs"></a><span data-ttu-id="97d2a-104">What are Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-104">What are Azure Diagnostic Logs</span></span>
<span data-ttu-id="97d2a-105">**Azure Diagnostic Logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span><span class="sxs-lookup"><span data-stu-id="97d2a-105">**Azure Diagnostic Logs** are logs emitted by a resource that provide rich, frequent data about the operation of that resource.</span></span> <span data-ttu-id="97d2a-106">The content of these logs varies by resource type.</span><span class="sxs-lookup"><span data-stu-id="97d2a-106">The content of these logs varies by resource type.</span></span> <span data-ttu-id="97d2a-107">For example, Windows event system logs are one category of Diagnostic Log for VMs and blob, table, and queue logs are categories of Diagnostic Logs for storage accounts.</span><span class="sxs-lookup"><span data-stu-id="97d2a-107">For example, Windows event system logs are one category of Diagnostic Log for VMs and blob, table, and queue logs are categories of Diagnostic Logs for storage accounts.</span></span>

<span data-ttu-id="97d2a-108">Diagnostics Logs differ from the [Activity Log (formerly known as Audit Log or Operational Log)](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="97d2a-108">Diagnostics Logs differ from the [Activity Log (formerly known as Audit Log or Operational Log)](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="97d2a-109">The Activity log provides insight into the operations that were performed on resources in your subscription.</span><span class="sxs-lookup"><span data-stu-id="97d2a-109">The Activity log provides insight into the operations that were performed on resources in your subscription.</span></span> <span data-ttu-id="97d2a-110">Diagnostics logs provide insight into operations that your resource performed itself.</span><span class="sxs-lookup"><span data-stu-id="97d2a-110">Diagnostics logs provide insight into operations that your resource performed itself.</span></span>

<span data-ttu-id="97d2a-111">Not all resources support the new type of Diagnostic Logs described here.</span><span class="sxs-lookup"><span data-stu-id="97d2a-111">Not all resources support the new type of Diagnostic Logs described here.</span></span> <span data-ttu-id="97d2a-112">This article contains a section listing which resource types support the new Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="97d2a-112">This article contains a section listing which resource types support the new Diagnostic Logs.</span></span>

![<span data-ttu-id="97d2a-113">Diagnostics Logs vs other types of logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-113">Diagnostics Logs vs other types of logs</span></span> ](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

<span data-ttu-id="97d2a-114">Figure 1: Diagnostics Logs vs other types of logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-114">Figure 1: Diagnostics Logs vs other types of logs</span></span>

## <a name="what-you-can-do-with-diagnostic-logs"></a><span data-ttu-id="97d2a-115">What you can do with Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-115">What you can do with Diagnostic Logs</span></span>
<span data-ttu-id="97d2a-116">Here are some of the things you can do with Diagnostic Logs:</span><span class="sxs-lookup"><span data-stu-id="97d2a-116">Here are some of the things you can do with Diagnostic Logs:</span></span>

![Logical placement of Diagnostic Logs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="97d2a-118">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span><span class="sxs-lookup"><span data-stu-id="97d2a-118">Save them to a [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="97d2a-119">You can specify the retention time (in days) using the **Diagnostic Settings**.</span><span class="sxs-lookup"><span data-stu-id="97d2a-119">You can specify the retention time (in days) using the **Diagnostic Settings**.</span></span>
* <span data-ttu-id="97d2a-120">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span><span class="sxs-lookup"><span data-stu-id="97d2a-120">[Stream them to **Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="97d2a-121">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="97d2a-121">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="97d2a-122">You can use a storage account or event hub namespace that is not in the same subscription as the one emitting logs.</span><span class="sxs-lookup"><span data-stu-id="97d2a-122">You can use a storage account or event hub namespace that is not in the same subscription as the one emitting logs.</span></span> <span data-ttu-id="97d2a-123">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span><span class="sxs-lookup"><span data-stu-id="97d2a-123">The user who configures the setting must have the appropriate RBAC access to both subscriptions.</span></span>

## <a name="diagnostic-settings"></a><span data-ttu-id="97d2a-124">Diagnostic Settings</span><span class="sxs-lookup"><span data-stu-id="97d2a-124">Diagnostic Settings</span></span>
<span data-ttu-id="97d2a-125">Diagnostic Logs for non-Compute resources are configured using Diagnostic Settings.</span><span class="sxs-lookup"><span data-stu-id="97d2a-125">Diagnostic Logs for non-Compute resources are configured using Diagnostic Settings.</span></span> <span data-ttu-id="97d2a-126">**Diagnostic Settings** for a resource control:</span><span class="sxs-lookup"><span data-stu-id="97d2a-126">**Diagnostic Settings** for a resource control:</span></span>

* <span data-ttu-id="97d2a-127">Where Diagnostic Logs are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="97d2a-127">Where Diagnostic Logs are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="97d2a-128">Which Log Categories are sent.</span><span class="sxs-lookup"><span data-stu-id="97d2a-128">Which Log Categories are sent.</span></span>
* <span data-ttu-id="97d2a-129">How long each log category should be retained in a Storage Account</span><span class="sxs-lookup"><span data-stu-id="97d2a-129">How long each log category should be retained in a Storage Account</span></span>
    - <span data-ttu-id="97d2a-130">A retention of zero days means logs are kept forever.</span><span class="sxs-lookup"><span data-stu-id="97d2a-130">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="97d2a-131">Otherwise, the value can be any number of days between 1 and 2147483647.</span><span class="sxs-lookup"><span data-stu-id="97d2a-131">Otherwise, the value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="97d2a-132">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span><span class="sxs-lookup"><span data-stu-id="97d2a-132">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), the retention policies have no effect.</span></span>
    - <span data-ttu-id="97d2a-133">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span><span class="sxs-lookup"><span data-stu-id="97d2a-133">Retention policies are applied per-day, so at the end of a day (UTC), logs from the day that is now beyond the retention policy are deleted.</span></span> <span data-ttu-id="97d2a-134">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span><span class="sxs-lookup"><span data-stu-id="97d2a-134">For example, if you had a retention policy of one day, at the beginning of the day today the logs from the day before yesterday would be deleted.</span></span>

<span data-ttu-id="97d2a-135">These settings are easily configured via the Diagnostics blade for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="97d2a-135">These settings are easily configured via the Diagnostics blade for a resource in the Azure portal, via Azure PowerShell and CLI commands, or via the [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="97d2a-136">Diagnostic logs and metrics for Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="97d2a-136">Diagnostic logs and metrics for Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-to-enable-collection-of-diagnostic-logs"></a><span data-ttu-id="97d2a-137">How to enable collection of Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-137">How to enable collection of Diagnostic Logs</span></span>
<span data-ttu-id="97d2a-138">Collection of Diagnostic Logs can be enabled as part of creating a resource or after a resource is created via the resource’s blade in the Portal.</span><span class="sxs-lookup"><span data-stu-id="97d2a-138">Collection of Diagnostic Logs can be enabled as part of creating a resource or after a resource is created via the resource’s blade in the Portal.</span></span> <span data-ttu-id="97d2a-139">You can also enable Diagnostic Logs at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span><span class="sxs-lookup"><span data-stu-id="97d2a-139">You can also enable Diagnostic Logs at any point using Azure PowerShell or CLI commands, or using the Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="97d2a-140">These instructions may not apply directly to every resource.</span><span class="sxs-lookup"><span data-stu-id="97d2a-140">These instructions may not apply directly to every resource.</span></span> <span data-ttu-id="97d2a-141">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span><span class="sxs-lookup"><span data-stu-id="97d2a-141">See the schema links at the bottom of this page to understand special steps that may apply to certain resource types.</span></span>
>
>

[<span data-ttu-id="97d2a-142">This article shows how you can use a resource template to enable Diagnostic Settings when creating a resource</span><span class="sxs-lookup"><span data-stu-id="97d2a-142">This article shows how you can use a resource template to enable Diagnostic Settings when creating a resource</span></span>](monitoring-enable-diagnostic-logs-using-template.md)

### <a name="enable-diagnostic-logs-in-the-portal"></a><span data-ttu-id="97d2a-143">Enable Diagnostic Logs in the portal</span><span class="sxs-lookup"><span data-stu-id="97d2a-143">Enable Diagnostic Logs in the portal</span></span>
<span data-ttu-id="97d2a-144">You can enable Diagnostic Logs in the Azure portal when you create compute resource types by enabling the Windows or Linux Azure Diagnostics extension:</span><span class="sxs-lookup"><span data-stu-id="97d2a-144">You can enable Diagnostic Logs in the Azure portal when you create compute resource types by enabling the Windows or Linux Azure Diagnostics extension:</span></span>

1. <span data-ttu-id="97d2a-145">Go to **New** and choose the resource you are interested in.</span><span class="sxs-lookup"><span data-stu-id="97d2a-145">Go to **New** and choose the resource you are interested in.</span></span>
2. <span data-ttu-id="97d2a-146">After configuring the basic settings and selecting a size, in the **Settings** blade, under **Monitoring**, select **Enabled** and choose a storage account where you would like to store the Diagnostic Logs.</span><span class="sxs-lookup"><span data-stu-id="97d2a-146">After configuring the basic settings and selecting a size, in the **Settings** blade, under **Monitoring**, select **Enabled** and choose a storage account where you would like to store the Diagnostic Logs.</span></span> <span data-ttu-id="97d2a-147">You are charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span><span class="sxs-lookup"><span data-stu-id="97d2a-147">You are charged normal data rates for storage and transactions when you send diagnostics to a storage account.</span></span>

   ![Enable Diagnostic Logs during resource creation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/enable-portal-new.png)
3. <span data-ttu-id="97d2a-149">Click **OK** and create the resource.</span><span class="sxs-lookup"><span data-stu-id="97d2a-149">Click **OK** and create the resource.</span></span>

<span data-ttu-id="97d2a-150">For non-compute resources, you can enable Diagnostic Logs in the Azure portal after a resource has been created by doing the following:</span><span class="sxs-lookup"><span data-stu-id="97d2a-150">For non-compute resources, you can enable Diagnostic Logs in the Azure portal after a resource has been created by doing the following:</span></span>

1. <span data-ttu-id="97d2a-151">Go to the blade for the resource and open the **Diagnostics** blade.</span><span class="sxs-lookup"><span data-stu-id="97d2a-151">Go to the blade for the resource and open the **Diagnostics** blade.</span></span>
2. <span data-ttu-id="97d2a-152">Click **On** and pick a Storage Account and/or Event Hub.</span><span class="sxs-lookup"><span data-stu-id="97d2a-152">Click **On** and pick a Storage Account and/or Event Hub.</span></span>

   ![Enable Diagnostic Logs after resource creation](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/enable-portal-existing.png)
3. <span data-ttu-id="97d2a-154">Under **Logs**, select which **Log Categories** you would like to collect or stream.</span><span class="sxs-lookup"><span data-stu-id="97d2a-154">Under **Logs**, select which **Log Categories** you would like to collect or stream.</span></span>
4. <span data-ttu-id="97d2a-155">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="97d2a-155">Click **Save**.</span></span>

### <a name="enable-diagnostic-logs-via-powershell"></a><span data-ttu-id="97d2a-156">Enable Diagnostic Logs via PowerShell</span><span class="sxs-lookup"><span data-stu-id="97d2a-156">Enable Diagnostic Logs via PowerShell</span></span>
<span data-ttu-id="97d2a-157">To enable Diagnostic Logs via the Azure PowerShell Cmdlets, use the following commands.</span><span class="sxs-lookup"><span data-stu-id="97d2a-157">To enable Diagnostic Logs via the Azure PowerShell Cmdlets, use the following commands.</span></span>

<span data-ttu-id="97d2a-158">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-158">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="97d2a-159">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span><span class="sxs-lookup"><span data-stu-id="97d2a-159">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="97d2a-160">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-160">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your service bus rule id] -Enabled $true
```

<span data-ttu-id="97d2a-161">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="97d2a-161">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="97d2a-162">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-162">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

```powershell
    Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of the log analytics workspace] -Enabled $true
```

<span data-ttu-id="97d2a-163">You can obtain the resource id of your Log Analytics workspace using the following command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-163">You can obtain the resource id of your Log Analytics workspace using the following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="97d2a-164">You can combine these parameters to enable multiple output options.</span><span class="sxs-lookup"><span data-stu-id="97d2a-164">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-diagnostic-logs-via-cli"></a><span data-ttu-id="97d2a-165">Enable Diagnostic Logs via CLI</span><span class="sxs-lookup"><span data-stu-id="97d2a-165">Enable Diagnostic Logs via CLI</span></span>
<span data-ttu-id="97d2a-166">To enable Diagnostic Logs via the Azure CLI, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="97d2a-166">To enable Diagnostic Logs via the Azure CLI, use the following commands:</span></span>

<span data-ttu-id="97d2a-167">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-167">To enable storage of Diagnostic Logs in a Storage Account, use this command:</span></span>

```azurecli
    azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="97d2a-168">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span><span class="sxs-lookup"><span data-stu-id="97d2a-168">The Storage Account ID is the resource id for the storage account to which you want to send the logs.</span></span>

<span data-ttu-id="97d2a-169">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-169">To enable streaming of Diagnostic Logs to an Event Hub, use this command:</span></span>

```azurecli
    azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="97d2a-170">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="97d2a-170">The Service Bus Rule ID is a string with this format: `{service bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="97d2a-171">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span><span class="sxs-lookup"><span data-stu-id="97d2a-171">To enable sending of Diagnostic Logs to a Log Analytics workspace, use this command:</span></span>

```azurecli
    azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of the log analytics workspace> --enabled true
```

<span data-ttu-id="97d2a-172">You can combine these parameters to enable multiple output options.</span><span class="sxs-lookup"><span data-stu-id="97d2a-172">You can combine these parameters to enable multiple output options.</span></span>

### <a name="enable-diagnostic-logs-via-rest-api"></a><span data-ttu-id="97d2a-173">Enable Diagnostic Logs via REST API</span><span class="sxs-lookup"><span data-stu-id="97d2a-173">Enable Diagnostic Logs via REST API</span></span>
<span data-ttu-id="97d2a-174">To change Diagnostic Settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="97d2a-174">To change Diagnostic Settings using the Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-diagnostic-settings-in-the-portal"></a><span data-ttu-id="97d2a-175">Manage Diagnostic Settings in the portal</span><span class="sxs-lookup"><span data-stu-id="97d2a-175">Manage Diagnostic Settings in the portal</span></span>
<span data-ttu-id="97d2a-176">Ensure that all of your resources are set up with diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="97d2a-176">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="97d2a-177">Navigate to the **Monitoring** blade in the portal and open the **Diagnostic Logs** blade.</span><span class="sxs-lookup"><span data-stu-id="97d2a-177">Navigate to the **Monitoring** blade in the portal and open the **Diagnostic Logs** blade.</span></span>

![Diagnostic Logs blade in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/manage-portal-nav.png)

<span data-ttu-id="97d2a-179">You may have to click "More services" to find the Monitoring blade.</span><span class="sxs-lookup"><span data-stu-id="97d2a-179">You may have to click "More services" to find the Monitoring blade.</span></span>

<span data-ttu-id="97d2a-180">In this blade, you can view and filter all resources that support Diagnostic Logs to see if they have diagnostics enabled.</span><span class="sxs-lookup"><span data-stu-id="97d2a-180">In this blade, you can view and filter all resources that support Diagnostic Logs to see if they have diagnostics enabled.</span></span> <span data-ttu-id="97d2a-181">You can also check which storage account, event hub, and/or Log Analytics workspace those logs are flowing to.</span><span class="sxs-lookup"><span data-stu-id="97d2a-181">You can also check which storage account, event hub, and/or Log Analytics workspace those logs are flowing to.</span></span>

![Diagnostic Logs blade results in portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/manage-portal-blade.png)

<span data-ttu-id="97d2a-183">Clicking on a resource shows all logs that have been stored in the storage account and give you the option to turn off or modify the diagnostic settings.</span><span class="sxs-lookup"><span data-stu-id="97d2a-183">Clicking on a resource shows all logs that have been stored in the storage account and give you the option to turn off or modify the diagnostic settings.</span></span> <span data-ttu-id="97d2a-184">Click the download icon to download logs for a particular time period.</span><span class="sxs-lookup"><span data-stu-id="97d2a-184">Click the download icon to download logs for a particular time period.</span></span>

![Diagnostic Logs blade one resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/monitoring-overview-of-diagnostic-logs/manage-portal-logs.png)

> [!NOTE]
> <span data-ttu-id="97d2a-186">Diagnostic logs only appear in this view and be available for download if you have configured diagnostic settings to save them to a storage account.</span><span class="sxs-lookup"><span data-stu-id="97d2a-186">Diagnostic logs only appear in this view and be available for download if you have configured diagnostic settings to save them to a storage account.</span></span>
>
>

<span data-ttu-id="97d2a-187">Clicking on the link for **Diagnostic Settings** shows the Diagnostic Settings blade, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span><span class="sxs-lookup"><span data-stu-id="97d2a-187">Clicking on the link for **Diagnostic Settings** shows the Diagnostic Settings blade, where you can enable, disable, or modify your diagnostic settings for the selected resource.</span></span>

## <a name="supported-services-and-schema-for-diagnostic-logs"></a><span data-ttu-id="97d2a-188">Supported services and schema for Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-188">Supported services and schema for Diagnostic Logs</span></span>
<span data-ttu-id="97d2a-189">The schema for Diagnostic Logs varies depending on the resource and log category.</span><span class="sxs-lookup"><span data-stu-id="97d2a-189">The schema for Diagnostic Logs varies depending on the resource and log category.</span></span>   

| <span data-ttu-id="97d2a-190">Service</span><span class="sxs-lookup"><span data-stu-id="97d2a-190">Service</span></span> | <span data-ttu-id="97d2a-191">Schema & Docs</span><span class="sxs-lookup"><span data-stu-id="97d2a-191">Schema & Docs</span></span> |
| --- | --- |
| <span data-ttu-id="97d2a-192">Load Balancer</span><span class="sxs-lookup"><span data-stu-id="97d2a-192">Load Balancer</span></span> |[<span data-ttu-id="97d2a-193">Log analytics for Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="97d2a-193">Log analytics for Azure Load Balancer</span></span>](../load-balancer/load-balancer-monitor-log.md) |
| <span data-ttu-id="97d2a-194">Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="97d2a-194">Network Security Groups</span></span> |[<span data-ttu-id="97d2a-195">Log analytics for network security groups (NSGs)</span><span class="sxs-lookup"><span data-stu-id="97d2a-195">Log analytics for network security groups (NSGs)</span></span>](../virtual-network/virtual-network-nsg-manage-log.md) |
| <span data-ttu-id="97d2a-196">Application Gateways</span><span class="sxs-lookup"><span data-stu-id="97d2a-196">Application Gateways</span></span> |[<span data-ttu-id="97d2a-197">Diagnostics Logging for Application Gateway</span><span class="sxs-lookup"><span data-stu-id="97d2a-197">Diagnostics Logging for Application Gateway</span></span>](../application-gateway/application-gateway-diagnostics.md) |
| <span data-ttu-id="97d2a-198">Key Vault</span><span class="sxs-lookup"><span data-stu-id="97d2a-198">Key Vault</span></span> |[<span data-ttu-id="97d2a-199">Azure Key Vault Logging</span><span class="sxs-lookup"><span data-stu-id="97d2a-199">Azure Key Vault Logging</span></span>](../key-vault/key-vault-logging.md) |
| <span data-ttu-id="97d2a-200">Azure Search</span><span class="sxs-lookup"><span data-stu-id="97d2a-200">Azure Search</span></span> |[<span data-ttu-id="97d2a-201">Enabling and using Search Traffic Analytics</span><span class="sxs-lookup"><span data-stu-id="97d2a-201">Enabling and using Search Traffic Analytics</span></span>](../search/search-traffic-analytics.md) |
| <span data-ttu-id="97d2a-202">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="97d2a-202">Data Lake Store</span></span> |[<span data-ttu-id="97d2a-203">Accessing diagnostic logs for Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="97d2a-203">Accessing diagnostic logs for Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-diagnostic-logs.md) |
| <span data-ttu-id="97d2a-204">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="97d2a-204">Data Lake Analytics</span></span> |[<span data-ttu-id="97d2a-205">Accessing diagnostic logs for Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="97d2a-205">Accessing diagnostic logs for Azure Data Lake Analytics</span></span>](../data-lake-analytics/data-lake-analytics-diagnostic-logs.md) |
| <span data-ttu-id="97d2a-206">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="97d2a-206">Logic Apps</span></span> |[<span data-ttu-id="97d2a-207">Logic Apps B2B custom tracking schema</span><span class="sxs-lookup"><span data-stu-id="97d2a-207">Logic Apps B2B custom tracking schema</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md) |
| <span data-ttu-id="97d2a-208">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="97d2a-208">Azure Batch</span></span> |[<span data-ttu-id="97d2a-209">Azure Batch diagnostic logging</span><span class="sxs-lookup"><span data-stu-id="97d2a-209">Azure Batch diagnostic logging</span></span>](../batch/batch-diagnostics.md) |
| <span data-ttu-id="97d2a-210">Azure Automation</span><span class="sxs-lookup"><span data-stu-id="97d2a-210">Azure Automation</span></span> |[<span data-ttu-id="97d2a-211">Log analytics for Azure Automation</span><span class="sxs-lookup"><span data-stu-id="97d2a-211">Log analytics for Azure Automation</span></span>](../automation/automation-manage-send-joblogs-log-analytics.md) |
| <span data-ttu-id="97d2a-212">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="97d2a-212">Event Hubs</span></span> |[<span data-ttu-id="97d2a-213">Azure Event Hubs diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-213">Azure Event Hubs diagnostic logs</span></span>](../event-hubs/event-hubs-diagnostic-logs.md) |
| <span data-ttu-id="97d2a-214">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="97d2a-214">Stream Analytics</span></span> |[<span data-ttu-id="97d2a-215">Job diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-215">Job diagnostic logs</span></span>](../stream-analytics/stream-analytics-job-diagnostic-logs.md) |
| <span data-ttu-id="97d2a-216">Service Bus</span><span class="sxs-lookup"><span data-stu-id="97d2a-216">Service Bus</span></span> |[<span data-ttu-id="97d2a-217">Azure Service Bus diagnostic logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-217">Azure Service Bus diagnostic logs</span></span>](../service-bus-messaging/service-bus-diagnostic-logs.md) |


## <a name="supported-log-categories-per-resource-type"></a><span data-ttu-id="97d2a-218">Supported log categories per resource type</span><span class="sxs-lookup"><span data-stu-id="97d2a-218">Supported log categories per resource type</span></span>
|<span data-ttu-id="97d2a-219">Resource Type</span><span class="sxs-lookup"><span data-stu-id="97d2a-219">Resource Type</span></span>|<span data-ttu-id="97d2a-220">Category</span><span class="sxs-lookup"><span data-stu-id="97d2a-220">Category</span></span>|<span data-ttu-id="97d2a-221">Category Display Name</span><span class="sxs-lookup"><span data-stu-id="97d2a-221">Category Display Name</span></span>|
|---|---|---|
|<span data-ttu-id="97d2a-222">Microsoft.ApiManagement/service</span><span class="sxs-lookup"><span data-stu-id="97d2a-222">Microsoft.ApiManagement/service</span></span>|<span data-ttu-id="97d2a-223">GatewayLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-223">GatewayLogs</span></span>|<span data-ttu-id="97d2a-224">Logs related to ApiManagement Gateway</span><span class="sxs-lookup"><span data-stu-id="97d2a-224">Logs related to ApiManagement Gateway</span></span>|
|<span data-ttu-id="97d2a-225">Microsoft.Automation/automationAccounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-225">Microsoft.Automation/automationAccounts</span></span>|<span data-ttu-id="97d2a-226">JobLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-226">JobLogs</span></span>|<span data-ttu-id="97d2a-227">Job Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-227">Job Logs</span></span>|
|<span data-ttu-id="97d2a-228">Microsoft.Automation/automationAccounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-228">Microsoft.Automation/automationAccounts</span></span>|<span data-ttu-id="97d2a-229">JobStreams</span><span class="sxs-lookup"><span data-stu-id="97d2a-229">JobStreams</span></span>|<span data-ttu-id="97d2a-230">Job Streams</span><span class="sxs-lookup"><span data-stu-id="97d2a-230">Job Streams</span></span>|
|<span data-ttu-id="97d2a-231">Microsoft.Automation/automationAccounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-231">Microsoft.Automation/automationAccounts</span></span>|<span data-ttu-id="97d2a-232">DscNodeStatus</span><span class="sxs-lookup"><span data-stu-id="97d2a-232">DscNodeStatus</span></span>|<span data-ttu-id="97d2a-233">Dsc Node Status</span><span class="sxs-lookup"><span data-stu-id="97d2a-233">Dsc Node Status</span></span>|
|<span data-ttu-id="97d2a-234">Microsoft.Batch/batchAccounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-234">Microsoft.Batch/batchAccounts</span></span>|<span data-ttu-id="97d2a-235">ServiceLog</span><span class="sxs-lookup"><span data-stu-id="97d2a-235">ServiceLog</span></span>|<span data-ttu-id="97d2a-236">Service Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-236">Service Logs</span></span>|
|<span data-ttu-id="97d2a-237">Microsoft.DataLakeAnalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-237">Microsoft.DataLakeAnalytics/accounts</span></span>|<span data-ttu-id="97d2a-238">Audit</span><span class="sxs-lookup"><span data-stu-id="97d2a-238">Audit</span></span>|<span data-ttu-id="97d2a-239">Audit Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-239">Audit Logs</span></span>|
|<span data-ttu-id="97d2a-240">Microsoft.DataLakeAnalytics/accounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-240">Microsoft.DataLakeAnalytics/accounts</span></span>|<span data-ttu-id="97d2a-241">Requests</span><span class="sxs-lookup"><span data-stu-id="97d2a-241">Requests</span></span>|<span data-ttu-id="97d2a-242">Request Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-242">Request Logs</span></span>|
|<span data-ttu-id="97d2a-243">Microsoft.DataLakeStore/accounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-243">Microsoft.DataLakeStore/accounts</span></span>|<span data-ttu-id="97d2a-244">Audit</span><span class="sxs-lookup"><span data-stu-id="97d2a-244">Audit</span></span>|<span data-ttu-id="97d2a-245">Audit Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-245">Audit Logs</span></span>|
|<span data-ttu-id="97d2a-246">Microsoft.DataLakeStore/accounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-246">Microsoft.DataLakeStore/accounts</span></span>|<span data-ttu-id="97d2a-247">Requests</span><span class="sxs-lookup"><span data-stu-id="97d2a-247">Requests</span></span>|<span data-ttu-id="97d2a-248">Request Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-248">Request Logs</span></span>|
|<span data-ttu-id="97d2a-249">Microsoft.EventHub/namespaces</span><span class="sxs-lookup"><span data-stu-id="97d2a-249">Microsoft.EventHub/namespaces</span></span>|<span data-ttu-id="97d2a-250">ArchiveLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-250">ArchiveLogs</span></span>|<span data-ttu-id="97d2a-251">Archive Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-251">Archive Logs</span></span>|
|<span data-ttu-id="97d2a-252">Microsoft.EventHub/namespaces</span><span class="sxs-lookup"><span data-stu-id="97d2a-252">Microsoft.EventHub/namespaces</span></span>|<span data-ttu-id="97d2a-253">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-253">OperationalLogs</span></span>|<span data-ttu-id="97d2a-254">Operational Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-254">Operational Logs</span></span>|
|<span data-ttu-id="97d2a-255">Microsoft.EventHub/namespaces</span><span class="sxs-lookup"><span data-stu-id="97d2a-255">Microsoft.EventHub/namespaces</span></span>|<span data-ttu-id="97d2a-256">AutoScaleLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-256">AutoScaleLogs</span></span>|<span data-ttu-id="97d2a-257">Auto Scale Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-257">Auto Scale Logs</span></span>|
|<span data-ttu-id="97d2a-258">Microsoft.KeyVault/vaults</span><span class="sxs-lookup"><span data-stu-id="97d2a-258">Microsoft.KeyVault/vaults</span></span>|<span data-ttu-id="97d2a-259">AuditEvent</span><span class="sxs-lookup"><span data-stu-id="97d2a-259">AuditEvent</span></span>|<span data-ttu-id="97d2a-260">Audit Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-260">Audit Logs</span></span>|
|<span data-ttu-id="97d2a-261">Microsoft.Logic/workflows</span><span class="sxs-lookup"><span data-stu-id="97d2a-261">Microsoft.Logic/workflows</span></span>|<span data-ttu-id="97d2a-262">WorkflowRuntime</span><span class="sxs-lookup"><span data-stu-id="97d2a-262">WorkflowRuntime</span></span>|<span data-ttu-id="97d2a-263">Workflow runtime diagnostic events</span><span class="sxs-lookup"><span data-stu-id="97d2a-263">Workflow runtime diagnostic events</span></span>|
|<span data-ttu-id="97d2a-264">Microsoft.Logic/integrationAccounts</span><span class="sxs-lookup"><span data-stu-id="97d2a-264">Microsoft.Logic/integrationAccounts</span></span>|<span data-ttu-id="97d2a-265">IntegrationAccountTrackingEvents</span><span class="sxs-lookup"><span data-stu-id="97d2a-265">IntegrationAccountTrackingEvents</span></span>|<span data-ttu-id="97d2a-266">Integration Account track events</span><span class="sxs-lookup"><span data-stu-id="97d2a-266">Integration Account track events</span></span>|
|<span data-ttu-id="97d2a-267">Microsoft.Network/networksecuritygroups</span><span class="sxs-lookup"><span data-stu-id="97d2a-267">Microsoft.Network/networksecuritygroups</span></span>|<span data-ttu-id="97d2a-268">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="97d2a-268">NetworkSecurityGroupEvent</span></span>|<span data-ttu-id="97d2a-269">Network Security Group Event</span><span class="sxs-lookup"><span data-stu-id="97d2a-269">Network Security Group Event</span></span>|
|<span data-ttu-id="97d2a-270">Microsoft.Network/networksecuritygroups</span><span class="sxs-lookup"><span data-stu-id="97d2a-270">Microsoft.Network/networksecuritygroups</span></span>|<span data-ttu-id="97d2a-271">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="97d2a-271">NetworkSecurityGroupRuleCounter</span></span>|<span data-ttu-id="97d2a-272">Network Security Group Rule Counter</span><span class="sxs-lookup"><span data-stu-id="97d2a-272">Network Security Group Rule Counter</span></span>|
|<span data-ttu-id="97d2a-273">Microsoft.Network/networksecuritygroups</span><span class="sxs-lookup"><span data-stu-id="97d2a-273">Microsoft.Network/networksecuritygroups</span></span>|<span data-ttu-id="97d2a-274">NetworkSecurityGroupFlowEvent</span><span class="sxs-lookup"><span data-stu-id="97d2a-274">NetworkSecurityGroupFlowEvent</span></span>|<span data-ttu-id="97d2a-275">Network Security Group Rule Flow Event</span><span class="sxs-lookup"><span data-stu-id="97d2a-275">Network Security Group Rule Flow Event</span></span>|
|<span data-ttu-id="97d2a-276">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="97d2a-276">Microsoft.Network/loadBalancers</span></span>|<span data-ttu-id="97d2a-277">LoadBalancerAlertEvent</span><span class="sxs-lookup"><span data-stu-id="97d2a-277">LoadBalancerAlertEvent</span></span>|<span data-ttu-id="97d2a-278">Load Balancer Alert Events</span><span class="sxs-lookup"><span data-stu-id="97d2a-278">Load Balancer Alert Events</span></span>|
|<span data-ttu-id="97d2a-279">Microsoft.Network/loadBalancers</span><span class="sxs-lookup"><span data-stu-id="97d2a-279">Microsoft.Network/loadBalancers</span></span>|<span data-ttu-id="97d2a-280">LoadBalancerProbeHealthStatus</span><span class="sxs-lookup"><span data-stu-id="97d2a-280">LoadBalancerProbeHealthStatus</span></span>|<span data-ttu-id="97d2a-281">Load Balancer Probe Health Status</span><span class="sxs-lookup"><span data-stu-id="97d2a-281">Load Balancer Probe Health Status</span></span>|
|<span data-ttu-id="97d2a-282">Microsoft.Network/applicationGateways</span><span class="sxs-lookup"><span data-stu-id="97d2a-282">Microsoft.Network/applicationGateways</span></span>|<span data-ttu-id="97d2a-283">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="97d2a-283">ApplicationGatewayAccessLog</span></span>|<span data-ttu-id="97d2a-284">Application Gateway Access Log</span><span class="sxs-lookup"><span data-stu-id="97d2a-284">Application Gateway Access Log</span></span>|
|<span data-ttu-id="97d2a-285">Microsoft.Network/applicationGateways</span><span class="sxs-lookup"><span data-stu-id="97d2a-285">Microsoft.Network/applicationGateways</span></span>|<span data-ttu-id="97d2a-286">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="97d2a-286">ApplicationGatewayPerformanceLog</span></span>|<span data-ttu-id="97d2a-287">Application Gateway Performance Log</span><span class="sxs-lookup"><span data-stu-id="97d2a-287">Application Gateway Performance Log</span></span>|
|<span data-ttu-id="97d2a-288">Microsoft.Network/applicationGateways</span><span class="sxs-lookup"><span data-stu-id="97d2a-288">Microsoft.Network/applicationGateways</span></span>|<span data-ttu-id="97d2a-289">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="97d2a-289">ApplicationGatewayFirewallLog</span></span>|<span data-ttu-id="97d2a-290">Application Gateway Firewall Log</span><span class="sxs-lookup"><span data-stu-id="97d2a-290">Application Gateway Firewall Log</span></span>|
|<span data-ttu-id="97d2a-291">Microsoft.Network/expressRouteCircuits</span><span class="sxs-lookup"><span data-stu-id="97d2a-291">Microsoft.Network/expressRouteCircuits</span></span>|<span data-ttu-id="97d2a-292">GWMCountersTable</span><span class="sxs-lookup"><span data-stu-id="97d2a-292">GWMCountersTable</span></span>|<span data-ttu-id="97d2a-293">Table of GWM counters</span><span class="sxs-lookup"><span data-stu-id="97d2a-293">Table of GWM counters</span></span>|
|<span data-ttu-id="97d2a-294">Microsoft.Search/searchServices</span><span class="sxs-lookup"><span data-stu-id="97d2a-294">Microsoft.Search/searchServices</span></span>|<span data-ttu-id="97d2a-295">OperationLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-295">OperationLogs</span></span>|<span data-ttu-id="97d2a-296">Operation Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-296">Operation Logs</span></span>|
|<span data-ttu-id="97d2a-297">Microsoft.ServerManagement/nodes</span><span class="sxs-lookup"><span data-stu-id="97d2a-297">Microsoft.ServerManagement/nodes</span></span>|<span data-ttu-id="97d2a-298">RequestLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-298">RequestLogs</span></span>|<span data-ttu-id="97d2a-299">Request Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-299">Request Logs</span></span>|
|<span data-ttu-id="97d2a-300">Microsoft.ServiceBus/namespaces</span><span class="sxs-lookup"><span data-stu-id="97d2a-300">Microsoft.ServiceBus/namespaces</span></span>|<span data-ttu-id="97d2a-301">OperationalLogs</span><span class="sxs-lookup"><span data-stu-id="97d2a-301">OperationalLogs</span></span>|<span data-ttu-id="97d2a-302">Operational Logs</span><span class="sxs-lookup"><span data-stu-id="97d2a-302">Operational Logs</span></span>|
|<span data-ttu-id="97d2a-303">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="97d2a-303">Microsoft.StreamAnalytics/streamingjobs</span></span>|<span data-ttu-id="97d2a-304">Execution</span><span class="sxs-lookup"><span data-stu-id="97d2a-304">Execution</span></span>|<span data-ttu-id="97d2a-305">Execution</span><span class="sxs-lookup"><span data-stu-id="97d2a-305">Execution</span></span>|
|<span data-ttu-id="97d2a-306">Microsoft.StreamAnalytics/streamingjobs</span><span class="sxs-lookup"><span data-stu-id="97d2a-306">Microsoft.StreamAnalytics/streamingjobs</span></span>|<span data-ttu-id="97d2a-307">Authoring</span><span class="sxs-lookup"><span data-stu-id="97d2a-307">Authoring</span></span>|<span data-ttu-id="97d2a-308">Authoring</span><span class="sxs-lookup"><span data-stu-id="97d2a-308">Authoring</span></span>|

## <a name="next-steps"></a><span data-ttu-id="97d2a-309">Next Steps</span><span class="sxs-lookup"><span data-stu-id="97d2a-309">Next Steps</span></span>

* [<span data-ttu-id="97d2a-310">Stream Diagnostic Logs to **Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="97d2a-310">Stream Diagnostic Logs to **Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="97d2a-311">Change Diagnostic Settings using the Azure Monitor REST API</span><span class="sxs-lookup"><span data-stu-id="97d2a-311">Change Diagnostic Settings using the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="97d2a-312">Analyze logs from Azure storage with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="97d2a-312">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)







