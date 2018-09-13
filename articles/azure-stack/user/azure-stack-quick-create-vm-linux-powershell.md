---
title: Create a Linux virtual machine by using PowerShell in Azure Stack | Microsoft Docs
description: Create a Linux virtual machine with PowerShell in Azure Stack.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: quickstart
ms.date: 09/07/2018
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: 09c719dd03f375127448851d0af9dada9238d1f1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871372"
---
# <a name="quickstart-create-a-linux-server-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="bc280-103">Quickstart: Create a Linux server virtual machine by using PowerShell in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="bc280-103">Quickstart: Create a Linux server virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="bc280-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="bc280-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="bc280-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using Azure Stack PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc280-105">You can create a Ubuntu Server 16.04 LTS virtual machine by using Azure Stack PowerShell.</span></span> <span data-ttu-id="bc280-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-106">Follow the steps in this article to create and use a virtual machine.</span></span>  <span data-ttu-id="bc280-107">This article also gives you the steps to:</span><span class="sxs-lookup"><span data-stu-id="bc280-107">This article also gives you the steps to:</span></span>

* <span data-ttu-id="bc280-108">Connect to the virtual machine with a remote client.</span><span class="sxs-lookup"><span data-stu-id="bc280-108">Connect to the virtual machine with a remote client.</span></span>
* <span data-ttu-id="bc280-109">Install the NGINX web server and view the default home page.</span><span class="sxs-lookup"><span data-stu-id="bc280-109">Install the NGINX web server and view the default home page.</span></span>
* <span data-ttu-id="bc280-110">Clean up unused resources.</span><span class="sxs-lookup"><span data-stu-id="bc280-110">Clean up unused resources.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc280-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bc280-111">Prerequisites</span></span>

* <span data-ttu-id="bc280-112">**A Linux image in the Azure Stack marketplace**</span><span class="sxs-lookup"><span data-stu-id="bc280-112">**A Linux image in the Azure Stack marketplace**</span></span>

   <span data-ttu-id="bc280-113">The Azure Stack marketplace doesn't contain a Linux image by default.</span><span class="sxs-lookup"><span data-stu-id="bc280-113">The Azure Stack marketplace doesn't contain a Linux image by default.</span></span> <span data-ttu-id="bc280-114">Get the Azure Stack operator to provide the **Ubuntu Server 16.04 LTS** image you need.</span><span class="sxs-lookup"><span data-stu-id="bc280-114">Get the Azure Stack operator to provide the **Ubuntu Server 16.04 LTS** image you need.</span></span> <span data-ttu-id="bc280-115">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span><span class="sxs-lookup"><span data-stu-id="bc280-115">The operator can use the steps described in the [Download marketplace items from Azure to Azure Stack](../azure-stack-download-azure-marketplace-item.md) article.</span></span>

* <span data-ttu-id="bc280-116">Azure Stack requires a specific version of Azure PowerShell to create and manage the resources.</span><span class="sxs-lookup"><span data-stu-id="bc280-116">Azure Stack requires a specific version of Azure PowerShell to create and manage the resources.</span></span> <span data-ttu-id="bc280-117">If you don't have PowerShell configured for Azure Stack, follow the steps to [install](azure-stack-powershell-install.md) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bc280-117">If you don't have PowerShell configured for Azure Stack, follow the steps to [install](azure-stack-powershell-install.md) PowerShell.</span></span>

