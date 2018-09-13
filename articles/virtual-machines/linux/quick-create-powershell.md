---
title: Azure Quick Start - Create VM PowerShell | Microsoft Docs
description: Quickly learn to create a Linux virtual machines with PowerShell
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/03/2017
ms.author: nepeters
ms.openlocfilehash: c090ce765ca4e985718399669909147a21cfe336
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554730"
---
# <a name="create-a-linux-virtual-machine-with-powershell"></a><span data-ttu-id="dde62-103">Create a Linux virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="dde62-103">Create a Linux virtual machine with PowerShell</span></span>

<span data-ttu-id="dde62-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="dde62-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="dde62-105">This guide details using PowerShell to create and Azure virtual machine running Ubuntu 14.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="dde62-105">This guide details using PowerShell to create and Azure virtual machine running Ubuntu 14.04 LTS.</span></span>

<span data-ttu-id="dde62-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="dde62-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="dde62-107">Also, make sure that the latest version of the Azure PowerShell module has been installed.</span><span class="sxs-lookup"><span data-stu-id="dde62-107">Also, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="dde62-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="dde62-108">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

<span data-ttu-id="dde62-109">Finally, a public SSH key with the name `id_rsa.pub` needs to be stored in the `.ssh` directory of your Windows user profile.</span><span class="sxs-lookup"><span data-stu-id="dde62-109">Finally, a public SSH key with the name `id_rsa.pub` needs to be stored in the `.ssh` directory of your Windows user profile.</span></span> <span data-ttu-id="dde62-110">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="dde62-110">For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="dde62-111">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="dde62-111">Log in to Azure</span></span>

<span data-ttu-id="dde62-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="dde62-112">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="dde62-113">Create resource group</span><span class="sxs-lookup"><span data-stu-id="dde62-113">Create resource group</span></span>

<span data-ttu-id="dde62-114">Create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="dde62-114">Create an Azure resource group.</span></span> <span data-ttu-id="dde62-115">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="dde62-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location westeurope
```

## <a name="create-networking-resources"></a><span data-ttu-id="dde62-116">Create networking resources</span><span class="sxs-lookup"><span data-stu-id="dde62-116">Create networking resources</span></span>

<span data-ttu-id="dde62-117">Create a virtual network, subnet, and a public IP address.</span><span class="sxs-lookup"><span data-stu-id="dde62-117">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="dde62-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span><span class="sxs-lookup"><span data-stu-id="dde62-118">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name mySubnet -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName myResourceGroup -Location westeurope `
-Name MYvNET -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup -Location westeurope `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="dde62-119">Create a network security group and a network security group rule.</span><span class="sxs-lookup"><span data-stu-id="dde62-119">Create a network security group and a network security group rule.</span></span> <span data-ttu-id="dde62-120">The network security group secures the virtual machine using inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="dde62-120">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="dde62-121">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span><span class="sxs-lookup"><span data-stu-id="dde62-121">In this case, an inbound rule is created for port 22, which allows incoming SSH connections.</span></span> <span data-ttu-id="dde62-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span><span class="sxs-lookup"><span data-stu-id="dde62-122">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleSSH  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location westeurope `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="dde62-123">Create a network card for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dde62-123">Create a network card for the virtual machine.</span></span> <span data-ttu-id="dde62-124">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span><span class="sxs-lookup"><span data-stu-id="dde62-124">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location westeurope `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="dde62-125">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="dde62-125">Create virtual machine</span></span>

<span data-ttu-id="dde62-126">Create a virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="dde62-126">Create a virtual machine configuration.</span></span> <span data-ttu-id="dde62-127">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span><span class="sxs-lookup"><span data-stu-id="dde62-127">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span>

```powershell
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_D1 | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName myVM -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName Canonical -Offer UbuntuServer -Skus 14.04.2-LTS -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="dde62-128">Create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dde62-128">Create the virtual machine.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="dde62-129">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="dde62-129">Connect to virtual machine</span></span>

<span data-ttu-id="dde62-130">After the deployment has completed, create an SSH connection with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dde62-130">After the deployment has completed, create an SSH connection with the virtual machine.</span></span>

<span data-ttu-id="dde62-131">Run the following commands to return the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dde62-131">Run the following commands to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="dde62-132">From a system with SSH installed, used the following command to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="dde62-132">From a system with SSH installed, used the following command to connect to the virtual machine.</span></span> <span data-ttu-id="dde62-133">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span><span class="sxs-lookup"><span data-stu-id="dde62-133">If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection.</span></span> 

```bash 
ssh <Public IP Address>
```

<span data-ttu-id="dde62-134">When prompted, the login user name is `azureuser`.</span><span class="sxs-lookup"><span data-stu-id="dde62-134">When prompted, the login user name is `azureuser`.</span></span> <span data-ttu-id="dde62-135">If a passphrase was entered when creating SSH keys, you will need to enter this as well.</span><span class="sxs-lookup"><span data-stu-id="dde62-135">If a passphrase was entered when creating SSH keys, you will need to enter this as well.</span></span>


## <a name="install-nginx"></a><span data-ttu-id="dde62-136">Install NGINX</span><span class="sxs-lookup"><span data-stu-id="dde62-136">Install NGINX</span></span>

<span data-ttu-id="dde62-137">Use the following bash script to update package sources and install the latest NGINX package.</span><span class="sxs-lookup"><span data-stu-id="dde62-137">Use the following bash script to update package sources and install the latest NGINX package.</span></span> 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a><span data-ttu-id="dde62-138">View the NGIX welcome page</span><span class="sxs-lookup"><span data-stu-id="dde62-138">View the NGIX welcome page</span></span>

<span data-ttu-id="dde62-139">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span><span class="sxs-lookup"><span data-stu-id="dde62-139">With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="dde62-140">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="dde62-140">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span></span> 

![NGINX default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-cli/nginx.png) 
## <a name="delete-virtual-machine"></a><span data-ttu-id="dde62-142">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="dde62-142">Delete virtual machine</span></span>

<span data-ttu-id="dde62-143">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="dde62-143">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="dde62-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="dde62-144">Next steps</span></span>

[<span data-ttu-id="dde62-145">Create highly available virtual machines tutorial</span><span class="sxs-lookup"><span data-stu-id="dde62-145">Create highly available virtual machines tutorial</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="dde62-146">Explore VM deployment PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="dde62-146">Explore VM deployment PowerShell samples</span></span>](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

