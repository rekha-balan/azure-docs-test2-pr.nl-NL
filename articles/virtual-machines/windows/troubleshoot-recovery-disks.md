---
title: Use a Windows troubleshooting VM with Azure PowerShell | Microsoft Docs
description: Learn how to troubleshoot Windows VM issues in Azure by connecting the OS disk to a recovery VM using Azure PowerShell
services: virtual-machines-windows
documentationCenter: ''
authors: iainfoulds
manager: timlt
editor: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 12/13/2016
ms.author: iainfou
ms.openlocfilehash: 657707ecd9e2d4fcdab823bec0f1c7836e51e888
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551851"
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="abea8-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="abea8-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="abea8-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span><span class="sxs-lookup"><span data-stu-id="abea8-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the virtual hard disk itself.</span></span> <span data-ttu-id="abea8-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="abea8-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="abea8-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-106">This article details how to use Azure PowerShell to connect your virtual hard disk to another Windows VM to fix any errors, then re-create your original VM.</span></span>


## <a name="recovery-process-overview"></a><span data-ttu-id="abea8-107">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="abea8-107">Recovery process overview</span></span>
<span data-ttu-id="abea8-108">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="abea8-108">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="abea8-109">Delete the VM encountering issues, keeping the virtual hard disks.</span><span class="sxs-lookup"><span data-stu-id="abea8-109">Delete the VM encountering issues, keeping the virtual hard disks.</span></span>
2. <span data-ttu-id="abea8-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="abea8-110">Attach and mount the virtual hard disk to another Windows VM for troubleshooting purposes.</span></span>
3. <span data-ttu-id="abea8-111">Connect to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-111">Connect to the troubleshooting VM.</span></span> <span data-ttu-id="abea8-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="abea8-112">Edit files or run any tools to fix issues on the original virtual hard disk.</span></span>
4. <span data-ttu-id="abea8-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-113">Unmount and detach the virtual hard disk from the troubleshooting VM.</span></span>
5. <span data-ttu-id="abea8-114">Create a VM using the original virtual hard disk.</span><span class="sxs-lookup"><span data-stu-id="abea8-114">Create a VM using the original virtual hard disk.</span></span>

<span data-ttu-id="abea8-115">Make sure that you have [the latest Azure PowerShell](/powershell/azureps-cmdlets-docs) installed and logged in to your subscription:</span><span class="sxs-lookup"><span data-stu-id="abea8-115">Make sure that you have [the latest Azure PowerShell](/powershell/azureps-cmdlets-docs) installed and logged in to your subscription:</span></span>

```powershell
Login-AzureRMAccount
```

<span data-ttu-id="abea8-116">In the following examples, replace parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="abea8-116">In the following examples, replace parameter names with your own values.</span></span> <span data-ttu-id="abea8-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span><span class="sxs-lookup"><span data-stu-id="abea8-117">Example parameter names include `myResourceGroup`, `mystorageaccount`, and `myVM`.</span></span>


## <a name="determine-boot-issues"></a><span data-ttu-id="abea8-118">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="abea8-118">Determine boot issues</span></span>
<span data-ttu-id="abea8-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span><span class="sxs-lookup"><span data-stu-id="abea8-119">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="abea8-120">This screenshot can help identify why a VM fails to boot.</span><span class="sxs-lookup"><span data-stu-id="abea8-120">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="abea8-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-121">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="abea8-122">Review the screenshot to determine why the VM is failing to boot.</span><span class="sxs-lookup"><span data-stu-id="abea8-122">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="abea8-123">Note any specific error messages or error codes provided.</span><span class="sxs-lookup"><span data-stu-id="abea8-123">Note any specific error messages or error codes provided.</span></span>


## <a name="view-existing-virtual-hard-disk-details"></a><span data-ttu-id="abea8-124">View existing virtual hard disk details</span><span class="sxs-lookup"><span data-stu-id="abea8-124">View existing virtual hard disk details</span></span>
<span data-ttu-id="abea8-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span><span class="sxs-lookup"><span data-stu-id="abea8-125">Before you can attach your virtual hard disk to another VM, you need to identify the name of the virtual hard disk (VHD).</span></span>

