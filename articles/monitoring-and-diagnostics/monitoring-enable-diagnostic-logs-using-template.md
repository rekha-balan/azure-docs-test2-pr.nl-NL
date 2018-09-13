---
title: Automatically enable diagnostic settings using a Resource Manager template
description: Learn how to use a Resource Manager template to create diagnostic settings that will enable you to stream your diagnostic logs to Event Hubs or store them in a storage account.
author: johnkemnetz
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 3/26/2018
ms.author: johnkem
ms.component: ''
ms.openlocfilehash: e8af84467c008f5c576142fa094b2757cfd30387
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44812317"
---
# <a name="automatically-enable-diagnostic-settings-at-resource-creation-using-a-resource-manager-template"></a><span data-ttu-id="a019f-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="a019f-103">Automatically enable Diagnostic Settings at resource creation using a Resource Manager template</span></span>
<span data-ttu-id="a019f-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span><span class="sxs-lookup"><span data-stu-id="a019f-104">In this article we show how you can use an [Azure Resource Manager template](../azure-resource-manager/resource-group-authoring-templates.md) to configure Diagnostic Settings on a resource when it is created.</span></span> <span data-ttu-id="a019f-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span><span class="sxs-lookup"><span data-stu-id="a019f-105">This enables you to automatically start streaming your Diagnostic Logs and metrics to Event Hubs, archiving them in a Storage Account, or sending them to Log Analytics when a resource is created.</span></span>

> [!WARNING]
> <span data-ttu-id="a019f-106">The format of the log data in the storage account will change to JSON Lines on Nov. 1st, 2018.</span><span class="sxs-lookup"><span data-stu-id="a019f-106">The format of the log data in the storage account will change to JSON Lines on Nov. 1st, 2018.</span></span> [<span data-ttu-id="a019f-107">See this article for a description of the impact and how to update your tooling to handle the new format.</span><span class="sxs-lookup"><span data-stu-id="a019f-107">See this article for a description of the impact and how to update your tooling to handle the new format.</span></span>](./monitor-diagnostic-logs-append-blobs.md) 
>
> 

<span data-ttu-id="a019f-108">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span><span class="sxs-lookup"><span data-stu-id="a019f-108">The method for enabling Diagnostic Logs using a Resource Manager template depends on the resource type.</span></span>

* <span data-ttu-id="a019f-109">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#diagnostic-settings).</span><span class="sxs-lookup"><span data-stu-id="a019f-109">**Non-Compute** resources (for example, Network Security Groups, Logic Apps, Automation) use [Diagnostic Settings described in this article](monitoring-overview-of-diagnostic-logs.md#diagnostic-settings).</span></span>
* <span data-ttu-id="a019f-110">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span><span class="sxs-lookup"><span data-stu-id="a019f-110">**Compute** (WAD/LAD-based) resources use the [WAD/LAD configuration file described in this article](../vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md).</span></span>

<span data-ttu-id="a019f-111">In this article we describe how to configure diagnostics using either method.</span><span class="sxs-lookup"><span data-stu-id="a019f-111">In this article we describe how to configure diagnostics using either method.</span></span>

<span data-ttu-id="a019f-112">The basic steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="a019f-112">The basic steps are as follows:</span></span>

1. <span data-ttu-id="a019f-113">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a019f-113">Create a template as a JSON file that describes how to create the resource and enable diagnostics.</span></span>
2. <span data-ttu-id="a019f-114">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="a019f-114">[Deploy the template using any deployment method](../azure-resource-manager/resource-group-template-deploy.md).</span></span>

<span data-ttu-id="a019f-115">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span><span class="sxs-lookup"><span data-stu-id="a019f-115">Below we give an example of the template JSON file you need to generate for non-Compute and Compute resources.</span></span>

## <a name="non-compute-resource-template"></a><span data-ttu-id="a019f-116">Non-Compute resource template</span><span class="sxs-lookup"><span data-stu-id="a019f-116">Non-Compute resource template</span></span>
<span data-ttu-id="a019f-117">For non-Compute resources, you will need to do two things:</span><span class="sxs-lookup"><span data-stu-id="a019f-117">For non-Compute resources, you will need to do two things:</span></span>

