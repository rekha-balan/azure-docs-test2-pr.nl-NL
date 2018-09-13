---
title: Reset the password or Remote Desktop configuration on a Windows VM | Microsoft Docs
description: Learn how to reset an account password or Remote Desktop services on a Windows VM using the Azure portal or Azure PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 45c69812-d3e4-48de-a98d-39a0f5675777
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 98bf246a2c36f5525ef57eeac1e92fdef5491a67
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553933"
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a><span data-ttu-id="9a03d-103">How to reset the Remote Desktop service or its login password in a Windows VM</span><span class="sxs-lookup"><span data-stu-id="9a03d-103">How to reset the Remote Desktop service or its login password in a Windows VM</span></span>
<span data-ttu-id="9a03d-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span><span class="sxs-lookup"><span data-stu-id="9a03d-104">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="9a03d-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span><span class="sxs-lookup"><span data-stu-id="9a03d-105">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span> <span data-ttu-id="9a03d-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9a03d-106">If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription.</span></span> <span data-ttu-id="9a03d-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="9a03d-107">You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="9a03d-108">Ways to reset configuration or credentials</span><span class="sxs-lookup"><span data-stu-id="9a03d-108">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="9a03d-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span><span class="sxs-lookup"><span data-stu-id="9a03d-109">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="9a03d-110">Reset using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a03d-110">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="9a03d-111">Reset using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a03d-111">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="9a03d-112">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9a03d-112">Azure portal</span></span>
<span data-ttu-id="9a03d-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span><span class="sxs-lookup"><span data-stu-id="9a03d-113">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:</span></span>

![Browse for your Azure VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-select-vm.png)

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="9a03d-115">**Reset the local administrator account password**</span><span class="sxs-lookup"><span data-stu-id="9a03d-115">**Reset the local administrator account password**</span></span>

<span data-ttu-id="9a03d-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="9a03d-116">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="9a03d-117">The password reset blade is displayed:</span><span class="sxs-lookup"><span data-stu-id="9a03d-117">The password reset blade is displayed:</span></span>

![Password reset page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-rm-pw-reset-windows.png)

<span data-ttu-id="9a03d-119">Enter the username and a new password, then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="9a03d-119">Enter the username and a new password, then click **Update**.</span></span> <span data-ttu-id="9a03d-120">Try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="9a03d-120">Try connecting to your VM again.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="9a03d-121">**Reset the Remote Desktop service configuration**</span><span class="sxs-lookup"><span data-stu-id="9a03d-121">**Reset the Remote Desktop service configuration**</span></span>

<span data-ttu-id="9a03d-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="9a03d-122">Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="9a03d-123">The password reset blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="9a03d-123">The password reset blade is displayed.</span></span> 

![Reset RDP configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-rm-rdp-reset.png)

<span data-ttu-id="9a03d-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span><span class="sxs-lookup"><span data-stu-id="9a03d-125">Select **Reset configuration only** from the drop-down menu, then click **Update**.</span></span> <span data-ttu-id="9a03d-126">Try connecting to your VM again.</span><span class="sxs-lookup"><span data-stu-id="9a03d-126">Try connecting to your VM again.</span></span>


## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="9a03d-127">VMAccess extension and PowerShell</span><span class="sxs-lookup"><span data-stu-id="9a03d-127">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="9a03d-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a03d-128">Make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="9a03d-129">**Reset the local administrator account password**</span><span class="sxs-lookup"><span data-stu-id="9a03d-129">**Reset the local administrator account password**</span></span>
<span data-ttu-id="9a03d-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a03d-130">Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="9a03d-131">Create your account credentials as follows:</span><span class="sxs-lookup"><span data-stu-id="9a03d-131">Create your account credentials as follows:</span></span>

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> <span data-ttu-id="9a03d-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span><span class="sxs-lookup"><span data-stu-id="9a03d-132">If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event.</span></span> <span data-ttu-id="9a03d-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span><span class="sxs-lookup"><span data-stu-id="9a03d-133">If the local administrator account on your VM is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="9a03d-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span><span class="sxs-lookup"><span data-stu-id="9a03d-134">The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="9a03d-135">**Reset the Remote Desktop service configuration**</span><span class="sxs-lookup"><span data-stu-id="9a03d-135">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="9a03d-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span><span class="sxs-lookup"><span data-stu-id="9a03d-136">Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet.</span></span> <span data-ttu-id="9a03d-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span><span class="sxs-lookup"><span data-stu-id="9a03d-137">The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:</span></span>

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> <span data-ttu-id="9a03d-138">At any point, a VM can have only a single VM access agent.</span><span class="sxs-lookup"><span data-stu-id="9a03d-138">At any point, a VM can have only a single VM access agent.</span></span> <span data-ttu-id="9a03d-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span><span class="sxs-lookup"><span data-stu-id="9a03d-139">To set the VM access agent properties successfully, the `-ForceRerun` option can be used.</span></span> <span data-ttu-id="9a03d-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span><span class="sxs-lookup"><span data-stu-id="9a03d-140">When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.</span></span>

<span data-ttu-id="9a03d-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a03d-141">If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>


## <a name="next-steps"></a><span data-ttu-id="9a03d-142">Next steps</span><span class="sxs-lookup"><span data-stu-id="9a03d-142">Next steps</span></span>
<span data-ttu-id="9a03d-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9a03d-143">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="9a03d-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span><span class="sxs-lookup"><span data-stu-id="9a03d-144">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="9a03d-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span><span class="sxs-lookup"><span data-stu-id="9a03d-145">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="9a03d-146">Azure VM extensions and features</span><span class="sxs-lookup"><span data-stu-id="9a03d-146">Azure VM extensions and features</span></span>](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="9a03d-147">Connect to an Azure virtual machine with RDP or SSH</span><span class="sxs-lookup"><span data-stu-id="9a03d-147">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="9a03d-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="9a03d-148">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)




