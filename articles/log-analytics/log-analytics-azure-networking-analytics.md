---
title: Azure Networking Analytics solution in Log Analytics | Microsoft Docs
description: You can use the Azure Networking Analytics solution in Log Analytics to review Azure network security group logs and Azure Application Gateway logs.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: ewinner
editor: ''
ms.assetid: 66a3b8a1-6c55-4533-9538-cad60c18f28b
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: richrund
ms.openlocfilehash: 0009911945ff14ae4c7ace49be3f9936147e445e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540691"
---
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a><span data-ttu-id="296fb-103">Azure networking monitoring solutions in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-103">Azure networking monitoring solutions in Log Analytics</span></span>

<span data-ttu-id="296fb-104">Log Analytics offers the following solutions for monitoring your networks:</span><span class="sxs-lookup"><span data-stu-id="296fb-104">Log Analytics offers the following solutions for monitoring your networks:</span></span>
* <span data-ttu-id="296fb-105">Network Performance Monitor (NPM) to</span><span class="sxs-lookup"><span data-stu-id="296fb-105">Network Performance Monitor (NPM) to</span></span>
 * <span data-ttu-id="296fb-106">Monitor the health of your network</span><span class="sxs-lookup"><span data-stu-id="296fb-106">Monitor the health of your network</span></span>
* <span data-ttu-id="296fb-107">Azure Application Gateway analytics to review</span><span class="sxs-lookup"><span data-stu-id="296fb-107">Azure Application Gateway analytics to review</span></span>
 * <span data-ttu-id="296fb-108">Azure Application Gateway logs</span><span class="sxs-lookup"><span data-stu-id="296fb-108">Azure Application Gateway logs</span></span>
 * <span data-ttu-id="296fb-109">Azure Application Gateway metrics</span><span class="sxs-lookup"><span data-stu-id="296fb-109">Azure Application Gateway metrics</span></span>
* <span data-ttu-id="296fb-110">Azure Network Security Group analytics to review</span><span class="sxs-lookup"><span data-stu-id="296fb-110">Azure Network Security Group analytics to review</span></span>
 * <span data-ttu-id="296fb-111">Azure Network Security Group logs</span><span class="sxs-lookup"><span data-stu-id="296fb-111">Azure Network Security Group logs</span></span>

## <a name="network-performance-monitor-npm"></a><span data-ttu-id="296fb-112">Network Performance Monitor (NPM)</span><span class="sxs-lookup"><span data-stu-id="296fb-112">Network Performance Monitor (NPM)</span></span>
<span data-ttu-id="296fb-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span><span class="sxs-lookup"><span data-stu-id="296fb-113">The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.</span></span>  <span data-ttu-id="296fb-114">It is used to monitor connectivity between:</span><span class="sxs-lookup"><span data-stu-id="296fb-114">It is used to monitor connectivity between:</span></span>
* <span data-ttu-id="296fb-115">public cloud and on-premises</span><span class="sxs-lookup"><span data-stu-id="296fb-115">public cloud and on-premises</span></span> 
* <span data-ttu-id="296fb-116">data centers and user locations (branch offices)</span><span class="sxs-lookup"><span data-stu-id="296fb-116">data centers and user locations (branch offices)</span></span>
* <span data-ttu-id="296fb-117">subnets hosting various tiers of a multi-tiered application.</span><span class="sxs-lookup"><span data-stu-id="296fb-117">subnets hosting various tiers of a multi-tiered application.</span></span>

<span data-ttu-id="296fb-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span><span class="sxs-lookup"><span data-stu-id="296fb-118">For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).</span></span>

