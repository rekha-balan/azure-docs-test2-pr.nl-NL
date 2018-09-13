---
title: Create VM from a specialized disk in Azure | Microsoft Docs
description: Create a new VM by attaching a specialized managed disk or unmanaged disk, in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: cynthn
ms.openlocfilehash: bba72086e78afc890d07fb34a5c7749bb0bf3ff0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562724"
---
# <a name="create-a-vm-from-a-specialized-disk"></a><span data-ttu-id="5e3a0-103">Create a VM from a specialized disk</span><span class="sxs-lookup"><span data-stu-id="5e3a0-103">Create a VM from a specialized disk</span></span>

<span data-ttu-id="5e3a0-104">Create a new VM by attaching a specialized disk as the OS disk using Powershell.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-104">Create a new VM by attaching a specialized disk as the OS disk using Powershell.</span></span> <span data-ttu-id="5e3a0-105">A specialized disk is a copy of VHD from an exisitng VM that maintains the user accounts, applications and other state data from your original VM.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-105">A specialized disk is a copy of VHD from an exisitng VM that maintains the user accounts, applications and other state data from your original VM.</span></span> <span data-ttu-id="5e3a0-106">You can use either a specialized [managed disk](../../storage/storage-managed-disks-overview.md) or a specialized unmanaged disk to create the new VM.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-106">You can use either a specialized [managed disk](../../storage/storage-managed-disks-overview.md) or a specialized unmanaged disk to create the new VM.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5e3a0-107">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5e3a0-107">Before you begin</span></span>
<span data-ttu-id="5e3a0-108">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-108">If you use PowerShell, make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="5e3a0-109">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-109">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="5e3a0-110">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-110">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>


## <a name="create-the-subnet-and-vnet"></a><span data-ttu-id="5e3a0-111">Create the subNet and vNet</span><span class="sxs-lookup"><span data-stu-id="5e3a0-111">Create the subNet and vNet</span></span>

<span data-ttu-id="5e3a0-112">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-112">Create the vNet and subNet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="5e3a0-113">Create the subNet.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-113">Create the subNet.</span></span> <span data-ttu-id="5e3a0-114">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-114">This example creates a subnet named **mySubNet**, in the resource group **myResourceGroup**, and sets the subnet address prefix to **10.0.0.0/24**.</span></span>
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="5e3a0-115">Create the vNet.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-115">Create the vNet.</span></span> <span data-ttu-id="5e3a0-116">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-116">This example sets the virtual network name to be **myVnetName**, the location to **West US**, and the address prefix for the virtual network to **10.0.0.0/16**.</span></span> 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-nic"></a><span data-ttu-id="5e3a0-117">Create a public IP address and NIC</span><span class="sxs-lookup"><span data-stu-id="5e3a0-117">Create a public IP address and NIC</span></span>
<span data-ttu-id="5e3a0-118">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-118">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="5e3a0-119">Create the public IP.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-119">Create the public IP.</span></span> <span data-ttu-id="5e3a0-120">In this example, the public IP address name is set to **myIP**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-120">In this example, the public IP address name is set to **myIP**.</span></span>
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="5e3a0-121">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-121">Create the NIC.</span></span> <span data-ttu-id="5e3a0-122">In this example, the NIC name is set to **myNicName**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-122">In this example, the NIC name is set to **myNicName**.</span></span>
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="5e3a0-123">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="5e3a0-123">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="5e3a0-124">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-124">To be able to log in to your VM using RDP, you need to have an security rule that allows RDP access on port 3389.</span></span> <span data-ttu-id="5e3a0-125">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-125">Because the VHD for the new VM was created from an existing specialized VM, after the VM is created you can use an existing account from the source virtual machine that had permission to log on using RDP.</span></span>
<span data-ttu-id="5e3a0-126">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-126">This example sets the NSG name to **myNsg** and the RDP rule name to **myRdpRule**.</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

<span data-ttu-id="5e3a0-127">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-127">For more information about endpoints and NSG rules, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="set-the-vm-name-and-size"></a><span data-ttu-id="5e3a0-128">Set the VM name and size</span><span class="sxs-lookup"><span data-stu-id="5e3a0-128">Set the VM name and size</span></span>

<span data-ttu-id="5e3a0-129">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span><span class="sxs-lookup"><span data-stu-id="5e3a0-129">This example sets the VM name to "myVM" and the VM size to "Standard_A2".</span></span>
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

## <a name="add-the-nic"></a><span data-ttu-id="5e3a0-130">Add the NIC</span><span class="sxs-lookup"><span data-stu-id="5e3a0-130">Add the NIC</span></span>
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
## <a name="configure-the-os-disk"></a><span data-ttu-id="5e3a0-131">Configure the OS disk</span><span class="sxs-lookup"><span data-stu-id="5e3a0-131">Configure the OS disk</span></span>

<span data-ttu-id="5e3a0-132">The specialised OS could be a VHD that you [uploaded to Azure](upload-image.md) or a [copy the VHD from an existing Azure VM](vhd-copy.md).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-132">The specialised OS could be a VHD that you [uploaded to Azure](upload-image.md) or a [copy the VHD from an existing Azure VM](vhd-copy.md).</span></span> 

<span data-ttu-id="5e3a0-133">You can choose one of two options:</span><span class="sxs-lookup"><span data-stu-id="5e3a0-133">You can choose one of two options:</span></span>
- <span data-ttu-id="5e3a0-134">**Option 1**: Create a specialized managed disk from a specialied VHD in an existing storage account to use as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-134">**Option 1**: Create a specialized managed disk from a specialied VHD in an existing storage account to use as the OS disk.</span></span>

<span data-ttu-id="5e3a0-135">or</span><span class="sxs-lookup"><span data-stu-id="5e3a0-135">or</span></span> 

