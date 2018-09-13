---
title: include file
description: include file
services: virtual-machines
author: msraiye
ms.service: virtual-machines
ms.topic: include
ms.date: 6/8/2018
ms.author: raiye
ms.custom: include file
ms.openlocfilehash: 049c5d86bc78a8861faff13d82a47579ac24c516
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871622"
---
# <a name="enable-write-accelerator"></a><span data-ttu-id="29c89-103">Enable Write Accelerator</span><span class="sxs-lookup"><span data-stu-id="29c89-103">Enable Write Accelerator</span></span>

<span data-ttu-id="29c89-104">Write Accelerator is a disk capability for M-Series Virtual Machines (VMs) on Premium Storage with Azure Managed Disks exclusively.</span><span class="sxs-lookup"><span data-stu-id="29c89-104">Write Accelerator is a disk capability for M-Series Virtual Machines (VMs) on Premium Storage with Azure Managed Disks exclusively.</span></span> <span data-ttu-id="29c89-105">As the name states, the purpose of the functionality is to improve the I/O latency of writes against Azure Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="29c89-105">As the name states, the purpose of the functionality is to improve the I/O latency of writes against Azure Premium Storage.</span></span> <span data-ttu-id="29c89-106">Write Accelerator is ideally suited where log file updates are required to persist to disk in a highly performant manner for modern databases.</span><span class="sxs-lookup"><span data-stu-id="29c89-106">Write Accelerator is ideally suited where log file updates are required to persist to disk in a highly performant manner for modern databases.</span></span>

<span data-ttu-id="29c89-107">Write Accelerator is generally available for M-series VMs in the Public Cloud.</span><span class="sxs-lookup"><span data-stu-id="29c89-107">Write Accelerator is generally available for M-series VMs in the Public Cloud.</span></span>

## <a name="planning-for-using-write-accelerator"></a><span data-ttu-id="29c89-108">Planning for using Write Accelerator</span><span class="sxs-lookup"><span data-stu-id="29c89-108">Planning for using Write Accelerator</span></span>

<span data-ttu-id="29c89-109">Write Accelerator should be used for the volumes that contain the transaction log or redo logs of a DBMS.</span><span class="sxs-lookup"><span data-stu-id="29c89-109">Write Accelerator should be used for the volumes that contain the transaction log or redo logs of a DBMS.</span></span> <span data-ttu-id="29c89-110">It is not recommended to use Write Accelerator for the data volumes of a DBMS as the feature has been optimized to be used against log disks.</span><span class="sxs-lookup"><span data-stu-id="29c89-110">It is not recommended to use Write Accelerator for the data volumes of a DBMS as the feature has been optimized to be used against log disks.</span></span>

