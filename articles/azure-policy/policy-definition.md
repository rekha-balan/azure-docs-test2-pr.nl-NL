---
title: Azure Policy definition structure
description: Describes how resource policy definition is used by Azure Policy to establish conventions for resources in your organization by describing when the policy is enforced and what effect to take.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 08/16/2018
ms.topic: conceptual
ms.service: azure-policy
manager: carmonm
ms.openlocfilehash: ac561be75306cab6b73b457a7d450bd640aac067
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869063"
---
# <a name="azure-policy-definition-structure"></a><span data-ttu-id="fc583-103">Azure Policy definition structure</span><span class="sxs-lookup"><span data-stu-id="fc583-103">Azure Policy definition structure</span></span>

<span data-ttu-id="fc583-104">Resource policy definition used by Azure Policy enables you to establish conventions for resources in your organization by describing when the policy is enforced and what effect to take.</span><span class="sxs-lookup"><span data-stu-id="fc583-104">Resource policy definition used by Azure Policy enables you to establish conventions for resources in your organization by describing when the policy is enforced and what effect to take.</span></span> <span data-ttu-id="fc583-105">By defining conventions, you can control costs and more easily manage your resources.</span><span class="sxs-lookup"><span data-stu-id="fc583-105">By defining conventions, you can control costs and more easily manage your resources.</span></span> <span data-ttu-id="fc583-106">For example, you can specify that only certain types of virtual machines are allowed.</span><span class="sxs-lookup"><span data-stu-id="fc583-106">For example, you can specify that only certain types of virtual machines are allowed.</span></span> <span data-ttu-id="fc583-107">Or, you can require that all resources have a particular tag.</span><span class="sxs-lookup"><span data-stu-id="fc583-107">Or, you can require that all resources have a particular tag.</span></span> <span data-ttu-id="fc583-108">Policies are inherited by all child resources.</span><span class="sxs-lookup"><span data-stu-id="fc583-108">Policies are inherited by all child resources.</span></span> <span data-ttu-id="fc583-109">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span><span class="sxs-lookup"><span data-stu-id="fc583-109">So, if a policy is applied to a resource group, it is applicable to all the resources in that resource group.</span></span>

