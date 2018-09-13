---
title: Azure resource policies | Microsoft Docs
description: Describes how to use Azure Resource Manager policies to ensure consistent resource properties are set during deployment. Policies can be applied at the subscription or resource groups.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: abde0f73-c0fe-4e6d-a1ee-32a6fce52a2d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: d75088bd83b0b70c889388c95331bb56fe9ba15b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550479"
---
# <a name="resource-policy-overview"></a><span data-ttu-id="2ea2e-104">Resource policy overview</span><span class="sxs-lookup"><span data-stu-id="2ea2e-104">Resource policy overview</span></span>
<span data-ttu-id="2ea2e-105">Resource policies enable you to establish conventions for resources in your organization.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-105">Resource policies enable you to establish conventions for resources in your organization.</span></span> <span data-ttu-id="2ea2e-106">By defining conventions, you can control costs and more easily manage your resources.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-106">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="2ea2e-107">For example, you can specify that only certain types of virtual machines are allowed, or you can require that all resources have a particular tag.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-107">For example, you can specify that only certain types of virtual machines are allowed, or you can require that all resources have a particular tag.</span></span> <span data-ttu-id="2ea2e-108">Policies are inherited by all child resources.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-108">Policies are inherited by all child resources.</span></span> <span data-ttu-id="2ea2e-109">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-109">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="2ea2e-110">There are two concepts to understand about policies:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-110">There are two concepts to understand about policies:</span></span>

* <span data-ttu-id="2ea2e-111">policy definition - you describe when the policy is enforced and what action to take</span><span class="sxs-lookup"><span data-stu-id="2ea2e-111">policy definition - you describe when the policy is enforced and what action to take</span></span>
* <span data-ttu-id="2ea2e-112">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span><span class="sxs-lookup"><span data-stu-id="2ea2e-112">policy assignment - you apply the policy definition to a scope (subscription or resource group)</span></span>

