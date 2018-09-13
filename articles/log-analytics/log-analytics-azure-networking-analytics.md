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
# <a name="azure-networking-monitoring-solutions-in-log-analytics"></a>Azure networking monitoring solutions in Log Analytics

Log Analytics offers the following solutions for monitoring your networks:
* Network Performance Monitor (NPM) to
 * Monitor the health of your network
* Azure Application Gateway analytics to review
 * Azure Application Gateway logs
 * Azure Application Gateway metrics
* Azure Network Security Group analytics to review
 * Azure Network Security Group logs

## <a name="network-performance-monitor-npm"></a>Network Performance Monitor (NPM)
The [Network Performance Monitor](log-analytics-network-performance-monitor.md) management solution is a network monitoring solution, that monitors the health, availability and reachability of networks.  It is used to monitor connectivity between:
* public cloud and on-premises 
* data centers and user locations (branch offices)
* subnets hosting various tiers of a multi-tiered application.

For more information, see [Network Performance Monitor](log-analytics-network-performance-monitor.md).

## <a name="azure-application-gateway-and-network-security-group-analytics"></a>Azure Application Gateway and Network Security Group analytics
To use the solutions:
1. Add the management solution to Log Analytics, and
2. Enable diagnostics to direct the diagnostics to a Log Analytics workspace. It is not necessary to write the logs to Azure Blob storage.

You can enable diagnostics and the corresponding solution for either one or both of Application Gateway and Networking Security Groups.

If you do not enable diagnostic logging for a particular resource type, but install the solution, the dashboard blades for that resource are blank and display an error message.

