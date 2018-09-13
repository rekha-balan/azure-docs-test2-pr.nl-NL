---
title: Assign and manage Azure resource policies | Microsoft Docs
description: Describes how to apply Azure resource policies to subscriptions and resource groups, and how to view resource policies.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: tomfitz
ms.openlocfilehash: fd15cbc8f6efa788ddaeaee4ab39ce1410c4be5a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669271"
---
# <a name="assign-and-manage-resource-policies"></a><span data-ttu-id="9bb43-103">Assign and manage resource policies</span><span class="sxs-lookup"><span data-stu-id="9bb43-103">Assign and manage resource policies</span></span>

<span data-ttu-id="9bb43-104">To implement a policy, you must perform three steps:</span><span class="sxs-lookup"><span data-stu-id="9bb43-104">To implement a policy, you must perform three steps:</span></span>

1. <span data-ttu-id="9bb43-105">Define the policy rule with JSON.</span><span class="sxs-lookup"><span data-stu-id="9bb43-105">Define the policy rule with JSON.</span></span>
2. <span data-ttu-id="9bb43-106">Create a policy definition in your subscription from the JSON you created in the preceding step.</span><span class="sxs-lookup"><span data-stu-id="9bb43-106">Create a policy definition in your subscription from the JSON you created in the preceding step.</span></span> <span data-ttu-id="9bb43-107">This step makes the policy available for assignment but does not apply the rules to your subscription.</span><span class="sxs-lookup"><span data-stu-id="9bb43-107">This step makes the policy available for assignment but does not apply the rules to your subscription.</span></span>
3. <span data-ttu-id="9bb43-108">Assign the policy to a scope (such as a subscription or resource group).</span><span class="sxs-lookup"><span data-stu-id="9bb43-108">Assign the policy to a scope (such as a subscription or resource group).</span></span> <span data-ttu-id="9bb43-109">The rules of the policy are now enforced.</span><span class="sxs-lookup"><span data-stu-id="9bb43-109">The rules of the policy are now enforced.</span></span>

<span data-ttu-id="9bb43-110">Azure provides some pre-defined policies that may reduce the number of policies you have to define.</span><span class="sxs-lookup"><span data-stu-id="9bb43-110">Azure provides some pre-defined policies that may reduce the number of policies you have to define.</span></span> <span data-ttu-id="9bb43-111">If a pre-defined policy works for your scenario, skip the first two steps and assign the pre-defined policy to a scope.</span><span class="sxs-lookup"><span data-stu-id="9bb43-111">If a pre-defined policy works for your scenario, skip the first two steps and assign the pre-defined policy to a scope.</span></span>

<span data-ttu-id="9bb43-112">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9bb43-112">This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI.</span></span> <span data-ttu-id="9bb43-113">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9bb43-113">If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md).</span></span> <span data-ttu-id="9bb43-114">This article does not focus on the syntax for creating the policy definition.</span><span class="sxs-lookup"><span data-stu-id="9bb43-114">This article does not focus on the syntax for creating the policy definition.</span></span> <span data-ttu-id="9bb43-115">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span><span class="sxs-lookup"><span data-stu-id="9bb43-115">For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).</span></span>

## <a name="rest-api"></a><span data-ttu-id="9bb43-116">REST API</span><span class="sxs-lookup"><span data-stu-id="9bb43-116">REST API</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="9bb43-117">Create policy definition</span><span class="sxs-lookup"><span data-stu-id="9bb43-117">Create policy definition</span></span>

<span data-ttu-id="9bb43-118">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span><span class="sxs-lookup"><span data-stu-id="9bb43-118">You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions).</span></span> <span data-ttu-id="9bb43-119">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span><span class="sxs-lookup"><span data-stu-id="9bb43-119">The REST API enables you to create and delete policy definitions, and get information about existing definitions.</span></span>

<span data-ttu-id="9bb43-120">To create a policy definition, run:</span><span class="sxs-lookup"><span data-stu-id="9bb43-120">To create a policy definition, run:</span></span>

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