<span data-ttu-id="abea8-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-126">The following example gets information for the VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="abea8-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span><span class="sxs-lookup"><span data-stu-id="abea8-127">Look for `Vhd URI` within the `StorageProfile` section from the output of the preceding command.</span></span> <span data-ttu-id="abea8-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span><span class="sxs-lookup"><span data-stu-id="abea8-128">The following truncated example output shows the `Vhd URI` towards the end of the code block:</span></span>

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a><span data-ttu-id="abea8-129">Delete existing VM</span><span class="sxs-lookup"><span data-stu-id="abea8-129">Delete existing VM</span></span>
<span data-ttu-id="abea8-130">Virtual hard disks and VMs are two distinct resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="abea8-130">Virtual hard disks and VMs are two distinct resources in Azure.</span></span> <span data-ttu-id="abea8-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span><span class="sxs-lookup"><span data-stu-id="abea8-131">A virtual hard disk is where the operating system itself, applications, and configurations are stored.</span></span> <span data-ttu-id="abea8-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span><span class="sxs-lookup"><span data-stu-id="abea8-132">The VM itself is just metadata that defines the size or location, and references resources such as a virtual hard disk or virtual network interface card (NIC).</span></span> <span data-ttu-id="abea8-133">Each virtual hard disk has a lease assigned when attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-133">Each virtual hard disk has a lease assigned when attached to a VM.</span></span> <span data-ttu-id="abea8-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span><span class="sxs-lookup"><span data-stu-id="abea8-134">Although data disks can be attached and detached even while the VM is running, the OS disk cannot be detached unless the VM resource is deleted.</span></span> <span data-ttu-id="abea8-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span><span class="sxs-lookup"><span data-stu-id="abea8-135">The lease continues to associate the OS disk with a VM even when that VM is in a stopped and deallocated state.</span></span>

<span data-ttu-id="abea8-136">The first step to recover your VM is to delete the VM resource itself.</span><span class="sxs-lookup"><span data-stu-id="abea8-136">The first step to recover your VM is to delete the VM resource itself.</span></span> <span data-ttu-id="abea8-137">Deleting the VM leaves the virtual hard disks in your storage account.</span><span class="sxs-lookup"><span data-stu-id="abea8-137">Deleting the VM leaves the virtual hard disks in your storage account.</span></span> <span data-ttu-id="abea8-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span><span class="sxs-lookup"><span data-stu-id="abea8-138">After the VM is deleted, you attach the virtual hard disk to another VM to troubleshoot and resolve the errors.</span></span>

<span data-ttu-id="abea8-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-139">The following example deletes the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="abea8-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-140">Wait until the VM has finished deleting before you attach the virtual hard disk to another VM.</span></span> <span data-ttu-id="abea8-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-141">The lease on the virtual hard disk that associates it with the VM needs to be released before you can attach the virtual hard disk to another VM.</span></span>


## <a name="attach-existing-virtual-hard-disk-to-another-vm"></a><span data-ttu-id="abea8-142">Attach existing virtual hard disk to another VM</span><span class="sxs-lookup"><span data-stu-id="abea8-142">Attach existing virtual hard disk to another VM</span></span>
<span data-ttu-id="abea8-143">For the next few steps, you use another VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="abea8-143">For the next few steps, you use another VM for troubleshooting purposes.</span></span> <span data-ttu-id="abea8-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span><span class="sxs-lookup"><span data-stu-id="abea8-144">You attach the existing virtual hard disk to this troubleshooting VM to browse and edit the disk's content.</span></span> <span data-ttu-id="abea8-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span><span class="sxs-lookup"><span data-stu-id="abea8-145">This process allows you to correct any configuration errors or review additional application or system log files, for example.</span></span> <span data-ttu-id="abea8-146">Choose or create another VM to use for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="abea8-146">Choose or create another VM to use for troubleshooting purposes.</span></span>

<span data-ttu-id="abea8-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span><span class="sxs-lookup"><span data-stu-id="abea8-147">When you attach the existing virtual hard disk, specify the URL to the disk obtained in the preceding `Get-AzureRmVM` command.</span></span> <span data-ttu-id="abea8-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-148">The following example attaches an existing virtual hard disk to the troubleshooting VM named `myVMRecovery` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> <span data-ttu-id="abea8-149">Adding a disk requires you to specify the size of the disk.</span><span class="sxs-lookup"><span data-stu-id="abea8-149">Adding a disk requires you to specify the size of the disk.</span></span> <span data-ttu-id="abea8-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span><span class="sxs-lookup"><span data-stu-id="abea8-150">As we attach an existing disk, the `-DiskSizeInGB` is specified as `$null`.</span></span> <span data-ttu-id="abea8-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span><span class="sxs-lookup"><span data-stu-id="abea8-151">This value ensures the data disk is correctly attached, and without the need to determine the true size of data disk.</span></span>


## <a name="mount-the-attached-data-disk"></a><span data-ttu-id="abea8-152">Mount the attached data disk</span><span class="sxs-lookup"><span data-stu-id="abea8-152">Mount the attached data disk</span></span>