<span data-ttu-id="29c89-111">Write Accelerator only works in conjunction with [Azure managed disks](https://azure.microsoft.com/services/managed-disks/).</span><span class="sxs-lookup"><span data-stu-id="29c89-111">Write Accelerator only works in conjunction with [Azure managed disks](https://azure.microsoft.com/services/managed-disks/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="29c89-112">Enabling Write Accelerator for the operating system disk of the VM will reboot the VM.</span><span class="sxs-lookup"><span data-stu-id="29c89-112">Enabling Write Accelerator for the operating system disk of the VM will reboot the VM.</span></span>
>
> <span data-ttu-id="29c89-113">To enable Write Accelerator to an existing Azure disk that is NOT part of a volume build out of multiple disks with Windows disk or volume managers, Windows Storage Spaces, Windows Scale-out file server (SOFS), Linux LVM, or MDADM, the workload accessing the Azure disk needs to be shut down.</span><span class="sxs-lookup"><span data-stu-id="29c89-113">To enable Write Accelerator to an existing Azure disk that is NOT part of a volume build out of multiple disks with Windows disk or volume managers, Windows Storage Spaces, Windows Scale-out file server (SOFS), Linux LVM, or MDADM, the workload accessing the Azure disk needs to be shut down.</span></span> <span data-ttu-id="29c89-114">Database applications using the Azure disk MUST be shut down.</span><span class="sxs-lookup"><span data-stu-id="29c89-114">Database applications using the Azure disk MUST be shut down.</span></span>
>
> <span data-ttu-id="29c89-115">If you want to enable or disable Write Accelerator for an existing volume that is built out of multiple Azure Premium Storage disks and striped using Windows disk or volume managers, Windows Storage Spaces, Windows Scale-out file server (SOFS), Linux LVM or MDADM, all disks building the volume must be enabled or disabled for Write Accelerator in separate steps.</span><span class="sxs-lookup"><span data-stu-id="29c89-115">If you want to enable or disable Write Accelerator for an existing volume that is built out of multiple Azure Premium Storage disks and striped using Windows disk or volume managers, Windows Storage Spaces, Windows Scale-out file server (SOFS), Linux LVM or MDADM, all disks building the volume must be enabled or disabled for Write Accelerator in separate steps.</span></span> <span data-ttu-id="29c89-116">**Before enabling or disabling Write Accelerator in such a configuration, shut down the Azure VM**.</span><span class="sxs-lookup"><span data-stu-id="29c89-116">**Before enabling or disabling Write Accelerator in such a configuration, shut down the Azure VM**.</span></span>

<span data-ttu-id="29c89-117">Enabling Write Accelerator for OS disks should not be necessary for SAP-related VM configurations.</span><span class="sxs-lookup"><span data-stu-id="29c89-117">Enabling Write Accelerator for OS disks should not be necessary for SAP-related VM configurations.</span></span>

### <a name="restrictions-when-using-write-accelerator"></a><span data-ttu-id="29c89-118">Restrictions when using Write Accelerator</span><span class="sxs-lookup"><span data-stu-id="29c89-118">Restrictions when using Write Accelerator</span></span>

<span data-ttu-id="29c89-119">When using Write Accelerator for an Azure disk/VHD, these restrictions apply:</span><span class="sxs-lookup"><span data-stu-id="29c89-119">When using Write Accelerator for an Azure disk/VHD, these restrictions apply:</span></span>

- <span data-ttu-id="29c89-120">The Premium disk caching must be set to 'None' or 'Read Only'.</span><span class="sxs-lookup"><span data-stu-id="29c89-120">The Premium disk caching must be set to 'None' or 'Read Only'.</span></span> <span data-ttu-id="29c89-121">All other caching modes are not supported.</span><span class="sxs-lookup"><span data-stu-id="29c89-121">All other caching modes are not supported.</span></span>
- <span data-ttu-id="29c89-122">Snapshots on a Write Accelerator enabled disk is not supported yet.</span><span class="sxs-lookup"><span data-stu-id="29c89-122">Snapshots on a Write Accelerator enabled disk is not supported yet.</span></span> <span data-ttu-id="29c89-123">This restriction blocks Azure Backup Service ability to perform an application consistent snapshot of all disks of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="29c89-123">This restriction blocks Azure Backup Service ability to perform an application consistent snapshot of all disks of the virtual machine.</span></span>
- <span data-ttu-id="29c89-124">Only smaller I/O sizes (<=32 KiB) are taking the accelerated path.</span><span class="sxs-lookup"><span data-stu-id="29c89-124">Only smaller I/O sizes (<=32 KiB) are taking the accelerated path.</span></span> <span data-ttu-id="29c89-125">In workload situations where data is getting bulk loaded or where the transaction log buffers of the different DBMS are filled to a larger degree before getting persisted to the storage, chances are that the I/O written to disk is not taking the accelerated path.</span><span class="sxs-lookup"><span data-stu-id="29c89-125">In workload situations where data is getting bulk loaded or where the transaction log buffers of the different DBMS are filled to a larger degree before getting persisted to the storage, chances are that the I/O written to disk is not taking the accelerated path.</span></span>

<span data-ttu-id="29c89-126">There are limits of Azure Premium Storage VHDs per VM that can be supported by Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-126">There are limits of Azure Premium Storage VHDs per VM that can be supported by Write Accelerator.</span></span> <span data-ttu-id="29c89-127">The current limits are:</span><span class="sxs-lookup"><span data-stu-id="29c89-127">The current limits are:</span></span>

| <span data-ttu-id="29c89-128">VM SKU</span><span class="sxs-lookup"><span data-stu-id="29c89-128">VM SKU</span></span> | <span data-ttu-id="29c89-129">Number of Write Accelerator disks</span><span class="sxs-lookup"><span data-stu-id="29c89-129">Number of Write Accelerator disks</span></span> | <span data-ttu-id="29c89-130">Write Accelerator Disk IOPS per VM</span><span class="sxs-lookup"><span data-stu-id="29c89-130">Write Accelerator Disk IOPS per VM</span></span> |
| --- | --- | --- |
| <span data-ttu-id="29c89-131">M128ms, 128s</span><span class="sxs-lookup"><span data-stu-id="29c89-131">M128ms, 128s</span></span> | <span data-ttu-id="29c89-132">16</span><span class="sxs-lookup"><span data-stu-id="29c89-132">16</span></span> | <span data-ttu-id="29c89-133">8000</span><span class="sxs-lookup"><span data-stu-id="29c89-133">8000</span></span> |
| <span data-ttu-id="29c89-134">M64ms, M64ls, M64s</span><span class="sxs-lookup"><span data-stu-id="29c89-134">M64ms, M64ls, M64s</span></span> | <span data-ttu-id="29c89-135">8</span><span class="sxs-lookup"><span data-stu-id="29c89-135">8</span></span> | <span data-ttu-id="29c89-136">4000</span><span class="sxs-lookup"><span data-stu-id="29c89-136">4000</span></span> |
| <span data-ttu-id="29c89-137">M32ms, M32ls, M32ts, M32s</span><span class="sxs-lookup"><span data-stu-id="29c89-137">M32ms, M32ls, M32ts, M32s</span></span> | <span data-ttu-id="29c89-138">4</span><span class="sxs-lookup"><span data-stu-id="29c89-138">4</span></span> | <span data-ttu-id="29c89-139">2000</span><span class="sxs-lookup"><span data-stu-id="29c89-139">2000</span></span> |
| <span data-ttu-id="29c89-140">M16ms, M16s</span><span class="sxs-lookup"><span data-stu-id="29c89-140">M16ms, M16s</span></span> | <span data-ttu-id="29c89-141">2</span><span class="sxs-lookup"><span data-stu-id="29c89-141">2</span></span> | <span data-ttu-id="29c89-142">1000</span><span class="sxs-lookup"><span data-stu-id="29c89-142">1000</span></span> |
| <span data-ttu-id="29c89-143">M8ms, M8s</span><span class="sxs-lookup"><span data-stu-id="29c89-143">M8ms, M8s</span></span> | <span data-ttu-id="29c89-144">1</span><span class="sxs-lookup"><span data-stu-id="29c89-144">1</span></span> | <span data-ttu-id="29c89-145">500</span><span class="sxs-lookup"><span data-stu-id="29c89-145">500</span></span> |

<span data-ttu-id="29c89-146">The IOPS limits are per VM and *not* per disk.</span><span class="sxs-lookup"><span data-stu-id="29c89-146">The IOPS limits are per VM and *not* per disk.</span></span> <span data-ttu-id="29c89-147">All Write Accelerator disks share the same IOPS limit per VM.</span><span class="sxs-lookup"><span data-stu-id="29c89-147">All Write Accelerator disks share the same IOPS limit per VM.</span></span>

## <a name="enabling-write-accelerator-on-a-specific-disk"></a><span data-ttu-id="29c89-148">Enabling Write Accelerator on a specific disk</span><span class="sxs-lookup"><span data-stu-id="29c89-148">Enabling Write Accelerator on a specific disk</span></span>

<span data-ttu-id="29c89-149">The next few sections will describe how Write Accelerator can be enabled on Azure Premium Storage VHDs.</span><span class="sxs-lookup"><span data-stu-id="29c89-149">The next few sections will describe how Write Accelerator can be enabled on Azure Premium Storage VHDs.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="29c89-150">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="29c89-150">Prerequisites</span></span>

<span data-ttu-id="29c89-151">The following prerequisites apply to the usage of Write Accelerator at this point in time:</span><span class="sxs-lookup"><span data-stu-id="29c89-151">The following prerequisites apply to the usage of Write Accelerator at this point in time:</span></span>

- <span data-ttu-id="29c89-152">The disks you want to apply Azure Write Accelerator against need to be [Azure managed disks](https://azure.microsoft.com/services/managed-disks/) on Premium Storage.</span><span class="sxs-lookup"><span data-stu-id="29c89-152">The disks you want to apply Azure Write Accelerator against need to be [Azure managed disks](https://azure.microsoft.com/services/managed-disks/) on Premium Storage.</span></span>
- <span data-ttu-id="29c89-153">You must be using an M-series VM</span><span class="sxs-lookup"><span data-stu-id="29c89-153">You must be using an M-series VM</span></span>

## <a name="enabling-azure-write-accelerator-using-azure-powershell"></a><span data-ttu-id="29c89-154">Enabling Azure Write Accelerator using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="29c89-154">Enabling Azure Write Accelerator using Azure PowerShell</span></span>

<span data-ttu-id="29c89-155">The Azure Power Shell module from version 5.5.0 include the changes to the relevant cmdlets to enable or disable Write Accelerator for specific Azure Premium Storage disks.</span><span class="sxs-lookup"><span data-stu-id="29c89-155">The Azure Power Shell module from version 5.5.0 include the changes to the relevant cmdlets to enable or disable Write Accelerator for specific Azure Premium Storage disks.</span></span>
<span data-ttu-id="29c89-156">In order to enable or deploy disks supported by Write Accelerator, the following Power Shell commands got changed, and extended to accept a parameter for Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-156">In order to enable or deploy disks supported by Write Accelerator, the following Power Shell commands got changed, and extended to accept a parameter for Write Accelerator.</span></span>

<span data-ttu-id="29c89-157">A new switch parameter, **-WriteAccelerator** has been added to the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="29c89-157">A new switch parameter, **-WriteAccelerator** has been added to the following cmdlets:</span></span>

- [<span data-ttu-id="29c89-158">Set-AzureRmVMOsDisk</span><span class="sxs-lookup"><span data-stu-id="29c89-158">Set-AzureRmVMOsDisk</span></span>](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/set-azurermvmosdisk?view=azurermps-6.0.0)
- [<span data-ttu-id="29c89-159">Add-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="29c89-159">Add-AzureRmVMDataDisk</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Add-AzureRmVMDataDisk?view=azurermps-6.0.0)
- [<span data-ttu-id="29c89-160">Set-AzureRmVMDataDisk</span><span class="sxs-lookup"><span data-stu-id="29c89-160">Set-AzureRmVMDataDisk</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Set-AzureRmVMDataDisk?view=azurermps-6.0.0)
- [<span data-ttu-id="29c89-161">Add-AzureRmVmssDataDisk</span><span class="sxs-lookup"><span data-stu-id="29c89-161">Add-AzureRmVmssDataDisk</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Add-AzureRmVmssDataDisk?view=azurermps-6.0.0)

<span data-ttu-id="29c89-162">Not giving the parameter sets the property to false and will deploy disks that have no support by Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-162">Not giving the parameter sets the property to false and will deploy disks that have no support by Write Accelerator.</span></span>

<span data-ttu-id="29c89-163">A new switch parameter, **-OsDiskWriteAccelerator** was added to the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="29c89-163">A new switch parameter, **-OsDiskWriteAccelerator** was added to the following cmdlets:</span></span>

- [<span data-ttu-id="29c89-164">Set-AzureRmVmssStorageProfile</span><span class="sxs-lookup"><span data-stu-id="29c89-164">Set-AzureRmVmssStorageProfile</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Set-AzureRmVmssStorageProfile?view=azurermps-6.0.0)

<span data-ttu-id="29c89-165">Not specifying the parameter sets the property to false by default, returning disks that don't leverage Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-165">Not specifying the parameter sets the property to false by default, returning disks that don't leverage Write Accelerator.</span></span>

<span data-ttu-id="29c89-166">A new optional Boolean (non-nullable) parameter, **-OsDiskWriteAccelerator** was added to the following cmdlets:</span><span class="sxs-lookup"><span data-stu-id="29c89-166">A new optional Boolean (non-nullable) parameter, **-OsDiskWriteAccelerator** was added to the following cmdlets:</span></span>

- [<span data-ttu-id="29c89-167">Update-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="29c89-167">Update-AzureRmVM</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Update-AzureRmVM?view=azurermps-6.0.0)
- [<span data-ttu-id="29c89-168">Update-AzureRmVmss</span><span class="sxs-lookup"><span data-stu-id="29c89-168">Update-AzureRmVmss</span></span>](https://docs.microsoft.com/en-us/powershell/module/AzureRM.Compute/Update-AzureRmVmss?view=azurermps-6.0.0)

<span data-ttu-id="29c89-169">Specify either $true or $false to control support of Azure Write Accelerator with the disks.</span><span class="sxs-lookup"><span data-stu-id="29c89-169">Specify either $true or $false to control support of Azure Write Accelerator with the disks.</span></span>

<span data-ttu-id="29c89-170">Examples of commands could look like:</span><span class="sxs-lookup"><span data-stu-id="29c89-170">Examples of commands could look like:</span></span>

```PowerShell
New-AzureRmVMConfig | Set-AzureRmVMOsDisk | Add-AzureRmVMDataDisk -Name "datadisk1" | Add-AzureRmVMDataDisk -Name "logdisk1" -WriteAccelerator | New-AzureRmVM

Get-AzureRmVM | Update-AzureRmVM -OsDiskWriteAccelerator $true

New-AzureRmVmssConfig | Set-AzureRmVmssStorageProfile -OsDiskWriteAccelerator | Add-AzureRmVmssDataDisk -Name "datadisk1" -WriteAccelerator:$false | Add-AzureRmVmssDataDisk -Name "logdisk1" -WriteAccelerator | New-AzureRmVmss

Get-AzureRmVmss | Update-AzureRmVmss -OsDiskWriteAccelerator:$false
```

<span data-ttu-id="29c89-171">Two main scenarios can be scripted as shown in the following sections.</span><span class="sxs-lookup"><span data-stu-id="29c89-171">Two main scenarios can be scripted as shown in the following sections.</span></span>

### <a name="adding-a-new-disk-supported-by-write-accelerator-using-powershell"></a><span data-ttu-id="29c89-172">Adding a new disk supported by Write Accelerator using PowerShell</span><span class="sxs-lookup"><span data-stu-id="29c89-172">Adding a new disk supported by Write Accelerator using PowerShell</span></span>

<span data-ttu-id="29c89-173">You can use this script to add a new disk to your VM.</span><span class="sxs-lookup"><span data-stu-id="29c89-173">You can use this script to add a new disk to your VM.</span></span> <span data-ttu-id="29c89-174">The disk created with this script uses Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-174">The disk created with this script uses Write Accelerator.</span></span>

<span data-ttu-id="29c89-175">Replace `myVM`, `myWAVMs`, `log001`, size of the disk, and LunID of the disk with values appropriate for your specific deployment.</span><span class="sxs-lookup"><span data-stu-id="29c89-175">Replace `myVM`, `myWAVMs`, `log001`, size of the disk, and LunID of the disk with values appropriate for your specific deployment.</span></span>

```PowerShell
# Specify your VM Name
$vmName="myVM"
#Specify your Resource Group
$rgName = "myWAVMs"
#data disk name
$datadiskname = "log001"
#LUN Id
$lunid=8
#size
$size=1023
#Pulls the VM info for later
$vm=Get-AzurermVM -ResourceGroupName $rgname -Name $vmname
#add a new VM data disk
Add-AzureRmVMDataDisk -CreateOption empty -DiskSizeInGB $size -Name $vmname-$datadiskname -VM $vm -Caching None -WriteAccelerator:$true -lun $lunid
#Updates the VM with the disk config - does not require a reboot
Update-AzureRmVM -ResourceGroupName $rgname -VM $vm
```

### <a name="enabling-write-accelerator-on-an-existing-azure-disk-using-powershell"></a><span data-ttu-id="29c89-176">Enabling Write Accelerator on an existing Azure disk using PowerShell</span><span class="sxs-lookup"><span data-stu-id="29c89-176">Enabling Write Accelerator on an existing Azure disk using PowerShell</span></span>

<span data-ttu-id="29c89-177">You can use this script to enable Write Accelerator on an existing disk.</span><span class="sxs-lookup"><span data-stu-id="29c89-177">You can use this script to enable Write Accelerator on an existing disk.</span></span> <span data-ttu-id="29c89-178">Replace `myVM`, `myWAVMs`, and `test-log001` with values appropriate for your specific deployment.</span><span class="sxs-lookup"><span data-stu-id="29c89-178">Replace `myVM`, `myWAVMs`, and `test-log001` with values appropriate for your specific deployment.</span></span> <span data-ttu-id="29c89-179">The script adds Write Accelerator to an existing disk where the value for **$newstatus** is set to '$true'.</span><span class="sxs-lookup"><span data-stu-id="29c89-179">The script adds Write Accelerator to an existing disk where the value for **$newstatus** is set to '$true'.</span></span> <span data-ttu-id="29c89-180">Using the value '$false' will disable Write Accelerator on a given disk.</span><span class="sxs-lookup"><span data-stu-id="29c89-180">Using the value '$false' will disable Write Accelerator on a given disk.</span></span>

```PowerShell
#Specify your VM Name
$vmName="myVM"
#Specify your Resource Group
$rgName = "myWAVMs"
#data disk name
$datadiskname = "test-log001" 
#new Write Accelerator status ($true for enabled, $false for disabled) 
$newstatus = $true
#Pulls the VM info for later
$vm=Get-AzurermVM -ResourceGroupName $rgname -Name $vmname
#add a new VM data disk
Set-AzureRmVMDataDisk -VM $vm -Name $datadiskname -Caching None -WriteAccelerator:$newstatus
#Updates the VM with the disk config - does not require a reboot
Update-AzureRmVM -ResourceGroupName $rgname -VM $vm
```

> [!Note]
> <span data-ttu-id="29c89-181">Executing the script above will detach the disk specified, enable Write Accelerator against the disk, and then attach the disk again</span><span class="sxs-lookup"><span data-stu-id="29c89-181">Executing the script above will detach the disk specified, enable Write Accelerator against the disk, and then attach the disk again</span></span>

## <a name="enabling-write-accelerator-using-the-azure-portal"></a><span data-ttu-id="29c89-182">Enabling Write Accelerator using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="29c89-182">Enabling Write Accelerator using the Azure portal</span></span>

<span data-ttu-id="29c89-183">You can enable Write Accelerator via the portal where you specify your disk caching settings:</span><span class="sxs-lookup"><span data-stu-id="29c89-183">You can enable Write Accelerator via the portal where you specify your disk caching settings:</span></span>

![Write Accelerator on the Azure portal](./media/virtual-machines-common-how-to-enable-write-accelerator/wa_scrnsht.png)

## <a name="enabling-write-accelerator-using-the-azure-cli"></a><span data-ttu-id="29c89-185">Enabling Write Accelerator using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="29c89-185">Enabling Write Accelerator using the Azure CLI</span></span>

<span data-ttu-id="29c89-186">You can use the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) to enable Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-186">You can use the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/?view=azure-cli-latest) to enable Write Accelerator.</span></span>

<span data-ttu-id="29c89-187">To enable Write Accelerator on an existing disk, use [az vm update](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az-vm-update), you may use the following examples if you replace the diskName, VMName, and ResourceGroup with your own values: `az vm update -g group1 -n vm1 -write-accelerator 1=true`</span><span class="sxs-lookup"><span data-stu-id="29c89-187">To enable Write Accelerator on an existing disk, use [az vm update](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az-vm-update), you may use the following examples if you replace the diskName, VMName, and ResourceGroup with your own values: `az vm update -g group1 -n vm1 -write-accelerator 1=true`</span></span>

<span data-ttu-id="29c89-188">To attach a disk with Write Accelerator enabled use [az vm disk attach](https://docs.microsoft.com/en-us/cli/azure/vm/disk?view=azure-cli-latest#az-vm-disk-attach), you may use the following example if you substitute in your own values: `az vm disk attach -g group1 -vm-name vm1 -disk d1 --enable-write-accelerator`</span><span class="sxs-lookup"><span data-stu-id="29c89-188">To attach a disk with Write Accelerator enabled use [az vm disk attach](https://docs.microsoft.com/en-us/cli/azure/vm/disk?view=azure-cli-latest#az-vm-disk-attach), you may use the following example if you substitute in your own values: `az vm disk attach -g group1 -vm-name vm1 -disk d1 --enable-write-accelerator`</span></span>

<span data-ttu-id="29c89-189">To disable Write Accelerator, use [az vm update](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az-vm-update), setting the properties to false: `az vm update -g group1 -n vm1 -write-accelerator 0=false 1=false`</span><span class="sxs-lookup"><span data-stu-id="29c89-189">To disable Write Accelerator, use [az vm update](https://docs.microsoft.com/en-us/cli/azure/vm?view=azure-cli-latest#az-vm-update), setting the properties to false: `az vm update -g group1 -n vm1 -write-accelerator 0=false 1=false`</span></span>

## <a name="enabling-write-accelerator-using-rest-apis"></a><span data-ttu-id="29c89-190">Enabling Write Accelerator using Rest APIs</span><span class="sxs-lookup"><span data-stu-id="29c89-190">Enabling Write Accelerator using Rest APIs</span></span>

<span data-ttu-id="29c89-191">To deploy through Azure Rest API, you need to install the Azure armclient.</span><span class="sxs-lookup"><span data-stu-id="29c89-191">To deploy through Azure Rest API, you need to install the Azure armclient.</span></span>

### <a name="install-armclient"></a><span data-ttu-id="29c89-192">Install armclient</span><span class="sxs-lookup"><span data-stu-id="29c89-192">Install armclient</span></span>

<span data-ttu-id="29c89-193">To run armclient, you need to install it through Chocolatey.</span><span class="sxs-lookup"><span data-stu-id="29c89-193">To run armclient, you need to install it through Chocolatey.</span></span> <span data-ttu-id="29c89-194">You can install it through cmd.exe or powershell.</span><span class="sxs-lookup"><span data-stu-id="29c89-194">You can install it through cmd.exe or powershell.</span></span> <span data-ttu-id="29c89-195">Use elevated rights for these commands (“Run as Administrator”).</span><span class="sxs-lookup"><span data-stu-id="29c89-195">Use elevated rights for these commands (“Run as Administrator”).</span></span>

<span data-ttu-id="29c89-196">Using cmd.exe, run the following command: `@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`</span><span class="sxs-lookup"><span data-stu-id="29c89-196">Using cmd.exe, run the following command: `@"%SystemRoot%\System32\WindowsPowerShell\v1.0\powershell.exe" -NoProfile -InputFormat None -ExecutionPolicy Bypass -Command "iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))" && SET "PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin"`</span></span>

<span data-ttu-id="29c89-197">Using Power Shell, run the following command: `Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`</span><span class="sxs-lookup"><span data-stu-id="29c89-197">Using Power Shell, run the following command: `Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))`</span></span>

<span data-ttu-id="29c89-198">Now you can install the armclient by using the following command in either cmd.exe or PowerShell `choco install armclient`</span><span class="sxs-lookup"><span data-stu-id="29c89-198">Now you can install the armclient by using the following command in either cmd.exe or PowerShell `choco install armclient`</span></span>

### <a name="getting-your-current-vm-configuration"></a><span data-ttu-id="29c89-199">Getting your current VM configuration</span><span class="sxs-lookup"><span data-stu-id="29c89-199">Getting your current VM configuration</span></span>

<span data-ttu-id="29c89-200">To change the attributes of your disk configuration, you first need to get the current configuration in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="29c89-200">To change the attributes of your disk configuration, you first need to get the current configuration in a JSON file.</span></span> <span data-ttu-id="29c89-201">You can get the current configuration by executing the following command: `armclient GET /subscriptions/<<subscription-ID<</resourceGroups/<<ResourceGroup>>/providers/Microsoft.Compute/virtualMachines/<<virtualmachinename>>?api-version=2017-12-01 > <<filename.json>>`</span><span class="sxs-lookup"><span data-stu-id="29c89-201">You can get the current configuration by executing the following command: `armclient GET /subscriptions/<<subscription-ID<</resourceGroups/<<ResourceGroup>>/providers/Microsoft.Compute/virtualMachines/<<virtualmachinename>>?api-version=2017-12-01 > <<filename.json>>`</span></span>

<span data-ttu-id="29c89-202">Replace the terms within '<<   >>' with your data, including the file name the JSON file should have.</span><span class="sxs-lookup"><span data-stu-id="29c89-202">Replace the terms within '<<   >>' with your data, including the file name the JSON file should have.</span></span>

<span data-ttu-id="29c89-203">The output could look like:</span><span class="sxs-lookup"><span data-stu-id="29c89-203">The output could look like:</span></span>

```JSON
{
  "properties": {
    "vmId": "2444c93e-f8bb-4a20-af2d-1658d9dbbbcb",
    "hardwareProfile": {
      "vmSize": "Standard_M64s"
    },
    "storageProfile": {
      "imageReference": {
        "publisher": "SUSE",
        "offer": "SLES-SAP",
        "sku": "12-SP3",
        "version": "latest"
      },
      "osDisk": {
        "osType": "Linux",
        "name": "mylittlesap_OsDisk_1_754a1b8bb390468e9b4c429b81cc5f5a",
        "createOption": "FromImage",
        "caching": "ReadWrite",
        "managedDisk": {
          "storageAccountType": "Premium_LRS",
          "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/mylittlesap_OsDisk_1_754a1b8bb390468e9b4c429b81cc5f5a"
        },
        "diskSizeGB": 30
      },
      "dataDisks": [
        {
          "lun": 0,
          "name": "data1",
          "createOption": "Attach",
          "caching": "None",
          "managedDisk": {
            "storageAccountType": "Premium_LRS",
            "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/data1"
          },
          "diskSizeGB": 1023
        },
        {
          "lun": 1,
          "name": "log1",
          "createOption": "Attach",
          "caching": "None",
          "managedDisk": {
            "storageAccountType": "Premium_LRS",
            "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/data2"
          },
          "diskSizeGB": 1023
        }
      ]
    },
    "osProfile": {
      "computerName": "mylittlesapVM",
      "adminUsername": "pl",
      "linuxConfiguration": {
        "disablePasswordAuthentication": false
      },
      "secrets": []
    },
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Network/networkInterfaces/mylittlesap518"
        }
      ]
    },
    "diagnosticsProfile": {
      "bootDiagnostics": {
        "enabled": true,
        "storageUri": "https://mylittlesapdiag895.blob.core.windows.net/"
      }
    },
    "provisioningState": "Succeeded"
  },
  "type": "Microsoft.Compute/virtualMachines",
  "location": "westeurope",
  "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/virtualMachines/mylittlesapVM",
  "name": "mylittlesapVM"

```

<span data-ttu-id="29c89-204">Next, update the JSON file and to enable Write Accelerator on the disk called 'log1'.</span><span class="sxs-lookup"><span data-stu-id="29c89-204">Next, update the JSON file and to enable Write Accelerator on the disk called 'log1'.</span></span> <span data-ttu-id="29c89-205">This can be accomplished by adding this attribute into the JSON file after the cache entry of the disk.</span><span class="sxs-lookup"><span data-stu-id="29c89-205">This can be accomplished by adding this attribute into the JSON file after the cache entry of the disk.</span></span>

```JSON
        {
          "lun": 1,
          "name": "log1",
          "createOption": "Attach",
          "caching": "None",
          "writeAcceleratorEnabled": true,
          "managedDisk": {
            "storageAccountType": "Premium_LRS",
            "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/data2"
          },
          "diskSizeGB": 1023
        }
```

<span data-ttu-id="29c89-206">Then update the existing deployment with this command: `armclient PUT /subscriptions/<<subscription-ID<</resourceGroups/<<ResourceGroup>>/providers/Microsoft.Compute/virtualMachines/<<virtualmachinename>>?api-version=2017-12-01 @<<filename.json>>`</span><span class="sxs-lookup"><span data-stu-id="29c89-206">Then update the existing deployment with this command: `armclient PUT /subscriptions/<<subscription-ID<</resourceGroups/<<ResourceGroup>>/providers/Microsoft.Compute/virtualMachines/<<virtualmachinename>>?api-version=2017-12-01 @<<filename.json>>`</span></span>

<span data-ttu-id="29c89-207">The output should look like the one below.</span><span class="sxs-lookup"><span data-stu-id="29c89-207">The output should look like the one below.</span></span> <span data-ttu-id="29c89-208">You can see that Write Accelerator enabled for one disk.</span><span class="sxs-lookup"><span data-stu-id="29c89-208">You can see that Write Accelerator enabled for one disk.</span></span>

```JSON
{
  "properties": {
    "vmId": "2444c93e-f8bb-4a20-af2d-1658d9dbbbcb",
    "hardwareProfile": {
      "vmSize": "Standard_M64s"
    },
    "storageProfile": {
      "imageReference": {
        "publisher": "SUSE",
        "offer": "SLES-SAP",
        "sku": "12-SP3",
        "version": "latest"
      },
      "osDisk": {
        "osType": "Linux",
        "name": "mylittlesap_OsDisk_1_754a1b8bb390468e9b4c429b81cc5f5a",
        "createOption": "FromImage",
        "caching": "ReadWrite",
        "managedDisk": {
          "storageAccountType": "Premium_LRS",
          "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/mylittlesap_OsDisk_1_754a1b8bb390468e9b4c429b81cc5f5a"
        },
        "diskSizeGB": 30
      },
      "dataDisks": [
        {
          "lun": 0,
          "name": "data1",
          "createOption": "Attach",
          "caching": "None",
          "managedDisk": {
            "storageAccountType": "Premium_LRS",
            "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/data1"
          },
          "diskSizeGB": 1023
        },
        {
          "lun": 1,
          "name": "log1",
          "createOption": "Attach",
          "caching": "None",
          "writeAcceleratorEnabled": true,
          "managedDisk": {
            "storageAccountType": "Premium_LRS",
            "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/disks/data2"
          },
          "diskSizeGB": 1023
        }
      ]
    },
    "osProfile": {
      "computerName": "mylittlesapVM",
      "adminUsername": "pl",
      "linuxConfiguration": {
        "disablePasswordAuthentication": false
      },
      "secrets": []
    },
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Network/networkInterfaces/mylittlesap518"
        }
      ]
    },
    "diagnosticsProfile": {
      "bootDiagnostics": {
        "enabled": true,
        "storageUri": "https://mylittlesapdiag895.blob.core.windows.net/"
      }
    },
    "provisioningState": "Succeeded"
  },
  "type": "Microsoft.Compute/virtualMachines",
  "location": "westeurope",
  "id": "/subscriptions/XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX/resourceGroups/mylittlesap/providers/Microsoft.Compute/virtualMachines/mylittlesapVM",
  "name": "mylittlesapVM"
```

<span data-ttu-id="29c89-209">Once you've made this change, the drive should be supported by Write Accelerator.</span><span class="sxs-lookup"><span data-stu-id="29c89-209">Once you've made this change, the drive should be supported by Write Accelerator.</span></span>
