---
title: How to configure managed identities for Azure resources on an Azure VM using PowerShell
description: Step by step instructions for configuring managed identities for Azure resources on an Azure VM using PowerShell.
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
ms.openlocfilehash: e8d85144b89d81e67d5ac225f0b6467230608ce0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856240"
---
# <a name="configure-managed-identities-for-azure-resources-on-an-azure-vm-using-powershell"></a><span data-ttu-id="c89a3-103">Configure managed identities for Azure resources on an Azure VM using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-103">Configure managed identities for Azure resources on an Azure VM using PowerShell</span></span>

[!INCLUDE [preview-notice](../../../includes/active-directory-msi-preview-notice.md)]

<span data-ttu-id="c89a3-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c89a3-104">Managed identities for Azure resources provides Azure services with an automatically managed identity in Azure Active Directory.</span></span> <span data-ttu-id="c89a3-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span><span class="sxs-lookup"><span data-stu-id="c89a3-105">You can use this identity to authenticate to any service that supports Azure AD authentication, without having credentials in your code.</span></span> 

<span data-ttu-id="c89a3-106">In this article, using PowerShell, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span><span class="sxs-lookup"><span data-stu-id="c89a3-106">In this article, using PowerShell, you learn how to perform the following managed identities for Azure resources operations on an Azure VM:</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c89a3-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c89a3-107">Prerequisites</span></span>

