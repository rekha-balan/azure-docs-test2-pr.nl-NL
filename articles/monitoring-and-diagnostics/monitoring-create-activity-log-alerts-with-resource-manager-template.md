---
title: Create an activity log alert with a Resource Manager template
description: Get notified when your Azure resources are created.
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 07/06/2017
ms.author: ancav
ms.component: alerts
ms.openlocfilehash: a1e28f08231ae1fbef3e0d0306e986c1dc9d1d1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791471"
---
# <a name="create-an-activity-log-alert-with-a-resource-manager-template"></a><span data-ttu-id="282e3-103">Create an activity log alert with a Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="282e3-103">Create an activity log alert with a Resource Manager template</span></span>
<span data-ttu-id="282e3-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span><span class="sxs-lookup"><span data-stu-id="282e3-104">This article shows you how to use an [Azure Resource Manager template](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authoring-templates) to configure activity log alerts.</span></span> <span data-ttu-id="282e3-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span><span class="sxs-lookup"><span data-stu-id="282e3-105">By using templates, you can easily set up many alerts that activate based on specific activity log event conditions as part of your automated deployment process.</span></span>

<span data-ttu-id="282e3-106">The basic steps are:</span><span class="sxs-lookup"><span data-stu-id="282e3-106">The basic steps are:</span></span>

1. <span data-ttu-id="282e3-107">Create a template as a JSON file that describes how to create the activity log alert.</span><span class="sxs-lookup"><span data-stu-id="282e3-107">Create a template as a JSON file that describes how to create the activity log alert.</span></span>

2. <span data-ttu-id="282e3-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="282e3-108">Deploy the template by using [any deployment method](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span>

## <a name="resource-manager-template-for-an-activity-log-alert"></a><span data-ttu-id="282e3-109">Resource Manager template for an activity log alert</span><span class="sxs-lookup"><span data-stu-id="282e3-109">Resource Manager template for an activity log alert</span></span>
<span data-ttu-id="282e3-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span><span class="sxs-lookup"><span data-stu-id="282e3-110">To create an activity log alert by using a Resource Manager template, you create a resource of the type `microsoft.insights/activityLogAlerts`.</span></span> <span data-ttu-id="282e3-111">Then you fill in all related properties.</span><span class="sxs-lookup"><span data-stu-id="282e3-111">Then you fill in all related properties.</span></span> <span data-ttu-id="282e3-112">Here's a template that creates an activity log alert.</span><span class="sxs-lookup"><span data-stu-id="282e3-112">Here's a template that creates an activity log alert.</span></span>

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
      "apiVersion": "2017-04-01",
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

<span data-ttu-id="282e3-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span><span class="sxs-lookup"><span data-stu-id="282e3-113">Visit our [Azure Quickstart gallery](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Insights) for some examples of activity log alert templates.</span></span>

> [!NOTE]

> <span data-ttu-id="282e3-114">You can also create activity log alert rules using the enhanced user experience in Monitor > [Alerts (Preview)](monitoring-overview-unified-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="282e3-114">You can also create activity log alert rules using the enhanced user experience in Monitor > [Alerts (Preview)](monitoring-overview-unified-alerts.md).</span></span> <span data-ttu-id="282e3-115">For more information on how to create these, see [this article](monitoring-activity-log-alerts-new-experience.md).</span><span class="sxs-lookup"><span data-stu-id="282e3-115">For more information on how to create these, see [this article](monitoring-activity-log-alerts-new-experience.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="282e3-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="282e3-116">Next steps</span></span>
- <span data-ttu-id="282e3-117">Learn more about [alerts](monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="282e3-117">Learn more about [alerts](monitoring-overview-alerts.md).</span></span>
- <span data-ttu-id="282e3-118">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="282e3-118">Learn how to add [action groups by using a Resource Manager template](monitoring-create-action-group-with-resource-manager-template.md).</span></span>
- <span data-ttu-id="282e3-119">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span><span class="sxs-lookup"><span data-stu-id="282e3-119">Learn how to [create an activity log alert to monitor all autoscale engine operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-alert).</span></span>
- <span data-ttu-id="282e3-120">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span><span class="sxs-lookup"><span data-stu-id="282e3-120">Learn how to [create an activity log alert to monitor all failed autoscale scale-in/scale-out operations on your subscription](https://github.com/Azure/azure-quickstart-templates/tree/master/monitor-autoscale-failed-alert).</span></span>
