---
title: Create a metric alert with a Resource Manager template
description: Learn how to use a Resource Manager template to create a metric alert.
author: snehithm
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 4/26/2018
ms.author: snmuvva
ms.component: alerts
ms.openlocfilehash: 7289259214f90507c5b9cf527f19f0cf7026798c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857537"
---
# <a name="create-a-metric-alert-with-a-resource-manager-template"></a><span data-ttu-id="1b9fc-103">Create a metric alert with a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="1b9fc-103">Create a metric alert with a Resource Manager template</span></span>
<span data-ttu-id="1b9fc-104">This article shows how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure [newer metric alerts](monitoring-near-real-time-metric-alerts.md) in Azure Monitor.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-104">This article shows how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure [newer metric alerts](monitoring-near-real-time-metric-alerts.md) in Azure Monitor.</span></span> <span data-ttu-id="1b9fc-105">Resource Manager templates enable you to programmatically set up alerts in a consistent and reproducible way across your environments.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-105">Resource Manager templates enable you to programmatically set up alerts in a consistent and reproducible way across your environments.</span></span> <span data-ttu-id="1b9fc-106">Newer metric alerts are currently available on [this set of resource types](monitoring-near-real-time-metric-alerts.md#metrics-and-dimensions-supported).</span><span class="sxs-lookup"><span data-stu-id="1b9fc-106">Newer metric alerts are currently available on [this set of resource types](monitoring-near-real-time-metric-alerts.md#metrics-and-dimensions-supported).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1b9fc-107">Resource Manager template specified for metric alert will not work for resource type: Microsoft.OperationalInsights/workspaces; as support for metrics from Log Analytics is in preview.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-107">Resource Manager template specified for metric alert will not work for resource type: Microsoft.OperationalInsights/workspaces; as support for metrics from Log Analytics is in preview.</span></span> <span data-ttu-id="1b9fc-108">Users interested in using the preview functionality with resource template, can contact [Azure Alerts Feedback](mailto:azurealertsfeedback@microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="1b9fc-108">Users interested in using the preview functionality with resource template, can contact [Azure Alerts Feedback](mailto:azurealertsfeedback@microsoft.com)</span></span>


<span data-ttu-id="1b9fc-109">The basic steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="1b9fc-109">The basic steps are as follows:</span></span>

1. <span data-ttu-id="1b9fc-110">Use one of the templates below as a JSON file that describes how to create the alert.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-110">Use one of the templates below as a JSON file that describes how to create the alert.</span></span>
2. <span data-ttu-id="1b9fc-111">Edit and use the corresponding parameters file as a JSON to customize the alert</span><span class="sxs-lookup"><span data-stu-id="1b9fc-111">Edit and use the corresponding parameters file as a JSON to customize the alert</span></span>
3. <span data-ttu-id="1b9fc-112">Deploy the template using [any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="1b9fc-112">Deploy the template using [any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>


## <a name="resource-manager-template-for-a-simple-metric-alert"></a><span data-ttu-id="1b9fc-113">Resource Manager template for a simple metric alert</span><span class="sxs-lookup"><span data-stu-id="1b9fc-113">Resource Manager template for a simple metric alert</span></span>
<span data-ttu-id="1b9fc-114">To create an alert using a Resource Manager template, you create a resource of type `Microsoft.Insights/metricAlerts` and fill in all related properties.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-114">To create an alert using a Resource Manager template, you create a resource of type `Microsoft.Insights/metricAlerts` and fill in all related properties.</span></span> <span data-ttu-id="1b9fc-115">Below is a sample template that creates a metric alert rule.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-115">Below is a sample template that creates a metric alert rule.</span></span>

<span data-ttu-id="1b9fc-116">Save the json below as simplemetricalert.json for the purpose of this walk through.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-116">Save the json below as simplemetricalert.json for the purpose of this walk through.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "This is a metric alert",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "alertSeverity": {
            "type": "int",
            "defaultValue": 3,
            "allowedValues": [
                0,
                1,
                2,
                3,
                4
            ],
            "metadata": {
                "description": "Severity of alert {0,1,2,3,4}"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether the alert is enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Full Resource ID of the resource emitting the metric that will be used for the comparison. For example /subscriptions/00000000-0000-0000-0000-0000-00000000/resourceGroups/ResourceGroupName/providers/Microsoft.compute/virtualMachines/VM_xyz"
            }
        },
        "metricName": {
            "type": "string",
            "minLength": 1,
            "metadata": {
                "description": "Name of the metric used in the comparison to activate the alert."
            }
        },
        "operator": {
            "type": "string",
            "defaultValue": "GreaterThan",
            "allowedValues": [
                "Equals",
                "NotEquals",
                "GreaterThan",
                "GreaterThanOrEqual",
                "LessThan",
                "LessThanOrEqual"
            ],
            "metadata": {
                "description": "Operator comparing the current value with the threshold value."
            }
        },
        "threshold": {
            "type": "string",
            "defaultValue": "0",
            "metadata": {
                "description": "The threshold value at which the alert is activated."
            }
        },
        "timeAggregation": {
            "type": "string",
            "defaultValue": "Average",
            "allowedValues": [
                "Average",
                "Minimum",
                "Maximum",
                "Total"
            ],
            "metadata": {
                "description": "How the data that is collected should be combined over time."
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "evaluationFrequency": {
            "type": "string",
            "defaultValue": "PT1M",
            "metadata": {
                "description": "how often the metric alert is evaluated represented in ISO 8601 duration format"
            }
        },
        "actionGroupId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The ID of the action group that is triggered when the alert is activated or deactivated"
            }
        }
    },
    "variables": {  },
    "resources": [
        {
            "name": "[parameters('alertName')]",
            "type": "Microsoft.Insights/metricAlerts",
            "location": "global",
            "apiVersion": "2018-03-01",
            "tags": {},
            "properties": {
                "description": "[parameters('alertDescription')]",
                "severity": "[parameters('alertSeverity')]",
                "enabled": "[parameters('isEnabled')]",
                "scopes": ["[parameters('resourceId')]"],
                "evaluationFrequency":"[parameters('evaluationFrequency')]",
                "windowSize": "[parameters('windowSize')]",
                "criteria": {
                    "odata.type": "Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria",
                    "allOf": [
                        {
                            "name" : "1st criterion",
                            "metricName": "[parameters('metricName')]",
                            "dimensions":[],   
                            "operator": "[parameters('operator')]",
                            "threshold" : "[parameters('threshold')]",
                            "timeAggregation": "[parameters('timeAggregation')]"
                        }
                    ]
                },
                "actions": [
                    {
                        "actionGroupId": "[parameters('actionGroupId')]"                
                    }
                ]
            }
        }
    ]
}
```

<span data-ttu-id="1b9fc-117">An explanation of the schema and properties for an alert rule [is available here](https://docs.microsoft.com/en-us/rest/api/monitor/metricalerts/createorupdate).</span><span class="sxs-lookup"><span data-stu-id="1b9fc-117">An explanation of the schema and properties for an alert rule [is available here](https://docs.microsoft.com/en-us/rest/api/monitor/metricalerts/createorupdate).</span></span>

<span data-ttu-id="1b9fc-118">You can set the values for the parameters either on the command line or through a parameter file.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-118">You can set the values for the parameters either on the command line or through a parameter file.</span></span> <span data-ttu-id="1b9fc-119">A sample parameter file is provided below.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-119">A sample parameter file is provided below.</span></span> 

<span data-ttu-id="1b9fc-120">Save the json below as simplemetricalert.parameters.json and modify it as required.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-120">Save the json below as simplemetricalert.parameters.json and modify it as required.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "value": "New Metric Alert"
        },
        "alertDescription": {
            "value": "New metric alert created via template"
        },
        "alertSeverity": {
            "value":3
        },
        "isEnabled": {
            "value": true
        },
        "resourceId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/replace-with-resourceGroup-name/providers/Microsoft.Compute/virtualMachines/replace-with-resource-name"
        },
        "metricName": {
            "value": "Percentage CPU"
        },
        "operator": {
          "value": "GreaterThan"
        },
        "threshold": {
            "value": "80"
        },
        "timeAggregation": {
            "value": "Average"
        },
        "actionGroupId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/resource-group-name/providers/Microsoft.Insights/actionGroups/replace-with-action-group"
        }
    }
}
```