1. <span data-ttu-id="a019f-118">Add parameters to the parameters blob for the storage account name, event hub authorization rule ID, and/or Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span><span class="sxs-lookup"><span data-stu-id="a019f-118">Add parameters to the parameters blob for the storage account name, event hub authorization rule ID, and/or Log Analytics workspace ID (enabling archival of Diagnostic Logs in a storage account, streaming of logs to Event Hubs, and/or sending logs to Log Analytics).</span></span>
   
    ```json
    "settingName": {
      "type": "string",
      "metadata": {
        "description": "Name for the diagnostic setting resource. Eg. 'archiveToStorage' or 'forSecurityTeam'."
      }
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "eventHubAuthorizationRuleId": {
      "type": "string",
      "metadata": {
        "description": "Resource ID of the event hub authorization rule for the Event Hubs namespace in which the event hub should be created or streamed to."
      }
    },
    "eventHubName": {
      "type": "string",
      "metadata": {
        "description": "Optional. Name of the event hub within the namespace to which logs are streamed. Without this, an event hub is created for each log category."
      }
    },
    "workspaceId":{
      "type": "string",
      "metadata": {
        "description": "Azure Resource ID of the Log Analytics workspace for the Log Analytics workspace to which logs will be sent."
      }
    }
    ```
2. <span data-ttu-id="a019f-119">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span><span class="sxs-lookup"><span data-stu-id="a019f-119">In the resources array of the resource for which you want to enable Diagnostic Logs, add a resource of type `[resource namespace]/providers/diagnosticSettings`.</span></span>
   
    ```json
    "resources": [
      {
        "type": "providers/diagnosticSettings",
        "name": "[concat('Microsoft.Insights/', parameters('settingName'))]",
        "dependsOn": [
          "[/*resource Id for which Diagnostic Logs will be enabled>*/]"
        ],
        "apiVersion": "2017-05-01-preview",
        "properties": {
          "name": "[parameters('settingName')]",
          "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
          "eventHubAuthorizationRuleId": "[parameters('eventHubAuthorizationRuleId')]",
          "eventHubName": "[parameters('eventHubName')]",
          "workspaceId": "[parameters('workspaceId')]",
          "logs": [ 
            {
              "category": "/* log category name */",
              "enabled": true,
              "retentionPolicy": {
                "days": 0,
                "enabled": false
              }
            }
          ],
          "metrics": [
            {
              "category": "AllMetrics",
              "enabled": true,
              "retentionPolicy": {
                "enabled": false,
                "days": 0
              }
            }
          ]
        }
      }
    ]
    ```

