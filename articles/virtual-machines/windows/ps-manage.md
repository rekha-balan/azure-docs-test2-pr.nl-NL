---
title: Manage Azure VMs using PowerShell | Microsoft Docs
description: Manage Azure virtual machines using PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: davidmu1
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 48930854-7888-4e4c-9efb-7d1971d4cc14
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: davidmu
ms.openlocfilehash: ad2ad1710669b15f10fab3ef31511fffe4c269e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563404"
---
# <a name="manage-azure-virtual-machines-using-powershell"></a><span data-ttu-id="5a474-103">Manage Azure Virtual Machines using PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a474-103">Manage Azure Virtual Machines using PowerShell</span></span>

<span data-ttu-id="5a474-104">This article shows you common management tasks you might perform on an Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-104">This article shows you common management tasks you might perform on an Azure virtual machine.</span></span>

<span data-ttu-id="5a474-105">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span><span class="sxs-lookup"><span data-stu-id="5a474-105">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for information about installing the latest version of Azure PowerShell, selecting your subscription, and signing in to your account.</span></span>

> [!NOTE]
> <span data-ttu-id="5a474-106">You may need to reinstall Azure PowerShell to use the functionality in this article.</span><span class="sxs-lookup"><span data-stu-id="5a474-106">You may need to reinstall Azure PowerShell to use the functionality in this article.</span></span> <span data-ttu-id="5a474-107">Managed Disks capabilities are in version 3.5 and higher.</span><span class="sxs-lookup"><span data-stu-id="5a474-107">Managed Disks capabilities are in version 3.5 and higher.</span></span>
> 
> 

<span data-ttu-id="5a474-108">Create these variables to make running the commands easier and change the values to match your environment:</span><span class="sxs-lookup"><span data-stu-id="5a474-108">Create these variables to make running the commands easier and change the values to match your environment:</span></span>
    
```powershell
$myResourceGroup = "myResourceGroup"
$myVM = "myVM"
$location = "centralus"
```

## <a name="display-information-about-a-virtual-machine"></a><span data-ttu-id="5a474-109">Display information about a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-109">Display information about a virtual machine</span></span>

<span data-ttu-id="5a474-110">Get information about a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-110">Get information about a virtual machine.</span></span>

```powershell
Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM -DisplayHint Expand
```

<span data-ttu-id="5a474-111">It returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-111">It returns something like this example:</span></span>

    ResourceGroupName             : myResourceGroup
    Id                            : /subscriptions/{subscription-id}/resourceGroups/
                                    myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
    VmId                          : #########-####-####-####-############
    Name                          : myVM
    Type                          : Microsoft.Compute/virtualMachines
    Location                      : centralus
    Tags                          : {}
    DiagnosticsProfile            :
      BootDiagnostics             :
      Enabled                     : True
      StorageUri                  : https://mystorage1.blob.core.windows.net/
    AvailabilitySetReference      : 
      Id                          : /subscriptions/{subscription-id}/resourceGroups/
                                    myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAV1
    Extensions[0]                 :
      Id                          : /subscriptions/{subscription-id}/resourceGroups/
                                    myResourceGroup/providers/Microsoft.Compute/
                                    virtualMachines/myVM/extensions/BGInfo
      Name                        : BGInfo
      Type                        : Microsoft.Compute/virtualMachines/extensions
      Location                    : centralus
      Publisher                   : Microsoft.Compute
      VirtualMachineExtensionType : BGInfo
      TypeHandlerVersion          : 2.1
      AutoUpgradeMinorVersion     : True
      ProvisioningState           : Succeeded
    HardwareProfile               : 
      VmSize                      : Standard_DS1_v2
    NetworkProfile          
      NetworkInterfaces[0]        :
        Id                        : /subscriptions/{subscription-id}/resourceGroups/
                                    myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNIC
    OSProfile                     : 
      ComputerName                : myVM
      AdminUsername               : myaccount1
      WindowsConfiguration        :
        ProvisionVMAgent          : True
         EnableAutomaticUpdates   : True
    ProvisioningState             : Succeeded
    StorageProfile                :
      ImageReference              :
        Publisher                 : MicrosoftWindowsServer
        Offer                     : WindowsServer
        Sku                       : 2012-R2-Datacenter
        Version                   : latest   
      OsDisk                      :
        OsType                    : Windows
        Name                      : myosdisk
        Vhd                       : 
          Uri                     : http://mystore1.blob.core.windows.net/vhds/myosdisk.vhd
        Caching                   : ReadWrite
        CreateOption              : FromImage
    NetworkInterfaceIDs[0]        : /subscriptions/{subscription-id}/resourceGroups/
                                    myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNIC

