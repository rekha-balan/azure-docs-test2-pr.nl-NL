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
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm"></a>How to reset the Remote Desktop service or its login password in a Windows VM
If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration. You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password. If you are using PowerShell, make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription. You can also [perform these steps for VMs created with the Classic deployment model](reset-rdp.md).

## <a name="ways-to-reset-configuration-or-credentials"></a>Ways to reset configuration or credentials
You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:

- [Reset using the Azure portal](#azure-portal)
- [Reset using Azure PowerShell](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a>Azure portal
To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines**:

![Browse for your Azure VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-select-vm.png)

### <a name="reset-the-local-administrator-account-password"></a>**Reset the local administrator account password**

Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**. The password reset blade is displayed:

![Password reset page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-rm-pw-reset-windows.png)

Enter the username and a new password, then click **Update**. Try connecting to your VM again.

### <a name="reset-the-remote-desktop-service-configuration"></a>**Reset the Remote Desktop service configuration**

Select your Windows virtual machine then click **Support + Troubleshooting** > **Reset password**. The password reset blade is displayed. 

![Reset RDP configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-rdp/portal-rm-rdp-reset.png)

Select **Reset configuration only** from the drop-down menu, then click **Update**. Try connecting to your VM again.


## <a name="vmaccess-extension-and-powershell"></a>VMAccess extension and PowerShell
Make sure that you have the [latest PowerShell module installed and configured](/powershell/azureps-cmdlets-docs) and are signed in to your Azure subscription with the `Login-AzureRmAccount` cmdlet.

### <a name="reset-the-local-administrator-account-password"></a>**Reset the local administrator account password**
Reset the administrator password or user name with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet. Create your account credentials as follows:

```powershell
$cred=Get-Credential
```

> [!NOTE] 
> If you type a different name than the current local administrator account on your VM, the VMAccess extension renames the local administrator account, assigns your specified password to that account, and issues a Remote Desktop logoff event. If the local administrator account on your VM is disabled, the VMAccess extension enables it.

The following example updates the VM named `myVM` in the resource group named `myResourceGroup` to the credentials specified.

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResourceGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password -typeHandlerVersion "2.0"
```

### <a name="reset-the-remote-desktop-service-configuration"></a>**Reset the Remote Desktop service configuration**
Reset remote access to your VM with the [Set-AzureRmVMAccessExtension](https://msdn.microsoft.com/library/mt619447.aspx) PowerShell cmdlet. The following example resets the access extension named `myVMAccess` on the VM named `myVM` in the `myResourceGroup` resource group:

```powershell
Set-AzureRmVMAccessExtension -ResourceGroupName "myResoureGroup" -VMName "myVM" `
    -Name "myVMAccess" -Location WestUS -typeHandlerVersion "2.0" -ForceRerun
```

> [!TIP]
> At any point, a VM can have only a single VM access agent. To set the VM access agent properties successfully, the `-ForceRerun` option can be used. When using `-ForceRerun`, make sure to use the same name for the VM access agent as used in any previous commands.

If you still can't connect remotely to your virtual machine, see more steps to try at [Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).


## <a name="next-steps"></a>Next steps
If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM. Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.

[Azure VM extensions and features](extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Connect to an Azure virtual machine with RDP or SSH](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)




