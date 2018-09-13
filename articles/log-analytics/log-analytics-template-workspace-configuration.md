---
title: Use Azure Resource Manager templates to Create and Configure a Log Analytics Workspace | Microsoft Docs
description: You can use Azure Resource Manager templates to create and configure Log Analytics workspaces.
services: log-analytics
documentationcenter: ''
author: richrundmsft
manager: jochan
editor: ''
ms.assetid: d21ca1b0-847d-4716-bb30-2a8c02a606aa
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: json
ms.topic: article
ms.date: 11/01/2016
ms.author: richrund
ms.openlocfilehash: f392b3c0ab6b4d2e133d59766732188ce97c2f3e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552385"
---
# <a name="manage-log-analytics-using-azure-resource-manager-templates"></a><span data-ttu-id="e5800-103">Manage Log Analytics using Azure Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="e5800-103">Manage Log Analytics using Azure Resource Manager templates</span></span>
<span data-ttu-id="e5800-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to create and configure Log Analytics workspaces.</span><span class="sxs-lookup"><span data-stu-id="e5800-104">You can use [Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md) to create and configure Log Analytics workspaces.</span></span> <span data-ttu-id="e5800-105">Examples of the tasks you can perform with templates include:</span><span class="sxs-lookup"><span data-stu-id="e5800-105">Examples of the tasks you can perform with templates include:</span></span>

* <span data-ttu-id="e5800-106">Create a workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-106">Create a workspace</span></span>
* <span data-ttu-id="e5800-107">Add a solution</span><span class="sxs-lookup"><span data-stu-id="e5800-107">Add a solution</span></span>
* <span data-ttu-id="e5800-108">Create saved searches</span><span class="sxs-lookup"><span data-stu-id="e5800-108">Create saved searches</span></span>
* <span data-ttu-id="e5800-109">Create a computer group</span><span class="sxs-lookup"><span data-stu-id="e5800-109">Create a computer group</span></span>
* <span data-ttu-id="e5800-110">Enable collection of IIS logs from computers with the Windows agent installed</span><span class="sxs-lookup"><span data-stu-id="e5800-110">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
* <span data-ttu-id="e5800-111">Collect performance counters from Linux and Windows computers</span><span class="sxs-lookup"><span data-stu-id="e5800-111">Collect performance counters from Linux and Windows computers</span></span>
* <span data-ttu-id="e5800-112">Collect events from syslog on Linux computers</span><span class="sxs-lookup"><span data-stu-id="e5800-112">Collect events from syslog on Linux computers</span></span> 
* <span data-ttu-id="e5800-113">Collect events from Windows event logs</span><span class="sxs-lookup"><span data-stu-id="e5800-113">Collect events from Windows event logs</span></span>
* <span data-ttu-id="e5800-114">Collect custom event logs</span><span class="sxs-lookup"><span data-stu-id="e5800-114">Collect custom event logs</span></span>
* <span data-ttu-id="e5800-115">Add the log analytics agent to an Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="e5800-115">Add the log analytics agent to an Azure virtual machine</span></span>
* <span data-ttu-id="e5800-116">Configure log analytics to index data collected using Azure diagnostics</span><span class="sxs-lookup"><span data-stu-id="e5800-116">Configure log analytics to index data collected using Azure diagnostics</span></span>

<span data-ttu-id="e5800-117">This article provides a template samples that illustrate some of the configuration that you can perform from templates.</span><span class="sxs-lookup"><span data-stu-id="e5800-117">This article provides a template samples that illustrate some of the configuration that you can perform from templates.</span></span>

## <a name="create-and-configure-a-log-analytics-workspace"></a><span data-ttu-id="e5800-118">Create and configure a Log Analytics Workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-118">Create and configure a Log Analytics Workspace</span></span>
<span data-ttu-id="e5800-119">The following template sample illustrates how to:</span><span class="sxs-lookup"><span data-stu-id="e5800-119">The following template sample illustrates how to:</span></span>

