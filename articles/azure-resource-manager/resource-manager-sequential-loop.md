---
title: Sequential looping in Azure templates | Microsoft Docs
description: Describes how to extend the functionality of Azure Resource Manager templates to implement sequential looping when deploying multiple instances of a resource type.
services: guidance, azure-resource-manager
documentationcenter: na
author: petertaylor9999
manager: christb
editor: ''
ms.service: guidance
ms.topic: article
ms.date: 04/18/2017
ms.author: petertay
ms.openlocfilehash: 75ed40d010a58a80082a68832505ad54809f4282
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563865"
---
# <a name="patterns-for-extending-the-functionality-of-azure-resource-manager-templates---sequential-looping"></a><span data-ttu-id="6f695-103">Patterns for extending the functionality of Azure Resource Manager templates - Sequential Looping</span><span class="sxs-lookup"><span data-stu-id="6f695-103">Patterns for extending the functionality of Azure Resource Manager templates - Sequential Looping</span></span>

<span data-ttu-id="6f695-104">Azure Resource Manager templates support the deployment of a group of similar resources via a copy loop.</span><span class="sxs-lookup"><span data-stu-id="6f695-104">Azure Resource Manager templates support the deployment of a group of similar resources via a copy loop.</span></span> <span data-ttu-id="6f695-105">A copy loop in a resource object can be used to iterate an array of strings that are then used to generate unique names for the resources.</span><span class="sxs-lookup"><span data-stu-id="6f695-105">A copy loop in a resource object can be used to iterate an array of strings that are then used to generate unique names for the resources.</span></span> <span data-ttu-id="6f695-106">A copy loop in the resource object can also be used to iterate over an array of variables that describe the resource.</span><span class="sxs-lookup"><span data-stu-id="6f695-106">A copy loop in the resource object can also be used to iterate over an array of variables that describe the resource.</span></span>

<span data-ttu-id="6f695-107">These patterns all work well, but they only work well when there are no dependencies between each member of the group.</span><span class="sxs-lookup"><span data-stu-id="6f695-107">These patterns all work well, but they only work well when there are no dependencies between each member of the group.</span></span> <span data-ttu-id="6f695-108">During an iteration loop, Resource Manager attempts to deploy resources in parallel.</span><span class="sxs-lookup"><span data-stu-id="6f695-108">During an iteration loop, Resource Manager attempts to deploy resources in parallel.</span></span> <span data-ttu-id="6f695-109">If a first resource depends on a second, the deployment may fail if Resource Manager deploys the second resource before the first resource.</span><span class="sxs-lookup"><span data-stu-id="6f695-109">If a first resource depends on a second, the deployment may fail if Resource Manager deploys the second resource before the first resource.</span></span>

<span data-ttu-id="6f695-110">The real problem is that Resource Manager does not currently support `dependsOn` within an iteration loop.</span><span class="sxs-lookup"><span data-stu-id="6f695-110">The real problem is that Resource Manager does not currently support `dependsOn` within an iteration loop.</span></span> <span data-ttu-id="6f695-111">However, this functionality can be implemented using existing Resource Manager functionality and some creative resource naming.</span><span class="sxs-lookup"><span data-stu-id="6f695-111">However, this functionality can be implemented using existing Resource Manager functionality and some creative resource naming.</span></span> 

## <a name="sequential-looping-pattern"></a><span data-ttu-id="6f695-112">Sequential looping pattern</span><span class="sxs-lookup"><span data-stu-id="6f695-112">Sequential looping pattern</span></span>

<span data-ttu-id="6f695-113">The pattern is as follows: a first resource is named using a concatenation of a name prefix and `0`, or, whatever the first index of the loop is.</span><span class="sxs-lookup"><span data-stu-id="6f695-113">The pattern is as follows: a first resource is named using a concatenation of a name prefix and `0`, or, whatever the first index of the loop is.</span></span> <span data-ttu-id="6f695-114">A second resource includes a copy loop, and in the copy loop the next resource name is a concatenation of the name prefix and the result of the `copyIndex(1)` function, which adds 1 to the current `copyIndex()`.</span><span class="sxs-lookup"><span data-stu-id="6f695-114">A second resource includes a copy loop, and in the copy loop the next resource name is a concatenation of the name prefix and the result of the `copyIndex(1)` function, which adds 1 to the current `copyIndex()`.</span></span> <span data-ttu-id="6f695-115">The second resource also includes a `dependsOn` element that references the concatenation of the name prefix and the result of the `copyIndex()` function.</span><span class="sxs-lookup"><span data-stu-id="6f695-115">The second resource also includes a `dependsOn` element that references the concatenation of the name prefix and the result of the `copyIndex()` function.</span></span> <span data-ttu-id="6f695-116">This approach creates a `dependsOn` relationship from the next resource back to the previous resource.</span><span class="sxs-lookup"><span data-stu-id="6f695-116">This approach creates a `dependsOn` relationship from the next resource back to the previous resource.</span></span> <span data-ttu-id="6f695-117">Resource Manager waits to deploy the next resource until the previous resource has deployed.</span><span class="sxs-lookup"><span data-stu-id="6f695-117">Resource Manager waits to deploy the next resource until the previous resource has deployed.</span></span>

