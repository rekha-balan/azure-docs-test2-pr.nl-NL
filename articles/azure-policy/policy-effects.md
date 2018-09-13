---
title: Understanding Azure Policy Effects
description: Azure Policy definition have various effects that determine how compliance is managed and reported.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 05/24/2018
ms.topic: conceptual
ms.service: azure-policy
manager: carmonm
ms.custom: mvc
ms.openlocfilehash: 17ad631e2441e4b8d6314557c17be143fd2f3de0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869589"
---
# <a name="understanding-policy-effects"></a><span data-ttu-id="91c85-103">Understanding Policy Effects</span><span class="sxs-lookup"><span data-stu-id="91c85-103">Understanding Policy Effects</span></span>

<span data-ttu-id="91c85-104">Each policy definition in Azure Policy has a single effect that determines what happens during scanning when the **if** segment of the policy rule is evaluated to match the resource being scanned.</span><span class="sxs-lookup"><span data-stu-id="91c85-104">Each policy definition in Azure Policy has a single effect that determines what happens during scanning when the **if** segment of the policy rule is evaluated to match the resource being scanned.</span></span> <span data-ttu-id="91c85-105">The effects can also behave differently if they are for a new resource, an updated resource, or an existing resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-105">The effects can also behave differently if they are for a new resource, an updated resource, or an existing resource.</span></span>

<span data-ttu-id="91c85-106">There are currently five effects that are supported in a policy definition:</span><span class="sxs-lookup"><span data-stu-id="91c85-106">There are currently five effects that are supported in a policy definition:</span></span>

- <span data-ttu-id="91c85-107">Append</span><span class="sxs-lookup"><span data-stu-id="91c85-107">Append</span></span>
- <span data-ttu-id="91c85-108">Audit</span><span class="sxs-lookup"><span data-stu-id="91c85-108">Audit</span></span>
- <span data-ttu-id="91c85-109">AuditIfNotExists</span><span class="sxs-lookup"><span data-stu-id="91c85-109">AuditIfNotExists</span></span>
- <span data-ttu-id="91c85-110">Deny</span><span class="sxs-lookup"><span data-stu-id="91c85-110">Deny</span></span>
- <span data-ttu-id="91c85-111">DeployIfNotExists (only available to **built-in** policies)</span><span class="sxs-lookup"><span data-stu-id="91c85-111">DeployIfNotExists (only available to **built-in** policies)</span></span>

## <a name="order-of-evaluation"></a><span data-ttu-id="91c85-112">Order of Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-112">Order of Evaluation</span></span>

<span data-ttu-id="91c85-113">When a request to create or update a resource through Azure Resource Manager is made, Policy processes several of the effects prior to handing the request to the appropriate Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="91c85-113">When a request to create or update a resource through Azure Resource Manager is made, Policy processes several of the effects prior to handing the request to the appropriate Resource Provider.</span></span>
<span data-ttu-id="91c85-114">Doing so prevents unnecessary processing by a Resource Provider when a resource does not meet the designed governance controls of Policy.</span><span class="sxs-lookup"><span data-stu-id="91c85-114">Doing so prevents unnecessary processing by a Resource Provider when a resource does not meet the designed governance controls of Policy.</span></span> <span data-ttu-id="91c85-115">Policy creates a list of all policy definitions assigned, by a policy or initiative assignment, that apply by scope (minus exclusions) to the resource and prepares to evaluate the resource against each definition.</span><span class="sxs-lookup"><span data-stu-id="91c85-115">Policy creates a list of all policy definitions assigned, by a policy or initiative assignment, that apply by scope (minus exclusions) to the resource and prepares to evaluate the resource against each definition.</span></span>

- <span data-ttu-id="91c85-116">**Append** is evaluated first.</span><span class="sxs-lookup"><span data-stu-id="91c85-116">**Append** is evaluated first.</span></span> <span data-ttu-id="91c85-117">Since append could alter the request, a change made by append may prevent an audit or deny effect from triggering.</span><span class="sxs-lookup"><span data-stu-id="91c85-117">Since append could alter the request, a change made by append may prevent an audit or deny effect from triggering.</span></span>
- <span data-ttu-id="91c85-118">**Deny** is then evaluated.</span><span class="sxs-lookup"><span data-stu-id="91c85-118">**Deny** is then evaluated.</span></span> <span data-ttu-id="91c85-119">By evaluating deny before audit, double logging of an undesired resource is prevented.</span><span class="sxs-lookup"><span data-stu-id="91c85-119">By evaluating deny before audit, double logging of an undesired resource is prevented.</span></span>
- <span data-ttu-id="91c85-120">**Audit** is then evaluated prior to the request going to the Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="91c85-120">**Audit** is then evaluated prior to the request going to the Resource Provider.</span></span>

<span data-ttu-id="91c85-121">Once the request is provided to the Resource Provider and the Resource Provider returns a success status code, **AuditIfNotExists** and **DeployIfNotExists** are evaluated to determine if follow-up compliance logging or action is required.</span><span class="sxs-lookup"><span data-stu-id="91c85-121">Once the request is provided to the Resource Provider and the Resource Provider returns a success status code, **AuditIfNotExists** and **DeployIfNotExists** are evaluated to determine if follow-up compliance logging or action is required.</span></span>