<span data-ttu-id="9bb43-121">Include a request body similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="9bb43-121">Include a request body similar to the following example:</span></span>

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

### <a name="assign-policy"></a><span data-ttu-id="9bb43-122">Assign policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-122">Assign policy</span></span>

<span data-ttu-id="9bb43-123">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span><span class="sxs-lookup"><span data-stu-id="9bb43-123">You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments).</span></span> <span data-ttu-id="9bb43-124">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span><span class="sxs-lookup"><span data-stu-id="9bb43-124">The REST API enables you to create and delete policy assignments, and get information about existing assignments.</span></span>

<span data-ttu-id="9bb43-125">To create a policy assignment, run:</span><span class="sxs-lookup"><span data-stu-id="9bb43-125">To create a policy assignment, run:</span></span>

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

<span data-ttu-id="9bb43-126">The {policy-assignment} is the name of the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="9bb43-126">The {policy-assignment} is the name of the policy assignment.</span></span>

<span data-ttu-id="9bb43-127">Include a request body similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="9bb43-127">Include a request body similar to the following example:</span></span>

```json
{
  "properties":{
    "displayName":"West US only policy assignment on the subscription ",
    "description":"Resources can only be provisioned in West US regions",
    "parameters": {
      "allowedLocations": { "value": ["northeurope", "westus"] }
     },
    "policyDefinitionId":"/subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{definition-name}",
      "scope":"/subscriptions/{subscription-id}"
  },
}
```

### <a name="view-policy"></a><span data-ttu-id="9bb43-128">View policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-128">View policy</span></span>
<span data-ttu-id="9bb43-129">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span><span class="sxs-lookup"><span data-stu-id="9bb43-129">To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.</span></span>

### <a name="get-aliases"></a><span data-ttu-id="9bb43-130">Get aliases</span><span class="sxs-lookup"><span data-stu-id="9bb43-130">Get aliases</span></span>
<span data-ttu-id="9bb43-131">You can retrieve aliases through the REST API:</span><span class="sxs-lookup"><span data-stu-id="9bb43-131">You can retrieve aliases through the REST API:</span></span>

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

<span data-ttu-id="9bb43-132">The following example shows a definition of an alias.</span><span class="sxs-lookup"><span data-stu-id="9bb43-132">The following example shows a definition of an alias.</span></span> <span data-ttu-id="9bb43-133">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span><span class="sxs-lookup"><span data-stu-id="9bb43-133">As you can see, an alias defines paths in different API versions, even when there is a property name change.</span></span> 

```json
"aliases": [
    {
      "name": "Microsoft.Storage/storageAccounts/sku.name",
      "paths": [
        {
          "path": "properties.accountType",
          "apiVersions": [
            "2015-06-15",
            "2015-05-01-preview"
          ]
        },
        {
          "path": "sku.name",
          "apiVersions": [
            "2016-01-01"
          ]
        }
      ]
    }
]
```

## <a name="powershell"></a><span data-ttu-id="9bb43-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9bb43-134">PowerShell</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="9bb43-135">Create policy definition</span><span class="sxs-lookup"><span data-stu-id="9bb43-135">Create policy definition</span></span>
<span data-ttu-id="9bb43-136">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9bb43-136">You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet.</span></span> <span data-ttu-id="9bb43-137">The following example creates a policy definition for allowing resources only in North Europe and West Europe.</span><span class="sxs-lookup"><span data-stu-id="9bb43-137">The following example creates a policy definition for allowing resources only in North Europe and West Europe.</span></span>

```powershell
$policy = New-AzureRmPolicyDefinition -Name regionPolicyDefinition -Description "Policy to allow resource creation only in certain regions" -Policy '{
   "if": {
     "not": {
       "field": "location",
       "in": "[parameters(''allowedLocations'')]"
     }
   },
   "then": {
     "effect": "deny"
   }
 }' -Parameter '{
     "allowedLocations": {
       "type": "array",
       "metadata": {
         "description": "An array of permitted locations for resources.",
         "strongType": "location",
         "displayName": "List of locations"
       }
     }
 }'
```            

