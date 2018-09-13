---
title: Manage Windows virtual machines with Azure PowerShell | Microsoft Docs
description: Tutorial - Manage Windows virtual machines with Azure PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/21/2017
ms.author: davidmu
ms.openlocfilehash: 8dde92d3bee451ee701508cec98b3581384fd16c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552961"
---
# <a name="manage-windows-virtual-machines-with-azure-powershell"></a><span data-ttu-id="f5536-103">Manage Windows virtual machines with Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5536-103">Manage Windows virtual machines with Azure PowerShell</span></span>

<span data-ttu-id="f5536-104">In this tutorial, you create a virtual machine and perform common management tasks such as adding a disk, automating software installation, managing firewall rules, and creating a virtual machine snapshot.</span><span class="sxs-lookup"><span data-stu-id="f5536-104">In this tutorial, you create a virtual machine and perform common management tasks such as adding a disk, automating software installation, managing firewall rules, and creating a virtual machine snapshot.</span></span>

<span data-ttu-id="f5536-105">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) module.</span><span class="sxs-lookup"><span data-stu-id="f5536-105">To complete this tutorial, make sure that you have installed the latest [Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) module.</span></span>

## <a name="step-1--log-in-to-azure"></a><span data-ttu-id="f5536-106">Step 1 – Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="f5536-106">Step 1 – Log in to Azure</span></span>

<span data-ttu-id="f5536-107">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="f5536-107">First, log in to your Azure subscription with the Login-AzureRmAccount command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="step-2---create-resource-group"></a><span data-ttu-id="f5536-108">Step 2 - Create resource group</span><span class="sxs-lookup"><span data-stu-id="f5536-108">Step 2 - Create resource group</span></span>

<span data-ttu-id="f5536-109">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f5536-109">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="f5536-110">A resource group must be created before a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-110">A resource group must be created before a virtual machine.</span></span>