## <a name="stop-a-virtual-machine"></a><span data-ttu-id="5a474-112">Stop a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-112">Stop a virtual machine</span></span>

<span data-ttu-id="5a474-113">You can stop a virtual machine in two ways.</span><span class="sxs-lookup"><span data-stu-id="5a474-113">You can stop a virtual machine in two ways.</span></span> <span data-ttu-id="5a474-114">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span><span class="sxs-lookup"><span data-stu-id="5a474-114">You can stop a virtual machine and keep all its settings, but continue to be charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="5a474-115">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span><span class="sxs-lookup"><span data-stu-id="5a474-115">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

### <a name="stop-and-deallocate"></a><span data-ttu-id="5a474-116">Stop and deallocate</span><span class="sxs-lookup"><span data-stu-id="5a474-116">Stop and deallocate</span></span>
    
```powershell
Stop-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM
```

<span data-ttu-id="5a474-117">You're asked for confirmation:</span><span class="sxs-lookup"><span data-stu-id="5a474-117">You're asked for confirmation:</span></span>

    Virtual machine stopping operation
    This cmdlet will stop the specified virtual machine. Do you want to continue?
    [Y] Yes [N] No [S] Suspend [?] Help (default is "Y"):
 
    Enter **Y** to stop the virtual machine.

<span data-ttu-id="5a474-118">After a few minutes, it returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-118">After a few minutes, it returns something like this example:</span></span>

    OperationId :
    Status      : Succeeded
    StartTime   : 9/13/2016 12:11:57 PM
    EndTime     : 9/13/2016 12:14:40 PM
    Error       :

### <a name="stop-and-stay-provisioned"></a><span data-ttu-id="5a474-119">Stop and stay provisioned</span><span class="sxs-lookup"><span data-stu-id="5a474-119">Stop and stay provisioned</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM -StayProvisioned
```

<span data-ttu-id="5a474-120">You're asked for confirmation:</span><span class="sxs-lookup"><span data-stu-id="5a474-120">You're asked for confirmation:</span></span>

    Virtual machine stopping operation
    This cmdlet will stop the specified virtual machine. Do you want to continue?
    [Y] Yes [N] No [S] Suspend [?] Help (default is "Y"):
 
<span data-ttu-id="5a474-121">Enter **Y** to stop the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-121">Enter **Y** to stop the virtual machine.</span></span>

<span data-ttu-id="5a474-122">After a few minutes, it returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-122">After a few minutes, it returns something like this example:</span></span>

    OperationId :
    Status      : Succeeded
    StartTime   : 9/13/2016 12:11:57 PM
    EndTime     : 9/13/2016 12:14:40 PM
    Error       :

## <a name="start-a-virtual-machine"></a><span data-ttu-id="5a474-123">Start a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-123">Start a virtual machine</span></span>
 
<span data-ttu-id="5a474-124">Start a virtual machine if it's stopped.</span><span class="sxs-lookup"><span data-stu-id="5a474-124">Start a virtual machine if it's stopped.</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM
```

<span data-ttu-id="5a474-125">After a few minutes, it returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-125">After a few minutes, it returns something like this example:</span></span>

    OperationId :
    Status      : Succeeded
    StartTime   : 9/13/2016 12:32:55 PM
    EndTime     : 9/13/2016 12:35:09 PM
    Error       :

<span data-ttu-id="5a474-126">If you want to restart a virtual machine that is already running, use **Restart-AzureRmVM** described next.</span><span class="sxs-lookup"><span data-stu-id="5a474-126">If you want to restart a virtual machine that is already running, use **Restart-AzureRmVM** described next.</span></span>

