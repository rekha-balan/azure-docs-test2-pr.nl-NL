---
title: Azure resource not found errors | Microsoft Docs
description: Describes how to resolve errors when a resource cannot be found.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: ''
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: troubleshooting
ms.date: 06/06/2018
ms.author: tomfitz
ms.openlocfilehash: 176de6f19274dfd8a6cf0335bb4cf16a8baa874b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857491"
---
# <a name="resolve-not-found-errors-for-azure-resources"></a><span data-ttu-id="4626c-103">Resolve not found errors for Azure resources</span><span class="sxs-lookup"><span data-stu-id="4626c-103">Resolve not found errors for Azure resources</span></span>

<span data-ttu-id="4626c-104">This article describes the errors you may see when a resource can't be found during deployment.</span><span class="sxs-lookup"><span data-stu-id="4626c-104">This article describes the errors you may see when a resource can't be found during deployment.</span></span>

## <a name="symptom"></a><span data-ttu-id="4626c-105">Symptom</span><span class="sxs-lookup"><span data-stu-id="4626c-105">Symptom</span></span>

<span data-ttu-id="4626c-106">When your template includes the name of a resource that can't be resolved, you receive an error similar to:</span><span class="sxs-lookup"><span data-stu-id="4626c-106">When your template includes the name of a resource that can't be resolved, you receive an error similar to:</span></span>

```
Code=NotFound;
Message=Cannot find ServerFarm with name exampleplan.
```

<span data-ttu-id="4626c-107">If you use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that can't be resolved, you receive the following error:</span><span class="sxs-lookup"><span data-stu-id="4626c-107">If you use the [reference](resource-group-template-functions-resource.md#reference) or [listKeys](resource-group-template-functions-resource.md#listkeys) functions with a resource that can't be resolved, you receive the following error:</span></span>

```
Code=ResourceNotFound;
Message=The Resource 'Microsoft.Storage/storageAccounts/{storage name}' under resource
group {resource group name} was not found.
```

## <a name="cause"></a><span data-ttu-id="4626c-108">Cause</span><span class="sxs-lookup"><span data-stu-id="4626c-108">Cause</span></span>

<span data-ttu-id="4626c-109">Resource Manager needs to retrieve the properties for a resource, but can't identify the resource in your subscription.</span><span class="sxs-lookup"><span data-stu-id="4626c-109">Resource Manager needs to retrieve the properties for a resource, but can't identify the resource in your subscription.</span></span>

## <a name="solution-1---set-dependencies"></a><span data-ttu-id="4626c-110">Solution 1 - set dependencies</span><span class="sxs-lookup"><span data-stu-id="4626c-110">Solution 1 - set dependencies</span></span>

<span data-ttu-id="4626c-111">If you're trying to deploy the missing resource in the template, check whether you need to add a dependency.</span><span class="sxs-lookup"><span data-stu-id="4626c-111">If you're trying to deploy the missing resource in the template, check whether you need to add a dependency.</span></span> <span data-ttu-id="4626c-112">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span><span class="sxs-lookup"><span data-stu-id="4626c-112">Resource Manager optimizes deployment by creating resources in parallel, when possible.</span></span> <span data-ttu-id="4626c-113">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template.</span><span class="sxs-lookup"><span data-stu-id="4626c-113">If one resource must be deployed after another resource, you need to use the **dependsOn** element in your template.</span></span> <span data-ttu-id="4626c-114">For example, when deploying a web app, the App Service plan must exist.</span><span class="sxs-lookup"><span data-stu-id="4626c-114">For example, when deploying a web app, the App Service plan must exist.</span></span> <span data-ttu-id="4626c-115">If you haven't specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span><span class="sxs-lookup"><span data-stu-id="4626c-115">If you haven't specified that the web app depends on the App Service plan, Resource Manager creates both resources at the same time.</span></span> <span data-ttu-id="4626c-116">You get an error stating that the App Service plan resource can't be found, because it doesn't exist yet when attempting to set a property on the web app.</span><span class="sxs-lookup"><span data-stu-id="4626c-116">You get an error stating that the App Service plan resource can't be found, because it doesn't exist yet when attempting to set a property on the web app.</span></span> <span data-ttu-id="4626c-117">You prevent this error by setting the dependency in the web app.</span><span class="sxs-lookup"><span data-stu-id="4626c-117">You prevent this error by setting the dependency in the web app.</span></span>

