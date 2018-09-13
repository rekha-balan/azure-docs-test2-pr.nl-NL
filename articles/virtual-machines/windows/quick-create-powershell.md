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
# <a name="create-a-windows-virtual-machine-with-powershell"></a><span data-ttu-id="13c14-103">Create a Windows virtual machine with PowerShell</span><span class="sxs-lookup"><span data-stu-id="13c14-103">Create a Windows virtual machine with PowerShell</span></span>

<span data-ttu-id="13c14-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="13c14-104">The Azure PowerShell module is used to create and manage Azure resources from the PowerShell command line or in scripts.</span></span> <span data-ttu-id="13c14-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="13c14-105">This guide details using PowerShell to create and Azure virtual machine running Windows Server 2016.</span></span>  <span data-ttu-id="13c14-106">Once deployment is complete, we connect to the server and install IIS.</span><span class="sxs-lookup"><span data-stu-id="13c14-106">Once deployment is complete, we connect to the server and install IIS.</span></span>  

<span data-ttu-id="13c14-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="13c14-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/en-us/free/?WT.mc_id=A261C142F) before you begin.</span></span>

<span data-ttu-id="13c14-108">Also, make sure that the latest version of the Azure PowerShell module has been installed.</span><span class="sxs-lookup"><span data-stu-id="13c14-108">Also, make sure that the latest version of the Azure PowerShell module has been installed.</span></span> <span data-ttu-id="13c14-109">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="13c14-109">For more information, see [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="log-in-to-azure"></a><span data-ttu-id="13c14-110">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="13c14-110">Log in to Azure</span></span>

<span data-ttu-id="13c14-111">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span><span class="sxs-lookup"><span data-stu-id="13c14-111">Log in to your Azure subscription with the `Login-AzureRmAccount` command and follow the on-screen directions.</span></span>

```powershell
Login-AzureRmAccount
```

## <a name="create-resource-group"></a><span data-ttu-id="13c14-112">Create resource group</span><span class="sxs-lookup"><span data-stu-id="13c14-112">Create resource group</span></span>

<span data-ttu-id="13c14-113">Create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="13c14-113">Create an Azure resource group.</span></span> <span data-ttu-id="13c14-114">A resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="13c14-114">A resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

```powershell
New-AzureRmResourceGroup -Name myResourceGroup -Location westeurope
```

## <a name="create-networking-resources"></a><span data-ttu-id="13c14-115">Create networking resources</span><span class="sxs-lookup"><span data-stu-id="13c14-115">Create networking resources</span></span>

### <a name="create-a-virtual-network-subnet-and-a-public-ip-address"></a><span data-ttu-id="13c14-116">Create a virtual network, subnet, and a public IP address.</span><span class="sxs-lookup"><span data-stu-id="13c14-116">Create a virtual network, subnet, and a public IP address.</span></span> 
<span data-ttu-id="13c14-117">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span><span class="sxs-lookup"><span data-stu-id="13c14-117">These resources are used to provide network connectivity to the virtual machine and connect it to the internet.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="13c14-118">Create a network security group and a network security group rule.</span><span class="sxs-lookup"><span data-stu-id="13c14-118">Create a network security group and a network security group rule.</span></span> 
<span data-ttu-id="13c14-119">The network security group secures the virtual machine using inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="13c14-119">The network security group secures the virtual machine using inbound and outbound rules.</span></span> <span data-ttu-id="13c14-120">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span><span class="sxs-lookup"><span data-stu-id="13c14-120">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>  <span data-ttu-id="13c14-121">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span><span class="sxs-lookup"><span data-stu-id="13c14-121">We also want to create an inbound rule for port 80, which allows incoming web traffic.</span></span>

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

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="13c14-122">Create a network card for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-122">Create a network card for the virtual machine.</span></span> 
<span data-ttu-id="13c14-123">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span><span class="sxs-lookup"><span data-stu-id="13c14-123">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

```powershell
# Create a virtual network card and associate with public IP address and NSG
$nic = New-AzureRmNetworkInterface -Name myNic -ResourceGroupName myResourceGroup -Location westeurope `
-SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```

## <a name="create-virtual-machine"></a><span data-ttu-id="13c14-124">Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="13c14-124">Create virtual machine</span></span>

<span data-ttu-id="13c14-125">Create a virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="13c14-125">Create a virtual machine configuration.</span></span> <span data-ttu-id="13c14-126">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span><span class="sxs-lookup"><span data-stu-id="13c14-126">This configuration includes the settings that are used when deploying the virtual machine such as a virtual machine image, size, and authentication configuration.</span></span> <span data-ttu-id="13c14-127">When running this step, you are prompted for credentials.</span><span class="sxs-lookup"><span data-stu-id="13c14-127">When running this step, you are prompted for credentials.</span></span> <span data-ttu-id="13c14-128">The values that you enter are configured as the user name and password for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-128">The values that you enter are configured as the user name and password for the virtual machine.</span></span>

```powershell
# Define a credential object
$cred = Get-Credential

# Create a virtual machine configuration
$vmConfig = New-AzureRmVMConfig -VMName myVM -VMSize Standard_DS2 | `
Set-AzureRmVMOperatingSystem -Windows -ComputerName myVM -Credential $cred | `
Set-AzureRmVMSourceImage -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2016-Datacenter -Version latest | `
Add-AzureRmVMNetworkInterface -Id $nic.Id
```

<span data-ttu-id="13c14-129">Create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-129">Create the virtual machine.</span></span>

```powershell
New-AzureRmVM -ResourceGroupName myResourceGroup -Location westeurope -VM $vmConfig
```

## <a name="connect-to-virtual-machine"></a><span data-ttu-id="13c14-130">Connect to virtual machine</span><span class="sxs-lookup"><span data-stu-id="13c14-130">Connect to virtual machine</span></span>

<span data-ttu-id="13c14-131">After the deployment has completed, create a remote desktop connection with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-131">After the deployment has completed, create a remote desktop connection with the virtual machine.</span></span>

<span data-ttu-id="13c14-132">Run the following commands to return the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-132">Run the following commands to return the public IP address of the virtual machine.</span></span>  <span data-ttu-id="13c14-133">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span><span class="sxs-lookup"><span data-stu-id="13c14-133">Take note of this IP Address so you can connect to it with your browser to test web connectivity in a future step.</span></span>

```powershell
Get-AzureRmPublicIpAddress -ResourceGroupName myResourceGroup | Select IpAddress
```

<span data-ttu-id="13c14-134">Use the following command to create a remote desktop session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-134">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="13c14-135">Replace the IP address with the `publicIPAddress` of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-135">Replace the IP address with the `publicIPAddress` of your virtual machine.</span></span> <span data-ttu-id="13c14-136">When prompted, enter the credentials used when creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="13c14-136">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="13c14-137">Install IIS via PowerShell</span><span class="sxs-lookup"><span data-stu-id="13c14-137">Install IIS via PowerShell</span></span>

<span data-ttu-id="13c14-138">Now that you have logged into the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span><span class="sxs-lookup"><span data-stu-id="13c14-138">Now that you have logged into the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span>  <span data-ttu-id="13c14-139">Open a PowerShell prompt and run the following command:</span><span class="sxs-lookup"><span data-stu-id="13c14-139">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="13c14-140">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="13c14-140">View the IIS welcome page</span></span>

<span data-ttu-id="13c14-141">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span><span class="sxs-lookup"><span data-stu-id="13c14-141">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="13c14-142">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="13c14-142">Be sure to use the `publicIpAddress` you documented above to visit the default page.</span></span> 

![IIS default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/quick-create-powershell/default-iis-website.png) 

## <a name="delete-virtual-machine"></a><span data-ttu-id="13c14-144">Delete virtual machine</span><span class="sxs-lookup"><span data-stu-id="13c14-144">Delete virtual machine</span></span>

<span data-ttu-id="13c14-145">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="13c14-145">When no longer needed, the following command can be used to remove the Resource Group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="13c14-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="13c14-146">Next steps</span></span>

[<span data-ttu-id="13c14-147">Install a role and configure firewall tutorial</span><span class="sxs-lookup"><span data-stu-id="13c14-147">Install a role and configure firewall tutorial</span></span>](hero-role.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

[<span data-ttu-id="13c14-148">Explore VM deployment PowerShell samples</span><span class="sxs-lookup"><span data-stu-id="13c14-148">Explore VM deployment PowerShell samples</span></span>](powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
