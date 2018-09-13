---
title: Azure Quick Start - Create Windows VM PowerShell | Microsoft Docs
description: Quickly learn to create a Windows virtual machines with PowerShell
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 04/03/2017
ms.author: nepeters
ms.openlocfilehash: 754c8ab262feec23c1291b43c18d234077a39d93
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551499"
---
# <a name="create-a-windows-virtual-machine-with-powershell"></a>Create a Windows virtual machine with PowerShell

The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts. This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.  Once deployment is complete, we connect to the server and install IIS.  

If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.

Also, make sure that the latest version of the Azure PowerShell module has been installed. For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).

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

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a>Create a virtual network, subnet, and a public IP address. 
These resources are used to provide network connectivity to the virtual machine and connect it to the internet.

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a>Create a network security group and a network security group rule. 
The network security group secures the virtual machine using inbound and outbound rules. In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.  We also want to create an inbound rule for port 80, which allows incoming web traffic.

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleRDP  -Protocol Tcp `
-Direction Inbound -Priority 1000 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 3389 -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig -Name myNetworkSecurityGroupRuleWWW  -Protocol Tcp `
-Direction Inbound -Priority 1001 -SourceAddressPrefix * -SourcePortRange * -DestinationAddressPrefix * `
-DestinationPortRange 80 -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName myResourceGroup -Location westeurope `
-Name myNetworkSecurityGroup -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a>Create a network card for the virtual machine. 
The network card connects the virtual machine to a subnet, network security group, and public IP address.

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location westeurope `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a>Create virtual machine

Create a virtual machine configuration. This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration. When running this step, you are prompted for credentials. The values that you enter are configured as the user name and password for the virtual machine.

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id
```

Create the virtual machine.

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a>Connect to virtual machine

After the deployment has completed, create a remote desktop connection with the virtual machine.

Run the following commands to return the public IP address of the virtual machine.  Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

Use the following command to create a remote desktop session with the virtual machine. Replace the IP address with the `publicIPAddress` of your virtual machine. When prompted, enter the credentials used when creating the virtual machine.

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a>Install IIS via PowerShell

Now that you have logged into the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.  Open a PowerShell prompt and run the following command:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a>View the IIS welcome page

With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page. Be sure to use the `publicIpAddress` you documented above to visit the default page. 

![IIS default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-powershell/default-iis-website.png) 

## <a name="delete-virtual-machine"></a>Delete virtual machine

When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a>Next steps

[Install a role and configure firewall tutorial](hero-role.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[Explore VM deployment PowerShell samples](powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
