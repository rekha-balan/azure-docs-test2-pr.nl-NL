---
title: Quickstart - Create a Linux VM with Azure PowerShell | Microsoft Docs
description: In this quickstart, you learn how to use Azure PowerShell to create a Linux virtual machine
services: virtual-machines-linux
documentationcenter: virtual-machines
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: quickstart
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/24/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 5d4588d74b00c789253f04dc7f03eb149f891eb2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805186"
---
# <a name="quickstart-create-a-linux-virtual-machine-in-azure-with-powershell"></a><span data-ttu-id="f2005-103">Quickstart: Create a Linux virtual machine in Azure with PowerShell</span><span class="sxs-lookup"><span data-stu-id="f2005-103">Quickstart: Create a Linux virtual machine in Azure with PowerShell</span></span>

<span data-ttu-id="f2005-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="f2005-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="f2005-105">This quickstart shows you how to use the Azure PowerShell module to deploy a Linux virtual machine (VM) in Azure that runs Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f2005-105">This quickstart shows you how to use the Azure PowerShell module to deploy a Linux virtual machine (VM) in Azure that runs Ubuntu.</span></span> <span data-ttu-id="f2005-106">To see your VM in action, you then SSH to the VM and install the NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="f2005-106">To see your VM in action, you then SSH to the VM and install the NGINX web server.</span></span>

<span data-ttu-id="f2005-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f2005-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-powershell.md](../../../includes/cloud-shell-powershell.md)]

<span data-ttu-id="f2005-108">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span><span class="sxs-lookup"><span data-stu-id="f2005-108">If you choose to install and use the PowerShell locally, this tutorial requires the Azure PowerShell module version 5.7.0 or later.</span></span> <span data-ttu-id="f2005-109">Run `Get-Module -ListAvailable AzureRM` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f2005-109">Run `Get-Module -ListAvailable AzureRM` to find the version.</span></span> <span data-ttu-id="f2005-110">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f2005-110">If you need to upgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="f2005-111">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span><span class="sxs-lookup"><span data-stu-id="f2005-111">If you are running PowerShell locally, you also need to run `Connect-AzureRmAccount` to create a connection with Azure.</span></span>

