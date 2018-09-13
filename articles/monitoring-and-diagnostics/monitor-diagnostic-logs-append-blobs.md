---
title: Prepare for format change to Azure Monitor diagnostic logs
description: Azure Diagnostic Logs will be moved to use append blobs on November 1, 2018.
author: johnkemnetz
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 07/06/2018
ms.author: johnkem
ms.component: logs
ms.openlocfilehash: b83c67e5c2ca47e73c1743d8eeaea03a8d92ea1f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864829"
---
# <a name="prepare-for-format-change-to-azure-monitor-diagnostic-logs-archived-to-a-storage-account"></a><span data-ttu-id="3750f-103">Prepare for format change to Azure Monitor diagnostic logs archived to a storage account</span><span class="sxs-lookup"><span data-stu-id="3750f-103">Prepare for format change to Azure Monitor diagnostic logs archived to a storage account</span></span>

> [!WARNING]
> <span data-ttu-id="3750f-104">If you are sending [Azure resource diagnostic logs or metrics to a storage account using resource diagnostic settings](./monitoring-archive-diagnostic-logs.md) or [activity logs to a storage account using log profiles](./monitoring-archive-activity-log.md), the format of the data in the storage account will change to JSON Lines on Nov. 1, 2018.</span><span class="sxs-lookup"><span data-stu-id="3750f-104">If you are sending [Azure resource diagnostic logs or metrics to a storage account using resource diagnostic settings](./monitoring-archive-diagnostic-logs.md) or [activity logs to a storage account using log profiles](./monitoring-archive-activity-log.md), the format of the data in the storage account will change to JSON Lines on Nov. 1, 2018.</span></span> <span data-ttu-id="3750f-105">The instructions below describe the impact and how to update your tooling to handle the new format.</span><span class="sxs-lookup"><span data-stu-id="3750f-105">The instructions below describe the impact and how to update your tooling to handle the new format.</span></span> 
>
> 

## <a name="what-is-changing"></a><span data-ttu-id="3750f-106">What is changing</span><span class="sxs-lookup"><span data-stu-id="3750f-106">What is changing</span></span>

<span data-ttu-id="3750f-107">Azure Monitor offers a capability that enables you to send resource diagnostic data and activity log data into an Azure storage account, Event Hubs namespace, or into Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="3750f-107">Azure Monitor offers a capability that enables you to send resource diagnostic data and activity log data into an Azure storage account, Event Hubs namespace, or into Log Analytics.</span></span> <span data-ttu-id="3750f-108">In order to address a system performance issue, on **November 1, 2018 at 12:00 midnight UTC** the format of log data send to blob storage will change.</span><span class="sxs-lookup"><span data-stu-id="3750f-108">In order to address a system performance issue, on **November 1, 2018 at 12:00 midnight UTC** the format of log data send to blob storage will change.</span></span> <span data-ttu-id="3750f-109">If you have tooling that is reading data out of blob storage, you need to update your tooling to understand the new data format.</span><span class="sxs-lookup"><span data-stu-id="3750f-109">If you have tooling that is reading data out of blob storage, you need to update your tooling to understand the new data format.</span></span>