<span data-ttu-id="a019f-120">The properties blob for the Diagnostic Setting follows [the format described in this article](https://docs.microsoft.com/rest/api/monitor/diagnosticsettings/createorupdate).</span><span class="sxs-lookup"><span data-stu-id="a019f-120">The properties blob for the Diagnostic Setting follows [the format described in this article](https://docs.microsoft.com/rest/api/monitor/diagnosticsettings/createorupdate).</span></span> <span data-ttu-id="a019f-121">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="a019f-121">Adding the `metrics` property will enable you to also send resource metrics to these same outputs, provided that [the resource supports Azure Monitor metrics](monitoring-supported-metrics.md).</span></span>

<span data-ttu-id="a019f-122">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span><span class="sxs-lookup"><span data-stu-id="a019f-122">Here is a full example that creates a Logic App and turns on streaming to Event Hubs and storage in a storage account.</span></span>

```json

{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "logicAppName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Logic App that will be created."
      }
    },
    "testUri": {
      "type": "string",
      "defaultValue": "http://azure.microsoft.com/status/feed/"
    },
    "settingName": {
      "type": "string",
      "metadata": {
        "description": "Name of the setting. Name for the diagnostic setting resource. Eg. 'archiveToStorage' or 'forSecurityTeam'."
      }
    },
    "storageAccountName": {
      "type": "string",
      "metadata": {
        "description": "Name of the Storage Account in which Diagnostic Logs should be saved."
      }
    },
    "eventHubAuthorizationRuleId": {
      "type": "string",
      "metadata": {
        "description": "Resource ID of the event hub authorization rule for the Event Hubs namespace in which the event hub should be created or streamed to."
      }
    },
    "eventHubName": {
      "type": "string",
      "metadata": {
        "description": "Optional. Name of the event hub within the namespace to which logs are streamed. Without this, an event hub is created for each log category."
      }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "Log Analytics workspace ID for the Log Analytics workspace to which logs will be sent."
      }
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Logic/workflows",
      "name": "[parameters('logicAppName')]",
      "apiVersion": "2016-06-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "definition": {
          "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      },
      "resources": [
        {
          "type": "providers/diagnosticSettings",
          "name": "[concat('Microsoft.Insights/', parameters('settingName'))]",
          "dependsOn": [
            "[resourceId('Microsoft.Logic/workflows', parameters('logicAppName'))]"
          ],
          "apiVersion": "2017-05-01-preview",
          "properties": {
            "name": "[parameters('settingName')]",
            "storageAccountId": "[resourceId('Microsoft.Storage/storageAccounts', parameters('storageAccountName'))]",
            "eventHubAuthorizationRuleId": "[parameters('eventHubAuthorizationRuleId')]",
            "eventHubName": "[parameters('eventHubName')]",
            "workspaceId": "[parameters('workspaceId')]",
            "logs": [
              {
                "category": "WorkflowRuntime",
                "enabled": true,
                "retentionPolicy": {
                  "days": 0,
                  "enabled": false
                }
              }
            ],
            "metrics": [
              {
                "timeGrain": "PT1M",
                "enabled": true,
                "retentionPolicy": {
                  "enabled": false,
                  "days": 0
                }
              }
            ]
          }
        }
      ],
      "dependsOn": []
    }
  ]
}

```

## <a name="compute-resource-template"></a><span data-ttu-id="a019f-123">Compute resource template</span><span class="sxs-lookup"><span data-stu-id="a019f-123">Compute resource template</span></span>
<span data-ttu-id="a019f-124">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span><span class="sxs-lookup"><span data-stu-id="a019f-124">To enable diagnostics on a Compute resource, for example a Virtual Machine or Service Fabric cluster, you need to:</span></span>

1. <span data-ttu-id="a019f-125">Add the Azure Diagnostics extension to the VM resource definition.</span><span class="sxs-lookup"><span data-stu-id="a019f-125">Add the Azure Diagnostics extension to the VM resource definition.</span></span>
2. <span data-ttu-id="a019f-126">Specify a storage account and/or event hub as a parameter.</span><span class="sxs-lookup"><span data-stu-id="a019f-126">Specify a storage account and/or event hub as a parameter.</span></span>
3. <span data-ttu-id="a019f-127">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span><span class="sxs-lookup"><span data-stu-id="a019f-127">Add the contents of your WADCfg XML file into the XMLCfg property, escaping all XML characters properly.</span></span>

> [!WARNING]
> <span data-ttu-id="a019f-128">This last step can be tricky to get right.</span><span class="sxs-lookup"><span data-stu-id="a019f-128">This last step can be tricky to get right.</span></span> <span data-ttu-id="a019f-129">[See this article](../virtual-machines/extensions/diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span><span class="sxs-lookup"><span data-stu-id="a019f-129">[See this article](../virtual-machines/extensions/diagnostics-template.md#diagnostics-configuration-variables) for an example that splits the Diagnostics Configuration Schema into variables that are escaped and formatted correctly.</span></span>
> 
> 

<span data-ttu-id="a019f-130">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="a019f-130">The entire process, including samples, is described [in this document](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a019f-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="a019f-131">Next steps</span></span>
* [<span data-ttu-id="a019f-132">Read more about Azure Diagnostic Logs</span><span class="sxs-lookup"><span data-stu-id="a019f-132">Read more about Azure Diagnostic Logs</span></span>](monitoring-overview-of-diagnostic-logs.md)
* [<span data-ttu-id="a019f-133">Stream Azure Diagnostic Logs to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="a019f-133">Stream Azure Diagnostic Logs to Event Hubs</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)