<span data-ttu-id="f2005-112">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span><span class="sxs-lookup"><span data-stu-id="f2005-112">Finally, a public SSH key with the name *id_rsa.pub* needs to be stored in the *.ssh* directory of your Windows user profile.</span></span> <span data-ttu-id="f2005-113">For detailed information on how to create and use SSH keys, see [Create SSH keys for Azure](ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="f2005-113">For detailed information on how to create and use SSH keys, see [Create SSH keys for Azure](ssh-from-windows.md).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="f2005-114">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f2005-114">Create a resource group</span></span>

<span data-ttu-id="f2005-115">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="f2005-115">Create an Azure resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="f2005-116">A resource group is a logical container into which Azure resources are deployed and managed:</span><span class="sxs-lookup"><span data-stu-id="f2005-116">A resource group is a logical container into which Azure resources are deployed and managed:</span></span>

```azurepowershell-interactive
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

## <a name="create-virtual-network-resources"></a><span data-ttu-id="f2005-117">Create virtual network resources</span><span class="sxs-lookup"><span data-stu-id="f2005-117">Create virtual network resources</span></span>

<span data-ttu-id="f2005-118">Create a virtual network, subnet, and a public IP address.</span><span class="sxs-lookup"><span data-stu-id="f2005-118">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="f2005-119">These resources are used to provide network connectivity to the VM and connect it to the internet:</span><span class="sxs-lookup"><span data-stu-id="f2005-119">These resources are used to provide network connectivity to the VM and connect it to the internet:</span></span>

```azurepowershell-interactive
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnet" -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" -Location "EastUS" `
-Name "myVNET" -AddressPrefix 192.168.0.0/16 -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress -ResourceGroupName "myResourceGroup" -Location "EastUS" `
-AllocationMethod Static -IdleTimeoutInMinutes 4 -Name "mypublicdns$(Get-Random)"
```

<span data-ttu-id="f2005-120">Create an Azure Network Security Group and traffic rule.</span><span class="sxs-lookup"><span data-stu-id="f2005-120">Create an Azure Network Security Group and traffic rule.</span></span> <span data-ttu-id="f2005-121">The Network Security Group secures the VM with inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="f2005-121">The Network Security Group secures the VM with inbound and outbound rules.</span></span> <span data-ttu-id="f2005-122">In the following example, an inbound rule is created for TCP port 22 that allows SSH connections.</span><span class="sxs-lookup"><span data-stu-id="f2005-122">In the following example, an inbound rule is created for TCP port 22 that allows SSH connections.</span></span> <span data-ttu-id="f2005-123">To allow incoming web traffic, an inbound rule for TCP port 80 is also created.</span><span class="sxs-lookup"><span data-stu-id="f2005-123">To allow incoming web traffic, an inbound rule for TCP port 80 is also created.</span></span>

```azurepowershell-interactive
# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name "myNetworkSecurityGroupRuleSSH"  -Protocol "Tcp" `
-Direction "Inbound" -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access "Allow"

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name "myNetworkSecurityGroupRuleWWW"  -Protocol "Tcp" `
-Direction "Inbound" -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access "Allow"

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName "myResourceGroup" -Location "EastUS" `
-Name "myNetworkSecurityGroup" -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

<span data-ttu-id="f2005-124">Create a virtual network interface card (NIC) with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="f2005-124">Create a virtual network interface card (NIC) with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="f2005-125">The virtual NIC connects the VM to a subnet, Network Security Group, and public IP address.</span><span class="sxs-lookup"><span data-stu-id="f2005-125">The virtual NIC connects the VM to a subnet, Network Security Group, and public IP address.</span></span>

```azurepowershell-interactive
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name "myNic" -ResourceGroupName "myResourceGroup" -Location "EastUS" `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="f2005-126">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="f2005-126">Create a virtual machine</span></span>

<span data-ttu-id="f2005-127">A virtual machine configuration includes the settings that are used when a VM is deployed such as a VM image, size, and authentication options.</span><span class="sxs-lookup"><span data-stu-id="f2005-127">A virtual machine configuration includes the settings that are used when a VM is deployed such as a VM image, size, and authentication options.</span></span> <span data-ttu-id="f2005-128">Define the SSH credentials, OS information, and VM size as follows:</span><span class="sxs-lookup"><span data-stu-id="f2005-128">Define the SSH credentials, OS information, and VM size as follows:</span></span>

```azurepowershell-interactive
# Define a credential object
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ("azureuser", $securePassword)

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_D1" | `
Set-AzureRmVMOperatingSystem -Linux -ComputerName "myVM" -Credential $cred -DisablePasswordAuthentication | `
Set-AzureRmVMSourceImage -PublisherName "Canonical" -Offer "UbuntuServer" -Skus "16.04-LTS" -Version "latest" | `
Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"
Add-AzureRmVMSshPublicKey -VM $vmconfig -KeyData $sshPublicKey -Path "/home/azureuser/.ssh/authorized_keys"
```

<span data-ttu-id="f2005-129">Now, combine the previous configuration definitions to create with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span><span class="sxs-lookup"><span data-stu-id="f2005-129">Now, combine the previous configuration definitions to create with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm):</span></span>

```azurepowershell-interactive
New-AzureRmVM -ResourceGroupName "myResourceGroup" -Location eastus -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="f2005-130">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="f2005-130">Connect to virtual machine</span></span>

<span data-ttu-id="f2005-131">After the deployment has completed, SSH to the VM.</span><span class="sxs-lookup"><span data-stu-id="f2005-131">After the deployment has completed, SSH to the VM.</span></span> <span data-ttu-id="f2005-132">To see your VM in action, the NGINX web server is then installed.</span><span class="sxs-lookup"><span data-stu-id="f2005-132">To see your VM in action, the NGINX web server is then installed.</span></span>

<span data-ttu-id="f2005-133">To see the public IP address of the VM, use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="f2005-133">To see the public IP address of the VM, use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress) cmdlet:</span></span>

```azurepowershell-interactive
Get-AzureRmPublicIpAddress -ResourceGroupName "myResourceGroup" | Select "IpAddress"
```

