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
# <a name="assign-and-manage-resource-policies"></a>Assign and manage resource policies

To implement a policy, you must perform three steps:

1. Define the policy rule with JSON.
2. Create a policy definition in your subscription from the JSON you created in the preceding step. This step makes the policy available for assignment but does not apply the rules to your subscription.
3. Assign the policy to a scope (such as a subscription or resource group). The rules of the policy are now enforced.

Azure provides some pre-defined policies that may reduce the number of policies you have to define. If a pre-defined policy works for your scenario, skip the first two steps and assign the pre-defined policy to a scope.

This article focuses on the steps to create a policy definition and assign that definition to a scope through REST API, PowerShell, or Azure CLI. If you prefer to use the portal to assign policies, see [Use Azure portal to assign and manage resource policies](resource-manager-policy-portal.md). This article does not focus on the syntax for creating the policy definition. For information about policy syntax, see [Resource policy overview](resource-manager-policy.md).

## <a name="rest-api"></a>REST API

### <a name="create-policy-definition"></a>Create policy definition

You can create a policy with the [REST API for Policy Definitions](/rest/api/resources/policydefinitions). The REST API enables you to create and delete policy definitions, and get information about existing definitions.

To create a policy definition, run:

```HTTP
PUT https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.authorization/policydefinitions/{policyDefinitionName}?api-version={api-version}
```

Include a request body similar to the following example:

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

### <a name="assign-policy"></a>Assign policy

You can apply the policy definition at the desired scope through the [REST API for policy assignments](/rest/api/resources/policyassignments). The REST API enables you to create and delete policy assignments, and get information about existing assignments.

To create a policy assignment, run:

```HTTP
PUT https://management.azure.com /subscriptions/{subscription-id}/providers/Microsoft.authorization/policyassignments/{policyAssignmentName}?api-version={api-version}
```

The {policy-assignment} is the name of the policy assignment.

Include a request body similar to the following example:

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

### <a name="view-policy"></a>View policy
To get a policy, use the [Get policy definition](https://docs.microsoft.com/rest/api/resources/policydefinitions#PolicyDefinitions_Get) operation.

### <a name="get-aliases"></a>Get aliases
You can retrieve aliases through the REST API:

```HTTP
GET /subscriptions/{id}/providers?$expand=resourceTypes/aliases&api-version=2015-11-01
```

The following example shows a definition of an alias. As you can see, an alias defines paths in different API versions, even when there is a property name change. 

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

## <a name="powershell"></a>PowerShell

### <a name="create-policy-definition"></a>Create policy definition
You can create a policy definition using the `New-AzureRmPolicyDefinition` cmdlet. The following example creates a policy definition for allowing resources only in North Europe and West Europe.

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

The output is stored in a `$policy` object, which is used during policy assignment. 

Rather than specifying the JSON as a parameter, you can provide the path to a .json file containing the policy rule.

```powershell
$policy = New-AzureRmPolicyDefinition -Name regionPolicyDefinition -Description "Policy to allow resource creation only in certain regions" -Policy "c:\policies\storageskupolicy.json"
```

### <a name="assign-policy"></a>Assign policy

You apply the policy at the desired scope by using the `New-AzureRmPolicyAssignment` cmdlet:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
$array = @("West US", "West US 2")
$param = @{"allowedLocations"=$array}
New-AzureRMPolicyAssignment -Name regionPolicyAssignment -Scope $rg.ResourceId -PolicyDefinition $policy -PolicyParameterObject $param
```

### <a name="view-policies"></a>View policies

To get all policy assignments, use:

```powershell
Get-AzureRmPolicyAssignment
```

To get a specific policy, use:

```powershell
$rg = Get-AzureRmResourceGroup -Name "ExampleGroup"
(Get-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope $rg.ResourceId
```

To view the policy rule for a policy definition, use:

```powershell
(Get-AzureRmPolicyDefinition -Name regionPolicyDefinition).Properties.policyRule | ConvertTo-Json
```

### <a name="remove-policy-assignment"></a>Remove policy assignment 

To remove a policy assignment, use:

```powershell
Remove-AzureRmPolicyAssignment -Name regionPolicyAssignment -Scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli-20"></a>Azure CLI 2.0

### <a name="create-policy-definition"></a>Create policy definition

You can create a policy definition using Azure CLI 2.0 with the policy definition command. The following example creates a policy for allowing resources only in North Europe and West Europe.

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

### <a name="assign-policy"></a>Assign policy

You can apply the policy to the desired scope by using the policy assignment command:

```azurecli
az policy assignment create --name regionPolicyAssignment --policy regionPolicyDefinition --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

### <a name="view-policy-definition"></a>View policy definition
To get a policy definition, use the following command:

```azurecli
az policy definition show --name regionPolicyAssignment
```

### <a name="remove-policy-assignment"></a>Remove policy assignment 

To remove a policy assignment, use:

```azurecli
az policy assignment delete --name regionPolicyAssignment --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="azure-cli-10"></a>Azure CLI 1.0

### <a name="create-policy-definition"></a>Create policy definition

You can create a policy definition using the Azure CLI with the policy definition command. The following example creates a policy for allowing resources only in North Europe and West Europe.

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

It is possible to specify the path to a .json file containing the policy instead of specifying the policy inline.

```azurecli
azure policy definition create --name regionPolicyDefinition --description "Policy to allow resource creation only in certain regions" --policy "path-to-policy-json-on-disk"
```

### <a name="assign-policy"></a>Assign policy

You can apply the policy to the desired scope by using the policy assignment command:

```azurecli
azure policy assignment create --name regionPolicyAssignment --policy-definition-id /subscriptions/{subscription-id}/providers/Microsoft.Authorization/policyDefinitions/{policy-name} --scope    /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

The scope here is the name of the resource group you specify. If the value of the parameter policy-definition-id is unknown, it is possible to obtain it through the Azure CLI. 

```azurecli
azure policy definition show {policy-name}
```

### <a name="view-policy"></a>View policy
To get a policy, use the following command:

```azurecli
azure policy definition show {definition-name} --json
```

### <a name="remove-policy-assignment"></a>Remove policy assignment 

To remove a policy assignment, use:

```azurecli
azure policy assignment delete --name regionPolicyAssignment --scope /subscriptions/{subscription-id}/resourceGroups/{resource-group-name}
```

## <a name="next-steps"></a>Next steps
* For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).