<span data-ttu-id="9bb43-138">The output is stored in a `$policy` object, which is used during policy assignment.</span><span class="sxs-lookup"><span data-stu-id="9bb43-138">The output is stored in a `$policy` object, which is used during policy assignment.</span></span> 

<span data-ttu-id="9bb43-139">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span><span class="sxs-lookup"><span data-stu-id="9bb43-139">Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.</span></span>

```powershell
$policy = New-AzureRmPolicyDefinition -Name regionPolicyDefinition -Description "Policy to allow resource creation only in certain regions" -Policy "c:\policies\storageskupolicy.json"
```

### <a name="assign-policy"></a><span data-ttu-id="9bb43-140">Assign policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-140">Assign policy</span></span>

<span data-ttu-id="9bb43-141">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="9bb43-141">You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$array = @("West US", "West US 2")
$param = @{"allowedLocations"=$array}
New-AzureRMPolicyAssignment -Name regionPolicyAssignment -Scope $rg.ResourceId -PolicyDefinition $policy -PolicyParameterObject $param
```

### <a name="view-policies"></a><span data-ttu-id="9bb43-142">View policies</span><span class="sxs-lookup"><span data-stu-id="9bb43-142">View policies</span></span>

<span data-ttu-id="9bb43-143">To get all policy assignments, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-143">To get all policy assignments, use:</span></span>

```powershell
Get-AzureRmPolicyAssignment
```

<span data-ttu-id="9bb43-144">To get a specific policy, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-144">To get a specific policy, use:</span></span>

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope $rg.ResourceId
```

<span data-ttu-id="9bb43-145">To view the policy rule for a policy definition, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-145">To view the policy rule for a policy definition, use:</span></span>

```powershell
(Get-AzureRmPolicyDefinition -Name regionPolicyDefinition).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="9bb43-146">Remove policy assignment</span><span class="sxs-lookup"><span data-stu-id="9bb43-146">Remove policy assignment</span></span> 

<span data-ttu-id="9bb43-147">To remove a policy assignment, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-147">To remove a policy assignment, use:</span></span>

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli-20"></a><span data-ttu-id="9bb43-148">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="9bb43-148">Azure CLI 2.0</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="9bb43-149">Create policy definition</span><span class="sxs-lookup"><span data-stu-id="9bb43-149">Create policy definition</span></span>

<span data-ttu-id="9bb43-150">You can create a policy definition using Azure CLI 2.0 with the policy definition command.</span><span class="sxs-lookup"><span data-stu-id="9bb43-150">You can create a policy definition using Azure CLI 2.0 with the policy definition command.</span></span> <span data-ttu-id="9bb43-151">The following example creates a policy for allowing resources only in North Europe and West Europe.</span><span class="sxs-lookup"><span data-stu-id="9bb43-151">The following example creates a policy for allowing resources only in North Europe and West Europe.</span></span>

```azurecli
az policy definition create --name regionPolicyDefinition --description "Policy to allow resource creation only in certain regions" --rules '{    
  "if" : {
    "not" : {
      "field" : "location",
      "in" : ["northeurope" , "westeurope"]
    }
  },
  "then" : {
    "effect" : "deny"
  }
}'    
```

### <a name="assign-policy"></a><span data-ttu-id="9bb43-152">Assign policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-152">Assign policy</span></span>

<span data-ttu-id="9bb43-153">You can apply the policy to the desired scope by using the policy assignment command:</span><span class="sxs-lookup"><span data-stu-id="9bb43-153">You can apply the policy to the desired scope by using the policy assignment command:</span></span>

```azurecli
az policy assignment create --name regionPolicyAssignment --policy regionPolicyDefinition --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-definition"></a><span data-ttu-id="9bb43-154">View policy definition</span><span class="sxs-lookup"><span data-stu-id="9bb43-154">View policy definition</span></span>
<span data-ttu-id="9bb43-155">To get a policy definition, use the following command:</span><span class="sxs-lookup"><span data-stu-id="9bb43-155">To get a policy definition, use the following command:</span></span>

