---
title: Deploy resources to Azure subscription | Microsoft Docs
description: Describes how to create an Azure Resource Manager template that deploys resources at the subscription scope.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2018
ms.author: tomfitz
ms.openlocfilehash: 6166161f6d50e747681217281a0afc6514df78fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866932"
---
# <a name="deploy-resources-to-an-azure-subscription"></a><span data-ttu-id="f20a5-103">Deploy resources to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="f20a5-103">Deploy resources to an Azure subscription</span></span>

<span data-ttu-id="f20a5-104">Typically, you deploy resources to a resource group in your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f20a5-104">Typically, you deploy resources to a resource group in your Azure subscription.</span></span> <span data-ttu-id="f20a5-105">However, some resources can be deployed at the level of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="f20a5-105">However, some resources can be deployed at the level of your Azure subscription.</span></span> <span data-ttu-id="f20a5-106">These resources apply across your subscription.</span><span class="sxs-lookup"><span data-stu-id="f20a5-106">These resources apply across your subscription.</span></span> <span data-ttu-id="f20a5-107">[Policies](../azure-policy/azure-policy-introduction.md), [Role-based access control](../role-based-access-control/overview.md), and [Azure Security Center](../security-center/security-center-intro.md) are services that you may want to apply at the subscription level, rather than the resource group level.</span><span class="sxs-lookup"><span data-stu-id="f20a5-107">[Policies](../azure-policy/azure-policy-introduction.md), [Role-based access control](../role-based-access-control/overview.md), and [Azure Security Center](../security-center/security-center-intro.md) are services that you may want to apply at the subscription level, rather than the resource group level.</span></span>

<span data-ttu-id="f20a5-108">This article uses Azure CLI and PowerShell to deploy the templates.</span><span class="sxs-lookup"><span data-stu-id="f20a5-108">This article uses Azure CLI and PowerShell to deploy the templates.</span></span>

## <a name="name-and-location-for-deployment"></a><span data-ttu-id="f20a5-109">Name and location for deployment</span><span class="sxs-lookup"><span data-stu-id="f20a5-109">Name and location for deployment</span></span>

<span data-ttu-id="f20a5-110">When deploying to your subscription, you must provide a location for the deployment.</span><span class="sxs-lookup"><span data-stu-id="f20a5-110">When deploying to your subscription, you must provide a location for the deployment.</span></span> <span data-ttu-id="f20a5-111">You can also provide a name for the deployment.</span><span class="sxs-lookup"><span data-stu-id="f20a5-111">You can also provide a name for the deployment.</span></span> <span data-ttu-id="f20a5-112">If you don't specify a name for the deployment, the name of the template is used as the deployment name.</span><span class="sxs-lookup"><span data-stu-id="f20a5-112">If you don't specify a name for the deployment, the name of the template is used as the deployment name.</span></span> <span data-ttu-id="f20a5-113">For example, deploying a template named **azuredeploy.json** creates a default deployment name of **azuredeploy**.</span><span class="sxs-lookup"><span data-stu-id="f20a5-113">For example, deploying a template named **azuredeploy.json** creates a default deployment name of **azuredeploy**.</span></span>

<span data-ttu-id="f20a5-114">The location of subscription level deployments is immutable.</span><span class="sxs-lookup"><span data-stu-id="f20a5-114">The location of subscription level deployments is immutable.</span></span> <span data-ttu-id="f20a5-115">You can't create a deployment in one location when there's an existing deployment with the same name but different location.</span><span class="sxs-lookup"><span data-stu-id="f20a5-115">You can't create a deployment in one location when there's an existing deployment with the same name but different location.</span></span> <span data-ttu-id="f20a5-116">If you get the error code `InvalidDeploymentLocation`, either use a different name or the same location as the previous deployment for that name.</span><span class="sxs-lookup"><span data-stu-id="f20a5-116">If you get the error code `InvalidDeploymentLocation`, either use a different name or the same location as the previous deployment for that name.</span></span>

## <a name="using-template-functions"></a><span data-ttu-id="f20a5-117">Using template functions</span><span class="sxs-lookup"><span data-stu-id="f20a5-117">Using template functions</span></span>

<span data-ttu-id="f20a5-118">For subscription level deployments, there are some important considerations when using template functions:</span><span class="sxs-lookup"><span data-stu-id="f20a5-118">For subscription level deployments, there are some important considerations when using template functions:</span></span>