<span data-ttu-id="1b9fc-121">You can create the metric alert using the template and parameters file using PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-121">You can create the metric alert using the template and parameters file using PowerShell or Azure CLI.</span></span>

<span data-ttu-id="1b9fc-122">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b9fc-122">Using Azure PowerShell</span></span>

```powershell
Connect-AzureRmAccount

Select-AzureRmSubscription -SubscriptionName <yourSubscriptionName>
 
New-AzureRmResourceGroupDeployment -Name AlertDeployment -ResourceGroupName ResourceGroupofTargetResource `
  -TemplateFile simplemetricalert.json -TemplateParametersFile simplemetricalert.parameters.json
```


<span data-ttu-id="1b9fc-123">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b9fc-123">Using Azure CLI</span></span>
```azurecli
az login

az group deployment create \
    --name AlertDeployment \
    --resource-group ResourceGroupofTargetResource \
    --template-file simplemetricalert.json \
    --parameters @simplemetricalert.parameters.json
```

> [!NOTE]
>
> <span data-ttu-id="1b9fc-124">While the metric alert could be created in a different resource group to the target resource, we recommend using the same resource group as your target resource.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-124">While the metric alert could be created in a different resource group to the target resource, we recommend using the same resource group as your target resource.</span></span>

## <a name="resource-manager-template-for-a-more-advanced-metric-alert"></a><span data-ttu-id="1b9fc-125">Resource Manager template for a more advanced metric alert</span><span class="sxs-lookup"><span data-stu-id="1b9fc-125">Resource Manager template for a more advanced metric alert</span></span>
<span data-ttu-id="1b9fc-126">Newer metric alerts support alerting on multi-dimensional metrics as well as supporting multiple criteria.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-126">Newer metric alerts support alerting on multi-dimensional metrics as well as supporting multiple criteria.</span></span> <span data-ttu-id="1b9fc-127">You can use the following template to create a more advanced metric alert on dimensional metrics and specify multiple criteria.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-127">You can use the following template to create a more advanced metric alert on dimensional metrics and specify multiple criteria.</span></span>

<span data-ttu-id="1b9fc-128">Save the json below as advancedmetricalert.json for the purpose of this walk through.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-128">Save the json below as advancedmetricalert.json for the purpose of this walk through.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "type": "string",
            "metadata": {
                "description": "Name of the alert"
            }
        },
        "alertDescription": {
            "type": "string",
            "defaultValue": "This is a metric alert",
            "metadata": {
                "description": "Description of alert"
            }
        },
        "alertSeverity": {
            "type": "int",
            "defaultValue": 3,
            "allowedValues": [
                0,
                1,
                2,
                3,
                4
            ],
            "metadata": {
                "description": "Severity of alert {0,1,2,3,4}"
            }
        },
        "isEnabled": {
            "type": "bool",
            "defaultValue": true,
            "metadata": {
                "description": "Specifies whether the alert is enabled"
            }
        },
        "resourceId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "Resource ID of the resource emitting the metric that will be used for the comparison."
            }
        },
        "criterion1":{
            "type": "object",
            "metadata": {
                "description": "Criterion includes metric name, dimension values, threshold and an operator. The alert rule fires when ALL criteria are met"
            }
        },
        "criterion2": {
            "type": "object",
            "metadata": {
                "description": "Criterion includes metric name, dimension values, threshold and an operator. The alert rule fires when ALL criteria are met"
            }
        },
        "windowSize": {
            "type": "string",
            "defaultValue": "PT5M",
            "metadata": {
                "description": "Period of time used to monitor alert activity based on the threshold. Must be between five minutes and one day. ISO 8601 duration format."
            }
        },
        "evaluationFrequency": {
            "type": "string",
            "defaultValue": "PT1M",
            "metadata": {
                "description": "how often the metric alert is evaluated represented in ISO 8601 duration format"
            }
        },
        "actionGroupId": {
            "type": "string",
            "defaultValue": "",
            "metadata": {
                "description": "The ID of the action group that is triggered when the alert is activated or deactivated"
            }
        }
    },
    "variables": { 
        "criterion1": "[array(parameters('criterion1'))]",
        "criterion2": "[array(parameters('criterion2'))]",
        "criteria": "[concat(variables('criterion1'),variables('criterion2'))]"
     },
    "resources": [
        {
            "name": "[parameters('alertName')]",
            "type": "Microsoft.Insights/metricAlerts",
            "location": "global",
            "apiVersion": "2018-03-01",
            "tags": {},
            "properties": {
                "description": "[parameters('alertDescription')]",
                "severity": "[parameters('alertSeverity')]",
                "enabled": "[parameters('isEnabled')]",
                "scopes": ["[parameters('resourceId')]"],
                "evaluationFrequency":"[parameters('evaluationFrequency')]",
                "windowSize": "[parameters('windowSize')]",
                "criteria": {
                    "odata.type": "Microsoft.Azure.Monitor.SingleResourceMultipleMetricCriteria",
                    "allOf": "[variables('criteria')]"
                },
                "actions": [
                    {
                        "actionGroupId": "[parameters('actionGroupId')]"                
                    }
                ]
            }
        }
    ]
}
```