<span data-ttu-id="f2005-134">Use an SSH client to connect to the VM.</span><span class="sxs-lookup"><span data-stu-id="f2005-134">Use an SSH client to connect to the VM.</span></span> <span data-ttu-id="f2005-135">You can use the Azure Cloud Shell from a web browser, or if you use Windows, you can use [Putty](ssh-from-windows.md) or the [Windows Subsystem for Linux](/windows/wsl/install-win10).</span><span class="sxs-lookup"><span data-stu-id="f2005-135">You can use the Azure Cloud Shell from a web browser, or if you use Windows, you can use [Putty](ssh-from-windows.md) or the [Windows Subsystem for Linux](/windows/wsl/install-win10).</span></span> <span data-ttu-id="f2005-136">Provide the public IP address of your VM:</span><span class="sxs-lookup"><span data-stu-id="f2005-136">Provide the public IP address of your VM:</span></span>

```bash
ssh azureuser@IpAddress
```

<span data-ttu-id="f2005-137">When prompted, the login user name is *azureuser*.</span><span class="sxs-lookup"><span data-stu-id="f2005-137">When prompted, the login user name is *azureuser*.</span></span> <span data-ttu-id="f2005-138">If a passphrase is used with your SSH keys, you need to enter that when prompted.</span><span class="sxs-lookup"><span data-stu-id="f2005-138">If a passphrase is used with your SSH keys, you need to enter that when prompted.</span></span>

## <a name="install-web-server"></a><span data-ttu-id="f2005-139">Install web server</span><span class="sxs-lookup"><span data-stu-id="f2005-139">Install web server</span></span>

<span data-ttu-id="f2005-140">To see your VM in action, install the NGINX web server.</span><span class="sxs-lookup"><span data-stu-id="f2005-140">To see your VM in action, install the NGINX web server.</span></span> <span data-ttu-id="f2005-141">To update package sources and install the latest NGINX package, run the following commands from your SSH session:</span><span class="sxs-lookup"><span data-stu-id="f2005-141">To update package sources and install the latest NGINX package, run the following commands from your SSH session:</span></span>

```bash
# update packages
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

<span data-ttu-id="f2005-142">When done, `exit` the SSH session</span><span class="sxs-lookup"><span data-stu-id="f2005-142">When done, `exit` the SSH session</span></span>

## <a name="view-the-web-server-in-action"></a><span data-ttu-id="f2005-143">View the web server in action</span><span class="sxs-lookup"><span data-stu-id="f2005-143">View the web server in action</span></span>

<span data-ttu-id="f2005-144">With NGINX installed and port 80 now open on your VM from the Internet, use a web browser of your choice to view the default NGINX welcome page.</span><span class="sxs-lookup"><span data-stu-id="f2005-144">With NGINX installed and port 80 now open on your VM from the Internet, use a web browser of your choice to view the default NGINX welcome page.</span></span> <span data-ttu-id="f2005-145">Use the public IP address of your VM obtained in a previous step.</span><span class="sxs-lookup"><span data-stu-id="f2005-145">Use the public IP address of your VM obtained in a previous step.</span></span> <span data-ttu-id="f2005-146">The following example shows the default NGINX web site:</span><span class="sxs-lookup"><span data-stu-id="f2005-146">The following example shows the default NGINX web site:</span></span>

![NGINX default site](./media/quick-create-cli/nginx.png)

## <a name="clean-up-resources"></a><span data-ttu-id="f2005-148">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f2005-148">Clean up resources</span></span>

<span data-ttu-id="f2005-149">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) cmdlet to remove the resource group, VM, and all related resources:</span><span class="sxs-lookup"><span data-stu-id="f2005-149">When no longer needed, you can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) cmdlet to remove the resource group, VM, and all related resources:</span></span>

```azurepowershell-interactive
Remove-AzureRmResourceGroup -Name "myResourceGroup"
```

## <a name="next-steps"></a><span data-ttu-id="f2005-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2005-150">Next steps</span></span>

<span data-ttu-id="f2005-151">In this quickstart, you deployed a simple virtual machine, created a Network Security Group and rule, and installed a basic web server.</span><span class="sxs-lookup"><span data-stu-id="f2005-151">In this quickstart, you deployed a simple virtual machine, created a Network Security Group and rule, and installed a basic web server.</span></span> <span data-ttu-id="f2005-152">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span><span class="sxs-lookup"><span data-stu-id="f2005-152">To learn more about Azure virtual machines, continue to the tutorial for Linux VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f2005-153">Azure Linux virtual machine tutorials</span><span class="sxs-lookup"><span data-stu-id="f2005-153">Azure Linux virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
