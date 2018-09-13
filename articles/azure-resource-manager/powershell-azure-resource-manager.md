---
title: Manage Azure solutions with PowerShell | Microsoft Docs
description: Use Azure PowerShell and Resource Manager to manage your resources.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: b33b7303-3330-4af8-8329-c80ac7e9bc7f
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: powershell
ms.devlang: na
ms.topic: conceptual
ms.date: 07/20/2018
ms.author: tomfitz
ms.openlocfilehash: 7cda2a406c6c49e9252bfd5840e8f943e5b7043f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782566"
---
# <a name="manage-resources-with-azure-powershell"></a><span data-ttu-id="0beb9-103">Manage resources with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0beb9-103">Manage resources with Azure PowerShell</span></span>

[!INCLUDE [Resource Manager governance introduction](../../includes/resource-manager-governance-intro.md)]

[!INCLUDE [cloud-shell-powershell.md](../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="0beb9-104">If you choose to install and use the PowerShell locally, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="0beb9-104">If you choose to install and use the PowerShell locally, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="0beb9-105">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="0beb9-105">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="understand-scope"></a><span data-ttu-id="0beb9-106">Understand scope</span><span class="sxs-lookup"><span data-stu-id="0beb9-106">Understand scope</span></span>

[!INCLUDE [Resource Manager governance scope](../../includes/resource-manager-governance-scope.md)]

<span data-ttu-id="0beb9-107">In this article, you apply all management settings to a resource group so you can easily remove those settings when done.</span><span class="sxs-lookup"><span data-stu-id="0beb9-107">In this article, you apply all management settings to a resource group so you can easily remove those settings when done.</span></span>

<span data-ttu-id="0beb9-108">Let's create the resource group.</span><span class="sxs-lookup"><span data-stu-id="0beb9-108">Let's create the resource group.</span></span>

```azurepowershell-interactive
Set-AzureRmContext -Subscription <subscription-name>
New-AzureRmResourceGroup -Name myResourceGroup -Location EastUS
```

<span data-ttu-id="0beb9-109">Currently, the resource group is empty.</span><span class="sxs-lookup"><span data-stu-id="0beb9-109">Currently, the resource group is empty.</span></span>

## <a name="role-based-access-control"></a><span data-ttu-id="0beb9-110">Role-based access control</span><span class="sxs-lookup"><span data-stu-id="0beb9-110">Role-based access control</span></span>

[!INCLUDE [Resource Manager governance policy](../../includes/resource-manager-governance-rbac.md)]

### <a name="assign-a-role"></a><span data-ttu-id="0beb9-111">Assign a role</span><span class="sxs-lookup"><span data-stu-id="0beb9-111">Assign a role</span></span>

<span data-ttu-id="0beb9-112">In this article, you deploy a virtual machine and its related virtual network.</span><span class="sxs-lookup"><span data-stu-id="0beb9-112">In this article, you deploy a virtual machine and its related virtual network.</span></span> <span data-ttu-id="0beb9-113">For managing virtual machine solutions, there are three resource-specific roles that provide commonly needed access:</span><span class="sxs-lookup"><span data-stu-id="0beb9-113">For managing virtual machine solutions, there are three resource-specific roles that provide commonly needed access:</span></span>

* [<span data-ttu-id="0beb9-114">Virtual Machine Contributor</span><span class="sxs-lookup"><span data-stu-id="0beb9-114">Virtual Machine Contributor</span></span>](../role-based-access-control/built-in-roles.md#virtual-machine-contributor)
* [<span data-ttu-id="0beb9-115">Network Contributor</span><span class="sxs-lookup"><span data-stu-id="0beb9-115">Network Contributor</span></span>](../role-based-access-control/built-in-roles.md#network-contributor)
* [<span data-ttu-id="0beb9-116">Storage Account Contributor</span><span class="sxs-lookup"><span data-stu-id="0beb9-116">Storage Account Contributor</span></span>](../role-based-access-control/built-in-roles.md#storage-account-contributor)

<span data-ttu-id="0beb9-117">Instead of assigning roles to individual users, it's often easier to [create an Azure Active Directory group](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md) for users who need to take similar actions.</span><span class="sxs-lookup"><span data-stu-id="0beb9-117">Instead of assigning roles to individual users, it's often easier to [create an Azure Active Directory group](../active-directory/fundamentals/active-directory-groups-create-azure-portal.md) for users who need to take similar actions.</span></span> <span data-ttu-id="0beb9-118">Then, assign that group to the appropriate role.</span><span class="sxs-lookup"><span data-stu-id="0beb9-118">Then, assign that group to the appropriate role.</span></span> <span data-ttu-id="0beb9-119">To simplify this article, you create an Azure Active Directory group without members.</span><span class="sxs-lookup"><span data-stu-id="0beb9-119">To simplify this article, you create an Azure Active Directory group without members.</span></span> <span data-ttu-id="0beb9-120">You can still assign this group to a role for a scope.</span><span class="sxs-lookup"><span data-stu-id="0beb9-120">You can still assign this group to a role for a scope.</span></span> 

<span data-ttu-id="0beb9-121">The following example creates a group and assigns it to the Virtual Machine Contributor role for the resource group.</span><span class="sxs-lookup"><span data-stu-id="0beb9-121">The following example creates a group and assigns it to the Virtual Machine Contributor role for the resource group.</span></span> <span data-ttu-id="0beb9-122">To run the `New-AzureAdGroup` command, you must either use the [Azure Cloud Shell](/azure/cloud-shell/overview) or [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span><span class="sxs-lookup"><span data-stu-id="0beb9-122">To run the `New-AzureAdGroup` command, you must either use the [Azure Cloud Shell](/azure/cloud-shell/overview) or [download the Azure AD PowerShell module](https://www.powershellgallery.com/packages/AzureAD/).</span></span>

```azurepowershell-interactive
$adgroup = New-AzureADGroup -DisplayName VMDemoContributors `
  -MailNickName vmDemoGroup `
  -MailEnabled $false `
  -SecurityEnabled $true
New-AzureRmRoleAssignment -ObjectId $adgroup.ObjectId `
  -ResourceGroupName myResourceGroup `
  -RoleDefinitionName "Virtual Machine Contributor"
```

<span data-ttu-id="0beb9-123">Typically, you repeat the process for **Network Contributor** and **Storage Account Contributor** to make sure users are assigned to manage the deployed resources.</span><span class="sxs-lookup"><span data-stu-id="0beb9-123">Typically, you repeat the process for **Network Contributor** and **Storage Account Contributor** to make sure users are assigned to manage the deployed resources.</span></span> <span data-ttu-id="0beb9-124">In this article, you can skip those steps.</span><span class="sxs-lookup"><span data-stu-id="0beb9-124">In this article, you can skip those steps.</span></span>

## <a name="azure-policy"></a><span data-ttu-id="0beb9-125">Azure Policy</span><span class="sxs-lookup"><span data-stu-id="0beb9-125">Azure Policy</span></span>

<span data-ttu-id="0beb9-126">[Azure Policy](../azure-policy/azure-policy-introduction.md) helps you make sure all resources in subscription meet corporate standards.</span><span class="sxs-lookup"><span data-stu-id="0beb9-126">[Azure Policy](../azure-policy/azure-policy-introduction.md) helps you make sure all resources in subscription meet corporate standards.</span></span> <span data-ttu-id="0beb9-127">Your subscription already has several policy definitions.</span><span class="sxs-lookup"><span data-stu-id="0beb9-127">Your subscription already has several policy definitions.</span></span> <span data-ttu-id="0beb9-128">To see the available policy definitions, use:</span><span class="sxs-lookup"><span data-stu-id="0beb9-128">To see the available policy definitions, use:</span></span>

```azurepowershell-interactive
(Get-AzureRmPolicyDefinition).Properties | Format-Table displayName, policyType
```

<span data-ttu-id="0beb9-129">You see the existing policy definitions.</span><span class="sxs-lookup"><span data-stu-id="0beb9-129">You see the existing policy definitions.</span></span> <span data-ttu-id="0beb9-130">The policy type is either **BuiltIn** or **Custom**.</span><span class="sxs-lookup"><span data-stu-id="0beb9-130">The policy type is either **BuiltIn** or **Custom**.</span></span> <span data-ttu-id="0beb9-131">Look through the definitions for ones that describe a condition you want assign.</span><span class="sxs-lookup"><span data-stu-id="0beb9-131">Look through the definitions for ones that describe a condition you want assign.</span></span> <span data-ttu-id="0beb9-132">In this article, you assign policies that:</span><span class="sxs-lookup"><span data-stu-id="0beb9-132">In this article, you assign policies that:</span></span>

* <span data-ttu-id="0beb9-133">limit the locations for all resources</span><span class="sxs-lookup"><span data-stu-id="0beb9-133">limit the locations for all resources</span></span>
* <span data-ttu-id="0beb9-134">limit the SKUs for virtual machines</span><span class="sxs-lookup"><span data-stu-id="0beb9-134">limit the SKUs for virtual machines</span></span>
* <span data-ttu-id="0beb9-135">audit virtual machines that do not use managed disks</span><span class="sxs-lookup"><span data-stu-id="0beb9-135">audit virtual machines that do not use managed disks</span></span>

```azurepowershell-interactive
$locations ="eastus", "eastus2"
$skus = "Standard_DS1_v2", "Standard_E2s_v2"

$rg = Get-AzureRmResourceGroup -Name myResourceGroup

$locationDefinition = Get-AzureRmPolicyDefinition | where-object {$_.properties.displayname -eq "Allowed locations"}
$skuDefinition = Get-AzureRmPolicyDefinition | where-object {$_.properties.displayname -eq "Allowed virtual machine SKUs"}
$auditDefinition = Get-AzureRmPolicyDefinition | where-object {$_.properties.displayname -eq "Audit VMs that do not use managed disks"}

New-AzureRMPolicyAssignment -Name "Set permitted locations" `
  -Scope $rg.ResourceId `
  -PolicyDefinition $locationDefinition `
  -listOfAllowedLocations $locations
New-AzureRMPolicyAssignment -Name "Set permitted VM SKUs" `
  -Scope $rg.ResourceId `
  -PolicyDefinition $skuDefinition `
  -listOfAllowedSKUs $skus
New-AzureRMPolicyAssignment -Name "Audit unmanaged disks" `
  -Scope $rg.ResourceId `
  -PolicyDefinition $auditDefinition
```

## <a name="deploy-the-virtual-machine"></a><span data-ttu-id="0beb9-136">Deploy the virtual machine</span><span class="sxs-lookup"><span data-stu-id="0beb9-136">Deploy the virtual machine</span></span>

<span data-ttu-id="0beb9-137">You have assigned roles and policies, so you're ready to deploy your solution.</span><span class="sxs-lookup"><span data-stu-id="0beb9-137">You have assigned roles and policies, so you're ready to deploy your solution.</span></span> <span data-ttu-id="0beb9-138">The default size is Standard_DS1_v2, which is one of your allowed SKUs.</span><span class="sxs-lookup"><span data-stu-id="0beb9-138">The default size is Standard_DS1_v2, which is one of your allowed SKUs.</span></span> <span data-ttu-id="0beb9-139">When running this step, you are prompted for credentials.</span><span class="sxs-lookup"><span data-stu-id="0beb9-139">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="0beb9-140">The values that you enter are configured as the user name and password for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="0beb9-140">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```azurepowershell-interactive
New-AzureRmVm -ResourceGroupName "myResourceGroup" `
     -Name "myVM" `
     -Location "East US" `
     -VirtualNetworkName "myVnet" `
     -SubnetName "mySubnet" `
     -SecurityGroupName "myNetworkSecurityGroup" `
     -PublicIpAddressName "myPublicIpAddress" `
     -OpenPorts 80,3389
```

<span data-ttu-id="0beb9-141">After your deployment finishes, you can apply more management settings to the solution.</span><span class="sxs-lookup"><span data-stu-id="0beb9-141">After your deployment finishes, you can apply more management settings to the solution.</span></span>

## <a name="lock-resources"></a><span data-ttu-id="0beb9-142">Lock resources</span><span class="sxs-lookup"><span data-stu-id="0beb9-142">Lock resources</span></span>

[!INCLUDE [Resource Manager governance locks](../../includes/resource-manager-governance-locks.md)]

### <a name="lock-a-resource"></a><span data-ttu-id="0beb9-143">Lock a resource</span><span class="sxs-lookup"><span data-stu-id="0beb9-143">Lock a resource</span></span>

<span data-ttu-id="0beb9-144">To lock the virtual machine and network security group, use:</span><span class="sxs-lookup"><span data-stu-id="0beb9-144">To lock the virtual machine and network security group, use:</span></span>

```azurepowershell-interactive
New-AzureRmResourceLock -LockLevel CanNotDelete `
  -LockName LockVM `
  -ResourceName myVM `
  -ResourceType Microsoft.Compute/virtualMachines `
  -ResourceGroupName myResourceGroup
New-AzureRmResourceLock -LockLevel CanNotDelete `
  -LockName LockNSG `
  -ResourceName myNetworkSecurityGroup `
  -ResourceType Microsoft.Network/networkSecurityGroups `
  -ResourceGroupName myResourceGroup
```

<span data-ttu-id="0beb9-145">The virtual machine can only be deleted if you specifically remove the lock.</span><span class="sxs-lookup"><span data-stu-id="0beb9-145">The virtual machine can only be deleted if you specifically remove the lock.</span></span> <span data-ttu-id="0beb9-146">That step is shown in [Clean up resources](#clean-up-resources).</span><span class="sxs-lookup"><span data-stu-id="0beb9-146">That step is shown in [Clean up resources](#clean-up-resources).</span></span>

## <a name="tag-resources"></a><span data-ttu-id="0beb9-147">Tag resources</span><span class="sxs-lookup"><span data-stu-id="0beb9-147">Tag resources</span></span>

[!INCLUDE [Resource Manager governance tags](../../includes/resource-manager-governance-tags.md)]

### <a name="tag-resources"></a><span data-ttu-id="0beb9-148">Tag resources</span><span class="sxs-lookup"><span data-stu-id="0beb9-148">Tag resources</span></span>

[!INCLUDE [Resource Manager governance tags Powershell](../../includes/resource-manager-governance-tags-powershell.md)]

<span data-ttu-id="0beb9-149">To apply tags to a virtual machine, use:</span><span class="sxs-lookup"><span data-stu-id="0beb9-149">To apply tags to a virtual machine, use:</span></span>

```azurepowershell-interactive
$r = Get-AzureRmResource -ResourceName myVM `
  -ResourceGroupName myResourceGroup `
  -ResourceType Microsoft.Compute/virtualMachines
Set-AzureRmResource -Tag @{ Dept="IT"; Environment="Test"; Project="Documentation" } -ResourceId $r.ResourceId -Force
```

### <a name="find-resources-by-tag"></a><span data-ttu-id="0beb9-150">Find resources by tag</span><span class="sxs-lookup"><span data-stu-id="0beb9-150">Find resources by tag</span></span>

<span data-ttu-id="0beb9-151">To find resources with a tag name and value, use:</span><span class="sxs-lookup"><span data-stu-id="0beb9-151">To find resources with a tag name and value, use:</span></span>

```azurepowershell-interactive
(Find-AzureRmResource -TagName Environment -TagValue Test).Name
```

<span data-ttu-id="0beb9-152">You can use the returned values for management tasks like stopping all virtual machines with a tag value.</span><span class="sxs-lookup"><span data-stu-id="0beb9-152">You can use the returned values for management tasks like stopping all virtual machines with a tag value.</span></span>

```azurepowershell-interactive
Find-AzureRmResource -TagName Environment -TagValue Test | Where-Object {$_.ResourceType -eq "Microsoft.Compute/virtualMachines"} | Stop-AzureRmVM
```

### <a name="view-costs-by-tag-values"></a><span data-ttu-id="0beb9-153">View costs by tag values</span><span class="sxs-lookup"><span data-stu-id="0beb9-153">View costs by tag values</span></span>

<span data-ttu-id="0beb9-154">After applying tags to resources, you can view costs for resources with those tags.</span><span class="sxs-lookup"><span data-stu-id="0beb9-154">After applying tags to resources, you can view costs for resources with those tags.</span></span> <span data-ttu-id="0beb9-155">It takes a while for cost analysis to show the latest usage, so you may not see the costs yet.</span><span class="sxs-lookup"><span data-stu-id="0beb9-155">It takes a while for cost analysis to show the latest usage, so you may not see the costs yet.</span></span> <span data-ttu-id="0beb9-156">When the costs are available, you can view costs for resources across resource groups in your subscription.</span><span class="sxs-lookup"><span data-stu-id="0beb9-156">When the costs are available, you can view costs for resources across resource groups in your subscription.</span></span> <span data-ttu-id="0beb9-157">Users must have [subscription level access to billing information](../billing/billing-manage-access.md) to see the costs.</span><span class="sxs-lookup"><span data-stu-id="0beb9-157">Users must have [subscription level access to billing information](../billing/billing-manage-access.md) to see the costs.</span></span>

<span data-ttu-id="0beb9-158">To view costs by tag in the portal, select your subscription and select **Cost Analysis**.</span><span class="sxs-lookup"><span data-stu-id="0beb9-158">To view costs by tag in the portal, select your subscription and select **Cost Analysis**.</span></span>

![Cost analysis](./media/powershell-azure-resource-manager/select-cost-analysis.png)

<span data-ttu-id="0beb9-160">Then, filter by the tag value, and select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="0beb9-160">Then, filter by the tag value, and select **Apply**.</span></span>

![View cost by tag](./media/powershell-azure-resource-manager/view-costs-by-tag.png)

<span data-ttu-id="0beb9-162">You can also use the [Azure Billing APIs](../billing/billing-usage-rate-card-overview.md) to programmatically view costs.</span><span class="sxs-lookup"><span data-stu-id="0beb9-162">You can also use the [Azure Billing APIs](../billing/billing-usage-rate-card-overview.md) to programmatically view costs.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="0beb9-163">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0beb9-163">Clean up resources</span></span>

<span data-ttu-id="0beb9-164">The locked network security group can't be deleted until the lock is removed.</span><span class="sxs-lookup"><span data-stu-id="0beb9-164">The locked network security group can't be deleted until the lock is removed.</span></span> <span data-ttu-id="0beb9-165">To remove the lock, use:</span><span class="sxs-lookup"><span data-stu-id="0beb9-165">To remove the lock, use:</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceLock -LockName LockVM `
  -ResourceName myVM `
  -ResourceType Microsoft.Compute/virtualMachines `
  -ResourceGroupName myResourceGroup
Remove-AzureRmResourceLock -LockName LockNSG `
  -ResourceName myNetworkSecurityGroup `
  -ResourceType Microsoft.Network/networkSecurityGroups `
  -ResourceGroupName myResourceGroup
```

<span data-ttu-id="0beb9-166">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="0beb9-166">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="0beb9-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="0beb9-167">Next steps</span></span>
* <span data-ttu-id="0beb9-168">To learn about monitoring your virtual machines, see [Monitor and update a Windows Virtual Machine with Azure PowerShell](../virtual-machines/windows/tutorial-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="0beb9-168">To learn about monitoring your virtual machines, see [Monitor and update a Windows Virtual Machine with Azure PowerShell](../virtual-machines/windows/tutorial-monitoring.md).</span></span>
* <span data-ttu-id="0beb9-169">To learn about using Azure Security Center to implement recommended security practices, [Monitor virtual machine security by using Azure Security Center](../virtual-machines/windows/tutorial-azure-security.md).</span><span class="sxs-lookup"><span data-stu-id="0beb9-169">To learn about using Azure Security Center to implement recommended security practices, [Monitor virtual machine security by using Azure Security Center](../virtual-machines/windows/tutorial-azure-security.md).</span></span>
* <span data-ttu-id="0beb9-170">You can move existing resources to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="0beb9-170">You can move existing resources to a new resource group.</span></span> <span data-ttu-id="0beb9-171">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span><span class="sxs-lookup"><span data-stu-id="0beb9-171">For examples, see [Move Resources to New Resource Group or Subscription](resource-group-move-resources.md).</span></span>
* <span data-ttu-id="0beb9-172">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span><span class="sxs-lookup"><span data-stu-id="0beb9-172">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](/azure/architecture/cloud-adoption-guide/subscription-governance).</span></span>