## <a name="append"></a><span data-ttu-id="91c85-122">Append</span><span class="sxs-lookup"><span data-stu-id="91c85-122">Append</span></span>

<span data-ttu-id="91c85-123">Append is used to add additional fields to the requested resource during creation or update.</span><span class="sxs-lookup"><span data-stu-id="91c85-123">Append is used to add additional fields to the requested resource during creation or update.</span></span> <span data-ttu-id="91c85-124">It can be useful for adding tags on resources such as costCenter or specifying allowed IPs for a storage resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-124">It can be useful for adding tags on resources such as costCenter or specifying allowed IPs for a storage resource.</span></span>

### <a name="append-evaluation"></a><span data-ttu-id="91c85-125">Append Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-125">Append Evaluation</span></span>

<span data-ttu-id="91c85-126">As mentioned, append evaluates prior to the request getting processed by a Resource Provider during the creation or updating of a resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-126">As mentioned, append evaluates prior to the request getting processed by a Resource Provider during the creation or updating of a resource.</span></span> <span data-ttu-id="91c85-127">Append adds field(s) to the resource when the **if** condition of the policy rule is met.</span><span class="sxs-lookup"><span data-stu-id="91c85-127">Append adds field(s) to the resource when the **if** condition of the policy rule is met.</span></span> <span data-ttu-id="91c85-128">If the append effect would override a value in the original request with a different value, then it acts as a deny effect and reject the request.</span><span class="sxs-lookup"><span data-stu-id="91c85-128">If the append effect would override a value in the original request with a different value, then it acts as a deny effect and reject the request.</span></span>

<span data-ttu-id="91c85-129">When a policy definition using the append effect is run as part of an evaluation cycle, it does not make changes to resources that already exist.</span><span class="sxs-lookup"><span data-stu-id="91c85-129">When a policy definition using the append effect is run as part of an evaluation cycle, it does not make changes to resources that already exist.</span></span> <span data-ttu-id="91c85-130">Instead, it marks any resource that meets the **if** condition as non-compliant.</span><span class="sxs-lookup"><span data-stu-id="91c85-130">Instead, it marks any resource that meets the **if** condition as non-compliant.</span></span>

### <a name="append-properties"></a><span data-ttu-id="91c85-131">Append Properties</span><span class="sxs-lookup"><span data-stu-id="91c85-131">Append Properties</span></span>