<span data-ttu-id="fc583-110">The schema used by Azure Policy can be found here: [https://schema.management.azure.com/schemas/2016-12-01/policyDefinition.json](https://schema.management.azure.com/schemas/2016-12-01/policyDefinition.json)</span><span class="sxs-lookup"><span data-stu-id="fc583-110">The schema used by Azure Policy can be found here: [https://schema.management.azure.com/schemas/2016-12-01/policyDefinition.json](https://schema.management.azure.com/schemas/2016-12-01/policyDefinition.json)</span></span>

<span data-ttu-id="fc583-111">You use JSON to create a policy definition.</span><span class="sxs-lookup"><span data-stu-id="fc583-111">You use JSON to create a policy definition.</span></span> <span data-ttu-id="fc583-112">The policy definition contains elements for:</span><span class="sxs-lookup"><span data-stu-id="fc583-112">The policy definition contains elements for:</span></span>

- <span data-ttu-id="fc583-113">mode</span><span class="sxs-lookup"><span data-stu-id="fc583-113">mode</span></span>
- <span data-ttu-id="fc583-114">parameters</span><span class="sxs-lookup"><span data-stu-id="fc583-114">parameters</span></span>
- <span data-ttu-id="fc583-115">display name</span><span class="sxs-lookup"><span data-stu-id="fc583-115">display name</span></span>
- <span data-ttu-id="fc583-116">description</span><span class="sxs-lookup"><span data-stu-id="fc583-116">description</span></span>
- <span data-ttu-id="fc583-117">policy rule</span><span class="sxs-lookup"><span data-stu-id="fc583-117">policy rule</span></span>
  - <span data-ttu-id="fc583-118">logical evaluation</span><span class="sxs-lookup"><span data-stu-id="fc583-118">logical evaluation</span></span>
  - <span data-ttu-id="fc583-119">effect</span><span class="sxs-lookup"><span data-stu-id="fc583-119">effect</span></span>

<span data-ttu-id="fc583-120">For example, the following JSON shows a policy that limits where resources are deployed:</span><span class="sxs-lookup"><span data-stu-id="fc583-120">For example, the following JSON shows a policy that limits where resources are deployed:</span></span>

```json
{
    "properties": {
        "mode": "all",
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

<span data-ttu-id="fc583-121">All Azure Policy samples are at [Policy samples](json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-121">All Azure Policy samples are at [Policy samples](json-samples.md).</span></span>

## <a name="mode"></a><span data-ttu-id="fc583-122">Mode</span><span class="sxs-lookup"><span data-stu-id="fc583-122">Mode</span></span>

<span data-ttu-id="fc583-123">The **mode** determines which resource types will be evaluated for a policy.</span><span class="sxs-lookup"><span data-stu-id="fc583-123">The **mode** determines which resource types will be evaluated for a policy.</span></span> <span data-ttu-id="fc583-124">The supported modes are:</span><span class="sxs-lookup"><span data-stu-id="fc583-124">The supported modes are:</span></span>

- <span data-ttu-id="fc583-125">`all`: evaluate resource groups and all resource types</span><span class="sxs-lookup"><span data-stu-id="fc583-125">`all`: evaluate resource groups and all resource types</span></span>
- <span data-ttu-id="fc583-126">`indexed`: only evaluate resource types that support tags and location</span><span class="sxs-lookup"><span data-stu-id="fc583-126">`indexed`: only evaluate resource types that support tags and location</span></span>

<span data-ttu-id="fc583-127">We recommend that you set **mode** to `all` in most cases.</span><span class="sxs-lookup"><span data-stu-id="fc583-127">We recommend that you set **mode** to `all` in most cases.</span></span> <span data-ttu-id="fc583-128">All policy definitions created through the portal use the `all` mode.</span><span class="sxs-lookup"><span data-stu-id="fc583-128">All policy definitions created through the portal use the `all` mode.</span></span> <span data-ttu-id="fc583-129">If you use PowerShell or Azure CLI, you can specify the **mode** parameter manually.</span><span class="sxs-lookup"><span data-stu-id="fc583-129">If you use PowerShell or Azure CLI, you can specify the **mode** parameter manually.</span></span> <span data-ttu-id="fc583-130">If the policy definition does not contain a **mode** value it defaults to `all` in Azure PowerShell and to `null` in Azure CLI, which is equivalent to `indexed`, for backwards compatibility.</span><span class="sxs-lookup"><span data-stu-id="fc583-130">If the policy definition does not contain a **mode** value it defaults to `all` in Azure PowerShell and to `null` in Azure CLI, which is equivalent to `indexed`, for backwards compatibility.</span></span>

<span data-ttu-id="fc583-131">`indexed` should be used when creating policies that will enforce tags or locations.</span><span class="sxs-lookup"><span data-stu-id="fc583-131">`indexed` should be used when creating policies that will enforce tags or locations.</span></span> <span data-ttu-id="fc583-132">This isn't required but it will prevent resources that don't support tags and locations from showing up as non-compliant in the compliance results.</span><span class="sxs-lookup"><span data-stu-id="fc583-132">This isn't required but it will prevent resources that don't support tags and locations from showing up as non-compliant in the compliance results.</span></span> <span data-ttu-id="fc583-133">The one exception to this is **resource groups**.</span><span class="sxs-lookup"><span data-stu-id="fc583-133">The one exception to this is **resource groups**.</span></span> <span data-ttu-id="fc583-134">Policies that are attempting to enforce location or tags on a resource group should set **mode** to `all` and specifically target the `Microsoft.Resources/subscriptions/resourceGroup` type.</span><span class="sxs-lookup"><span data-stu-id="fc583-134">Policies that are attempting to enforce location or tags on a resource group should set **mode** to `all` and specifically target the `Microsoft.Resources/subscriptions/resourceGroup` type.</span></span> <span data-ttu-id="fc583-135">For an example, see [Enforce resource group tags](scripts/enforce-tag-rg.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-135">For an example, see [Enforce resource group tags](scripts/enforce-tag-rg.md).</span></span>

## <a name="parameters"></a><span data-ttu-id="fc583-136">Parameters</span><span class="sxs-lookup"><span data-stu-id="fc583-136">Parameters</span></span>

<span data-ttu-id="fc583-137">Parameters help simplify your policy management by reducing the number of policy definitions.</span><span class="sxs-lookup"><span data-stu-id="fc583-137">Parameters help simplify your policy management by reducing the number of policy definitions.</span></span> <span data-ttu-id="fc583-138">Think of parameters like the fields on a form – `name`, `address`, `city`, `state`.</span><span class="sxs-lookup"><span data-stu-id="fc583-138">Think of parameters like the fields on a form – `name`, `address`, `city`, `state`.</span></span> <span data-ttu-id="fc583-139">These parameters always stay the same, however their values change based on the individual filling out the form.</span><span class="sxs-lookup"><span data-stu-id="fc583-139">These parameters always stay the same, however their values change based on the individual filling out the form.</span></span> <span data-ttu-id="fc583-140">Parameters work the same way when building policies.</span><span class="sxs-lookup"><span data-stu-id="fc583-140">Parameters work the same way when building policies.</span></span> <span data-ttu-id="fc583-141">By including parameters in a policy definition, you can reuse that policy for different scenarios by using different values.</span><span class="sxs-lookup"><span data-stu-id="fc583-141">By including parameters in a policy definition, you can reuse that policy for different scenarios by using different values.</span></span>

<span data-ttu-id="fc583-142">For example, you could define a policy for a resource property to limit the locations where resources can be deployed.</span><span class="sxs-lookup"><span data-stu-id="fc583-142">For example, you could define a policy for a resource property to limit the locations where resources can be deployed.</span></span> <span data-ttu-id="fc583-143">In this case, you would declare the following parameters when you create your policy:</span><span class="sxs-lookup"><span data-stu-id="fc583-143">In this case, you would declare the following parameters when you create your policy:</span></span>

```json
"parameters": {
    "allowedLocations": {
        "type": "array",
        "metadata": {
            "description": "The list of allowed locations for resources.",
            "displayName": "Allowed locations",
            "strongType": "location"
        }
    }
}
```

<span data-ttu-id="fc583-144">The type of a parameter can be either string or array.</span><span class="sxs-lookup"><span data-stu-id="fc583-144">The type of a parameter can be either string or array.</span></span> <span data-ttu-id="fc583-145">The metadata property is used for tools like the Azure portal to display user-friendly information.</span><span class="sxs-lookup"><span data-stu-id="fc583-145">The metadata property is used for tools like the Azure portal to display user-friendly information.</span></span>

<span data-ttu-id="fc583-146">Within the metadata property, you can use **strongType** to provide a multi-select list of options within the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="fc583-146">Within the metadata property, you can use **strongType** to provide a multi-select list of options within the Azure portal.</span></span>  <span data-ttu-id="fc583-147">Allowed values for **strongType** currently include:</span><span class="sxs-lookup"><span data-stu-id="fc583-147">Allowed values for **strongType** currently include:</span></span>

- `"location"`
- `"resourceTypes"`
- `"storageSkus"`
- `"vmSKUs"`
- `"existingResourceGroups"`
- `"omsWorkspace"`

<span data-ttu-id="fc583-148">In the policy rule, you reference parameters with the following `parameters` deployment value function syntax:</span><span class="sxs-lookup"><span data-stu-id="fc583-148">In the policy rule, you reference parameters with the following `parameters` deployment value function syntax:</span></span>

```json
{
    "field": "location",
    "in": "[parameters('allowedLocations')]"
}
```

## <a name="definition-location"></a><span data-ttu-id="fc583-149">Definition location</span><span class="sxs-lookup"><span data-stu-id="fc583-149">Definition location</span></span>

<span data-ttu-id="fc583-150">While creating an initiative or policy definition, it is important that you specify the definition location.</span><span class="sxs-lookup"><span data-stu-id="fc583-150">While creating an initiative or policy definition, it is important that you specify the definition location.</span></span>

<span data-ttu-id="fc583-151">The definition location determines the scope to which the initiative or policy definition can be assigned to.</span><span class="sxs-lookup"><span data-stu-id="fc583-151">The definition location determines the scope to which the initiative or policy definition can be assigned to.</span></span> <span data-ttu-id="fc583-152">The location can be specified as a management group or a subscription.</span><span class="sxs-lookup"><span data-stu-id="fc583-152">The location can be specified as a management group or a subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="fc583-153">If you plan to apply this policy definition to multiple subscriptions, the location must be a management group that contains the subscriptions you will assign the initiative or policy to.</span><span class="sxs-lookup"><span data-stu-id="fc583-153">If you plan to apply this policy definition to multiple subscriptions, the location must be a management group that contains the subscriptions you will assign the initiative or policy to.</span></span>

## <a name="display-name-and-description"></a><span data-ttu-id="fc583-154">Display name and description</span><span class="sxs-lookup"><span data-stu-id="fc583-154">Display name and description</span></span>

<span data-ttu-id="fc583-155">You can use **displayName** and **description** to identify the policy definition and provide context for when it is used.</span><span class="sxs-lookup"><span data-stu-id="fc583-155">You can use **displayName** and **description** to identify the policy definition and provide context for when it is used.</span></span>

## <a name="policy-rule"></a><span data-ttu-id="fc583-156">Policy rule</span><span class="sxs-lookup"><span data-stu-id="fc583-156">Policy rule</span></span>

<span data-ttu-id="fc583-157">The policy rule consists of **If** and **Then** blocks.</span><span class="sxs-lookup"><span data-stu-id="fc583-157">The policy rule consists of **If** and **Then** blocks.</span></span> <span data-ttu-id="fc583-158">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span><span class="sxs-lookup"><span data-stu-id="fc583-158">In the **If** block, you define one or more conditions that specify when the policy is enforced.</span></span> <span data-ttu-id="fc583-159">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span><span class="sxs-lookup"><span data-stu-id="fc583-159">You can apply logical operators to these conditions to precisely define the scenario for a policy.</span></span>

<span data-ttu-id="fc583-160">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span><span class="sxs-lookup"><span data-stu-id="fc583-160">In the **Then** block, you define the effect that happens when the **If** conditions are fulfilled.</span></span>

```json
{
    "if": {
        <condition> | <logical operator>
    },
    "then": {
        "effect": "deny | audit | append | auditIfNotExists | deployIfNotExists"
    }
}
```

### <a name="logical-operators"></a><span data-ttu-id="fc583-161">Logical operators</span><span class="sxs-lookup"><span data-stu-id="fc583-161">Logical operators</span></span>

<span data-ttu-id="fc583-162">Supported logical operators are:</span><span class="sxs-lookup"><span data-stu-id="fc583-162">Supported logical operators are:</span></span>

- `"not": {condition  or operator}`
- `"allOf": [{condition or operator},{condition or operator}]`
- `"anyOf": [{condition or operator},{condition or operator}]`

<span data-ttu-id="fc583-163">The **not** syntax inverts the result of the condition.</span><span class="sxs-lookup"><span data-stu-id="fc583-163">The **not** syntax inverts the result of the condition.</span></span> <span data-ttu-id="fc583-164">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span><span class="sxs-lookup"><span data-stu-id="fc583-164">The **allOf** syntax (similar to the logical **And** operation) requires all conditions to be true.</span></span> <span data-ttu-id="fc583-165">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span><span class="sxs-lookup"><span data-stu-id="fc583-165">The **anyOf** syntax (similar to the logical **Or** operation) requires one or more conditions to be true.</span></span>

<span data-ttu-id="fc583-166">You can nest logical operators.</span><span class="sxs-lookup"><span data-stu-id="fc583-166">You can nest logical operators.</span></span> <span data-ttu-id="fc583-167">The following example shows a **not** operation that is nested within an **allOf** operation.</span><span class="sxs-lookup"><span data-stu-id="fc583-167">The following example shows a **not** operation that is nested within an **allOf** operation.</span></span>

```json
"if": {
    "allOf": [{
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

### <a name="conditions"></a><span data-ttu-id="fc583-168">Conditions</span><span class="sxs-lookup"><span data-stu-id="fc583-168">Conditions</span></span>

<span data-ttu-id="fc583-169">A condition evaluates whether a **field** meets certain criteria.</span><span class="sxs-lookup"><span data-stu-id="fc583-169">A condition evaluates whether a **field** meets certain criteria.</span></span> <span data-ttu-id="fc583-170">The supported conditions are:</span><span class="sxs-lookup"><span data-stu-id="fc583-170">The supported conditions are:</span></span>

- `"equals": "value"`
- `"notEquals": "value"`
- `"like": "value"`
- `"notLike": "value"`
- `"match": "value"`
- `"notMatch": "value"`
- `"contains": "value"`
- `"notContains": "value"`
- `"in": ["value1","value2"]`
- `"notIn": ["value1","value2"]`
- `"containsKey": "keyName"`
- `"notContainsKey": "keyName"`
- `"exists": "bool"`

<span data-ttu-id="fc583-171">When using the **like** and **notLike** conditions, you can provide a wildcard `*` in the value.</span><span class="sxs-lookup"><span data-stu-id="fc583-171">When using the **like** and **notLike** conditions, you can provide a wildcard `*` in the value.</span></span>
<span data-ttu-id="fc583-172">The value should not contain more than one wildcard `*`.</span><span class="sxs-lookup"><span data-stu-id="fc583-172">The value should not contain more than one wildcard `*`.</span></span>

<span data-ttu-id="fc583-173">When using the **match** and **notMatch** conditions, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span><span class="sxs-lookup"><span data-stu-id="fc583-173">When using the **match** and **notMatch** conditions, provide `#` to represent a digit, `?` for a letter, and any other character to represent that actual character.</span></span> <span data-ttu-id="fc583-174">For examples, see [Allow multiple name patterns](scripts/allow-multiple-name-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-174">For examples, see [Allow multiple name patterns](scripts/allow-multiple-name-patterns.md).</span></span>

### <a name="fields"></a><span data-ttu-id="fc583-175">Fields</span><span class="sxs-lookup"><span data-stu-id="fc583-175">Fields</span></span>

<span data-ttu-id="fc583-176">Conditions are formed by using fields.</span><span class="sxs-lookup"><span data-stu-id="fc583-176">Conditions are formed by using fields.</span></span> <span data-ttu-id="fc583-177">A field represents properties in the resource request payload that is used to describe the state of the resource.</span><span class="sxs-lookup"><span data-stu-id="fc583-177">A field represents properties in the resource request payload that is used to describe the state of the resource.</span></span>  

<span data-ttu-id="fc583-178">The following fields are supported:</span><span class="sxs-lookup"><span data-stu-id="fc583-178">The following fields are supported:</span></span>

- `name`
- `fullName`
  - <span data-ttu-id="fc583-179">Returns the full name of the resource.</span><span class="sxs-lookup"><span data-stu-id="fc583-179">Returns the full name of the resource.</span></span> <span data-ttu-id="fc583-180">The full name of a resource is the resource name prepended by any parent resource names (for example "myServer/myDatabase").</span><span class="sxs-lookup"><span data-stu-id="fc583-180">The full name of a resource is the resource name prepended by any parent resource names (for example "myServer/myDatabase").</span></span>
- `kind`
- `type`
- `location`
- `tags`
- `tags.<tagName>`
  - <span data-ttu-id="fc583-181">Where **\<tagName\>** is the name of the tag to validate the condition for.</span><span class="sxs-lookup"><span data-stu-id="fc583-181">Where **\<tagName\>** is the name of the tag to validate the condition for.</span></span>
  - <span data-ttu-id="fc583-182">Example: `tags.CostCenter` where **CostCenter** is the name of the tag.</span><span class="sxs-lookup"><span data-stu-id="fc583-182">Example: `tags.CostCenter` where **CostCenter** is the name of the tag.</span></span>
- `tags[<tagName>]`
  - <span data-ttu-id="fc583-183">This bracket syntax supports tag names that contain periods.</span><span class="sxs-lookup"><span data-stu-id="fc583-183">This bracket syntax supports tag names that contain periods.</span></span>
  - <span data-ttu-id="fc583-184">Where **\<tagName\>** is the name of the tag to validate the condition for.</span><span class="sxs-lookup"><span data-stu-id="fc583-184">Where **\<tagName\>** is the name of the tag to validate the condition for.</span></span>
  - <span data-ttu-id="fc583-185">Example: `tags.[Acct.CostCenter]` where **Acct.CostCenter** is the name of the tag.</span><span class="sxs-lookup"><span data-stu-id="fc583-185">Example: `tags.[Acct.CostCenter]` where **Acct.CostCenter** is the name of the tag.</span></span>
- <span data-ttu-id="fc583-186">property aliases - for a list, see [Aliases](#aliases).</span><span class="sxs-lookup"><span data-stu-id="fc583-186">property aliases - for a list, see [Aliases](#aliases).</span></span>

### <a name="effect"></a><span data-ttu-id="fc583-187">Effect</span><span class="sxs-lookup"><span data-stu-id="fc583-187">Effect</span></span>

<span data-ttu-id="fc583-188">Policy supports the following types of effect:</span><span class="sxs-lookup"><span data-stu-id="fc583-188">Policy supports the following types of effect:</span></span>

- <span data-ttu-id="fc583-189">**Deny**: generates an event in the audit log and fails the request</span><span class="sxs-lookup"><span data-stu-id="fc583-189">**Deny**: generates an event in the audit log and fails the request</span></span>
- <span data-ttu-id="fc583-190">**Audit**: generates a warning event in audit log but does not fail the request</span><span class="sxs-lookup"><span data-stu-id="fc583-190">**Audit**: generates a warning event in audit log but does not fail the request</span></span>
- <span data-ttu-id="fc583-191">**Append**: adds the defined set of fields to the request</span><span class="sxs-lookup"><span data-stu-id="fc583-191">**Append**: adds the defined set of fields to the request</span></span>
- <span data-ttu-id="fc583-192">**AuditIfNotExists**: enables auditing if a resource does not exist</span><span class="sxs-lookup"><span data-stu-id="fc583-192">**AuditIfNotExists**: enables auditing if a resource does not exist</span></span>
- <span data-ttu-id="fc583-193">**DeployIfNotExists**: deploys a resource if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="fc583-193">**DeployIfNotExists**: deploys a resource if it does not already exist.</span></span> <span data-ttu-id="fc583-194">Currently, this effect is only supported through built-in policies.</span><span class="sxs-lookup"><span data-stu-id="fc583-194">Currently, this effect is only supported through built-in policies.</span></span>

<span data-ttu-id="fc583-195">For **append**, you must provide the following details:</span><span class="sxs-lookup"><span data-stu-id="fc583-195">For **append**, you must provide the following details:</span></span>

```json
"effect": "append",
"details": [{
    "field": "field name",
    "value": "value of the field"
}]
```

<span data-ttu-id="fc583-196">The value can be either a string or a JSON format object.</span><span class="sxs-lookup"><span data-stu-id="fc583-196">The value can be either a string or a JSON format object.</span></span>

<span data-ttu-id="fc583-197">With **AuditIfNotExists** and **DeployIfNotExists** you can evaluate the existence of a related resource and apply a rule and a corresponding effect when that resource does not exist.</span><span class="sxs-lookup"><span data-stu-id="fc583-197">With **AuditIfNotExists** and **DeployIfNotExists** you can evaluate the existence of a related resource and apply a rule and a corresponding effect when that resource does not exist.</span></span> <span data-ttu-id="fc583-198">For example, you can require that a network watcher is deployed for all virtual networks.</span><span class="sxs-lookup"><span data-stu-id="fc583-198">For example, you can require that a network watcher is deployed for all virtual networks.</span></span>
<span data-ttu-id="fc583-199">For an example of auditing when a virtual machine extension is not deployed, see [Audit if extension does not exist](scripts/audit-ext-not-exist.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-199">For an example of auditing when a virtual machine extension is not deployed, see [Audit if extension does not exist](scripts/audit-ext-not-exist.md).</span></span>

<span data-ttu-id="fc583-200">For complete details on each effect, order of evaluation, properties, and examples, see [Understanding Policy Effects](policy-effects.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-200">For complete details on each effect, order of evaluation, properties, and examples, see [Understanding Policy Effects](policy-effects.md).</span></span>

### <a name="policy-functions"></a><span data-ttu-id="fc583-201">Policy functions</span><span class="sxs-lookup"><span data-stu-id="fc583-201">Policy functions</span></span>

<span data-ttu-id="fc583-202">A subset of [Resource Manager template functions](../azure-resource-manager/resource-group-template-functions.md) are available to use within a policy rule.</span><span class="sxs-lookup"><span data-stu-id="fc583-202">A subset of [Resource Manager template functions](../azure-resource-manager/resource-group-template-functions.md) are available to use within a policy rule.</span></span> <span data-ttu-id="fc583-203">The functions currently supported are:</span><span class="sxs-lookup"><span data-stu-id="fc583-203">The functions currently supported are:</span></span>

- [<span data-ttu-id="fc583-204">parameters</span><span class="sxs-lookup"><span data-stu-id="fc583-204">parameters</span></span>](../azure-resource-manager/resource-group-template-functions-deployment.md#parameters)
- [<span data-ttu-id="fc583-205">concat</span><span class="sxs-lookup"><span data-stu-id="fc583-205">concat</span></span>](../azure-resource-manager/resource-group-template-functions-array.md#concat)
- [<span data-ttu-id="fc583-206">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="fc583-206">resourceGroup</span></span>](../azure-resource-manager/resource-group-template-functions-resource.md#resourcegroup)
- [<span data-ttu-id="fc583-207">subscription</span><span class="sxs-lookup"><span data-stu-id="fc583-207">subscription</span></span>](../azure-resource-manager/resource-group-template-functions-resource.md#subscription)

<span data-ttu-id="fc583-208">Additionally, the `field` function is available to policy rules.</span><span class="sxs-lookup"><span data-stu-id="fc583-208">Additionally, the `field` function is available to policy rules.</span></span> <span data-ttu-id="fc583-209">This function is primarily for use with **AuditIfNotExists** and **DeployIfNotExists** to reference fields on the resource that is being evaluated.</span><span class="sxs-lookup"><span data-stu-id="fc583-209">This function is primarily for use with **AuditIfNotExists** and **DeployIfNotExists** to reference fields on the resource that is being evaluated.</span></span> <span data-ttu-id="fc583-210">An example of this can be seen on the [DeployIfNotExists example](policy-effects.md#deployifnotexists-example).</span><span class="sxs-lookup"><span data-stu-id="fc583-210">An example of this can be seen on the [DeployIfNotExists example](policy-effects.md#deployifnotexists-example).</span></span>

#### <a name="policy-function-examples"></a><span data-ttu-id="fc583-211">Policy function examples</span><span class="sxs-lookup"><span data-stu-id="fc583-211">Policy function examples</span></span>

<span data-ttu-id="fc583-212">This policy rule example uses the `resourceGroup` resource function to get the **name** property, combined with the `concat` array and object function to build a `like` condition that enforces the resource name to start with the resource group name.</span><span class="sxs-lookup"><span data-stu-id="fc583-212">This policy rule example uses the `resourceGroup` resource function to get the **name** property, combined with the `concat` array and object function to build a `like` condition that enforces the resource name to start with the resource group name.</span></span>

```json
{
    "if": {
        "not": {
            "field": "name",
            "like": "[concat(resourceGroup().name,'*')]"
        }
    },
    "then": {
        "effect": "deny"
    }
}
```

<span data-ttu-id="fc583-213">This policy rule example uses the `resourceGroup` resource function to get the **tags** property array value of the **CostCenter** tag on the resource group and append it to the **CostCenter** tag on the new resource.</span><span class="sxs-lookup"><span data-stu-id="fc583-213">This policy rule example uses the `resourceGroup` resource function to get the **tags** property array value of the **CostCenter** tag on the resource group and append it to the **CostCenter** tag on the new resource.</span></span>

```json
{
    "if": {
        "field": "tags.CostCenter",
        "exists": "false"
    },
    "then": {
        "effect": "append",
        "details": [{
            "field": "tags.CostCenter",
            "value": "[resourceGroup().tags.CostCenter]"
        }]
    }
}
```

## <a name="aliases"></a><span data-ttu-id="fc583-214">Aliases</span><span class="sxs-lookup"><span data-stu-id="fc583-214">Aliases</span></span>

<span data-ttu-id="fc583-215">You use property aliases to access specific properties for a resource type.</span><span class="sxs-lookup"><span data-stu-id="fc583-215">You use property aliases to access specific properties for a resource type.</span></span> <span data-ttu-id="fc583-216">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span><span class="sxs-lookup"><span data-stu-id="fc583-216">Aliases enable you to restrict what values or conditions are permitted for a property on a resource.</span></span> <span data-ttu-id="fc583-217">Each alias maps to paths in different API versions for a given resource type.</span><span class="sxs-lookup"><span data-stu-id="fc583-217">Each alias maps to paths in different API versions for a given resource type.</span></span> <span data-ttu-id="fc583-218">During policy evaluation, the policy engine gets the property path for that API version.</span><span class="sxs-lookup"><span data-stu-id="fc583-218">During policy evaluation, the policy engine gets the property path for that API version.</span></span>

<span data-ttu-id="fc583-219">The list of aliases is always growing.</span><span class="sxs-lookup"><span data-stu-id="fc583-219">The list of aliases is always growing.</span></span> <span data-ttu-id="fc583-220">To discover what aliases are currently supported by Azure Policy, use one of the following methods:</span><span class="sxs-lookup"><span data-stu-id="fc583-220">To discover what aliases are currently supported by Azure Policy, use one of the following methods:</span></span>

- <span data-ttu-id="fc583-221">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fc583-221">Azure PowerShell</span></span>

  ```azurepowershell-interactive
  # Login first with Connect-AzureRmAccount if not using Cloud Shell

  $azContext = Get-AzureRmContext
  $azProfile = [Microsoft.Azure.Commands.Common.Authentication.Abstractions.AzureRmProfileProvider]::Instance.Profile
  $profileClient = New-Object -TypeName Microsoft.Azure.Commands.ResourceManager.Common.RMProfileClient -ArgumentList ($azProfile)
  $token = $profileClient.AcquireAccessToken($azContext.Subscription.TenantId)
  $authHeader = @{
    'Authorization'='Bearer ' + $token.AccessToken
  }

  # Create a splatting variable for Invoke-RestMethod
  $invokeRest = @{
    Uri = 'https://management.azure.com/providers/?api-version=2017-08-01&$expand=resourceTypes/aliases'
    Method = 'Get'
    ContentType = 'application/json'
    Headers = $authHeader
  }

  # Invoke the REST API
  $response = Invoke-RestMethod @invokeRest

  # Create an List to hold discovered aliases
  $aliases = [System.Collections.Generic.List[pscustomobject]]::new()

  foreach ($ns in $response.value)
  {
      foreach ($rT in $ns.resourceTypes)
      {
          if ($rT.aliases)
          {
              foreach ($obj in $rT.aliases)
              {
                  $alias = [PSCustomObject]@{
                      Namespace    = $ns.namespace
                      resourceType = $rT.resourceType
                      alias        = $obj.name
                  }
                  $aliases.Add($alias)
              }
          }
      }
  }

  # Output the list and sort it by Namespace, resourceType and alias. You can customize with Where-Object to limit as desired.
  $aliases | Sort-Object -Property Namespace, resourceType, alias
  ```

- <span data-ttu-id="fc583-222">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc583-222">Azure CLI</span></span>

  ```azurecli-interactive
  # Login first with az login if not using Cloud Shell

  # List namespaces
  az provider list --query [*].namespace

  # Get Azure Policy aliases for a specific Namespace (such as Azure Automation -- Microsoft.Automation)
  az provider show --namespace Microsoft.Automation --expand "resourceTypes/aliases" --query "resourceTypes[].aliases[].name"
  ```

- <span data-ttu-id="fc583-223">REST API / ARMClient</span><span class="sxs-lookup"><span data-stu-id="fc583-223">REST API / ARMClient</span></span>

  ```http
  GET https://management.azure.com/providers/?api-version=2017-08-01&$expand=resourceTypes/aliases
  ```

## <a name="initiatives"></a><span data-ttu-id="fc583-224">Initiatives</span><span class="sxs-lookup"><span data-stu-id="fc583-224">Initiatives</span></span>

<span data-ttu-id="fc583-225">Initiatives enable you to group several related policy definitions to simplify assignments and management because you work with a group as a single item.</span><span class="sxs-lookup"><span data-stu-id="fc583-225">Initiatives enable you to group several related policy definitions to simplify assignments and management because you work with a group as a single item.</span></span> <span data-ttu-id="fc583-226">For example, you can group all related tagging policy definitions in a single initiative.</span><span class="sxs-lookup"><span data-stu-id="fc583-226">For example, you can group all related tagging policy definitions in a single initiative.</span></span> <span data-ttu-id="fc583-227">Rather than assigning each policy individually, you apply the initiative.</span><span class="sxs-lookup"><span data-stu-id="fc583-227">Rather than assigning each policy individually, you apply the initiative.</span></span>

<span data-ttu-id="fc583-228">The following example illustrates how to create an initiative for handling two tags: `costCenter` and `productName`.</span><span class="sxs-lookup"><span data-stu-id="fc583-228">The following example illustrates how to create an initiative for handling two tags: `costCenter` and `productName`.</span></span> <span data-ttu-id="fc583-229">It uses two built-in policies to apply the default tag value.</span><span class="sxs-lookup"><span data-stu-id="fc583-229">It uses two built-in policies to apply the default tag value.</span></span>

```json
{
    "properties": {
        "displayName": "Billing Tags Policy",
        "policyType": "Custom",
        "description": "Specify cost Center tag and product name tag",
        "parameters": {
            "costCenterValue": {
                "type": "String",
                "metadata": {
                    "description": "required value for Cost Center tag"
                }
            },
            "productNameValue": {
                "type": "String",
                "metadata": {
                    "description": "required value for product Name tag"
                }
            }
        },
        "policyDefinitions": [{
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
                "parameters": {
                    "tagName": {
                        "value": "costCenter"
                    },
                    "tagValue": {
                        "value": "[parameters('costCenterValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/2a0e14a6-b0a6-4fab-991a-187a4f81c498",
                "parameters": {
                    "tagName": {
                        "value": "costCenter"
                    },
                    "tagValue": {
                        "value": "[parameters('costCenterValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/1e30110a-5ceb-460c-a204-c1c3969c6d62",
                "parameters": {
                    "tagName": {
                        "value": "productName"
                    },
                    "tagValue": {
                        "value": "[parameters('productNameValue')]"
                    }
                }
            },
            {
                "policyDefinitionId": "/providers/Microsoft.Authorization/policyDefinitions/2a0e14a6-b0a6-4fab-991a-187a4f81c498",
                "parameters": {
                    "tagName": {
                        "value": "productName"
                    },
                    "tagValue": {
                        "value": "[parameters('productNameValue')]"
                    }
                }
            }
        ]
    },
    "id": "/subscriptions/<subscription-id>/providers/Microsoft.Authorization/policySetDefinitions/billingTagsPolicy",
    "type": "Microsoft.Authorization/policySetDefinitions",
    "name": "billingTagsPolicy"
}
```

## <a name="next-steps"></a><span data-ttu-id="fc583-230">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc583-230">Next steps</span></span>

- <span data-ttu-id="fc583-231">Review more examples at [Azure Policy samples](json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="fc583-231">Review more examples at [Azure Policy samples](json-samples.md).</span></span>
