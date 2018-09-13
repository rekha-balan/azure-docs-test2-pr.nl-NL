---
title: Reset the password or Remote Desktop configuration on a Windows VM | Microsoft Docs
description: Learn how to reset an account password or Remote Desktop services on a Windows VM using the Azure portal or Azure PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/23/2018
ms.author: cynthn
ms.openlocfilehash: e350b9f7af37350b57d71e4a5ee4fb32590d472d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44830531"
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="84a69-103">How to reset the Remote Desktop service or its login password in a Windows VM</span><span class="sxs-lookup"><span data-stu-id="84a69-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="84a69-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration (not supported on Windows Domain Controllers).</span><span class="sxs-lookup"><span data-stu-id="84a69-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration (not supported on Windows Domain Controllers).</span></span> <span data-ttu-id="84a69-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span><span class="sxs-lookup"><span data-stu-id="84a69-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="84a69-106">Once you have logged into the VM, you should reset the password for that user.</span><span class="sxs-lookup"><span data-stu-id="84a69-106">Once you have logged into the VM, you should reset the password for that user.</span></span>  
<span data-ttu-id="84a69-107">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="84a69-107">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="84a69-108">You can also [perform these steps for VMs created with the Classic deployment model](https://docs.microsoft.com/azure/virtual-machines/windows/classic/reset-rdp).</span><span class="sxs-lookup"><span data-stu-id="84a69-108">You can also [perform these steps for VMs created with the Classic deployment model](https://docs.microsoft.com/azure/virtual-machines/windows/classic/reset-rdp).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="84a69-109">Ways to reset configuration or credentials</span><span class="sxs-lookup"><span data-stu-id="84a69-109">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="84a69-110">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span><span class="sxs-lookup"><span data-stu-id="84a69-110">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="84a69-111">Reset using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="84a69-111">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="84a69-112">Reset using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a69-112">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="84a69-113">Azure portal</span><span class="sxs-lookup"><span data-stu-id="84a69-113">Azure portal</span></span>
<span data-ttu-id="84a69-114">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span><span class="sxs-lookup"><span data-stu-id="84a69-114">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Browse for your Azure VM](./media/reset-rdp/Portal-Select-VM.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="84a69-116">**Reset the local administrator account password**</span><span class="sxs-lookup"><span data-stu-id="84a69-116">**Reset the local administrator account password**</span></span>

<span data-ttu-id="84a69-117">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="84a69-117">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="84a69-118">The password reset blade is displayed:</span><span class="sxs-lookup"><span data-stu-id="84a69-118">The password reset blade is displayed:</span></span>

![Password reset page](./media/reset-rdp/Portal-RM-PW-Reset-Windows.png)

<span data-ttu-id="84a69-120">Enter the username and a new password, then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="84a69-120">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="84a69-121">Try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="84a69-121">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="84a69-122">**Reset the Remote Desktop service configuration**</span><span class="sxs-lookup"><span data-stu-id="84a69-122">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="84a69-123">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="84a69-123">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="84a69-124">The password reset blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="84a69-124">The password reset blade is displayed.</span></span> 

![Reset RDP configuration](./media/reset-rdp/Portal-RM-RDP-Reset.png)

<span data-ttu-id="84a69-126">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="84a69-126">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="84a69-127">Try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="84a69-127">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="84a69-128">VMAccess extension and PowerShell</span><span class="sxs-lookup"><span data-stu-id="84a69-128">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="84a69-129">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Connect-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84a69-129">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azure/overview) and are signed in to your Azure subscription with the `Connect-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="84a69-130">**Reset the local administrator account password**</span><span class="sxs-lookup"><span data-stu-id="84a69-130">**Reset the local administrator account password**</span></span>
<span data-ttu-id="84a69-131">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84a69-131">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="84a69-132">The typeHandlerVersion must be 2.0 or greater, as version 1 is deprecated.</span><span class="sxs-lookup"><span data-stu-id="84a69-132">The typeHandlerVersion must be 2.0 or greater, as version 1 is deprecated.</span></span> 

```powershell
$SubID = "<SUBSCRIPTION ID>" 
$RgName = "<RESOURCE GROUP NAME>" 
$VmName = "<VM NAME>" 
$Location = "<LOCATION>" 
 
Connect-AzureRmAccount 
Select-AzureRMSubscription -SubscriptionId $SubID 
Set-AzureRmVMAccessExtension -ResourceGroupName $RgName -Location $Location -VMName $VmName -Credential (get-credential) -typeHandlerVersion "2.0" -Name VMAccessAgent 
```

> [!NOTE] 
> <span data-ttu-id="84a69-133">If you type a different name than the current local administrator account on your VM, the VMAccess extension will add a local administrator account with that name, and assign your specified password to that account.</span><span class="sxs-lookup"><span data-stu-id="84a69-133">If you type a different name than the current local administrator account on your VM, the VMAccess extension will add a local administrator account with that name, and assign your specified password to that account.</span></span> <span data-ttu-id="84a69-134">If the local administrator account on your VM exists, it will reset the password and if the account is disabled, the VMAccess extension enables it.</span><span class="sxs-lookup"><span data-stu-id="84a69-134">If the local administrator account on your VM exists, it will reset the password and if the account is disabled, the VMAccess extension enables it.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="84a69-135">**Reset the Remote Desktop service configuration**</span><span class="sxs-lookup"><span data-stu-id="84a69-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="84a69-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="84a69-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](/powershell/module/azurerm.compute/set-azurermvmaccessextension) PowerShell cmdlet.</span></span> <span data-ttu-id="84a69-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="84a69-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="84a69-138">At any point, a VM can have only a single VM access agent.</span><span class="sxs-lookup"><span data-stu-id="84a69-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="84a69-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span><span class="sxs-lookup"><span data-stu-id="84a69-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="84a69-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span><span class="sxs-lookup"><span data-stu-id="84a69-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="84a69-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84a69-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="84a69-142">If you lose connection to the Windows domain controller, you will need to restore it from a domain controller backup.</span><span class="sxs-lookup"><span data-stu-id="84a69-142">If you lose connection to the Windows domain controller, you will need to restore it from a domain controller backup.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84a69-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="84a69-143">Next steps</span></span>
<span data-ttu-id="84a69-144">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="84a69-144">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="84a69-145">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span><span class="sxs-lookup"><span data-stu-id="84a69-145">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="84a69-146">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span><span class="sxs-lookup"><span data-stu-id="84a69-146">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="84a69-147">Azure VM extensions and features</span><span class="sxs-lookup"><span data-stu-id="84a69-147">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="84a69-148">Connect to an Azure virtual machine with RDP or SSH</span><span class="sxs-lookup"><span data-stu-id="84a69-148">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="84a69-149">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="84a69-149">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

