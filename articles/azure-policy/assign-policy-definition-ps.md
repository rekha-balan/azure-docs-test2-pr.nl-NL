---
title: Quickstart - Use PowerShell to create a policy assignment to identify non-compliant resources in your Azure environment
description: In this quickstart, you use PowerShell to create an Azure Policy assignment to identify non-compliant resources.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 05/24/2018
ms.topic: quickstart
ms.service: azure-policy
ms.custom: mvc
manager: carmonm
ms.openlocfilehash: 92e1d94f9d68e6d877e2c39b71151dee77f5a49f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856491"
---
# <a name="quickstart-create-a-policy-assignment-to-identify-non-compliant-resources-using-the-azure-rm-powershell-module"></a><span data-ttu-id="66a24-103">Quickstart: Create a policy assignment to identify non-compliant resources using the Azure RM PowerShell module</span><span class="sxs-lookup"><span data-stu-id="66a24-103">Quickstart: Create a policy assignment to identify non-compliant resources using the Azure RM PowerShell module</span></span>

<span data-ttu-id="66a24-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span><span class="sxs-lookup"><span data-stu-id="66a24-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span></span> <span data-ttu-id="66a24-105">In this quickstart, you create a policy assignment to identify virtual machines that are not using managed disks.</span><span class="sxs-lookup"><span data-stu-id="66a24-105">In this quickstart, you create a policy assignment to identify virtual machines that are not using managed disks.</span></span> <span data-ttu-id="66a24-106">When complete, you'll identify virtual machines that are *non-compliant* with the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="66a24-106">When complete, you'll identify virtual machines that are *non-compliant* with the policy assignment.</span></span>

<span data-ttu-id="66a24-107">The AzureRM PowerShell module is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="66a24-107">The AzureRM PowerShell module is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="66a24-108">This guide explains how to use AzureRM to create a policy assignment.</span><span class="sxs-lookup"><span data-stu-id="66a24-108">This guide explains how to use AzureRM to create a policy assignment.</span></span> <span data-ttu-id="66a24-109">The policy identifies non-compliant resources in your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="66a24-109">The policy identifies non-compliant resources in your Azure environment.</span></span>

<span data-ttu-id="66a24-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="66a24-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="66a24-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="66a24-111">Prerequisites</span></span>

- <span data-ttu-id="66a24-112">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="66a24-112">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span></span> <span data-ttu-id="66a24-113">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span><span class="sxs-lookup"><span data-stu-id="66a24-113">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span></span>
- <span data-ttu-id="66a24-114">Before you start, make sure that the latest version of PowerShell is installed.</span><span class="sxs-lookup"><span data-stu-id="66a24-114">Before you start, make sure that the latest version of PowerShell is installed.</span></span> <span data-ttu-id="66a24-115">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for detailed information.</span><span class="sxs-lookup"><span data-stu-id="66a24-115">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for detailed information.</span></span>
- <span data-ttu-id="66a24-116">Update your AzureRM PowerShell module to the latest version.</span><span class="sxs-lookup"><span data-stu-id="66a24-116">Update your AzureRM PowerShell module to the latest version.</span></span> <span data-ttu-id="66a24-117">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="66a24-117">If you need to install or upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>
- <span data-ttu-id="66a24-118">Register the Policy Insights resource provider using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66a24-118">Register the Policy Insights resource provider using Azure PowerShell.</span></span> <span data-ttu-id="66a24-119">Registering the resource provider makes sure that your subscription works with it.</span><span class="sxs-lookup"><span data-stu-id="66a24-119">Registering the resource provider makes sure that your subscription works with it.</span></span> <span data-ttu-id="66a24-120">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="66a24-120">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span></span> <span data-ttu-id="66a24-121">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="66a24-121">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="66a24-122">Run the following command to register the resource provider:</span><span class="sxs-lookup"><span data-stu-id="66a24-122">Run the following command to register the resource provider:</span></span>

  ```azurepowershell-interactive
  Register-AzureRmResourceProvider -ProviderNamespace 'Microsoft.PolicyInsights'
  ```

  <span data-ttu-id="66a24-123">For more information about registering and viewing resource providers, see [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md)</span><span class="sxs-lookup"><span data-stu-id="66a24-123">For more information about registering and viewing resource providers, see [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md)</span></span>

