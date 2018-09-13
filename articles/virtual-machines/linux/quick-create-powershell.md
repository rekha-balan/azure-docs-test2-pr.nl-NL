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
# <a name="create-a-linux-virtual-machine-with-powershell"></a>Create a Linux virtual machine with PowerShell

The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts. This guide details using PowerShell to create and Azure virtual machine running Ubuntu 14.04 LTS.

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.

Also, make sure that the latest version of the Azure PowerShell module has been installed. For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).

Finally, a public SSH key with the name `id_rsa.pub` needs to be stored in the `.ssh` directory of your Windows user profile. For detailed information on creating SSH keys for Azure, see [Create SSH keys for Azure](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="log-in-to-azure"></a>Log in to Azure

Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a>Create resource group

Create an Azure resource group. A resource group is a logical container into which Azure resources are deployed and managed. 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location westeurope
```

## <a name="create-networking-resources"></a>Create networking resources

Create a virtual network, subnet, and a public IP address. These resources are used to provide network connectivity to the virtual machine and connect it to the internet.

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

Create a network security group and a network security group rule. The network security group secures the virtual machine using inbound and outbound rules. In this case, an inbound rule is created for port 22, which allows incoming SSH connections. We also want to create an inbound rule for port 80, which allows incoming web traffic.

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

Create a network card for the virtual machine. The network card connects the virtual machine to a subnet, network security group, and public IP address.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location westeurope `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

Create a virtual machine configuration. This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.

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

Create the virtual machine.

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a>Connect to virtual machine

After the deployment has completed, create an SSH connection with the virtual machine.

Run the following commands to return the public IP address of the virtual machine.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

From a system with SSH installed, used the following command to connect to the virtual machine. If working on Windows, [Putty](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-linux-ssh-from-windows?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#create-a-private-key-for-putty) can be used to create the connection. 

```bash 
ssh <Public IP Address>
```

When prompted, the login user name is `azureuser`. If a passphrase was entered when creating SSH keys, you will need to enter this as well.


## <a name="install-nginx"></a>Install NGINX

Use the following bash script to update package sources and install the latest NGINX package. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-the-ngix-welcome-page"></a>View the NGIX welcome page

With NGINX installed and port 80 now open on your VM from the Internet - you can use a web browser of your choice to view the default NGINX welcome page. Be sure to use the `publicIpAddress` you documented above to visit the default page. 

![NGINX default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/quick-create-cli/nginx.png) 
## <a name="delete-virtual-machine"></a>Delete virtual machine

When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Next steps

[Create highly available virtual machines tutorial](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Explore VM deployment PowerShell samples](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