- <span data-ttu-id="5e3a0-136">**Option 2**: Use a specialized VHD stored in your own storage account (an unmanaged disk).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-136">**Option 2**: Use a specialized VHD stored in your own storage account (an unmanaged disk).</span></span> 

### <a name="option-1-create-a-managed-disk-from-an-unmanaged-specialized-disk"></a><span data-ttu-id="5e3a0-137">Option 1: Create a managed disk from an unmanaged specialized disk</span><span class="sxs-lookup"><span data-stu-id="5e3a0-137">Option 1: Create a managed disk from an unmanaged specialized disk</span></span>

1. <span data-ttu-id="5e3a0-138">Create a managed disk from the existing specialized VHD in your storage account.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-138">Create a managed disk from the existing specialized VHD in your storage account.</span></span> <span data-ttu-id="5e3a0-139">This example uses **myOSDisk1** for the disk name, puts the disk in **StandardLRS** storage and uses **https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vh.vhd** as the URI for the source VHD.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-139">This example uses **myOSDisk1** for the disk name, puts the disk in **StandardLRS** storage and uses **https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vh.vhd** as the URI for the source VHD.</span></span>

    ```powershell
    $osDisk = New-AzureRmDisk -DiskName "myOSDisk1" -Disk (New-AzureRmDiskConfig `
    -AccountType StandardLRS  -Location $location -CreationDataCreateOption Import `
    -SourceUri https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vh.vhd) `
    -ResourceGroupName $rgName
    ```

2. <span data-ttu-id="5e3a0-140">Add the OS disk to the configuration.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-140">Add the OS disk to the configuration.</span></span> <span data-ttu-id="5e3a0-141">This example sets the size of the disk to **128 GB** and attaches the managed disk as a **Windows** OS disk.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-141">This example sets the size of the disk to **128 GB** and attaches the managed disk as a **Windows** OS disk.</span></span>
    
    ```powershell
    $vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
    ```

<span data-ttu-id="5e3a0-142">Optional: Attach additional managed disks as data disks.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-142">Optional: Attach additional managed disks as data disks.</span></span> <span data-ttu-id="5e3a0-143">This option assumes that you created your managed data disks using [Create managed data disks](create-managed-disk-ps.md).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-143">This option assumes that you created your managed data disks using [Create managed data disks](create-managed-disk-ps.md).</span></span> 

```powershell
$vm = Add-AzureRmVMDataDisk -VM $VirtualMachine -Name $dataDiskName -CreateOption Attach -ManagedDiskId $dataDisk1.Id -Lun 1
```


### <a name="option-2-attach-a-vhd-that-is-in-an-existing-storage-account"></a><span data-ttu-id="5e3a0-144">Option 2: Attach a VHD that is in an existing storage account</span><span class="sxs-lookup"><span data-stu-id="5e3a0-144">Option 2: Attach a VHD that is in an existing storage account</span></span>

1. <span data-ttu-id="5e3a0-145">Set the URI for the VHD that you want to use.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-145">Set the URI for the VHD that you want to use.</span></span> <span data-ttu-id="5e3a0-146">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-146">In this example, the VHD file named **myOsDisk.vhd** is kept in a storage account named **myStorageAccount** in a container named **myContainer**.</span></span>

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. <span data-ttu-id="5e3a0-147">Add the OS disk by using the URL of the copied OS VHD.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-147">Add the OS disk by using the URL of the copied OS VHD.</span></span> <span data-ttu-id="5e3a0-148">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-148">In this example, when the OS disk is created, the term "osDisk" is appened to the VM name to create the OS disk name.</span></span> <span data-ttu-id="5e3a0-149">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-149">This example also specifies that this Windows-based VHD should be attached to the VM as the OS disk.</span></span>
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

<span data-ttu-id="5e3a0-150">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-150">Optional: If you have data disks that need to be attached to the VM, add the data disks by using the URLs of data VHDs and the appropriate Logical Unit Number (Lun).</span></span>

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

<span data-ttu-id="5e3a0-151">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-151">When using a storage account, the data and operating system disk URLs look something like this: `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`.</span></span> <span data-ttu-id="5e3a0-152">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-152">You can find this on the portal by browsing to the target storage container, clicking the operating system or data VHD that was copied, and then copying the contents of the URL.</span></span>


## <a name="create-the-vm"></a><span data-ttu-id="5e3a0-153">Create the VM</span><span class="sxs-lookup"><span data-stu-id="5e3a0-153">Create the VM</span></span>

<span data-ttu-id="5e3a0-154">Create the VM using the configurations that we just created.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-154">Create the VM using the configurations that we just created.</span></span>

```powershell
#Create the new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

<span data-ttu-id="5e3a0-155">If this command was successful, you'll see output like this:</span><span class="sxs-lookup"><span data-stu-id="5e3a0-155">If this command was successful, you'll see output like this:</span></span>

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="5e3a0-156">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="5e3a0-156">Verify that the VM was created</span></span>
<span data-ttu-id="5e3a0-157">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="5e3a0-157">You should see the newly created VM either in the [Azure portal](https://portal.azure.com), under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="5e3a0-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e3a0-158">Next steps</span></span>
<span data-ttu-id="5e3a0-159">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-159">To sign in to your new virtual machine, browse to the VM in the [portal](https://portal.azure.com), click **Connect**, and open the Remote Desktop RDP file.</span></span> <span data-ttu-id="5e3a0-160">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5e3a0-160">Use the account credentials of your original virtual machine to sign in to your new virtual machine.</span></span> <span data-ttu-id="5e3a0-161">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="5e3a0-161">For more information, see [How to connect and log on to an Azure virtual machine running Windows](connect-logon.md).</span></span>

