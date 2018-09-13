---
title: Use Azure Policy to create and manage policies to enforce organizational compliance
description: Use Azure Policy to enforce standards, meet regulatory compliance and audit requirements, control costs, maintain security and performance consistency, and impose enterprise wide design principles.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 08/22/2018
ms.topic: tutorial
ms.service: azure-policy
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 68ee6b64baf4284bbd0977e82fc473a58a59874c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866372"
---
# <a name="create-and-manage-policies-to-enforce-compliance"></a><span data-ttu-id="dde95-103">Create and manage policies to enforce compliance</span><span class="sxs-lookup"><span data-stu-id="dde95-103">Create and manage policies to enforce compliance</span></span>

<span data-ttu-id="dde95-104">Understanding how to create and manage policies in Azure is important for staying compliant with your corporate standards and service level agreements.</span><span class="sxs-lookup"><span data-stu-id="dde95-104">Understanding how to create and manage policies in Azure is important for staying compliant with your corporate standards and service level agreements.</span></span> <span data-ttu-id="dde95-105">In this tutorial, you learn to use Azure Policy to do some of the more common tasks related to creating, assigning, and managing policies across your organization, such as:</span><span class="sxs-lookup"><span data-stu-id="dde95-105">In this tutorial, you learn to use Azure Policy to do some of the more common tasks related to creating, assigning, and managing policies across your organization, such as:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="dde95-106">Assign a policy to enforce a condition for resources you create in the future</span><span class="sxs-lookup"><span data-stu-id="dde95-106">Assign a policy to enforce a condition for resources you create in the future</span></span>
> - <span data-ttu-id="dde95-107">Create and assign an initiative definition to track compliance for multiple resources</span><span class="sxs-lookup"><span data-stu-id="dde95-107">Create and assign an initiative definition to track compliance for multiple resources</span></span>
> - <span data-ttu-id="dde95-108">Resolve a non-compliant or denied resource</span><span class="sxs-lookup"><span data-stu-id="dde95-108">Resolve a non-compliant or denied resource</span></span>
> - <span data-ttu-id="dde95-109">Implement a new policy across an organization</span><span class="sxs-lookup"><span data-stu-id="dde95-109">Implement a new policy across an organization</span></span>

<span data-ttu-id="dde95-110">If you would like to assign a policy to identify the current compliance state of your existing resources, the quickstart articles go over how to do so.</span><span class="sxs-lookup"><span data-stu-id="dde95-110">If you would like to assign a policy to identify the current compliance state of your existing resources, the quickstart articles go over how to do so.</span></span> <span data-ttu-id="dde95-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="dde95-111">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="assign-a-policy"></a><span data-ttu-id="dde95-112">Assign a policy</span><span class="sxs-lookup"><span data-stu-id="dde95-112">Assign a policy</span></span>

<span data-ttu-id="dde95-113">The first step in enforcing compliance with Azure Policy is to assign a policy definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-113">The first step in enforcing compliance with Azure Policy is to assign a policy definition.</span></span> <span data-ttu-id="dde95-114">A policy definition defines under what condition a policy is enforced and what effect to take.</span><span class="sxs-lookup"><span data-stu-id="dde95-114">A policy definition defines under what condition a policy is enforced and what effect to take.</span></span> <span data-ttu-id="dde95-115">In this example, assign a built-in policy definition, called *Require SQL Server version 12.0*, to enforce the condition that all SQL Server databases must be v12.0 to be compliant.</span><span class="sxs-lookup"><span data-stu-id="dde95-115">In this example, assign a built-in policy definition, called *Require SQL Server version 12.0*, to enforce the condition that all SQL Server databases must be v12.0 to be compliant.</span></span>

1. <span data-ttu-id="dde95-116">Launch the Azure Policy service in the Azure portal by clicking **All services**, then searching for and selecting **Policy**.</span><span class="sxs-lookup"><span data-stu-id="dde95-116">Launch the Azure Policy service in the Azure portal by clicking **All services**, then searching for and selecting **Policy**.</span></span>

   ![Search for policy](media/create-manage-policy/search-policy.png)

1. <span data-ttu-id="dde95-118">Select **Assignments** on the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-118">Select **Assignments** on the left side of the Azure Policy page.</span></span> <span data-ttu-id="dde95-119">An assignment is a policy that has been assigned to take place within a specific scope.</span><span class="sxs-lookup"><span data-stu-id="dde95-119">An assignment is a policy that has been assigned to take place within a specific scope.</span></span>
1. <span data-ttu-id="dde95-120">Select **Assign Policy** from the top of the **Policy - Assignments** page.</span><span class="sxs-lookup"><span data-stu-id="dde95-120">Select **Assign Policy** from the top of the **Policy - Assignments** page.</span></span>

   ![Assign a policy definition](media/create-manage-policy/select-assign-policy.png)

1. <span data-ttu-id="dde95-122">On the **Assign Policy** page, select the **Scope** by clicking the ellipsis and selecting a subscription (required) and resource group (optional).</span><span class="sxs-lookup"><span data-stu-id="dde95-122">On the **Assign Policy** page, select the **Scope** by clicking the ellipsis and selecting a subscription (required) and resource group (optional).</span></span> <span data-ttu-id="dde95-123">A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span><span class="sxs-lookup"><span data-stu-id="dde95-123">A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span></span>  <span data-ttu-id="dde95-124">Then click **Select** at the bottom of the **Scope** page.</span><span class="sxs-lookup"><span data-stu-id="dde95-124">Then click **Select** at the bottom of the **Scope** page.</span></span>

   <span data-ttu-id="dde95-125">This example uses the **Contoso Subscription**.</span><span class="sxs-lookup"><span data-stu-id="dde95-125">This example uses the **Contoso Subscription**.</span></span> <span data-ttu-id="dde95-126">Your subscription will differ.</span><span class="sxs-lookup"><span data-stu-id="dde95-126">Your subscription will differ.</span></span>