## <a name="create-a-policy-assignment"></a><span data-ttu-id="66a24-124">Create a policy assignment</span><span class="sxs-lookup"><span data-stu-id="66a24-124">Create a policy assignment</span></span>

<span data-ttu-id="66a24-125">In this quickstart, you create a policy assignment and assign the *Audit Virtual Machines without Managed Disks* definition.</span><span class="sxs-lookup"><span data-stu-id="66a24-125">In this quickstart, you create a policy assignment and assign the *Audit Virtual Machines without Managed Disks* definition.</span></span> <span data-ttu-id="66a24-126">This policy definition identifies resources that don't comply with the conditions set in the policy definition.</span><span class="sxs-lookup"><span data-stu-id="66a24-126">This policy definition identifies resources that don't comply with the conditions set in the policy definition.</span></span>

<span data-ttu-id="66a24-127">Run the following commands to create a new policy assignment:</span><span class="sxs-lookup"><span data-stu-id="66a24-127">Run the following commands to create a new policy assignment:</span></span>

```azurepowershell-interactive
$rg = Get-AzureRmResourceGroup -Name '<resourceGroupName>'
$definition = Get-AzureRmPolicyDefinition | Where-Object { $_.Properties.DisplayName -eq 'Audit VMs that do not use managed disks' }
New-AzureRmPolicyAssignment -Name 'audit-vm-manageddisks' -DisplayName 'Audit Virtual Machines without Managed Disks Assignment' -Scope $rg.ResourceId -PolicyDefinition $definition
```

<span data-ttu-id="66a24-128">The preceding commands use the following information:</span><span class="sxs-lookup"><span data-stu-id="66a24-128">The preceding commands use the following information:</span></span>

- <span data-ttu-id="66a24-129">**Name** - The actual name of the assignment.</span><span class="sxs-lookup"><span data-stu-id="66a24-129">**Name** - The actual name of the assignment.</span></span>  <span data-ttu-id="66a24-130">For this example, *audit-vm-manageddisks* was used.</span><span class="sxs-lookup"><span data-stu-id="66a24-130">For this example, *audit-vm-manageddisks* was used.</span></span>
- <span data-ttu-id="66a24-131">**DisplayName** - Display name for the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="66a24-131">**DisplayName** - Display name for the policy assignment.</span></span> <span data-ttu-id="66a24-132">In this case, you're using *Audit Virtual Machines without Managed Disks Assignment*.</span><span class="sxs-lookup"><span data-stu-id="66a24-132">In this case, you're using *Audit Virtual Machines without Managed Disks Assignment*.</span></span>
- <span data-ttu-id="66a24-133">**Definition** – The policy definition, based on which you're using to create the assignment.</span><span class="sxs-lookup"><span data-stu-id="66a24-133">**Definition** – The policy definition, based on which you're using to create the assignment.</span></span> <span data-ttu-id="66a24-134">In this case, it is the ID of policy definition *Audit VMs that do not use managed disks*.</span><span class="sxs-lookup"><span data-stu-id="66a24-134">In this case, it is the ID of policy definition *Audit VMs that do not use managed disks*.</span></span>
- <span data-ttu-id="66a24-135">**Scope** - A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span><span class="sxs-lookup"><span data-stu-id="66a24-135">**Scope** - A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span></span> <span data-ttu-id="66a24-136">It could range from a subscription to resource groups.</span><span class="sxs-lookup"><span data-stu-id="66a24-136">It could range from a subscription to resource groups.</span></span> <span data-ttu-id="66a24-137">Be sure to replace &lt;scope&gt; with the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="66a24-137">Be sure to replace &lt;scope&gt; with the name of your resource group.</span></span>

<span data-ttu-id="66a24-138">You’re now ready to identify non-compliant resources to understand the compliance state of your environment.</span><span class="sxs-lookup"><span data-stu-id="66a24-138">You’re now ready to identify non-compliant resources to understand the compliance state of your environment.</span></span>

## <a name="identify-non-compliant-resources"></a><span data-ttu-id="66a24-139">Identify non-compliant resources</span><span class="sxs-lookup"><span data-stu-id="66a24-139">Identify non-compliant resources</span></span>

<span data-ttu-id="66a24-140">Use the following information to identify resources that aren't compliant with the policy assignment you created.</span><span class="sxs-lookup"><span data-stu-id="66a24-140">Use the following information to identify resources that aren't compliant with the policy assignment you created.</span></span> <span data-ttu-id="66a24-141">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="66a24-141">Run the following commands:</span></span>

