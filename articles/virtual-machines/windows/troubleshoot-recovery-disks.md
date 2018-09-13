---
title: Use a Windows troubleshooting VM with Azure PowerShell | Microsoft Docs
description: Learn how to troubleshoot Windows VM issues in Azure by connecting the OS disk to a recovery VM using Azure PowerShell
services: virtual-machines-windows
documentationCenter: ''
authors: genlin
manager: jeconnoc
editor: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/09/2018
ms.author: genli
ms.openlocfilehash: dd65572fb9a74d2fafc5e667f3d831e214f16380
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44809249"
---
# <a name="troubleshoot-a-windows-vm-by-attaching-the-os-disk-to-a-recovery-vm-using-azure-powershell"></a><span data-ttu-id="72c21-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="72c21-103">Troubleshoot a Windows VM by attaching the OS disk to a recovery VM using Azure PowerShell</span></span>
<span data-ttu-id="72c21-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the disk itself.</span><span class="sxs-lookup"><span data-stu-id="72c21-104">If your Windows virtual machine (VM) in Azure encounters a boot or disk error, you may need to perform troubleshooting steps on the disk itself.</span></span> <span data-ttu-id="72c21-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span><span class="sxs-lookup"><span data-stu-id="72c21-105">A common example would be a failed application update that prevents the VM from being able to boot successfully.</span></span> <span data-ttu-id="72c21-106">This article details how to use Azure PowerShell to connect the disk to another Windows VM to fix any errors, then repair your original VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-106">This article details how to use Azure PowerShell to connect the disk to another Windows VM to fix any errors, then repair your original VM.</span></span> 

