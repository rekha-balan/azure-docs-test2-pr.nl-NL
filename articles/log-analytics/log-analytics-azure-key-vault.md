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
ms.topic: conceptual
ms.date: 02/09/2017
ms.author: richrund
ms.component: na
ms.openlocfilehash: ee78ea4b52e2ab372bdb8fef2c884f2e4e989fdb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791549"
---
# <a name="azure-key-vault-analytics-solution-in-log-analytics"></a><span data-ttu-id="51774-103">Azure Key Vault Analytics solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="51774-103">Azure Key Vault Analytics solution in Log Analytics</span></span>

![Key Vault symbol](./media/log-analytics-azure-keyvault/key-vault-analytics-symbol.png)

<span data-ttu-id="51774-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span><span class="sxs-lookup"><span data-stu-id="51774-105">You can use the Azure Key Vault solution in Log Analytics to review Azure Key Vault AuditEvent logs.</span></span>

<span data-ttu-id="51774-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="51774-106">To use the solution, you need to enable logging of Azure Key Vault diagnostics and direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="51774-107">It is not necessary to write the logs to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="51774-107">It is not necessary to write the logs to Azure Blob storage.</span></span>

> [!NOTE]
> <span data-ttu-id="51774-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="51774-108">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="51774-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span><span class="sxs-lookup"><span data-stu-id="51774-109">If the Key Vault solution you are using shows *(deprecated)* in the title, refer to [migrating from the old Key Vault solution](#migrating-from-the-old-key-vault-solution) for steps you need to follow.</span></span>
>
>

## <a name="install-and-configure-the-solution"></a><span data-ttu-id="51774-110">Install and configure the solution</span><span class="sxs-lookup"><span data-stu-id="51774-110">Install and configure the solution</span></span>
<span data-ttu-id="51774-111">Use the following instructions to install and configure the Azure Key Vault solution:</span><span class="sxs-lookup"><span data-stu-id="51774-111">Use the following instructions to install and configure the Azure Key Vault solution:</span></span>

1. <span data-ttu-id="51774-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="51774-112">Enable the Azure Key Vault solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="51774-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span><span class="sxs-lookup"><span data-stu-id="51774-113">Enable diagnostics logging for the Key Vault resources to monitor, using either the [portal](#enable-key-vault-diagnostics-in-the-portal) or [PowerShell](#enable-key-vault-diagnostics-using-powershell)</span></span>

### <a name="enable-key-vault-diagnostics-in-the-portal"></a><span data-ttu-id="51774-114">Enable Key Vault diagnostics in the portal</span><span class="sxs-lookup"><span data-stu-id="51774-114">Enable Key Vault diagnostics in the portal</span></span>

1. <span data-ttu-id="51774-115">In the Azure portal, navigate to the Key Vault resource to monitor</span><span class="sxs-lookup"><span data-stu-id="51774-115">In the Azure portal, navigate to the Key Vault resource to monitor</span></span>
2. <span data-ttu-id="51774-116">Select *Diagnostics logs* to open the following page</span><span class="sxs-lookup"><span data-stu-id="51774-116">Select *Diagnostics logs* to open the following page</span></span>

   ![image of Azure Key Vault tile](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics01.png)
3. <span data-ttu-id="51774-118">Click *Turn on diagnostics* to open the following page</span><span class="sxs-lookup"><span data-stu-id="51774-118">Click *Turn on diagnostics* to open the following page</span></span>

   ![image of Azure Key Vault tile](./media/log-analytics-azure-keyvault/log-analytics-keyvault-enable-diagnostics02.png)
4. <span data-ttu-id="51774-120">To turn on diagnostics, click *On* under *Status*</span><span class="sxs-lookup"><span data-stu-id="51774-120">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="51774-121">Click the checkbox for *Send to Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="51774-121">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="51774-122">Select an existing Log Analytics workspace, or create a workspace</span><span class="sxs-lookup"><span data-stu-id="51774-122">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="51774-123">To enable *AuditEvent* logs, click the checkbox under Log</span><span class="sxs-lookup"><span data-stu-id="51774-123">To enable *AuditEvent* logs, click the checkbox under Log</span></span>
8. <span data-ttu-id="51774-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="51774-124">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-key-vault-diagnostics-using-powershell"></a><span data-ttu-id="51774-125">Enable Key Vault diagnostics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="51774-125">Enable Key Vault diagnostics using PowerShell</span></span>
<span data-ttu-id="51774-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span><span class="sxs-lookup"><span data-stu-id="51774-126">The following PowerShell script provides an example of how to use `Set-AzureRmDiagnosticSetting` to enable diagnostic logging for Key Vault:</span></span>
```
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'

Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```



## <a name="review-azure-key-vault-data-collection-details"></a><span data-ttu-id="51774-127">Review Azure Key Vault data collection details</span><span class="sxs-lookup"><span data-stu-id="51774-127">Review Azure Key Vault data collection details</span></span>
<span data-ttu-id="51774-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span><span class="sxs-lookup"><span data-stu-id="51774-128">Azure Key Vault solution collects diagnostics logs directly from the Key Vault.</span></span>
<span data-ttu-id="51774-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span><span class="sxs-lookup"><span data-stu-id="51774-129">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="51774-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="51774-130">The following table shows data collection methods and other details about how data is collected for Azure Key Vault.</span></span>

| <span data-ttu-id="51774-131">Platform</span><span class="sxs-lookup"><span data-stu-id="51774-131">Platform</span></span> | <span data-ttu-id="51774-132">Direct agent</span><span class="sxs-lookup"><span data-stu-id="51774-132">Direct agent</span></span> | <span data-ttu-id="51774-133">Systems Center Operations Manager agent</span><span class="sxs-lookup"><span data-stu-id="51774-133">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="51774-134">Azure</span><span class="sxs-lookup"><span data-stu-id="51774-134">Azure</span></span> | <span data-ttu-id="51774-135">Operations Manager required?</span><span class="sxs-lookup"><span data-stu-id="51774-135">Operations Manager required?</span></span> | <span data-ttu-id="51774-136">Operations Manager agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="51774-136">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="51774-137">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="51774-137">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="51774-138">Azure</span><span class="sxs-lookup"><span data-stu-id="51774-138">Azure</span></span> |  |  |<span data-ttu-id="51774-139">&#8226;</span><span class="sxs-lookup"><span data-stu-id="51774-139">&#8226;</span></span> |  |  | <span data-ttu-id="51774-140">on arrival</span><span class="sxs-lookup"><span data-stu-id="51774-140">on arrival</span></span> |

## <a name="use-azure-key-vault"></a><span data-ttu-id="51774-141">Use Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="51774-141">Use Azure Key Vault</span></span>
<span data-ttu-id="51774-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="51774-142">After you [install the solution](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.KeyVaultAnalyticsOMS?tab=Overview), view the Key Vault data by clicking the **Azure Key Vault** tile from the **Overview** page of Log Analytics.</span></span>

![image of Azure Key Vault tile](./media/log-analytics-azure-keyvault/log-analytics-keyvault-tile.png)

<span data-ttu-id="51774-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span><span class="sxs-lookup"><span data-stu-id="51774-144">After you click the **Overview** tile, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="51774-145">Volume of all key vault operations over time</span><span class="sxs-lookup"><span data-stu-id="51774-145">Volume of all key vault operations over time</span></span>
* <span data-ttu-id="51774-146">Failed operation volumes over time</span><span class="sxs-lookup"><span data-stu-id="51774-146">Failed operation volumes over time</span></span>
* <span data-ttu-id="51774-147">Average operational latency by operation</span><span class="sxs-lookup"><span data-stu-id="51774-147">Average operational latency by operation</span></span>
* <span data-ttu-id="51774-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span><span class="sxs-lookup"><span data-stu-id="51774-148">Quality of service for operations with the number of operations that take more than 1000 ms and a list of operations that take more than 1000 ms</span></span>

![image of Azure Key Vault dashboard](./media/log-analytics-azure-keyvault/log-analytics-keyvault01.png)

![image of Azure Key Vault dashboard](./media/log-analytics-azure-keyvault/log-analytics-keyvault02.png)

### <a name="to-view-details-for-any-operation"></a><span data-ttu-id="51774-151">To view details for any operation</span><span class="sxs-lookup"><span data-stu-id="51774-151">To view details for any operation</span></span>
1. <span data-ttu-id="51774-152">On the **Overview** page, click the **Azure Key Vault** tile.</span><span class="sxs-lookup"><span data-stu-id="51774-152">On the **Overview** page, click the **Azure Key Vault** tile.</span></span>
2. <span data-ttu-id="51774-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span><span class="sxs-lookup"><span data-stu-id="51774-153">On the **Azure Key Vault** dashboard, review the summary information in one of the blades, and then click one to view detailed information about it in the log search page.</span></span>

    <span data-ttu-id="51774-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span><span class="sxs-lookup"><span data-stu-id="51774-154">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="51774-155">You can also filter by facets to narrow the results.</span><span class="sxs-lookup"><span data-stu-id="51774-155">You can also filter by facets to narrow the results.</span></span>

## <a name="log-analytics-records"></a><span data-ttu-id="51774-156">Log Analytics records</span><span class="sxs-lookup"><span data-stu-id="51774-156">Log Analytics records</span></span>
<span data-ttu-id="51774-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="51774-157">The Azure Key Vault solution analyzes records that have a type of **KeyVaults** that are collected from [AuditEvent logs](../key-vault/key-vault-logging.md) in Azure Diagnostics.</span></span>  <span data-ttu-id="51774-158">Properties for these records are in the following table:</span><span class="sxs-lookup"><span data-stu-id="51774-158">Properties for these records are in the following table:</span></span>  

| <span data-ttu-id="51774-159">Property</span><span class="sxs-lookup"><span data-stu-id="51774-159">Property</span></span> | <span data-ttu-id="51774-160">Description</span><span class="sxs-lookup"><span data-stu-id="51774-160">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="51774-161">Type</span><span class="sxs-lookup"><span data-stu-id="51774-161">Type</span></span> |<span data-ttu-id="51774-162">*AzureDiagnostics*</span><span class="sxs-lookup"><span data-stu-id="51774-162">*AzureDiagnostics*</span></span> |
| <span data-ttu-id="51774-163">SourceSystem</span><span class="sxs-lookup"><span data-stu-id="51774-163">SourceSystem</span></span> |<span data-ttu-id="51774-164">*Azure*</span><span class="sxs-lookup"><span data-stu-id="51774-164">*Azure*</span></span> |
| <span data-ttu-id="51774-165">CallerIpAddress</span><span class="sxs-lookup"><span data-stu-id="51774-165">CallerIpAddress</span></span> |<span data-ttu-id="51774-166">IP address of the client who made the request</span><span class="sxs-lookup"><span data-stu-id="51774-166">IP address of the client who made the request</span></span> |
| <span data-ttu-id="51774-167">Category</span><span class="sxs-lookup"><span data-stu-id="51774-167">Category</span></span> | <span data-ttu-id="51774-168">*AuditEvent*</span><span class="sxs-lookup"><span data-stu-id="51774-168">*AuditEvent*</span></span> |
| <span data-ttu-id="51774-169">CorrelationId</span><span class="sxs-lookup"><span data-stu-id="51774-169">CorrelationId</span></span> |<span data-ttu-id="51774-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span><span class="sxs-lookup"><span data-stu-id="51774-170">An optional GUID that the client can pass to correlate client-side logs with service-side (Key Vault) logs.</span></span> |
| <span data-ttu-id="51774-171">DurationMs</span><span class="sxs-lookup"><span data-stu-id="51774-171">DurationMs</span></span> |<span data-ttu-id="51774-172">Time it took to service the REST API request, in milliseconds.</span><span class="sxs-lookup"><span data-stu-id="51774-172">Time it took to service the REST API request, in milliseconds.</span></span> <span data-ttu-id="51774-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span><span class="sxs-lookup"><span data-stu-id="51774-173">This time does not include network latency, so the time that you measure on the client side might not match this time.</span></span> |
| <span data-ttu-id="51774-174">httpStatusCode_d</span><span class="sxs-lookup"><span data-stu-id="51774-174">httpStatusCode_d</span></span> |<span data-ttu-id="51774-175">HTTP status code returned by the request (for example, *200*)</span><span class="sxs-lookup"><span data-stu-id="51774-175">HTTP status code returned by the request (for example, *200*)</span></span> |
| <span data-ttu-id="51774-176">id_s</span><span class="sxs-lookup"><span data-stu-id="51774-176">id_s</span></span> |<span data-ttu-id="51774-177">Unique ID of the request</span><span class="sxs-lookup"><span data-stu-id="51774-177">Unique ID of the request</span></span> |
| <span data-ttu-id="51774-178">identity_claim_appid_g</span><span class="sxs-lookup"><span data-stu-id="51774-178">identity_claim_appid_g</span></span> | <span data-ttu-id="51774-179">GUID for the application id</span><span class="sxs-lookup"><span data-stu-id="51774-179">GUID for the application id</span></span> |
| <span data-ttu-id="51774-180">OperationName</span><span class="sxs-lookup"><span data-stu-id="51774-180">OperationName</span></span> |<span data-ttu-id="51774-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span><span class="sxs-lookup"><span data-stu-id="51774-181">Name of the operation, as documented in [Azure Key Vault Logging](../key-vault/key-vault-logging.md)</span></span> |
| <span data-ttu-id="51774-182">OperationVersion</span><span class="sxs-lookup"><span data-stu-id="51774-182">OperationVersion</span></span> |<span data-ttu-id="51774-183">REST API version requested by the client (for example *2015-06-01*)</span><span class="sxs-lookup"><span data-stu-id="51774-183">REST API version requested by the client (for example *2015-06-01*)</span></span> |
| <span data-ttu-id="51774-184">requestUri_s</span><span class="sxs-lookup"><span data-stu-id="51774-184">requestUri_s</span></span> |<span data-ttu-id="51774-185">Uri of the request</span><span class="sxs-lookup"><span data-stu-id="51774-185">Uri of the request</span></span> |
| <span data-ttu-id="51774-186">Resource</span><span class="sxs-lookup"><span data-stu-id="51774-186">Resource</span></span> |<span data-ttu-id="51774-187">Name of the key vault</span><span class="sxs-lookup"><span data-stu-id="51774-187">Name of the key vault</span></span> |
| <span data-ttu-id="51774-188">ResourceGroup</span><span class="sxs-lookup"><span data-stu-id="51774-188">ResourceGroup</span></span> |<span data-ttu-id="51774-189">Resource group of the key vault</span><span class="sxs-lookup"><span data-stu-id="51774-189">Resource group of the key vault</span></span> |
| <span data-ttu-id="51774-190">ResourceId</span><span class="sxs-lookup"><span data-stu-id="51774-190">ResourceId</span></span> |<span data-ttu-id="51774-191">Azure Resource Manager Resource ID.</span><span class="sxs-lookup"><span data-stu-id="51774-191">Azure Resource Manager Resource ID.</span></span> <span data-ttu-id="51774-192">For Key Vault logs, this is the Key Vault resource ID.</span><span class="sxs-lookup"><span data-stu-id="51774-192">For Key Vault logs, this is the Key Vault resource ID.</span></span> |
| <span data-ttu-id="51774-193">ResourceProvider</span><span class="sxs-lookup"><span data-stu-id="51774-193">ResourceProvider</span></span> |<span data-ttu-id="51774-194">*MICROSOFT.KEYVAULT*</span><span class="sxs-lookup"><span data-stu-id="51774-194">*MICROSOFT.KEYVAULT*</span></span> |
| <span data-ttu-id="51774-195">ResourceType</span><span class="sxs-lookup"><span data-stu-id="51774-195">ResourceType</span></span> | <span data-ttu-id="51774-196">*VAULTS*</span><span class="sxs-lookup"><span data-stu-id="51774-196">*VAULTS*</span></span> |
| <span data-ttu-id="51774-197">ResultSignature</span><span class="sxs-lookup"><span data-stu-id="51774-197">ResultSignature</span></span> |<span data-ttu-id="51774-198">HTTP status (for example, *OK*)</span><span class="sxs-lookup"><span data-stu-id="51774-198">HTTP status (for example, *OK*)</span></span> |
| <span data-ttu-id="51774-199">ResultType</span><span class="sxs-lookup"><span data-stu-id="51774-199">ResultType</span></span> |<span data-ttu-id="51774-200">Result of REST API request (for example, *Success*)</span><span class="sxs-lookup"><span data-stu-id="51774-200">Result of REST API request (for example, *Success*)</span></span> |
| <span data-ttu-id="51774-201">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="51774-201">SubscriptionId</span></span> |<span data-ttu-id="51774-202">Azure subscription ID of the subscription containing the Key Vault</span><span class="sxs-lookup"><span data-stu-id="51774-202">Azure subscription ID of the subscription containing the Key Vault</span></span> |

## <a name="migrating-from-the-old-key-vault-solution"></a><span data-ttu-id="51774-203">Migrating from the old Key Vault solution</span><span class="sxs-lookup"><span data-stu-id="51774-203">Migrating from the old Key Vault solution</span></span>
<span data-ttu-id="51774-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="51774-204">In January 2017, the supported way of sending logs from Key Vault to Log Analytics changed.</span></span> <span data-ttu-id="51774-205">These changes provide the following advantages:</span><span class="sxs-lookup"><span data-stu-id="51774-205">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="51774-206">Logs are written directly to Log Analytics without the need to use a storage account</span><span class="sxs-lookup"><span data-stu-id="51774-206">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="51774-207">Less latency from the time when logs are generated to them being available in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="51774-207">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="51774-208">Fewer configuration steps</span><span class="sxs-lookup"><span data-stu-id="51774-208">Fewer configuration steps</span></span>
+ <span data-ttu-id="51774-209">A common format for all types of Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="51774-209">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="51774-210">To use the updated solution:</span><span class="sxs-lookup"><span data-stu-id="51774-210">To use the updated solution:</span></span>

1. [<span data-ttu-id="51774-211">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span><span class="sxs-lookup"><span data-stu-id="51774-211">Configure diagnostics to be sent directly to Log Analytics from Key Vault</span></span>](#enable-key-vault-diagnostics-in-the-portal)  
2. <span data-ttu-id="51774-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="51774-212">Enable the Azure Key Vault solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="51774-213">Update any saved queries, dashboards, or alerts to use the new data type</span><span class="sxs-lookup"><span data-stu-id="51774-213">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="51774-214">Type is change from: KeyVaults to AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="51774-214">Type is change from: KeyVaults to AzureDiagnostics.</span></span> <span data-ttu-id="51774-215">You can use the ResourceType to filter to Key Vault Logs.</span><span class="sxs-lookup"><span data-stu-id="51774-215">You can use the ResourceType to filter to Key Vault Logs.</span></span>
  - <span data-ttu-id="51774-216">Instead of: `KeyVaults`, use `AzureDiagnostics | where ResourceType'=="VAULTS"`</span><span class="sxs-lookup"><span data-stu-id="51774-216">Instead of: `KeyVaults`, use `AzureDiagnostics | where ResourceType'=="VAULTS"`</span></span>
  + <span data-ttu-id="51774-217">Fields: (Field names are case-sensitive)</span><span class="sxs-lookup"><span data-stu-id="51774-217">Fields: (Field names are case-sensitive)</span></span>
  - <span data-ttu-id="51774-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span><span class="sxs-lookup"><span data-stu-id="51774-218">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
  - <span data-ttu-id="51774-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span><span class="sxs-lookup"><span data-stu-id="51774-219">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span> <span data-ttu-id="51774-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span><span class="sxs-lookup"><span data-stu-id="51774-220">For example, the UPN of the caller is stored in a field `identity_claim_http_schemas_xmlsoap_org_ws_2005_05_identity_claims_upn_s`</span></span>
   - <span data-ttu-id="51774-221">Field CallerIpAddress changed to CallerIPAddress</span><span class="sxs-lookup"><span data-stu-id="51774-221">Field CallerIpAddress changed to CallerIPAddress</span></span>
   - <span data-ttu-id="51774-222">Field RemoteIPCountry is no longer present</span><span class="sxs-lookup"><span data-stu-id="51774-222">Field RemoteIPCountry is no longer present</span></span>
4. <span data-ttu-id="51774-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span><span class="sxs-lookup"><span data-stu-id="51774-223">Remove the *Key Vault Analytics (Deprecated)* solution.</span></span> <span data-ttu-id="51774-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="51774-224">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "KeyVault" -Enabled $false`</span></span>

<span data-ttu-id="51774-225">Data collected before the change is not visible in the new solution.</span><span class="sxs-lookup"><span data-stu-id="51774-225">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="51774-226">You can continue to query for this data using the old Type and field names.</span><span class="sxs-lookup"><span data-stu-id="51774-226">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="51774-227">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="51774-227">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="51774-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="51774-228">Next steps</span></span>
* <span data-ttu-id="51774-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span><span class="sxs-lookup"><span data-stu-id="51774-229">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure Key Vault data.</span></span>