> [!NOTE]
> In January 2017, the supported way of sending logs from Application Gateways and Network Security Groups to Log Analytics changed. If you see the **Azure Networking Analytics (deprecated)** solution, refer to [migrating from the old Networking Analytics solution](#migrating-from-the-old-networking-analytics-solution) for steps you need to follow.
>
>

## <a name="review-azure-networking-data-collection-details"></a>Review Azure networking data collection details
The Azure Application Gateway analytics and the Network Security Group analytics management solutions collect diagnostics logs directly from Azure Application Gateways and Network Security Groups. It is not necessary to write the logs to Azure Blob storage and no agent is required for data collection.

The following table shows data collection methods and other details about how data is collected for Azure Application Gateway analytics and the Network Security Group analytics.

| Platform | Direct agent | Systems Center Operations Manager agent | Azure | Operations Manager required? | Operations Manager agent data sent via management group | Collection frequency |
| --- | --- | --- | --- | --- | --- | --- |
| Azure |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![Yes](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-green.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |![No](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/oms-bullet-red.png) |when logged |


## <a name="azure-application-gateway-analytics-solution-in-log-analytics"></a>Azure Application Gateway analytics solution in Log Analytics

The following logs are supported for Application Gateways:

* ApplicationGatewayAccessLog
* ApplicationGatewayPerformanceLog
* ApplicationGatewayFirewallLog

The following metrics are supported for Application Gateways:

* 5 minute throughput

### <a name="install-and-configure-the-solution"></a>Install and configure the solution
Use the following instructions to install and configure the Azure Application Gateway analytics solution:

1. Enable the Azure Application Gateway analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureAppGatewayAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).
2. Enable diagnostics logging for the [Application Gateways](../application-gateway/application-gateway-diagnostics.md) you want to monitor. 

#### <a name="enable-azure-application-gateway-diagnostics-in-the-portal"></a>Enable Azure Application Gateway diagnostics in the portal

1. In the Azure portal, navigate to the Application Gateway resource to monitor
2. Select *Diagnostics logs* to open the following page

   ![image of Azure Application Gateway resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics01.png)
3. Click *Turn on diagnostics* to open the following page

   ![image of Azure Application Gateway resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-enable-diagnostics02.png)
4. To turn on diagnostics, click *On* under *Status*
5. Click the checkbox for *Send to Log Analytics*
6. Select an existing Log Analytics workspace, or create a workspace
7. Click the checkbox under **Log** for each of the log types to collect
8. Click *Save* to enable the logging of diagnostics to Log Analytics

#### <a name="enable-azure-network-diagnostics-using-powershell"></a>Enable Azure network diagnostics using PowerShell

The following PowerShell script provides an example of how to enable diagnostic logging for application gateways.

```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$gateway = Get-AzureRmApplicationGateway -Name 'ContosoGateway'

Set-AzureRmDiagnosticSetting -ResourceId $gateway.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-application-gateway-analytics"></a>Use Azure Application Gateway analytics
![image of Azure Application Gateway analytics tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway-tile.png)

After you click the **Azure Application Gateway analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:

* Application Gateway Access logs
  * Client and server errors for Application Gateway access logs
  * Requests per hour for each Application Gateway
  * Failed requests per hour for each Application Gateway
  * Errors by user agent for Application Gateways
* Application Gateway performance
  * Host health for Application Gateway
  * Maximum and 95th percentile for Application Gateway failed requests

![image of Azure Application Gateway analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway01.png)

![image of Azure Application Gateway analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-appgateway02.png)

On the **Azure Application Gateway analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.
   
On any of the log search pages, you can view results by time, detailed results, and your log search history. You can also filter by facets to narrow the results.


## <a name="azure-network-security-group-analytics-solution-in-log-analytics"></a>Azure Network Security Group analytics solution in Log Analytics

The following logs are supported for network security groups:

* NetworkSecurityGroupEvent
* NetworkSecurityGroupRuleCounter

### <a name="install-and-configure-the-solution"></a>Install and configure the solution
Use the following instructions to install and configure the Azure Networking Analytics solution:

1. Enable the Azure Network Security Group analytics solution from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureNSGAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md). 
2. Enable diagnostics logging for the [Network Security Group](../virtual-network/virtual-network-nsg-manage-log.md) resources you want to monitor.

### <a name="enable-azure-network-security-group-diagnostics-in-the-portal"></a>Enable Azure network security group diagnostics in the portal

1. In the Azure portal, navigate to the Network Security Group resource to monitor
2. Select *Diagnostics logs* to open the following page

   ![image of Azure Network Security Group resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics01.png)
3. Click *Turn on diagnostics* to open the following page

   ![image of Azure Network Security Group resource](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg-enable-diagnostics02.png)
4. To turn on diagnostics, click *On* under *Status*
5. Click the checkbox for *Send to Log Analytics*
6. Select an existing Log Analytics workspace, or create a workspace
7. Click the checkbox under **Log** for each of the log types to collect
8. Click *Save* to enable the logging of diagnostics to Log Analytics

### <a name="enable-azure-network-diagnostics-using-powershell"></a>Enable Azure network diagnostics using PowerShell

The following PowerShell script provides an example of how to enable diagnostic logging for network security groups 
```powershell
$workspaceId = "/subscriptions/d2e37fee-1234-40b2-5678-0b2199de3b50/resourcegroups/oi-default-east-us/providers/microsoft.operationalinsights/workspaces/rollingbaskets"

$nsg = Get-AzureRmNetworkSecurityGroup -Name 'ContosoNSG'

Set-AzureRmDiagnosticSetting -ResourceId $nsg.ResourceId  -WorkspaceId $workspaceId -Enabled $true
```

### <a name="use-azure-network-security-group-analytics"></a>Use Azure Network Security Group analytics
After you click the **Azure Network Security Group analytics** tile on the Overview, you can view summaries of your logs and then drill in to details for the following categories:

* Network security group blocked flows
  * Network security group rules with blocked flows
  * MAC addresses with blocked flows
* Network security group allowed flows
  * Network security group rules with allowed flows
  * MAC addresses with allowed flows

![image of Azure Network Security Group analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg01.png)

![image of Azure Network Security Group analytics dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/log-analytics/media/log-analytics-azure-networking/log-analytics-nsg02.png)

On the **Azure Network Security Group analytics** dashboard, review the summary information in one of the blades, and then click one to view detailed information on the log search page.
   
On any of the log search pages, you can view results by time, detailed results, and your log search history. You can also filter by facets to narrow the results.

## <a name="migrating-from-the-old-networking-analytics-solution"></a>Migrating from the old Networking Analytics solution
In January 2017, the supported way of sending logs from Azure Application Gateways and Azure Network Security Groups to Log Analytics changed. These changes provide the following advantages:
+ Logs are written directly to Log Analytics without the need to use a storage account
+ Less latency from the time when logs are generated to them being available in Log Analytics
+ Fewer configuration steps
+ A common format for all types of Azure diagnostics

To use the updated solutions:

1. [Configure diagnostics to be sent directly to Log Analytics from Azure Application Gateways](#enable-azure-application-gateway-diagnostics-in-the-portal)
2. [Configure diagnostics to be sent directly to Log Analytics from Azure Network Security Groups](#enable-azure-network-security-group-diagnostics-in-the-portal)
2. Enable the *Azure Application Gateway Analytics* and the *Azure Network Security Group Analytics* solution by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md)
3. Update any saved queries, dashboards, or alerts to use the new data type
  + Type is to AzureDiagnostics. You can use the ResourceType to filter to Azure networking logs.
  
    | Instead of: | Use: |
    | --- | --- |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayAccess`| `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayAccess` |
    |`Type=NetworkApplicationgateways OperationName=ApplicationGatewayPerformance` | `Type=AzureDiagnostics ResourceType=APPLICATIONGATEWAYS OperationName=ApplicationGatewayPerformance` |
    | `Type=NetworkSecuritygroups` | `Type=AzureDiagnostics ResourceType=NETWORKSECURITYGROUPS` |
    
   + For any field that has a suffix of \_s, \_d, or \_g in the name, change the first character to lower case
   + For any field that has a suffix of \_o in name, the data is split into individual fields based on the nested field names.
4. Remove the *Azure Networking Analytics (Deprecated)* solution. 
  + If you are using PowerShell, use `Set-AzureOperationalInsightsIntelligencePack -ResourceGroupName <resource group that the workspace is in> -WorkspaceName <name of the log analytics workspace> -IntelligencePackName "AzureNetwork" -Enabled $false` 

Data collected before the change is not visible in the new solution. You can continue to query for this data using the old Type and field names.

## <a name="troubleshooting"></a>Troubleshooting
[!INCLUDE [log-analytics-troubleshoot-azure-diagnostics](../../includes/log-analytics-troubleshoot-azure-diagnostics.md)]

## <a name="next-steps"></a>Next steps
* Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Azure diagnostics data.