## <a name="azure-application-gateway-and-network-security-group-analytics"></a><span data-ttu-id="296fb-119">Azure Application Gateway and Network Security Group analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-119">Azure Application Gateway and Network Security Group analytics</span></span>
<span data-ttu-id="296fb-120">To use the solutions:</span><span class="sxs-lookup"><span data-stu-id="296fb-120">To use the solutions:</span></span>
1. <span data-ttu-id="296fb-121">Add the management solution to Log Analytics, and</span><span class="sxs-lookup"><span data-stu-id="296fb-121">Add the management solution to Log Analytics, and</span></span>
2. <span data-ttu-id="296fb-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span><span class="sxs-lookup"><span data-stu-id="296fb-122">Enable diagnostics to direct the diagnostics to a Log Analytics workspace.</span></span> <span data-ttu-id="296fb-123">It is not necessary to write the logs to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="296fb-123">It is not necessary to write the logs to Azure Blob storage.</span></span>

<span data-ttu-id="296fb-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span><span class="sxs-lookup"><span data-stu-id="296fb-124">You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.</span></span>

<span data-ttu-id="296fb-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span><span class="sxs-lookup"><span data-stu-id="296fb-125">If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.</span></span>

> [!NOTE]
> <span data-ttu-id="296fb-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="296fb-126">In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="296fb-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span><span class="sxs-lookup"><span data-stu-id="296fb-127">If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.</span></span>
>
>

## <a name="review-azure-networking-data-collection-details"></a><span data-ttu-id="296fb-128">Review Azure networking data collection details</span><span class="sxs-lookup"><span data-stu-id="296fb-128">Review Azure networking data collection details</span></span>
<span data-ttu-id="296fb-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span><span class="sxs-lookup"><span data-stu-id="296fb-129">The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups.</span></span> <span data-ttu-id="296fb-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span><span class="sxs-lookup"><span data-stu-id="296fb-130">It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.</span></span>

<span data-ttu-id="296fb-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span><span class="sxs-lookup"><span data-stu-id="296fb-131">The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.</span></span>

| <span data-ttu-id="296fb-132">Platform</span><span class="sxs-lookup"><span data-stu-id="296fb-132">Platform</span></span> | <span data-ttu-id="296fb-133">Direct agent</span><span class="sxs-lookup"><span data-stu-id="296fb-133">Direct agent</span></span> | <span data-ttu-id="296fb-134">Systems Center Operations Manager agent</span><span class="sxs-lookup"><span data-stu-id="296fb-134">Systems Center Operations Manager agent</span></span> | <span data-ttu-id="296fb-135">Azure</span><span class="sxs-lookup"><span data-stu-id="296fb-135">Azure</span></span> | <span data-ttu-id="296fb-136">Operations Manager required?</span><span class="sxs-lookup"><span data-stu-id="296fb-136">Operations Manager required?</span></span> | <span data-ttu-id="296fb-137">Operations Manager agent data sent via management group</span><span class="sxs-lookup"><span data-stu-id="296fb-137">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="296fb-138">Collection frequency</span><span class="sxs-lookup"><span data-stu-id="296fb-138">Collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="296fb-139">Azure</span><span class="sxs-lookup"><span data-stu-id="296fb-139">Azure</span></span> |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |<span data-ttu-id="296fb-145">when logged</span><span class="sxs-lookup"><span data-stu-id="296fb-145">when logged</span></span> |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a><span data-ttu-id="296fb-146">Azure Application Gateway analytics solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-146">Azure Application Gateway analytics solution in Log Analytics</span></span>

<span data-ttu-id="296fb-147">The following logs are supported for Application Gateways:</span><span class="sxs-lookup"><span data-stu-id="296fb-147">The following logs are supported for Application Gateways:</span></span>

* <span data-ttu-id="296fb-148">ApplicationGatewayAccessLog</span><span class="sxs-lookup"><span data-stu-id="296fb-148">ApplicationGatewayAccessLog</span></span>
* <span data-ttu-id="296fb-149">ApplicationGatewayPerformanceLog</span><span class="sxs-lookup"><span data-stu-id="296fb-149">ApplicationGatewayPerformanceLog</span></span>
* <span data-ttu-id="296fb-150">ApplicationGatewayFirewallLog</span><span class="sxs-lookup"><span data-stu-id="296fb-150">ApplicationGatewayFirewallLog</span></span>