<span data-ttu-id="1b9fc-129">You can use the above template along with the parameter file provided below.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-129">You can use the above template along with the parameter file provided below.</span></span> 

<span data-ttu-id="1b9fc-130">Save and modify the json below as advancedmetricalert.parameters.json for the purpose of this walk through.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-130">Save and modify the json below as advancedmetricalert.parameters.json for the purpose of this walk through.</span></span>

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "alertName": {
            "value": "New Multi-dimensional Metric Alert (Replace with your alert name)"
        },
        "alertDescription": {
            "value": "New multi-dimensional metric alert created via template (Replace with your alert description)"
        },
        "alertSeverity": {
            "value":3
        },
        "isEnabled": {
            "value": true
        },
        "resourceId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/replace-with-resourcegroup-name/providers/Microsoft.Storage/storageAccounts/replace-with-storage-account"
        },
        "criterion1": {
            "value": {
                    "name": "1st criterion",
                    "metricName": "Transactions",
                    "dimensions": [
                        {
                            "name":"ResponseType",
                            "operator": "Include",
                            "values": ["Success"]
                        },
                        {
                            "name":"ApiName",
                            "operator": "Include",
                            "values": ["GetBlob"]
                        }
                    ],
                    "operator": "GreaterThan",
                    "threshold": "5",
                    "timeAggregation": "Total"
                }
        },
        "criterion2": {
            "value":{
                "name": "2nd criterion",
                "metricName": "SuccessE2ELatency",
                "dimensions": [
                    {
                        "name":"ApiName",
                        "operator": "Include",
                        "values": ["GetBlob"]
                    }
                ],
                "operator": "GreaterThan",
                "threshold": "250",
                "timeAggregation": "Average"
            }      
        },          
        "actionGroupId": {
            "value": "/subscriptions/replace-with-subscription-id/resourceGroups/Default-ActivityLogAlerts/providers/Microsoft.Insights/actionGroups/replace-with-actiongroup-name"
        }
    }    
}
```


<span data-ttu-id="1b9fc-131">You can create the metric alert using the template and parameters file using PowerShell or Azure CLI from your current working directory</span><span class="sxs-lookup"><span data-stu-id="1b9fc-131">You can create the metric alert using the template and parameters file using PowerShell or Azure CLI from your current working directory</span></span>

<span data-ttu-id="1b9fc-132">Using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1b9fc-132">Using Azure PowerShell</span></span>
```powershell
Connect-AzureRmAccount

