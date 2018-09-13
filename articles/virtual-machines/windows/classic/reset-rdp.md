---
title: Reset the password or Remote Desktop configuration on a Windows VM in Azure | Microsoft Docs
description: Learn how to reset an account password or Remote Desktop services on a Windows VM created using the Classic deployment model using the Azure portal or Azure PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 3979e03054fead53bc99ccf319ea42b621257566
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563352"
---
# <a name="how-to-reset-the-remote-desktop-service-or-its-login-password-in-a-windows-vm-created-using-the-classic-deployment-model"></a><span data-ttu-id="f5448-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span><span class="sxs-lookup"><span data-stu-id="f5448-103">How to reset the Remote Desktop service or its login password in a Windows VM created using the Classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="f5448-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="f5448-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="f5448-105">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="f5448-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="f5448-106">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="f5448-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="f5448-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span><span class="sxs-lookup"><span data-stu-id="f5448-107">You can also [perform these steps for VMs created with the Resource Manager deployment model](../reset-rdp.md).</span></span>

<span data-ttu-id="f5448-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span><span class="sxs-lookup"><span data-stu-id="f5448-108">If you can't connect to a Windows virtual machine (VM), you can reset the local administrator password or reset the Remote Desktop service configuration.</span></span> <span data-ttu-id="f5448-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span><span class="sxs-lookup"><span data-stu-id="f5448-109">You can use either the Azure portal or the VM Access extension in Azure PowerShell to reset the password.</span></span>

## <a name="ways-to-reset-configuration-or-credentials"></a><span data-ttu-id="f5448-110">Ways to reset configuration or credentials</span><span class="sxs-lookup"><span data-stu-id="f5448-110">Ways to reset configuration or credentials</span></span>
<span data-ttu-id="f5448-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span><span class="sxs-lookup"><span data-stu-id="f5448-111">You can reset Remote Desktop services and credentials in a few different ways, depending on your needs:</span></span>