<span data-ttu-id="296fb-151">The following metrics are supported for Application Gateways:</span><span class="sxs-lookup"><span data-stu-id="296fb-151">The following metrics are supported for Application Gateways:</span></span>

* <span data-ttu-id="296fb-152">5 minute throughput</span><span class="sxs-lookup"><span data-stu-id="296fb-152">5 minute throughput</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="296fb-153">Install and configure the solution</span><span class="sxs-lookup"><span data-stu-id="296fb-153">Install and configure the solution</span></span>
<span data-ttu-id="296fb-154">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span><span class="sxs-lookup"><span data-stu-id="296fb-154">Use the following instructions to install and configure the Azure Application Gateway analytics solution:</span></span>

1. <span data-ttu-id="296fb-155">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="296fb-155">Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="296fb-156">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="296fb-156">Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor.</span></span> 

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a><span data-ttu-id="296fb-157">Enable Azure Application Gateway diagnostics in the portal</span><span class="sxs-lookup"><span data-stu-id="296fb-157">Enable Azure Application Gateway diagnostics in the portal</span></span>

1. <span data-ttu-id="296fb-158">In the Azure portal, navigate to the Application Gateway resource to monitor</span><span class="sxs-lookup"><span data-stu-id="296fb-158">In the Azure portal, navigate to the Application Gateway resource to monitor</span></span>
2. <span data-ttu-id="296fb-159">Select *Diagnostics logs* to open the following page</span><span class="sxs-lookup"><span data-stu-id="296fb-159">Select *Diagnostics logs* to open the following page</span></span>

   ![image of Azure Application Gateway resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. <span data-ttu-id="296fb-161">Click *Turn on diagnostics* to open the following page</span><span class="sxs-lookup"><span data-stu-id="296fb-161">Click *Turn on diagnostics* to open the following page</span></span>

   ![image of Azure Application Gateway resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. <span data-ttu-id="296fb-163">To turn on diagnostics, click *On* under *Status*</span><span class="sxs-lookup"><span data-stu-id="296fb-163">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="296fb-164">Click the checkbox for *Send to Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="296fb-164">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="296fb-165">Select an existing Log Analytics workspace, or create a workspace</span><span class="sxs-lookup"><span data-stu-id="296fb-165">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="296fb-166">Click the checkbox under **Log** for each of the log types to collect</span><span class="sxs-lookup"><span data-stu-id="296fb-166">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="296fb-167">Click *Save* to enable the logging of diagnostics to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-167">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

#### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="296fb-168">Enable Azure network diagnostics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="296fb-168">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="296fb-169">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span><span class="sxs-lookup"><span data-stu-id="296fb-169">The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.</span></span>

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a><span data-ttu-id="296fb-170">Use Azure Application Gateway analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-170">Use Azure Application Gateway analytics</span></span>
![image of Azure Application Gateway analytics tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

<span data-ttu-id="296fb-172">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span><span class="sxs-lookup"><span data-stu-id="296fb-172">After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="296fb-173">Application Gateway Access logs</span><span class="sxs-lookup"><span data-stu-id="296fb-173">Application Gateway Access logs</span></span>
  * <span data-ttu-id="296fb-174">Client and server errors for Application Gateway access logs</span><span class="sxs-lookup"><span data-stu-id="296fb-174">Client and server errors for Application Gateway access logs</span></span>
  * <span data-ttu-id="296fb-175">Requests per hour for each Application Gateway</span><span class="sxs-lookup"><span data-stu-id="296fb-175">Requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="296fb-176">Failed requests per hour for each Application Gateway</span><span class="sxs-lookup"><span data-stu-id="296fb-176">Failed requests per hour for each Application Gateway</span></span>
  * <span data-ttu-id="296fb-177">Errors by user agent for Application Gateways</span><span class="sxs-lookup"><span data-stu-id="296fb-177">Errors by user agent for Application Gateways</span></span>
* <span data-ttu-id="296fb-178">Application Gateway performance</span><span class="sxs-lookup"><span data-stu-id="296fb-178">Application Gateway performance</span></span>
  * <span data-ttu-id="296fb-179">Host health for Application Gateway</span><span class="sxs-lookup"><span data-stu-id="296fb-179">Host health for Application Gateway</span></span>
  * <span data-ttu-id="296fb-180">Maximum and 95th percentile for Application Gateway failed requests</span><span class="sxs-lookup"><span data-stu-id="296fb-180">Maximum and 95th percentile for Application Gateway failed requests</span></span>

![image of Azure Application Gateway analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![image of Azure Application Gateway analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway02.png)

<span data-ttu-id="296fb-183">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span><span class="sxs-lookup"><span data-stu-id="296fb-183">On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>
   
<span data-ttu-id="296fb-184">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span><span class="sxs-lookup"><span data-stu-id="296fb-184">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="296fb-185">You can also filter by facets to narrow the results.</span><span class="sxs-lookup"><span data-stu-id="296fb-185">You can also filter by facets to narrow the results.</span></span>


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a><span data-ttu-id="296fb-186">Azure Network Security Group analytics solution in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-186">Azure Network Security Group analytics solution in Log Analytics</span></span>

<span data-ttu-id="296fb-187">The following logs are supported for network security groups:</span><span class="sxs-lookup"><span data-stu-id="296fb-187">The following logs are supported for network security groups:</span></span>

* <span data-ttu-id="296fb-188">NetworkSecurityGroupEvent</span><span class="sxs-lookup"><span data-stu-id="296fb-188">NetworkSecurityGroupEvent</span></span>
* <span data-ttu-id="296fb-189">NetworkSecurityGroupRuleCounter</span><span class="sxs-lookup"><span data-stu-id="296fb-189">NetworkSecurityGroupRuleCounter</span></span>

### <a name="install-and-configure-the-solution"></a><span data-ttu-id="296fb-190">Install and configure the solution</span><span class="sxs-lookup"><span data-stu-id="296fb-190">Install and configure the solution</span></span>
<span data-ttu-id="296fb-191">Use the following instructions to install and configure the Azure Networking Analytics solution:</span><span class="sxs-lookup"><span data-stu-id="296fb-191">Use the following instructions to install and configure the Azure Networking Analytics solution:</span></span>

1. <span data-ttu-id="296fb-192">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="296fb-192">Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> 
2. <span data-ttu-id="296fb-193">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span><span class="sxs-lookup"><span data-stu-id="296fb-193">Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.</span></span>

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a><span data-ttu-id="296fb-194">Enable Azure network security group diagnostics in the portal</span><span class="sxs-lookup"><span data-stu-id="296fb-194">Enable Azure network security group diagnostics in the portal</span></span>

1. <span data-ttu-id="296fb-195">In the Azure portal, navigate to the Network Security Group resource to monitor</span><span class="sxs-lookup"><span data-stu-id="296fb-195">In the Azure portal, navigate to the Network Security Group resource to monitor</span></span>
2. <span data-ttu-id="296fb-196">Select *Diagnostics logs* to open the following page</span><span class="sxs-lookup"><span data-stu-id="296fb-196">Select *Diagnostics logs* to open the following page</span></span>

   ![image of Azure Network Security Group resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. <span data-ttu-id="296fb-198">Click *Turn on diagnostics* to open the following page</span><span class="sxs-lookup"><span data-stu-id="296fb-198">Click *Turn on diagnostics* to open the following page</span></span>

   ![image of Azure Network Security Group resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. <span data-ttu-id="296fb-200">To turn on diagnostics, click *On* under *Status*</span><span class="sxs-lookup"><span data-stu-id="296fb-200">To turn on diagnostics, click *On* under *Status*</span></span>
5. <span data-ttu-id="296fb-201">Click the checkbox for *Send to Log Analytics*</span><span class="sxs-lookup"><span data-stu-id="296fb-201">Click the checkbox for *Send to Log Analytics*</span></span>
6. <span data-ttu-id="296fb-202">Select an existing Log Analytics workspace, or create a workspace</span><span class="sxs-lookup"><span data-stu-id="296fb-202">Select an existing Log Analytics workspace, or create a workspace</span></span>
7. <span data-ttu-id="296fb-203">Click the checkbox under **Log** for each of the log types to collect</span><span class="sxs-lookup"><span data-stu-id="296fb-203">Click the checkbox under **Log** for each of the log types to collect</span></span>
8. <span data-ttu-id="296fb-204">Click *Save* to enable the logging of diagnostics to Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-204">Click *Save* to enable the logging of diagnostics to Log Analytics</span></span>

### <a name="enable-azure-network-diagnostics-using-powershell"></a><span data-ttu-id="296fb-205">Enable Azure network diagnostics using PowerShell</span><span class="sxs-lookup"><span data-stu-id="296fb-205">Enable Azure network diagnostics using PowerShell</span></span>

<span data-ttu-id="296fb-206">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span><span class="sxs-lookup"><span data-stu-id="296fb-206">The following PowerShell script provides an example of how to enable diagnostic logging for network security groups</span></span> 
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a><span data-ttu-id="296fb-207">Use Azure Network Security Group analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-207">Use Azure Network Security Group analytics</span></span>
<span data-ttu-id="296fb-208">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span><span class="sxs-lookup"><span data-stu-id="296fb-208">After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:</span></span>

* <span data-ttu-id="296fb-209">Network security group blocked flows</span><span class="sxs-lookup"><span data-stu-id="296fb-209">Network security group blocked flows</span></span>
  * <span data-ttu-id="296fb-210">Network security group rules with blocked flows</span><span class="sxs-lookup"><span data-stu-id="296fb-210">Network security group rules with blocked flows</span></span>
  * <span data-ttu-id="296fb-211">MAC addresses with blocked flows</span><span class="sxs-lookup"><span data-stu-id="296fb-211">MAC addresses with blocked flows</span></span>
* <span data-ttu-id="296fb-212">Network security group allowed flows</span><span class="sxs-lookup"><span data-stu-id="296fb-212">Network security group allowed flows</span></span>
  * <span data-ttu-id="296fb-213">Network security group rules with allowed flows</span><span class="sxs-lookup"><span data-stu-id="296fb-213">Network security group rules with allowed flows</span></span>
  * <span data-ttu-id="296fb-214">MAC addresses with allowed flows</span><span class="sxs-lookup"><span data-stu-id="296fb-214">MAC addresses with allowed flows</span></span>

![image of Azure Network Security Group analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg01.png)

![image of Azure Network Security Group analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg02.png)

<span data-ttu-id="296fb-217">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span><span class="sxs-lookup"><span data-stu-id="296fb-217">On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.</span></span>
   
<span data-ttu-id="296fb-218">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span><span class="sxs-lookup"><span data-stu-id="296fb-218">On any of the log search pages, you can view results by time, detailed results, and your log search history.</span></span> <span data-ttu-id="296fb-219">You can also filter by facets to narrow the results.</span><span class="sxs-lookup"><span data-stu-id="296fb-219">You can also filter by facets to narrow the results.</span></span>

## <a name="migrating-from-the-old-networking-analytics-solution"></a><span data-ttu-id="296fb-220">Migrating from the old Networking Analytics solution</span><span class="sxs-lookup"><span data-stu-id="296fb-220">Migrating from the old Networking Analytics solution</span></span>
<span data-ttu-id="296fb-221">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span><span class="sxs-lookup"><span data-stu-id="296fb-221">In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed.</span></span> <span data-ttu-id="296fb-222">These changes provide the following advantages:</span><span class="sxs-lookup"><span data-stu-id="296fb-222">These changes provide the following advantages:</span></span>
+ <span data-ttu-id="296fb-223">Logs are written directly to Log Analytics without the need to use a storage account</span><span class="sxs-lookup"><span data-stu-id="296fb-223">Logs are written directly to Log Analytics without the need to use a storage account</span></span>
+ <span data-ttu-id="296fb-224">Less latency from the time when logs are generated to them being available in Log Analytics</span><span class="sxs-lookup"><span data-stu-id="296fb-224">Less latency from the time when logs are generated to them being available in Log Analytics</span></span>
+ <span data-ttu-id="296fb-225">Fewer configuration steps</span><span class="sxs-lookup"><span data-stu-id="296fb-225">Fewer configuration steps</span></span>
+ <span data-ttu-id="296fb-226">A common format for all types of Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="296fb-226">A common format for all types of Azure diagnostics</span></span>

<span data-ttu-id="296fb-227">To use the updated solutions:</span><span class="sxs-lookup"><span data-stu-id="296fb-227">To use the updated solutions:</span></span>

1. [<span data-ttu-id="296fb-228">Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways</span><span class="sxs-lookup"><span data-stu-id="296fb-228">Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways</span></span>](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [<span data-ttu-id="296fb-229">Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="296fb-229">Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups</span></span>](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. <span data-ttu-id="296fb-230">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span><span class="sxs-lookup"><span data-stu-id="296fb-230">Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)</span></span>
3. <span data-ttu-id="296fb-231">Update any saved queries, dashboards, or alerts to use the new data type</span><span class="sxs-lookup"><span data-stu-id="296fb-231">Update any saved queries, dashboards, or alerts to use the new data type</span></span>
  + <span data-ttu-id="296fb-232">Type is to AzureDiagnostics.</span><span class="sxs-lookup"><span data-stu-id="296fb-232">Type is to AzureDiagnostics.</span></span> <span data-ttu-id="296fb-233">You can use the ResourceType to filter to Azure networking logs.</span><span class="sxs-lookup"><span data-stu-id="296fb-233">You can use the ResourceType to filter to Azure networking logs.</span></span>
  
    | <span data-ttu-id="296fb-234">Instead of:</span><span class="sxs-lookup"><span data-stu-id="296fb-234">Instead of:</span></span> | <span data-ttu-id="296fb-235">Use:</span><span class="sxs-lookup"><span data-stu-id="296fb-235">Use:</span></span> |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |
    
   + <span data-ttu-id="296fb-236">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span><span class="sxs-lookup"><span data-stu-id="296fb-236">For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case</span></span>
   + <span data-ttu-id="296fb-237">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span><span class="sxs-lookup"><span data-stu-id="296fb-237">For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.</span></span>
4. <span data-ttu-id="296fb-238">Remove the *Azure Networking Analytics (Deprecated)* solution.</span><span class="sxs-lookup"><span data-stu-id="296fb-238">Remove the *Azure Networking Analytics (Deprecated)* solution.</span></span> 
  + <span data-ttu-id="296fb-239">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span><span class="sxs-lookup"><span data-stu-id="296fb-239">If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false`</span></span> 

<span data-ttu-id="296fb-240">Data collected before the change is not visible in the new solution.</span><span class="sxs-lookup"><span data-stu-id="296fb-240">Data collected before the change is not visible in the new solution.</span></span> <span data-ttu-id="296fb-241">You can continue to query for this data using the old Type and field names.</span><span class="sxs-lookup"><span data-stu-id="296fb-241">You can continue to query for this data using the old Type and field names.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="296fb-242">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="296fb-242">Troubleshooting</span></span>
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a><span data-ttu-id="296fb-243">Next steps</span><span class="sxs-lookup"><span data-stu-id="296fb-243">Next steps</span></span>
* <span data-ttu-id="296fb-244">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span><span class="sxs-lookup"><span data-stu-id="296fb-244">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.</span></span>