* <span data-ttu-id="bc280-118">With the Azure Stack PowerShell set up, you will need to connect to your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="bc280-118">With the Azure Stack PowerShell set up, you will need to connect to your Azure Stack environment.</span></span> <span data-ttu-id="bc280-119">For instruction, see [Connect to Azure Stack with PowerShell as a user](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="bc280-119">For instruction, see [Connect to Azure Stack with PowerShell as a user](azure-stack-powershell-configure-user.md).</span></span>

* <span data-ttu-id="bc280-120">A public SSH key with the name id_rsa.pub saved in the .ssh directory of your Windows user profile.</span><span class="sxs-lookup"><span data-stu-id="bc280-120">A public SSH key with the name id_rsa.pub saved in the .ssh directory of your Windows user profile.</span></span> <span data-ttu-id="bc280-121">For detailed information about creating SSH keys, see [Creating SSH keys on Windows](../../virtual-machines/linux/ssh-from-windows.md).</span><span class="sxs-lookup"><span data-stu-id="bc280-121">For detailed information about creating SSH keys, see [Creating SSH keys on Windows](../../virtual-machines/linux/ssh-from-windows.md).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="bc280-122">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="bc280-122">Create a resource group</span></span>

<span data-ttu-id="bc280-123">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span><span class="sxs-lookup"><span data-stu-id="bc280-123">A resource group is a logical container where you can deploy and manage Azure Stack resources.</span></span> <span data-ttu-id="bc280-124">From your development kit or the Azure Stack integrated system, run the following code block to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="bc280-124">From your development kit or the Azure Stack integrated system, run the following code block to create a resource group.</span></span> <span data-ttu-id="bc280-125">Values are assigned for all the variables in this document, you can use these values or assign new values.</span><span class="sxs-lookup"><span data-stu-id="bc280-125">Values are assigned for all the variables in this document, you can use these values or assign new values.</span></span>

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="bc280-126">Create storage resources</span><span class="sxs-lookup"><span data-stu-id="bc280-126">Create storage resources</span></span>

<span data-ttu-id="bc280-127">Create a storage account and then create a storage container for the Ubuntu Server 16.04 LTS image.</span><span class="sxs-lookup"><span data-stu-id="bc280-127">Create a storage account and then create a storage container for the Ubuntu Server 16.04 LTS image.</span></span>

```powershell
# Create variables to store the storage account name and the storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob
```

## <a name="create-networking-resources"></a><span data-ttu-id="bc280-128">Create networking resources</span><span class="sxs-lookup"><span data-stu-id="bc280-128">Create networking resources</span></span>

<span data-ttu-id="bc280-129">Create a virtual network, subnet, and a public IP address.</span><span class="sxs-lookup"><span data-stu-id="bc280-129">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="bc280-130">These resources are used to provide network connectivity to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-130">These resources are used to provide network connectivity to the virtual machine.</span></span>

```powershell
# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"

```

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="bc280-131">Create a network security group and a network security group rule</span><span class="sxs-lookup"><span data-stu-id="bc280-131">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="bc280-132">The network security group secures the virtual machine by using inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="bc280-132">The network security group secures the virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="bc280-133">Create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.</span><span class="sxs-lookup"><span data-stu-id="bc280-133">Create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.</span></span>

```powershell
# Create variables to store the network security group and rules names.
$nsgName = "myNetworkSecurityGroup"
$nsgRuleSSHName = "myNetworkSecurityGroupRuleSSH"
$nsgRuleWebName = "myNetworkSecurityGroupRuleWeb"


# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name $nsgRuleSSHName -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name $nsgRuleWebName -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $ResourceGroupName -Location $location `
-Name $nsgName -SecurityRules $nsgRuleSSH,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="bc280-134">Create a network card for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="bc280-134">Create a network card for the virtual machine</span></span>

<span data-ttu-id="bc280-135">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span><span class="sxs-lookup"><span data-stu-id="bc280-135">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-a-virtual-machine"></a><span data-ttu-id="bc280-136">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="bc280-136">Create a virtual machine</span></span>

<span data-ttu-id="bc280-137">Create a virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="bc280-137">Create a virtual machine configuration.</span></span> <span data-ttu-id="bc280-138">This configuration includes the settings used when deploying the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-138">This configuration includes the settings used when deploying the virtual machine.</span></span> <span data-ttu-id="bc280-139">For example: user credentials, size, and the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="bc280-139">For example: user credentials, size, and the virtual machine image.</span></span>

```powershell
# Define a credential object.
$UserName='demouser'
$securePassword = ConvertTo-SecureString ' ' -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ($UserName, $securePassword)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_D1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Linux `
  -ComputerName "MainComputer" `
  -Credential $cred

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "Canonical" `
  -Offer "UbuntuServer" `
  -Skus "16.04-LTS" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets the operating system disk properties on a virtual machine.
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id

# Configure SSH Keys
$sshPublicKey = Get-Content "$env:USERPROFILE\.ssh\id_rsa.pub"

# Adds the SSH Key to the virtual machine
Add-AzureRmVMSshPublicKey -VM $VirtualMachine `
 -KeyData $sshPublicKey `
 -Path "/home/azureuser/.ssh/authorized_keys"

# Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
 -Location $location `
  -VM $VirtualMachine
```

## <a name="quick-create-virtual-machine---full-script"></a><span data-ttu-id="bc280-140">Quick Create virtual machine - Full script</span><span class="sxs-lookup"><span data-stu-id="bc280-140">Quick Create virtual machine - Full script</span></span>

> [!NOTE]
> <span data-ttu-id="bc280-141">It is more or less the code above merged, but with a password rather than SSH key for authentication.</span><span class="sxs-lookup"><span data-stu-id="bc280-141">It is more or less the code above merged, but with a password rather than SSH key for authentication.</span></span>

```powershell
## Create a resource group

<#
A resource group is a logical container where you can deploy and manage Azure Stack resources. From your development kit or the Azure Stack integrated system, run the following code block to create a resource group. Values are assigned for all the variables in this document, you can use these values or assign new values.
#>

# Edit your variables here if required

# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

# Create variables to store the storage account name and the storage account SKU information
$StorageAccountName = "mystorageaccount"
$SkuName = "Standard_LRS"

# Create variables to store the network security group and rules names.
$nsgName = "myNetworkSecurityGroup"
$nsgRuleSSHName = "myNetworkSecurityGroupRuleSSH"
$nsgRuleWebName = "myNetworkSecurityGroupRuleWeb"

# Create variable for virtual machine password
$VMPassword = 'Password123!'

# End of Variables - no need to edit anything past that point to deploy a single VM

# Create Resource Group
New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location

## Create storage resources

# Create a storage account and then create a storage container for the Ubuntu Server 16.04 LTS image.

# Create a new storage account
$StorageAccount = New-AzureRMStorageAccount `
  -Location $location `
  -ResourceGroupName $ResourceGroupName `
  -Type $SkuName `
  -Name $StorageAccountName

Set-AzureRmCurrentStorageAccount `
  -StorageAccountName $storageAccountName `
  -ResourceGroupName $resourceGroupName

# Create a storage container to store the virtual machine image
$containerName = 'osdisks'
$container = New-AzureStorageContainer `
  -Name $containerName `
  -Permission Blob


## Create networking resources

# Create a virtual network, subnet, and a public IP address. These resources are used to provide network connectivity to the virtual machine.

# Create a subnet configuration
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create a virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name MyVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig

# Create a public IP address and specify a DNS name
$pip = New-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -AllocationMethod Static `
  -IdleTimeoutInMinutes 4 `
  -Name "mypublicdns$(Get-Random)"


### Create a network security group and a network security group rule

<#
The network security group secures the virtual machine by using inbound and outbound rules. Create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.
#>

# Create an inbound network security group rule for port 22
$nsgRuleSSH = New-AzureRmNetworkSecurityRuleConfig -Name $nsgRuleSSHName -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 22 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name $nsgRuleWebName -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $ResourceGroupName -Location $location `
-Name $nsgName -SecurityRules $nsgRuleSSH,$nsgRuleWeb

### Create a network card for the virtual machine

# The network card connects the virtual machine to a subnet, network security group, and public IP address.

# Create a virtual network card and associate it with public IP address and NSG
$nic = New-AzureRmNetworkInterface `
  -Name myNic `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -SubnetId $vnet.Subnets[0].Id `
  -PublicIpAddressId $pip.Id `
  -NetworkSecurityGroupId $nsg.Id

## Create a virtual machine
<#
Create a virtual machine configuration. This configuration includes the settings used when deploying the virtual machine. For example: user credentials, size, and the virtual machine image.
#>

# Define a credential object.
$UserName='demouser'
$securePassword = ConvertTo-SecureString $VMPassword -AsPlainText -Force
$cred = New-Object System.Management.Automation.PSCredential ($UserName, $securePassword)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_D1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Linux `
  -ComputerName "MainComputer" `
  -Credential $cred

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "Canonical" `
  -Offer "UbuntuServer" `
  -Skus "16.04-LTS" `
  -Version "latest"

$osDiskName = "OsDisk"
$osDiskUri = '{0}vhds/{1}-{2}.vhd' -f `
  $StorageAccount.PrimaryEndpoints.Blob.ToString(),`
  $vmName.ToLower(), `
  $osDiskName

# Sets the operating system disk properties on a virtual machine.
$VirtualMachine = Set-AzureRmVMOSDisk `
  -VM $VirtualMachine `
  -Name $osDiskName `
  -VhdUri $OsDiskUri `
  -CreateOption FromImage | `
  Add-AzureRmVMNetworkInterface -Id $nic.Id

# Create the virtual machine.
New-AzureRmVM `
  -ResourceGroupName $ResourceGroupName `
 -Location $location `
  -VM $VirtualMachine
```

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="bc280-142">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="bc280-142">Connect to the virtual machine</span></span>

<span data-ttu-id="bc280-143">After the virtual machine is deployed, configure an SSH connection for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-143">After the virtual machine is deployed, configure an SSH connection for the virtual machine.</span></span> <span data-ttu-id="bc280-144">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?view=azurermps-4.3.1) command to return the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-144">Use the [Get-AzureRmPublicIpAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress?view=azurermps-4.3.1) command to return the public IP address of the virtual machine.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="bc280-145">From a client system with SSH installed, use the following command to connect to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-145">From a client system with SSH installed, use the following command to connect to the virtual machine.</span></span> <span data-ttu-id="bc280-146">If you are working on Windows, you can use [Putty](http://www.putty.org/) to create the connection.</span><span class="sxs-lookup"><span data-stu-id="bc280-146">If you are working on Windows, you can use [Putty](http://www.putty.org/) to create the connection.</span></span>

```
ssh <Public IP Address>
```

<span data-ttu-id="bc280-147">When prompted, enter azureuser as the login user.</span><span class="sxs-lookup"><span data-stu-id="bc280-147">When prompted, enter azureuser as the login user.</span></span> <span data-ttu-id="bc280-148">If you used a passphrase when you created the SSH keys, you'll have to provide the passphrase.</span><span class="sxs-lookup"><span data-stu-id="bc280-148">If you used a passphrase when you created the SSH keys, you'll have to provide the passphrase.</span></span>

## <a name="install-the-nginx-web-server"></a><span data-ttu-id="bc280-149">Install the NGINX web server</span><span class="sxs-lookup"><span data-stu-id="bc280-149">Install the NGINX web server</span></span>

<span data-ttu-id="bc280-150">To update package resources and install the latest NGINX package, run the following script:</span><span class="sxs-lookup"><span data-stu-id="bc280-150">To update package resources and install the latest NGINX package, run the following script:</span></span>

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-nginx-welcome-page"></a><span data-ttu-id="bc280-151">View the NGINX welcome page</span><span class="sxs-lookup"><span data-stu-id="bc280-151">View the NGINX welcome page</span></span>

<span data-ttu-id="bc280-152">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span><span class="sxs-lookup"><span data-stu-id="bc280-152">With NGINX installed, and port 80 open on your virtual machine, you can access the web server using the virtual machine's public IP address.</span></span> <span data-ttu-id="bc280-153">Open a web browser, and browse to ```http://<public IP address>```.</span><span class="sxs-lookup"><span data-stu-id="bc280-153">Open a web browser, and browse to ```http://<public IP address>```.</span></span>

![NGINX web server Welcome page](./media/azure-stack-quick-create-vm-linux-cli/nginx.png)

## <a name="clean-up-resources"></a><span data-ttu-id="bc280-155">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="bc280-155">Clean up resources</span></span>

<span data-ttu-id="bc280-156">Clean up the resources that you don't need any longer.</span><span class="sxs-lookup"><span data-stu-id="bc280-156">Clean up the resources that you don't need any longer.</span></span> <span data-ttu-id="bc280-157">You can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup?view=azurermps-4.3.1) command to remove these resources.</span><span class="sxs-lookup"><span data-stu-id="bc280-157">You can use the [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup?view=azurermps-4.3.1) command to remove these resources.</span></span> <span data-ttu-id="bc280-158">To delete the resource group and all its resources, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bc280-158">To delete the resource group and all its resources, run the following command:</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="bc280-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc280-159">Next steps</span></span>

<span data-ttu-id="bc280-160">In this quickstart, you deployed a basic Linux server virtual machine.</span><span class="sxs-lookup"><span data-stu-id="bc280-160">In this quickstart, you deployed a basic Linux server virtual machine.</span></span> <span data-ttu-id="bc280-161">To learn more about Azure Stack virtual machines, go to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="bc280-161">To learn more about Azure Stack virtual machines, go to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
