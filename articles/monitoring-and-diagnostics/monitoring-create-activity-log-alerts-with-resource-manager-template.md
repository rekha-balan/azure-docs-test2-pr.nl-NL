---
title: Create an activity log alert with a Resource Manager Template  | Microsoft Docs
description: Get notified when your Azure resources are created.
author: anirudhcavale
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 239b8fe2a7724bb34e7060c90af73825e61d8398
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662899"
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a>Create an activity log alert with a Resource Manager Template
This article shows how you can use an [Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts. This enables you to automatically set up alerts on your resources when they are created as part of your automated deployment process.

The basic steps are as follows:

1.  Create a template as a JSON file that describes how to create the activity log alert.
2.  [Deploy the template using any deployment method.](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)

Below we describe how to create a Resource Manager template first for an activity log alert alone, then for an activity log alert during the creation of another resource.

## <a name="resource-manager-template-for-an-activity-log-alert"></a>Resource Manager template for an activity log alert
To create an activity log alert using a Resource Manager template, you create a resource of type `microsoft.insights/activityLogAlerts` and fill in all related properties. Below is a template that creates an activity log alert.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "activityLogAlertName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Activity log alert."
      }
    },
    "activityLogAlertEnabled": {
      "type": "bool",
      "defaultValue": true,
      "metadata": {
        "description": "Indicates whether or not the alert is enabled."
      }
    },
    "actionGroupResourceId": {
      "type": "string",
      "metadata": {
        "description": "Resource Id for the Action group."
      }
    }
  },
  "resources": [   
    {
      "type": "Microsoft.Insights/activityLogAlerts",
      "apiVersion": "2017-03-01-preview",
      "name": "[parameters('activityLogAlertName')]",      
      "location": "Global",
      "properties": {
        "enabled": "[parameters('activityLogAlertEnabled')]",
        "scopes": [
            "[subscription().id]"
        ],        
        "condition": {
          "allOf": [
            {
              "field": "category",
              "equals": "Administrative"
            },
            {
              "field": "operationName",
              "equals": "Microsoft.Resources/deployments/write"
            },
            {
              "field": "resourceType",
              "equals": "Microsoft.Resources/deployments"
            }
          ] 
        },
        "actions": {
          "actionGroups": 
          [
            {
              "actionGroupId": "[parameters('actionGroupResourceId')]"
            }
          ]
        }
      }
    }
  ]
}
```

## <a name="next-steps"></a>Next Steps
Learn more about [Alerts](monitoring-overview-alerts.md)  
How to add [action groups using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md)