Select-AzureRmSubscription -SubscriptionName <yourSubscriptionName>
 
New-AzureRmResourceGroupDeployment -Name AlertDeployment -ResourceGroupName ResourceGroupofTargetResource `
  -TemplateFile advancedmetricalert.json -TemplateParametersFile advancedmetricalert.parameters.json
```



<span data-ttu-id="1b9fc-133">Using Azure CLI</span><span class="sxs-lookup"><span data-stu-id="1b9fc-133">Using Azure CLI</span></span>
```azurecli
az login

az group deployment create \
    --name AlertDeployment \
    --resource-group ResourceGroupofTargetResource \
    --template-file advancedmetricalert.json \
    --parameters @advancedmetricalert.parameters.json
```

>[!NOTE]
>
> <span data-ttu-id="1b9fc-134">While the metric alert could be created in a different resource group to the target resource, we recommend using the same resource group as your target resource.</span><span class="sxs-lookup"><span data-stu-id="1b9fc-134">While the metric alert could be created in a different resource group to the target resource, we recommend using the same resource group as your target resource.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1b9fc-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="1b9fc-135">Next steps</span></span>
* <span data-ttu-id="1b9fc-136">Read more about [alerts in Azure](monitoring-overview-unified-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="1b9fc-136">Read more about [alerts in Azure](monitoring-overview-unified-alerts.md)</span></span>
* <span data-ttu-id="1b9fc-137">Learn how to [create an action group with Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="1b9fc-137">Learn how to [create an action group with Resource Manager templates](monitoring-create-action-group-with-resource-manager-template.md)</span></span>