- <span data-ttu-id="c89a3-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span><span class="sxs-lookup"><span data-stu-id="c89a3-108">If you're unfamiliar with managed identities for Azure resources, check out the [overview section](overview.md).</span></span> <span data-ttu-id="c89a3-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span><span class="sxs-lookup"><span data-stu-id="c89a3-109">**Be sure to review the [difference between a system-assigned and user-assigned managed identity](overview.md#how-does-it-work)**.</span></span>
- <span data-ttu-id="c89a3-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span><span class="sxs-lookup"><span data-stu-id="c89a3-110">If you don't already have an Azure account, [sign up for a free account](https://azure.microsoft.com/free/) before continuing.</span></span>
- <span data-ttu-id="c89a3-111">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span><span class="sxs-lookup"><span data-stu-id="c89a3-111">To perform the management operations in this article, your account needs the following Azure role based access control assignments:</span></span>

    > [!NOTE]
    > <span data-ttu-id="c89a3-112">No additional Azure AD directory role assignments required.</span><span class="sxs-lookup"><span data-stu-id="c89a3-112">No additional Azure AD directory role assignments required.</span></span>

    - <span data-ttu-id="c89a3-113">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-113">[Virtual Machine Contributor](/azure/role-based-access-control/built-in-roles#virtual-machine-contributor) to create a VM and enable and remove system and/or user-assigned managed identity from an Azure VM.</span></span>
    - <span data-ttu-id="c89a3-114">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span><span class="sxs-lookup"><span data-stu-id="c89a3-114">[Managed Identity Contributor](/azure/role-based-access-control/built-in-roles#managed-identity-contributor) role to create a user-assigned managed identity.</span></span>
    - <span data-ttu-id="c89a3-115">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-115">[Managed Identity Operator](/azure/role-based-access-control/built-in-roles#managed-identity-operator) role to assign and remove a user-assigned managed identity from and to a VM.</span></span>
- <span data-ttu-id="c89a3-116">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span><span class="sxs-lookup"><span data-stu-id="c89a3-116">Install [the latest version of Azure PowerShell](https://www.powershellgallery.com/packages/AzureRM) if you haven't already.</span></span>

## <a name="system-assigned-managed-identity"></a><span data-ttu-id="c89a3-117">System-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="c89a3-117">System-assigned managed identity</span></span>

<span data-ttu-id="c89a3-118">In this section, you will learn how to enable and disable the system-assigned managed identity using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c89a3-118">In this section, you will learn how to enable and disable the system-assigned managed identity using Azure PowerShell.</span></span>

### <a name="enable-system-assigned-managed-identity-during-creation-of-an-azure-vm"></a><span data-ttu-id="c89a3-119">Enable system-assigned managed identity during creation of an Azure VM</span><span class="sxs-lookup"><span data-stu-id="c89a3-119">Enable system-assigned managed identity during creation of an Azure VM</span></span>

<span data-ttu-id="c89a3-120">To create an Azure VM with system-assigned managed identity enabled:</span><span class="sxs-lookup"><span data-stu-id="c89a3-120">To create an Azure VM with system-assigned managed identity enabled:</span></span>

1. <span data-ttu-id="c89a3-121">Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Log in to Azure", "Create resource group", "Create networking group", "Create the VM").</span><span class="sxs-lookup"><span data-stu-id="c89a3-121">Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Log in to Azure", "Create resource group", "Create networking group", "Create the VM").</span></span>
    
    <span data-ttu-id="c89a3-122">When you get to the "Create the VM" section, make a slight modification to the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvm) cmdlet syntax.</span><span class="sxs-lookup"><span data-stu-id="c89a3-122">When you get to the "Create the VM" section, make a slight modification to the [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvm) cmdlet syntax.</span></span> <span data-ttu-id="c89a3-123">Be sure to add a `-AssignIdentity:$SystemAssigned` parameter to provision the VM with the system-assigned identity enabled, for example:</span><span class="sxs-lookup"><span data-stu-id="c89a3-123">Be sure to add a `-AssignIdentity:$SystemAssigned` parameter to provision the VM with the system-assigned identity enabled, for example:</span></span>
      
    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName myVM -AssignIdentity:$SystemAssigned ...
    ```

   - [<span data-ttu-id="c89a3-124">Create a Windows virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-124">Create a Windows virtual machine using PowerShell</span></span>](../../virtual-machines/windows/quick-create-powershell.md)
   - [<span data-ttu-id="c89a3-125">Create a Linux virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-125">Create a Linux virtual machine using PowerShell</span></span>](../../virtual-machines/linux/quick-create-powershell.md)

2. <span data-ttu-id="c89a3-126">(Optional) Add the managed identities for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-126">(Optional) Add the managed identities for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span></span> <span data-ttu-id="c89a3-127">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="c89a3-127">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="c89a3-128">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span><span class="sxs-lookup"><span data-stu-id="c89a3-128">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition:</span></span>

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```
    > [!NOTE]
    > <span data-ttu-id="c89a3-129">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="c89a3-129">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span> <span data-ttu-id="c89a3-130">The managed identities for Azure resources VM extension is planned for deprecation in January 2019.</span><span class="sxs-lookup"><span data-stu-id="c89a3-130">The managed identities for Azure resources VM extension is planned for deprecation in January 2019.</span></span> 

### <a name="enable-system-assigned-managed-identity-on-an-existing-azure-vm"></a><span data-ttu-id="c89a3-131">Enable system-assigned managed identity on an existing Azure VM</span><span class="sxs-lookup"><span data-stu-id="c89a3-131">Enable system-assigned managed identity on an existing Azure VM</span></span>

<span data-ttu-id="c89a3-132">If you need to enable a system-assigned managed identity on an existing Virtual Machine:</span><span class="sxs-lookup"><span data-stu-id="c89a3-132">If you need to enable a system-assigned managed identity on an existing Virtual Machine:</span></span>

1. <span data-ttu-id="c89a3-133">Sign in to Azure using `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="c89a3-133">Sign in to Azure using `Login-AzureRmAccount`.</span></span> <span data-ttu-id="c89a3-134">Use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-134">Use an account that is associated with the Azure subscription that contains the VM.</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

2. <span data-ttu-id="c89a3-135">First retrieve the VM properties using the `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-135">First retrieve the VM properties using the `Get-AzureRmVM` cmdlet.</span></span> <span data-ttu-id="c89a3-136">Then to enable a system-assigned managed identity, use the `-AssignIdentity` switch on the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c89a3-136">Then to enable a system-assigned managed identity, use the `-AssignIdentity` switch on the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet:</span></span>

   ```powershell
   $vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
   Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm -AssignIdentity:$SystemAssigned
   ```

3. <span data-ttu-id="c89a3-137">(Optional) Add the managed identities for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-137">(Optional) Add the managed identities for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span></span> <span data-ttu-id="c89a3-138">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="c89a3-138">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="c89a3-139">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span><span class="sxs-lookup"><span data-stu-id="c89a3-139">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span></span> <span data-ttu-id="c89a3-140">Be sure to specify the correct `-Location` parameter, matching the location of the existing VM:</span><span class="sxs-lookup"><span data-stu-id="c89a3-140">Be sure to specify the correct `-Location` parameter, matching the location of the existing VM:</span></span>

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```
    > [!NOTE]
    > <span data-ttu-id="c89a3-141">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="c89a3-141">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span>

## <a name="disable-system-assigned-managed-identity-from-an-azure-vm"></a><span data-ttu-id="c89a3-142">Disable system-assigned managed identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="c89a3-142">Disable system-assigned managed identity from an Azure VM</span></span>

<span data-ttu-id="c89a3-143">If you have a Virtual Machine that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:</span><span class="sxs-lookup"><span data-stu-id="c89a3-143">If you have a Virtual Machine that no longer needs the system-assigned managed identity but still needs user-assigned managed identities, use the following cmdlet:</span></span>

1. <span data-ttu-id="c89a3-144">Sign in to Azure using `Login-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="c89a3-144">Sign in to Azure using `Login-AzureRmAccount`.</span></span> <span data-ttu-id="c89a3-145">Use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-145">Use an account that is associated with the Azure subscription that contains the VM.</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

2. <span data-ttu-id="c89a3-146">Retrieve the VM properties using the `Get-AzureRmVM` cmdlet and set the `-IdentityType` parameter to `UserAssigned`:</span><span class="sxs-lookup"><span data-stu-id="c89a3-146">Retrieve the VM properties using the `Get-AzureRmVM` cmdlet and set the `-IdentityType` parameter to `UserAssigned`:</span></span>

   ```powershell   
   $vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM    
   Update-AzureRmVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType "UserAssigned"
   ```

<span data-ttu-id="c89a3-147">If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="c89a3-147">If you have a virtual machine that no longer needs system-assigned managed identity and it has no user-assigned managed identities, use the following commands:</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
Update-AzureRmVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType None
```

<span data-ttu-id="c89a3-148">To remove the managed identities for Azure resources VM extension, user the -Name switch with the [Remove-AzureRmVMExtension](/powershell/module/azurerm.compute/remove-azurermvmextension) cmdlet, specifying the same name you used when you added the extension:</span><span class="sxs-lookup"><span data-stu-id="c89a3-148">To remove the managed identities for Azure resources VM extension, user the -Name switch with the [Remove-AzureRmVMExtension](/powershell/module/azurerm.compute/remove-azurermvmextension) cmdlet, specifying the same name you used when you added the extension:</span></span>

   ```powershell
   Remove-AzureRmVMExtension -ResourceGroupName myResourceGroup -Name "ManagedIdentityExtensionForWindows" -VMName myVM
   ```

## <a name="user-assigned-managed-identity"></a><span data-ttu-id="c89a3-149">User-assigned managed identity</span><span class="sxs-lookup"><span data-stu-id="c89a3-149">User-assigned managed identity</span></span>

<span data-ttu-id="c89a3-150">In this section, you learn how to add and remove a user-assigned managed identity from a VM using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c89a3-150">In this section, you learn how to add and remove a user-assigned managed identity from a VM using Azure PowerShell.</span></span>

### <a name="assign-a-user-assigned-managed-identity-to-a-vm-during-creation"></a><span data-ttu-id="c89a3-151">Assign a user-assigned managed identity to a VM during creation</span><span class="sxs-lookup"><span data-stu-id="c89a3-151">Assign a user-assigned managed identity to a VM during creation</span></span>

<span data-ttu-id="c89a3-152">To assign a user-assigned managed identity to an Azure VM when creating the VM:</span><span class="sxs-lookup"><span data-stu-id="c89a3-152">To assign a user-assigned managed identity to an Azure VM when creating the VM:</span></span>

1. <span data-ttu-id="c89a3-153">Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Log in to Azure", "Create resource group", "Create networking group", "Create the VM").</span><span class="sxs-lookup"><span data-stu-id="c89a3-153">Refer to one of the following Azure VM Quickstarts, completing only the necessary sections ("Log in to Azure", "Create resource group", "Create networking group", "Create the VM").</span></span> 
  
    <span data-ttu-id="c89a3-154">When you get to the "Create the VM" section, make a slight modification to the [`New-AzureRmVMConfig`](/powershell/module/azurerm.compute/new-azurermvm) cmdlet syntax.</span><span class="sxs-lookup"><span data-stu-id="c89a3-154">When you get to the "Create the VM" section, make a slight modification to the [`New-AzureRmVMConfig`](/powershell/module/azurerm.compute/new-azurermvm) cmdlet syntax.</span></span> <span data-ttu-id="c89a3-155">Add the `-IdentityType UserAssigned` and `-IdentityID ` parameters to provision the VM with a user-assigned identity.</span><span class="sxs-lookup"><span data-stu-id="c89a3-155">Add the `-IdentityType UserAssigned` and `-IdentityID ` parameters to provision the VM with a user-assigned identity.</span></span>  <span data-ttu-id="c89a3-156">Replace `<VM NAME>`,`<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values.</span><span class="sxs-lookup"><span data-stu-id="c89a3-156">Replace `<VM NAME>`,`<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values.</span></span>  <span data-ttu-id="c89a3-157">For example:</span><span class="sxs-lookup"><span data-stu-id="c89a3-157">For example:</span></span>
    
    ```powershell 
    $vmConfig = New-AzureRmVMConfig -VMName <VM NAME> -IdentityType UserAssigned -IdentityID "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESROURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>..."
    ```
    
    - [<span data-ttu-id="c89a3-158">Create a Windows virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-158">Create a Windows virtual machine using PowerShell</span></span>](../../virtual-machines/windows/quick-create-powershell.md)
    - [<span data-ttu-id="c89a3-159">Create a Linux virtual machine using PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-159">Create a Linux virtual machine using PowerShell</span></span>](../../virtual-machines/linux/quick-create-powershell.md)

2. <span data-ttu-id="c89a3-160">(Optional) Add the managed identity for Azure resources VM extension using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-160">(Optional) Add the managed identity for Azure resources VM extension using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span></span> <span data-ttu-id="c89a3-161">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="c89a3-161">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="c89a3-162">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span><span class="sxs-lookup"><span data-stu-id="c89a3-162">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span></span> <span data-ttu-id="c89a3-163">Be sure to specify the correct `-Location` parameter, matching the location of the existing VM:</span><span class="sxs-lookup"><span data-stu-id="c89a3-163">Be sure to specify the correct `-Location` parameter, matching the location of the existing VM:</span></span>
      > [!NOTE]
    > <span data-ttu-id="c89a3-164">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span><span class="sxs-lookup"><span data-stu-id="c89a3-164">This step is optional as you can use the Azure Instance Metadata Service (IMDS) identity endpoint, to retrieve tokens as well.</span></span> <span data-ttu-id="c89a3-165">The managed identities for Azure resources VM extension is planned for deprecation in January 2019.</span><span class="sxs-lookup"><span data-stu-id="c89a3-165">The managed identities for Azure resources VM extension is planned for deprecation in January 2019.</span></span>

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```

### <a name="assign-a-user-assigned-managed-identity-to-an-existing-azure-vm"></a><span data-ttu-id="c89a3-166">Assign a user-assigned managed identity to an existing Azure VM</span><span class="sxs-lookup"><span data-stu-id="c89a3-166">Assign a user-assigned managed identity to an existing Azure VM</span></span>

<span data-ttu-id="c89a3-167">To assign a user-assigned managed identity to an existing Azure VM:</span><span class="sxs-lookup"><span data-stu-id="c89a3-167">To assign a user-assigned managed identity to an existing Azure VM:</span></span>

1. <span data-ttu-id="c89a3-168">Sign in to Azure using `Connect-AzureRmAccount`.</span><span class="sxs-lookup"><span data-stu-id="c89a3-168">Sign in to Azure using `Connect-AzureRmAccount`.</span></span> <span data-ttu-id="c89a3-169">Use an account that is associated with the Azure subscription that contains the VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-169">Use an account that is associated with the Azure subscription that contains the VM.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

2. <span data-ttu-id="c89a3-170">Create a user-assigned managed identity using the [New-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/new-azurermuserassignedidentity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-170">Create a user-assigned managed identity using the [New-AzureRmUserAssignedIdentity](/powershell/module/azurerm.managedserviceidentity/new-azurermuserassignedidentity) cmdlet.</span></span>  <span data-ttu-id="c89a3-171">Note the `Id` in the output because you will need this in the next step.</span><span class="sxs-lookup"><span data-stu-id="c89a3-171">Note the `Id` in the output because you will need this in the next step.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="c89a3-172">Creating user-assigned managed identities only supports alphanumeric and hyphen (0-9 or a-z or A-Z or -) characters.</span><span class="sxs-lookup"><span data-stu-id="c89a3-172">Creating user-assigned managed identities only supports alphanumeric and hyphen (0-9 or a-z or A-Z or -) characters.</span></span> <span data-ttu-id="c89a3-173">Additionally, name should be limited to 24 character length for the assignment to VM/VMSS to work properly.</span><span class="sxs-lookup"><span data-stu-id="c89a3-173">Additionally, name should be limited to 24 character length for the assignment to VM/VMSS to work properly.</span></span> <span data-ttu-id="c89a3-174">Check back for updates.</span><span class="sxs-lookup"><span data-stu-id="c89a3-174">Check back for updates.</span></span> <span data-ttu-id="c89a3-175">For more information see [FAQs and known issues](known-issues.md)</span><span class="sxs-lookup"><span data-stu-id="c89a3-175">For more information see [FAQs and known issues](known-issues.md)</span></span>

   ```powershell
   New-AzureRmUserAssignedIdentity -ResourceGroupName <RESOURCEGROUP> -Name <USER ASSIGNED IDENTITY NAME>
   ```
3. <span data-ttu-id="c89a3-176">Retrieve the VM properties using the `Get-AzureRmVM` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-176">Retrieve the VM properties using the `Get-AzureRmVM` cmdlet.</span></span> <span data-ttu-id="c89a3-177">Then to assign a user-assigned managed identity to the Azure VM, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-177">Then to assign a user-assigned managed identity to the Azure VM, use the `-IdentityType` and `-IdentityID` switch on the [Update-AzureRmVM](/powershell/module/azurerm.compute/update-azurermvm) cmdlet.</span></span>  <span data-ttu-id="c89a3-178">The value for the`-IdentityId` parameter is the `Id` you noted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="c89a3-178">The value for the`-IdentityId` parameter is the `Id` you noted in the previous step.</span></span>  <span data-ttu-id="c89a3-179">Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values.</span><span class="sxs-lookup"><span data-stu-id="c89a3-179">Replace `<VM NAME>`, `<SUBSCRIPTION ID>`, `<RESROURCE GROUP>`, and `<USER ASSIGNED IDENTITY NAME>` with your own values.</span></span>

   ```powershell
   $vm = Get-AzureRmVM -ResourceGroupName <RESOURCE GROUP> -Name <VM NAME>
   Update-AzureRmVM -ResourceGroupName <RESOURCE GROUP> -VM $vm -IdentityType UserAssigned -IdentityID "/subscriptions/<SUBSCRIPTION ID>/resourcegroups/<RESROURCE GROUP>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<USER ASSIGNED IDENTITY NAME>"
   ```

4. <span data-ttu-id="c89a3-180">Add the managed identity for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="c89a3-180">Add the managed identity for Azure resources VM extension (planned for deprecation in January 2019) using the `-Type` parameter on the [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) cmdlet.</span></span> <span data-ttu-id="c89a3-181">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span><span class="sxs-lookup"><span data-stu-id="c89a3-181">You can pass either "ManagedIdentityExtensionForWindows" or "ManagedIdentityExtensionForLinux", depending on the type of VM, and name it using the `-Name` parameter.</span></span> <span data-ttu-id="c89a3-182">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span><span class="sxs-lookup"><span data-stu-id="c89a3-182">The `-Settings` parameter specifies the port used by the OAuth token endpoint for token acquisition.</span></span> <span data-ttu-id="c89a3-183">Specify the correct `-Location` parameter, matching the location of the existing VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-183">Specify the correct `-Location` parameter, matching the location of the existing VM.</span></span>

   ```powershell
   $settings = @{ "port" = 50342 }
   Set-AzureRmVMExtension -ResourceGroupName myResourceGroup -Location WestUS -VMName myVM -Name "ManagedIdentityExtensionForWindows" -Type "ManagedIdentityExtensionForWindows" -Publisher "Microsoft.ManagedIdentity" -TypeHandlerVersion "1.0" -Settings $settings 
   ```

### <a name="remove-a-user-assigned-managed-identity-from-an-azure-vm"></a><span data-ttu-id="c89a3-184">Remove a user-assigned managed identity from an Azure VM</span><span class="sxs-lookup"><span data-stu-id="c89a3-184">Remove a user-assigned managed identity from an Azure VM</span></span>

<span data-ttu-id="c89a3-185">If your VM has multiple user-assigned managed identities, you can remove all but the last one using the following commands.</span><span class="sxs-lookup"><span data-stu-id="c89a3-185">If your VM has multiple user-assigned managed identities, you can remove all but the last one using the following commands.</span></span> <span data-ttu-id="c89a3-186">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span><span class="sxs-lookup"><span data-stu-id="c89a3-186">Be sure to replace the `<RESOURCE GROUP>` and `<VM NAME>` parameter values with your own values.</span></span> <span data-ttu-id="c89a3-187">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the VM.</span><span class="sxs-lookup"><span data-stu-id="c89a3-187">The `<USER ASSIGNED IDENTITY NAME>` is the user-assigned managed identity's name property, which should remain on the VM.</span></span> <span data-ttu-id="c89a3-188">This information can be found in the identity section of the VM using `az vm show`:</span><span class="sxs-lookup"><span data-stu-id="c89a3-188">This information can be found in the identity section of the VM using `az vm show`:</span></span>

```powershell
$vm = Get-AzureRmVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzureRmVm -ResourceGroupName myResourceGroup -VirtualMachine $vm -IdentityType UserAssigned -IdentityID <USER ASSIGNED IDENTITY NAME>
```
<span data-ttu-id="c89a3-189">If your VM does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c89a3-189">If your VM does not have a system-assigned managed identity and you want to remove all user-assigned managed identities from it, use the following command:</span></span>

```powershell
$vm = Get-AzureRmVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzureRmVm -ResourceGroupName myResourceGroup -VM $vm -IdentityType None
```
<span data-ttu-id="c89a3-190">If your VM has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identities.</span><span class="sxs-lookup"><span data-stu-id="c89a3-190">If your VM has both system-assigned and user-assigned managed identities, you can remove all the user-assigned managed identities by switching to use only system-assigned managed identities.</span></span>

```powershell 
$vm = Get-AzureRmVm -ResourceGroupName myResourceGroup -Name myVm
Update-AzureRmVm -ResourceGroupName myResourceGroup -VirtualMachine $vm -IdentityType "SystemAssigned"
```

## <a name="next-steps"></a><span data-ttu-id="c89a3-191">Next steps</span><span class="sxs-lookup"><span data-stu-id="c89a3-191">Next steps</span></span>

- [<span data-ttu-id="c89a3-192">Managed identities for Azure resources overview</span><span class="sxs-lookup"><span data-stu-id="c89a3-192">Managed identities for Azure resources overview</span></span>](overview.md)
- <span data-ttu-id="c89a3-193">For the full Azure VM creation Quickstarts, see:</span><span class="sxs-lookup"><span data-stu-id="c89a3-193">For the full Azure VM creation Quickstarts, see:</span></span>
  
  - [<span data-ttu-id="c89a3-194">Create a Windows virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-194">Create a Windows virtual machine with PowerShell</span></span>](../../virtual-machines/windows/quick-create-powershell.md) 
  - [<span data-ttu-id="c89a3-195">Create a Linux virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="c89a3-195">Create a Linux virtual machine with PowerShell</span></span>](../../virtual-machines/linux/quick-create-powershell.md) 