1. <span data-ttu-id="dde95-127">If you wanted to exclude one or more resource groups (if you only scoped a subscription) or specific resources within a resource group (either scoping case), you could configure **Exclusions** from the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-127">If you wanted to exclude one or more resource groups (if you only scoped a subscription) or specific resources within a resource group (either scoping case), you could configure **Exclusions** from the policy assignment.</span></span> <span data-ttu-id="dde95-128">Leave it blank for now.</span><span class="sxs-lookup"><span data-stu-id="dde95-128">Leave it blank for now.</span></span>

1. <span data-ttu-id="dde95-129">Select the **Policy definition** ellipsis to open the list of available definitions.</span><span class="sxs-lookup"><span data-stu-id="dde95-129">Select the **Policy definition** ellipsis to open the list of available definitions.</span></span> <span data-ttu-id="dde95-130">You can filter the policy definition **Type** to *Built-in* to view all and read their descriptions.</span><span class="sxs-lookup"><span data-stu-id="dde95-130">You can filter the policy definition **Type** to *Built-in* to view all and read their descriptions.</span></span>

1. <span data-ttu-id="dde95-131">Select **Require SQL Server version 12.0**.</span><span class="sxs-lookup"><span data-stu-id="dde95-131">Select **Require SQL Server version 12.0**.</span></span> <span data-ttu-id="dde95-132">If you cannot find it right away, type **require sql server** into the search box and then press ENTER or click out of the search box.</span><span class="sxs-lookup"><span data-stu-id="dde95-132">If you cannot find it right away, type **require sql server** into the search box and then press ENTER or click out of the search box.</span></span> <span data-ttu-id="dde95-133">Click **Select** at the bottom of the **Available Definitions** page once you have found and selected the policy definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-133">Click **Select** at the bottom of the **Available Definitions** page once you have found and selected the policy definition.</span></span>

   ![Locate a policy](media/create-manage-policy/select-available-definition.png)

1. <span data-ttu-id="dde95-135">The **Assignment name** is automatically populated with the policy name you selected, but you can change it.</span><span class="sxs-lookup"><span data-stu-id="dde95-135">The **Assignment name** is automatically populated with the policy name you selected, but you can change it.</span></span> <span data-ttu-id="dde95-136">For this example, leave *Require SQL Server version 12.0*.</span><span class="sxs-lookup"><span data-stu-id="dde95-136">For this example, leave *Require SQL Server version 12.0*.</span></span> <span data-ttu-id="dde95-137">You can also add an optional **Description**.</span><span class="sxs-lookup"><span data-stu-id="dde95-137">You can also add an optional **Description**.</span></span> <span data-ttu-id="dde95-138">The description provides details about this policy assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-138">The description provides details about this policy assignment.</span></span>

1. <span data-ttu-id="dde95-139">Click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="dde95-139">Click **Assign**.</span></span>

## <a name="implement-a-new-custom-policy"></a><span data-ttu-id="dde95-140">Implement a new custom policy</span><span class="sxs-lookup"><span data-stu-id="dde95-140">Implement a new custom policy</span></span>

<span data-ttu-id="dde95-141">Now that you've assigned a built-in policy definition, you can do more with Azure Policy.</span><span class="sxs-lookup"><span data-stu-id="dde95-141">Now that you've assigned a built-in policy definition, you can do more with Azure Policy.</span></span> <span data-ttu-id="dde95-142">Next, create a new custom policy to save costs by ensuring that VMs created in your environment cannot be in the G series.</span><span class="sxs-lookup"><span data-stu-id="dde95-142">Next, create a new custom policy to save costs by ensuring that VMs created in your environment cannot be in the G series.</span></span> <span data-ttu-id="dde95-143">This way, every time a user in your organization tries to create VM in the G series, the request is denied.</span><span class="sxs-lookup"><span data-stu-id="dde95-143">This way, every time a user in your organization tries to create VM in the G series, the request is denied.</span></span>

1. <span data-ttu-id="dde95-144">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-144">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span></span>

   ![Definition under authoring](media/create-manage-policy/definition-under-authoring.png)

