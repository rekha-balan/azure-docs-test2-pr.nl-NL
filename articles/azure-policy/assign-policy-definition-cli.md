---
title: Use the Azure CLI to create a policy assignment to identify non-compliant resources in your Azure environment
description: Use PowerShell to create an Azure Policy assignment to identify non-compliant resources.
services: azure-policy
author: DCtheGeek
ms.author: dacoulte
ms.date: 05/24/2018
ms.topic: quickstart
ms.service: azure-policy
ms.custom: mvc
ms.openlocfilehash: 813a5a3855132ab4bd5dd0ff3eb3a0c83696b904
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868203"
---
# <a name="create-a-policy-assignment-to-identify-non-compliant-resources-in-your-azure-environment-with-the-azure-cli"></a><span data-ttu-id="df46d-103">Create a policy assignment to identify non-compliant resources in your Azure environment with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="df46d-103">Create a policy assignment to identify non-compliant resources in your Azure environment with the Azure CLI</span></span>

<span data-ttu-id="df46d-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span><span class="sxs-lookup"><span data-stu-id="df46d-104">The first step in understanding compliance in Azure is to identify the status of your resources.</span></span> <span data-ttu-id="df46d-105">This quickstart steps you through the process of creating a policy assignment to identify virtual machines that aren't using managed disks.</span><span class="sxs-lookup"><span data-stu-id="df46d-105">This quickstart steps you through the process of creating a policy assignment to identify virtual machines that aren't using managed disks.</span></span>

<span data-ttu-id="df46d-106">At the end of this process, you'll successfully identify virtual machines that aren't using managed disks.</span><span class="sxs-lookup"><span data-stu-id="df46d-106">At the end of this process, you'll successfully identify virtual machines that aren't using managed disks.</span></span> <span data-ttu-id="df46d-107">They're *non-compliant* with the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="df46d-107">They're *non-compliant* with the policy assignment.</span></span>

<span data-ttu-id="df46d-108">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="df46d-108">Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="df46d-109">This guide uses Azure CLI to create a policy assignment and to identify non-compliant resources in your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="df46d-109">This guide uses Azure CLI to create a policy assignment and to identify non-compliant resources in your Azure environment.</span></span>

<span data-ttu-id="df46d-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="df46d-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="df46d-111">This quickstart requires that you run Azure CLI version 2.0.4 or later to install and use the CLI locally.</span><span class="sxs-lookup"><span data-stu-id="df46d-111">This quickstart requires that you run Azure CLI version 2.0.4 or later to install and use the CLI locally.</span></span> <span data-ttu-id="df46d-112">To find the version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="df46d-112">To find the version, run `az --version`.</span></span> <span data-ttu-id="df46d-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="df46d-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="df46d-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="df46d-114">Prerequisites</span></span>

<span data-ttu-id="df46d-115">Register the Policy Insights resource provider using Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="df46d-115">Register the Policy Insights resource provider using Azure CLI.</span></span> <span data-ttu-id="df46d-116">Registering the resource provider makes sure that your subscription works with it.</span><span class="sxs-lookup"><span data-stu-id="df46d-116">Registering the resource provider makes sure that your subscription works with it.</span></span> <span data-ttu-id="df46d-117">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span><span class="sxs-lookup"><span data-stu-id="df46d-117">To register a resource provider, you must have permission to perform the register action operation for the resource provider.</span></span> <span data-ttu-id="df46d-118">This operation is included in the Contributor and Owner roles.</span><span class="sxs-lookup"><span data-stu-id="df46d-118">This operation is included in the Contributor and Owner roles.</span></span> <span data-ttu-id="df46d-119">Run the following command to register the resource provider:</span><span class="sxs-lookup"><span data-stu-id="df46d-119">Run the following command to register the resource provider:</span></span>

```azurecli-interactive
az provider register --namespace 'Microsoft.PolicyInsights'
```

<span data-ttu-id="df46d-120">For more information about registering and viewing resource providers, see [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md)</span><span class="sxs-lookup"><span data-stu-id="df46d-120">For more information about registering and viewing resource providers, see [Resource Providers and Types](../azure-resource-manager/resource-manager-supported-services.md)</span></span>

