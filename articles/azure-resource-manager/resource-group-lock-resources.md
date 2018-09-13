---
title: Prevent changes in critical Azure resources | Microsoft Docs
description: Prevent users from updating or deleting certain resources by applying a restriction to all users and roles.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 53c57e8f-741c-4026-80e0-f4c02638c98b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/14/2016
ms.author: tomfitz
ms.openlocfilehash: de8137a69ccc2028a7dcbff491573f36640bdc50
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669927"
---
# <a name="lock-resources-to-prevent-unexpected-changes"></a><span data-ttu-id="cd9cc-103">Lock resources to prevent unexpected changes</span><span class="sxs-lookup"><span data-stu-id="cd9cc-103">Lock resources to prevent unexpected changes</span></span> 
<span data-ttu-id="cd9cc-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-104">As an administrator, you may need to lock a subscription, resource group, or resource to prevent other users in your organization from accidentally deleting or modifying critical resources.</span></span> <span data-ttu-id="cd9cc-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-105">You can set the lock level to **CanNotDelete** or **ReadOnly**.</span></span> 

* <span data-ttu-id="cd9cc-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-106">**CanNotDelete** means authorized users can still read and modify a resource, but they can't delete the resource.</span></span> 
* <span data-ttu-id="cd9cc-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-107">**ReadOnly** means authorized users can read a resource, but they can't delete or update the resource.</span></span> <span data-ttu-id="cd9cc-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-108">Applying this lock is similar to restricting all authorized users to the permissions granted by the **Reader** role.</span></span> 

<span data-ttu-id="cd9cc-109">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-109">Resource Manager locks apply only to operations that happen in the management plane, which consists of operations sent to `https://management.azure.com`.</span></span> <span data-ttu-id="cd9cc-110">The locks do not restrict how resources perform their own functions.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-110">The locks do not restrict how resources perform their own functions.</span></span> <span data-ttu-id="cd9cc-111">Resource changes are restricted, but resource operations are not restricted.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-111">Resource changes are restricted, but resource operations are not restricted.</span></span> <span data-ttu-id="cd9cc-112">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-112">For example, a ReadOnly lock on a SQL Database prevents you from deleting or modifying the database, but it does not prevent you from creating, updating, or deleting data in the database.</span></span> <span data-ttu-id="cd9cc-113">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-113">Data transactions are permitted because those operations are not sent to `https://management.azure.com`.</span></span>

<span data-ttu-id="cd9cc-114">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-114">Applying **ReadOnly** can lead to unexpected results because some operations that seem like read operations actually require additional actions.</span></span> <span data-ttu-id="cd9cc-115">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-115">For example, placing a **ReadOnly** lock on a storage account prevents all users from listing the keys.</span></span> <span data-ttu-id="cd9cc-116">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-116">The list keys operation is handled through a POST request because the returned keys are available for write operations.</span></span> <span data-ttu-id="cd9cc-117">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-117">For another example, placing a **ReadOnly** lock on an App Service resource prevents Visual Studio Server Explorer from displaying files for the resource because that interaction requires write access.</span></span>

<span data-ttu-id="cd9cc-118">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-118">Unlike role-based access control, you use management locks to apply a restriction across all users and roles.</span></span> <span data-ttu-id="cd9cc-119">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span><span class="sxs-lookup"><span data-stu-id="cd9cc-119">To learn about setting permissions for users and roles, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span>

<span data-ttu-id="cd9cc-120">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-120">When you apply a lock at a parent scope, all resources within that scope inherit the same lock.</span></span> <span data-ttu-id="cd9cc-121">Even resources you add later inherit the lock from the parent.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-121">Even resources you add later inherit the lock from the parent.</span></span> <span data-ttu-id="cd9cc-122">The most restrictive lock in the inheritance takes precedence.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-122">The most restrictive lock in the inheritance takes precedence.</span></span>

## <a name="who-can-create-or-delete-locks-in-your-organization"></a><span data-ttu-id="cd9cc-123">Who can create or delete locks in your organization</span><span class="sxs-lookup"><span data-stu-id="cd9cc-123">Who can create or delete locks in your organization</span></span>
<span data-ttu-id="cd9cc-124">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-124">To create or delete management locks, you must have access to `Microsoft.Authorization/*` or `Microsoft.Authorization/locks/*` actions.</span></span> <span data-ttu-id="cd9cc-125">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-125">Of the built-in roles, only **Owner** and **User Access Administrator** are granted those actions.</span></span>

## <a name="creating-a-lock-through-the-portal"></a><span data-ttu-id="cd9cc-126">Creating a lock through the portal</span><span class="sxs-lookup"><span data-stu-id="cd9cc-126">Creating a lock through the portal</span></span>
[!INCLUDE [resource-manager-lock-resources](../../includes/resource-manager-lock-resources.md)]