<span data-ttu-id="6f695-118">The following template demonstrates this pattern.</span><span class="sxs-lookup"><span data-stu-id="6f695-118">The following template demonstrates this pattern.</span></span> <span data-ttu-id="6f695-119">The Microsoft.Resources/deployments resource type is just a nested template that doesn't actually deploy anything.</span><span class="sxs-lookup"><span data-stu-id="6f695-119">The Microsoft.Resources/deployments resource type is just a nested template that doesn't actually deploy anything.</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "numberToDeploy": {
      "type": "int",
      "minValue": 2,
      "defaultValue": 5
    }
  },
  "variables": {
    "count": "[sub(parameters('numberToDeploy'), 1)]"
  },
  "resources": [
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "loop-0",
      "properties": {
        "mode": "Incremental",
        "parameters": {},
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
            "collection": {
              "type": "string",
              "value": "loop-0 "
            }
          }
        }
      }
    },
    {
      "apiVersion": "2015-01-01",
      "type": "Microsoft.Resources/deployments",
      "name": "[concat('loop-', copyIndex(1))]",
      "dependsOn": [
        "[concat('loop-', copyIndex())]"
      ],
      "copy": {
        "name": "iterator",
        "count": "[variables('count')]"
      },
      "properties": {
        "mode": "Incremental",
        "template": {
          "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {},
          "variables": {},
          "resources": [],
          "outputs": {
            "collection": {
              "type": "string",
              "value": "[concat(reference(concat('loop-',copyIndex())).outputs.collection.value,'loop-',copyIndex(1), ' ')]"
            }
          }
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference(concat('loop-',variables('count'))).outputs.collection.value]"
    }
  }
}