<span data-ttu-id="df46d-121">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span><span class="sxs-lookup"><span data-stu-id="df46d-121">If you haven't already, install the [ARMClient](https://github.com/projectkudu/ARMClient).</span></span> <span data-ttu-id="df46d-122">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span><span class="sxs-lookup"><span data-stu-id="df46d-122">It's a tool that sends HTTP requests to Azure Resource Manager-based APIs.</span></span>

## <a name="create-a-policy-assignment"></a><span data-ttu-id="df46d-123">Create a policy assignment</span><span class="sxs-lookup"><span data-stu-id="df46d-123">Create a policy assignment</span></span>

<span data-ttu-id="df46d-124">In this quickstart, you create a policy assignment and assign the **Audit VMs that do not use managed disks** definition.</span><span class="sxs-lookup"><span data-stu-id="df46d-124">In this quickstart, you create a policy assignment and assign the **Audit VMs that do not use managed disks** definition.</span></span> <span data-ttu-id="df46d-125">This policy definition identifies resources that don't comply with the conditions set in the policy definition.</span><span class="sxs-lookup"><span data-stu-id="df46d-125">This policy definition identifies resources that don't comply with the conditions set in the policy definition.</span></span>

<span data-ttu-id="df46d-126">Run the following command to create a policy assignment:</span><span class="sxs-lookup"><span data-stu-id="df46d-126">Run the following command to create a policy assignment:</span></span>

```azurecli-interactive
az policy assignment create --name 'audit-vm-manageddisks' --display-name 'Audit Virtual Machines without Managed Disks Assignment' --scope '<scope>' --policy '<policy definition ID>'
```

<span data-ttu-id="df46d-127">The preceding command uses the following information:</span><span class="sxs-lookup"><span data-stu-id="df46d-127">The preceding command uses the following information:</span></span>

- <span data-ttu-id="df46d-128">**Name** - The actual name of the assignment.</span><span class="sxs-lookup"><span data-stu-id="df46d-128">**Name** - The actual name of the assignment.</span></span>  <span data-ttu-id="df46d-129">For this example, *audit-vm-manageddisks* was used.</span><span class="sxs-lookup"><span data-stu-id="df46d-129">For this example, *audit-vm-manageddisks* was used.</span></span>
- <span data-ttu-id="df46d-130">**DisplayName** - Display name for the policy assignment.</span><span class="sxs-lookup"><span data-stu-id="df46d-130">**DisplayName** - Display name for the policy assignment.</span></span> <span data-ttu-id="df46d-131">In this case, you're using *Audit Virtual Machines without Managed Disks Assignment*.</span><span class="sxs-lookup"><span data-stu-id="df46d-131">In this case, you're using *Audit Virtual Machines without Managed Disks Assignment*.</span></span>
- <span data-ttu-id="df46d-132">**Policy** – The policy definition ID, based on which you're using to create the assignment.</span><span class="sxs-lookup"><span data-stu-id="df46d-132">**Policy** – The policy definition ID, based on which you're using to create the assignment.</span></span> <span data-ttu-id="df46d-133">In this case, it is the ID of policy definition *Audit VMs that do not use managed disks*.</span><span class="sxs-lookup"><span data-stu-id="df46d-133">In this case, it is the ID of policy definition *Audit VMs that do not use managed disks*.</span></span> <span data-ttu-id="df46d-134">To get the policy definition ID, run this command: `az policy definition list --query "[?displayName=='Audit VMs that do not use managed disks']"`</span><span class="sxs-lookup"><span data-stu-id="df46d-134">To get the policy definition ID, run this command: `az policy definition list --query "[?displayName=='Audit VMs that do not use managed disks']"`</span></span>
- <span data-ttu-id="df46d-135">**Scope** - A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span><span class="sxs-lookup"><span data-stu-id="df46d-135">**Scope** - A scope determines what resources or grouping of resources the policy assignment gets enforced on.</span></span> <span data-ttu-id="df46d-136">It could range from a subscription to resource groups.</span><span class="sxs-lookup"><span data-stu-id="df46d-136">It could range from a subscription to resource groups.</span></span> <span data-ttu-id="df46d-137">Be sure to replace &lt;scope&gt; with the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="df46d-137">Be sure to replace &lt;scope&gt; with the name of your resource group.</span></span>