1. <span data-ttu-id="abea8-153">RDP to your troubleshooting VM using the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="abea8-153">RDP to your troubleshooting VM using the appropriate credentials.</span></span> <span data-ttu-id="abea8-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="abea8-154">The following example downloads the RDP connection file for the VM named `myVMRecovery` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="abea8-155">The data disk is automatically detected and attached.</span><span class="sxs-lookup"><span data-stu-id="abea8-155">The data disk is automatically detected and attached.</span></span> <span data-ttu-id="abea8-156">View the list of attached volumes to determine the drive letter as follows:</span><span class="sxs-lookup"><span data-stu-id="abea8-156">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="abea8-157">The following example output shows the virtual hard disk connected a disk **2**.</span><span class="sxs-lookup"><span data-stu-id="abea8-157">The following example output shows the virtual hard disk connected a disk **2**.</span></span> <span data-ttu-id="abea8-158">(You can also use `Get-Volume` to view the drive letter):</span><span class="sxs-lookup"><span data-stu-id="abea8-158">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a><span data-ttu-id="abea8-159">Fix issues on original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="abea8-159">Fix issues on original virtual hard disk</span></span>
<span data-ttu-id="abea8-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="abea8-160">With the existing virtual hard disk mounted, you can now perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="abea8-161">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="abea8-161">Once you have addressed the issues, continue with the following steps.</span></span>


## <a name="unmount-and-detach-original-virtual-hard-disk"></a><span data-ttu-id="abea8-162">Unmount and detach original virtual hard disk</span><span class="sxs-lookup"><span data-stu-id="abea8-162">Unmount and detach original virtual hard disk</span></span>
<span data-ttu-id="abea8-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-163">Once your errors are resolved, you unmount and detach the existing virtual hard disk from your troubleshooting VM.</span></span> <span data-ttu-id="abea8-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span><span class="sxs-lookup"><span data-stu-id="abea8-164">You cannot use your virtual hard disk with any other VM until the lease attaching the virtual hard disk to the troubleshooting VM is released.</span></span>

1. <span data-ttu-id="abea8-165">From within your RDP session, unmount the data disk on your recovery VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-165">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="abea8-166">You need the disk number from the previous `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="abea8-166">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="abea8-167">Then, use `Set-Disk` to set the disk as offline:</span><span class="sxs-lookup"><span data-stu-id="abea8-167">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="abea8-168">Confirm the disk is now set as offline using `Get-Disk` again.</span><span class="sxs-lookup"><span data-stu-id="abea8-168">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="abea8-169">The following example output shows the disk is now set as offline:</span><span class="sxs-lookup"><span data-stu-id="abea8-169">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="abea8-170">Exit your RDP session.</span><span class="sxs-lookup"><span data-stu-id="abea8-170">Exit your RDP session.</span></span> <span data-ttu-id="abea8-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-171">From your Azure PowerShell session, remove the virtual hard disk from the troubleshooting VM.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a><span data-ttu-id="abea8-172">Create VM from original hard disk</span><span class="sxs-lookup"><span data-stu-id="abea8-172">Create VM from original hard disk</span></span>
<span data-ttu-id="abea8-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span><span class="sxs-lookup"><span data-stu-id="abea8-173">To create a VM from your original virtual hard disk, use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet).</span></span> <span data-ttu-id="abea8-174">The actual JSON template is at the following link:</span><span class="sxs-lookup"><span data-stu-id="abea8-174">The actual JSON template is at the following link:</span></span>

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

<span data-ttu-id="abea8-175">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span><span class="sxs-lookup"><span data-stu-id="abea8-175">The template deploys a VM into an existing virtual network, using the VHD URL from the earlier command.</span></span> <span data-ttu-id="abea8-176">The following example deploys the template to the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-176">The following example deploys the template to the resource group named `myResourceGroup`:</span></span>

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

<span data-ttu-id="abea8-177">Answer the prompts for the template such as VM name, OS type, and VM size.</span><span class="sxs-lookup"><span data-stu-id="abea8-177">Answer the prompts for the template such as VM name, OS type, and VM size.</span></span> <span data-ttu-id="abea8-178">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="abea8-178">The `osDiskVhdUri` is the same as previously used when attaching the existing virtual hard disk to the troubleshooting VM.</span></span>


## <a name="re-enable-boot-diagnostics"></a><span data-ttu-id="abea8-179">Re-enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="abea8-179">Re-enable boot diagnostics</span></span>

<span data-ttu-id="abea8-180">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span><span class="sxs-lookup"><span data-stu-id="abea8-180">When you create your VM from the existing virtual hard disk, boot diagnostics may not automatically be enabled.</span></span> <span data-ttu-id="abea8-181">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="abea8-181">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="abea8-182">Next steps</span><span class="sxs-lookup"><span data-stu-id="abea8-182">Next steps</span></span>
<span data-ttu-id="abea8-183">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abea8-183">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="abea8-184">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abea8-184">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="abea8-185">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="abea8-185">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>