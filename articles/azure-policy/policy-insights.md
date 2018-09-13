---
title: Programmatically create policies and view compliance data with Azure Policy
description: This article walks you through programmatically creating and managing policies for Azure Policy.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 05/24/2018
ms.topic: conceptual
ms.service: azure-policy
manager: carmonm
ms.openlocfilehash: ebcfe42bef99319250b64aa1d90b1e717b431932
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869341"
---
# <a name="programmatically-create-policies-and-view-compliance-data"></a><span data-ttu-id="9e72d-103">Programmatically create policies and view compliance data</span><span class="sxs-lookup"><span data-stu-id="9e72d-103">Programmatically create policies and view compliance data</span></span>

<span data-ttu-id="9e72d-104">This article walks you through programmatically creating and managing policies.</span><span class="sxs-lookup"><span data-stu-id="9e72d-104">This article walks you through programmatically creating and managing policies.</span></span> <span data-ttu-id="9e72d-105">It also shows you how to view resource compliance states and polices.</span><span class="sxs-lookup"><span data-stu-id="9e72d-105">It also shows you how to view resource compliance states and polices.</span></span> <span data-ttu-id="9e72d-106">Policy definitions enforce different rules and effects over your resources.</span><span class="sxs-lookup"><span data-stu-id="9e72d-106">Policy definitions enforce different rules and effects over your resources.</span></span> <span data-ttu-id="9e72d-107">Enforcement makes sure that resources stay compliant with your corporate standards and service level agreements.</span><span class="sxs-lookup"><span data-stu-id="9e72d-107">Enforcement makes sure that resources stay compliant with your corporate standards and service level agreements.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e72d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9e72d-108">Prerequisites</span></span>

<span data-ttu-id="9e72d-109">Before you begin, make sure that the following prerequisites are met:</span><span class="sxs-lookup"><span data-stu-id="9e72d-109">Before you begin, make sure that the following prerequisites are met:</span></span>