- [<span data-ttu-id="f5448-112">Reset using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5448-112">Reset using the Azure portal</span></span>](#azure-portal)
- [<span data-ttu-id="f5448-113">Reset using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5448-113">Reset using Azure PowerShell</span></span>](#vmaccess-extension-and-powershell)

## <a name="azure-portal"></a><span data-ttu-id="f5448-114">Azure portal</span><span class="sxs-lookup"><span data-stu-id="f5448-114">Azure portal</span></span>
<span data-ttu-id="f5448-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span><span class="sxs-lookup"><span data-stu-id="f5448-115">You can use the [Azure portal](https://portal.azure.com) to reset the Remote Desktop service.</span></span> <span data-ttu-id="f5448-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span><span class="sxs-lookup"><span data-stu-id="f5448-116">To expand the portal menu, click the three bars in the upper left corner and then click **Virtual machines (classic)**:</span></span>

![Browse for your Azure VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/reset-rdp/portal-select-classic-vm.png)

<span data-ttu-id="f5448-118">Select your Windows virtual machine and then click **Reset Remote...**. The following dialog appears to reset the Remote Desktop configuration:</span><span class="sxs-lookup"><span data-stu-id="f5448-118">Select your Windows virtual machine and then click **Reset Remote...**. The following dialog appears to reset the Remote Desktop configuration:</span></span>

![Reset RDP configuration page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/reset-rdp/portal-rdp-reset-windows.png)

<span data-ttu-id="f5448-120">You can also reset the username and password of the local administrator account.</span><span class="sxs-lookup"><span data-stu-id="f5448-120">You can also reset the username and password of the local administrator account.</span></span> <span data-ttu-id="f5448-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span><span class="sxs-lookup"><span data-stu-id="f5448-121">From your VM, click **Support + Troubleshooting** > **Reset password**.</span></span> <span data-ttu-id="f5448-122">The password reset blade is displayed:</span><span class="sxs-lookup"><span data-stu-id="f5448-122">The password reset blade is displayed:</span></span>

![Password reset page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/reset-rdp/portal-pw-reset-windows.png)

<span data-ttu-id="f5448-124">After you enter the new user name and password, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="f5448-124">After you enter the new user name and password, click **Save**.</span></span>

## <a name="vmaccess-extension-and-powershell"></a><span data-ttu-id="f5448-125">VMAccess extension and PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5448-125">VMAccess extension and PowerShell</span></span>
<span data-ttu-id="f5448-126">Make sure the VM Agent is installed on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5448-126">Make sure the VM Agent is installed on the virtual machine.</span></span> <span data-ttu-id="f5448-127">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span><span class="sxs-lookup"><span data-stu-id="f5448-127">The VMAccess extension doesn't need to be installed before you can use it, as long as the VM Agent is available.</span></span> <span data-ttu-id="f5448-128">Verify that the VM Agent is already installed by using the following command.</span><span class="sxs-lookup"><span data-stu-id="f5448-128">Verify that the VM Agent is already installed by using the following command.</span></span> <span data-ttu-id="f5448-129">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span><span class="sxs-lookup"><span data-stu-id="f5448-129">(Replace "myCloudService" and "myVM" by the names of your cloud service and your VM, respectively.</span></span> <span data-ttu-id="f5448-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span><span class="sxs-lookup"><span data-stu-id="f5448-130">You can learn these names by running `Get-AzureVM` without any parameters.)</span></span>

```powershell
$vm = Get-AzureVM -ServiceName "myCloudService" -Name "myVM"
write-host $vm.VM.ProvisionGuestAgent
```

<span data-ttu-id="f5448-131">If the **write-host** command displays **True**, the VM Agent is installed.</span><span class="sxs-lookup"><span data-stu-id="f5448-131">If the **write-host** command displays **True**, the VM Agent is installed.</span></span> <span data-ttu-id="f5448-132">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span><span class="sxs-lookup"><span data-stu-id="f5448-132">If it displays **False**, see the instructions and a link to the download in the [VM Agent and Extensions - Part 2](http://go.microsoft.com/fwlink/p/?linkid=403947&clcid=0x409) Azure blog post.</span></span>

<span data-ttu-id="f5448-133">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span><span class="sxs-lookup"><span data-stu-id="f5448-133">If you created the virtual machine by using the portal, check whether `$vm.GetInstance().ProvisionGuestAgent` returns **True**.</span></span> <span data-ttu-id="f5448-134">If not, you can set it by using this command:</span><span class="sxs-lookup"><span data-stu-id="f5448-134">If not, you can set it by using this command:</span></span>

```powershell
$vm.GetInstance().ProvisionGuestAgent = $true
```

<span data-ttu-id="f5448-135">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span><span class="sxs-lookup"><span data-stu-id="f5448-135">This command prevents the following error when you're running the **Set-AzureVMExtension** command in the next steps: “Provision Guest Agent must be enabled on the VM object before setting IaaS VM Access Extension.”</span></span>

### <a name="reset-the-local-administrator-account-password"></a><span data-ttu-id="f5448-136">**Reset the local administrator account password**</span><span class="sxs-lookup"><span data-stu-id="f5448-136">**Reset the local administrator account password**</span></span>
<span data-ttu-id="f5448-137">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span><span class="sxs-lookup"><span data-stu-id="f5448-137">Create a sign-in credential with the current local administrator account name and a new password, and then run the `Set-AzureVMAccessExtension` as follows.</span></span>

```powershell
$cred=Get-Credential
Set-AzureVMAccessExtension –vm $vm -UserName $cred.GetNetworkCredential().Username `
    -Password $cred.GetNetworkCredential().Password  | Update-AzureVM
```

<span data-ttu-id="f5448-138">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out. If the local administrator account is disabled, the VMAccess extension enables it.</span><span class="sxs-lookup"><span data-stu-id="f5448-138">If you type a different name than the current account, the VMAccess extension renames the local administrator account, assigns the password to that account, and issues a Remote Desktop sign-out. If the local administrator account is disabled, the VMAccess extension enables it.</span></span>

<span data-ttu-id="f5448-139">These commands also reset the Remote Desktop service configuration.</span><span class="sxs-lookup"><span data-stu-id="f5448-139">These commands also reset the Remote Desktop service configuration.</span></span>

### <a name="reset-the-remote-desktop-service-configuration"></a><span data-ttu-id="f5448-140">**Reset the Remote Desktop service configuration**</span><span class="sxs-lookup"><span data-stu-id="f5448-140">**Reset the Remote Desktop service configuration**</span></span>
<span data-ttu-id="f5448-141">To reset the Remote Desktop service configuration, run the following command:</span><span class="sxs-lookup"><span data-stu-id="f5448-141">To reset the Remote Desktop service configuration, run the following command:</span></span>

```powershell
Set-AzureVMAccessExtension –vm $vm | Update-AzureVM
```

<span data-ttu-id="f5448-142">The VMAccess extension runs two commands on the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="f5448-142">The VMAccess extension runs two commands on the virtual machine:</span></span>

```powershell
netsh advfirewall firewall set rule group="Remote Desktop" new enable=Yes
```

<span data-ttu-id="f5448-143">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span><span class="sxs-lookup"><span data-stu-id="f5448-143">This command enables the built-in Windows Firewall group that allows incoming Remote Desktop traffic, which uses TCP port 3389.</span></span>

```powershell
Set-ItemProperty -Path 'HKLM:\System\CurrentControlSet\Control\Terminal Server' -name "fDenyTSConnections" -Value 0
```

<span data-ttu-id="f5448-144">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span><span class="sxs-lookup"><span data-stu-id="f5448-144">This command sets the fDenyTSConnections registry value to 0, enabling Remote Desktop connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5448-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="f5448-145">Next steps</span></span>
<span data-ttu-id="f5448-146">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f5448-146">If the Azure VM access extension does not respond and you are unable to reset the password, you can [reset the local Windows password offline](../reset-local-password-without-agent.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="f5448-147">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span><span class="sxs-lookup"><span data-stu-id="f5448-147">This method is a more advanced process and requires you to connect the virtual hard disk of the problematic VM to another VM.</span></span> <span data-ttu-id="f5448-148">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span><span class="sxs-lookup"><span data-stu-id="f5448-148">Follow the steps documented in this article first, and only attempt the offline password reset method as a last resort.</span></span>

[<span data-ttu-id="f5448-149">Azure VM extensions and features</span><span class="sxs-lookup"><span data-stu-id="f5448-149">Azure VM extensions and features</span></span>](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="f5448-150">Connect to an Azure virtual machine with RDP or SSH</span><span class="sxs-lookup"><span data-stu-id="f5448-150">Connect to an Azure virtual machine with RDP or SSH</span></span>](http://msdn.microsoft.com/library/azure/dn535788.aspx)

[<span data-ttu-id="f5448-151">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5448-151">Troubleshoot Remote Desktop connections to a Windows-based Azure virtual machine</span></span>](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)