## <a name="creating-a-lock-in-a-template"></a><span data-ttu-id="cd9cc-127">Creating a lock in a template</span><span class="sxs-lookup"><span data-stu-id="cd9cc-127">Creating a lock in a template</span></span>
<span data-ttu-id="cd9cc-128">The following example shows a template that creates a lock on a storage account.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-128">The following example shows a template that creates a lock on a storage account.</span></span> <span data-ttu-id="cd9cc-129">The storage account on which to apply the lock is provided as a parameter.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-129">The storage account on which to apply the lock is provided as a parameter.</span></span> <span data-ttu-id="cd9cc-130">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-130">The name of the lock is created by concatenating the resource name with **/Microsoft.Authorization/** and the name of the lock, in this case **myLock**.</span></span>

<span data-ttu-id="cd9cc-131">The type provided is specific to the resource type.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-131">The type provided is specific to the resource type.</span></span> <span data-ttu-id="cd9cc-132">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span><span class="sxs-lookup"><span data-stu-id="cd9cc-132">For storage, set the type to "Microsoft.Storage/storageaccounts/providers/locks".</span></span>

    {
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "lockedResource": {
          "type": "string"
        }
      },
      "resources": [
        {
          "name": "[concat(parameters('lockedResource'), '/Microsoft.Authorization/myLock')]",
          "type": "Microsoft.Storage/storageAccounts/providers/locks",
          "apiVersion": "2015-01-01",
          "properties": {
            "level": "CannotDelete"
          }
        }
      ]
    }

## <a name="creating-a-lock-with-rest-api"></a><span data-ttu-id="cd9cc-133">Creating a lock with REST API</span><span class="sxs-lookup"><span data-stu-id="cd9cc-133">Creating a lock with REST API</span></span>
<span data-ttu-id="cd9cc-134">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span><span class="sxs-lookup"><span data-stu-id="cd9cc-134">You can lock deployed resources with the [REST API for management locks](https://docs.microsoft.com/rest/api/resources/managementlocks).</span></span> <span data-ttu-id="cd9cc-135">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-135">The REST API enables you to create and delete locks, and retrieve information about existing locks.</span></span>

<span data-ttu-id="cd9cc-136">To create a lock, run:</span><span class="sxs-lookup"><span data-stu-id="cd9cc-136">To create a lock, run:</span></span>

    PUT https://management.azure.com/{scope}/providers/Microsoft.Authorization/locks/{lock-name}?api-version={api-version}

<span data-ttu-id="cd9cc-137">The scope could be a subscription, resource group, or resource.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-137">The scope could be a subscription, resource group, or resource.</span></span> <span data-ttu-id="cd9cc-138">The lock-name is whatever you want to call the lock.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-138">The lock-name is whatever you want to call the lock.</span></span> <span data-ttu-id="cd9cc-139">For api-version, use **2015-01-01**.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-139">For api-version, use **2015-01-01**.</span></span>

<span data-ttu-id="cd9cc-140">In the request, include a JSON object that specifies the properties for the lock.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-140">In the request, include a JSON object that specifies the properties for the lock.</span></span>

    {
      "properties": {
        "level": "CanNotDelete",
        "notes": "Optional text notes."
      }
    } 


## <a name="creating-a-lock-with-azure-powershell"></a><span data-ttu-id="cd9cc-141">Creating a lock with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cd9cc-141">Creating a lock with Azure PowerShell</span></span>
<span data-ttu-id="cd9cc-142">You can lock deployed resources with Azure PowerShell by using the **New-AzureRmResourceLock** as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-142">You can lock deployed resources with Azure PowerShell by using the **New-AzureRmResourceLock** as shown in the following example.</span></span>

    New-AzureRmResourceLock -LockLevel CanNotDelete -LockName LockSite -ResourceName examplesite -ResourceType Microsoft.Web/sites -ResourceGroupName exampleresourcegroup

<span data-ttu-id="cd9cc-143">Azure PowerShell provides other commands for working locks, such as **Set-AzureRmResourceLock** to update a lock and **Remove-AzureRmResourceLock** to delete a lock.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-143">Azure PowerShell provides other commands for working locks, such as **Set-AzureRmResourceLock** to update a lock and **Remove-AzureRmResourceLock** to delete a lock.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cd9cc-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="cd9cc-144">Next steps</span></span>
* <span data-ttu-id="cd9cc-145">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span><span class="sxs-lookup"><span data-stu-id="cd9cc-145">For more information about working with resource locks, see [Lock Down Your Azure Resources](http://blogs.msdn.com/b/cloud_solution_architect/archive/2015/06/18/lock-down-your-azure-resources.aspx)</span></span>
* <span data-ttu-id="cd9cc-146">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span><span class="sxs-lookup"><span data-stu-id="cd9cc-146">To learn about logically organizing your resources, see [Using tags to organize your resources](resource-group-using-tags.md)</span></span>
* <span data-ttu-id="cd9cc-147">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span><span class="sxs-lookup"><span data-stu-id="cd9cc-147">To change which resource group a resource resides in, see [Move resources to new resource group](resource-group-move-resources.md)</span></span>
* <span data-ttu-id="cd9cc-148">You can apply restrictions and conventions across your subscription with customized policies.</span><span class="sxs-lookup"><span data-stu-id="cd9cc-148">You can apply restrictions and conventions across your subscription with customized policies.</span></span> <span data-ttu-id="cd9cc-149">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="cd9cc-149">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>
* <span data-ttu-id="cd9cc-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="cd9cc-150">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

