---
title: Azure Key Vault solution in Log Analytics | Microsoft Docs
description: You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault logs.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: jochan
editor: ''
ms.assetid: 5e25e6d6-dd20-4528-9820-6e2958a40dae
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 1366abee48c84e6fad3e647e86497648927f4ced
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553571"
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="20aee-103">Azure Key Vault Analytics solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="20aee-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

<span data-ttu-id="20aee-104">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span><span class="sxs-lookup"><span data-stu-id="20aee-104">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="20aee-105">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="20aee-105">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="20aee-106">It is not necessary to write the logs to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="20aee-106">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="20aee-107">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="20aee-107">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="20aee-108">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span><span class="sxs-lookup"><span data-stu-id="20aee-108">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="20aee-109">Install and configure the solution</span><span class="sxs-lookup"><span data-stu-id="20aee-109">Install and configure the solution</span></span>
<span data-ttu-id="20aee-110">Use the following instructions to install and configure the Azure Key Vault solution:</span><span class="sxs-lookup"><span data-stu-id="20aee-110">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="20aee-111">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="20aee-111">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> 
2. <span data-ttu-id="20aee-112">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="20aee-112">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span> 

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="20aee-113">Enable Key Vault diagnostics in the portal</span><span class="sxs-lookup"><span data-stu-id="20aee-113">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="20aee-114">In the Azure portal, navigate to the Key Vault resource to monitor</span><span class="sxs-lookup"><span data-stu-id="20aee-114">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="20aee-115">Select *Diagnostics logs* to open the following page</span><span class="sxs-lookup"><span data-stu-id="20aee-115">Select *Diagnostics logs* to open the following page</span></span>

   ![image of Azure Key Vault tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="20aee-117">Click *Turn on diagnostics* to open the following page</span><span class="sxs-lookup"><span data-stu-id="20aee-117">Click *Turn on diagnostics* to open the following page</span></span>

   ![image of Azure Key Vault tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="20aee-119">To turn on diagnostics, click *On* under *Status*</span><span class="sxs-lookup"><span data-stu-id="20aee-119">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="20aee-120">Click the checkbox for *Send to Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="20aee-120">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="20aee-121">Select an existing Log Analytics workspace, or create a workspace</span><span class="sxs-lookup"><span data-stu-id="20aee-121">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="20aee-122">To enable *AuditEvent* logs, click the checkbox under Log</span><span class="sxs-lookup"><span data-stu-id="20aee-122">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="20aee-123">Click *Save* to enable the logging of diagnostics to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="20aee-123">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="20aee-124">Enable Key Vault diagnostics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="20aee-124">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="20aee-125">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span><span class="sxs-lookup"><span data-stu-id="20aee-125">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```
 
 

## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="20aee-126">Review Azure Key Vault data collection details</span><span class="sxs-lookup"><span data-stu-id="20aee-126">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="20aee-127">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="20aee-127">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="20aee-128">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span><span class="sxs-lookup"><span data-stu-id="20aee-128">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="20aee-129">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="20aee-129">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="20aee-130">Platform</span><span class="sxs-lookup"><span data-stu-id="20aee-130">Platform</span></span> | <span data-ttu-id="20aee-131">Direct agent</span><span class="sxs-lookup"><span data-stu-id="20aee-131">Direct agent</span></span> | <span data-ttu-id="20aee-132">Systems Center Operations Manager agent</span><span class="sxs-lookup"><span data-stu-id="20aee-132">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="20aee-133">Azure</span><span class="sxs-lookup"><span data-stu-id="20aee-133">Azure</span></span> | <span data-ttu-id="20aee-134">Operations Manager required?</span><span class="sxs-lookup"><span data-stu-id="20aee-134">Operations Manager required?</span></span> | <span data-ttu-id="20aee-135">Operations Manager agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="20aee-135">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="20aee-136">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="20aee-136">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="20aee-137">Azure</span><span class="sxs-lookup"><span data-stu-id="20aee-137">Azure</span></span> |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/oms-bullet-red.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/oms-bullet-red.png) | <span data-ttu-id="20aee-143">on arrival</span><span class="sxs-lookup"><span data-stu-id="20aee-143">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="20aee-144">Use Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="20aee-144">Use Azure Key Vault</span></span>
<span data-ttu-id="20aee-145">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="20aee-145">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![image of Azure Key Vault tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="20aee-147">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span><span class="sxs-lookup"><span data-stu-id="20aee-147">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="20aee-148">Volume of all key vault operations over time</span><span class="sxs-lookup"><span data-stu-id="20aee-148">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="20aee-149">Failed operation volumes over time</span><span class="sxs-lookup"><span data-stu-id="20aee-149">Failed operation volumes over time</span></span>
* <span data-ttu-id="20aee-150">Average operational latency by operation</span><span class="sxs-lookup"><span data-stu-id="20aee-150">Average operational latency by operation</span></span>
* <span data-ttu-id="20aee-151">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span><span class="sxs-lookup"><span data-stu-id="20aee-151">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![image of Azure Key Vault dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![image of Azure Key Vault dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="20aee-154">To view details for any operation</span><span class="sxs-lookup"><span data-stu-id="20aee-154">To view details for any operation</span></span>
1. <span data-ttu-id="20aee-155">On the **Overview** page, click the **Azure Key Vault** tile.</span><span class="sxs-lookup"><span data-stu-id="20aee-155">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="20aee-156">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span><span class="sxs-lookup"><span data-stu-id="20aee-156">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>
   
    <span data-ttu-id="20aee-157">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span><span class="sxs-lookup"><span data-stu-id="20aee-157">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="20aee-158">You can also filter by facets to narrow the results.</span><span class="sxs-lookup"><span data-stu-id="20aee-158">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="20aee-159">Log Analytics records</span><span class="sxs-lookup"><span data-stu-id="20aee-159">Log Analytics records</span></span>
<span data-ttu-id="20aee-160">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="20aee-160">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="20aee-161">Properties for these records are in the following table:</span><span class="sxs-lookup"><span data-stu-id="20aee-161">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="20aee-162">Property</span><span class="sxs-lookup"><span data-stu-id="20aee-162">Property</span></span> | <span data-ttu-id="20aee-163">Description</span><span class="sxs-lookup"><span data-stu-id="20aee-163">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="20aee-164">Type</span><span class="sxs-lookup"><span data-stu-id="20aee-164">Type</span></span> |<span data-ttu-id="20aee-165">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="20aee-165">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="20aee-166">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="20aee-166">SourceSystem</span></span> |<span data-ttu-id="20aee-167">*Azure*</span><span class="sxs-lookup"><span data-stu-id="20aee-167">*Azure*</span></span> |
| <span data-ttu-id="20aee-168">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="20aee-168">CallerIpAddress</span></span> |<span data-ttu-id="20aee-169">IP address of the client who made the request</span><span class="sxs-lookup"><span data-stu-id="20aee-169">IP address of the client who made the request</span></span> |
| <span data-ttu-id="20aee-170">Category</span><span class="sxs-lookup"><span data-stu-id="20aee-170">Category</span></span> | <span data-ttu-id="20aee-171">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="20aee-171">*AuditEvent*</span></span> |
| <span data-ttu-id="20aee-172">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="20aee-172">CorrelationId</span></span> |<span data-ttu-id="20aee-173">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span><span class="sxs-lookup"><span data-stu-id="20aee-173">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="20aee-174">DurationMs</span><span class="sxs-lookup"><span data-stu-id="20aee-174">DurationMs</span></span> |<span data-ttu-id="20aee-175">Time it took to service the REST API request, in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="20aee-175">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="20aee-176">This time does not include network latency, so the time that you measure on the client side might not match this time.</span><span class="sxs-lookup"><span data-stu-id="20aee-176">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="20aee-177">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="20aee-177">httpStatusCode_d</span></span> |<span data-ttu-id="20aee-178">HTTP status code returned by the request (for example, *200*)</span><span class="sxs-lookup"><span data-stu-id="20aee-178">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="20aee-179">id_s</span><span class="sxs-lookup"><span data-stu-id="20aee-179">id_s</span></span> |<span data-ttu-id="20aee-180">Unique ID of the request</span><span class="sxs-lookup"><span data-stu-id="20aee-180">Unique ID of the request</span></span> |
| <span data-ttu-id="20aee-181">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="20aee-181">identity_claim_appid_g</span></span> | <span data-ttu-id="20aee-182">GUID for the application id</span><span class="sxs-lookup"><span data-stu-id="20aee-182">GUID for the application id</span></span> |
| <span data-ttu-id="20aee-183">OperationName</span><span class="sxs-lookup"><span data-stu-id="20aee-183">OperationName</span></span> |<span data-ttu-id="20aee-184">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="20aee-184">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="20aee-185">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="20aee-185">OperationVersion</span></span> |<span data-ttu-id="20aee-186">REST API version requested by the client (for example *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="20aee-186">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="20aee-187">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="20aee-187">requestUri_s</span></span> |<span data-ttu-id="20aee-188">Uri of the request</span><span class="sxs-lookup"><span data-stu-id="20aee-188">Uri of the request</span></span> |
| <span data-ttu-id="20aee-189">Resource</span><span class="sxs-lookup"><span data-stu-id="20aee-189">Resource</span></span> |<span data-ttu-id="20aee-190">Name of the key vault</span><span class="sxs-lookup"><span data-stu-id="20aee-190">Name of the key vault</span></span> |
| <span data-ttu-id="20aee-191">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="20aee-191">ResourceGroup</span></span> |<span data-ttu-id="20aee-192">Resource group of the key vault</span><span class="sxs-lookup"><span data-stu-id="20aee-192">Resource group of the key vault</span></span> |
| <span data-ttu-id="20aee-193">ResourceId</span><span class="sxs-lookup"><span data-stu-id="20aee-193">ResourceId</span></span> |<span data-ttu-id="20aee-194">Azure Resource Manager Resource ID.</span><span class="sxs-lookup"><span data-stu-id="20aee-194">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="20aee-195">For Key Vault logs, this is the Key Vault resource ID.</span><span class="sxs-lookup"><span data-stu-id="20aee-195">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="20aee-196">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="20aee-196">ResourceProvider</span></span> |<span data-ttu-id="20aee-197">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="20aee-197">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="20aee-198">ResourceType</span><span class="sxs-lookup"><span data-stu-id="20aee-198">ResourceType</span></span> | <span data-ttu-id="20aee-199">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="20aee-199">*VAULTS*</span></span> |
| <span data-ttu-id="20aee-200">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="20aee-200">ResultSignature</span></span> |<span data-ttu-id="20aee-201">HTTP status (for example, *OK*)</span><span class="sxs-lookup"><span data-stu-id="20aee-201">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="20aee-202">ResultType</span><span class="sxs-lookup"><span data-stu-id="20aee-202">ResultType</span></span> |<span data-ttu-id="20aee-203">Result of REST API request (for example, *Success*)</span><span class="sxs-lookup"><span data-stu-id="20aee-203">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="20aee-204">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="20aee-204">SubscriptionId</span></span> |<span data-ttu-id="20aee-205">Azure subscription ID of the subscription containing the Key Vault</span><span class="sxs-lookup"><span data-stu-id="20aee-205">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="20aee-206">Migrating from the old Key Vault solution</span><span class="sxs-lookup"><span data-stu-id="20aee-206">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="20aee-207">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="20aee-207">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="20aee-208">These changes provide the following advantages:</span><span class="sxs-lookup"><span data-stu-id="20aee-208">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="20aee-209">Logs are written directly to Log Analytics without the need to use a storage account</span><span class="sxs-lookup"><span data-stu-id="20aee-209">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="20aee-210">Less latency from the time when logs are generated to them being available in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="20aee-210">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="20aee-211">Fewer configuration steps</span><span class="sxs-lookup"><span data-stu-id="20aee-211">Fewer configuration steps</span></span>
+ <span data-ttu-id="20aee-212">A common format for all types of Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="20aee-212">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="20aee-213">To use the updated solution:</span><span class="sxs-lookup"><span data-stu-id="20aee-213">To use the updated solution:</span></span>

1. [<span data-ttu-id="20aee-214">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span><span class="sxs-lookup"><span data-stu-id="20aee-214">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="20aee-215">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="20aee-215">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="20aee-216">Update any saved queries, dashboards, or alerts to use the new data type</span><span class="sxs-lookup"><span data-stu-id="20aee-216">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="20aee-217">Type is change from: KeyVaults to AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="20aee-217">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="20aee-218">You can use the ResourceType to filter to Key Vault Logs.</span><span class="sxs-lookup"><span data-stu-id="20aee-218">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="20aee-219">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span><span class="sxs-lookup"><span data-stu-id="20aee-219">Instead of: `Type=KeyVaults`, use `Type=AzureDiagnostics ResourceType=VAULTS`</span></span>
  + <span data-ttu-id="20aee-220">Fields: (Field names are case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="20aee-220">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="20aee-221">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span><span class="sxs-lookup"><span data-stu-id="20aee-221">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="20aee-222">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span><span class="sxs-lookup"><span data-stu-id="20aee-222">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="20aee-223">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="20aee-223">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="20aee-224">Field CallerIpAddress changed to CallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="20aee-224">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="20aee-225">Field RemoteIPCountry is no longer present</span><span class="sxs-lookup"><span data-stu-id="20aee-225">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="20aee-226">Remove the *Key Vault Analytics (Deprecated)* solution.</span><span class="sxs-lookup"><span data-stu-id="20aee-226">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="20aee-227">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="20aee-227">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span> 

<span data-ttu-id="20aee-228">Data collected before the change is not visible in the new solution.</span><span class="sxs-lookup"><span data-stu-id="20aee-228">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="20aee-229">You can continue to query for this data using the old Type and field names.</span><span class="sxs-lookup"><span data-stu-id="20aee-229">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="20aee-230">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="20aee-230">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="20aee-231">Next steps</span><span class="sxs-lookup"><span data-stu-id="20aee-231">Next steps</span></span>
* <span data-ttu-id="20aee-232">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span><span class="sxs-lookup"><span data-stu-id="20aee-232">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>