```
<span data-ttu-id="6f695-120">In this template, the first resource object is named `loop-0`.</span><span class="sxs-lookup"><span data-stu-id="6f695-120">In this template, the first resource object is named `loop-0`.</span></span> <span data-ttu-id="6f695-121">Then, in the second resource object, the next resource name is a concatenation of the word `loop-` and the result of the `copyIndex(1)` function: `loop-1`.</span><span class="sxs-lookup"><span data-stu-id="6f695-121">Then, in the second resource object, the next resource name is a concatenation of the word `loop-` and the result of the `copyIndex(1)` function: `loop-1`.</span></span> <span data-ttu-id="6f695-122">The `dependsOn` element references the previous resource because it’s a concatenation of the word `loop-` and the result of the `copyIndex()` function: `loop-0`.</span><span class="sxs-lookup"><span data-stu-id="6f695-122">The `dependsOn` element references the previous resource because it’s a concatenation of the word `loop-` and the result of the `copyIndex()` function: `loop-0`.</span></span> <span data-ttu-id="6f695-123">The pattern in the second resource object repeats until `count` has been reached, ending with a resource named `loop-4` that `dependsOn` `loop-3`.</span><span class="sxs-lookup"><span data-stu-id="6f695-123">The pattern in the second resource object repeats until `count` has been reached, ending with a resource named `loop-4` that `dependsOn` `loop-3`.</span></span> <span data-ttu-id="6f695-124">Notice that `count` is a variable that subtracts `1` from the `numberToDeploy` parameter to keep the zero-based count correct.</span><span class="sxs-lookup"><span data-stu-id="6f695-124">Notice that `count` is a variable that subtracts `1` from the `numberToDeploy` parameter to keep the zero-based count correct.</span></span>

## <a name="try-the-template"></a><span data-ttu-id="6f695-125">Try the template</span><span class="sxs-lookup"><span data-stu-id="6f695-125">Try the template</span></span>

<span data-ttu-id="6f695-126">If you would like to experiment with this template, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="6f695-126">If you would like to experiment with this template, follow these steps:</span></span>

1.  <span data-ttu-id="6f695-127">Go to the Azure portal, select the "+" icon, and search for the "template deployment" resource type.</span><span class="sxs-lookup"><span data-stu-id="6f695-127">Go to the Azure portal, select the "+" icon, and search for the "template deployment" resource type.</span></span> <span data-ttu-id="6f695-128">When you find it in the search results, select it.</span><span class="sxs-lookup"><span data-stu-id="6f695-128">When you find it in the search results, select it.</span></span>
2.  <span data-ttu-id="6f695-129">When you get to the "template deployment" page, select the "create" button.</span><span class="sxs-lookup"><span data-stu-id="6f695-129">When you get to the "template deployment" page, select the "create" button.</span></span> <span data-ttu-id="6f695-130">You go to the "custom deployment" blade, and see that the template has no resources.</span><span class="sxs-lookup"><span data-stu-id="6f695-130">You go to the "custom deployment" blade, and see that the template has no resources.</span></span>
3.  <span data-ttu-id="6f695-131">Select the "edit" icon.</span><span class="sxs-lookup"><span data-stu-id="6f695-131">Select the "edit" icon.</span></span>
4.  <span data-ttu-id="6f695-132">Delete the empty template in the right-hand pane.</span><span class="sxs-lookup"><span data-stu-id="6f695-132">Delete the empty template in the right-hand pane.</span></span>
5.  <span data-ttu-id="6f695-133">Copy and paste the preceding sample template into the right-hand pane.</span><span class="sxs-lookup"><span data-stu-id="6f695-133">Copy and paste the preceding sample template into the right-hand pane.</span></span>
6.  <span data-ttu-id="6f695-134">Select the "save" button.</span><span class="sxs-lookup"><span data-stu-id="6f695-134">Select the "save" button.</span></span>
7.  <span data-ttu-id="6f695-135">You are returned to the "custom deployment" pane, but this time there are some drop-down boxes.</span><span class="sxs-lookup"><span data-stu-id="6f695-135">You are returned to the "custom deployment" pane, but this time there are some drop-down boxes.</span></span> <span data-ttu-id="6f695-136">Select your subscription, either create new or use existing resource group, and select a location.</span><span class="sxs-lookup"><span data-stu-id="6f695-136">Select your subscription, either create new or use existing resource group, and select a location.</span></span> <span data-ttu-id="6f695-137">Review the terms and conditions, and click the "I agree" button.</span><span class="sxs-lookup"><span data-stu-id="6f695-137">Review the terms and conditions, and click the "I agree" button.</span></span>
8.  <span data-ttu-id="6f695-138">Select the "purchase" button.</span><span class="sxs-lookup"><span data-stu-id="6f695-138">Select the "purchase" button.</span></span>

<span data-ttu-id="6f695-139">To verify that the resources are being deployed sequentially, select "resource groups", then select the resource group that you selected earlier.</span><span class="sxs-lookup"><span data-stu-id="6f695-139">To verify that the resources are being deployed sequentially, select "resource groups", then select the resource group that you selected earlier.</span></span> <span data-ttu-id="6f695-140">Select the "deployments" button in the resource group blade, and you see the resources deployed in sequential order with corresponding timestamp.</span><span class="sxs-lookup"><span data-stu-id="6f695-140">Select the "deployments" button in the resource group blade, and you see the resources deployed in sequential order with corresponding timestamp.</span></span>

![Deployment of sequential loop template in Azure Resource Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-manager-sequential-loop/deployments.png)

## <a name="next-steps"></a><span data-ttu-id="6f695-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="6f695-142">Next steps</span></span>

<span data-ttu-id="6f695-143">Use this pattern in your templates by adding your resources to the nested template.</span><span class="sxs-lookup"><span data-stu-id="6f695-143">Use this pattern in your templates by adding your resources to the nested template.</span></span> <span data-ttu-id="6f695-144">You can either author them directly in the template element of the `Microsoft.Resources/deployments` resource or link to them using the `templateLink` element.</span><span class="sxs-lookup"><span data-stu-id="6f695-144">You can either author them directly in the template element of the `Microsoft.Resources/deployments` resource or link to them using the `templateLink` element.</span></span> <span data-ttu-id="6f695-145">The resource type in the example is a nested template, but any resource type can be deployed.</span><span class="sxs-lookup"><span data-stu-id="6f695-145">The resource type in the example is a nested template, but any resource type can be deployed.</span></span> <span data-ttu-id="6f695-146">The only exception is that child resources cannot be referenced from within an iteration loop.</span><span class="sxs-lookup"><span data-stu-id="6f695-146">The only exception is that child resources cannot be referenced from within an iteration loop.</span></span>

* <span data-ttu-id="6f695-147">For an introduction to creating multiple instances of a resource, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span><span class="sxs-lookup"><span data-stu-id="6f695-147">For an introduction to creating multiple instances of a resource, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
* <span data-ttu-id="6f695-148">This pattern is also implemented in the [template building blocks project](https://github.com/mspnp/template-building-blocks) and the [Azure reference architectures](/azure/architecture/reference-architectures/).</span><span class="sxs-lookup"><span data-stu-id="6f695-148">This pattern is also implemented in the [template building blocks project](https://github.com/mspnp/template-building-blocks) and the [Azure reference architectures](/azure/architecture/reference-architectures/).</span></span>