* <span data-ttu-id="f20a5-119">The [resourceGroup()](resource-group-template-functions-resource.md#resourcegroup) function is **not** supported.</span><span class="sxs-lookup"><span data-stu-id="f20a5-119">The [resourceGroup()](resource-group-template-functions-resource.md#resourcegroup) function is **not** supported.</span></span>
* <span data-ttu-id="f20a5-120">The [resourceId()](resource-group-template-functions-resource.md#resourceid) function is supported.</span><span class="sxs-lookup"><span data-stu-id="f20a5-120">The [resourceId()](resource-group-template-functions-resource.md#resourceid) function is supported.</span></span> <span data-ttu-id="f20a5-121">Use it to get the resource ID for resources that are used at subscription level deployments.</span><span class="sxs-lookup"><span data-stu-id="f20a5-121">Use it to get the resource ID for resources that are used at subscription level deployments.</span></span> <span data-ttu-id="f20a5-122">For example, get the resource ID for a policy definition with `resourceId('Microsoft.Authorization/roleDefinitions/', parameters('roleDefinition'))`</span><span class="sxs-lookup"><span data-stu-id="f20a5-122">For example, get the resource ID for a policy definition with `resourceId('Microsoft.Authorization/roleDefinitions/', parameters('roleDefinition'))`</span></span>
* <span data-ttu-id="f20a5-123">The [reference()](resource-group-template-functions-resource.md#reference) and [list()](resource-group-template-functions-resource.md#list) functions are supported.</span><span class="sxs-lookup"><span data-stu-id="f20a5-123">The [reference()](resource-group-template-functions-resource.md#reference) and [list()](resource-group-template-functions-resource.md#list) functions are supported.</span></span>

## <a name="assign-policy"></a><span data-ttu-id="f20a5-124">Assign policy</span><span class="sxs-lookup"><span data-stu-id="f20a5-124">Assign policy</span></span>

<span data-ttu-id="f20a5-125">The following example assigns an existing policy definition to the subscription.</span><span class="sxs-lookup"><span data-stu-id="f20a5-125">The following example assigns an existing policy definition to the subscription.</span></span> <span data-ttu-id="f20a5-126">If the policy takes parameters, provide them as an object.</span><span class="sxs-lookup"><span data-stu-id="f20a5-126">If the policy takes parameters, provide them as an object.</span></span> <span data-ttu-id="f20a5-127">If the policy doesn't take parameters, use the default empty object.</span><span class="sxs-lookup"><span data-stu-id="f20a5-127">If the policy doesn't take parameters, use the default empty object.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "policyDefinitionID": {
            "type": "string"
        },
        "policyName": {
            "type": "string"
        },
        "policyParameters": {
            "type": "object",
            "defaultValue": {}
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Authorization/policyAssignments",
            "name": "[parameters('policyName')]",
            "apiVersion": "2018-03-01",
            "properties": {
                "scope": "[subscription().id]",
                "policyDefinitionId": "[parameters('policyDefinitionID')]",
                "parameters": "[parameters('policyParameters')]"
            }
        }
    ]
}
```

<span data-ttu-id="f20a5-128">To apply a built-in policy to your Azure subscription, use the following Azure CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f20a5-128">To apply a built-in policy to your Azure subscription, use the following Azure CLI commands.</span></span> <span data-ttu-id="f20a5-129">In this example, the policy doesn't have parameters</span><span class="sxs-lookup"><span data-stu-id="f20a5-129">In this example, the policy doesn't have parameters</span></span>

```azurecli-interactive
# Built-in policy that does not accept parameters
definition=$(az policy definition list --query "[?displayName=='Audit resource location matches resource group location'].id" --output tsv)

az deployment create \
  -n policyassign \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json \
  --parameters policyDefinitionID=$definition policyName=auditRGLocation
```

<span data-ttu-id="f20a5-130">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f20a5-130">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
$definition = Get-AzureRmPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Audit resource location matches resource group location' }

New-AzureRmDeployment `
  -Name policyassign `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json `
  -policyDefinitionID $definition.PolicyDefinitionId `
  -policyName auditRGLocation
```

<span data-ttu-id="f20a5-131">To apply a built-in policy to your Azure subscription, use the following Azure CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f20a5-131">To apply a built-in policy to your Azure subscription, use the following Azure CLI commands.</span></span> <span data-ttu-id="f20a5-132">In this example, the policy has parameters.</span><span class="sxs-lookup"><span data-stu-id="f20a5-132">In this example, the policy has parameters.</span></span>

```azurecli-interactive
# Built-in policy that accepts parameters
definition=$(az policy definition list --query "[?displayName=='Allowed locations'].id" --output tsv)

az deployment create \
  -n policyassign \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json \
  --parameters policyDefinitionID=$definition policyName=setLocation policyParameters="{'listOfAllowedLocations': {'value': ['westus']} }"
```

<span data-ttu-id="f20a5-133">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f20a5-133">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
$definition = Get-AzureRmPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Allowed locations' }

$locations = @("westus", "westus2")
$policyParams =@{listOfAllowedLocations = @{ value = $locations}}

New-AzureRmDeployment `
  -Name policyassign `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policyassign.json `
  -policyDefinitionID $definition.PolicyDefinitionId `
  -policyName setLocation `
  -policyParameters $policyParams
```

## <a name="define-and-assign-policy"></a><span data-ttu-id="f20a5-134">Define and assign policy</span><span class="sxs-lookup"><span data-stu-id="f20a5-134">Define and assign policy</span></span>

<span data-ttu-id="f20a5-135">You can [define](../azure-policy/policy-definition.md) and assign a policy in the same template.</span><span class="sxs-lookup"><span data-stu-id="f20a5-135">You can [define](../azure-policy/policy-definition.md) and assign a policy in the same template.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {},
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Authorization/policyDefinitions",
            "name": "locationpolicy",
            "apiVersion": "2018-03-01",
            "properties": {
                "policyType": "Custom",
                "parameters": {},
                "policyRule": {
                    "if": {
                        "field": "location",
                        "equals": "northeurope"
                    },
                    "then": {
                        "effect": "deny"
                    }
                }
            }
        },
        {
            "type": "Microsoft.Authorization/policyAssignments",
            "name": "location-lock",
            "apiVersion": "2018-03-01",
            "dependsOn": [
                "locationpolicy"
            ],
            "properties": {
                "scope": "[subscription().id]",
                "policyDefinitionId": "[resourceId('Microsoft.Authorization/policyDefinitions', 'locationpolicy')]"
            }
        }
    ]
}
```

<span data-ttu-id="f20a5-136">To create the policy definition in your subscription, and apply it to the subscription, use the following CLI command.</span><span class="sxs-lookup"><span data-stu-id="f20a5-136">To create the policy definition in your subscription, and apply it to the subscription, use the following CLI command.</span></span>

```azurecli-interactive
az deployment create \
  -n definePolicy \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policydefineandassign.json
