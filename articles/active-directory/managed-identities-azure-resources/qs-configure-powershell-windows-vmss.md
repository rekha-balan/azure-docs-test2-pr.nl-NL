---
title: How to configure managed identities for Azure resources on a virtual machine scale set using PowerShell
description: Step by step instructions for configuring a system and user-assigned managed identities on a virtual machine scale set using PowerShell.
services: active-directory
documentationcenter: ''
author: daveba
manager: mtillman
editor: ''
ms.service: active-directory
ms.component: msi
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 11/27/2017
ms.author: daveba
ms.openlocfilehash: e426da9e48c24a83c0612d233923227cf057e0f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858116"
---
# <a name="configure-managed-identities-for-azure-resources-on-virtual-machine-scale-sets-using-powershell"></a><span data-ttu-id="f6f16-103">Configure managed identities for Azure resources on virtual machine scale sets using PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6f16-103">Configure managed identities for Azure resources on virtual machine scale sets using PowerShell</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="f6f16-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f6f16-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="f6f16-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="f6f16-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="f6f16-106">In this article, using PowerShell, you learn how to perform the managed identities for Azure resources operations on a virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="f6f16-106">In this article, using PowerShell, you learn how to perform the managed identities for Azure resources operations on a virtual machine scale set:</span></span>
- <span data-ttu-id="f6f16-107">Enable and disable the system-assigned managed identity on a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-107">Enable and disable the system-assigned managed identity on a virtual machine scale set</span></span>
- <span data-ttu-id="f6f16-108">Add and remove a user-assigned managed identity on a virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-108">Add and remove a user-assigned managed identity on a virtual machine scale set</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f6f16-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f6f16-109">Prerequisites</span></span>

- <span data-ttu-id="f6f16-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="f6f16-110">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="f6f16-111">**Be sure to review the [difference between a system-assigned and user managed assigned identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="f6f16-111">**Be sure to review the [difference between a system-assigned and user managed assigned identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="f6f16-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="f6f16-112">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="f6f16-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="f6f16-113">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="f6f16-114">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="f6f16-114">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="f6f16-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system-assigned managed and/or user-assigned managed identity from a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-115">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a virtual machine scale set and enable and remove system-assigned managed and/or user-assigned managed identity from a virtual machine scale set.</span></span>
    - <span data-ttu-id="f6f16-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f6f16-116">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="f6f16-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-117">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a virtual machine scale set.</span></span>
- <span data-ttu-id="f6f16-118">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="f6f16-118">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span></span> 

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="f6f16-119">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f6f16-119">System-assigned managed identity</span></span>

<span data-ttu-id="f6f16-120">In this section, you learn how to enable and remove a system-assigned managed identity using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6f16-120">In this section, you learn how to enable and remove a system-assigned managed identity using Azure PowerShell.</span></span>

### <a name="enable-system-assigned-managed-identity-during-the-creation-of-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-121">Enable system-assigned managed identity during the creation of an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-121">Enable system-assigned managed identity during the creation of an Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-122">To create a VMSS with the system-assigned managed identity enabled:</span><span class="sxs-lookup"><span data-stu-id="f6f16-122">To create a VMSS with the system-assigned managed identity enabled:</span></span>

1. <span data-ttu-id="f6f16-123">Refer to *Example 1* in the [New-AzureRmVmssConfig](/powershell/module/azurerm.compute/new-azurermvmssconfig) cmdlet reference article to create a VMSS with a system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f6f16-123">Refer to *Example 1* in the [New-AzureRmVmssConfig](/powershell/module/azurerm.compute/new-azurermvmssconfig) cmdlet reference article to create a VMSS with a system-assigned managed identity.</span></span>  <span data-ttu-id="f6f16-124">Add the parameter `-IdentityType SystemAssigned` to the `New-AzureRmVmssConfig` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6f16-124">Add the parameter `-IdentityType SystemAssigned` to the `New-AzureRmVmssConfig` cmdlet:</span></span>

    ```powershell
    $VMSS = New-AzureRmVmssConfig -Location $Loc -SkuCapacity 2 -SkuName "Standard_A0" -UpgradePolicyMode "Automatic" -NetworkInterfaceConfiguration $NetCfg -IdentityType SystemAssigned`
    ```

2. <span data-ttu-id="f6f16-125">(Optional) Add the managed identities for Azure resources virtual machine scale set extension using the `-Name` and `-Type` parameter on the [Add-AzureRmVmssExtension](/powershell/module/azurerm.compute/add-azurermvmssextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6f16-125">(Optional) Add the managed identities for Azure resources virtual machine scale set extension using the `-Name` and `-Type` parameter on the [Add-AzureRmVmssExtension](/powershell/module/azurerm.compute/add-azurermvmssextension) cmdlet.</span></span> <span data-ttu-id="f6f16-126">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of virtual machine scale set, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="f6f16-126">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of virtual machine scale set, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="f6f16-127">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span><span class="sxs-lookup"><span data-stu-id="f6f16-127">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span></span>

    > [!NOTE]
    > <span data-ttu-id="f6f16-128">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="f6f16-128">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span>

   ```powershell
   $setting = @{ "port" = 50342 }
   $vmss = Get-AzureRmVmss
   Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Setting $settings 
   ```

## <a name="enable-system-assigned-managed-identity-on-an-existing-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-129">Enable system-assigned managed identity on an existing Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-129">Enable system-assigned managed identity on an existing Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-130">If you need to enable a system-assigned managed identity on an existing Azure virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="f6f16-130">If you need to enable a system-assigned managed identity on an existing Azure virtual machine scale set:</span></span>

1. <span data-ttu-id="f6f16-131">Sign in to Azure using `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="f6f16-131">Sign in to Azure using `Login-AzureRmAccount`.</span></span> <span data-ttu-id="f6f16-132">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-132">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span> <span data-ttu-id="f6f16-133">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span><span class="sxs-lookup"><span data-stu-id="f6f16-133">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

