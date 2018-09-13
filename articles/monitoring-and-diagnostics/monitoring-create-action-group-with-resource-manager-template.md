---
title: Create Action Groups with Resource Manager Templates | Microsoft Docs
description: Action groups allow you to notify email, SMS or call webhooks when certain events occur.
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
ms.openlocfilehash: 2dd7b14f1466fa7244a2af2c030d8b794658aaad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662406"
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="7222a-103">Create an action group with a Resource Manager Template</span><span class="sxs-lookup"><span data-stu-id="7222a-103">Create an action group with a Resource Manager Template</span></span>
<span data-ttu-id="7222a-104">This article shows how you can use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span><span class="sxs-lookup"><span data-stu-id="7222a-104">This article shows how you can use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="7222a-105">Templates enable you to automatically set up action groups on your resources when they are created to ensure that all the correct parties are notified when an alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="7222a-105">Templates enable you to automatically set up action groups on your resources when they are created to ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="7222a-106">The basic steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="7222a-106">The basic steps are as follows:</span></span>

1.  <span data-ttu-id="7222a-107">Create a template as a JSON file that describes how to create the action group.</span><span class="sxs-lookup"><span data-stu-id="7222a-107">Create a template as a JSON file that describes how to create the action group.</span></span>
2.  [<span data-ttu-id="7222a-108">Deploy the template using any deployment method.</span><span class="sxs-lookup"><span data-stu-id="7222a-108">Deploy the template using any deployment method.</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)

<span data-ttu-id="7222a-109">Below we describe how to create a Resource Manager template first for an action group alone, then for an action group during the creation of another resource.</span><span class="sxs-lookup"><span data-stu-id="7222a-109">Below we describe how to create a Resource Manager template first for an action group alone, then for an action group during the creation of another resource.</span></span>

## <a name="resource-manager-template-for-an-action-group"></a><span data-ttu-id="7222a-110">Resource Manager template for an action group</span><span class="sxs-lookup"><span data-stu-id="7222a-110">Resource Manager template for an action group</span></span>

<span data-ttu-id="7222a-111">To create an action group using a Resource Manager template, you create a resource of type `Microsoft.Insights/actionGroups` and fill in all related properties.</span><span class="sxs-lookup"><span data-stu-id="7222a-111">To create an action group using a Resource Manager template, you create a resource of type `Microsoft.Insights/actionGroups` and fill in all related properties.</span></span> <span data-ttu-id="7222a-112">Following are a couple sample templates that create an action group.</span><span class="sxs-lookup"><span data-stu-id="7222a-112">Following are a couple sample templates that create an action group.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    }
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-03-01-preview",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
          {
            "name": "contosoSMS",
            "countryCode": "1",
            "phoneNumber": "5555551212"
          },
          {
            "name": "contosoSMS2",
            "countryCode": "1",
            "phoneNumber": "5555552121"
          }
        ],
        "emailReceivers": [
          {
            "name": "contosoEmail",
            "emailAddress": "devops@contoso.com"
          },
          {
            "name": "contosoEmail2",
            "emailAddress": "devops2@contoso.com"
          }
        ],
        "webhookReceivers": [
          {
            "name": "contosoHook",
            "serviceUri": "http://requestb.in/1bq62iu1"
          },
          {
            "name": "contosoHook2",
            "serviceUri": "http://requestb.in/1bq62iu2"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "actionGroupName": {
      "type": "string",
      "metadata": {
        "description": "Unique name (within the Resource Group) for the Action group."
      }
    },
    "actionGroupShortName": {
      "type": "string",
      "metadata": {
        "description": "Short name (maximum 12 characters) for the Action group."
      }
    },
    "webhookReceiverName": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    },    
    "webhookServiceUri": {
      "type": "string",
      "metadata": {
        "description": "Webhook receiver service URI."
      }
    }    
  },
  "resources": [
    {
      "type": "Microsoft.Insights/actionGroups",
      "apiVersion": "2017-03-01-preview",
      "name": "[parameters('actionGroupName')]",
      "location": "Global",
      "properties": {
        "groupShortName": "[parameters('actionGroupShortName')]",
        "enabled": true,
        "smsReceivers": [
        ],
        "emailReceivers": [
        ],
        "webhookReceivers": [
          {
            "name": "[parameters('webhookReceiverName')]",
            "serviceUri": "[parameters('webhookServiceUri')]"
          }
        ]
      }
    }
  ],
  "outputs":{
      "actionGroupResourceId":{
          "type":"string",
          "value":"[resourceId('Microsoft.Insights/actionGroups',parameters('actionGroupName'))]"
      }
  }
}
```


## <a name="next-steps"></a><span data-ttu-id="7222a-113">Next Steps</span><span class="sxs-lookup"><span data-stu-id="7222a-113">Next Steps</span></span>
<span data-ttu-id="7222a-114">Learn more about [Action Groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="7222a-114">Learn more about [Action Groups](monitoring-action-groups.md)</span></span>  
<span data-ttu-id="7222a-115">Learn more about [Alerts](monitoring-overview-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="7222a-115">Learn more about [Alerts](monitoring-overview-alerts.md)</span></span>  
<span data-ttu-id="7222a-116">How to add [Alerts using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span><span class="sxs-lookup"><span data-stu-id="7222a-116">How to add [Alerts using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md)</span></span>