## <a name="identify-non-compliant-resources"></a><span data-ttu-id="df46d-138">Identify non-compliant resources</span><span class="sxs-lookup"><span data-stu-id="df46d-138">Identify non-compliant resources</span></span>

<span data-ttu-id="df46d-139">To view the resources that aren't compliant under this new assignment, get the policy assignment ID by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="df46d-139">To view the resources that aren't compliant under this new assignment, get the policy assignment ID by running the following commands:</span></span>

```azurepowershell-interactive
$policyAssignment = Get-AzureRmPolicyAssignment | Where-Object { $_.Properties.DisplayName -eq 'Audit Virtual Machines without Managed Disks Assignment' }
$policyAssignment.PolicyAssignmentId
```

<span data-ttu-id="df46d-140">For more information about policy assignment IDs, see [Get-AzureRMPolicyAssignment](/powershell/module/azurerm.resources/get-azurermpolicyassignment).</span><span class="sxs-lookup"><span data-stu-id="df46d-140">For more information about policy assignment IDs, see [Get-AzureRMPolicyAssignment](/powershell/module/azurerm.resources/get-azurermpolicyassignment).</span></span>

<span data-ttu-id="df46d-141">Next, run the following command to get the resource IDs of the non-compliant resources that are output into a JSON file:</span><span class="sxs-lookup"><span data-stu-id="df46d-141">Next, run the following command to get the resource IDs of the non-compliant resources that are output into a JSON file:</span></span>

```
armclient post "/subscriptions/<subscriptionID>/resourceGroups/<rgName>/providers/Microsoft.PolicyInsights/policyStates/latest/queryResults?api-version=2017-12-12-preview&$filter=IsCompliant eq false and PolicyAssignmentId eq '<policyAssignmentID>'&$apply=groupby((ResourceId))" > <json file to direct the output with the resource IDs into>
```

<span data-ttu-id="df46d-142">Your results resemble the following example:</span><span class="sxs-lookup"><span data-stu-id="df46d-142">Your results resemble the following example:</span></span>

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

<span data-ttu-id="df46d-143">The results are comparable to what you'd typically see listed under **Non-compliant resources** in the Azure portal view.</span><span class="sxs-lookup"><span data-stu-id="df46d-143">The results are comparable to what you'd typically see listed under **Non-compliant resources** in the Azure portal view.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="df46d-144">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="df46d-144">Clean up resources</span></span>

<span data-ttu-id="df46d-145">Other guides in this collection build upon this quickstart.</span><span class="sxs-lookup"><span data-stu-id="df46d-145">Other guides in this collection build upon this quickstart.</span></span> <span data-ttu-id="df46d-146">If you plan to continue to work with later tutorials, don't clean up the resources created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="df46d-146">If you plan to continue to work with later tutorials, don't clean up the resources created in this quickstart.</span></span> <span data-ttu-id="df46d-147">If you don't plan to continue, delete the assignment you created by running the following command:</span><span class="sxs-lookup"><span data-stu-id="df46d-147">If you don't plan to continue, delete the assignment you created by running the following command:</span></span>

```azurecli-interactive
az policy assignment delete --name 'audit-vm-manageddisks' --scope '/subscriptions/<subscriptionID>/<resourceGroupName>'
```

## <a name="next-steps"></a><span data-ttu-id="df46d-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="df46d-148">Next steps</span></span>

<span data-ttu-id="df46d-149">In this quickstart, you assigned a policy definition to identify non-compliant resources in your Azure environment.</span><span class="sxs-lookup"><span data-stu-id="df46d-149">In this quickstart, you assigned a policy definition to identify non-compliant resources in your Azure environment.</span></span>

<span data-ttu-id="df46d-150">To learn more about assigning policies and ensure that resources you create in the **future** are compliant, continue to the tutorial for:</span><span class="sxs-lookup"><span data-stu-id="df46d-150">To learn more about assigning policies and ensure that resources you create in the **future** are compliant, continue to the tutorial for:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="df46d-151">Creating and managing policies</span><span class="sxs-lookup"><span data-stu-id="df46d-151">Creating and managing policies</span></span>](create-manage-policy.md)