<span data-ttu-id="91c85-132">An append effect only has a **details** array, which is required.</span><span class="sxs-lookup"><span data-stu-id="91c85-132">An append effect only has a **details** array, which is required.</span></span> <span data-ttu-id="91c85-133">As **details** is an array, it can take either a single **field/value** pair or multiples.</span><span class="sxs-lookup"><span data-stu-id="91c85-133">As **details** is an array, it can take either a single **field/value** pair or multiples.</span></span> <span data-ttu-id="91c85-134">Refer to [policy definition](policy-definition.md#fields) for the list of acceptable fields.</span><span class="sxs-lookup"><span data-stu-id="91c85-134">Refer to [policy definition](policy-definition.md#fields) for the list of acceptable fields.</span></span>

### <a name="append-examples"></a><span data-ttu-id="91c85-135">Append Examples</span><span class="sxs-lookup"><span data-stu-id="91c85-135">Append Examples</span></span>

<span data-ttu-id="91c85-136">Example 1: Single **field/value** pair to append a tag.</span><span class="sxs-lookup"><span data-stu-id="91c85-136">Example 1: Single **field/value** pair to append a tag.</span></span>

```json
"then": {
    "effect": "append",
    "details": [{
        "field": "tags.myTag",
        "value": "myTagValue"
    }]
}
```

<span data-ttu-id="91c85-137">Example 2: Multiple **field/value** pairs to append a set of tags.</span><span class="sxs-lookup"><span data-stu-id="91c85-137">Example 2: Multiple **field/value** pairs to append a set of tags.</span></span>

```json
"then": {
    "effect": "append",
    "details": [{
            "field": "tags.myTag",
            "value": "myTagValue"
        },
        {
            "field": "tags.myOtherTag",
            "value": "myOtherTagValue"
        }
    ]
}
```

<span data-ttu-id="91c85-138">Example 3: Single **field/value** pair using an [alias](policy-definition.md#aliases) with an array **value** to set IP rules on a storage account.</span><span class="sxs-lookup"><span data-stu-id="91c85-138">Example 3: Single **field/value** pair using an [alias](policy-definition.md#aliases) with an array **value** to set IP rules on a storage account.</span></span>

```json
"then": {
    "effect": "append",
    "details": [{
        "field": "Microsoft.Storage/storageAccounts/networkAcls.ipRules",
        "value": [{
            "action": "Allow",
            "value": "134.5.0.0/21"
        }]
    }]
}
```

## <a name="deny"></a><span data-ttu-id="91c85-139">Deny</span><span class="sxs-lookup"><span data-stu-id="91c85-139">Deny</span></span>

<span data-ttu-id="91c85-140">Deny is used to prevent a resource request that doesn't match desired standards through a policy definition and fails the request.</span><span class="sxs-lookup"><span data-stu-id="91c85-140">Deny is used to prevent a resource request that doesn't match desired standards through a policy definition and fails the request.</span></span>

### <a name="deny-evaluation"></a><span data-ttu-id="91c85-141">Deny Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-141">Deny Evaluation</span></span>

<span data-ttu-id="91c85-142">When creating or updating a resource, deny prevents the request prior to being sent to the Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="91c85-142">When creating or updating a resource, deny prevents the request prior to being sent to the Resource Provider.</span></span> <span data-ttu-id="91c85-143">The request is returned as a 403 (Forbidden).</span><span class="sxs-lookup"><span data-stu-id="91c85-143">The request is returned as a 403 (Forbidden).</span></span> <span data-ttu-id="91c85-144">In the portal, the Forbidden can be viewed as a status on the deployment that was prevented due to the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="91c85-144">In the portal, the Forbidden can be viewed as a status on the deployment that was prevented due to the policy assignment.</span></span>

<span data-ttu-id="91c85-145">During an evaluation cycle, policy definitions with a deny effect that match resources are marked as non-compliant, but no action is performed on that resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-145">During an evaluation cycle, policy definitions with a deny effect that match resources are marked as non-compliant, but no action is performed on that resource.</span></span>

### <a name="deny-properties"></a><span data-ttu-id="91c85-146">Deny Properties</span><span class="sxs-lookup"><span data-stu-id="91c85-146">Deny Properties</span></span>

<span data-ttu-id="91c85-147">The deny effect does not have any additional properties for use in the **then** condition of the policy definition.</span><span class="sxs-lookup"><span data-stu-id="91c85-147">The deny effect does not have any additional properties for use in the **then** condition of the policy definition.</span></span>

### <a name="deny-example"></a><span data-ttu-id="91c85-148">Deny Example</span><span class="sxs-lookup"><span data-stu-id="91c85-148">Deny Example</span></span>

<span data-ttu-id="91c85-149">Example: Using the deny effect.</span><span class="sxs-lookup"><span data-stu-id="91c85-149">Example: Using the deny effect.</span></span>

```json
"then": {
    "effect": "deny"
}
```

## <a name="audit"></a><span data-ttu-id="91c85-150">Audit</span><span class="sxs-lookup"><span data-stu-id="91c85-150">Audit</span></span>

<span data-ttu-id="91c85-151">Audit effect is used to create a warning event in the activity log when a non-compliant resource is evaluated, but it does not stop the request.</span><span class="sxs-lookup"><span data-stu-id="91c85-151">Audit effect is used to create a warning event in the activity log when a non-compliant resource is evaluated, but it does not stop the request.</span></span>

### <a name="audit-evaluation"></a><span data-ttu-id="91c85-152">Audit Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-152">Audit Evaluation</span></span>

<span data-ttu-id="91c85-153">The audit effect is the last to run during the creation or update of a resource prior to the resource is sent to the Resource Provider.</span><span class="sxs-lookup"><span data-stu-id="91c85-153">The audit effect is the last to run during the creation or update of a resource prior to the resource is sent to the Resource Provider.</span></span> <span data-ttu-id="91c85-154">Audit works the same for a resource request and an evaluation cycle, and executes a `Microsoft.Authorization/policies/audit/action` operation to the activity log.</span><span class="sxs-lookup"><span data-stu-id="91c85-154">Audit works the same for a resource request and an evaluation cycle, and executes a `Microsoft.Authorization/policies/audit/action` operation to the activity log.</span></span> <span data-ttu-id="91c85-155">In both cases, the resource is marked as non-compliant.</span><span class="sxs-lookup"><span data-stu-id="91c85-155">In both cases, the resource is marked as non-compliant.</span></span>

### <a name="audit-properties"></a><span data-ttu-id="91c85-156">Audit Properties</span><span class="sxs-lookup"><span data-stu-id="91c85-156">Audit Properties</span></span>

<span data-ttu-id="91c85-157">The audit effect does not have any additional properties for use in the **then** condition of the policy definition.</span><span class="sxs-lookup"><span data-stu-id="91c85-157">The audit effect does not have any additional properties for use in the **then** condition of the policy definition.</span></span>

### <a name="audit-example"></a><span data-ttu-id="91c85-158">Audit Example</span><span class="sxs-lookup"><span data-stu-id="91c85-158">Audit Example</span></span>

<span data-ttu-id="91c85-159">Example: Using the audit effect.</span><span class="sxs-lookup"><span data-stu-id="91c85-159">Example: Using the audit effect.</span></span>

```json
"then": {
    "effect": "audit"
}
```

## <a name="auditifnotexists"></a><span data-ttu-id="91c85-160">AuditIfNotExists</span><span class="sxs-lookup"><span data-stu-id="91c85-160">AuditIfNotExists</span></span>

<span data-ttu-id="91c85-161">AuditIfNotExists enables auditing on a resource that matches the **if** condition, but does not have the components specified in the **details** of the **then** condition.</span><span class="sxs-lookup"><span data-stu-id="91c85-161">AuditIfNotExists enables auditing on a resource that matches the **if** condition, but does not have the components specified in the **details** of the **then** condition.</span></span>

### <a name="auditifnotexists-evaluation"></a><span data-ttu-id="91c85-162">AuditIfNotExists Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-162">AuditIfNotExists Evaluation</span></span>

<span data-ttu-id="91c85-163">AuditIfNotExists runs after a Resource Provider has handled a create or update request to a resource and has returned a success status code.</span><span class="sxs-lookup"><span data-stu-id="91c85-163">AuditIfNotExists runs after a Resource Provider has handled a create or update request to a resource and has returned a success status code.</span></span> <span data-ttu-id="91c85-164">The effect is triggered if there are no related resources or if the resources defined by **ExistenceCondition** do not evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="91c85-164">The effect is triggered if there are no related resources or if the resources defined by **ExistenceCondition** do not evaluate to true.</span></span> <span data-ttu-id="91c85-165">When the effect is triggered, a `Microsoft.Authorization/policies/audit/action` operation to the activity log is executed in the same way as the audit effect.</span><span class="sxs-lookup"><span data-stu-id="91c85-165">When the effect is triggered, a `Microsoft.Authorization/policies/audit/action` operation to the activity log is executed in the same way as the audit effect.</span></span> <span data-ttu-id="91c85-166">When triggered, the resource that satisfied the **if** condition is the resource that is marked as non-compliant.</span><span class="sxs-lookup"><span data-stu-id="91c85-166">When triggered, the resource that satisfied the **if** condition is the resource that is marked as non-compliant.</span></span>

### <a name="auditifnotexists-properties"></a><span data-ttu-id="91c85-167">AuditIfNotExists Properties</span><span class="sxs-lookup"><span data-stu-id="91c85-167">AuditIfNotExists Properties</span></span>

<span data-ttu-id="91c85-168">The **details** property of the AuditIfNotExists effects has all the subproperties that define the related resources to match.</span><span class="sxs-lookup"><span data-stu-id="91c85-168">The **details** property of the AuditIfNotExists effects has all the subproperties that define the related resources to match.</span></span>

- <span data-ttu-id="91c85-169">**Type** [required]</span><span class="sxs-lookup"><span data-stu-id="91c85-169">**Type** [required]</span></span>
  - <span data-ttu-id="91c85-170">Specifies the type of the related resource to match.</span><span class="sxs-lookup"><span data-stu-id="91c85-170">Specifies the type of the related resource to match.</span></span>
  - <span data-ttu-id="91c85-171">Starts by trying to fetch a resource underneath the **if** condition resource, then queries within the same resource group as the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-171">Starts by trying to fetch a resource underneath the **if** condition resource, then queries within the same resource group as the **if** condition resource.</span></span>
- <span data-ttu-id="91c85-172">**Name** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-172">**Name** (optional)</span></span>
  - <span data-ttu-id="91c85-173">Specifies the exact name of the resource to match and causes the policy to fetch one specific resource instead of all resources of the specified type.</span><span class="sxs-lookup"><span data-stu-id="91c85-173">Specifies the exact name of the resource to match and causes the policy to fetch one specific resource instead of all resources of the specified type.</span></span>
- <span data-ttu-id="91c85-174">**ResourceGroupName** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-174">**ResourceGroupName** (optional)</span></span>
  - <span data-ttu-id="91c85-175">Allows the matching of the related resource to come from a different resource group.</span><span class="sxs-lookup"><span data-stu-id="91c85-175">Allows the matching of the related resource to come from a different resource group.</span></span>
  - <span data-ttu-id="91c85-176">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-176">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span></span>
  - <span data-ttu-id="91c85-177">Default is the **if** condition resource's resource group.</span><span class="sxs-lookup"><span data-stu-id="91c85-177">Default is the **if** condition resource's resource group.</span></span>
- <span data-ttu-id="91c85-178">**ExistenceScope** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-178">**ExistenceScope** (optional)</span></span>
  - <span data-ttu-id="91c85-179">Allowed values are _Subscription_ and _ResourceGroup_.</span><span class="sxs-lookup"><span data-stu-id="91c85-179">Allowed values are _Subscription_ and _ResourceGroup_.</span></span>
  - <span data-ttu-id="91c85-180">Sets the scope of where to fetch the related resource to match from.</span><span class="sxs-lookup"><span data-stu-id="91c85-180">Sets the scope of where to fetch the related resource to match from.</span></span>
  - <span data-ttu-id="91c85-181">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-181">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span></span>
  - <span data-ttu-id="91c85-182">For _ResourceGroup_, would limit to the **if** condition resource's resource group or the resource group specified in **ResourceGroupName**.</span><span class="sxs-lookup"><span data-stu-id="91c85-182">For _ResourceGroup_, would limit to the **if** condition resource's resource group or the resource group specified in **ResourceGroupName**.</span></span>
  - <span data-ttu-id="91c85-183">For _Subscription_, queries the entire subscription for the related resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-183">For _Subscription_, queries the entire subscription for the related resource.</span></span>
  - <span data-ttu-id="91c85-184">Default is _ResourceGroup_.</span><span class="sxs-lookup"><span data-stu-id="91c85-184">Default is _ResourceGroup_.</span></span>
- <span data-ttu-id="91c85-185">**ExistenceCondition** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-185">**ExistenceCondition** (optional)</span></span>
  - <span data-ttu-id="91c85-186">If not specified, any related resource of **type** satisfies the effect and does not trigger the audit.</span><span class="sxs-lookup"><span data-stu-id="91c85-186">If not specified, any related resource of **type** satisfies the effect and does not trigger the audit.</span></span>
  - <span data-ttu-id="91c85-187">Uses the same language as the policy rule for the **if** condition, but is evaluated against each related resource individually.</span><span class="sxs-lookup"><span data-stu-id="91c85-187">Uses the same language as the policy rule for the **if** condition, but is evaluated against each related resource individually.</span></span>
  - <span data-ttu-id="91c85-188">If any matching related resource evaluates to true, the effect is satisfied and does not trigger the audit.</span><span class="sxs-lookup"><span data-stu-id="91c85-188">If any matching related resource evaluates to true, the effect is satisfied and does not trigger the audit.</span></span>
  - <span data-ttu-id="91c85-189">Can use [field()] to check equivalence with values in the **if** condition.</span><span class="sxs-lookup"><span data-stu-id="91c85-189">Can use [field()] to check equivalence with values in the **if** condition.</span></span>
  - <span data-ttu-id="91c85-190">For example, could be used to validate that the parent resource (in the **if** condition) is in the same resource location as the matching related resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-190">For example, could be used to validate that the parent resource (in the **if** condition) is in the same resource location as the matching related resource.</span></span>

### <a name="auditifnotexists-example"></a><span data-ttu-id="91c85-191">AuditIfNotExists Example</span><span class="sxs-lookup"><span data-stu-id="91c85-191">AuditIfNotExists Example</span></span>

<span data-ttu-id="91c85-192">Example: Evaluates Virtual Machines to determine if the Antimalware extension exists then audits when missing.</span><span class="sxs-lookup"><span data-stu-id="91c85-192">Example: Evaluates Virtual Machines to determine if the Antimalware extension exists then audits when missing.</span></span>

```json
{
    "if": {
        "field": "type",
        "equals": "Microsoft.Compute/virtualMachines"
    },
    "then": {
        "effect": "auditIfNotExists",
        "details": {
            "type": "Microsoft.Compute/virtualMachines/extensions",
            "existenceCondition": {
                "allOf": [{
                        "field": "Microsoft.Compute/virtualMachines/extensions/publisher",
                        "equals": "Microsoft.Azure.Security"
                    },
                    {
                        "field": "Microsoft.Compute/virtualMachines/extensions/type",
                        "equals": "IaaSAntimalware"
                    }
                ]
            }
        }
    }
}
```

## <a name="deployifnotexists"></a><span data-ttu-id="91c85-193">DeployIfNotExists</span><span class="sxs-lookup"><span data-stu-id="91c85-193">DeployIfNotExists</span></span>

<span data-ttu-id="91c85-194">Similar to AuditIfNotExists, DeployIfNotExists executes a template deployment when the condition is met.</span><span class="sxs-lookup"><span data-stu-id="91c85-194">Similar to AuditIfNotExists, DeployIfNotExists executes a template deployment when the condition is met.</span></span>

> [!WARNING]
> <span data-ttu-id="91c85-195">DeployIfNotExists is only available to **built-in** policies.</span><span class="sxs-lookup"><span data-stu-id="91c85-195">DeployIfNotExists is only available to **built-in** policies.</span></span>

### <a name="deployifnotexists-evaluation"></a><span data-ttu-id="91c85-196">DeployIfNotExists Evaluation</span><span class="sxs-lookup"><span data-stu-id="91c85-196">DeployIfNotExists Evaluation</span></span>

<span data-ttu-id="91c85-197">DeployIfNotExists also runs after a Resource Provider has handled a create or update request to a resource and has returned a success status code.</span><span class="sxs-lookup"><span data-stu-id="91c85-197">DeployIfNotExists also runs after a Resource Provider has handled a create or update request to a resource and has returned a success status code.</span></span> <span data-ttu-id="91c85-198">The effect is triggered if there are no related resources or if the resources defined by **ExistenceCondition** do not evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="91c85-198">The effect is triggered if there are no related resources or if the resources defined by **ExistenceCondition** do not evaluate to true.</span></span> <span data-ttu-id="91c85-199">When the effect is triggered, a template deployment is executed.</span><span class="sxs-lookup"><span data-stu-id="91c85-199">When the effect is triggered, a template deployment is executed.</span></span>

<span data-ttu-id="91c85-200">During an evaluation cycle, policy definitions with a DeployIfNotExists effect that match resources are marked as non-compliant, but no action is performed on that resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-200">During an evaluation cycle, policy definitions with a DeployIfNotExists effect that match resources are marked as non-compliant, but no action is performed on that resource.</span></span>

### <a name="deployifnotexists-properties"></a><span data-ttu-id="91c85-201">DeployIfNotExists Properties</span><span class="sxs-lookup"><span data-stu-id="91c85-201">DeployIfNotExists Properties</span></span>

<span data-ttu-id="91c85-202">The **details** property of the DeployIfNotExists effects has all the subproperties that define the related resources to match and the template deployment to execute.</span><span class="sxs-lookup"><span data-stu-id="91c85-202">The **details** property of the DeployIfNotExists effects has all the subproperties that define the related resources to match and the template deployment to execute.</span></span>

- <span data-ttu-id="91c85-203">**Type** [required]</span><span class="sxs-lookup"><span data-stu-id="91c85-203">**Type** [required]</span></span>
  - <span data-ttu-id="91c85-204">Specifies the type of the related resource to match.</span><span class="sxs-lookup"><span data-stu-id="91c85-204">Specifies the type of the related resource to match.</span></span>
  - <span data-ttu-id="91c85-205">Starts by trying to fetch a resource underneath the **if** condition resource, then queries within the same resource group as the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-205">Starts by trying to fetch a resource underneath the **if** condition resource, then queries within the same resource group as the **if** condition resource.</span></span>
- <span data-ttu-id="91c85-206">**Name** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-206">**Name** (optional)</span></span>
  - <span data-ttu-id="91c85-207">Specifies the exact name of the resource to match and causes the policy to fetch one specific resource instead of all resources of the specified type.</span><span class="sxs-lookup"><span data-stu-id="91c85-207">Specifies the exact name of the resource to match and causes the policy to fetch one specific resource instead of all resources of the specified type.</span></span>
- <span data-ttu-id="91c85-208">**ResourceGroupName** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-208">**ResourceGroupName** (optional)</span></span>
  - <span data-ttu-id="91c85-209">Allows the matching of the related resource to come from a different resource group.</span><span class="sxs-lookup"><span data-stu-id="91c85-209">Allows the matching of the related resource to come from a different resource group.</span></span>
  - <span data-ttu-id="91c85-210">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-210">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span></span>
  - <span data-ttu-id="91c85-211">Default is the **if** condition resource's resource group.</span><span class="sxs-lookup"><span data-stu-id="91c85-211">Default is the **if** condition resource's resource group.</span></span>
  - <span data-ttu-id="91c85-212">If a template deployment is executed, it is deployed in the resource group of this value.</span><span class="sxs-lookup"><span data-stu-id="91c85-212">If a template deployment is executed, it is deployed in the resource group of this value.</span></span>
- <span data-ttu-id="91c85-213">**ExistenceScope** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-213">**ExistenceScope** (optional)</span></span>
  - <span data-ttu-id="91c85-214">Allowed values are _Subscription_ and _ResourceGroup_.</span><span class="sxs-lookup"><span data-stu-id="91c85-214">Allowed values are _Subscription_ and _ResourceGroup_.</span></span>
  - <span data-ttu-id="91c85-215">Sets the scope of where to fetch the related resource to match from.</span><span class="sxs-lookup"><span data-stu-id="91c85-215">Sets the scope of where to fetch the related resource to match from.</span></span>
  - <span data-ttu-id="91c85-216">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-216">Does not apply if **type** is a resource that would be underneath the **if** condition resource.</span></span>
  - <span data-ttu-id="91c85-217">For _ResourceGroup_, would limit to the **if** condition resource's resource group or the resource group specified in **ResourceGroupName**.</span><span class="sxs-lookup"><span data-stu-id="91c85-217">For _ResourceGroup_, would limit to the **if** condition resource's resource group or the resource group specified in **ResourceGroupName**.</span></span>
  - <span data-ttu-id="91c85-218">For _Subscription_, queries the entire subscription for the related resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-218">For _Subscription_, queries the entire subscription for the related resource.</span></span>
  - <span data-ttu-id="91c85-219">Default is _ResourceGroup_.</span><span class="sxs-lookup"><span data-stu-id="91c85-219">Default is _ResourceGroup_.</span></span>
- <span data-ttu-id="91c85-220">**ExistenceCondition** (optional)</span><span class="sxs-lookup"><span data-stu-id="91c85-220">**ExistenceCondition** (optional)</span></span>
  - <span data-ttu-id="91c85-221">If not specified, any related resource of **type** satisfies the effect and does not trigger the deployment.</span><span class="sxs-lookup"><span data-stu-id="91c85-221">If not specified, any related resource of **type** satisfies the effect and does not trigger the deployment.</span></span>
  - <span data-ttu-id="91c85-222">Uses the same language as the policy rule for the **if** condition, but is evaluated against each related resource individually.</span><span class="sxs-lookup"><span data-stu-id="91c85-222">Uses the same language as the policy rule for the **if** condition, but is evaluated against each related resource individually.</span></span>
  - <span data-ttu-id="91c85-223">If any matching related resource evaluates to true, the effect is satisfied and does not trigger the deployment.</span><span class="sxs-lookup"><span data-stu-id="91c85-223">If any matching related resource evaluates to true, the effect is satisfied and does not trigger the deployment.</span></span>
  - <span data-ttu-id="91c85-224">Can use [field()] to check equivalence with values in the **if** condition.</span><span class="sxs-lookup"><span data-stu-id="91c85-224">Can use [field()] to check equivalence with values in the **if** condition.</span></span>
  - <span data-ttu-id="91c85-225">For example, could be used to validate that the parent resource (in the **if** condition) is in the same resource location as the matching related resource.</span><span class="sxs-lookup"><span data-stu-id="91c85-225">For example, could be used to validate that the parent resource (in the **if** condition) is in the same resource location as the matching related resource.</span></span>
- <span data-ttu-id="91c85-226">**Deployment** [required]</span><span class="sxs-lookup"><span data-stu-id="91c85-226">**Deployment** [required]</span></span>
  - <span data-ttu-id="91c85-227">This property should contain the full template deployment as it would be passed to the `Microsoft.Resources/deployments` PUT API.</span><span class="sxs-lookup"><span data-stu-id="91c85-227">This property should contain the full template deployment as it would be passed to the `Microsoft.Resources/deployments` PUT API.</span></span> <span data-ttu-id="91c85-228">For more information, see the [Deployments REST API](/rest/api/resources/deployments).</span><span class="sxs-lookup"><span data-stu-id="91c85-228">For more information, see the [Deployments REST API](/rest/api/resources/deployments).</span></span>

  > [!NOTE]
  > <span data-ttu-id="91c85-229">All functions inside the **Deployment** property are evaluated as components of the template, not the policy.</span><span class="sxs-lookup"><span data-stu-id="91c85-229">All functions inside the **Deployment** property are evaluated as components of the template, not the policy.</span></span> <span data-ttu-id="91c85-230">The exception is the **parameters** property that passes values from the policy to the template.</span><span class="sxs-lookup"><span data-stu-id="91c85-230">The exception is the **parameters** property that passes values from the policy to the template.</span></span> <span data-ttu-id="91c85-231">The **value** in this section under a template parameter name is used to perform this value passing (see _fullDbName_ in the DeployIfNotExists example).</span><span class="sxs-lookup"><span data-stu-id="91c85-231">The **value** in this section under a template parameter name is used to perform this value passing (see _fullDbName_ in the DeployIfNotExists example).</span></span>

### <a name="deployifnotexists-example"></a><span data-ttu-id="91c85-232">DeployIfNotExists Example</span><span class="sxs-lookup"><span data-stu-id="91c85-232">DeployIfNotExists Example</span></span>

<span data-ttu-id="91c85-233">Example: Evaluates SQL Server databases to determine if transparentDataEncryption is enabled.</span><span class="sxs-lookup"><span data-stu-id="91c85-233">Example: Evaluates SQL Server databases to determine if transparentDataEncryption is enabled.</span></span> <span data-ttu-id="91c85-234">If not, then a deployment to enable it is executed.</span><span class="sxs-lookup"><span data-stu-id="91c85-234">If not, then a deployment to enable it is executed.</span></span>

```json
"if": {
    "field": "type",
    "equals": "Microsoft.Sql/servers/databases"
},
"then": {
    "effect": "DeployIfNotExists",
    "details": {
        "type": "Microsoft.Sql/servers/databases/transparentDataEncryption",
        "name": "current",
        "existenceCondition": {
            "field": "Microsoft.Sql/transparentDataEncryption.status",
            "equals": "Enabled"
        },
        "deployment": {
            "properties": {
                "mode": "incremental",
                "template": {
                    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {
                        "fullDbName": {
                            "type": "string"
                        }
                    },
                    "resources": [{
                        "name": "[concat(parameters('fullDbName'), '/current')]",
                        "type": "Microsoft.Sql/servers/databases/transparentDataEncryption",
                        "apiVersion": "2014-04-01",
                        "properties": {
                            "status": "Enabled"
                        }
                    }]
                },
                "parameters": {
                    "fullDbName": {
                        "value": "[field('fullName')]"
                    }
                }
            }
        }
    }
}
```

## <a name="layering-policies"></a><span data-ttu-id="91c85-235">Layering policies</span><span class="sxs-lookup"><span data-stu-id="91c85-235">Layering policies</span></span>

<span data-ttu-id="91c85-236">A resource may be impacted by multiple assignments.</span><span class="sxs-lookup"><span data-stu-id="91c85-236">A resource may be impacted by multiple assignments.</span></span> <span data-ttu-id="91c85-237">These assignments may be at the same scope (specific resource, resource group, subscription, or management group) or at different scopes.</span><span class="sxs-lookup"><span data-stu-id="91c85-237">These assignments may be at the same scope (specific resource, resource group, subscription, or management group) or at different scopes.</span></span> <span data-ttu-id="91c85-238">Each of these assignments is also likely to have a different effect defined.</span><span class="sxs-lookup"><span data-stu-id="91c85-238">Each of these assignments is also likely to have a different effect defined.</span></span> <span data-ttu-id="91c85-239">Regardless, the condition and effect for each policy (assigned directly or as part of an initiative) is independently evaluated.</span><span class="sxs-lookup"><span data-stu-id="91c85-239">Regardless, the condition and effect for each policy (assigned directly or as part of an initiative) is independently evaluated.</span></span> <span data-ttu-id="91c85-240">For example, if policy 1 has a condition that restricts resource location for subscription A to only be created in ‘westus’ with the deny effect and policy 2 has a condition that restricts resource location for resource group B (which is in subscription A) to only be created in ‘eastus’ with the audit effect are both assigned, the resulting outcome would be::</span><span class="sxs-lookup"><span data-stu-id="91c85-240">For example, if policy 1 has a condition that restricts resource location for subscription A to only be created in ‘westus’ with the deny effect and policy 2 has a condition that restricts resource location for resource group B (which is in subscription A) to only be created in ‘eastus’ with the audit effect are both assigned, the resulting outcome would be::</span></span>

- <span data-ttu-id="91c85-241">Any resource already in resource group B in 'eastus' is compliant to policy 2, but marked as non-compliant to policy 1.</span><span class="sxs-lookup"><span data-stu-id="91c85-241">Any resource already in resource group B in 'eastus' is compliant to policy 2, but marked as non-compliant to policy 1.</span></span>
- <span data-ttu-id="91c85-242">Any resource already in resource group B not in 'eastus' will be marked as non-compliant to policy 2, and would also be marked not-compliant to policy 1 if not 'westus'.</span><span class="sxs-lookup"><span data-stu-id="91c85-242">Any resource already in resource group B not in 'eastus' will be marked as non-compliant to policy 2, and would also be marked not-compliant to policy 1 if not 'westus'.</span></span>
- <span data-ttu-id="91c85-243">Any new resource in subscription A not in 'westus' would be denied by policy 1.</span><span class="sxs-lookup"><span data-stu-id="91c85-243">Any new resource in subscription A not in 'westus' would be denied by policy 1.</span></span>
- <span data-ttu-id="91c85-244">Any new resource in subscription A / resource group B in 'westus' would be marked as non-compliant on policy 2, but would be created (compliant to policy 1 and policy 2 is audit and not deny).</span><span class="sxs-lookup"><span data-stu-id="91c85-244">Any new resource in subscription A / resource group B in 'westus' would be marked as non-compliant on policy 2, but would be created (compliant to policy 1 and policy 2 is audit and not deny).</span></span>

<span data-ttu-id="91c85-245">If both policy 1 and policy 2 had effect of deny, the situation would change to:</span><span class="sxs-lookup"><span data-stu-id="91c85-245">If both policy 1 and policy 2 had effect of deny, the situation would change to:</span></span>

- <span data-ttu-id="91c85-246">Any resource already in resource group B not in 'eastus' will be marked as non-compliant to policy 2.</span><span class="sxs-lookup"><span data-stu-id="91c85-246">Any resource already in resource group B not in 'eastus' will be marked as non-compliant to policy 2.</span></span>
- <span data-ttu-id="91c85-247">Any resource already in resource group B not in 'westus' will be marked as non-compliant to policy 1.</span><span class="sxs-lookup"><span data-stu-id="91c85-247">Any resource already in resource group B not in 'westus' will be marked as non-compliant to policy 1.</span></span>
- <span data-ttu-id="91c85-248">Any new resource in subscription A not in 'westus' would be denied by policy 1.</span><span class="sxs-lookup"><span data-stu-id="91c85-248">Any new resource in subscription A not in 'westus' would be denied by policy 1.</span></span>
- <span data-ttu-id="91c85-249">Any new resource in subscription A / resource group B would be denied (since its location could never satisfy both policy 1 and policy 2).</span><span class="sxs-lookup"><span data-stu-id="91c85-249">Any new resource in subscription A / resource group B would be denied (since its location could never satisfy both policy 1 and policy 2).</span></span>

<span data-ttu-id="91c85-250">As each assignment is individually evaluated, there isn't an opportunity for a resource to slip through a gap due to differences in scope.</span><span class="sxs-lookup"><span data-stu-id="91c85-250">As each assignment is individually evaluated, there isn't an opportunity for a resource to slip through a gap due to differences in scope.</span></span> <span data-ttu-id="91c85-251">Therefore, the net result of layering policies or policy overlap is considered to be **cumulative most restrictive**.</span><span class="sxs-lookup"><span data-stu-id="91c85-251">Therefore, the net result of layering policies or policy overlap is considered to be **cumulative most restrictive**.</span></span> <span data-ttu-id="91c85-252">In other words, a resource you want created could be blocked due to overlapping and conflicting policies such as the example above if both policy 1 and policy 2 had a deny effect.</span><span class="sxs-lookup"><span data-stu-id="91c85-252">In other words, a resource you want created could be blocked due to overlapping and conflicting policies such as the example above if both policy 1 and policy 2 had a deny effect.</span></span> <span data-ttu-id="91c85-253">If you still need the resource to be created in the target scope, review the exclusions on each assignment to ensure the right policies are affecting the right scopes.</span><span class="sxs-lookup"><span data-stu-id="91c85-253">If you still need the resource to be created in the target scope, review the exclusions on each assignment to ensure the right policies are affecting the right scopes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="91c85-254">Next steps</span><span class="sxs-lookup"><span data-stu-id="91c85-254">Next steps</span></span>

<span data-ttu-id="91c85-255">Now that you have a deeper understanding of policy definition effects, review the policy samples:</span><span class="sxs-lookup"><span data-stu-id="91c85-255">Now that you have a deeper understanding of policy definition effects, review the policy samples:</span></span>

- <span data-ttu-id="91c85-256">Review more examples at [Azure Policy samples](json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="91c85-256">Review more examples at [Azure Policy samples](json-samples.md).</span></span>