<span data-ttu-id="2ea2e-113">This topic focuses on policy definition.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-113">This topic focuses on policy definition.</span></span> <span data-ttu-id="2ea2e-114">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-114">For information about policy assignment, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md) or [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>

<span data-ttu-id="2ea2e-115">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-115">Azure provides some built-in policy definitions that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="2ea2e-116">If a built-in policy definition works for your scenario, use that definition when assigning to a scope.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-116">If a built-in policy definition works for your scenario, use that definition when assigning to a scope.</span></span>

<span data-ttu-id="2ea2e-117">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-117">Policies are evaluated when creating and updating resources (PUT and PATCH operations).</span></span>

> [!NOTE]
> <span data-ttu-id="2ea2e-118">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-118">Currently, policy does not evaluate resource types that do not support tags, kind, and location, such as the Microsoft.Resources/deployments resource type.</span></span> <span data-ttu-id="2ea2e-119">This support will be added at a future time.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-119">This support will be added at a future time.</span></span> <span data-ttu-id="2ea2e-120">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-120">To avoid backward compatibility issues, you should explicitly specify type when authoring policies.</span></span> <span data-ttu-id="2ea2e-121">For example, a tag policy that does not specify types is applied for all types.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-121">For example, a tag policy that does not specify types is applied for all types.</span></span> <span data-ttu-id="2ea2e-122">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-122">In that case, a template deployment may fail if there is a nested resource that doesn't support tags, and the deployment resource type has been added to policy evaluation.</span></span> 
> 
> 

## <a name="how-is-it-different-from-rbac"></a><span data-ttu-id="2ea2e-123">How is it different from RBAC?</span><span class="sxs-lookup"><span data-stu-id="2ea2e-123">How is it different from RBAC?</span></span>
<span data-ttu-id="2ea2e-124">There are a few key differences between policy and role-based access control (RBAC).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-124">There are a few key differences between policy and role-based access control (RBAC).</span></span> <span data-ttu-id="2ea2e-125">RBAC focuses on **user** actions at different scopes.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-125">RBAC focuses on **user** actions at different scopes.</span></span> <span data-ttu-id="2ea2e-126">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-126">For example, you are added to the contributor role for a resource group at the desired scope, so you can make changes to that resource group.</span></span> <span data-ttu-id="2ea2e-127">Policy focuses on **resource** properties during deployment.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-127">Policy focuses on **resource** properties during deployment.</span></span> <span data-ttu-id="2ea2e-128">For example, through policies, you can control the types of resources that can be provisioned or restrict the locations in which the resources can be provisioned.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-128">For example, through policies, you can control the types of resources that can be provisioned or restrict the locations in which the resources can be provisioned.</span></span> <span data-ttu-id="2ea2e-129">Unlike RBAC, policy is a default allow and explicit deny system.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-129">Unlike RBAC, policy is a default allow and explicit deny system.</span></span> 

<span data-ttu-id="2ea2e-130">To use policies, you must be authenticated through RBAC.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-130">To use policies, you must be authenticated through RBAC.</span></span> <span data-ttu-id="2ea2e-131">Specifically, your account needs the:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-131">Specifically, your account needs the:</span></span>

* <span data-ttu-id="2ea2e-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span><span class="sxs-lookup"><span data-stu-id="2ea2e-132">`Microsoft.Authorization/policydefinitions/write` permission to define a policy</span></span>
* <span data-ttu-id="2ea2e-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span><span class="sxs-lookup"><span data-stu-id="2ea2e-133">`Microsoft.Authorization/policyassignments/write` permission to assign a policy</span></span> 

<span data-ttu-id="2ea2e-134">These permissions are not included in the **Contributor** role.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-134">These permissions are not included in the **Contributor** role.</span></span>

## <a name="policy-definition-structure"></a><span data-ttu-id="2ea2e-135">Policy definition structure</span><span class="sxs-lookup"><span data-stu-id="2ea2e-135">Policy definition structure</span></span>
<span data-ttu-id="2ea2e-136">You use JSON to create a policy definition.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-136">You use JSON to create a policy definition.</span></span> <span data-ttu-id="2ea2e-137">The policy definition contains elements for:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-137">The policy definition contains elements for:</span></span>

* <span data-ttu-id="2ea2e-138">parameters</span><span class="sxs-lookup"><span data-stu-id="2ea2e-138">parameters</span></span>
* <span data-ttu-id="2ea2e-139">display name</span><span class="sxs-lookup"><span data-stu-id="2ea2e-139">display name</span></span>
* <span data-ttu-id="2ea2e-140">description</span><span class="sxs-lookup"><span data-stu-id="2ea2e-140">description</span></span>
* <span data-ttu-id="2ea2e-141">policy rule</span><span class="sxs-lookup"><span data-stu-id="2ea2e-141">policy rule</span></span>
  * <span data-ttu-id="2ea2e-142">logical evaluation</span><span class="sxs-lookup"><span data-stu-id="2ea2e-142">logical evaluation</span></span>
  * <span data-ttu-id="2ea2e-143">effect</span><span class="sxs-lookup"><span data-stu-id="2ea2e-143">effect</span></span>

<span data-ttu-id="2ea2e-144">The following example shows a policy that limits where resources are deployed:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-144">The following example shows a policy that limits where resources are deployed:</span></span>

```json
{
  "properties": {
    "parameters": {
      "allowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that can be specified when deploying resources",
          "strongType": "location",
          "displayName": "Allowed locations"
        }
      }
    },
    "displayName": "Allowed locations",
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "not": {
          "field": "location",
          "in": "[parameters('allowedLocations')]"
        }
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

## <a name="parameters"></a><span data-ttu-id="2ea2e-145">Parameters</span><span class="sxs-lookup"><span data-stu-id="2ea2e-145">Parameters</span></span>
<span data-ttu-id="2ea2e-146">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-146">Using parameters helps simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="2ea2e-147">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-147">You define a policy for a resource property (such as limiting the locations where resources can be deployed), and include parameters in the definition.</span></span> <span data-ttu-id="2ea2e-148">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-148">Then, you reuse that policy definition for different scenarios by passing in different values (such as specifying one set of locations for a subscription) when assigning the policy.</span></span>

<span data-ttu-id="2ea2e-149">You declare parameters when you create policy definitions.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-149">You declare parameters when you create policy definitions.</span></span>

```json
"parameters": {
  "allowedLocations": {
    "type": "array",
    "metadata": {
      "description": "The list of allowed locations for resources.",
      "displayName": "Allowed locations"
    }
  }
}
```

<span data-ttu-id="2ea2e-150">The type of a parameter can be either string or array.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-150">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="2ea2e-151">The metadata property is used for tools like Azure portal to display user-friendly information.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-151">The metadata property is used for tools like Azure portal to display user-friendly information.</span></span> 

<span data-ttu-id="2ea2e-152">In the policy rule, you reference parameters with the following syntax:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-152">In the policy rule, you reference parameters with the following syntax:</span></span> 

```json
{ 
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="display-name-and-description"></a><span data-ttu-id="2ea2e-153">Display name and description</span><span class="sxs-lookup"><span data-stu-id="2ea2e-153">Display name and description</span></span>

<span data-ttu-id="2ea2e-154">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-154">You use the **displayName** and **description** to identify the policy definition, and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="2ea2e-155">Policy rule</span><span class="sxs-lookup"><span data-stu-id="2ea2e-155">Policy rule</span></span>

<span data-ttu-id="2ea2e-156">The policy rule consists of **If** and **Then** blocks.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-156">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="2ea2e-157">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-157">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="2ea2e-158">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-158">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span> <span data-ttu-id="2ea2e-159">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-159">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
  "if": {
    <condition> | <logical operator>
  },
  "then": {
    "effect": "deny | audit | append"
  }
}
```

### <a name="logical-operators"></a><span data-ttu-id="2ea2e-160">Logical operators</span><span class="sxs-lookup"><span data-stu-id="2ea2e-160">Logical operators</span></span>
<span data-ttu-id="2ea2e-161">The supported logical operators are:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-161">The supported logical operators are:</span></span>

* `"not": {condition  or operator}`
* `"allOf": [{condition or operator},{condition or operator}]`
* `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="2ea2e-162">The **not** syntax inverts the result of the condition.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-162">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="2ea2e-163">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-163">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="2ea2e-164">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-164">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="2ea2e-165">You can nest logical operators.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-165">You can nest logical operators.</span></span> <span data-ttu-id="2ea2e-166">The following example shows a **Not** operation that is nested within an **And** operation.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-166">The following example shows a **Not** operation that is nested within an **And** operation.</span></span> 

```json
"if": {
  "allOf": [
    {
      "not": {
        "field": "tags",
        "containsKey": "application"
      }
    },
    {
      "field": "type",
      "equals": "Microsoft.Storage/storageAccounts"
    }
  ]
},
```

### <a name="conditions"></a><span data-ttu-id="2ea2e-167">Conditions</span><span class="sxs-lookup"><span data-stu-id="2ea2e-167">Conditions</span></span>
<span data-ttu-id="2ea2e-168">The condition evaluates whether a **field** meets certain criteria.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-168">The condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="2ea2e-169">The supported conditions are:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-169">The supported conditions are:</span></span>

* `"equals": "value"`
* `"like": "value"`
* `"contains": "value"`
* `"in": ["value1","value2"]`
* `"containsKey": "keyName"`
* `"exists": "bool"`

<span data-ttu-id="2ea2e-170">When using the **like** condition, you can provide a wildcard (\*) in the value.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-170">When using the **like** condition, you can provide a wildcard (\*) in the value.</span></span>

### <a name="fields"></a><span data-ttu-id="2ea2e-171">Fields</span><span class="sxs-lookup"><span data-stu-id="2ea2e-171">Fields</span></span>
<span data-ttu-id="2ea2e-172">Conditions are formed by using fields.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-172">Conditions are formed by using fields.</span></span> <span data-ttu-id="2ea2e-173">A field represents properties in the resource request payload that is used to describe the state of the resource.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-173">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="2ea2e-174">The following fields are supported:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-174">The following fields are supported:</span></span>

* `name`
* `kind`
* `type`
* `location`
* `tags`
* `tags.*` 
* <span data-ttu-id="2ea2e-175">property aliases</span><span class="sxs-lookup"><span data-stu-id="2ea2e-175">property aliases</span></span>

<span data-ttu-id="2ea2e-176">You use property aliases to access specific properties for a resource type.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-176">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="2ea2e-177">The supported aliases are:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-177">The supported aliases are:</span></span>

* <span data-ttu-id="2ea2e-178">Microsoft.CDN/profiles/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ea2e-178">Microsoft.CDN/profiles/sku.name</span></span>
* <span data-ttu-id="2ea2e-179">Microsoft.Compute/virtualMachines/imageOffer</span><span class="sxs-lookup"><span data-stu-id="2ea2e-179">Microsoft.Compute/virtualMachines/imageOffer</span></span>
* <span data-ttu-id="2ea2e-180">Microsoft.Compute/virtualMachines/imagePublisher</span><span class="sxs-lookup"><span data-stu-id="2ea2e-180">Microsoft.Compute/virtualMachines/imagePublisher</span></span>
* <span data-ttu-id="2ea2e-181">Microsoft.Compute/virtualMachines/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ea2e-181">Microsoft.Compute/virtualMachines/sku.name</span></span>
* <span data-ttu-id="2ea2e-182">Microsoft.Compute/virtualMachines/imageSku</span><span class="sxs-lookup"><span data-stu-id="2ea2e-182">Microsoft.Compute/virtualMachines/imageSku</span></span> 
* <span data-ttu-id="2ea2e-183">Microsoft.Compute/virtualMachines/imageVersion</span><span class="sxs-lookup"><span data-stu-id="2ea2e-183">Microsoft.Compute/virtualMachines/imageVersion</span></span>
* <span data-ttu-id="2ea2e-184">Microsoft.SQL/servers/databases/edition</span><span class="sxs-lookup"><span data-stu-id="2ea2e-184">Microsoft.SQL/servers/databases/edition</span></span>
* <span data-ttu-id="2ea2e-185">Microsoft.SQL/servers/databases/elasticPoolName</span><span class="sxs-lookup"><span data-stu-id="2ea2e-185">Microsoft.SQL/servers/databases/elasticPoolName</span></span>
* <span data-ttu-id="2ea2e-186">Microsoft.SQL/servers/databases/requestedServiceObjectiveId</span><span class="sxs-lookup"><span data-stu-id="2ea2e-186">Microsoft.SQL/servers/databases/requestedServiceObjectiveId</span></span>
* <span data-ttu-id="2ea2e-187">Microsoft.SQL/servers/databases/requestedServiceObjectiveName</span><span class="sxs-lookup"><span data-stu-id="2ea2e-187">Microsoft.SQL/servers/databases/requestedServiceObjectiveName</span></span>
* <span data-ttu-id="2ea2e-188">Microsoft.SQL/servers/elasticPools/dtu</span><span class="sxs-lookup"><span data-stu-id="2ea2e-188">Microsoft.SQL/servers/elasticPools/dtu</span></span>
* <span data-ttu-id="2ea2e-189">Microsoft.SQL/servers/elasticPools/edition</span><span class="sxs-lookup"><span data-stu-id="2ea2e-189">Microsoft.SQL/servers/elasticPools/edition</span></span>
* <span data-ttu-id="2ea2e-190">Microsoft.SQL/servers/version</span><span class="sxs-lookup"><span data-stu-id="2ea2e-190">Microsoft.SQL/servers/version</span></span>
* <span data-ttu-id="2ea2e-191">Microsoft.Storage/storageAccounts/accessTier</span><span class="sxs-lookup"><span data-stu-id="2ea2e-191">Microsoft.Storage/storageAccounts/accessTier</span></span>
* <span data-ttu-id="2ea2e-192">Microsoft.Storage/storageAccounts/enableBlobEncryption</span><span class="sxs-lookup"><span data-stu-id="2ea2e-192">Microsoft.Storage/storageAccounts/enableBlobEncryption</span></span>
* <span data-ttu-id="2ea2e-193">Microsoft.Storage/storageAccounts/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ea2e-193">Microsoft.Storage/storageAccounts/sku.name</span></span>
* <span data-ttu-id="2ea2e-194">Microsoft.Web/serverFarms/sku.name</span><span class="sxs-lookup"><span data-stu-id="2ea2e-194">Microsoft.Web/serverFarms/sku.name</span></span>

### <a name="effect"></a><span data-ttu-id="2ea2e-195">Effect</span><span class="sxs-lookup"><span data-stu-id="2ea2e-195">Effect</span></span>
<span data-ttu-id="2ea2e-196">Policy supports three types of effect - `deny`, `audit`, and `append`.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-196">Policy supports three types of effect - `deny`, `audit`, and `append`.</span></span> 

* <span data-ttu-id="2ea2e-197">**Deny** generates an event in the audit log and fails the request</span><span class="sxs-lookup"><span data-stu-id="2ea2e-197">**Deny** generates an event in the audit log and fails the request</span></span>
* <span data-ttu-id="2ea2e-198">**Audit** generates a warning event in audit log but does not fail the request</span><span class="sxs-lookup"><span data-stu-id="2ea2e-198">**Audit** generates a warning event in audit log but does not fail the request</span></span>
* <span data-ttu-id="2ea2e-199">**Append** adds the defined set of fields to the request</span><span class="sxs-lookup"><span data-stu-id="2ea2e-199">**Append** adds the defined set of fields to the request</span></span> 

<span data-ttu-id="2ea2e-200">For **append**, you must provide the following details:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-200">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [
  {
    "field": "field name",
    "value": "value of the field"
  }
]
```

<span data-ttu-id="2ea2e-201">The value can be either a string or a JSON format object.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-201">The value can be either a string or a JSON format object.</span></span> 

## <a name="policy-examples"></a><span data-ttu-id="2ea2e-202">Policy examples</span><span class="sxs-lookup"><span data-stu-id="2ea2e-202">Policy examples</span></span>

<span data-ttu-id="2ea2e-203">The following topics contain policy examples:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-203">The following topics contain policy examples:</span></span>

* <span data-ttu-id="2ea2e-204">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-204">For examples of tag polices, see [Apply resource policies for tags](resource-manager-policy-tags.md).</span></span>
* <span data-ttu-id="2ea2e-205">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-205">For examples of storage policies, see [Apply resource policies to storage accounts](resource-manager-policy-storage.md).</span></span>
* <span data-ttu-id="2ea2e-206">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="2ea2e-206">For examples of virtual machine policies, see [Apply resource policies to Linux VMs](../virtual-machines/linux/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json) and [Apply resource policies to Windows VMs](../virtual-machines/windows/policy.md?toc=%2fazure%2fazure-resource-manager%2ftoc.json)</span></span>

### <a name="allowed-resource-locations"></a><span data-ttu-id="2ea2e-207">Allowed resource locations</span><span class="sxs-lookup"><span data-stu-id="2ea2e-207">Allowed resource locations</span></span>
<span data-ttu-id="2ea2e-208">To specify which locations are allowed, see the example in the [Policy definition structure](#policy-definition-structure) section.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-208">To specify which locations are allowed, see the example in the [Policy definition structure](#policy-definition-structure) section.</span></span> <span data-ttu-id="2ea2e-209">To assign this policy definition, use the built-in policy with the resource ID `/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c`.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-209">To assign this policy definition, use the built-in policy with the resource ID `/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c`.</span></span>

### <a name="not-allowed-resource-locations"></a><span data-ttu-id="2ea2e-210">Not allowed resource locations</span><span class="sxs-lookup"><span data-stu-id="2ea2e-210">Not allowed resource locations</span></span>
<span data-ttu-id="2ea2e-211">To specify which locations are not allowed, use the following policy definition:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-211">To specify which locations are not allowed, use the following policy definition:</span></span>

```json
{
  "properties": {
    "parameters": {
      "notAllowedLocations": {
        "type": "array",
        "metadata": {
          "description": "The list of locations that are not allowed when deploying resources",
          "strongType": "location",
          "displayName": "Not allowed locations"
        }
      }
    },
    "displayName": "Not allowed locations",
    "description": "This policy enables you to block locations that your organization can specify when deploying resources.",
    "policyRule": {
      "if": {
        "field": "location",
        "in": "[parameters('notAllowedLocations')]"
      },
      "then": {
        "effect": "deny"
      }
    }
  }
}
```

### <a name="allowed-resource-types"></a><span data-ttu-id="2ea2e-212">Allowed resource types</span><span class="sxs-lookup"><span data-stu-id="2ea2e-212">Allowed resource types</span></span>
<span data-ttu-id="2ea2e-213">The following example shows a policy that permits deployments for only the Microsoft.Resources, Microsoft.Compute, Microsoft.Storage, Microsoft.Network resource types.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-213">The following example shows a policy that permits deployments for only the Microsoft.Resources, Microsoft.Compute, Microsoft.Storage, Microsoft.Network resource types.</span></span> <span data-ttu-id="2ea2e-214">All others are denied:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-214">All others are denied:</span></span>

```json
{
  "if": {
    "not": {
      "anyOf": [
        {
          "field": "type",
          "like": "Microsoft.Resources/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Compute/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Storage/*"
        },
        {
          "field": "type",
          "like": "Microsoft.Network/*"
        }
      ]
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

### <a name="set-naming-convention"></a><span data-ttu-id="2ea2e-215">Set naming convention</span><span class="sxs-lookup"><span data-stu-id="2ea2e-215">Set naming convention</span></span>
<span data-ttu-id="2ea2e-216">The following example shows the use of wildcard, which is supported by the **like** condition.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-216">The following example shows the use of wildcard, which is supported by the **like** condition.</span></span> <span data-ttu-id="2ea2e-217">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span><span class="sxs-lookup"><span data-stu-id="2ea2e-217">The condition states that if the name does match the mentioned pattern (namePrefix\*nameSuffix) then deny the request:</span></span>

```json
{
  "if": {
    "not": {
      "field": "name",
      "like": "namePrefix*nameSuffix"
    }
  },
  "then": {
    "effect": "deny"
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2ea2e-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="2ea2e-218">Next steps</span></span>
* <span data-ttu-id="2ea2e-219">After defining a policy rule, assign it to a scope.</span><span class="sxs-lookup"><span data-stu-id="2ea2e-219">After defining a policy rule, assign it to a scope.</span></span> <span data-ttu-id="2ea2e-220">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-220">To assign policies through the portal, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="2ea2e-221">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-221">To assign policies through REST API, PowerShell or Azure CLI, see [Assign and manage policies through script](resource-manager-policy-create-assign.md).</span></span>
* <span data-ttu-id="2ea2e-222">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-222">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>
* <span data-ttu-id="2ea2e-223">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span><span class="sxs-lookup"><span data-stu-id="2ea2e-223">The policy schema is published at [http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json](http://schema.management.azure.com/schemas/2015-10-01-preview/policyDefinition.json).</span></span> 