> [!Important]
> <span data-ttu-id="72c21-107">The scripts in this article only apply to the VMs that use [Managed Disk](managed-disks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="72c21-107">The scripts in this article only apply to the VMs that use [Managed Disk](managed-disks-overview.md).</span></span> 


## <a name="recovery-process-overview"></a><span data-ttu-id="72c21-108">Recovery process overview</span><span class="sxs-lookup"><span data-stu-id="72c21-108">Recovery process overview</span></span>
<span data-ttu-id="72c21-109">We can now use Azure PowerShell to change the OS disk for a VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-109">We can now use Azure PowerShell to change the OS disk for a VM.</span></span> <span data-ttu-id="72c21-110">We no longer need to delete and recreate the VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-110">We no longer need to delete and recreate the VM.</span></span>

<span data-ttu-id="72c21-111">The troubleshooting process is as follows:</span><span class="sxs-lookup"><span data-stu-id="72c21-111">The troubleshooting process is as follows:</span></span>

1. <span data-ttu-id="72c21-112">Stop the affected VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-112">Stop the affected VM.</span></span>
2. <span data-ttu-id="72c21-113">Create a snapshot from the OS Disk of the VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-113">Create a snapshot from the OS Disk of the VM.</span></span>
3. <span data-ttu-id="72c21-114">Create a disk from the OS disk snapshot.</span><span class="sxs-lookup"><span data-stu-id="72c21-114">Create a disk from the OS disk snapshot.</span></span>
4. <span data-ttu-id="72c21-115">Attach the disk as a data disk to a recovery VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-115">Attach the disk as a data disk to a recovery VM.</span></span>
5. <span data-ttu-id="72c21-116">Connect to the recovery VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-116">Connect to the recovery VM.</span></span> <span data-ttu-id="72c21-117">Edit files or run any tools to fix issues on the copied OS disk.</span><span class="sxs-lookup"><span data-stu-id="72c21-117">Edit files or run any tools to fix issues on the copied OS disk.</span></span>
6. <span data-ttu-id="72c21-118">Unmount and detach disk from recovery VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-118">Unmount and detach disk from recovery VM.</span></span>
7. <span data-ttu-id="72c21-119">Change the OS disk for the affected VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-119">Change the OS disk for the affected VM.</span></span>

<span data-ttu-id="72c21-120">You can use the VM recovery scripts to automate steps 1, 2, 3, 4, 6, and 7.</span><span class="sxs-lookup"><span data-stu-id="72c21-120">You can use the VM recovery scripts to automate steps 1, 2, 3, 4, 6, and 7.</span></span> <span data-ttu-id="72c21-121">For more documentation and instructions, see [VM Recovery Scripts for Resource Manager VM](https://github.com/Azure/azure-support-scripts/tree/master/VMRecovery/ResourceManager).</span><span class="sxs-lookup"><span data-stu-id="72c21-121">For more documentation and instructions, see [VM Recovery Scripts for Resource Manager VM](https://github.com/Azure/azure-support-scripts/tree/master/VMRecovery/ResourceManager).</span></span>

<span data-ttu-id="72c21-122">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span><span class="sxs-lookup"><span data-stu-id="72c21-122">Make sure that you have [the latest Azure PowerShell](/powershell/azure/overview) installed and logged in to your subscription:</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="72c21-123">In the following examples, replace the parameter names with your own values.</span><span class="sxs-lookup"><span data-stu-id="72c21-123">In the following examples, replace the parameter names with your own values.</span></span> 

## <a name="determine-boot-issues"></a><span data-ttu-id="72c21-124">Determine boot issues</span><span class="sxs-lookup"><span data-stu-id="72c21-124">Determine boot issues</span></span>
<span data-ttu-id="72c21-125">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span><span class="sxs-lookup"><span data-stu-id="72c21-125">You can view a screenshot of your VM in Azure to help troubleshoot boot issues.</span></span> <span data-ttu-id="72c21-126">This screenshot can help identify why a VM fails to boot.</span><span class="sxs-lookup"><span data-stu-id="72c21-126">This screenshot can help identify why a VM fails to boot.</span></span> <span data-ttu-id="72c21-127">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="72c21-127">The following example gets the screenshot from the Windows VM named `myVM` in the resource group named `myResourceGroup`:</span></span>

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

<span data-ttu-id="72c21-128">Review the screenshot to determine why the VM is failing to boot.</span><span class="sxs-lookup"><span data-stu-id="72c21-128">Review the screenshot to determine why the VM is failing to boot.</span></span> <span data-ttu-id="72c21-129">Note any specific error messages or error codes provided.</span><span class="sxs-lookup"><span data-stu-id="72c21-129">Note any specific error messages or error codes provided.</span></span>

## <a name="stop-the-vm"></a><span data-ttu-id="72c21-130">Stop the VM</span><span class="sxs-lookup"><span data-stu-id="72c21-130">Stop the VM</span></span>

<span data-ttu-id="72c21-131">The following example stops the VM named `myVM` from the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="72c21-131">The following example stops the VM named `myVM` from the resource group named `myResourceGroup`:</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

<span data-ttu-id="72c21-132">Wait until the VM has finished deleting before you process to the next step.</span><span class="sxs-lookup"><span data-stu-id="72c21-132">Wait until the VM has finished deleting before you process to the next step.</span></span>


## <a name="create-a-snapshot-from-the-os-disk-of-the-vm"></a><span data-ttu-id="72c21-133">Create a snapshot from the OS Disk of the VM</span><span class="sxs-lookup"><span data-stu-id="72c21-133">Create a snapshot from the OS Disk of the VM</span></span>

<span data-ttu-id="72c21-134">The following example creates a snapshot with name `mySnapshot` from the OS disk of the VM named \`myVM'.</span><span class="sxs-lookup"><span data-stu-id="72c21-134">The following example creates a snapshot with name `mySnapshot` from the OS disk of the VM named \`myVM'.</span></span> 

```powershell
$resourceGroupName = 'myResourceGroup' 
$location = 'eastus' 
$vmName = 'myVM'
$snapshotName = 'mySnapshot'  

#Get the VM
$vm = get-azurermvm `
-ResourceGroupName $resourceGroupName `
-Name $vmName

#Create the snapshot configuration for the OS disk
$snapshot =  New-AzureRmSnapshotConfig `
-SourceUri $vm.StorageProfile.OsDisk.ManagedDisk.Id `
-Location $location `
-CreateOption copy

#Take the snapshot
New-AzureRmSnapshot `
   -Snapshot $snapshot `
   -SnapshotName $snapshotName `
   -ResourceGroupName $resourceGroupName 
```

<span data-ttu-id="72c21-135">A snapshot is a full, read-only copy of a VHD.</span><span class="sxs-lookup"><span data-stu-id="72c21-135">A snapshot is a full, read-only copy of a VHD.</span></span> <span data-ttu-id="72c21-136">It cannot be attached to a VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-136">It cannot be attached to a VM.</span></span> <span data-ttu-id="72c21-137">In the next step, we will create a disk from this snapshot.</span><span class="sxs-lookup"><span data-stu-id="72c21-137">In the next step, we will create a disk from this snapshot.</span></span>

## <a name="create-a-disk-from-the-snapshot"></a><span data-ttu-id="72c21-138">Create a disk from the snapshot</span><span class="sxs-lookup"><span data-stu-id="72c21-138">Create a disk from the snapshot</span></span>

<span data-ttu-id="72c21-139">This script creates a managed disk with name `newOSDisk` from the snapshot named `mysnapshot`.</span><span class="sxs-lookup"><span data-stu-id="72c21-139">This script creates a managed disk with name `newOSDisk` from the snapshot named `mysnapshot`.</span></span>  

```powershell
#Set the context to the subscription Id where Managed Disk will be created
#You can skip this step if the subscription is already selected

$subscriptionId = 'yourSubscriptionId'

Select-AzureRmSubscription -SubscriptionId $SubscriptionId

#Provide the name of your resource group
$resourceGroupName ='myResourceGroup'

#Provide the name of the snapshot that will be used to create Managed Disks
$snapshotName = 'mySnapshot' 

#Provide the name of the Managed Disk
$diskName = 'newOSDisk'

#Provide the size of the disks in GB. It should be greater than the VHD file size.
$diskSize = '128'

#Provide the storage type for Managed Disk. PremiumLRS or StandardLRS.
$storageType = 'StandardLRS'

#Provide the Azure region (e.g. westus) where Managed Disks will be located.
#This location should be same as the snapshot location
#Get all the Azure location using command below:
#Get-AzureRmLocation
$location = 'eastus'

$snapshot = Get-AzureRmSnapshot -ResourceGroupName $resourceGroupName -SnapshotName $snapshotName 
 
$diskConfig = New-AzureRmDiskConfig -AccountType $storageType -Location $location -CreateOption Copy -SourceResourceId $snapshot.Id
 
New-AzureRmDisk -Disk $diskConfig -ResourceGroupName $resourceGroupName -DiskName $diskName
```
<span data-ttu-id="72c21-140">Now you have a copy of the original OS disk.</span><span class="sxs-lookup"><span data-stu-id="72c21-140">Now you have a copy of the original OS disk.</span></span> <span data-ttu-id="72c21-141">You can mount this disk to another Windows VM for troubleshooting purposes.</span><span class="sxs-lookup"><span data-stu-id="72c21-141">You can mount this disk to another Windows VM for troubleshooting purposes.</span></span>

## <a name="attach-the-disk-to-another-windows-vm-for-troubleshooting"></a><span data-ttu-id="72c21-142">Attach the disk to another Windows VM for troubleshooting</span><span class="sxs-lookup"><span data-stu-id="72c21-142">Attach the disk to another Windows VM for troubleshooting</span></span>

<span data-ttu-id="72c21-143">Now we attach the copy of the original OS disk to a VM as a data disk.</span><span class="sxs-lookup"><span data-stu-id="72c21-143">Now we attach the copy of the original OS disk to a VM as a data disk.</span></span> <span data-ttu-id="72c21-144">This process allows you to correct configuration errors or review additional application or system log files in the disk.</span><span class="sxs-lookup"><span data-stu-id="72c21-144">This process allows you to correct configuration errors or review additional application or system log files in the disk.</span></span> <span data-ttu-id="72c21-145">The following example attaches the disk named `newOSDisk` to the VM named `RecoveryVM`.</span><span class="sxs-lookup"><span data-stu-id="72c21-145">The following example attaches the disk named `newOSDisk` to the VM named `RecoveryVM`.</span></span>

> [!NOTE]
> <span data-ttu-id="72c21-146">To attach the disk, the copy of the original OS disk and the recovery VM must be in the same location.</span><span class="sxs-lookup"><span data-stu-id="72c21-146">To attach the disk, the copy of the original OS disk and the recovery VM must be in the same location.</span></span>

```powershell
$rgName = "myResourceGroup"
$vmName = "RecoveryVM"
$location = "eastus" 
$dataDiskName = "newOSDisk"
$disk = Get-AzureRmDisk -ResourceGroupName $rgName -DiskName $dataDiskName 

$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName 

$vm = Add-AzureRmVMDataDisk -CreateOption Attach -Lun 0 -VM $vm -ManagedDiskId $disk.Id

Update-AzureRmVM -VM $vm -ResourceGroupName $rgName
```

## <a name="connect-to-the-recovery-vm-and-fix-issues-on-the-attached-disk"></a><span data-ttu-id="72c21-147">Connect to the recovery VM and fix issues on the attached disk</span><span class="sxs-lookup"><span data-stu-id="72c21-147">Connect to the recovery VM and fix issues on the attached disk</span></span>

1. <span data-ttu-id="72c21-148">RDP to your recovery VM using the appropriate credentials.</span><span class="sxs-lookup"><span data-stu-id="72c21-148">RDP to your recovery VM using the appropriate credentials.</span></span> <span data-ttu-id="72c21-149">The following example downloads the RDP connection file for the VM named `RecoveryVM` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span><span class="sxs-lookup"><span data-stu-id="72c21-149">The following example downloads the RDP connection file for the VM named `RecoveryVM` in the resource group named `myResourceGroup`, and downloads it to `C:\Users\ops\Documents`"</span></span>

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "RecoveryVM" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. <span data-ttu-id="72c21-150">The data disk should be automatically detected and attached.</span><span class="sxs-lookup"><span data-stu-id="72c21-150">The data disk should be automatically detected and attached.</span></span> <span data-ttu-id="72c21-151">View the list of attached volumes to determine the drive letter as follows:</span><span class="sxs-lookup"><span data-stu-id="72c21-151">View the list of attached volumes to determine the drive letter as follows:</span></span>

    ```powershell
    Get-Disk
    ```

    <span data-ttu-id="72c21-152">The following example output shows the disk connected a disk **2**.</span><span class="sxs-lookup"><span data-stu-id="72c21-152">The following example output shows the disk connected a disk **2**.</span></span> <span data-ttu-id="72c21-153">(You can also use `Get-Volume` to view the drive letter):</span><span class="sxs-lookup"><span data-stu-id="72c21-153">(You can also use `Get-Volume` to view the drive letter):</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        newOSDisk                                  Healthy             Online       127 GB MBR
    ```

<span data-ttu-id="72c21-154">After the copy of the original OS disk is mounted, you can perform any maintenance and troubleshooting steps as needed.</span><span class="sxs-lookup"><span data-stu-id="72c21-154">After the copy of the original OS disk is mounted, you can perform any maintenance and troubleshooting steps as needed.</span></span> <span data-ttu-id="72c21-155">Once you have addressed the issues, continue with the following steps.</span><span class="sxs-lookup"><span data-stu-id="72c21-155">Once you have addressed the issues, continue with the following steps.</span></span>

## <a name="unmount-and-detach-original-os-disk"></a><span data-ttu-id="72c21-156">Unmount and detach original OS disk</span><span class="sxs-lookup"><span data-stu-id="72c21-156">Unmount and detach original OS disk</span></span>
<span data-ttu-id="72c21-157">Once your errors are resolved, you unmount and detach the existing disk from your recovery VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-157">Once your errors are resolved, you unmount and detach the existing disk from your recovery VM.</span></span> <span data-ttu-id="72c21-158">You cannot use your disk with any other VM until the lease attaching the disk to the recovery VM is released.</span><span class="sxs-lookup"><span data-stu-id="72c21-158">You cannot use your disk with any other VM until the lease attaching the disk to the recovery VM is released.</span></span>

1. <span data-ttu-id="72c21-159">From within your RDP session, unmount the data disk on your recovery VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-159">From within your RDP session, unmount the data disk on your recovery VM.</span></span> <span data-ttu-id="72c21-160">You need the disk number from the previous `Get-Disk` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="72c21-160">You need the disk number from the previous `Get-Disk` cmdlet.</span></span> <span data-ttu-id="72c21-161">Then, use `Set-Disk` to set the disk as offline:</span><span class="sxs-lookup"><span data-stu-id="72c21-161">Then, use `Set-Disk` to set the disk as offline:</span></span>

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    <span data-ttu-id="72c21-162">Confirm the disk is now set as offline using `Get-Disk` again.</span><span class="sxs-lookup"><span data-stu-id="72c21-162">Confirm the disk is now set as offline using `Get-Disk` again.</span></span> <span data-ttu-id="72c21-163">The following example output shows the disk is now set as offline:</span><span class="sxs-lookup"><span data-stu-id="72c21-163">The following example output shows the disk is now set as offline:</span></span>

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. <span data-ttu-id="72c21-164">Exit your RDP session.</span><span class="sxs-lookup"><span data-stu-id="72c21-164">Exit your RDP session.</span></span> <span data-ttu-id="72c21-165">From your Azure PowerShell session, remove the disk named `newOSDisk` from the VM named 'RecoveryVM'.</span><span class="sxs-lookup"><span data-stu-id="72c21-165">From your Azure PowerShell session, remove the disk named `newOSDisk` from the VM named 'RecoveryVM'.</span></span>

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "RecoveryVM"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "newOSDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```

## <a name="change-the-os-disk-for-the-affected-vm"></a><span data-ttu-id="72c21-166">Change the OS disk for the affected VM</span><span class="sxs-lookup"><span data-stu-id="72c21-166">Change the OS disk for the affected VM</span></span>

<span data-ttu-id="72c21-167">You can use Azure PowerShell to swap the OS disks.</span><span class="sxs-lookup"><span data-stu-id="72c21-167">You can use Azure PowerShell to swap the OS disks.</span></span> <span data-ttu-id="72c21-168">You don't have to delete and recreate the VM.</span><span class="sxs-lookup"><span data-stu-id="72c21-168">You don't have to delete and recreate the VM.</span></span>

<span data-ttu-id="72c21-169">This example stops the VM named `myVM` and assigns the disk named `newOSDisk` as the new OS disk.</span><span class="sxs-lookup"><span data-stu-id="72c21-169">This example stops the VM named `myVM` and assigns the disk named `newOSDisk` as the new OS disk.</span></span> 

```powershell
# Get the VM 
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM 

# Make sure the VM is stopped\deallocated
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name $vm.Name -Force

# Get the new disk that you want to swap in
$disk = Get-AzureRmDisk -ResourceGroupName myResourceGroup -Name newDisk

# Set the VM configuration to point to the new disk  
Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $disk.Id -Name $disk.Name 

# Update the VM with the new OS disk
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm 

# Start the VM
Start-AzureRmVM -Name $vm.Name -ResourceGroupName myResourceGroup
```

## <a name="verify-and-enable-boot-diagnostics"></a><span data-ttu-id="72c21-170">Verify and enable boot diagnostics</span><span class="sxs-lookup"><span data-stu-id="72c21-170">Verify and enable boot diagnostics</span></span>

<span data-ttu-id="72c21-171">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span><span class="sxs-lookup"><span data-stu-id="72c21-171">The following example enables the diagnostic extension on the VM named `myVMDeployed` in the resource group named `myResourceGroup`:</span></span>

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a><span data-ttu-id="72c21-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="72c21-172">Next steps</span></span>
<span data-ttu-id="72c21-173">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72c21-173">If you are having issues connecting to your VM, see [Troubleshoot RDP connections to an Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="72c21-174">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72c21-174">For issues with accessing applications running on your VM, see [Troubleshoot application connectivity issues on a Windows VM](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="72c21-175">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="72c21-175">For more information about using Resource Manager, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