1. <span data-ttu-id="dde95-146">Select **+ Policy definition** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="dde95-146">Select **+ Policy definition** at the top of the page.</span></span> <span data-ttu-id="dde95-147">This opens to the **Policy definition** page.</span><span class="sxs-lookup"><span data-stu-id="dde95-147">This opens to the **Policy definition** page.</span></span>
1. <span data-ttu-id="dde95-148">Enter the following:</span><span class="sxs-lookup"><span data-stu-id="dde95-148">Enter the following:</span></span>

   - <span data-ttu-id="dde95-149">The management group or subscription in which the policy definition is saved.</span><span class="sxs-lookup"><span data-stu-id="dde95-149">The management group or subscription in which the policy definition is saved.</span></span> <span data-ttu-id="dde95-150">Select by using the ellipsis on **Definition location**.</span><span class="sxs-lookup"><span data-stu-id="dde95-150">Select by using the ellipsis on **Definition location**.</span></span>

     > [!NOTE]
     > <span data-ttu-id="dde95-151">If you plan to apply this policy definition to multiple subscriptions, the location must be a management group that contains the subscriptions you will assign the policy to.</span><span class="sxs-lookup"><span data-stu-id="dde95-151">If you plan to apply this policy definition to multiple subscriptions, the location must be a management group that contains the subscriptions you will assign the policy to.</span></span> <span data-ttu-id="dde95-152">The same is true for an initiative definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-152">The same is true for an initiative definition.</span></span>

   - <span data-ttu-id="dde95-153">The name of the policy definition - *Require VM SKUs smaller than the G series*</span><span class="sxs-lookup"><span data-stu-id="dde95-153">The name of the policy definition - *Require VM SKUs smaller than the G series*</span></span>
   - <span data-ttu-id="dde95-154">The description of what the policy definition is intended to do – *This policy definition enforces that all VMs created in this scope have SKUs smaller than the G series to reduce cost.*</span><span class="sxs-lookup"><span data-stu-id="dde95-154">The description of what the policy definition is intended to do – *This policy definition enforces that all VMs created in this scope have SKUs smaller than the G series to reduce cost.*</span></span>
   - <span data-ttu-id="dde95-155">Choose from existing options, or create a new category for this policy definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-155">Choose from existing options, or create a new category for this policy definition.</span></span>
   - <span data-ttu-id="dde95-156">Copy the following json code and then update it for your needs with:</span><span class="sxs-lookup"><span data-stu-id="dde95-156">Copy the following json code and then update it for your needs with:</span></span>
      - <span data-ttu-id="dde95-157">The policy parameters.</span><span class="sxs-lookup"><span data-stu-id="dde95-157">The policy parameters.</span></span>
      - <span data-ttu-id="dde95-158">The policy rules/conditions, in this case – VM SKU size equal to G series</span><span class="sxs-lookup"><span data-stu-id="dde95-158">The policy rules/conditions, in this case – VM SKU size equal to G series</span></span>
      - <span data-ttu-id="dde95-159">The policy effect, in this case – **Deny**.</span><span class="sxs-lookup"><span data-stu-id="dde95-159">The policy effect, in this case – **Deny**.</span></span>

    <span data-ttu-id="dde95-160">Here's what the json should look like.</span><span class="sxs-lookup"><span data-stu-id="dde95-160">Here's what the json should look like.</span></span> <span data-ttu-id="dde95-161">Paste your revised code into the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="dde95-161">Paste your revised code into the Azure portal.</span></span>

    ```json
    {
        "policyRule": {
            "if": {
                "allOf": [{
                        "field": "type",
                        "equals": "Microsoft.Compute/virtualMachines"
                    },
                    {
                        "field": "Microsoft.Compute/virtualMachines/sku.name",
                        "like": "Standard_G*"
                    }
                ]
            },
            "then": {
                "effect": "deny"
            }
        }
    }
    ```

    <span data-ttu-id="dde95-162">The value of the *field* property in the policy rule must be one of the following: Name, Type, Location, Tags, or an alias.</span><span class="sxs-lookup"><span data-stu-id="dde95-162">The value of the *field* property in the policy rule must be one of the following: Name, Type, Location, Tags, or an alias.</span></span> <span data-ttu-id="dde95-163">An example of an alias might be `"Microsoft.Compute/VirtualMachines/Size"`.</span><span class="sxs-lookup"><span data-stu-id="dde95-163">An example of an alias might be `"Microsoft.Compute/VirtualMachines/Size"`.</span></span>

    <span data-ttu-id="dde95-164">To view more Azure policy samples, see [Templates for Azure Policy](json-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dde95-164">To view more Azure policy samples, see [Templates for Azure Policy](json-samples.md).</span></span>

1. <span data-ttu-id="dde95-165">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="dde95-165">Select **Save**.</span></span>

## <a name="create-a-policy-definition-with-rest-api"></a><span data-ttu-id="dde95-166">Create a policy definition with REST API</span><span class="sxs-lookup"><span data-stu-id="dde95-166">Create a policy definition with REST API</span></span>

<span data-ttu-id="dde95-167">You can create a policy with the REST API for Policy Definitions.</span><span class="sxs-lookup"><span data-stu-id="dde95-167">You can create a policy with the REST API for Policy Definitions.</span></span> <span data-ttu-id="dde95-168">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span><span class="sxs-lookup"><span data-stu-id="dde95-168">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>
<span data-ttu-id="dde95-169">To create a policy definition, use the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-169">To create a policy definition, use the following example:</span></span>

```http-interactive
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="dde95-170">Include a request body similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-170">Include a request body similar to the following example:</span></span>

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

## <a name="create-a-policy-definition-with-powershell"></a><span data-ttu-id="dde95-171">Create a policy definition with PowerShell</span><span class="sxs-lookup"><span data-stu-id="dde95-171">Create a policy definition with PowerShell</span></span>

<span data-ttu-id="dde95-172">Before proceeding with the PowerShell example, make sure you have installed the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="dde95-172">Before proceeding with the PowerShell example, make sure you have installed the latest version of Azure PowerShell.</span></span> <span data-ttu-id="dde95-173">Policy parameters were added in version 3.6.0.</span><span class="sxs-lookup"><span data-stu-id="dde95-173">Policy parameters were added in version 3.6.0.</span></span> <span data-ttu-id="dde95-174">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span><span class="sxs-lookup"><span data-stu-id="dde95-174">If you have an earlier version, the examples return an error indicating the parameter cannot be found.</span></span>

<span data-ttu-id="dde95-175">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="dde95-175">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span>

<span data-ttu-id="dde95-176">To create a policy definition from a file, pass the path to the file.</span><span class="sxs-lookup"><span data-stu-id="dde95-176">To create a policy definition from a file, pass the path to the file.</span></span> <span data-ttu-id="dde95-177">For an external file, use the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-177">For an external file, use the following example:</span></span>

```azurepowershell-interactive
$definition = New-AzureRmPolicyDefinition `
    -Name 'denyCoolTiering' `
    -DisplayName 'Deny cool access tiering for storage' `
    -Policy 'https://raw.githubusercontent.com/Azure/azure-policy-samples/master/samples/Storage/storage-account-access-tier/azurepolicy.rules.json'
```

<span data-ttu-id="dde95-178">For a local file use, use the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-178">For a local file use, use the following example:</span></span>

```azurepowershell-interactive
$definition = New-AzureRmPolicyDefinition `
    -Name 'denyCoolTiering' `
    -Description 'Deny cool access tiering for storage' `
    -Policy 'c:\policies\coolAccessTier.json'
```

<span data-ttu-id="dde95-179">To create a policy definition with an inline rule, use the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-179">To create a policy definition with an inline rule, use the following example:</span></span>

```azurepowershell-interactive
$definition = New-AzureRmPolicyDefinition -Name 'denyCoolTiering' -Description 'Deny cool access tiering for storage' -Policy '{
    "if": {
        "allOf": [{
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "field": "kind",
                "equals": "BlobStorage"
            },
            {
                "field": "Microsoft.Storage/storageAccounts/accessTier",
                "equals": "cool"
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}'
```

<span data-ttu-id="dde95-180">The output is stored in a `$definition` object, which is used during policy assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-180">The output is stored in a `$definition` object, which is used during policy assignment.</span></span>
<span data-ttu-id="dde95-181">The following example creates a policy definition that includes parameters:</span><span class="sxs-lookup"><span data-stu-id="dde95-181">The following example creates a policy definition that includes parameters:</span></span>

```azurepowershell-interactive
$policy = '{
    "if": {
        "allOf": [{
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "not": {
                    "field": "location",
                    "in": "[parameters(''allowedLocations'')]"
                }
            }
        ]
    },
    "then": {
        "effect": "Deny"
    }
}'

$parameters = '{
    "allowedLocations": {
        "type": "array",
        "metadata": {
            "description": "The list of locations that can be specified when deploying storage accounts.",
            "strongType": "location",
            "displayName": "Allowed locations"
        }
    }
}'

$definition = New-AzureRmPolicyDefinition -Name 'storageLocations' -Description 'Policy to specify locations for storage accounts.' -Policy $policy -Parameter $parameters
```

### <a name="view-policy-definitions-with-powershell"></a><span data-ttu-id="dde95-182">View policy definitions with PowerShell</span><span class="sxs-lookup"><span data-stu-id="dde95-182">View policy definitions with PowerShell</span></span>

<span data-ttu-id="dde95-183">To see all policy definitions in your subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dde95-183">To see all policy definitions in your subscription, use the following command:</span></span>

```azurepowershell-interactive
Get-AzureRmPolicyDefinition
```

<span data-ttu-id="dde95-184">It returns all available policy definitions, including built-in policies.</span><span class="sxs-lookup"><span data-stu-id="dde95-184">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="dde95-185">Each policy is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="dde95-185">Each policy is returned in the following format:</span></span>

```output
Name               : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceId         : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceName       : e56962a6-4747-49cd-b67b-bf8b01975c4c
ResourceType       : Microsoft.Authorization/policyDefinitions
Properties         : @{displayName=Allowed locations; policyType=BuiltIn; description=This policy enables you to
                     restrict the locations your organization can specify when deploying resources. Use to enforce
                     your geo-compliance requirements.; parameters=; policyRule=}
PolicyDefinitionId : /providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c
```

## <a name="create-a-policy-definition-with-azure-cli"></a><span data-ttu-id="dde95-186">Create a policy definition with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dde95-186">Create a policy definition with Azure CLI</span></span>

<span data-ttu-id="dde95-187">You can create a policy definition using Azure CLI with the policy definition command.</span><span class="sxs-lookup"><span data-stu-id="dde95-187">You can create a policy definition using Azure CLI with the policy definition command.</span></span>
<span data-ttu-id="dde95-188">To create a policy definition with an inline rule, use the following example:</span><span class="sxs-lookup"><span data-stu-id="dde95-188">To create a policy definition with an inline rule, use the following example:</span></span>

```azurecli-interactive
az policy definition create --name 'denyCoolTiering' --description 'Deny cool access tiering for storage' --rules '{
    "if": {
        "allOf": [{
                "field": "type",
                "equals": "Microsoft.Storage/storageAccounts"
            },
            {
                "field": "kind",
                "equals": "BlobStorage"
            },
            {
                "field": "Microsoft.Storage/storageAccounts/accessTier",
                "equals": "cool"
            }
        ]
    },
    "then": {
        "effect": "deny"
    }
}'
```

### <a name="view-policy-definitions-with-azure-cli"></a><span data-ttu-id="dde95-189">View policy definitions with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="dde95-189">View policy definitions with Azure CLI</span></span>

<span data-ttu-id="dde95-190">To see all policy definitions in your subscription, use the following command:</span><span class="sxs-lookup"><span data-stu-id="dde95-190">To see all policy definitions in your subscription, use the following command:</span></span>

```azurecli-interactive
az policy definition list
```

<span data-ttu-id="dde95-191">It returns all available policy definitions, including built-in policies.</span><span class="sxs-lookup"><span data-stu-id="dde95-191">It returns all available policy definitions, including built-in policies.</span></span> <span data-ttu-id="dde95-192">Each policy is returned in the following format:</span><span class="sxs-lookup"><span data-stu-id="dde95-192">Each policy is returned in the following format:</span></span>

```json
{
    "description": "This policy enables you to restrict the locations your organization can specify when deploying resources. Use to enforce your geo-compliance requirements.",
    "displayName": "Allowed locations",
    "id": "/providers/Microsoft.Authorization/policyDefinitions/e56962a6-4747-49cd-b67b-bf8b01975c4c",
    "name": "e56962a6-4747-49cd-b67b-bf8b01975c4c",
    "policyRule": {
        "if": {
            "not": {
                "field": "location",
                "in": "[parameters('listOfAllowedLocations')]"
            }
        },
        "then": {
            "effect": "Deny"
        }
    },
    "policyType": "BuiltIn"
}
```

## <a name="create-and-assign-an-initiative-definition"></a><span data-ttu-id="dde95-193">Create and assign an initiative definition</span><span class="sxs-lookup"><span data-stu-id="dde95-193">Create and assign an initiative definition</span></span>

<span data-ttu-id="dde95-194">With an initiative definition, you can group several policy definitions to achieve one overarching goal.</span><span class="sxs-lookup"><span data-stu-id="dde95-194">With an initiative definition, you can group several policy definitions to achieve one overarching goal.</span></span> <span data-ttu-id="dde95-195">You create an initiative definition to ensure that resources within the scope of the definition stay compliant with the policy definitions that make up the initiative definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-195">You create an initiative definition to ensure that resources within the scope of the definition stay compliant with the policy definitions that make up the initiative definition.</span></span>  <span data-ttu-id="dde95-196">For more information about initiative definitions, see [Azure Policy overview](azure-policy-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="dde95-196">For more information about initiative definitions, see [Azure Policy overview](azure-policy-introduction.md).</span></span>

### <a name="create-an-initiative-definition"></a><span data-ttu-id="dde95-197">Create an initiative definition</span><span class="sxs-lookup"><span data-stu-id="dde95-197">Create an initiative definition</span></span>

1. <span data-ttu-id="dde95-198">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-198">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span></span>

   ![Select definitions](media/create-manage-policy/select-definitions.png)

1. <span data-ttu-id="dde95-200">Select **+ Initiative Definition** at the top of the page to open the **Initiative definition** page.</span><span class="sxs-lookup"><span data-stu-id="dde95-200">Select **+ Initiative Definition** at the top of the page to open the **Initiative definition** page.</span></span>

   ![Initiative definition](media/create-manage-policy/initiative-definition.png)

1. <span data-ttu-id="dde95-202">Use the **Definition location** ellipsis to select a management group or subscription to store the definition.</span><span class="sxs-lookup"><span data-stu-id="dde95-202">Use the **Definition location** ellipsis to select a management group or subscription to store the definition.</span></span>

1. <span data-ttu-id="dde95-203">Enter the **Name** and **Description** of the initiative.</span><span class="sxs-lookup"><span data-stu-id="dde95-203">Enter the **Name** and **Description** of the initiative.</span></span>

   <span data-ttu-id="dde95-204">This example will ensure that resources are in compliance with policy definitions about getting secure.</span><span class="sxs-lookup"><span data-stu-id="dde95-204">This example will ensure that resources are in compliance with policy definitions about getting secure.</span></span> <span data-ttu-id="dde95-205">So, the name of the initiative would be **Get Secure** and the description would be: **This initiative has been created to handle all policy definitions associated with securing resources**.</span><span class="sxs-lookup"><span data-stu-id="dde95-205">So, the name of the initiative would be **Get Secure** and the description would be: **This initiative has been created to handle all policy definitions associated with securing resources**.</span></span>

1. <span data-ttu-id="dde95-206">For **Category**, choose from existing options or create a new category.</span><span class="sxs-lookup"><span data-stu-id="dde95-206">For **Category**, choose from existing options or create a new category.</span></span>

1. <span data-ttu-id="dde95-207">Browse through the list of **Available Definitions** (right half of **Initiative definition** page) and select the policy definition(s) you would like to add to this initiative.</span><span class="sxs-lookup"><span data-stu-id="dde95-207">Browse through the list of **Available Definitions** (right half of **Initiative definition** page) and select the policy definition(s) you would like to add to this initiative.</span></span> <span data-ttu-id="dde95-208">For the **Get secure** initiative, add the following built-in policy definitions by clicking the **+** next to the policy definition information or clicking a policy definition row and then the **+ Add** option in the details page:</span><span class="sxs-lookup"><span data-stu-id="dde95-208">For the **Get secure** initiative, add the following built-in policy definitions by clicking the **+** next to the policy definition information or clicking a policy definition row and then the **+ Add** option in the details page:</span></span>
   - <span data-ttu-id="dde95-209">Require SQL Server version 12.0</span><span class="sxs-lookup"><span data-stu-id="dde95-209">Require SQL Server version 12.0</span></span>
   - [Preview]: Monitor unprotected web applications in Security Center.
   - [Preview]: Monitor permissive network across in Security Center.
   - [Preview]: Monitor possible app Whitelisting in Security Center.
   - [Preview]: Monitor unencrypted VM Disks in Security Center.

   <span data-ttu-id="dde95-210">After selecting the policy definition from the list, it is added under **POLICIES AND PARAMETERS**.</span><span class="sxs-lookup"><span data-stu-id="dde95-210">After selecting the policy definition from the list, it is added under **POLICIES AND PARAMETERS**.</span></span>

   ![Initiative definitions](media/create-manage-policy/initiative-definition-2.png)

1. <span data-ttu-id="dde95-212">If a policy definition being added to the initiative has parameters, they are shown under the policy name in the **POLICIES AND PARAMETERS** area.</span><span class="sxs-lookup"><span data-stu-id="dde95-212">If a policy definition being added to the initiative has parameters, they are shown under the policy name in the **POLICIES AND PARAMETERS** area.</span></span> <span data-ttu-id="dde95-213">The _value_ can be set to either 'Set value' (hard coded for all assignments of this initiative) or 'Use Initiative Parameter' (set during each initiative assignment).</span><span class="sxs-lookup"><span data-stu-id="dde95-213">The _value_ can be set to either 'Set value' (hard coded for all assignments of this initiative) or 'Use Initiative Parameter' (set during each initiative assignment).</span></span> <span data-ttu-id="dde95-214">If 'Set value' is selected, the drown-down to the right of _Values_ allows entering or selecting the desired value(s).</span><span class="sxs-lookup"><span data-stu-id="dde95-214">If 'Set value' is selected, the drown-down to the right of _Values_ allows entering or selecting the desired value(s).</span></span> <span data-ttu-id="dde95-215">If 'Use Initiative Parameter' is selected, a new **Initiative parameters** section is displayed allowing you to define the parameter that will be set during initiative assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-215">If 'Use Initiative Parameter' is selected, a new **Initiative parameters** section is displayed allowing you to define the parameter that will be set during initiative assignment.</span></span> <span data-ttu-id="dde95-216">The allowed values on this initiative parameter can further restrict what may be set during initiative assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-216">The allowed values on this initiative parameter can further restrict what may be set during initiative assignment.</span></span>

   ![Initiative definition parameters](media/create-manage-policy/initiative-definition-3.png)

   > [!NOTE]
   > <span data-ttu-id="dde95-218">In the case of some `strongType` parameters, the list of values cannot be automatically determined.</span><span class="sxs-lookup"><span data-stu-id="dde95-218">In the case of some `strongType` parameters, the list of values cannot be automatically determined.</span></span> <span data-ttu-id="dde95-219">In these cases, an ellipsis will appear to the right of the parameter row.</span><span class="sxs-lookup"><span data-stu-id="dde95-219">In these cases, an ellipsis will appear to the right of the parameter row.</span></span> <span data-ttu-id="dde95-220">Clicking it will open the 'Parameter scope (&lt;parameter name&gt;)' page.</span><span class="sxs-lookup"><span data-stu-id="dde95-220">Clicking it will open the 'Parameter scope (&lt;parameter name&gt;)' page.</span></span> <span data-ttu-id="dde95-221">On this page, select the subscription to use for providing the value options.</span><span class="sxs-lookup"><span data-stu-id="dde95-221">On this page, select the subscription to use for providing the value options.</span></span> <span data-ttu-id="dde95-222">This parameter scope is only used during creation of the initiative definition and has no impact on policy evaluation or the scope of the initiative when assigned.</span><span class="sxs-lookup"><span data-stu-id="dde95-222">This parameter scope is only used during creation of the initiative definition and has no impact on policy evaluation or the scope of the initiative when assigned.</span></span>

1. <span data-ttu-id="dde95-223">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dde95-223">Click **Save**.</span></span>

### <a name="assign-an-initiative-definition"></a><span data-ttu-id="dde95-224">Assign an initiative definition</span><span class="sxs-lookup"><span data-stu-id="dde95-224">Assign an initiative definition</span></span>

1. <span data-ttu-id="dde95-225">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-225">Select **Definitions** under **AUTHORING** in the left side of the Azure Policy page.</span></span>
1. <span data-ttu-id="dde95-226">Locate the **Get Secure** initiative definition you previously created and select it.</span><span class="sxs-lookup"><span data-stu-id="dde95-226">Locate the **Get Secure** initiative definition you previously created and select it.</span></span>
1. <span data-ttu-id="dde95-227">Select **Assign** at the top of the page to open to the **Get Secure: Assign Initiative** page.</span><span class="sxs-lookup"><span data-stu-id="dde95-227">Select **Assign** at the top of the page to open to the **Get Secure: Assign Initiative** page.</span></span>

   ![Assign a definition](media/create-manage-policy/assign-definition.png)

   <span data-ttu-id="dde95-229">Alternatively, you can right-click on the selected row or left-click on the ellipsis at the end of the row for a contextual menu.</span><span class="sxs-lookup"><span data-stu-id="dde95-229">Alternatively, you can right-click on the selected row or left-click on the ellipsis at the end of the row for a contextual menu.</span></span>  <span data-ttu-id="dde95-230">Then select **Assign**.</span><span class="sxs-lookup"><span data-stu-id="dde95-230">Then select **Assign**.</span></span>

   ![Right-click a row](media/create-manage-policy/select-right-click.png)

1. <span data-ttu-id="dde95-232">Fill out the **Get Secure: Assign Initiative** page by entering the following example information.</span><span class="sxs-lookup"><span data-stu-id="dde95-232">Fill out the **Get Secure: Assign Initiative** page by entering the following example information.</span></span> <span data-ttu-id="dde95-233">You can use your own information.</span><span class="sxs-lookup"><span data-stu-id="dde95-233">You can use your own information.</span></span>

   - <span data-ttu-id="dde95-234">Scope: The subscription you saved the initiative to will be the default.</span><span class="sxs-lookup"><span data-stu-id="dde95-234">Scope: The subscription you saved the initiative to will be the default.</span></span>  <span data-ttu-id="dde95-235">You can change scope to assign the initiative to a resource group within the subscription save location.</span><span class="sxs-lookup"><span data-stu-id="dde95-235">You can change scope to assign the initiative to a resource group within the subscription save location.</span></span>
   - <span data-ttu-id="dde95-236">Exclusions: Configure any resources within the scope to prevent the initiative assignment from being applied to them.</span><span class="sxs-lookup"><span data-stu-id="dde95-236">Exclusions: Configure any resources within the scope to prevent the initiative assignment from being applied to them.</span></span>
   - <span data-ttu-id="dde95-237">Initiative definition and Assignment name: Get Secure (pre-populated as name of initiative being assigned).</span><span class="sxs-lookup"><span data-stu-id="dde95-237">Initiative definition and Assignment name: Get Secure (pre-populated as name of initiative being assigned).</span></span>
   - <span data-ttu-id="dde95-238">Description: This initiative assignment is tailored to enforce this group of policy definitions.</span><span class="sxs-lookup"><span data-stu-id="dde95-238">Description: This initiative assignment is tailored to enforce this group of policy definitions.</span></span>

1. <span data-ttu-id="dde95-239">Click **Assign**.</span><span class="sxs-lookup"><span data-stu-id="dde95-239">Click **Assign**.</span></span>

## <a name="exempt-a-non-compliant-or-denied-resource-using-exclusion"></a><span data-ttu-id="dde95-240">Exempt a non-compliant or denied resource using Exclusion</span><span class="sxs-lookup"><span data-stu-id="dde95-240">Exempt a non-compliant or denied resource using Exclusion</span></span>

<span data-ttu-id="dde95-241">Following the example above, after assigning the policy definition to require SQL server version 12.0, a SQL server created with any version other 12.0 would get denied.</span><span class="sxs-lookup"><span data-stu-id="dde95-241">Following the example above, after assigning the policy definition to require SQL server version 12.0, a SQL server created with any version other 12.0 would get denied.</span></span> <span data-ttu-id="dde95-242">In this section, you walk through resolving a denied attempt to create a SQL server by creating an exclusion on a single resource group.</span><span class="sxs-lookup"><span data-stu-id="dde95-242">In this section, you walk through resolving a denied attempt to create a SQL server by creating an exclusion on a single resource group.</span></span> <span data-ttu-id="dde95-243">The exclusion prevents enforcement of the policy (or initiative) on that resource.</span><span class="sxs-lookup"><span data-stu-id="dde95-243">The exclusion prevents enforcement of the policy (or initiative) on that resource.</span></span> <span data-ttu-id="dde95-244">In the following example, any SQL server version will be allowed in a single resource group.</span><span class="sxs-lookup"><span data-stu-id="dde95-244">In the following example, any SQL server version will be allowed in a single resource group.</span></span> <span data-ttu-id="dde95-245">An exclusion can apply to a resource group or you can narrow the exclusion to individual resources.</span><span class="sxs-lookup"><span data-stu-id="dde95-245">An exclusion can apply to a resource group or you can narrow the exclusion to individual resources.</span></span>

<span data-ttu-id="dde95-246">A deployment prevented due to an assigned policy or initiative can be viewed in two locations:</span><span class="sxs-lookup"><span data-stu-id="dde95-246">A deployment prevented due to an assigned policy or initiative can be viewed in two locations:</span></span>

- <span data-ttu-id="dde95-247">On the resource group targeted by the deployment: Select **Deployments** in the left side of the page and click on the **Deployment Name** of the failed deployment.</span><span class="sxs-lookup"><span data-stu-id="dde95-247">On the resource group targeted by the deployment: Select **Deployments** in the left side of the page and click on the **Deployment Name** of the failed deployment.</span></span> <span data-ttu-id="dde95-248">The resource that was denied will be listed with a status of _Forbidden_.</span><span class="sxs-lookup"><span data-stu-id="dde95-248">The resource that was denied will be listed with a status of _Forbidden_.</span></span> <span data-ttu-id="dde95-249">To determine the policy or initiative and assignment that denied the resource, click **Failed. Click here for details ->** on the Deployment Overview page.</span><span class="sxs-lookup"><span data-stu-id="dde95-249">To determine the policy or initiative and assignment that denied the resource, click **Failed. Click here for details ->** on the Deployment Overview page.</span></span> <span data-ttu-id="dde95-250">A window will open on the right side of the page with the error information.</span><span class="sxs-lookup"><span data-stu-id="dde95-250">A window will open on the right side of the page with the error information.</span></span> <span data-ttu-id="dde95-251">Under **Error Details** will be the GUIDs of the related policy objects.</span><span class="sxs-lookup"><span data-stu-id="dde95-251">Under **Error Details** will be the GUIDs of the related policy objects.</span></span>

   ![Deployment denied by policy assignment](media/create-manage-policy/rg-deployment-denied.png)

- <span data-ttu-id="dde95-253">On the Azure Policy page: Select **Compliance** in the left side of the page and click on the **Require SQL Server version 12.0** policy.</span><span class="sxs-lookup"><span data-stu-id="dde95-253">On the Azure Policy page: Select **Compliance** in the left side of the page and click on the **Require SQL Server version 12.0** policy.</span></span> <span data-ttu-id="dde95-254">On the page that opens, you would see an increase in the **Deny** count.</span><span class="sxs-lookup"><span data-stu-id="dde95-254">On the page that opens, you would see an increase in the **Deny** count.</span></span> <span data-ttu-id="dde95-255">Under the **Events** tab, you would also see who attempted the deployment that was denied by the policy.</span><span class="sxs-lookup"><span data-stu-id="dde95-255">Under the **Events** tab, you would also see who attempted the deployment that was denied by the policy.</span></span>

   ![Compliance overview of an assigned policy](media/create-manage-policy/compliance-overview.png)

<span data-ttu-id="dde95-257">In this example, Trent Baker, one of Contoso's Sr. Virtualization specialists, was doing required work.</span><span class="sxs-lookup"><span data-stu-id="dde95-257">In this example, Trent Baker, one of Contoso's Sr. Virtualization specialists, was doing required work.</span></span> <span data-ttu-id="dde95-258">We need to grant him an exception, but we don't want the non-version 12.0 SQL servers in just any resource group.</span><span class="sxs-lookup"><span data-stu-id="dde95-258">We need to grant him an exception, but we don't want the non-version 12.0 SQL servers in just any resource group.</span></span> <span data-ttu-id="dde95-259">We've created a new resource group, **SQLServers_Excluded** and will now grant it an exception to this policy assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-259">We've created a new resource group, **SQLServers_Excluded** and will now grant it an exception to this policy assignment.</span></span>

### <a name="update-assignment-with-exclusion"></a><span data-ttu-id="dde95-260">Update assignment with exclusion</span><span class="sxs-lookup"><span data-stu-id="dde95-260">Update assignment with exclusion</span></span>

1. <span data-ttu-id="dde95-261">Select **Assignments** under **AUTHORING** in the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-261">Select **Assignments** under **AUTHORING** in the left side of the Azure Policy page.</span></span>
1. <span data-ttu-id="dde95-262">Browse through all policy assignments and open the *Require SQL Server version 12.0* assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-262">Browse through all policy assignments and open the *Require SQL Server version 12.0* assignment.</span></span>
1. <span data-ttu-id="dde95-263">Set the **Exclusion** by clicking the ellipsis and selecting the resource group to exclude, *SQLServers_Excluded* in this example.</span><span class="sxs-lookup"><span data-stu-id="dde95-263">Set the **Exclusion** by clicking the ellipsis and selecting the resource group to exclude, *SQLServers_Excluded* in this example.</span></span>

   ![Request exclusion](media/create-manage-policy/request-exclusion.png)

   > [!NOTE]
   > <span data-ttu-id="dde95-265">Depending on the policy and its effect, the exclusion could also be granted to specific resources within a resource group inside the scope of the assignment.</span><span class="sxs-lookup"><span data-stu-id="dde95-265">Depending on the policy and its effect, the exclusion could also be granted to specific resources within a resource group inside the scope of the assignment.</span></span> <span data-ttu-id="dde95-266">As a **Deny** effect was used in this tutorial, it would not make sense to set the exclusion on a specific resource that already exists.</span><span class="sxs-lookup"><span data-stu-id="dde95-266">As a **Deny** effect was used in this tutorial, it would not make sense to set the exclusion on a specific resource that already exists.</span></span>

1. <span data-ttu-id="dde95-267">Click **Select** and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="dde95-267">Click **Select** and then click **Save**.</span></span>

<span data-ttu-id="dde95-268">In this section, you resolved the denial of the attempt to create a prohibited version of SQL server by creating an exclusion on a single resource group.</span><span class="sxs-lookup"><span data-stu-id="dde95-268">In this section, you resolved the denial of the attempt to create a prohibited version of SQL server by creating an exclusion on a single resource group.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="dde95-269">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="dde95-269">Clean up resources</span></span>

<span data-ttu-id="dde95-270">If you are done working with resources from this tutorial, use the following steps to delete any of the assignments or definitions created above:</span><span class="sxs-lookup"><span data-stu-id="dde95-270">If you are done working with resources from this tutorial, use the following steps to delete any of the assignments or definitions created above:</span></span>

1. <span data-ttu-id="dde95-271">Select **Definitions** (or **Assignments** if you are trying to delete an assignment) under **AUTHORING** in the left side of the Azure Policy page.</span><span class="sxs-lookup"><span data-stu-id="dde95-271">Select **Definitions** (or **Assignments** if you are trying to delete an assignment) under **AUTHORING** in the left side of the Azure Policy page.</span></span>
1. <span data-ttu-id="dde95-272">Search for the new initiative or policy definition (or assignment) you want to remove.</span><span class="sxs-lookup"><span data-stu-id="dde95-272">Search for the new initiative or policy definition (or assignment) you want to remove.</span></span>
1. <span data-ttu-id="dde95-273">Right-click the row or select the ellipses at the end of the definition (or assignment), and select **Delete definition** (or **Delete assignment**).</span><span class="sxs-lookup"><span data-stu-id="dde95-273">Right-click the row or select the ellipses at the end of the definition (or assignment), and select **Delete definition** (or **Delete assignment**).</span></span>

## <a name="next-steps"></a><span data-ttu-id="dde95-274">Next steps</span><span class="sxs-lookup"><span data-stu-id="dde95-274">Next steps</span></span>

<span data-ttu-id="dde95-275">In this tutorial, you successfully accomplished the following:</span><span class="sxs-lookup"><span data-stu-id="dde95-275">In this tutorial, you successfully accomplished the following:</span></span>

> [!div class="checklist"]
> - <span data-ttu-id="dde95-276">Assigned a policy to enforce a condition for resources you create in the future</span><span class="sxs-lookup"><span data-stu-id="dde95-276">Assigned a policy to enforce a condition for resources you create in the future</span></span>
> - <span data-ttu-id="dde95-277">Created and assign an initiative definition to track compliance for multiple resources</span><span class="sxs-lookup"><span data-stu-id="dde95-277">Created and assign an initiative definition to track compliance for multiple resources</span></span>
> - <span data-ttu-id="dde95-278">Resolved a non-compliant or denied resource</span><span class="sxs-lookup"><span data-stu-id="dde95-278">Resolved a non-compliant or denied resource</span></span>
> - <span data-ttu-id="dde95-279">Implemented a new policy across an organization</span><span class="sxs-lookup"><span data-stu-id="dde95-279">Implemented a new policy across an organization</span></span>

<span data-ttu-id="dde95-280">To learn more about the structures of policy definitions, look at this article:</span><span class="sxs-lookup"><span data-stu-id="dde95-280">To learn more about the structures of policy definitions, look at this article:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dde95-281">Azure Policy definition structure</span><span class="sxs-lookup"><span data-stu-id="dde95-281">Azure Policy definition structure</span></span>](policy-definition.md)