## <a name="restart-a-virtual-machine"></a><span data-ttu-id="5a474-127">Restart a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-127">Restart a virtual machine</span></span>

<span data-ttu-id="5a474-128">Restart a running virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-128">Restart a running virtual machine.</span></span>

```powershell
Restart-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM
```

<span data-ttu-id="5a474-129">It returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-129">It returns something like this example:</span></span>

    OperationId :
    Status      : Succeeded
    StartTime   : 9/13/2016 12:54:40 PM
    EndTime     : 9/13/2016 12:55:54 PM
    Error       :    

## <a name="add-a-data-disk-to-a-virtual-machine"></a><span data-ttu-id="5a474-130">Add a data disk to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-130">Add a data disk to a virtual machine</span></span>
    
### <a name="managed-data-disk"></a><span data-ttu-id="5a474-131">Managed data disk</span><span class="sxs-lookup"><span data-stu-id="5a474-131">Managed data disk</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -AccountType PremiumLRS -Location $location -CreateOption Empty -DiskSizeGB 128
$dataDisk = New-AzureRmDisk -DiskName "myDataDisk1" -Disk $diskConfig -ResourceGroupName $myResourceGroup
$vm = Get-AzureRmVM -Name $myVM -ResourceGroupName $myResourceGroup
Add-AzureRmVMDataDisk -VM $vm -Name "myDataDisk1" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
Update-AzureRmVM -ResourceGroupName $myResourceGroup -VM $vm
```

<span data-ttu-id="5a474-132">After running Add-AzureRmVMDataDisk, you should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-132">After running Add-AzureRmVMDataDisk, you should see something like this example:</span></span>

    ResourceGroupName        : myResourceGroup
    Id                       : /subscriptions/{subscription-id}/resourceGroups/myResourceGroup/providers/
                               Microsoft.Compute/virtualMachines/myVM
    VmId                     : ########-####-####-####-############
    Name                     : myVM
    Type                     : Microsoft.Compute/virtualMachines
    Location                 : centralus
    Tags                     : {}
    AvailabilitySetReference : {Id}
    DiagnosticsProfile       : {BootDiagnostics}
    HardwareProfile          : {VmSize}
    NetworkProfile           : {NetworkInterfaces}
    OSProfile                : {ComputerName, AdminUsername, WindowsConfiguration, Secrets}
    ProvisioningState        : Succeeded
    StorageProfile           : {ImageReference, OsDisk, DataDisks}
    DataDiskNames            : {myDataDisk1}
    NetworkInterfaceIDs      : {/subscriptions/{subscription-id}/resourceGroups/myResourceGroup/providers/
                               Microsoft.Network/networkInterfaces/myNIC}

<span data-ttu-id="5a474-133">After running Update-AzureRmVM, you should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-133">After running Update-AzureRmVM, you should see something like this example:</span></span>

    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK

### <a name="unmanaged-data-disk"></a><span data-ttu-id="5a474-134">Unmanaged data disk</span><span class="sxs-lookup"><span data-stu-id="5a474-134">Unmanaged data disk</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM
Add-AzureRmVMDataDisk -VM $vm -Name "myDataDisk1" -VhdUri "https://mystore1.blob.core.windows.net/vhds/myDataDisk1.vhd" -LUN 0 -Caching ReadWrite -DiskSizeinGB 1 -CreateOption Empty
Update-AzureRmVM -ResourceGroupName $myResourceGroup -VM $vm
```

<span data-ttu-id="5a474-135">After running Add-AzureRmVMDataDisk, you should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-135">After running Add-AzureRmVMDataDisk, you should see something like this example:</span></span>

    ResourceGroupName        : myResourceGroup
    Id                       : /subscriptions/{subscription-id}/resourceGroups/myResourceGroup/providers/
                               Microsoft.Compute/virtualMachines/myVM
    VmId                     : ########-####-####-####-############
    Name                     : myVM
    Type                     : Microsoft.Compute/virtualMachines
    Location                 : centralus
    Tags                     : {}
    AvailabilitySetReference : {Id}
    DiagnosticsProfile       : {BootDiagnostics}
    HardwareProfile          : {VmSize}
    NetworkProfile           : {NetworkInterfaces}
    OSProfile                : {ComputerName, AdminUsername, WindowsConfiguration, Secrets}
    ProvisioningState        : Succeeded
    StorageProfile           : {ImageReference, OsDisk, DataDisks}
    DataDiskNames            : {myDataDisk1}
    NetworkInterfaceIDs      : {/subscriptions/{subscription-id}/resourceGroups/myResourceGroup/providers/
                               Microsoft.Network/networkInterfaces/myNIC}