```json
{
  "apiVersion": "2015-08-01",
  "type": "Microsoft.Web/sites",
  "dependsOn": [
    "[variables('hostingPlanName')]"
  ],
  ...
}
```

<span data-ttu-id="4626c-118">But, you want to avoid setting dependencies that aren't needed.</span><span class="sxs-lookup"><span data-stu-id="4626c-118">But, you want to avoid setting dependencies that aren't needed.</span></span> <span data-ttu-id="4626c-119">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that aren't dependent on each other from being deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="4626c-119">When you have unnecessary dependencies, you prolong the duration of the deployment by preventing resources that aren't dependent on each other from being deployed in parallel.</span></span> <span data-ttu-id="4626c-120">In addition, you may create circular dependencies that block the deployment.</span><span class="sxs-lookup"><span data-stu-id="4626c-120">In addition, you may create circular dependencies that block the deployment.</span></span> <span data-ttu-id="4626c-121">The [reference](resource-group-template-functions-resource.md#reference) function and [list\*](resource-group-template-functions-resource.md#list) functions creates an implicit dependency on the referenced resource, when that resource is deployed in the same template and is referenced by its name (not resource ID).</span><span class="sxs-lookup"><span data-stu-id="4626c-121">The [reference](resource-group-template-functions-resource.md#reference) function and [list\*](resource-group-template-functions-resource.md#list) functions creates an implicit dependency on the referenced resource, when that resource is deployed in the same template and is referenced by its name (not resource ID).</span></span> <span data-ttu-id="4626c-122">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span><span class="sxs-lookup"><span data-stu-id="4626c-122">Therefore, you may have more dependencies than the dependencies specified in the **dependsOn** property.</span></span> <span data-ttu-id="4626c-123">The [resourceId](resource-group-template-functions-resource.md#resourceid) function doesn't create an implicit dependency or validate that the resource exists.</span><span class="sxs-lookup"><span data-stu-id="4626c-123">The [resourceId](resource-group-template-functions-resource.md#resourceid) function doesn't create an implicit dependency or validate that the resource exists.</span></span> <span data-ttu-id="4626c-124">The [reference](resource-group-template-functions-resource.md#reference) function and [list\*](resource-group-template-functions-resource.md#list) functions don't create an implicit dependency when the resource is referred to by its resource ID.</span><span class="sxs-lookup"><span data-stu-id="4626c-124">The [reference](resource-group-template-functions-resource.md#reference) function and [list\*](resource-group-template-functions-resource.md#list) functions don't create an implicit dependency when the resource is referred to by its resource ID.</span></span> <span data-ttu-id="4626c-125">To create an implicit dependency, pass the name of the resource that is deployed in the same template.</span><span class="sxs-lookup"><span data-stu-id="4626c-125">To create an implicit dependency, pass the name of the resource that is deployed in the same template.</span></span>

<span data-ttu-id="4626c-126">When you see dependency problems, you need to gain insight into the order of resource deployment.</span><span class="sxs-lookup"><span data-stu-id="4626c-126">When you see dependency problems, you need to gain insight into the order of resource deployment.</span></span> <span data-ttu-id="4626c-127">To view the order of deployment operations:</span><span class="sxs-lookup"><span data-stu-id="4626c-127">To view the order of deployment operations:</span></span>

1. <span data-ttu-id="4626c-128">Select the deployment history for your resource group.</span><span class="sxs-lookup"><span data-stu-id="4626c-128">Select the deployment history for your resource group.</span></span>

   ![select deployment history](./media/resource-manager-not-found-errors/select-deployment.png)

2. <span data-ttu-id="4626c-130">Select a deployment from the history, and select **Events**.</span><span class="sxs-lookup"><span data-stu-id="4626c-130">Select a deployment from the history, and select **Events**.</span></span>

   ![select deployment events](./media/resource-manager-not-found-errors/select-deployment-events.png)

3. <span data-ttu-id="4626c-132">Examine the sequence of events for each resource.</span><span class="sxs-lookup"><span data-stu-id="4626c-132">Examine the sequence of events for each resource.</span></span> <span data-ttu-id="4626c-133">Pay attention to the status of each operation.</span><span class="sxs-lookup"><span data-stu-id="4626c-133">Pay attention to the status of each operation.</span></span> <span data-ttu-id="4626c-134">For example, the following image shows three storage accounts that deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="4626c-134">For example, the following image shows three storage accounts that deployed in parallel.</span></span> <span data-ttu-id="4626c-135">Notice that the three storage accounts are started at the same time.</span><span class="sxs-lookup"><span data-stu-id="4626c-135">Notice that the three storage accounts are started at the same time.</span></span>

   ![parallel deployment](./media/resource-manager-not-found-errors/deployment-events-parallel.png)

   <span data-ttu-id="4626c-137">The next image shows three storage accounts that aren't deployed in parallel.</span><span class="sxs-lookup"><span data-stu-id="4626c-137">The next image shows three storage accounts that aren't deployed in parallel.</span></span> <span data-ttu-id="4626c-138">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span><span class="sxs-lookup"><span data-stu-id="4626c-138">The second storage account depends on the first storage account, and the third storage account depends on the second storage account.</span></span> <span data-ttu-id="4626c-139">The first storage account is started, accepted, and completed before the next is started.</span><span class="sxs-lookup"><span data-stu-id="4626c-139">The first storage account is started, accepted, and completed before the next is started.</span></span>

   ![sequential deployment](./media/resource-manager-not-found-errors/deployment-events-sequence.png)

## <a name="solution-2---get-resource-from-different-resource-group"></a><span data-ttu-id="4626c-141">Solution 2 - get resource from different resource group</span><span class="sxs-lookup"><span data-stu-id="4626c-141">Solution 2 - get resource from different resource group</span></span>

<span data-ttu-id="4626c-142">When the resource exists in a different resource group than the one being deployed to, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span><span class="sxs-lookup"><span data-stu-id="4626c-142">When the resource exists in a different resource group than the one being deployed to, use the [resourceId function](resource-group-template-functions-resource.md#resourceid) to get the fully qualified name of the resource.</span></span>

```json
"properties": {
    "name": "[parameters('siteName')]",
    "serverFarmId": "[resourceId('plangroup', 'Microsoft.Web/serverfarms', parameters('hostingPlanName'))]"
}
```

## <a name="solution-3---check-reference-function"></a><span data-ttu-id="4626c-143">Solution 3 - check reference function</span><span class="sxs-lookup"><span data-stu-id="4626c-143">Solution 3 - check reference function</span></span>

<span data-ttu-id="4626c-144">Look for an expression that includes the [reference](resource-group-template-functions-resource.md#reference) function.</span><span class="sxs-lookup"><span data-stu-id="4626c-144">Look for an expression that includes the [reference](resource-group-template-functions-resource.md#reference) function.</span></span> <span data-ttu-id="4626c-145">The values you provide vary based on whether the resource is in the same template, resource group, and subscription.</span><span class="sxs-lookup"><span data-stu-id="4626c-145">The values you provide vary based on whether the resource is in the same template, resource group, and subscription.</span></span> <span data-ttu-id="4626c-146">Double check that you're providing the required parameter values for your scenario.</span><span class="sxs-lookup"><span data-stu-id="4626c-146">Double check that you're providing the required parameter values for your scenario.</span></span> <span data-ttu-id="4626c-147">If the resource is in a different resource group, provide the full resource ID.</span><span class="sxs-lookup"><span data-stu-id="4626c-147">If the resource is in a different resource group, provide the full resource ID.</span></span> <span data-ttu-id="4626c-148">For example, to reference a storage account in another resource group, use:</span><span class="sxs-lookup"><span data-stu-id="4626c-148">For example, to reference a storage account in another resource group, use:</span></span>

```json
"[reference(resourceId('exampleResourceGroup', 'Microsoft.Storage/storageAccounts', 'myStorage'), '2017-06-01')]"
```