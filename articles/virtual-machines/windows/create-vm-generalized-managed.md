---
title: Create VM from a managed VM image in Azure | Microsoft Docs
description: Create a Windows virtual machine from a generalized managed VM image using Azure PowerShell, in the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/7/2017
ms.author: cynthn
ms.openlocfilehash: 0af15dc4a65d1e01c551479ee67c3fb9799c1e3f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564426"
---
# <a name="create-a-vm-from-a-generalized-managed-vm-image"></a><span data-ttu-id="ed06b-103">Create a VM from a generalized managed VM image</span><span class="sxs-lookup"><span data-stu-id="ed06b-103">Create a VM from a generalized managed VM image</span></span>

<span data-ttu-id="ed06b-104">You can create multiple VMs from a managed VM image in Azure.</span><span class="sxs-lookup"><span data-stu-id="ed06b-104">You can create multiple VMs from a managed VM image in Azure.</span></span> <span data-ttu-id="ed06b-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span><span class="sxs-lookup"><span data-stu-id="ed06b-105">A managed VM image contains the information necessary to create a VM, including the OS and data disks.</span></span> <span data-ttu-id="ed06b-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span><span class="sxs-lookup"><span data-stu-id="ed06b-106">The VHDs that make up the image, including both the OS disks and any data disks, are stored as managed disks.</span></span> 