1. <span data-ttu-id="e5800-120">Create a workspace, including setting data retention</span><span class="sxs-lookup"><span data-stu-id="e5800-120">Create a workspace, including setting data retention</span></span>
2. <span data-ttu-id="e5800-121">Add solutions to the workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-121">Add solutions to the workspace</span></span>
3. <span data-ttu-id="e5800-122">Create saved searches</span><span class="sxs-lookup"><span data-stu-id="e5800-122">Create saved searches</span></span>
4. <span data-ttu-id="e5800-123">Create a computer group</span><span class="sxs-lookup"><span data-stu-id="e5800-123">Create a computer group</span></span>
5. <span data-ttu-id="e5800-124">Enable collection of IIS logs from computers with the Windows agent installed</span><span class="sxs-lookup"><span data-stu-id="e5800-124">Enable collection of IIS logs from computers with the Windows agent installed</span></span>
6. <span data-ttu-id="e5800-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span><span class="sxs-lookup"><span data-stu-id="e5800-125">Collect Logical Disk perf counters from Linux computers (% Used Inodes; Free Megabytes; % Used Space; Disk Transfers/sec; Disk Reads/sec; Disk Writes/sec)</span></span>
7. <span data-ttu-id="e5800-126">Collect syslog events from Linux computers</span><span class="sxs-lookup"><span data-stu-id="e5800-126">Collect syslog events from Linux computers</span></span>
8. <span data-ttu-id="e5800-127">Collect Error and Warning events from the Application Event Log from Windows computers</span><span class="sxs-lookup"><span data-stu-id="e5800-127">Collect Error and Warning events from the Application Event Log from Windows computers</span></span>
9. <span data-ttu-id="e5800-128">Collect Memory Available Mbytes performance counter from Windows computers</span><span class="sxs-lookup"><span data-stu-id="e5800-128">Collect Memory Available Mbytes performance counter from Windows computers</span></span>
10. <span data-ttu-id="e5800-129">Collect a custom log</span><span class="sxs-lookup"><span data-stu-id="e5800-129">Collect a custom log</span></span> 
11. <span data-ttu-id="e5800-130">Collect IIS logs and Windows Event logs written by Azure diagnostics to a storage account</span><span class="sxs-lookup"><span data-stu-id="e5800-130">Collect IIS logs and Windows Event logs written by Azure diagnostics to a storage account</span></span>