2. <span data-ttu-id="f6f16-134">First retrieve the virtual machine scale set properties using the [`Get-AzureRmVmss`](/powershell/module/azurerm.compute/get-azurermvmss) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6f16-134">First retrieve the virtual machine scale set properties using the [`Get-AzureRmVmss`](/powershell/module/azurerm.compute/get-azurermvmss) cmdlet.</span></span> <span data-ttu-id="f6f16-135">Then to enable a system-assigned managed identity, use the `-IdentityType` switch on the [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6f16-135">Then to enable a system-assigned managed identity, use the `-IdentityType` switch on the [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss) cmdlet:</span></span>

   ```powershell
   Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name -myVmss -IdentityType "SystemAssigned"
   ```

3. <span data-ttu-id="f6f16-136">Add the managed identities for Azure resources VMSS extension using the `-Name` and `-Type` parameter on the [Add-AzureRmVmssExtension](/powershell/module/azurerm.compute/add-azurermvmssextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6f16-136">Add the managed identities for Azure resources VMSS extension using the `-Name` and `-Type` parameter on the [Add-AzureRmVmssExtension](/powershell/module/azurerm.compute/add-azurermvmssextension) cmdlet.</span></span> <span data-ttu-id="f6f16-137">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of virtual machine scale set, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="f6f16-137">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of virtual machine scale set, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="f6f16-138">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span><span class="sxs-lookup"><span data-stu-id="f6f16-138">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span></span>

   ```powershell
   $setting = @{ "port" = 50342 }
   $vmss = Get-AzureRmVmss
   Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Setting $settings 
   ```

### <a name="disable-the-system-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-139">Disable the system-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-139">Disable the system-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-140">If you have a virtual machine scale set that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6f16-140">If you have a virtual machine scale set that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:</span></span>

1. <span data-ttu-id="f6f16-141">Sign in to Azure using `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="f6f16-141">Sign in to Azure using `Login-AzureRmAccount`.</span></span> <span data-ttu-id="f6f16-142">Use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="f6f16-142">Use an account that is associated with the Azure subscription that contains the VM.</span></span> <span data-ttu-id="f6f16-143">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span><span class="sxs-lookup"><span data-stu-id="f6f16-143">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span></span>

2. <span data-ttu-id="f6f16-144">Run the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f6f16-144">Run the following cmdlet:</span></span>

   ```powershell
   Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType "UserAssigned"
   ```

<span data-ttu-id="f6f16-145">If you have a virtual machine scale set that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="f6f16-145">If you have a virtual machine scale set that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following commands:</span></span>

```powershell
Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType None
```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="f6f16-146">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="f6f16-146">User-assigned managed identity</span></span>

<span data-ttu-id="f6f16-147">In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6f16-147">In this section, you learn how to add and remove a user-assigned managed identity from a virtual machine scale set using Azure PowerShell.</span></span>

### <a name="assign-a-user-assigned-managed-identity-during-creation-of-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-148">Assign a user-assigned managed identity during creation of an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-148">Assign a user-assigned managed identity during creation of an Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-149">Creating a new virtual machine scale set with a user-assigned managed identity isn't currently supported via PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f6f16-149">Creating a new virtual machine scale set with a user-assigned managed identity isn't currently supported via PowerShell.</span></span> <span data-ttu-id="f6f16-150">See the next section on how to add a user-assigned managed identity to an existing virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-150">See the next section on how to add a user-assigned managed identity to an existing virtual machine scale set.</span></span> <span data-ttu-id="f6f16-151">Check back for updates.</span><span class="sxs-lookup"><span data-stu-id="f6f16-151">Check back for updates.</span></span>

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-152">Assign a user-assigned managed identity to an existing Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-152">Assign a user-assigned managed identity to an existing Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-153">To assign a user-assigned managed identity to an existing Azure virtual machine scale set:</span><span class="sxs-lookup"><span data-stu-id="f6f16-153">To assign a user-assigned managed identity to an existing Azure virtual machine scale set:</span></span>

1. <span data-ttu-id="f6f16-154">Sign in to Azure using `Connect-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="f6f16-154">Sign in to Azure using `Connect-AzureRmAccount`.</span></span> <span data-ttu-id="f6f16-155">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-155">Use an account that is associated with the Azure subscription that contains the virtual machine scale set.</span></span> <span data-ttu-id="f6f16-156">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span><span class="sxs-lookup"><span data-stu-id="f6f16-156">Also make sure your account belongs to a role that gives you write permissions on the virtual machine scale set, such as “Virtual Machine Contributor”:</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

2. <span data-ttu-id="f6f16-157">First retrieve the virtual machine scale set properties using the `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6f16-157">First retrieve the virtual machine scale set properties using the `Get-AzureRmVM` cmdlet.</span></span> <span data-ttu-id="f6f16-158">Then to assign a user-assigned managed identity to the virtual machine scale set, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f6f16-158">Then to assign a user-assigned managed identity to the virtual machine scale set, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzureRmVmss](/powershell/module/azurerm.compute/update-azurermvmss) cmdlet.</span></span> <span data-ttu-id="f6f16-159">Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, `<USER ASSIGNED ID1>`, `USER ASSIGNED ID2` with your own values.</span><span class="sxs-lookup"><span data-stu-id="f6f16-159">Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, `<USER ASSIGNED ID1>`, `USER ASSIGNED ID2` with your own values.</span></span>

   [!INCLUDE [ua-character-limit](~/includes/managed-identity-ua-character-limits.md)]

   ```powershell
   Update-AzureRmVmss -ResourceGroupName <RESOURCE GROUP> -Name <VMSS NAME> -IdentityType UserAssigned -IdentityID "<USER ASSIGNED ID1>","<USER ASSIGNED ID2>"
   ```

### <a name="remove-a-user-assigned-managed-identity-from-an-azure-virtual-machine-scale-set"></a><span data-ttu-id="f6f16-160">Remove a user-assigned managed identity from an Azure virtual machine scale set</span><span class="sxs-lookup"><span data-stu-id="f6f16-160">Remove a user-assigned managed identity from an Azure virtual machine scale set</span></span>

<span data-ttu-id="f6f16-161">If your virtual machine scale set has multiple user-assigned managed identities, you can remove all but the last one using the following commands.</span><span class="sxs-lookup"><span data-stu-id="f6f16-161">If your virtual machine scale set has multiple user-assigned managed identities, you can remove all but the last one using the following commands.</span></span> <span data-ttu-id="f6f16-162">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="f6f16-162">Be sure to replace the `<RESOURCE GROUP>` and `<VMSS NAME>` parameter values with your own values.</span></span> <span data-ttu-id="f6f16-163">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the virtual machine scale set.</span><span class="sxs-lookup"><span data-stu-id="f6f16-163">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the virtual machine scale set.</span></span> <span data-ttu-id="f6f16-164">This information can be found in the identity section of the virtual machine scale set using `az vmss show`:</span><span class="sxs-lookup"><span data-stu-id="f6f16-164">This information can be found in the identity section of the virtual machine scale set using `az vmss show`:</span></span>

```powershell
Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType UserAssigned -IdentityID "<USER ASSIGNED IDENTITY NAME>"
```
<span data-ttu-id="f6f16-165">If your virtual machine scale set does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span><span class="sxs-lookup"><span data-stu-id="f6f16-165">If your virtual machine scale set does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span></span>

```powershell
Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType None
```
<span data-ttu-id="f6f16-166">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="f6f16-166">If your virtual machine scale set has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identity.</span></span>

```powershell 
Update-AzureRmVmss -ResourceGroupName myResourceGroup -Name myVmss -IdentityType "SystemAssigned"
```

## <a name="next-steps"></a><span data-ttu-id="f6f16-167">Next steps</span><span class="sxs-lookup"><span data-stu-id="f6f16-167">Next steps</span></span>

- [<span data-ttu-id="f6f16-168">Managed identities for Azure resources overview</span><span class="sxs-lookup"><span data-stu-id="f6f16-168">Managed identities for Azure resources overview</span></span>](overview.md)
- <span data-ttu-id="f6f16-169">For the full Azure VM creation Quickstarts, see:</span><span class="sxs-lookup"><span data-stu-id="f6f16-169">For the full Azure VM creation Quickstarts, see:</span></span>
  
  - [<span data-ttu-id="f6f16-170">Create a Windows virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6f16-170">Create a Windows virtual machine with PowerShell</span></span>](../../virtual-machines/windows/quick-create-powershell.md) 
  - [<span data-ttu-id="f6f16-171">Create a Linux virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f6f16-171">Create a Linux virtual machine with PowerShell</span></span>](../../virtual-machines/linux/quick-create-powershell.md) 

