<span data-ttu-id="5a474-136">After running Update-AzureRmVM, you should see something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-136">After running Update-AzureRmVM, you should see something like this example:</span></span>

    RequestId IsSuccessStatusCode StatusCode ReasonPhrase
    --------- ------------------- ---------- ------------
                             True         OK OK

## <a name="update-a-virtual-machine"></a><span data-ttu-id="5a474-137">Update a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-137">Update a virtual machine</span></span>

<span data-ttu-id="5a474-138">This example shows how to update the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-138">This example shows how to update the size of the virtual machine.</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName $myResourceGroup -Name $myVM
$vm.HardwareProfile.vmSize = "Standard_DS2_v2"
Update-AzureRmVM -ResourceGroupName $myResourceGroup -VM $vm
```

<span data-ttu-id="5a474-139">It returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-139">It returns something like this example:</span></span>

    RequestId  IsSuccessStatusCode  StatusCode  ReasonPhrase
    ---------  -------------------  ----------  ------------
                              True          OK  OK

<span data-ttu-id="5a474-140">See [Sizes for virtual machines in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for a list of available sizes for a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-140">See [Sizes for virtual machines in Azure](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for a list of available sizes for a virtual machine.</span></span>

## <a name="delete-a-virtual-machine"></a><span data-ttu-id="5a474-141">Delete a virtual machine</span><span class="sxs-lookup"><span data-stu-id="5a474-141">Delete a virtual machine</span></span>

<span data-ttu-id="5a474-142">Delete the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5a474-142">Delete the virtual machine.</span></span>  

```powershell
Remove-AzureRmVM -ResourceGroupName $myResourceGroup –Name $myVM
```

> [!NOTE]
> <span data-ttu-id="5a474-143">You can use the **-Force** parameter to skip the confirmation prompt.</span><span class="sxs-lookup"><span data-stu-id="5a474-143">You can use the **-Force** parameter to skip the confirmation prompt.</span></span>
> 
> 

<span data-ttu-id="5a474-144">If you didn't use the -Force parameter, you're asked for confirmation:</span><span class="sxs-lookup"><span data-stu-id="5a474-144">If you didn't use the -Force parameter, you're asked for confirmation:</span></span>

    Virtual machine removal operation
    This cmdlet will remove the specified virtual machine. Do you want to continue?
    [Y] Yes [N] No [S] Suspend [?] Help (default is "Y"):

<span data-ttu-id="5a474-145">It returns something like this example:</span><span class="sxs-lookup"><span data-stu-id="5a474-145">It returns something like this example:</span></span>

    RequestId  IsSuccessStatusCode  StatusCode  ReasonPhrase
    ---------  -------------------  ----------  ------------
                              True          OK  OK

## <a name="next-steps"></a><span data-ttu-id="5a474-146">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5a474-146">Next Steps</span></span>

- <span data-ttu-id="5a474-147">If there were issues with a deployment, you might look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md)</span><span class="sxs-lookup"><span data-stu-id="5a474-147">If there were issues with a deployment, you might look at [Troubleshoot common Azure deployment errors with Azure Resource Manager](../../resource-manager-common-deployment-errors.md)</span></span>
- <span data-ttu-id="5a474-148">Learn how to use Azure PowerShell to create a virtual machine from [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5a474-148">Learn how to use Azure PowerShell to create a virtual machine from [Create a Windows VM using Resource Manager and PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
- <span data-ttu-id="5a474-149">Take advantage of using a template to create a virtual machine by using the information in [Create a Windows virtual machine with a Resource Manager template](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="5a474-149">Take advantage of using a template to create a virtual machine by using the information in [Create a Windows virtual machine with a Resource Manager template](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