<span data-ttu-id="ed06b-107">A generalized VM has had all of your personal account information removed using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed06b-107">A generalized VM has had all of your personal account information removed using [Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ed06b-108">You can create a generalized VM by running Sysprep on an on-premises VM, then [uploading the VHD to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), or by running Sysprep on an existing Azure VM, and then [capturing an image of the VM](capture-image-resource.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed06b-108">You can create a generalized VM by running Sysprep on an on-premises VM, then [uploading the VHD to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), or by running Sysprep on an existing Azure VM, and then [capturing an image of the VM](capture-image-resource.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>



## <a name="prerequisites"></a><span data-ttu-id="ed06b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ed06b-109">Prerequisites</span></span>

<span data-ttu-id="ed06b-110">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span><span class="sxs-lookup"><span data-stu-id="ed06b-110">You need to have already [created a managed VM image](capture-image-resource.md) to use for creating the new VM.</span></span> 

<span data-ttu-id="ed06b-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="ed06b-111">Make sure that you have the latest version of the AzureRM.Compute PowerShell module.</span></span> <span data-ttu-id="ed06b-112">Run the following command to install it.</span><span class="sxs-lookup"><span data-stu-id="ed06b-112">Run the following command to install it.</span></span>

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
<span data-ttu-id="ed06b-113">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span><span class="sxs-lookup"><span data-stu-id="ed06b-113">For more information, see [Azure PowerShell Versioning](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/#azure-powershell-versioning).</span></span>



## <a name="collect-information-about-the-image"></a><span data-ttu-id="ed06b-114">Collect information about the image</span><span class="sxs-lookup"><span data-stu-id="ed06b-114">Collect information about the image</span></span>

<span data-ttu-id="ed06b-115">First we need to gather basic information about the image and create a variable for the image.</span><span class="sxs-lookup"><span data-stu-id="ed06b-115">First we need to gather basic information about the image and create a variable for the image.</span></span> <span data-ttu-id="ed06b-116">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span><span class="sxs-lookup"><span data-stu-id="ed06b-116">This example uses a managed VM image named **myImage** that is in the **myResourceGroup** resource group in the **West Central US** location.</span></span> 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="ed06b-117">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="ed06b-117">Create a virtual network</span></span>
<span data-ttu-id="ed06b-118">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed06b-118">Create the vNet and subnet of the [virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="ed06b-119">Create the subnet.</span><span class="sxs-lookup"><span data-stu-id="ed06b-119">Create the subnet.</span></span> <span data-ttu-id="ed06b-120">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-120">This example creates a subnet named **mySubnet** with the address prefix of **10.0.0.0/24**.</span></span>  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. <span data-ttu-id="ed06b-121">Create the virtual network.</span><span class="sxs-lookup"><span data-stu-id="ed06b-121">Create the virtual network.</span></span> <span data-ttu-id="ed06b-122">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-122">This example creates a virtual network named **myVnet** with the address prefix of **10.0.0.0/16**.</span></span>  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a><span data-ttu-id="ed06b-123">Create a public IP address and network interface</span><span class="sxs-lookup"><span data-stu-id="ed06b-123">Create a public IP address and network interface</span></span>

<span data-ttu-id="ed06b-124">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span><span class="sxs-lookup"><span data-stu-id="ed06b-124">To enable communication with the virtual machine in the virtual network, you need a [public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) and a network interface.</span></span>

1. <span data-ttu-id="ed06b-125">Create a public IP address.</span><span class="sxs-lookup"><span data-stu-id="ed06b-125">Create a public IP address.</span></span> <span data-ttu-id="ed06b-126">This example creates a public IP address named **myPip**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-126">This example creates a public IP address named **myPip**.</span></span> 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. <span data-ttu-id="ed06b-127">Create the NIC.</span><span class="sxs-lookup"><span data-stu-id="ed06b-127">Create the NIC.</span></span> <span data-ttu-id="ed06b-128">This example creates a NIC named **myNic**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-128">This example creates a NIC named **myNic**.</span></span> 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

## <a name="create-the-network-security-group-and-an-rdp-rule"></a><span data-ttu-id="ed06b-129">Create the network security group and an RDP rule</span><span class="sxs-lookup"><span data-stu-id="ed06b-129">Create the network security group and an RDP rule</span></span>

<span data-ttu-id="ed06b-130">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span><span class="sxs-lookup"><span data-stu-id="ed06b-130">To be able to log in to your VM using RDP, you need to have a network security rule (NSG) that allows RDP access on port 3389.</span></span> 

<span data-ttu-id="ed06b-131">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span><span class="sxs-lookup"><span data-stu-id="ed06b-131">This example creates an NSG named **myNsg** that contains a rule called **myRdpRule** that allows RDP traffic over port 3389.</span></span> <span data-ttu-id="ed06b-132">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed06b-132">For more information about NSGs, see [Opening ports to a VM in Azure using PowerShell](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-the-virtual-network"></a><span data-ttu-id="ed06b-133">Create a variable for the virtual network</span><span class="sxs-lookup"><span data-stu-id="ed06b-133">Create a variable for the virtual network</span></span>

<span data-ttu-id="ed06b-134">Create a variable for the completed virtual network.</span><span class="sxs-lookup"><span data-stu-id="ed06b-134">Create a variable for the completed virtual network.</span></span> 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-the-credentials-for-the-vm"></a><span data-ttu-id="ed06b-135">Get the credentials for the VM</span><span class="sxs-lookup"><span data-stu-id="ed06b-135">Get the credentials for the VM</span></span>

<span data-ttu-id="ed06b-136">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span><span class="sxs-lookup"><span data-stu-id="ed06b-136">The following cmdlet will open a window where you will enter a new user name and password to use as the local administrator account for remotely accessing the VM.</span></span> 

```powershell
$cred = Get-Credential
```

## <a name="set-variables-for-the-vm-name-computer-name-and-the-size-of-the-vm"></a><span data-ttu-id="ed06b-137">Set variables for the VM name, computer name and the size of the VM</span><span class="sxs-lookup"><span data-stu-id="ed06b-137">Set variables for the VM name, computer name and the size of the VM</span></span>

1. <span data-ttu-id="ed06b-138">Create variables for the VM name and computer name.</span><span class="sxs-lookup"><span data-stu-id="ed06b-138">Create variables for the VM name and computer name.</span></span> <span data-ttu-id="ed06b-139">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-139">This example sets the VM name as **myVM** and the computer name as **myComputer**.</span></span>

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. <span data-ttu-id="ed06b-140">Set the size of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ed06b-140">Set the size of the virtual machine.</span></span> <span data-ttu-id="ed06b-141">This example creates **Standard_DS1_v2** sized VM.</span><span class="sxs-lookup"><span data-stu-id="ed06b-141">This example creates **Standard_DS1_v2** sized VM.</span></span> <span data-ttu-id="ed06b-142">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span><span class="sxs-lookup"><span data-stu-id="ed06b-142">See the [VM sizes](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/) documentation for more information.</span></span>

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. <span data-ttu-id="ed06b-143">Add the VM name and size to the VM configuration.</span><span class="sxs-lookup"><span data-stu-id="ed06b-143">Add the VM name and size to the VM configuration.</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-the-vm-image-as-source-image-for-the-new-vm"></a><span data-ttu-id="ed06b-144">Set the VM image as source image for the new VM</span><span class="sxs-lookup"><span data-stu-id="ed06b-144">Set the VM image as source image for the new VM</span></span>

<span data-ttu-id="ed06b-145">Set the source image using the ID of the managed VM image.</span><span class="sxs-lookup"><span data-stu-id="ed06b-145">Set the source image using the ID of the managed VM image.</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-the-os-configuration-and-add-the-nic"></a><span data-ttu-id="ed06b-146">Set the OS configuration and add the NIC.</span><span class="sxs-lookup"><span data-stu-id="ed06b-146">Set the OS configuration and add the NIC.</span></span>

<span data-ttu-id="ed06b-147">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span><span class="sxs-lookup"><span data-stu-id="ed06b-147">Enter the storage type (PremiumLRS or StandardLRS) and the size of the OS disk.</span></span> <span data-ttu-id="ed06b-148">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="ed06b-148">This example sets the account type to **PremiumLRS**, the disk size to **128 GB** and disk caching to **ReadWrite**.</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-the-vm"></a><span data-ttu-id="ed06b-149">Create the VM</span><span class="sxs-lookup"><span data-stu-id="ed06b-149">Create the VM</span></span>

<span data-ttu-id="ed06b-150">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span><span class="sxs-lookup"><span data-stu-id="ed06b-150">Create the new Vm using the configuration that we have built and stored in the **$vm** variable.</span></span>

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-the-vm-was-created"></a><span data-ttu-id="ed06b-151">Verify that the VM was created</span><span class="sxs-lookup"><span data-stu-id="ed06b-151">Verify that the VM was created</span></span>
<span data-ttu-id="ed06b-152">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="ed06b-152">When complete, you should see the newly created VM in the [Azure portal](https://portal.azure.com) under **Browse** > **Virtual machines**, or by using the following PowerShell commands:</span></span>

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a><span data-ttu-id="ed06b-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed06b-153">Next steps</span></span>
<span data-ttu-id="ed06b-154">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ed06b-154">To manage your new virtual machine with Azure PowerShell, see [Manage virtual machines using Azure Resource Manager and PowerShell](ps-manage.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