<span data-ttu-id="f5536-111">Create a resource group with [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v2.0.3/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f5536-111">Create a resource group with [New-AzureRmResourceGroup](https://docs.microsoft.com/powershell/resourcemanager/AzureRM.Resources/v2.0.3/new-azurermresourcegroup).</span></span>  <span data-ttu-id="f5536-112">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region:</span><span class="sxs-lookup"><span data-stu-id="f5536-112">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region:</span></span>

```powershell
New-AzureRmResourceGroup -ResourceGroupName myResourceGroup -Location westeurope
```

## <a name="step-3---create-virtual-machine"></a><span data-ttu-id="f5536-113">Step 3 - Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-113">Step 3 - Create virtual machine</span></span>

<span data-ttu-id="f5536-114">A virtual machine must be connected to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="f5536-114">A virtual machine must be connected to a virtual network.</span></span> <span data-ttu-id="f5536-115">You communicate with the virtual machine using a public IP address through a network interface card.</span><span class="sxs-lookup"><span data-stu-id="f5536-115">You communicate with the virtual machine using a public IP address through a network interface card.</span></span>

### <a name="create-virtual-network"></a><span data-ttu-id="f5536-116">Create virtual network</span><span class="sxs-lookup"><span data-stu-id="f5536-116">Create virtual network</span></span>

<span data-ttu-id="f5536-117">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f5536-117">Create a subnet with [New-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="f5536-118">Create a virtual network with [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="f5536-118">Create a virtual network with [New-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermvirtualnetwork):</span></span>

```powershell
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```
### <a name="create-public-ip-address"></a><span data-ttu-id="f5536-119">Create public IP address</span><span class="sxs-lookup"><span data-stu-id="f5536-119">Create public IP address</span></span>

<span data-ttu-id="f5536-120">Create a public IP address with [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="f5536-120">Create a public IP address with [New-AzureRmPublicIpAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermpublicipaddress):</span></span>

```powershell
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -AllocationMethod Static `
  -Name myPublicIPAddress
```

### <a name="create-network-interface-card"></a><span data-ttu-id="f5536-121">Create network interface card</span><span class="sxs-lookup"><span data-stu-id="f5536-121">Create network interface card</span></span>

<span data-ttu-id="f5536-122">Create a network interface card with [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f5536-122">Create a network interface card with [New-AzureRmNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworkinterface):</span></span>

```powershell
$nic = New-AzureRmNetworkInterface `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNic `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id
```

### <a name="create-network-security-group"></a><span data-ttu-id="f5536-123">Create network security group</span><span class="sxs-lookup"><span data-stu-id="f5536-123">Create network security group</span></span>

<span data-ttu-id="f5536-124">An Azure [network security group](../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span><span class="sxs-lookup"><span data-stu-id="f5536-124">An Azure [network security group](../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="f5536-125">Network security group rules allow or deny network traffic on a specific port or port range.</span><span class="sxs-lookup"><span data-stu-id="f5536-125">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="f5536-126">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-126">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span> <span data-ttu-id="f5536-127">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span><span class="sxs-lookup"><span data-stu-id="f5536-127">To access the IIS webserver that you are installing, you must add an inbound NSG rule.</span></span>

<span data-ttu-id="f5536-128">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/add-azurermnetworksecurityruleconfig).</span><span class="sxs-lookup"><span data-stu-id="f5536-128">To create an inbound NSG rule, use [Add-AzureRmNetworkSecurityRuleConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/add-azurermnetworksecurityruleconfig).</span></span> <span data-ttu-id="f5536-129">The following example creates an NSG rule named `myNSGRule` that opens port `80` for the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="f5536-129">The following example creates an NSG rule named `myNSGRule` that opens port `80` for the virtual machine:</span></span>

```powershell
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNSGRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow
```

<span data-ttu-id="f5536-130">Create the NSG using `myNSGRule` with [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecuritygroup):</span><span class="sxs-lookup"><span data-stu-id="f5536-130">Create the NSG using `myNSGRule` with [New-AzureRmNetworkSecurityGroup](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/new-azurermnetworksecuritygroup):</span></span>

```powershell
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule
```

<span data-ttu-id="f5536-131">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetworksubnetconfig):</span><span class="sxs-lookup"><span data-stu-id="f5536-131">Add the NSG to the subnet in the virtual network with [Set-AzureRmVirtualNetworkSubnetConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetworksubnetconfig):</span></span>

```powershell
Set-AzureRmVirtualNetworkSubnetConfig -Name mySubnet `
  -VirtualNetwork $vnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24
```

<span data-ttu-id="f5536-132">Update the virtual network with [Set-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetwork):</span><span class="sxs-lookup"><span data-stu-id="f5536-132">Update the virtual network with [Set-AzureRmVirtualNetwork](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/set-azurermvirtualnetwork):</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

### <a name="create-virtual-machine"></a><span data-ttu-id="f5536-133">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-133">Create virtual machine</span></span>

<span data-ttu-id="f5536-134">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="f5536-134">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="f5536-135">In this example, a virtual machine is created with a name of `myVM` running the latest version of Windows Server 2016 Datacenter.</span><span class="sxs-lookup"><span data-stu-id="f5536-135">In this example, a virtual machine is created with a name of `myVM` running the latest version of Windows Server 2016 Datacenter.</span></span>

<span data-ttu-id="f5536-136">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="f5536-136">Set the username and password needed for the administrator account on the virtual machine with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="f5536-137">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="f5536-137">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="f5536-138">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem):</span><span class="sxs-lookup"><span data-stu-id="f5536-138">Add the operating system information to the virtual machine configuration with [Set-AzureRmVMOperatingSystem](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmoperatingsystem):</span></span>

```powershell
$vm = Set-AzureRmVMOperatingSystem -VM $vm `
  -Windows `
  -ComputerName myVM `
  -Credential $cred `
  -ProvisionVMAgent `
  -EnableAutoUpdate
```

<span data-ttu-id="f5536-139">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage):</span><span class="sxs-lookup"><span data-stu-id="f5536-139">Add the image information to the virtual machine configuration with [Set-AzureRmVMSourceImage](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmsourceimage):</span></span>

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm `
  -PublisherName MicrosoftWindowsServer `
  -Offer WindowsServer `
  -Skus 2016-Datacenter `
  -Version latest
```

<span data-ttu-id="f5536-140">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-140">Add the operating system disk settings to the virtual machine configuration with [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm `
  -Name myOsDisk `
  -DiskSizeInGB 128 `
  -CreateOption FromImage `
  -Caching ReadWrite
```

<span data-ttu-id="f5536-141">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f5536-141">Add the network interface card that you previously created to the virtual machine configuration with [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="f5536-142">Create the virtual machine with [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-142">Create the virtual machine with [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm):</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vm
```

## <a name="step-4--add-data-disk"></a><span data-ttu-id="f5536-143">Step 4 – Add data disk</span><span class="sxs-lookup"><span data-stu-id="f5536-143">Step 4 – Add data disk</span></span>

<span data-ttu-id="f5536-144">By default, Azure virtual machines are created with a single operating system disk.</span><span class="sxs-lookup"><span data-stu-id="f5536-144">By default, Azure virtual machines are created with a single operating system disk.</span></span> <span data-ttu-id="f5536-145">Additional disks can be added for multi-disk storage configuration, application installation, and data.</span><span class="sxs-lookup"><span data-stu-id="f5536-145">Additional disks can be added for multi-disk storage configuration, application installation, and data.</span></span>

### <a name="create-disk"></a><span data-ttu-id="f5536-146">Create disk</span><span class="sxs-lookup"><span data-stu-id="f5536-146">Create disk</span></span>

<span data-ttu-id="f5536-147">Create the initial configuration of the data disk with [New-AzureRmDiskConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdiskconfig).</span><span class="sxs-lookup"><span data-stu-id="f5536-147">Create the initial configuration of the data disk with [New-AzureRmDiskConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdiskconfig).</span></span> <span data-ttu-id="f5536-148">The following example creates a disk named `myDataDisk` that is 50 gigabytes in size:</span><span class="sxs-lookup"><span data-stu-id="f5536-148">The following example creates a disk named `myDataDisk` that is 50 gigabytes in size:</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig `
  -Location westeurope `
  -CreateOption Empty `
  -DiskSizeGB 50
```

<span data-ttu-id="f5536-149">Create the data disk with [New-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-149">Create the data disk with [New-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdisk):</span></span>

```powershell
$dataDisk = New-AzureRmDisk `
  -ResourceGroupName myResourceGroup `
  -DiskName myDataDisk `
  -Disk $diskConfig
```

<span data-ttu-id="f5536-150">Get the virtual machine that you want to add the data disk to with [Get-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-150">Get the virtual machine that you want to add the data disk to with [Get-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermvm):</span></span>

```powershell
$vm = Get-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

<span data-ttu-id="f5536-151">Add the data disk to the virtual machine configuration with [Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmdatadisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-151">Add the data disk to the virtual machine configuration with [Add-AzureRmVMDataDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmdatadisk):</span></span>

```powershell
$vm = Add-AzureRmVMDataDisk `
  -VM $vm `
  -Name myDataDisk `
  -CreateOption Attach `
  -ManagedDiskId $dataDisk.Id `
  -Lun 1
```

<span data-ttu-id="f5536-152">Update the virtual machine with [Update-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/update-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-152">Update the virtual machine with [Update-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/update-azurermvm):</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

## <a name="step-5--automate-configuration"></a><span data-ttu-id="f5536-153">Step 5 – Automate configuration</span><span class="sxs-lookup"><span data-stu-id="f5536-153">Step 5 – Automate configuration</span></span>

<span data-ttu-id="f5536-154">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span><span class="sxs-lookup"><span data-stu-id="f5536-154">Azure virtual machine extensions are used to automate virtual machine configuration tasks such as installing applications and configuring the operating system.</span></span> <span data-ttu-id="f5536-155">The [custom script extension for Windows](./virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-155">The [custom script extension for Windows](./virtual-machines-windows-extensions-customscript.md) is used to run any PowerShell script on the virtual machine.</span></span> <span data-ttu-id="f5536-156">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span><span class="sxs-lookup"><span data-stu-id="f5536-156">The script can be stored in Azure storage, any accessible HTTP endpoint, or embedded in the custom script extension configuration.</span></span> <span data-ttu-id="f5536-157">In this tutorial, two actions are automated:</span><span class="sxs-lookup"><span data-stu-id="f5536-157">In this tutorial, two actions are automated:</span></span>

- <span data-ttu-id="f5536-158">Installing IIS</span><span class="sxs-lookup"><span data-stu-id="f5536-158">Installing IIS</span></span>
- <span data-ttu-id="f5536-159">Formatting a data disk on the VM</span><span class="sxs-lookup"><span data-stu-id="f5536-159">Formatting a data disk on the VM</span></span>

<span data-ttu-id="f5536-160">Because the extension runs at VM deployment time, the **install-iis-format-disk.ps1** file needs to be defined before creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-160">Because the extension runs at VM deployment time, the **install-iis-format-disk.ps1** file needs to be defined before creating the virtual machine.</span></span> <span data-ttu-id="f5536-161">For this tutorial, the file is located in the Azure PowerShell scripts repository.</span><span class="sxs-lookup"><span data-stu-id="f5536-161">For this tutorial, the file is located in the Azure PowerShell scripts repository.</span></span> <span data-ttu-id="f5536-162">The file contains the `Add-WindowsFeature Web-Server` command and the `Get-Disk | Where partitionstyle -eq 'raw' | Initialize-Disk -PartitionStyle MBR -PassThru | New-Partition -AssignDriveLetter -UseMaximumSize | Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false**` command.</span><span class="sxs-lookup"><span data-stu-id="f5536-162">The file contains the `Add-WindowsFeature Web-Server` command and the `Get-Disk | Where partitionstyle -eq 'raw' | Initialize-Disk -PartitionStyle MBR -PassThru | New-Partition -AssignDriveLetter -UseMaximumSize | Format-Volume -FileSystem NTFS -NewFileSystemLabel "myDataDisk" -Confirm:$false**` command.</span></span>

<span data-ttu-id="f5536-163">Add the extension with [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmextension):</span><span class="sxs-lookup"><span data-stu-id="f5536-163">Add the extension with [Set-AzureRmVMExtension](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmextension):</span></span>

```powershell
Set-AzureRmVMExtension -Name myScript `
  -ResourceGroupName myResourceGroup `
  -Location westeurope `
  -VMName myVM `
  -Publisher Microsoft.Compute `
  -ExtensionType CustomScriptExtension `
  -TypeHandlerVersion 1.4 `
  -SettingString '{"fileUris":["https://raw.githubusercontent.com/Azure/azure-docs-powershell-samples/master/virtual-machine/install-iis-format-disk/install-iis-format-disk.ps1?token=ABlGkLjzVTdZGoCRbu1pCXjvSDRMHnUlks5Y5nbZwA%3D%3D"], "commandToExecute":"powershell.exe -ExecutionPolicy Unrestricted -File install-iis-format-disk.ps1" }'
```

<span data-ttu-id="f5536-164">Get the public IP address of the virtual machine with [Get-AzureRmPublicIPAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermpublicipaddress):</span><span class="sxs-lookup"><span data-stu-id="f5536-164">Get the public IP address of the virtual machine with [Get-AzureRmPublicIPAddress](https://docs.microsoft.com/powershell/resourcemanager/azurerm.network/v3.6.0/get-azurermpublicipaddress):</span></span>

```powershell
Get-AzureRmPublicIPAddress -ResourceGroupName myResourceGroup -Name myPublicIPAddress | select IpAddress
```

<span data-ttu-id="f5536-165">Now browse to the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-165">Now browse to the public IP address of the virtual machine.</span></span> <span data-ttu-id="f5536-166">With the NSG rule in place, the default IIS website is displayed.</span><span class="sxs-lookup"><span data-stu-id="f5536-166">With the NSG rule in place, the default IIS website is displayed.</span></span>


## <a name="step-6--snapshot-virtual-machine"></a><span data-ttu-id="f5536-167">Step 6 – Snapshot virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-167">Step 6 – Snapshot virtual machine</span></span>

<span data-ttu-id="f5536-168">Taking a snapshot of a virtual machine creates a read only, point-in-time copy of the virtual machines operating system disk.</span><span class="sxs-lookup"><span data-stu-id="f5536-168">Taking a snapshot of a virtual machine creates a read only, point-in-time copy of the virtual machines operating system disk.</span></span> <span data-ttu-id="f5536-169">With a snapshot, the virtual machine can be restored to a specific state, or the snapshot can be used to create a new virtual machine with an identical state.</span><span class="sxs-lookup"><span data-stu-id="f5536-169">With a snapshot, the virtual machine can be restored to a specific state, or the snapshot can be used to create a new virtual machine with an identical state.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="f5536-170">Create snapshot</span><span class="sxs-lookup"><span data-stu-id="f5536-170">Create snapshot</span></span>

<span data-ttu-id="f5536-171">Before creating a virtual machine disk snapshot, the Id of the operating system disk for the virtual machine is needed.</span><span class="sxs-lookup"><span data-stu-id="f5536-171">Before creating a virtual machine disk snapshot, the Id of the operating system disk for the virtual machine is needed.</span></span>

<span data-ttu-id="f5536-172">Get the operating system disk with [Get-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-172">Get the operating system disk with [Get-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermdisk):</span></span>

```powershell
$vmOSDisk = Get-AzureRmDisk -ResourceGroupName myResourceGroup -Name myOSDisk
```

<span data-ttu-id="f5536-173">Create the configuration of the snapshot with New-AzureRmSnapshotConfig:</span><span class="sxs-lookup"><span data-stu-id="f5536-173">Create the configuration of the snapshot with New-AzureRmSnapshotConfig:</span></span>

```powershell
$snapshotConfig = New-AzureRmSnapshotConfig -Location westeurope -CreateOption Copy -SourceResourceId $vmOSDisk.id
```

<span data-ttu-id="f5536-174">Create the snapshot with New-AzureRmSnapshot:</span><span class="sxs-lookup"><span data-stu-id="f5536-174">Create the snapshot with New-AzureRmSnapshot:</span></span>

```powershell
$snapshot = New-AzureRmSnapshot -ResourceGroupName myResourceGroup -SnapshotName mySnapshot -Snapshot $snapshotConfig
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="f5536-175">Create disk from snapshot</span><span class="sxs-lookup"><span data-stu-id="f5536-175">Create disk from snapshot</span></span>

<span data-ttu-id="f5536-176">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-176">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

<span data-ttu-id="f5536-177">Create the configuration of the disk with [New-AzureRmDiskConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdiskconfig):</span><span class="sxs-lookup"><span data-stu-id="f5536-177">Create the configuration of the disk with [New-AzureRmDiskConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdiskconfig):</span></span>

```powershell
$diskConfig = New-AzureRmDiskConfig -Location westeurope -CreateOption Copy -SourceResourceId $snapshot.id
```

<span data-ttu-id="f5536-178">Create the disk with [New-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-178">Create the disk with [New-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermdisk):</span></span>

```powershell
$disk = New-AzureRmDisk -ResourceGroupName myResourceGroup -DiskName myOSDiskFromSnapshot -Disk $diskConfig
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="f5536-179">Restore virtual machine from snapshot</span><span class="sxs-lookup"><span data-stu-id="f5536-179">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="f5536-180">To demonstrate virtual machine recovery, delete the existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-180">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span>

```powershell
Remove-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM -Force
```

<span data-ttu-id="f5536-181">Create a new virtual machine from the snapshot disk.</span><span class="sxs-lookup"><span data-stu-id="f5536-181">Create a new virtual machine from the snapshot disk.</span></span> <span data-ttu-id="f5536-182">In this example, the existing network interface is being specified.</span><span class="sxs-lookup"><span data-stu-id="f5536-182">In this example, the existing network interface is being specified.</span></span> <span data-ttu-id="f5536-183">This configuration applies all previously created NSG rules to the new virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-183">This configuration applies all previously created NSG rules to the new virtual machine.</span></span>

<span data-ttu-id="f5536-184">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig):</span><span class="sxs-lookup"><span data-stu-id="f5536-184">Create the initial configuration for the virtual machine with [New-AzureRmVMConfig](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvmconfig):</span></span>

```powershell
$vm = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1
```

<span data-ttu-id="f5536-185">Add the operating system disk with [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-185">Add the operating system disk with [Set-AzureRmVMOSDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/set-azurermvmosdisk):</span></span>

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -CreateOption Attach -ManagedDiskId $disk.Id -Windows
```

<span data-ttu-id="f5536-186">Add the network interface card with [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface):</span><span class="sxs-lookup"><span data-stu-id="f5536-186">Add the network interface card with [Add-AzureRmVMNetworkInterface](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/add-azurermvmnetworkinterface):</span></span>

```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

<span data-ttu-id="f5536-187">Create the virtual machine with [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-187">Create the virtual machine with [New-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/new-azurermvm):</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm -Location westeurope
```

<span data-ttu-id="f5536-188">Enter the public IP address of the virtual machine into the address bar of the internet browser.</span><span class="sxs-lookup"><span data-stu-id="f5536-188">Enter the public IP address of the virtual machine into the address bar of the internet browser.</span></span> <span data-ttu-id="f5536-189">You should see that IIS is running in the restored virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-189">You should see that IIS is running in the restored virtual machine.</span></span>

## <a name="step-7--management-tasks"></a><span data-ttu-id="f5536-190">Step 7 – Management tasks</span><span class="sxs-lookup"><span data-stu-id="f5536-190">Step 7 – Management tasks</span></span>

<span data-ttu-id="f5536-191">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="f5536-191">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="f5536-192">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span><span class="sxs-lookup"><span data-stu-id="f5536-192">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="f5536-193">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="f5536-193">Using Azure PowerShell, many common management tasks can be run from the command line or in scripts.</span></span>

### <a name="stop-virtual-machine"></a><span data-ttu-id="f5536-194">Stop virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-194">Stop virtual machine</span></span>

<span data-ttu-id="f5536-195">Stop and deallocate a virtual machine with [Stop-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/stop-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-195">Stop and deallocate a virtual machine with [Stop-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/stop-azurermvm):</span></span>

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM -Force
```

<span data-ttu-id="f5536-196">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span><span class="sxs-lookup"><span data-stu-id="f5536-196">If you want to keep the virtual machine in a provisioned state, use the -StayProvisioned parameter.</span></span>

### <a name="resize-virtual-machine"></a><span data-ttu-id="f5536-197">Resize virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-197">Resize virtual machine</span></span>

<span data-ttu-id="f5536-198">To resize a stopped and deallocated virtual machine, you need the name of the sizes available in the chosen Azure region.</span><span class="sxs-lookup"><span data-stu-id="f5536-198">To resize a stopped and deallocated virtual machine, you need the name of the sizes available in the chosen Azure region.</span></span> <span data-ttu-id="f5536-199">These sizes can be found with[Get-AzureRmVMSize](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermvmsize):</span><span class="sxs-lookup"><span data-stu-id="f5536-199">These sizes can be found with[Get-AzureRmVMSize](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermvmsize):</span></span>

```powershell
Get-AzureRmVMSize -Location westeurope
```

<span data-ttu-id="f5536-200">Get the virtual machine that you want to resize with [Get-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermdisk):</span><span class="sxs-lookup"><span data-stu-id="f5536-200">Get the virtual machine that you want to resize with [Get-AzureRmDisk](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/get-azurermdisk):</span></span>

```powershell
$vm = Get-AzureRmVM -Name myVM -ResourceGroupName myResourceGroup
```

<span data-ttu-id="f5536-201">Set the new size of the virtual machine by setting the vmSize property with the size that you selected.</span><span class="sxs-lookup"><span data-stu-id="f5536-201">Set the new size of the virtual machine by setting the vmSize property with the size that you selected.</span></span>

```powershell
$vm.HardwareProfile.vmSize = "Standard_F4s"
```

<span data-ttu-id="f5536-202">Update the virtual machine with [Update-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/update-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f5536-202">Update the virtual machine with [Update-AzureRmVM](https://docs.microsoft.com/powershell/resourcemanager/azurerm.compute/v2.8.0/update-azurermvm):</span></span>

```powershell
Update-AzureRmVM -ResourceGroupName myResourceGroup -VM $vm
```

### <a name="start-virtual-machine"></a><span data-ttu-id="f5536-203">Start virtual machine</span><span class="sxs-lookup"><span data-stu-id="f5536-203">Start virtual machine</span></span>

```powershell
Start-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="f5536-204">Delete resource group</span><span class="sxs-lookup"><span data-stu-id="f5536-204">Delete resource group</span></span>

<span data-ttu-id="f5536-205">Deleting a resource group also deletes all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="f5536-205">Deleting a resource group also deletes all resources contained within.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="next-steps"></a><span data-ttu-id="f5536-206">Next Steps</span><span class="sxs-lookup"><span data-stu-id="f5536-206">Next Steps</span></span>

<span data-ttu-id="f5536-207">Samples – [Azure Virtual Machine PowerShell sample scripts](./virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="f5536-207">Samples – [Azure Virtual Machine PowerShell sample scripts](./virtual-machines-windows-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span>