```
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "workspaceName": {
      "type": "string",
      "metadata": {
        "description": "workspaceName"
      }
    },
    "serviceTier": {
      "type": "string",
      "allowedValues": [
        "Free",
        "Standalone",
        "PerNode"
      ],
      "metadata": {
        "description": "Service Tier: Free, Standalone, or PerNode"
    }
      },
    "dataRetention": {
      "type": "int",
      "defaultValue": 30,
      "minValue": 7,
      "maxValue": 730,
      "metadata": {
        "description": "Number of days of retention. Free plans can only have 7 days, Standalone and OMS plans include 30 days for free"
      }
    },
    "location": {
      "type": "string",
      "allowedValues": [
        "East US",
        "West Europe",
        "Southeast Asia",
        "Australia Southeast"
      ]
    },
    "applicationDiagnosticsStorageAccountName": {
        "type": "string",
        "metadata": {
          "description": "Name of the storage account with Azure diagnostics output"
        }
    },
    "applicationDiagnosticsStorageAccountResourceGroup": {
        "type": "string",
        "metadata": {
          "description": "The resource group name containing the storage account with Azure diagnostics output"
        }
    }
  },
  "variables": {
    "Updates": {
      "Name": "[Concat('Updates', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "Updates"
    },
    "AntiMalware": {
      "Name": "[concat('AntiMalware', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "AntiMalware"
    },
    "SQLAssessment": {
      "Name": "[Concat('SQLAssessment', '(', parameters('workspaceName'), ')')]",
      "GalleryName": "SQLAssessment"
    },
    "diagnosticsStorageAccount": "[resourceId(parameters('applicationDiagnosticsStorageAccountResourceGroup'), 'Microsoft.Storage/storageAccounts', parameters('applicationDiagnosticsStorageAccountName'))]"
  },
  "resources": [
    {
      "apiVersion": "2015-11-01-preview",
      "type": "Microsoft.OperationalInsights/workspaces",
      "name": "[parameters('workspaceName')]",
      "location": "[parameters('location')]",
      "properties": {
        "sku": {
          "Name": "[parameters('serviceTier')]"
        },
    "retentionInDays": "[parameters('dataRetention')]"
      },
      "resources": [
        {
          "apiVersion": "2015-11-01-preview",
          "name": "VMSS Queries2",
          "type": "savedSearches",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "Category": "VMSS",
            "ETag": "*",
            "DisplayName": "VMSS Instance Count",
            "Query": "Type:Event Source=ServiceFabricNodeBootstrapAgent | dedup Computer | measure count () by Computer",
            "Version": 1
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsEvent1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsEvent",
          "properties": {
            "eventLogName": "Application",
            "eventTypes": [
              {
                "eventType": "Error"
              },
              {
                "eventType": "Warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleWindowsPerfCounter1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "WindowsPerformanceCounter",
          "properties": {
            "objectName": "Memory",
            "instanceName": "*",
            "intervalSeconds": 10,
            "counterName": "Available MBytes"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleIISLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "IISLogs",
          "properties": {
            "state": "OnPremiseEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslog",
          "properties": {
            "syslogName": "kern",
            "syslogSeverities": [
              {
                "severity": "emerg"
              },
              {
                "severity": "alert"
              },
              {
                "severity": "crit"
              },
              {
                "severity": "err"
              },
              {
                "severity": "warning"
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleSyslogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxSyslogCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerf1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceObject",
          "properties": {
            "performanceCounters": [
              {
                "counterName": "% Used Inodes"
              },
              {
                "counterName": "Free Megabytes"
              },
              {
                "counterName": "% Used Space"
              },
              {
                "counterName": "Disk Transfers/sec"
              },
              {
                "counterName": "Disk Reads/sec"
              },
              {
                "counterName": "Disk Writes/sec"
              }
            ],
            "objectName": "Logical Disk",
            "instanceName": "*",
            "intervalSeconds": 10
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleLinuxPerfCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "LinuxPerformanceCollection",
          "properties": {
            "state": "Enabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLog1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLog",
          "properties": {
            "customLogName": "sampleCustomLog1",
            "description": "test custom log datasources",
            "inputs": [
              {
                "location": {
                  "fileSystemLocations": {
                    "windowsFileTypeLogPaths": [ "e:\\iis5\\*.log" ],
                    "linuxFileTypeLogPaths": [ "/var/logs" ]
                  }
                },
                "recordDelimiter": {
                  "regexDelimiter": {
                    "pattern": "\\n",
                    "matchIndex": 0,
                    "matchIndexSpecified": true,
                    "numberedGroup": null
                  }
                }
              }
            ],
            "extractions": [
              {
                "extractionName": "TimeGenerated",
                "extractionType": "DateTime",
                "extractionProperties": {
                  "dateTimeExtraction": {
                    "regex": null,
                    "joinStringRegex": null
                  }
                }
              }
            ]
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "type": "datasources",
          "name": "sampleCustomLogCollection1",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "kind": "CustomLogCollection",
          "properties": {
            "state": "LinuxLogsEnabled"
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "name": "[concat(parameters('applicationDiagnosticsStorageAccountName'),parameters('workspaceName'))]",
          "type": "storageinsightconfigs",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "containers": [ 
              "wad-iis-logfiles" 
            ],
            "tables": [
              "WADWindowsEventLogsTable"
            ],
            "storageAccount": {
              "id": "[variables('diagnosticsStorageAccount')]",
              "key": "[listKeys(variables('diagnosticsStorageAccount'),'2015-06-15').key1]"
            }
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('Updates').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('Updates').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('Updates').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('Updates').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('AntiMalware').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('AntiMalware').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('AntiMalware').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('AntiMalware').GalleryName)]",
            "promotionCode": ""
          }
        },
        {
          "apiVersion": "2015-11-01-preview",
          "location": "[parameters('location')]",
          "name": "[variables('SQLAssessment').Name]",
          "type": "Microsoft.OperationsManagement/solutions",
          "id": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', resourceGroup().name, '/providers/Microsoft.OperationsManagement/solutions/', variables('SQLAssessment').Name)]",
          "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          ],
          "properties": {
            "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'))]"
          },
          "plan": {
            "name": "[variables('SQLAssessment').Name]",
            "publisher": "Microsoft",
            "product": "[Concat('OMSGallery/', variables('SQLAssessment').GalleryName)]",
            "promotionCode": ""
          }
        }
      ]
    }
  ],
  "outputs": {
    "workspaceOutput": {
      "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-11-01-preview')]",
      "type": "object"
    }
  }
}

```
### <a name="deploying-the-sample-template"></a><span data-ttu-id="e5800-131">Deploying the sample template</span><span class="sxs-lookup"><span data-stu-id="e5800-131">Deploying the sample template</span></span>
<span data-ttu-id="e5800-132">To deploy the sample template:</span><span class="sxs-lookup"><span data-stu-id="e5800-132">To deploy the sample template:</span></span>