```

<span data-ttu-id="f20a5-137">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f20a5-137">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
New-AzureRmDeployment `
  -Name definePolicy `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/policydefineandassign.json
```

## <a name="assign-role"></a><span data-ttu-id="f20a5-138">Assign role</span><span class="sxs-lookup"><span data-stu-id="f20a5-138">Assign role</span></span>

<span data-ttu-id="f20a5-139">The following example assigns a role to a user or group.</span><span class="sxs-lookup"><span data-stu-id="f20a5-139">The following example assigns a role to a user or group.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "principalId": {
            "type": "string"
        },
        "roleDefinitionId": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "type": "Microsoft.Authorization/roleAssignments",
            "name": "[guid(parameters('principalId'), deployment().name)]",
            "apiVersion": "2017-05-01",
            "properties": {
                "roleDefinitionId": "[resourceId('Microsoft.Authorization/roleDefinitions', parameters('roleDefinitionId'))]",
                "principalId": "[parameters('principalId')]"
            }
        }
    ]
}
```

<span data-ttu-id="f20a5-140">To assign an Active Directory group to a role for your subscription, use the following Azure CLI commands.</span><span class="sxs-lookup"><span data-stu-id="f20a5-140">To assign an Active Directory group to a role for your subscription, use the following Azure CLI commands.</span></span>

```azurecli-interactive
# Get ID of the role you want to assign
role=$(az role definition list --name Contributor --query [].name --output tsv)

# Get ID of the AD group to assign the role to
principalid=$(az ad group show --group demogroup --query objectId --output tsv)

az deployment create \
  -n demoRole \
  -l southcentralus \
  --template-uri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/roleassign.json \
  --parameters principalId=$principalid roleDefinitionId=$role
```

<span data-ttu-id="f20a5-141">To deploy this template with PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="f20a5-141">To deploy this template with PowerShell, use:</span></span>

```azurepowershell-interactive
$role = Get-AzureRmRoleDefinition -Name Contributor

$adgroup = Get-AzureRmADGroup -DisplayName demogroup

New-AzureRmDeployment `
  -Name demoRole `
  -Location southcentralus `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/azure-resource-manager/roleassign.json `
  -roleDefinitionId $role.Id `
  -principalId $adgroup.Id
```

## <a name="next-steps"></a><span data-ttu-id="f20a5-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="f20a5-142">Next steps</span></span>
* <span data-ttu-id="f20a5-143">For an example of deploying workspace settings for Azure Security Center, see [deployASCwithWorkspaceSettings.json](https://github.com/krnese/AzureDeploy/blob/master/ARM/deployments/deployASCwithWorkspaceSettings.json).</span><span class="sxs-lookup"><span data-stu-id="f20a5-143">For an example of deploying workspace settings for Azure Security Center, see [deployASCwithWorkspaceSettings.json](https://github.com/krnese/AzureDeploy/blob/master/ARM/deployments/deployASCwithWorkspaceSettings.json).</span></span>
* <span data-ttu-id="f20a5-144">To create a resource group, see [Create resource groups in Azure Resource Manager templates](create-resource-group-in-template.md).</span><span class="sxs-lookup"><span data-stu-id="f20a5-144">To create a resource group, see [Create resource groups in Azure Resource Manager templates](create-resource-group-in-template.md).</span></span>
* <span data-ttu-id="f20a5-145">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f20a5-145">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="f20a5-146">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span><span class="sxs-lookup"><span data-stu-id="f20a5-146">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

