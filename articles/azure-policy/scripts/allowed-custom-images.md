---
title: Azure Policy sample - Approved VM images
description: This policy requires that only approved custom images are deployed in your environment.
services: azure-policy
author: DCtheGeek
manager: carmonm
ms.service: azure-policy
ms.topic: sample
ms.date: 06/03/2018
ms.author: dacoulte
ms.custom: mvc
ms.openlocfilehash: b7506f858271ae9b4346a5253b1207f1b8e3f15e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869413"
---
# <a name="approved-vm-images"></a><span data-ttu-id="985ed-103">Approved VM images</span><span class="sxs-lookup"><span data-stu-id="985ed-103">Approved VM images</span></span>

<span data-ttu-id="985ed-104">This policy requires that only approved custom images are deployed in your environment.</span><span class="sxs-lookup"><span data-stu-id="985ed-104">This policy requires that only approved custom images are deployed in your environment.</span></span> <span data-ttu-id="985ed-105">You specify an array of approved image IDs.</span><span class="sxs-lookup"><span data-stu-id="985ed-105">You specify an array of approved image IDs.</span></span>

<span data-ttu-id="985ed-106">You can deploy this sample policy using:</span><span class="sxs-lookup"><span data-stu-id="985ed-106">You can deploy this sample policy using:</span></span>