```azurepowershell-interactive
$policyAssignment = Get-AzureRmPolicyAssignment | Where-Object { $_.Properties.DisplayName -eq 'Audit Virtual Machines without Managed Disks Assignment' }
$policyAssignment.PolicyAssignmentId
```

<span data-ttu-id="66a24-142">For more information about policy assignment IDs, see [Get-AzureRmPolicyAssignment](/powershell/module/azurerm.resources/get-azurermpolicyassignment).</span><span class="sxs-lookup"><span data-stu-id="66a24-142">For more information about policy assignment IDs, see [Get-AzureRmPolicyAssignment](/powershell/module/azurerm.resources/get-azurermpolicyassignment).</span></span>

<span data-ttu-id="66a24-143">Next, run the following command to get the resource IDs of the non-compliant resources that are output into a JSON file:</span><span class="sxs-lookup"><span data-stu-id="66a24-143">Next, run the following command to get the resource IDs of the non-compliant resources that are output into a JSON file:</span></span>

```
armclient post "/subscriptions/<subscriptionID>/resourceGroups/<rgName>/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2017-12-12-preview&$filter=IsCompliant eq false and PolicyAssignmentId eq '<policyAssignmentID>'&$apply=groupby((ResourceId))" > <json file to direct the output with the resource IDs into>
```

<span data-ttu-id="66a24-144">Your results resemble the following example:</span><span class="sxs-lookup"><span data-stu-id="66a24-144">Your results resemble the following example:</span></span>

```json
{
    "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest",
    "@odata.count": 3,
    "value": [{
            "@odata.id": null,
            "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
            "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachineId>"
        },
        {
            "@odata.id": null,
            "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
            "ResourceId": "/subscriptions/<subscriptionId>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachine2Id>"
        },
        {
            "@odata.id": null,
            "@odata.context": "https://management.azure.com/subscriptions/<subscriptionId>/providers/Microsoft.PolicyInsights/policyStates/$metadata#latest/$entity",
            "ResourceId": "/subscriptions/<subscriptionName>/resourcegroups/<rgname>/providers/microsoft.compute/virtualmachines/<virtualmachine3ID>"
        }

    ]
}
```

<span data-ttu-id="66a24-145">The results are comparable to what you'd typically see listed under **Non-compliant resources** in the Azure portal view.</span><span class="sxs-lookup"><span data-stu-id="66a24-145">The results are comparable to what you'd typically see listed under **Non-compliant resources** in the Azure portal view.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="66a24-146">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="66a24-146">Clean up resources</span></span>

<span data-ttu-id="66a24-147">Subsequent guides in this collection build on this quickstart.</span><span class="sxs-lookup"><span data-stu-id="66a24-147">Subsequent guides in this collection build on this quickstart.</span></span> <span data-ttu-id="66a24-148">If you plan to continue to work with other tutorials, do not clean up the resources created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="66a24-148">If you plan to continue to work with other tutorials, do not clean up the resources created in this quickstart.</span></span> <span data-ttu-id="66a24-149">If you don't plan to continue, you can delete the assignment you created by running this command:</span><span class="sxs-lookup"><span data-stu-id="66a24-149">If you don't plan to continue, you can delete the assignment you created by running this command:</span></span>

```azurepowershell-interactive
Remove-AzureRmPolicyAssignment -Name 'audit-vm-manageddisks' -Scope '/subscriptions/<subscriptionID>/resourceGroups/<resourceGroupName>'
```

## <a name="next-steps"></a><span data-ttu-id="66a24-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="66a24-150">Next steps</span></span>

<span data-ttu-id="66a24-151">In this quickstart, you assigned a policy definition to identify non-compliant resources in your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="66a24-151">In this quickstart, you assigned a policy definition to identify non-compliant resources in your Azure environment.</span></span>

<span data-ttu-id="66a24-152">To learn more about assigning policies and ensure that **future** resources that get created are compliant, continue to the tutorial for:</span><span class="sxs-lookup"><span data-stu-id="66a24-152">To learn more about assigning policies and ensure that **future** resources that get created are compliant, continue to the tutorial for:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="66a24-153">Creating and managing policies</span><span class="sxs-lookup"><span data-stu-id="66a24-153">Creating and managing policies</span></span>](create-manage-policy.md)