1. <span data-ttu-id="9e72d-110">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="9e72d-110">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span></span> <span data-ttu-id="9e72d-111">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span><span class="sxs-lookup"><span data-stu-id="9e72d-111">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span></span>
2. <span data-ttu-id="9e72d-112">Update your AzureRM PowerShell module to the latest version.</span><span class="sxs-lookup"><span data-stu-id="9e72d-112">Update your AzureRM PowerShell module to the latest version.</span></span> <span data-ttu-id="9e72d-113">For more information about the latest version, see [Azure PowerShell](https://github.com/Azure/azure-powershell/releases).</span><span class="sxs-lookup"><span data-stu-id="9e72d-113">For more information about the latest version, see [Azure PowerShell](https://github.com/Azure/azure-powershell/releases).</span></span>
3. <span data-ttu-id="9e72d-114">Register the Policy Insights resource provider using Azure PowerShell to ensure that your subscription works with the resource provider.</span><span class="sxs-lookup"><span data-stu-id="9e72d-114">Register the Policy Insights resource provider using Azure PowerShell to ensure that your subscription works with the resource provider.</span></span> <span data-ttu-id="9e72d-115">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="9e72d-115">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span></span> <span data-ttu-id="9e72d-116">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="9e72d-116">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="9e72d-117">Run the following command to register the resource provider:</span><span class="sxs-lookup"><span data-stu-id="9e72d-117">Run the following command to register the resource provider:</span></span>

  ```azurepowershell-interactive
  Register-AzureRmResourceProvider -ProviderNamespace 'Microsoft.PolicyInsights'
  ```

  <span data-ttu-id="9e72d-118">For more information about registering and viewing resource providers, see  [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md).</span><span class="sxs-lookup"><span data-stu-id="9e72d-118">For more information about registering and viewing resource providers, see  [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md).</span></span>
4. <span data-ttu-id="9e72d-119">If you haven't already, install Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="9e72d-119">If you haven't already, install Azure CLI.</span></span> <span data-ttu-id="9e72d-120">You can get the latest version at [Install Azure CLI 2.0 on Windows](/cli/azure/install-azure-cli-windows).</span><span class="sxs-lookup"><span data-stu-id="9e72d-120">You can get the latest version at [Install Azure CLI 2.0 on Windows](/cli/azure/install-azure-cli-windows).</span></span>

## <a name="create-and-assign-a-policy-definition"></a><span data-ttu-id="9e72d-121">Create and assign a policy definition</span><span class="sxs-lookup"><span data-stu-id="9e72d-121">Create and assign a policy definition</span></span>

<span data-ttu-id="9e72d-122">The first step toward better visibility of your resources is to create and assign policies over your resources.</span><span class="sxs-lookup"><span data-stu-id="9e72d-122">The first step toward better visibility of your resources is to create and assign policies over your resources.</span></span> <span data-ttu-id="9e72d-123">The next step is to learn how to programmatically create and assign a policy.</span><span class="sxs-lookup"><span data-stu-id="9e72d-123">The next step is to learn how to programmatically create and assign a policy.</span></span> <span data-ttu-id="9e72d-124">The example policy audits storage accounts that are open to all public networks using PowerShell, Azure CLI, and HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="9e72d-124">The example policy audits storage accounts that are open to all public networks using PowerShell, Azure CLI, and HTTP requests.</span></span>

### <a name="create-and-assign-a-policy-definition-with-powershell"></a><span data-ttu-id="9e72d-125">Create and assign a policy definition with PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e72d-125">Create and assign a policy definition with PowerShell</span></span>

1. <span data-ttu-id="9e72d-126">Use the following JSON snippet to create a JSON file with the name AuditStorageAccounts.json.</span><span class="sxs-lookup"><span data-stu-id="9e72d-126">Use the following JSON snippet to create a JSON file with the name AuditStorageAccounts.json.</span></span>

  ```json
  {
      "if": {
          "allOf": [{
                  "field": "type",
                  "equals": "Microsoft.Storage/storageAccounts"
              },
              {
                  "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
                  "equals": "Allow"
              }
          ]
      },
      "then": {
          "effect": "audit"
      }
  }
  ```

  <span data-ttu-id="9e72d-127">For more information about authoring a policy definition, see [Azure Policy Definition Structure](policy-definition.md).</span><span class="sxs-lookup"><span data-stu-id="9e72d-127">For more information about authoring a policy definition, see [Azure Policy Definition Structure](policy-definition.md).</span></span>
2. <span data-ttu-id="9e72d-128">Run the following command to create a policy definition using the AuditStorageAccounts.json file.</span><span class="sxs-lookup"><span data-stu-id="9e72d-128">Run the following command to create a policy definition using the AuditStorageAccounts.json file.</span></span>

  ```azurepowershell-interactive
  New-AzureRmPolicyDefinition -Name 'AuditStorageAccounts' -DisplayName 'Audit Storage Accounts Open to Public Networks' -Policy 'AuditStorageAccounts.json'
  ```

  <span data-ttu-id="9e72d-129">The command creates a policy definition named _Audit Storage Accounts Open to Public Networks_.</span><span class="sxs-lookup"><span data-stu-id="9e72d-129">The command creates a policy definition named _Audit Storage Accounts Open to Public Networks_.</span></span> <span data-ttu-id="9e72d-130">For more information about other parameters that you can use, see [New-AzureRmPolicyDefinition](/powershell/module/azurerm.resources/new-azurermpolicydefinition).</span><span class="sxs-lookup"><span data-stu-id="9e72d-130">For more information about other parameters that you can use, see [New-AzureRmPolicyDefinition](/powershell/module/azurerm.resources/new-azurermpolicydefinition).</span></span>
3. <span data-ttu-id="9e72d-131">After you create your policy definition, you can create a policy assignment by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="9e72d-131">After you create your policy definition, you can create a policy assignment by running the following commands:</span></span>

  ```azurepowershell-interactive
  $rg = Get-AzureRmResourceGroup -Name 'ContosoRG'
  $Policy = Get-AzureRmPolicyDefinition -Name 'AuditStorageAccounts'
  New-AzureRmPolicyAssignment -Name 'AuditStorageAccounts' -PolicyDefinition $Policy -Scope $rg.ResourceId
  ```

  <span data-ttu-id="9e72d-132">Replace _ContosoRG_ with the name of your intended resource group.</span><span class="sxs-lookup"><span data-stu-id="9e72d-132">Replace _ContosoRG_ with the name of your intended resource group.</span></span>

<span data-ttu-id="9e72d-133">For more information about managing resource policies using the Azure Resource Manager PowerShell module, see [AzureRM.Resources](/powershell/module/azurerm.resources/#policies).</span><span class="sxs-lookup"><span data-stu-id="9e72d-133">For more information about managing resource policies using the Azure Resource Manager PowerShell module, see [AzureRM.Resources](/powershell/module/azurerm.resources/#policies).</span></span>

### <a name="create-and-assign-a-policy-definition-using-armclient"></a><span data-ttu-id="9e72d-134">Create and assign a policy definition using ARMClient</span><span class="sxs-lookup"><span data-stu-id="9e72d-134">Create and assign a policy definition using ARMClient</span></span>

<span data-ttu-id="9e72d-135">Use the following procedure to create a policy definition.</span><span class="sxs-lookup"><span data-stu-id="9e72d-135">Use the following procedure to create a policy definition.</span></span>

1. <span data-ttu-id="9e72d-136">Copy the following JSON snippet to create a JSON file.</span><span class="sxs-lookup"><span data-stu-id="9e72d-136">Copy the following JSON snippet to create a JSON file.</span></span> <span data-ttu-id="9e72d-137">You'll call the file in the next step.</span><span class="sxs-lookup"><span data-stu-id="9e72d-137">You'll call the file in the next step.</span></span>

  ```json
  "properties": {
      "displayName": "Audit Storage Accounts Open to Public Networks",
      "policyType": "Custom",
      "mode": "Indexed",
      "description": "This policy ensures that storage accounts with exposure to Public Networks are audited.",
      "parameters": {},
      "policyRule": {
          "if": {
              "allOf": [{
                      "field": "type",
                      "equals": "Microsoft.Storage/storageAccounts"
                  },
                  {
                      "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
                      "equals": "Allow"
                  }
              ]
          },
          "then": {
              "effect": "audit"
          }
      }
  }
  ```

2. <span data-ttu-id="9e72d-138">Create the policy definition using one of the following calls:</span><span class="sxs-lookup"><span data-stu-id="9e72d-138">Create the policy definition using one of the following calls:</span></span>

  ```
  # For defining a policy in a subscription
  armclient PUT "/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/AuditStorageAccounts?api-version=2016-12-01" @<path to policy definition JSON file>

  # For defining a policy in a management group
  armclient PUT "/providers/Microsoft.Management/managementgroups/{managementGroupId}/providers/Microsoft.Authorization/policyDefinitions/AuditStorageAccounts?api-version=2016-12-01" @<path to policy definition JSON file>
  ```

  <span data-ttu-id="9e72d-139">Replace the preceding {subscriptionId} with the ID of your subscription or {managementGroupId} with the ID of your [management group](../azure-resource-manager/management-groups-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9e72d-139">Replace the preceding {subscriptionId} with the ID of your subscription or {managementGroupId} with the ID of your [management group](../azure-resource-manager/management-groups-overview.md).</span></span>

  <span data-ttu-id="9e72d-140">For more information about the structure of the query, see [Policy Definitions – Create or Update](/rest/api/resources/policydefinitions/createorupdate) and [Policy Definitions – Create or Update At Management Group](/rest/api/resources/policydefinitions/createorupdateatmanagementgroup)</span><span class="sxs-lookup"><span data-stu-id="9e72d-140">For more information about the structure of the query, see [Policy Definitions – Create or Update](/rest/api/resources/policydefinitions/createorupdate) and [Policy Definitions – Create or Update At Management Group](/rest/api/resources/policydefinitions/createorupdateatmanagementgroup)</span></span>

<span data-ttu-id="9e72d-141">Use the following procedure to create a policy assignment and assign the policy definition at the resource group level.</span><span class="sxs-lookup"><span data-stu-id="9e72d-141">Use the following procedure to create a policy assignment and assign the policy definition at the resource group level.</span></span>

1. <span data-ttu-id="9e72d-142">Copy the following JSON snippet to create a JSON policy assignment file.</span><span class="sxs-lookup"><span data-stu-id="9e72d-142">Copy the following JSON snippet to create a JSON policy assignment file.</span></span> <span data-ttu-id="9e72d-143">Replace example information in &lt;&gt; symbols with your own values.</span><span class="sxs-lookup"><span data-stu-id="9e72d-143">Replace example information in &lt;&gt; symbols with your own values.</span></span>

  ```json
  {
      "properties": {
          "description": "This policy assignment makes sure that storage accounts with exposure to Public Networks are audited.",
          "displayName": "Audit Storage Accounts Open to Public Networks Assignment",
          "parameters": {},
          "policyDefinitionId": "/subscriptions/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/Audit Storage Accounts Open to Public Networks",
          "scope": "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>"
      }
  }
  ```

2. <span data-ttu-id="9e72d-144">Create the policy assignment using the following call:</span><span class="sxs-lookup"><span data-stu-id="9e72d-144">Create the policy assignment using the following call:</span></span>

  ```
  armclient PUT "/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>/providers/Microsoft.Authorization/policyAssignments/Audit Storage Accounts Open to Public Networks?api-version=2017-06-01-preview" @<path to Assignment JSON file>
  ```

  <span data-ttu-id="9e72d-145">Replace example information in &lt;&gt; symbols with your own values.</span><span class="sxs-lookup"><span data-stu-id="9e72d-145">Replace example information in &lt;&gt; symbols with your own values.</span></span>

  <span data-ttu-id="9e72d-146">For more information about making HTTP calls to the REST API, see [Azure REST API Resources](/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="9e72d-146">For more information about making HTTP calls to the REST API, see [Azure REST API Resources](/rest/api/resources/).</span></span>

### <a name="create-and-assign-a-policy-definition-with-azure-cli"></a><span data-ttu-id="9e72d-147">Create and assign a policy definition with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9e72d-147">Create and assign a policy definition with Azure CLI</span></span>

<span data-ttu-id="9e72d-148">To create a policy definition, use the following procedure:</span><span class="sxs-lookup"><span data-stu-id="9e72d-148">To create a policy definition, use the following procedure:</span></span>

1. <span data-ttu-id="9e72d-149">Copy the following JSON snippet to create a JSON policy assignment file.</span><span class="sxs-lookup"><span data-stu-id="9e72d-149">Copy the following JSON snippet to create a JSON policy assignment file.</span></span>

  ```json
  {
      "if": {
          "allOf": [{
                  "field": "type",
                  "equals": "Microsoft.Storage/storageAccounts"
              },
              {
                  "field": "Microsoft.Storage/storageAccounts/networkAcls.defaultAction",
                  "equals": "Allow"
              }
          ]
      },
      "then": {
          "effect": "audit"
      }
  }
  ```

2. <span data-ttu-id="9e72d-150">Run the following command to create a policy definition:</span><span class="sxs-lookup"><span data-stu-id="9e72d-150">Run the following command to create a policy definition:</span></span>

  ```azurecli-interactive
az policy definition create --name 'audit-storage-accounts-open-to-public-networks' --display-name 'Audit Storage Accounts Open to Public Networks' --description 'This policy ensures that storage accounts with exposures to public networks are audited.' --rules '<path to json file>' --mode All
  ```

3. <span data-ttu-id="9e72d-151">Use the following command to create a policy assignment.</span><span class="sxs-lookup"><span data-stu-id="9e72d-151">Use the following command to create a policy assignment.</span></span> <span data-ttu-id="9e72d-152">Replace example information in &lt;&gt; symbols with your own values.</span><span class="sxs-lookup"><span data-stu-id="9e72d-152">Replace example information in &lt;&gt; symbols with your own values.</span></span>

  ```azurecli-interactive
  az policy assignment create --name '<name>' --scope '<scope>' --policy '<policy definition ID>'
  ```

<span data-ttu-id="9e72d-153">You can get the Policy Definition ID by using PowerShell with the following command:</span><span class="sxs-lookup"><span data-stu-id="9e72d-153">You can get the Policy Definition ID by using PowerShell with the following command:</span></span>

```azurecli-interactive
az policy definition show --name 'Audit Storage Accounts with Open Public Networks'
```

<span data-ttu-id="9e72d-154">The policy definition ID for the policy definition that you created should resemble the following example:</span><span class="sxs-lookup"><span data-stu-id="9e72d-154">The policy definition ID for the policy definition that you created should resemble the following example:</span></span>

```
"/subscription/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/Audit Storage Accounts Open to Public Networks"
```

<span data-ttu-id="9e72d-155">For more information about how you can manage resource policies with Azure CLI, see [Azure CLI Resource Policies](/cli/azure/policy?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="9e72d-155">For more information about how you can manage resource policies with Azure CLI, see [Azure CLI Resource Policies](/cli/azure/policy?view=azure-cli-latest).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e72d-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e72d-156">Next steps</span></span>

<span data-ttu-id="9e72d-157">Review the following articles for more information about the commands and queries in this article.</span><span class="sxs-lookup"><span data-stu-id="9e72d-157">Review the following articles for more information about the commands and queries in this article.</span></span>

- [<span data-ttu-id="9e72d-158">Azure REST API Resources</span><span class="sxs-lookup"><span data-stu-id="9e72d-158">Azure REST API Resources</span></span>](/rest/api/resources/)
- [<span data-ttu-id="9e72d-159">Azure RM PowerShell Modules</span><span class="sxs-lookup"><span data-stu-id="9e72d-159">Azure RM PowerShell Modules</span></span>](/powershell/module/azurerm.resources/#policies)
- [<span data-ttu-id="9e72d-160">Azure CLI Policy Commands</span><span class="sxs-lookup"><span data-stu-id="9e72d-160">Azure CLI Policy Commands</span></span>](/cli/azure/policy?view=azure-cli-latest)
- [<span data-ttu-id="9e72d-161">Policy Insights resource provider REST API reference</span><span class="sxs-lookup"><span data-stu-id="9e72d-161">Policy Insights resource provider REST API reference</span></span>](/rest/api/policy-insights)
- [<span data-ttu-id="9e72d-162">Organize your resources with Azure management groups</span><span class="sxs-lookup"><span data-stu-id="9e72d-162">Organize your resources with Azure management groups</span></span>](../azure-resource-manager/management-groups-overview.md)