* <span data-ttu-id="3750f-110">On Thursday, November 1, 2018 at 12:00 midnight UTC, the blob format will change to be [JSON Lines](http://jsonlines.org/).</span><span class="sxs-lookup"><span data-stu-id="3750f-110">On Thursday, November 1, 2018 at 12:00 midnight UTC, the blob format will change to be [JSON Lines](http://jsonlines.org/).</span></span> <span data-ttu-id="3750f-111">This means each record will be delimited by a newline, with no outer records array and no commas between JSON records.</span><span class="sxs-lookup"><span data-stu-id="3750f-111">This means each record will be delimited by a newline, with no outer records array and no commas between JSON records.</span></span>
* <span data-ttu-id="3750f-112">The blob format changes for all diagnostic settings across all subscriptions at once.</span><span class="sxs-lookup"><span data-stu-id="3750f-112">The blob format changes for all diagnostic settings across all subscriptions at once.</span></span> <span data-ttu-id="3750f-113">The first PT1H.json file emitted for November 1 will use this new format.</span><span class="sxs-lookup"><span data-stu-id="3750f-113">The first PT1H.json file emitted for November 1 will use this new format.</span></span> <span data-ttu-id="3750f-114">The blob and container names remain the same.</span><span class="sxs-lookup"><span data-stu-id="3750f-114">The blob and container names remain the same.</span></span>
* <span data-ttu-id="3750f-115">Setting a diagnostic setting between now and November 1 continues to emit data in the current format until November 1.</span><span class="sxs-lookup"><span data-stu-id="3750f-115">Setting a diagnostic setting between now and November 1 continues to emit data in the current format until November 1.</span></span>
* <span data-ttu-id="3750f-116">This change will occur at once across all public cloud regions.</span><span class="sxs-lookup"><span data-stu-id="3750f-116">This change will occur at once across all public cloud regions.</span></span> <span data-ttu-id="3750f-117">The change will not occur in Azure China, Azure Germany, or Azure Government clouds yet.</span><span class="sxs-lookup"><span data-stu-id="3750f-117">The change will not occur in Azure China, Azure Germany, or Azure Government clouds yet.</span></span>
* <span data-ttu-id="3750f-118">This change impacts the following data types:</span><span class="sxs-lookup"><span data-stu-id="3750f-118">This change impacts the following data types:</span></span>
  * <span data-ttu-id="3750f-119">[Azure resource diagnostic logs](./monitoring-archive-diagnostic-logs.md) ([see list of resources here](./monitoring-diagnostic-logs-schema.md))</span><span class="sxs-lookup"><span data-stu-id="3750f-119">[Azure resource diagnostic logs](./monitoring-archive-diagnostic-logs.md) ([see list of resources here](./monitoring-diagnostic-logs-schema.md))</span></span>
  * [<span data-ttu-id="3750f-120">Azure resource metrics being exported by diagnostic settings</span><span class="sxs-lookup"><span data-stu-id="3750f-120">Azure resource metrics being exported by diagnostic settings</span></span>](./monitoring-overview-of-diagnostic-logs.md#diagnostic-settings)
  * [<span data-ttu-id="3750f-121">Azure Activity log data being exported by log profiles</span><span class="sxs-lookup"><span data-stu-id="3750f-121">Azure Activity log data being exported by log profiles</span></span>](./monitoring-archive-activity-log.md)
* <span data-ttu-id="3750f-122">This change does not impact:</span><span class="sxs-lookup"><span data-stu-id="3750f-122">This change does not impact:</span></span>
  * <span data-ttu-id="3750f-123">Network flow logs</span><span class="sxs-lookup"><span data-stu-id="3750f-123">Network flow logs</span></span>
  * <span data-ttu-id="3750f-124">Azure service logs not made available through Azure Monitor yet (for example, Azure App Service diagnostic logs, storage analytics logs)</span><span class="sxs-lookup"><span data-stu-id="3750f-124">Azure service logs not made available through Azure Monitor yet (for example, Azure App Service diagnostic logs, storage analytics logs)</span></span>
  * <span data-ttu-id="3750f-125">Routing of Azure diagnostic logs and activity logs to other destinations (Event Hubs, Log Analytics)</span><span class="sxs-lookup"><span data-stu-id="3750f-125">Routing of Azure diagnostic logs and activity logs to other destinations (Event Hubs, Log Analytics)</span></span>

### <a name="how-to-see-if-you-are-impacted"></a><span data-ttu-id="3750f-126">How to see if you are impacted</span><span class="sxs-lookup"><span data-stu-id="3750f-126">How to see if you are impacted</span></span>

<span data-ttu-id="3750f-127">You are only impacted by this change if you:</span><span class="sxs-lookup"><span data-stu-id="3750f-127">You are only impacted by this change if you:</span></span>
1. <span data-ttu-id="3750f-128">Are sending log data to an Azure storage account using a resource diagnostic setting, and</span><span class="sxs-lookup"><span data-stu-id="3750f-128">Are sending log data to an Azure storage account using a resource diagnostic setting, and</span></span>
2. <span data-ttu-id="3750f-129">Have tooling that depends on the JSON structure of these logs in storage.</span><span class="sxs-lookup"><span data-stu-id="3750f-129">Have tooling that depends on the JSON structure of these logs in storage.</span></span>
 
<span data-ttu-id="3750f-130">To identify if you have resource diagnostic settings that are sending data to an Azure storage account, you can navigate to the **Monitor** section of the portal, click on **Diagnostic Settings**, and identify any resources that have **Diagnostic Status** set to **Enabled**:</span><span class="sxs-lookup"><span data-stu-id="3750f-130">To identify if you have resource diagnostic settings that are sending data to an Azure storage account, you can navigate to the **Monitor** section of the portal, click on **Diagnostic Settings**, and identify any resources that have **Diagnostic Status** set to **Enabled**:</span></span>

![Azure Monitor Diagnostic Settings blade](./media/monitor-diagnostic-logs-append-blobs\portal-diag-settings.png)

<span data-ttu-id="3750f-132">If Diagnostic Status is set to enabled, you have an active diagnostic setting on that resource.</span><span class="sxs-lookup"><span data-stu-id="3750f-132">If Diagnostic Status is set to enabled, you have an active diagnostic setting on that resource.</span></span> <span data-ttu-id="3750f-133">Click on the resource to see if any diagnostic settings are sending data to a storage account:</span><span class="sxs-lookup"><span data-stu-id="3750f-133">Click on the resource to see if any diagnostic settings are sending data to a storage account:</span></span>

![Storage account enabled](./media/monitor-diagnostic-logs-append-blobs\portal-storage-enabled.png)

<span data-ttu-id="3750f-135">If you do have resources sending data to a storage account using these resource diagnostic settings, the format of the data in that storage account will be impacted by this change.</span><span class="sxs-lookup"><span data-stu-id="3750f-135">If you do have resources sending data to a storage account using these resource diagnostic settings, the format of the data in that storage account will be impacted by this change.</span></span> <span data-ttu-id="3750f-136">Unless you have custom tooling that operates off of these storage accounts, the format change will not impact you.</span><span class="sxs-lookup"><span data-stu-id="3750f-136">Unless you have custom tooling that operates off of these storage accounts, the format change will not impact you.</span></span>

### <a name="details-of-the-format-change"></a><span data-ttu-id="3750f-137">Details of the format change</span><span class="sxs-lookup"><span data-stu-id="3750f-137">Details of the format change</span></span>

<span data-ttu-id="3750f-138">The current format of the PT1H.json file in Azure blob storage uses a JSON array of records.</span><span class="sxs-lookup"><span data-stu-id="3750f-138">The current format of the PT1H.json file in Azure blob storage uses a JSON array of records.</span></span> <span data-ttu-id="3750f-139">Here is a sample of a KeyVault log file now:</span><span class="sxs-lookup"><span data-stu-id="3750f-139">Here is a sample of a KeyVault log file now:</span></span>

```json
{
    "records": [
        {
            "time": "2016-01-05T01:32:01.2691226Z",
            "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
            "operationName": "VaultGet",
            "operationVersion": "2015-06-01",
            "category": "AuditEvent",
            "resultType": "Success",
            "resultSignature": "OK",
            "resultDescription": "",
            "durationMs": "78",
            "callerIpAddress": "104.40.82.76",
            "correlationId": "",
            "identity": {
                "claim": {
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "d9da5048-2737-4770-bd64-XXXXXXXXXXXX",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "live.com#username@outlook.com",
                    "appid": "1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"
                }
            },
            "properties": {
                "clientInfo": "azure-resource-manager/2.0",
                "requestUri": "https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01",
                "id": "https://contosokeyvault.vault.azure.net/",
                "httpStatusCode": 200
            }
        },
        {
            "time": "2016-01-05T01:33:56.5264523Z",
            "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
            "operationName": "VaultGet",
            "operationVersion": "2015-06-01",
            "category": "AuditEvent",
            "resultType": "Success",
            "resultSignature": "OK",
            "resultDescription": "",
            "durationMs": "83",
            "callerIpAddress": "104.40.82.76",
            "correlationId": "",
            "identity": {
                "claim": {
                    "http://schemas.microsoft.com/identity/claims/objectidentifier": "d9da5048-2737-4770-bd64-XXXXXXXXXXXX",
                    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "live.com#username@outlook.com",
                    "appid": "1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"
                }
            },
            "properties": {
                "clientInfo": "azure-resource-manager/2.0",
                "requestUri": "https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01",
                "id": "https://contosokeyvault.vault.azure.net/",
                "httpStatusCode": 200
            }
        }
    ]
}
```

<span data-ttu-id="3750f-140">The new format uses [JSON lines](http://jsonlines.org/), where each event is a line and the newline character indicates a new event.</span><span class="sxs-lookup"><span data-stu-id="3750f-140">The new format uses [JSON lines](http://jsonlines.org/), where each event is a line and the newline character indicates a new event.</span></span> <span data-ttu-id="3750f-141">Here is what the above sample will look like in the PT1H.json file after the change:</span><span class="sxs-lookup"><span data-stu-id="3750f-141">Here is what the above sample will look like in the PT1H.json file after the change:</span></span>

```json
{"time": "2016-01-05T01:32:01.2691226Z","resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT","operationName": "VaultGet","operationVersion": "2015-06-01","category": "AuditEvent","resultType": "Success","resultSignature": "OK","resultDescription": "","durationMs": "78","callerIpAddress": "104.40.82.76","correlationId": "","identity": {"claim": {"http://schemas.microsoft.com/identity/claims/objectidentifier": "d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "live.com#username@outlook.com","appid": "1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},"properties": {"clientInfo": "azure-resource-manager/2.0","requestUri": "https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id": "https://contosokeyvault.vault.azure.net/","httpStatusCode": 200}}
{"time": "2016-01-05T01:33:56.5264523Z","resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT","operationName": "VaultGet","operationVersion": "2015-06-01","category": "AuditEvent","resultType": "Success","resultSignature": "OK","resultDescription": "","durationMs": "83","callerIpAddress": "104.40.82.76","correlationId": "","identity": {"claim": {"http://schemas.microsoft.com/identity/claims/objectidentifier": "d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "live.com#username@outlook.com","appid": "1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},"properties": {"clientInfo": "azure-resource-manager/2.0","requestUri": "https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id": "https://contosokeyvault.vault.azure.net/","httpStatusCode": 200}}
```

<span data-ttu-id="3750f-142">This new format enables Azure Monitor to push log files using [append blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs#about-append-blobs), which are more efficient for continuously appending new event data.</span><span class="sxs-lookup"><span data-stu-id="3750f-142">This new format enables Azure Monitor to push log files using [append blobs](https://docs.microsoft.com/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs#about-append-blobs), which are more efficient for continuously appending new event data.</span></span>

## <a name="how-to-update"></a><span data-ttu-id="3750f-143">How to update</span><span class="sxs-lookup"><span data-stu-id="3750f-143">How to update</span></span>

<span data-ttu-id="3750f-144">You only need to make updates if you have custom tooling that ingests these log files for further processing.</span><span class="sxs-lookup"><span data-stu-id="3750f-144">You only need to make updates if you have custom tooling that ingests these log files for further processing.</span></span> <span data-ttu-id="3750f-145">If you are making use of an external log analytics or SIEM tool, we recommend [using event hubs to ingest this data instead](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/).</span><span class="sxs-lookup"><span data-stu-id="3750f-145">If you are making use of an external log analytics or SIEM tool, we recommend [using event hubs to ingest this data instead](https://azure.microsoft.com/blog/use-azure-monitor-to-integrate-with-siem-tools/).</span></span> <span data-ttu-id="3750f-146">Event hubs integration is easier in terms of processing logs from many services and bookmarking location in a particular log.</span><span class="sxs-lookup"><span data-stu-id="3750f-146">Event hubs integration is easier in terms of processing logs from many services and bookmarking location in a particular log.</span></span>

<span data-ttu-id="3750f-147">Custom tools should be updated to handle both the current format and the JSON Lines format described above.</span><span class="sxs-lookup"><span data-stu-id="3750f-147">Custom tools should be updated to handle both the current format and the JSON Lines format described above.</span></span> <span data-ttu-id="3750f-148">This will ensure that when data starts to appear in the new format, your tools do not break.</span><span class="sxs-lookup"><span data-stu-id="3750f-148">This will ensure that when data starts to appear in the new format, your tools do not break.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3750f-149">Next steps</span><span class="sxs-lookup"><span data-stu-id="3750f-149">Next steps</span></span>

* <span data-ttu-id="3750f-150">Learn about [archiving resource diagnostic logs to a storage account](./monitoring-archive-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="3750f-150">Learn about [archiving resource diagnostic logs to a storage account](./monitoring-archive-diagnostic-logs.md)</span></span>
* <span data-ttu-id="3750f-151">Learn about [archiving activity log data to a storage account](./monitoring-archive-activity-log.md)</span><span class="sxs-lookup"><span data-stu-id="3750f-151">Learn about [archiving activity log data to a storage account](./monitoring-archive-activity-log.md)</span></span>