1. <span data-ttu-id="e5800-133">Save the attached sample in a file, for example `azuredeploy.json`</span><span class="sxs-lookup"><span data-stu-id="e5800-133">Save the attached sample in a file, for example `azuredeploy.json`</span></span> 
2. <span data-ttu-id="e5800-134">Edit the template to have the configuration you want</span><span class="sxs-lookup"><span data-stu-id="e5800-134">Edit the template to have the configuration you want</span></span>
3. <span data-ttu-id="e5800-135">Use PowerShell or the command line to deploy the template</span><span class="sxs-lookup"><span data-stu-id="e5800-135">Use PowerShell or the command line to deploy the template</span></span>

#### <a name="powershell"></a><span data-ttu-id="e5800-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e5800-136">PowerShell</span></span>
`New-AzureRmResourceGroupDeployment -Name <deployment-name> -ResourceGroupName <resource-group-name> -TemplateFile azuredeploy.json`

#### <a name="command-line"></a><span data-ttu-id="e5800-137">Command line</span><span class="sxs-lookup"><span data-stu-id="e5800-137">Command line</span></span>
```
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> --TemplateFile azuredeploy.json
```


## <a name="example-resource-manager-templates"></a><span data-ttu-id="e5800-138">Example Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="e5800-138">Example Resource Manager templates</span></span>
<span data-ttu-id="e5800-139">The Azure quickstart template gallery includes several templates for Log Analytics, including:</span><span class="sxs-lookup"><span data-stu-id="e5800-139">The Azure quickstart template gallery includes several templates for Log Analytics, including:</span></span>

* [<span data-ttu-id="e5800-140">Deploy a virtual machine running Windows with the Log Analytics VM extension</span><span class="sxs-lookup"><span data-stu-id="e5800-140">Deploy a virtual machine running Windows with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-windows-vm/)
* [<span data-ttu-id="e5800-141">Deploy a virtual machine running Linux with the Log Analytics VM extension</span><span class="sxs-lookup"><span data-stu-id="e5800-141">Deploy a virtual machine running Linux with the Log Analytics VM extension</span></span>](https://azure.microsoft.com/documentation/templates/201-oms-extension-ubuntu-vm/)
* [<span data-ttu-id="e5800-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-142">Monitor Azure Site Recovery using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/asr-oms-monitoring/)
* [<span data-ttu-id="e5800-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-143">Monitor Azure Web Apps using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-webappazure-oms-monitoring/)
* [<span data-ttu-id="e5800-144">Monitor SQL Azure using an existing Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-144">Monitor SQL Azure using an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/101-sqlazure-oms-monitoring/)
* [<span data-ttu-id="e5800-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span><span class="sxs-lookup"><span data-stu-id="e5800-145">Deploy a Service Fabric cluster and monitor it with an existing Log Analytics workspace</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-oms/)
* [<span data-ttu-id="e5800-146">Deploy a Service Fabric cluster and create a Log Analytics workspace to monitor it</span><span class="sxs-lookup"><span data-stu-id="e5800-146">Deploy a Service Fabric cluster and create a Log Analytics workspace to monitor it</span></span>](https://azure.microsoft.com/documentation/templates/service-fabric-vmss-oms/)

## <a name="next-steps"></a><span data-ttu-id="e5800-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5800-147">Next steps</span></span>
* [<span data-ttu-id="e5800-148">Deploy agents into Azure VMs using Resource Manager templates</span><span class="sxs-lookup"><span data-stu-id="e5800-148">Deploy agents into Azure VMs using Resource Manager templates</span></span>](log-analytics-azure-vm-extension.md)