```azurecli
az policy definition show --name regionPolicyAssignment
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="9bb43-156">Remove policy assignment</span><span class="sxs-lookup"><span data-stu-id="9bb43-156">Remove policy assignment</span></span> 

<span data-ttu-id="9bb43-157">To remove a policy assignment, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-157">To remove a policy assignment, use:</span></span>

```azurecli
az policy assignment delete --name regionPolicyAssignment --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli-10"></a><span data-ttu-id="9bb43-158">Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="9bb43-158">Azure CLI 1.0</span></span>

### <a name="create-policy-definition"></a><span data-ttu-id="9bb43-159">Create policy definition</span><span class="sxs-lookup"><span data-stu-id="9bb43-159">Create policy definition</span></span>

<span data-ttu-id="9bb43-160">You can create a policy definition using the Azure CLI with the policy definition command.</span><span class="sxs-lookup"><span data-stu-id="9bb43-160">You can create a policy definition using the Azure CLI with the policy definition command.</span></span> <span data-ttu-id="9bb43-161">The following example creates a policy for allowing resources only in North Europe and West Europe.</span><span class="sxs-lookup"><span data-stu-id="9bb43-161">The following example creates a policy for allowing resources only in North Europe and West Europe.</span></span>

```azurecli
azure policy definition create --name regionPolicyDefinition --description "Policy to allow resource creation only in certain regions" --policy-string '{    
  "if" : {
    "not" : {
      "field" : "location",
      "in" : ["northeurope" , "westeurope"]
    }
  },
  "then" : {
    "effect" : "deny"
  }
}'    
```

<span data-ttu-id="9bb43-162">It is possible to specify the path to a .json file containing the policy instead of specifying the policy inline.</span><span class="sxs-lookup"><span data-stu-id="9bb43-162">It is possible to specify the path to a .json file containing the policy instead of specifying the policy inline.</span></span>

```azurecli
azure policy definition create --name regionPolicyDefinition --description "Policy to allow resource creation only in certain regions" --policy "path-to-policy-json-on-disk"
```

### <a name="assign-policy"></a><span data-ttu-id="9bb43-163">Assign policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-163">Assign policy</span></span>

<span data-ttu-id="9bb43-164">You can apply the policy to the desired scope by using the policy assignment command:</span><span class="sxs-lookup"><span data-stu-id="9bb43-164">You can apply the policy to the desired scope by using the policy assignment command:</span></span>

```azurecli
azure policy assignment create --name regionPolicyAssignment --policy-definition-id /subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{policy-name} --scope    /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

<span data-ttu-id="9bb43-165">The scope here is the name of the resource group you specify.</span><span class="sxs-lookup"><span data-stu-id="9bb43-165">The scope here is the name of the resource group you specify.</span></span> <span data-ttu-id="9bb43-166">If the value of the parameter policy-definition-id is unknown, it is possible to obtain it through the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9bb43-166">If the value of the parameter policy-definition-id is unknown, it is possible to obtain it through the Azure CLI.</span></span> 

```azurecli
azure policy definition show {policy-name}
```

### <a name="view-policy"></a><span data-ttu-id="9bb43-167">View policy</span><span class="sxs-lookup"><span data-stu-id="9bb43-167">View policy</span></span>
<span data-ttu-id="9bb43-168">To get a policy, use the following command:</span><span class="sxs-lookup"><span data-stu-id="9bb43-168">To get a policy, use the following command:</span></span>

```azurecli
azure policy definition show {definition-name} --json
```

### <a name="remove-policy-assignment"></a><span data-ttu-id="9bb43-169">Remove policy assignment</span><span class="sxs-lookup"><span data-stu-id="9bb43-169">Remove policy assignment</span></span> 

<span data-ttu-id="9bb43-170">To remove a policy assignment, use:</span><span class="sxs-lookup"><span data-stu-id="9bb43-170">To remove a policy assignment, use:</span></span>

```azurecli
azure policy assignment delete --name regionPolicyAssignment --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a><span data-ttu-id="9bb43-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bb43-171">Next steps</span></span>
* <span data-ttu-id="9bb43-172">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="9bb43-172">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

