---
title: Create action groups with Resource Manager templates
description: Learn how to create an action group by using an Azure Resource Manager template.
author: dkamstra
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 02/16/2018
ms.author: dukek
ms.component: alerts
ms.openlocfilehash: 9b49d21dad9bb1e48194cc31940c5cd53c909dc0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44794916"
---
# <a name="create-an-action-group-with-a-resource-manager-template"></a><span data-ttu-id="440fa-103">Create an action group with a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="440fa-103">Create an action group with a Resource Manager template</span></span>
<span data-ttu-id="440fa-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span><span class="sxs-lookup"><span data-stu-id="440fa-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure action groups.</span></span> <span data-ttu-id="440fa-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span><span class="sxs-lookup"><span data-stu-id="440fa-105">By using templates, you can automatically set up action groups that can be reused in certain types of alerts.</span></span> <span data-ttu-id="440fa-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="440fa-106">These action groups ensure that all the correct parties are notified when an alert is triggered.</span></span>

<span data-ttu-id="440fa-107">The basic steps are:</span><span class="sxs-lookup"><span data-stu-id="440fa-107">The basic steps are:</span></span>

1. <span data-ttu-id="440fa-108">Create a template as a JSON file that describes how to create the action group.</span><span class="sxs-lookup"><span data-stu-id="440fa-108">Create a template as a JSON file that describes how to create the action group.</span></span>

2. <span data-ttu-id="440fa-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="440fa-109">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

<span data-ttu-id="440fa-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span><span class="sxs-lookup"><span data-stu-id="440fa-110">First, we describe how to create a Resource Manager template for an action group where the action definitions are hard-coded in the template.</span></span> <span data-ttu-id="440fa-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span><span class="sxs-lookup"><span data-stu-id="440fa-111">Second, we describe how to create a template that takes the webhook configuration information as input parameters when the template is deployed.</span></span>

## <a name="resource-manager-templates-for-an-action-group"></a><span data-ttu-id="440fa-112">Resource Manager templates for an action group</span><span class="sxs-lookup"><span data-stu-id="440fa-112">Resource Manager templates for an action group</span></span>

<span data-ttu-id="440fa-113">To create an action group using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span><span class="sxs-lookup"><span data-stu-id="440fa-113">To create an action group using a Resource Manager template, you create a resource of the type `Microsoft.Insights/actionGroups`.</span></span> <span data-ttu-id="440fa-114">Then you fill in all related properties.</span><span class="sxs-lookup"><span data-stu-id="440fa-114">Then you fill in all related properties.</span></span> <span data-ttu-id="440fa-115">Here are two sample templates that create an action group.</span><span class="sxs-lookup"><span data-stu-id="440fa-115">Here are two sample templates that create an action group.</span></span>

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
      "apiVersion": "2018-03-01",
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
        "description": "Webhook receiver service Name."
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
      "apiVersion": "2018-03-01",
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


## <a name="next-steps"></a><span data-ttu-id="440fa-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="440fa-116">Next steps</span></span>
* <span data-ttu-id="440fa-117">Learn more about [action groups](monitoring-action-groups.md).</span><span class="sxs-lookup"><span data-stu-id="440fa-117">Learn more about [action groups](monitoring-action-groups.md).</span></span>
* <span data-ttu-id="440fa-118">Learn more about [alerts](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="440fa-118">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
* <span data-ttu-id="440fa-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="440fa-119">Learn how to add [alerts by using a Resource Manager template](monitoring-create-activity-log-alerts-with-resource-manager-template.md).</span></span>
