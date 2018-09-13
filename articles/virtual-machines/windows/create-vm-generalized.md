---
title: Create VM from a generalized VHD | Microsoft Docs
description: Learn how to create a Windows virtual machine from a generalized VHD image in a storage account, using Azure PowerShell.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: b4808871-9ef1-49ea-a617-9154d417abb0
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: cynthn
ms.openlocfilehash: 58d7c4f3f0ba253d8b6eed198c0fead3adc54eb5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562767"
---
# <a name="create-a-vm-from-a-generalized-vhd-image-in-a-storage-account"></a><span data-ttu-id="d895b-103">Create a VM from a generalized VHD image in a storage account</span><span class="sxs-lookup"><span data-stu-id="d895b-103">Create a VM from a generalized VHD image in a storage account</span></span> 

<span data-ttu-id="d895b-104">This topic covers creating a VM from a generalized unmanaged disk that is in a storage account.</span><span class="sxs-lookup"><span data-stu-id="d895b-104">This topic covers creating a VM from a generalized unmanaged disk that is in a storage account.</span></span> <span data-ttu-id="d895b-105">A generalized VHD image has had all of your personal account information removed using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-105">A generalized VHD image has had all of your personal account information removed using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d895b-106">You can create a generalized VHD by running Sysprep on an on-premises VM, then [uploading the VHD to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), or by running Sysprep on an existing Azure VM and then [copying the VHD](vhd-copy.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-106">You can create a generalized VHD by running Sysprep on an on-premises VM, then [uploading the VHD to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), or by running Sysprep on an existing Azure VM and then [copying the VHD](vhd-copy.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d895b-107">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-107">If you want to create a VM from a specialized VHD in a storage account, see [Create a VM from a specialized VHD](create-vm-specialized.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="d895b-108">For information about using Managed Disks instead of disks in a storage account, see [Created a managed VM image](capture-image-resource.md) and [Create a VM from a managed image](create-vm-generalized-managed.md).</span><span class="sxs-lookup"><span data-stu-id="d895b-108">For information about using Managed Disks instead of disks in a storage account, see [Created a managed VM image](capture-image-resource.md) and [Create a VM from a managed image](create-vm-generalized-managed.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d895b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d895b-109">Prerequisites</span></span>
<span data-ttu-id="d895b-110">If you are going to use a VHD uploaded from an on-premises VM, like one created using Hyper-V, you should make sure you followed the directions in [Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-110">If you are going to use a VHD uploaded from an on-premises VM, like one created using Hyper-V, you should make sure you followed the directions in [Prepare a Windows VHD to upload to Azure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="d895b-111">Both uploaded VHDs and existing Azure VM VHDs need to be generalized before you can create a VM using this method.</span><span class="sxs-lookup"><span data-stu-id="d895b-111">Both uploaded VHDs and existing Azure VM VHDs need to be generalized before you can create a VM using this method.</span></span> <span data-ttu-id="d895b-112">For more information, see [Generalize a Windows virtual machine using Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-112">For more information, see [Generalize a Windows virtual machine using Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="set-the-uri-of-the-vhd"></a><span data-ttu-id="d895b-113">Set the URI of the VHD</span><span class="sxs-lookup"><span data-stu-id="d895b-113">Set the URI of the VHD</span></span>

<span data-ttu-id="d895b-114">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span><span class="sxs-lookup"><span data-stu-id="d895b-114">The URI for the VHD to use is in the format: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd.</span></span> <span data-ttu-id="d895b-115">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="d895b-115">In this example the VHD named **myVHD** is in the storage account **mystorageaccount** in the container **mycontainer**.</span></span>

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


## <a name="create-a-virtual-network"></a><span data-ttu-id="d895b-116">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="d895b-116">Create a virtual network</span></span>
<span data-ttu-id="d895b-117">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d895b-117">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="d895b-118">Create the subnet.</span><span class="sxs-lookup"><span data-stu-id="d895b-118">Create the subnet.</span></span> <span data-ttu-id="d895b-119">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="d895b-119">The following sample creates a subnet named **mySubnet** in the resource group **myResourceGroup** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="d895b-120">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="d895b-120">Create the virtual network.</span></span> <span data-ttu-id="d895b-121">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="d895b-121">The following sample creates a virtual network named **myVnet** in the **West US** location with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="d895b-122">Create a public IP address and network interface</span><span class="sxs-lookup"><span data-stu-id="d895b-122">Create a public IP address and network interface</span></span>
<span data-ttu-id="d895b-123">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="d895b-123">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="d895b-124">Create a public IP address.</span><span class="sxs-lookup"><span data-stu-id="d895b-124">Create a public IP address.</span></span> <span data-ttu-id="d895b-125">This example creates a public IP address named **myPip**.</span><span class="sxs-lookup"><span data-stu-id="d895b-125">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="d895b-126">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="d895b-126">Create the NIC.</span></span> <span data-ttu-id="d895b-127">This example creates a NIC named **myNic**.</span><span class="sxs-lookup"><span data-stu-id="d895b-127">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="d895b-128">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="d895b-128">Create the network security group and an RDP rule</span></span>
<span data-ttu-id="d895b-129">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="d895b-129">To be able to log in to your VM using RDP, you need to have a security rule that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="d895b-130">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span><span class="sxs-lookup"><span data-stu-id="d895b-130">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="d895b-131">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-131">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="d895b-132">Create a variable for the virtual network</span><span class="sxs-lookup"><span data-stu-id="d895b-132">Create a variable for the virtual network</span></span>
<span data-ttu-id="d895b-133">Create a variable for the completed virtual network.</span><span class="sxs-lookup"><span data-stu-id="d895b-133">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

## <a name="create-the-vm"></a><span data-ttu-id="d895b-134">Create the VM</span><span class="sxs-lookup"><span data-stu-id="d895b-134">Create the VM</span></span>
<span data-ttu-id="d895b-135">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span><span class="sxs-lookup"><span data-stu-id="d895b-135">The following PowerShell script shows how to set up the virtual machine configurations and use the uploaded VM image as the source for the new installation.</span></span>

</br>

```powershell
    # Enter a new user name and password to use as the local administrator account 
    # for remotely accessing the VM.
    $cred = Get-Credential

    # Name of the storage account where the VHD is located. This example sets the 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of the virtual machine. This example sets the VM name as "myVM".
    $vmName = "myVM"

    # Size of the virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See the VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for the VM. This examples sets the computer name as "myComputer".
    $computerName = "myComputer"

    # Name of the disk that holds the OS. This example sets the 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets the SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get the storage account where the uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set the VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set the Windows operating system configuration and add the NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create the OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure the OS disk to be created from the existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create the new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="d895b-136">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="d895b-136">Verify that the VM was created</span></span>
<span data-ttu-id="d895b-137">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="d895b-137">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="d895b-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="d895b-138">Next steps</span></span>
<span data-ttu-id="d895b-139">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d895b-139">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
