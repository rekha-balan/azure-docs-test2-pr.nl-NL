---
title: Create a log alert with a Resource Manager template
description: Learn how to create log alert by using an Azure Resource Manager template and API.
author: msvijayn
services: monitoring
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 05/01/2018
ms.author: vinagara
ms.component: alerts
ms.openlocfilehash: 588a0686eda1966582b82a4673a8b6805453c94c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865480"
---
# <a name="create-a-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="c7413-103">Create a log alert with a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="c7413-103">Create a log alert with a Resource Manager template</span></span>
<span data-ttu-id="c7413-104">This article shows how you can manage [log alerts](monitor-alerts-unified-log.md) programmatically at scale, in Azure using [Azure Resource Manager template](..//azure-resource-manager/resource-group-authoring-templates.md) via [Azure Powershell](../azure-resource-manager/resource-group-template-deploy.md) and [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c7413-104">This article shows how you can manage [log alerts](monitor-alerts-unified-log.md) programmatically at scale, in Azure using [Azure Resource Manager template](..//azure-resource-manager/resource-group-authoring-templates.md) via [Azure Powershell](../azure-resource-manager/resource-group-template-deploy.md) and [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md).</span></span> <span data-ttu-id="c7413-105">Currently Azure Alerts, supports log alerts on queries from [Azure Log Analytics](../log-analytics/log-analytics-tutorial-viewdata.md) and [Azure Application Insights](../application-insights/app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="c7413-105">Currently Azure Alerts, supports log alerts on queries from [Azure Log Analytics](../log-analytics/log-analytics-tutorial-viewdata.md) and [Azure Application Insights](../application-insights/app-insights-analytics-tour.md).</span></span>

## <a name="managing-log-alert-on-log-analytics"></a><span data-ttu-id="c7413-106">Managing log alert on Log Analytics</span><span class="sxs-lookup"><span data-stu-id="c7413-106">Managing log alert on Log Analytics</span></span>
<span data-ttu-id="c7413-107">Log alert for [Azure Log Analytics](../log-analytics/log-analytics-tutorial-viewdata.md) is integrated into the [new Azure alerts experience](monitoring-overview-unified-alerts.md); while it still runs off Log Analytics APIs and remains compatibility with schema used earlier to manage [alerts in OMS portal](..//log-analytics/log-analytics-alerts-creating.md).</span><span class="sxs-lookup"><span data-stu-id="c7413-107">Log alert for [Azure Log Analytics](../log-analytics/log-analytics-tutorial-viewdata.md) is integrated into the [new Azure alerts experience](monitoring-overview-unified-alerts.md); while it still runs off Log Analytics APIs and remains compatibility with schema used earlier to manage [alerts in OMS portal](..//log-analytics/log-analytics-alerts-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c7413-108">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span><span class="sxs-lookup"><span data-stu-id="c7413-108">Beginning May 14, 2018, all alerts in a workspace will automatically begin to extend into Azure.</span></span> <span data-ttu-id="c7413-109">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span><span class="sxs-lookup"><span data-stu-id="c7413-109">A user can voluntarily initiate extending alerts to Azure before May 14, 2018.</span></span> <span data-ttu-id="c7413-110">For more information, see [Extend Alerts into Azure from OMS](monitoring-alerts-extend.md).</span><span class="sxs-lookup"><span data-stu-id="c7413-110">For more information, see [Extend Alerts into Azure from OMS](monitoring-alerts-extend.md).</span></span> 

### <a name="using-azure-resource-manager-template"></a><span data-ttu-id="c7413-111">Using Azure Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="c7413-111">Using Azure Resource Manager Template</span></span>
<span data-ttu-id="c7413-112">Log alerts for Log Analytics are created by alert rules that run a saved search on a regular interval.</span><span class="sxs-lookup"><span data-stu-id="c7413-112">Log alerts for Log Analytics are created by alert rules that run a saved search on a regular interval.</span></span> <span data-ttu-id="c7413-113">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span><span class="sxs-lookup"><span data-stu-id="c7413-113">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span> 

<span data-ttu-id="c7413-114">Resource template for Log analytics saved search and Log analytics alertsare available in Log Analytics section of documentation.</span><span class="sxs-lookup"><span data-stu-id="c7413-114">Resource template for Log analytics saved search and Log analytics alertsare available in Log Analytics section of documentation.</span></span> <span data-ttu-id="c7413-115">To learn more see, [Adding Log Analytics saved searches and alerts](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md); which includes illustrative samples as well as schema details.</span><span class="sxs-lookup"><span data-stu-id="c7413-115">To learn more see, [Adding Log Analytics saved searches and alerts](../operations-management-suite/operations-management-suite-solutions-resources-searches-alerts.md); which includes illustrative samples as well as schema details.</span></span>

### <a name="using-resource-template-via-apipowershell"></a><span data-ttu-id="c7413-116">Using Resource Template via API/Powershell</span><span class="sxs-lookup"><span data-stu-id="c7413-116">Using Resource Template via API/Powershell</span></span>
<span data-ttu-id="c7413-117">The Log Analytics Alert REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span><span class="sxs-lookup"><span data-stu-id="c7413-117">The Log Analytics Alert REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="c7413-118">The API can thus be accessed from a PowerShell command line and will output search results to you in JSON format, allowing you to use the results in many different ways programmatically.</span><span class="sxs-lookup"><span data-stu-id="c7413-118">The API can thus be accessed from a PowerShell command line and will output search results to you in JSON format, allowing you to use the results in many different ways programmatically.</span></span>

<span data-ttu-id="c7413-119">Learn more  about [create and manage alert rules in Log Analytics with REST API](../log-analytics/log-analytics-api-alerts.md); including examples of accessing the API from Powershell.</span><span class="sxs-lookup"><span data-stu-id="c7413-119">Learn more  about [create and manage alert rules in Log Analytics with REST API](../log-analytics/log-analytics-api-alerts.md); including examples of accessing the API from Powershell.</span></span>

## <a name="managing-log-alert-on-application-insights"></a><span data-ttu-id="c7413-120">Managing log alert on Application Insights</span><span class="sxs-lookup"><span data-stu-id="c7413-120">Managing log alert on Application Insights</span></span>
<span data-ttu-id="c7413-121">Log alerts for Azure Application Insights have been introduced as part of the new Azure alerts under Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="c7413-121">Log alerts for Azure Application Insights have been introduced as part of the new Azure alerts under Azure Monitor.</span></span> <span data-ttu-id="c7413-122">Hence it runs under Azure Monitor API as [Scheduled Query Rules](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/) REST operation group.</span><span class="sxs-lookup"><span data-stu-id="c7413-122">Hence it runs under Azure Monitor API as [Scheduled Query Rules](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/) REST operation group.</span></span>

### <a name="using-azure-resource-manager-template"></a><span data-ttu-id="c7413-123">Using Azure Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="c7413-123">Using Azure Resource Manager Template</span></span>
<span data-ttu-id="c7413-124">Log alert for Application Insights resources has a type of `Microsoft.Insights/scheduledQueryRules/`.</span><span class="sxs-lookup"><span data-stu-id="c7413-124">Log alert for Application Insights resources has a type of `Microsoft.Insights/scheduledQueryRules/`.</span></span> <span data-ttu-id="c7413-125">For more information on this resource type, see [Azure Monitor - Scheduled Query Rules API reference](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/).</span><span class="sxs-lookup"><span data-stu-id="c7413-125">For more information on this resource type, see [Azure Monitor - Scheduled Query Rules API reference](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/).</span></span>

<span data-ttu-id="c7413-126">The following is the structure for [Scheduled Query Rules creation](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/createorupdate) based resource template, with sample data set as variables.</span><span class="sxs-lookup"><span data-stu-id="c7413-126">The following is the structure for [Scheduled Query Rules creation](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/createorupdate) based resource template, with sample data set as variables.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0", 
    "parameters": {      
    },   
    "variables": {
    "alertLocation": "southcentralus",
    "alertName": "samplelogalert",
    "alertTag": "hidden-link:/subscriptions/a123d7efg-123c-1234-5678-a12bc3defgh4/resourceGroups/myRG/providers/microsoft.insights/components/sampleAIapplication",
    "alertDesription": "Sample log search alert",
    "alertStatus": "true",
    "alertSource":{
        "Query":"requests",
        "SourceId": "/subscriptions/a123d7efg-123c-1234-5678-a12bc3defgh4/resourceGroups/myRG/providers/microsoft.insights/components/sampleAIapplication",
        "Type":"ResultCount"
         },
     "alertSchedule":{
         "Frequency": 15,
         "Time": 60
         },
     "alertActions":{
         "SeverityLevel": "4"
         },
      "alertTrigger":{
        "Operator":"GreaterThan",
        "Threshold":"1"
         },
       "actionGrp":{
        "ActionGroup": "/subscriptions/a123d7efg-123c-1234-5678-a12bc3defgh4/resourceGroups/myRG/providers/microsoft.insights/actiongroups/sampleAG",
        "Subject": "Customized Email Header",
        "Webhook": "{ \"alertname\":\"#alertrulename\", \"IncludeSearchResults\":true }"           
         }
  },
  "resources":[ {
    "name":"[variables('alertName')]",
    "type":"Microsoft.Insights/scheduledQueryRules",
    "apiVersion": "2018-04-16",
    "location": "[variables('alertLocation')]",
    "tags":{"[variables('alertTag')]": "Resource"},
    "properties":{
       "description": "[variables('alertDesription')]",
       "enabled": "[variables('alertStatus')]",
       "source": {
           "query": "[variables('alertSource').Query]",
           "dataSourceId": "[variables('alertSource').SourceId]",
           "queryType":"[variables('alertSource').Type]"
       },
      "schedule":{
           "frequencyInMinutes": "[variables('alertSchedule').Frequency]",
           "timeWindowInMinutes": "[variables('alertSchedule').Time]"    
       },
      "action":{
           "odata.type": "Microsoft.WindowsAzure.Management.Monitoring.Alerts.Models.Microsoft.AppInsights.Nexus.DataContracts.Resources.ScheduledQueryRules.AlertingAction",
           "severity":"[variables('alertActions').SeverityLevel]",
           "aznsAction":{
               "actionGroup":"[array(variables('actionGrp').ActionGroup)]",
               "emailSubject":"[variables('actionGrp').Subject]",
               "customWebhookPayload":"[variables('actionGrp').Webhook]"
           },
       "trigger":{
               "thresholdOperator":"[variables('alertTrigger').Operator]",
               "threshold":"[variables('alertTrigger').Threshold]"
           }
       }
     }
   }
 ]
}
```
> [!IMPORTANT]
> <span data-ttu-id="c7413-127">Tag field with hidden-link to target resource is mandatory in use of [Scheduled Query Rules ](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/) API call or resource template.</span><span class="sxs-lookup"><span data-stu-id="c7413-127">Tag field with hidden-link to target resource is mandatory in use of [Scheduled Query Rules ](https://docs.microsoft.com/en-us/rest/api/monitor/scheduledqueryrules/) API call or resource template.</span></span> 

<span data-ttu-id="c7413-128">The sample json above can be saved as (say) sampleScheduledQueryRule.json for the purpose of this walkthrough and can be deployed using [Azure Resource Manager in Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template).</span><span class="sxs-lookup"><span data-stu-id="c7413-128">The sample json above can be saved as (say) sampleScheduledQueryRule.json for the purpose of this walkthrough and can be deployed using [Azure Resource Manager in Azure portal](../azure-resource-manager/resource-group-template-deploy-portal.md#deploy-resources-from-custom-template).</span></span>

### <a name="using-resource-template-via-clipowershell"></a><span data-ttu-id="c7413-129">Using Resource Template via CLI/Powershell</span><span class="sxs-lookup"><span data-stu-id="c7413-129">Using Resource Template via CLI/Powershell</span></span>
<span data-ttu-id="c7413-130">Azure Monitor - Scheduled Query Rules API is a REST API and fully compatible with Azure Resource Manager REST API.</span><span class="sxs-lookup"><span data-stu-id="c7413-130">Azure Monitor - Scheduled Query Rules API is a REST API and fully compatible with Azure Resource Manager REST API.</span></span> <span data-ttu-id="c7413-131">Hence it can be used via Powershell using Resource Manager cmdlet as well as Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="c7413-131">Hence it can be used via Powershell using Resource Manager cmdlet as well as Azure CLI.</span></span>

<span data-ttu-id="c7413-132">Illustrated below usage via Azure Resource Manager PowerShell cmdlet for sample Resource Template shown earlier (sampleScheduledQueryRule.json):</span><span class="sxs-lookup"><span data-stu-id="c7413-132">Illustrated below usage via Azure Resource Manager PowerShell cmdlet for sample Resource Template shown earlier (sampleScheduledQueryRule.json):</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName "myRG" -TemplateFile "D:\Azure\Templates\sampleScheduledQueryRule.json"
```
<span data-ttu-id="c7413-133">Illustrated below usage via Azure Resource Manager command in Azure CLI for sample Resource Template shown earlier (sampleScheduledQueryRule.json):</span><span class="sxs-lookup"><span data-stu-id="c7413-133">Illustrated below usage via Azure Resource Manager command in Azure CLI for sample Resource Template shown earlier (sampleScheduledQueryRule.json):</span></span>

```azurecli
az group deployment create --resource-group myRG --template-file sampleScheduledQueryRule.json
```
<span data-ttu-id="c7413-134">On successful operation, 201 will be returned to state new alert rule creation or 200 will be returned if an existing alert rule was modified.</span><span class="sxs-lookup"><span data-stu-id="c7413-134">On successful operation, 201 will be returned to state new alert rule creation or 200 will be returned if an existing alert rule was modified.</span></span>


## <a name="next-steps"></a><span data-ttu-id="c7413-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="c7413-135">Next steps</span></span>
* <span data-ttu-id="c7413-136">Understand [Webhook actions for log alerts](monitor-alerts-unified-log-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="c7413-136">Understand [Webhook actions for log alerts](monitor-alerts-unified-log-webhook.md)</span></span>
* <span data-ttu-id="c7413-137">Learn about the new [Azure Alerts](monitoring-overview-unified-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="c7413-137">Learn about the new [Azure Alerts](monitoring-overview-unified-alerts.md)</span></span>
* <span data-ttu-id="c7413-138">Learn more about [Application Insights](../application-insights/app-insights-analytics.md)</span><span class="sxs-lookup"><span data-stu-id="c7413-138">Learn more about [Application Insights](../application-insights/app-insights-analytics.md)</span></span>
* <span data-ttu-id="c7413-139">Learn more about [Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c7413-139">Learn more about [Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>   