- <span data-ttu-id="985ed-107">The [Azure portal](#azure-portal)</span><span class="sxs-lookup"><span data-stu-id="985ed-107">The [Azure portal](#azure-portal)</span></span>
- [<span data-ttu-id="985ed-108">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="985ed-108">Azure PowerShell</span></span>](#azure-powershell)
- [<span data-ttu-id="985ed-109">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="985ed-109">Azure CLI</span></span>](#azure-cli)
- [<span data-ttu-id="985ed-110">REST API</span><span class="sxs-lookup"><span data-stu-id="985ed-110">REST API</span></span>](#rest-api)

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-policy"></a><span data-ttu-id="985ed-111">Sample policy</span><span class="sxs-lookup"><span data-stu-id="985ed-111">Sample policy</span></span>

### <a name="policy-definition"></a><span data-ttu-id="985ed-112">Policy definition</span><span class="sxs-lookup"><span data-stu-id="985ed-112">Policy definition</span></span>

<span data-ttu-id="985ed-113">The complete composed JSON policy definition, used by the REST API, 'Deploy to Azure' buttons, and manually in the portal.</span><span class="sxs-lookup"><span data-stu-id="985ed-113">The complete composed JSON policy definition, used by the REST API, 'Deploy to Azure' buttons, and manually in the portal.</span></span>

[!code-json[full](../../../policy-templates/samples/compute/allowed-custom-images/azurepolicy.json "Complete policy definition (JSON)")]

> [!NOTE]
> <span data-ttu-id="985ed-114">If manually creating a policy in the portal, use the **properties.parameters** and **properties.policyRule** portions of the above.</span><span class="sxs-lookup"><span data-stu-id="985ed-114">If manually creating a policy in the portal, use the **properties.parameters** and **properties.policyRule** portions of the above.</span></span> <span data-ttu-id="985ed-115">Wrap the two sections together with curly braces `{}` to make it valid JSON.</span><span class="sxs-lookup"><span data-stu-id="985ed-115">Wrap the two sections together with curly braces `{}` to make it valid JSON.</span></span>

### <a name="policy-rules"></a><span data-ttu-id="985ed-116">Policy rules</span><span class="sxs-lookup"><span data-stu-id="985ed-116">Policy rules</span></span>

<span data-ttu-id="985ed-117">The JSON defining the rules of the policy, used by Azure CLI and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="985ed-117">The JSON defining the rules of the policy, used by Azure CLI and Azure PowerShell.</span></span>

[!code-json[rule](../../../policy-templates/samples/compute/allowed-custom-images/azurepolicy.rules.json "Policy rules (JSON)")]

### <a name="policy-parameters"></a><span data-ttu-id="985ed-118">Policy parameters</span><span class="sxs-lookup"><span data-stu-id="985ed-118">Policy parameters</span></span>

<span data-ttu-id="985ed-119">The JSON defining the policy parameters, used by Azure CLI and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="985ed-119">The JSON defining the policy parameters, used by Azure CLI and Azure PowerShell.</span></span>

[!code-json[parameters](../../../policy-templates/samples/compute/allowed-custom-images/azurepolicy.parameters.json "Policy parameters (JSON)")]

## <a name="parameters"></a><span data-ttu-id="985ed-120">Parameters</span><span class="sxs-lookup"><span data-stu-id="985ed-120">Parameters</span></span>

|<span data-ttu-id="985ed-121">Name</span><span class="sxs-lookup"><span data-stu-id="985ed-121">Name</span></span> |<span data-ttu-id="985ed-122">Type</span><span class="sxs-lookup"><span data-stu-id="985ed-122">Type</span></span> |<span data-ttu-id="985ed-123">Field</span><span class="sxs-lookup"><span data-stu-id="985ed-123">Field</span></span> |<span data-ttu-id="985ed-124">Description</span><span class="sxs-lookup"><span data-stu-id="985ed-124">Description</span></span> |
|---|---|---|---|
|<span data-ttu-id="985ed-125">imageIds</span><span class="sxs-lookup"><span data-stu-id="985ed-125">imageIds</span></span> |<span data-ttu-id="985ed-126">Array</span><span class="sxs-lookup"><span data-stu-id="985ed-126">Array</span></span> |<span data-ttu-id="985ed-127">Microsoft.Compute/imageIds</span><span class="sxs-lookup"><span data-stu-id="985ed-127">Microsoft.Compute/imageIds</span></span> |<span data-ttu-id="985ed-128">The list of approved VM images</span><span class="sxs-lookup"><span data-stu-id="985ed-128">The list of approved VM images</span></span>|

<span data-ttu-id="985ed-129">When creating an assignment via PowerShell or Azure CLI, the parameter values can be passed as JSON in either a string or via a file using `-PolicyParameter` (PowerShell) or `--params` (Azure CLI).</span><span class="sxs-lookup"><span data-stu-id="985ed-129">When creating an assignment via PowerShell or Azure CLI, the parameter values can be passed as JSON in either a string or via a file using `-PolicyParameter` (PowerShell) or `--params` (Azure CLI).</span></span>
<span data-ttu-id="985ed-130">PowerShell also supports `-PolicyParameterObject` which requires passing the cmdlet a Name/Value hashtable where **Name** is the parameter name and **Value** is the single value or array of values being passed during assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-130">PowerShell also supports `-PolicyParameterObject` which requires passing the cmdlet a Name/Value hashtable where **Name** is the parameter name and **Value** is the single value or array of values being passed during assignment.</span></span>

<span data-ttu-id="985ed-131">In this example parameter, only the _ContosoStdImage_ in resource group _YourResourceGroup_ or the May 2018 image version of Windows Server 2016 Datacenter located in 'Central US' will be allowed.</span><span class="sxs-lookup"><span data-stu-id="985ed-131">In this example parameter, only the _ContosoStdImage_ in resource group _YourResourceGroup_ or the May 2018 image version of Windows Server 2016 Datacenter located in 'Central US' will be allowed.</span></span>

```json
{
    "imageIds": {
        "value": [
            "/subscriptions/<subscriptionId>/resourceGroups/YourResourceGroup/providers/Microsoft.Compute/images/ContosoStdImage",
            "/Subscriptions/<subscriptionId>/Providers/Microsoft.Compute/Locations/centralus/Publishers/MicrosoftWindowsServer/ArtifactTypes/VMImage/Offers/WindowsServer/Skus/2016-Datacenter/Versions/2016.127.20180510"
        ]
    }
}
```

## <a name="azure-portal"></a><span data-ttu-id="985ed-132">Azure portal</span><span class="sxs-lookup"><span data-stu-id="985ed-132">Azure portal</span></span>

<span data-ttu-id="985ed-133">[![Deploy to Azure](../media/deploy/deploybutton.png)](https://portal.azure.com/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fallowed-custom-images%2Fazurepolicy.json)
[![Deploy to Azure Gov](../media/deploy/deployGovbutton.png)](https://portal.azure.us/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fallowed-custom-images%2Fazurepolicy.json)</span><span class="sxs-lookup"><span data-stu-id="985ed-133">[![Deploy to Azure](../media/deploy/deploybutton.png)](https://portal.azure.com/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fallowed-custom-images%2Fazurepolicy.json)
[![Deploy to Azure Gov](../media/deploy/deployGovbutton.png)](https://portal.azure.us/?#blade/Microsoft_Azure_Policy/CreatePolicyDefinitionBlade/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-policy%2Fmaster%2Fsamples%2FCompute%2Fallowed-custom-images%2Fazurepolicy.json)</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="985ed-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="985ed-134">Azure PowerShell</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

### <a name="deploy-with-azure-powershell"></a><span data-ttu-id="985ed-135">Deploy with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="985ed-135">Deploy with Azure PowerShell</span></span>

```azurepowershell-interactive
# Create the Policy Definition (Subscription scope)
$definition = New-AzureRmPolicyDefinition -Name 'allowed-custom-images' -DisplayName 'Approved VM images' -description 'This policy governs the approved VM images' -Policy 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/allowed-custom-images/azurepolicy.rules.json' -Parameter 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/allowed-custom-images/azurepolicy.parameters.json' -Mode All

# Set the scope to a resource group; may also be a subscription or management group
$scope = Get-AzureRmResourceGroup -Name 'YourResourceGroup'

# Set the Policy Parameter (JSON format)
$policyparam = '{ "imageIds": { "value": [ "/subscriptions/<subscriptionId>/resourceGroups/YourResourceGroup/providers/Microsoft.Compute/images/ContosoStdImage", "/Subscriptions/<subscriptionId>/Providers/Microsoft.Compute/Locations/centralus/Publishers/MicrosoftWindowsServer/ArtifactTypes/VMImage/Offers/WindowsServer/Skus/2016-Datacenter/Versions/2016.127.20180510" ] } }'

# Create the Policy Assignment
$assignment = New-AzureRmPolicyAssignment -Name 'allowed-custom-images-assignment' -DisplayName 'Approved VM images Assignment' -Scope $scope.ResourceId -PolicyDefinition $definition -PolicyParameter $policyparam
```

### <a name="remove-with-azure-powershell"></a><span data-ttu-id="985ed-136">Remove with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="985ed-136">Remove with Azure PowerShell</span></span>

<span data-ttu-id="985ed-137">Run the following commands to remove the previous assignment and definition:</span><span class="sxs-lookup"><span data-stu-id="985ed-137">Run the following commands to remove the previous assignment and definition:</span></span>

```azurepowershell-interactive
# Remove the Policy Assignment
Remove-AzureRmPolicyAssignment -Id $assignment.ResourceId

# Remove the Policy Definition
Remove-AzureRmPolicyDefinition -Id $definition.ResourceId
```

### <a name="azure-powershell-explanation"></a><span data-ttu-id="985ed-138">Azure PowerShell explanation</span><span class="sxs-lookup"><span data-stu-id="985ed-138">Azure PowerShell explanation</span></span>

<span data-ttu-id="985ed-139">The deploy and remove scripts use the following commands.</span><span class="sxs-lookup"><span data-stu-id="985ed-139">The deploy and remove scripts use the following commands.</span></span> <span data-ttu-id="985ed-140">Each command in the following table links to command-specific documentation:</span><span class="sxs-lookup"><span data-stu-id="985ed-140">Each command in the following table links to command-specific documentation:</span></span>

| <span data-ttu-id="985ed-141">Command</span><span class="sxs-lookup"><span data-stu-id="985ed-141">Command</span></span> | <span data-ttu-id="985ed-142">Notes</span><span class="sxs-lookup"><span data-stu-id="985ed-142">Notes</span></span> |
|---|---|
| [<span data-ttu-id="985ed-143">New-AzureRmPolicyDefinition</span><span class="sxs-lookup"><span data-stu-id="985ed-143">New-AzureRmPolicyDefinition</span></span>](/powershell/module/azurerm.resources/new-azurermpolicydefinition) | <span data-ttu-id="985ed-144">Creates a new Azure Policy definition.</span><span class="sxs-lookup"><span data-stu-id="985ed-144">Creates a new Azure Policy definition.</span></span> |
| [<span data-ttu-id="985ed-145">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="985ed-145">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="985ed-146">Gets a single resource group.</span><span class="sxs-lookup"><span data-stu-id="985ed-146">Gets a single resource group.</span></span> |
| [<span data-ttu-id="985ed-147">New-AzureRmPolicyAssignment</span><span class="sxs-lookup"><span data-stu-id="985ed-147">New-AzureRmPolicyAssignment</span></span>](/powershell/module/azurerm.resources/new-azurermpolicyassignment) | <span data-ttu-id="985ed-148">Creates a new Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-148">Creates a new Azure Policy assignment.</span></span> <span data-ttu-id="985ed-149">In this example, we provide it a definition, but it can also take an initiative.</span><span class="sxs-lookup"><span data-stu-id="985ed-149">In this example, we provide it a definition, but it can also take an initiative.</span></span> |
| [<span data-ttu-id="985ed-150">Remove-AzureRmPolicyAssignment</span><span class="sxs-lookup"><span data-stu-id="985ed-150">Remove-AzureRmPolicyAssignment</span></span>](/powershell/module/azurerm.resources/remove-azurermpolicyassignment) | <span data-ttu-id="985ed-151">Removes an existing Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-151">Removes an existing Azure Policy assignment.</span></span> |
| [<span data-ttu-id="985ed-152">Remove-AzureRmPolicyDefinition</span><span class="sxs-lookup"><span data-stu-id="985ed-152">Remove-AzureRmPolicyDefinition</span></span>](/powershell/module/azurerm.resources/remove-azurermpolicydefinition) | <span data-ttu-id="985ed-153">Removes an existing Azure Policy definition.</span><span class="sxs-lookup"><span data-stu-id="985ed-153">Removes an existing Azure Policy definition.</span></span> |

## <a name="azure-cli"></a><span data-ttu-id="985ed-154">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="985ed-154">Azure CLI</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

### <a name="deploy-with-azure-cli"></a><span data-ttu-id="985ed-155">Deploy with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="985ed-155">Deploy with Azure CLI</span></span>

```azurecli-interactive
# Create the Policy Definition (Subscription scope)
definition=$(az policy definition create --name 'allowed-custom-images' --display-name 'Approved VM images' --description 'This policy governs the approved VM images' --rules 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/allowed-custom-images/azurepolicy.rules.json' --params 'https://raw.githubusercontent.com/Azure/azure-policy/master/samples/Compute/allowed-custom-images/azurepolicy.parameters.json' --mode All)

# Set the scope to a resource group; may also be a subscription or management group
scope=$(az group show --name 'YourResourceGroup')

# Set the Policy Parameter (JSON format)
policyparam='{ "imageIds": { "value": [ "/subscriptions/<subscriptionId>/resourceGroups/YourResourceGroup/providers/Microsoft.Compute/images/ContosoStdImage", "/Subscriptions/<subscriptionId>/Providers/Microsoft.Compute/Locations/centralus/Publishers/MicrosoftWindowsServer/ArtifactTypes/VMImage/Offers/WindowsServer/Skus/2016-Datacenter/Versions/2016.127.20180510" ] } }'

# Create the Policy Assignment
assignment=$(az policy assignment create --name 'allowed-custom-images-assignment' --display-name 'Approved VM images Assignment' --scope `echo $scope | jq '.id' -r` --policy `echo $definition | jq '.name' -r` --params "$policyparam")
```

### <a name="remove-with-azure-cli"></a><span data-ttu-id="985ed-156">Remove with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="985ed-156">Remove with Azure CLI</span></span>

<span data-ttu-id="985ed-157">Run the following commands to remove the previous assignment and definition:</span><span class="sxs-lookup"><span data-stu-id="985ed-157">Run the following commands to remove the previous assignment and definition:</span></span>

```azurecli-interactive
# Remove the Policy Assignment
az policy assignment delete --name `echo $assignment | jq '.name' -r`

# Remove the Policy Definition
az policy definition delete --name `echo $definition | jq '.name' -r`
```

### <a name="azure-cli-explanation"></a><span data-ttu-id="985ed-158">Azure CLI explanation</span><span class="sxs-lookup"><span data-stu-id="985ed-158">Azure CLI explanation</span></span>

| <span data-ttu-id="985ed-159">Command</span><span class="sxs-lookup"><span data-stu-id="985ed-159">Command</span></span> | <span data-ttu-id="985ed-160">Notes</span><span class="sxs-lookup"><span data-stu-id="985ed-160">Notes</span></span> |
|---|---|
| [<span data-ttu-id="985ed-161">az policy definition create</span><span class="sxs-lookup"><span data-stu-id="985ed-161">az policy definition create</span></span>](/cli/azure/policy/definition?view=azure-cli-latest#az-policy-definition-create) | <span data-ttu-id="985ed-162">Creates a new Azure Policy definition.</span><span class="sxs-lookup"><span data-stu-id="985ed-162">Creates a new Azure Policy definition.</span></span> |
| [<span data-ttu-id="985ed-163">az group show</span><span class="sxs-lookup"><span data-stu-id="985ed-163">az group show</span></span>](/cli/azure/group?view=azure-cli-latest#az-group-show) | <span data-ttu-id="985ed-164">Gets a single resource group.</span><span class="sxs-lookup"><span data-stu-id="985ed-164">Gets a single resource group.</span></span> |
| [<span data-ttu-id="985ed-165">az policy assignment create</span><span class="sxs-lookup"><span data-stu-id="985ed-165">az policy assignment create</span></span>](/cli/azure/policy/assignment?view=azure-cli-latest#az-policy-assignment-create) | <span data-ttu-id="985ed-166">Creates a new Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-166">Creates a new Azure Policy assignment.</span></span> <span data-ttu-id="985ed-167">In this example, we provide it a definition, but it can also take an initiative.</span><span class="sxs-lookup"><span data-stu-id="985ed-167">In this example, we provide it a definition, but it can also take an initiative.</span></span> |
| [<span data-ttu-id="985ed-168">az policy assignment delete</span><span class="sxs-lookup"><span data-stu-id="985ed-168">az policy assignment delete</span></span>](/cli/azure/policy/assignment?view=azure-cli-latest#az-policy-assignment-delete) | <span data-ttu-id="985ed-169">Removes an existing Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-169">Removes an existing Azure Policy assignment.</span></span> |
| [<span data-ttu-id="985ed-170">az policy definition delete</span><span class="sxs-lookup"><span data-stu-id="985ed-170">az policy definition delete</span></span>](/cli/azure/policy/definition?view=azure-cli-latest#az-policy-definition-delete) | <span data-ttu-id="985ed-171">Removes an existing Azure Policy definition.</span><span class="sxs-lookup"><span data-stu-id="985ed-171">Removes an existing Azure Policy definition.</span></span> |

## <a name="rest-api"></a><span data-ttu-id="985ed-172">REST API</span><span class="sxs-lookup"><span data-stu-id="985ed-172">REST API</span></span>

<span data-ttu-id="985ed-173">There are several tools that can be used to interact with the Resource Manager REST API such as [ARMClient](https://github.com/projectkudu/ARMClient) or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="985ed-173">There are several tools that can be used to interact with the Resource Manager REST API such as [ARMClient](https://github.com/projectkudu/ARMClient) or PowerShell.</span></span> <span data-ttu-id="985ed-174">An example of calling REST API from PowerShell can be found in the **Aliases** section of [Policy definition structure](../policy-definition.md#aliases).</span><span class="sxs-lookup"><span data-stu-id="985ed-174">An example of calling REST API from PowerShell can be found in the **Aliases** section of [Policy definition structure](../policy-definition.md#aliases).</span></span>

### <a name="deploy-with-rest-api"></a><span data-ttu-id="985ed-175">Deploy with REST API</span><span class="sxs-lookup"><span data-stu-id="985ed-175">Deploy with REST API</span></span>

- <span data-ttu-id="985ed-176">Create the Policy Definition (Subscription scope).</span><span class="sxs-lookup"><span data-stu-id="985ed-176">Create the Policy Definition (Subscription scope).</span></span> <span data-ttu-id="985ed-177">Use the [policy definition](#policy-definition) JSON for the Request Body.</span><span class="sxs-lookup"><span data-stu-id="985ed-177">Use the [policy definition](#policy-definition) JSON for the Request Body.</span></span>

  ```http
  PUT https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/allowed-custom-images?api-version=2016-12-01
  ```

- <span data-ttu-id="985ed-178">Create the Policy Assignment (Resource Group scope)</span><span class="sxs-lookup"><span data-stu-id="985ed-178">Create the Policy Assignment (Resource Group scope)</span></span>

  ```http
  PUT https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/YourResourceGroup/providers/Microsoft.Authorization/policyAssignments/allowed-custom-images-assignment?api-version=2017-06-01-preview
  ```

  <span data-ttu-id="985ed-179">Use the following JSON example for the Request Body:</span><span class="sxs-lookup"><span data-stu-id="985ed-179">Use the following JSON example for the Request Body:</span></span>

  ```json
  {
      "properties": {
          "displayName": "Approved VM images Assignment",
          "policyDefinitionId": "/subscriptions/<subscriptionId>/providers/Microsoft.Authorization/policyDefinitions/allowed-custom-images",
          "parameters": {
              "imageIds": {
                  "value": [
                      "/subscriptions/<subscriptionId>/resourceGroups/YourResourceGroup/providers/Microsoft.Compute/images/ContosoStdImage",
                      "/Subscriptions/<subscriptionId>/Providers/Microsoft.Compute/Locations/centralus/Publishers/MicrosoftWindowsServer/ArtifactTypes/VMImage/Offers/WindowsServer/Skus/2016-Datacenter/Versions/2016.127.20180510"
                  ]
              }
          }
      }
  }
  ```

### <a name="remove-with-rest-api"></a><span data-ttu-id="985ed-180">Remove with REST API</span><span class="sxs-lookup"><span data-stu-id="985ed-180">Remove with REST API</span></span>

- <span data-ttu-id="985ed-181">Remove the Policy Assignment</span><span class="sxs-lookup"><span data-stu-id="985ed-181">Remove the Policy Assignment</span></span>

  ```http
  DELETE https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyAssignments/allowed-custom-images-assignment?api-version=2017-06-01-preview
  ```

- <span data-ttu-id="985ed-182">Remove the Policy Definition</span><span class="sxs-lookup"><span data-stu-id="985ed-182">Remove the Policy Definition</span></span>

  ```http
  DELETE https://management.azure.com/subscriptions/{subscriptionId}/providers/Microsoft.Authorization/policyDefinitions/allowed-custom-images?api-version=2016-12-01
  ```

### <a name="rest-api-explanation"></a><span data-ttu-id="985ed-183">REST API explanation</span><span class="sxs-lookup"><span data-stu-id="985ed-183">REST API explanation</span></span>

| <span data-ttu-id="985ed-184">Service</span><span class="sxs-lookup"><span data-stu-id="985ed-184">Service</span></span> | <span data-ttu-id="985ed-185">Group</span><span class="sxs-lookup"><span data-stu-id="985ed-185">Group</span></span> | <span data-ttu-id="985ed-186">Operation</span><span class="sxs-lookup"><span data-stu-id="985ed-186">Operation</span></span> | <span data-ttu-id="985ed-187">Notes</span><span class="sxs-lookup"><span data-stu-id="985ed-187">Notes</span></span> |
|---|---|---|---|
| <span data-ttu-id="985ed-188">Resource Management</span><span class="sxs-lookup"><span data-stu-id="985ed-188">Resource Management</span></span> | <span data-ttu-id="985ed-189">Policy Definitions</span><span class="sxs-lookup"><span data-stu-id="985ed-189">Policy Definitions</span></span> | [<span data-ttu-id="985ed-190">Create</span><span class="sxs-lookup"><span data-stu-id="985ed-190">Create</span></span>](/rest/api/resources/policydefinitions/createorupdate) | <span data-ttu-id="985ed-191">Creates a new Azure Policy definition at a subscription.</span><span class="sxs-lookup"><span data-stu-id="985ed-191">Creates a new Azure Policy definition at a subscription.</span></span> <span data-ttu-id="985ed-192">Alternative: [Create at management group](/rest/api/resources/policydefinitions/createorupdateatmanagementgroup)</span><span class="sxs-lookup"><span data-stu-id="985ed-192">Alternative: [Create at management group](/rest/api/resources/policydefinitions/createorupdateatmanagementgroup)</span></span> |
| <span data-ttu-id="985ed-193">Resource Management</span><span class="sxs-lookup"><span data-stu-id="985ed-193">Resource Management</span></span> | <span data-ttu-id="985ed-194">Policy Assignments</span><span class="sxs-lookup"><span data-stu-id="985ed-194">Policy Assignments</span></span> | [<span data-ttu-id="985ed-195">Create</span><span class="sxs-lookup"><span data-stu-id="985ed-195">Create</span></span>](/rest/api/resources/policyassignments/create) | <span data-ttu-id="985ed-196">Creates a new Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-196">Creates a new Azure Policy assignment.</span></span> <span data-ttu-id="985ed-197">In this example, we provide it a definition, but it can also take an initiative.</span><span class="sxs-lookup"><span data-stu-id="985ed-197">In this example, we provide it a definition, but it can also take an initiative.</span></span> |
| <span data-ttu-id="985ed-198">Resource Management</span><span class="sxs-lookup"><span data-stu-id="985ed-198">Resource Management</span></span> | <span data-ttu-id="985ed-199">Policy Assignments</span><span class="sxs-lookup"><span data-stu-id="985ed-199">Policy Assignments</span></span> | [<span data-ttu-id="985ed-200">Delete</span><span class="sxs-lookup"><span data-stu-id="985ed-200">Delete</span></span>](/rest/api/resources/policyassignments/delete) | <span data-ttu-id="985ed-201">Removes an existing Azure Policy assignment.</span><span class="sxs-lookup"><span data-stu-id="985ed-201">Removes an existing Azure Policy assignment.</span></span> |
| <span data-ttu-id="985ed-202">Resource Management</span><span class="sxs-lookup"><span data-stu-id="985ed-202">Resource Management</span></span> | <span data-ttu-id="985ed-203">Policy Definitions</span><span class="sxs-lookup"><span data-stu-id="985ed-203">Policy Definitions</span></span> | [<span data-ttu-id="985ed-204">Delete</span><span class="sxs-lookup"><span data-stu-id="985ed-204">Delete</span></span>](/rest/api/resources/policydefinitions/delete) | <span data-ttu-id="985ed-205">Removes an existing Azure Policy definition.</span><span class="sxs-lookup"><span data-stu-id="985ed-205">Removes an existing Azure Policy definition.</span></span> <span data-ttu-id="985ed-206">Alternative: [Delete at management group](/rest/api/resources/policydefinitions/deleteatmanagementgroup)</span><span class="sxs-lookup"><span data-stu-id="985ed-206">Alternative: [Delete at management group](/rest/api/resources/policydefinitions/deleteatmanagementgroup)</span></span> |

## <a name="next-steps"></a><span data-ttu-id="985ed-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="985ed-207">Next steps</span></span>

- <span data-ttu-id="985ed-208">Review additional [Azure Policy samples](../json-samples.md)</span><span class="sxs-lookup"><span data-stu-id="985ed-208">Review additional [Azure Policy samples](../json-samples.md)</span></span>
- <span data-ttu-id="985ed-209">Review [Azure Policy definition structure](../policy-definition.md)</span><span class="sxs-lookup"><span data-stu-id="985ed-209">Review [Azure Policy definition structure](../policy-definition.md)</span></span>
- <span data-ttu-id="985ed-210">See Azure Policy examples for Virtual Machines at [Apply policies to Windows VMs](../../virtual-machines/windows/policy.md)</span><span class="sxs-lookup"><span data-stu-id="985ed-210">See Azure Policy examples for Virtual Machines at [Apply policies to Windows VMs](../../virtual-machines/windows/policy.md)</span></span>