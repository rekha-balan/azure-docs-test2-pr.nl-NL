---
title: Create a Windows virtual machine by using PowerShell in Azure Stack | Microsoft Docs
description: Create a Windows virtual machine with PowerShell in Azure Stack.
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
ms.date: 09/10/2018
ms.author: mabrigg
ms.custom: mvc
ms.openlocfilehash: 4795de2126a34907ecdec69e87a059dbadd0c3d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869743"
---
# <a name="quickstart-create-a-windows-server-virtual-machine-by-using-powershell-in-azure-stack"></a><span data-ttu-id="22db7-103">Quickstart: create a Windows Server virtual machine by using PowerShell in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="22db7-103">Quickstart: create a Windows Server virtual machine by using PowerShell in Azure Stack</span></span>

<span data-ttu-id="22db7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="22db7-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="22db7-105">You can create a Windows Server 2016 virtual machine by using Azure Stack PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22db7-105">You can create a Windows Server 2016 virtual machine by using Azure Stack PowerShell.</span></span> <span data-ttu-id="22db7-106">Follow the steps in this article to create and use a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-106">Follow the steps in this article to create and use a virtual machine.</span></span> <span data-ttu-id="22db7-107">This article also gives you the steps to:</span><span class="sxs-lookup"><span data-stu-id="22db7-107">This article also gives you the steps to:</span></span>

* <span data-ttu-id="22db7-108">Connect to the virtual machine with a remote client.</span><span class="sxs-lookup"><span data-stu-id="22db7-108">Connect to the virtual machine with a remote client.</span></span>
* <span data-ttu-id="22db7-109">Install the IIS web server and view the default home page.</span><span class="sxs-lookup"><span data-stu-id="22db7-109">Install the IIS web server and view the default home page.</span></span>
* <span data-ttu-id="22db7-110">Clean up your resources.</span><span class="sxs-lookup"><span data-stu-id="22db7-110">Clean up your resources.</span></span>

>[!NOTE]
 <span data-ttu-id="22db7-111">You can run the steps described in this article from the Azure Stack Development Kit, or from a Windows-based external client if you are connected over a VPN.</span><span class="sxs-lookup"><span data-stu-id="22db7-111">You can run the steps described in this article from the Azure Stack Development Kit, or from a Windows-based external client if you are connected over a VPN.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22db7-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="22db7-112">Prerequisites</span></span>

* <span data-ttu-id="22db7-113">Make sure that your Azure Stack operator has added the **Windows Server 2016** image to the Azure Stack marketplace.</span><span class="sxs-lookup"><span data-stu-id="22db7-113">Make sure that your Azure Stack operator has added the **Windows Server 2016** image to the Azure Stack marketplace.</span></span>

* <span data-ttu-id="22db7-114">Azure Stack requires a specific version of Azure PowerShell to create and manage the resources.</span><span class="sxs-lookup"><span data-stu-id="22db7-114">Azure Stack requires a specific version of Azure PowerShell to create and manage the resources.</span></span> <span data-ttu-id="22db7-115">If you don't have PowerShell configured for Azure Stack, follow the steps to [install](azure-stack-powershell-install.md) PowerShell.</span><span class="sxs-lookup"><span data-stu-id="22db7-115">If you don't have PowerShell configured for Azure Stack, follow the steps to [install](azure-stack-powershell-install.md) PowerShell.</span></span>

* <span data-ttu-id="22db7-116">With the Azure Stack PowerShell set up, you will need to connect to your Azure Stack environment.</span><span class="sxs-lookup"><span data-stu-id="22db7-116">With the Azure Stack PowerShell set up, you will need to connect to your Azure Stack environment.</span></span> <span data-ttu-id="22db7-117">For instruction, see [Connect to Azure Stack with PowerShell as a user](azure-stack-powershell-configure-user.md).</span><span class="sxs-lookup"><span data-stu-id="22db7-117">For instruction, see [Connect to Azure Stack with PowerShell as a user](azure-stack-powershell-configure-user.md).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="22db7-118">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="22db7-118">Create a resource group</span></span>

<span data-ttu-id="22db7-119">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="22db7-119">A resource group is a logical container into which Azure Stack resources are deployed and managed.</span></span> <span data-ttu-id="22db7-120">From your development kit or the Azure Stack integrated system, run the following code block to create a resource group.</span><span class="sxs-lookup"><span data-stu-id="22db7-120">From your development kit or the Azure Stack integrated system, run the following code block to create a resource group.</span></span> <span data-ttu-id="22db7-121">Values are assigned for all the variables in this document, you can use these values or assign new values.</span><span class="sxs-lookup"><span data-stu-id="22db7-121">Values are assigned for all the variables in this document, you can use these values or assign new values.</span></span>

```powershell
# Create variables to store the location and resource group names.
$location = "local"
$ResourceGroupName = "myResourceGroup"

New-AzureRmResourceGroup `
  -Name $ResourceGroupName `
  -Location $location
```

## <a name="create-storage-resources"></a><span data-ttu-id="22db7-122">Create storage resources</span><span class="sxs-lookup"><span data-stu-id="22db7-122">Create storage resources</span></span>

<span data-ttu-id="22db7-123">Create a storage account, and a storage container to store the Windows Server 2016 image.</span><span class="sxs-lookup"><span data-stu-id="22db7-123">Create a storage account, and a storage container to store the Windows Server 2016 image.</span></span>

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

## <a name="create-networking-resources"></a><span data-ttu-id="22db7-124">Create networking resources</span><span class="sxs-lookup"><span data-stu-id="22db7-124">Create networking resources</span></span>

<span data-ttu-id="22db7-125">Create a virtual network, subnet, and a public IP address.</span><span class="sxs-lookup"><span data-stu-id="22db7-125">Create a virtual network, subnet, and a public IP address.</span></span> <span data-ttu-id="22db7-126">These resources are used to provide network connectivity to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-126">These resources are used to provide network connectivity to the virtual machine.</span></span>

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

### <a name="create-a-network-security-group-and-a-network-security-group-rule"></a><span data-ttu-id="22db7-127">Create a network security group and a network security group rule</span><span class="sxs-lookup"><span data-stu-id="22db7-127">Create a network security group and a network security group rule</span></span>

<span data-ttu-id="22db7-128">The network security group secures the virtual machine by using inbound and outbound rules.</span><span class="sxs-lookup"><span data-stu-id="22db7-128">The network security group secures the virtual machine by using inbound and outbound rules.</span></span> <span data-ttu-id="22db7-129">Lets create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.</span><span class="sxs-lookup"><span data-stu-id="22db7-129">Lets create an inbound rule for port 3389 to allow incoming Remote Desktop connections and an inbound rule for port 80 to allow incoming web traffic.</span></span>

```powershell
# Create an inbound network security group rule for port 3389
$nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleRDP `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1000 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 3389 `
  -Access Allow

# Create an inbound network security group rule for port 80
$nsgRuleWeb = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRuleWWW `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create a network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName $ResourceGroupName `
  -Location $location `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRuleRDP,$nsgRuleWeb
```

### <a name="create-a-network-card-for-the-virtual-machine"></a><span data-ttu-id="22db7-130">Create a network card for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="22db7-130">Create a network card for the virtual machine</span></span>

<span data-ttu-id="22db7-131">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span><span class="sxs-lookup"><span data-stu-id="22db7-131">The network card connects the virtual machine to a subnet, network security group, and public IP address.</span></span>

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

## <a name="create-a-virtual-machine"></a><span data-ttu-id="22db7-132">Create a virtual machine</span><span class="sxs-lookup"><span data-stu-id="22db7-132">Create a virtual machine</span></span>

<span data-ttu-id="22db7-133">Create a virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="22db7-133">Create a virtual machine configuration.</span></span> <span data-ttu-id="22db7-134">This configuration includes the settings used when deploying the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-134">This configuration includes the settings used when deploying the virtual machine.</span></span> <span data-ttu-id="22db7-135">For example: credentials, size,  and the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="22db7-135">For example: credentials, size,  and the virtual machine image.</span></span>

```powershell
# Define a credential object to store the username and password for the virtual machine
$UserName='demouser'
$Password='Password@123'| ConvertTo-SecureString -Force -AsPlainText
$Credential=New-Object PSCredential($UserName,$Password)

# Create the virtual machine configuration object
$VmName = "VirtualMachinelatest"
$VmSize = "Standard_A1"
$VirtualMachine = New-AzureRmVMConfig `
  -VMName $VmName `
  -VMSize $VmSize

$VirtualMachine = Set-AzureRmVMOperatingSystem `
  -VM $VirtualMachine `
  -Windows `
  -ComputerName "MainComputer" `
  -Credential $Credential

$VirtualMachine = Set-AzureRmVMSourceImage `
  -VM $VirtualMachine `
  -PublisherName "MicrosoftWindowsServer" `
  -Offer "WindowsServer" `
  -Skus "2016-Datacenter" `
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

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="22db7-136">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="22db7-136">Connect to the virtual machine</span></span>

<span data-ttu-id="22db7-137">To remote into the virtual machine that you created in the previous step, you need its public IP address.</span><span class="sxs-lookup"><span data-stu-id="22db7-137">To remote into the virtual machine that you created in the previous step, you need its public IP address.</span></span> <span data-ttu-id="22db7-138">Run the following command to get the public IP address of the virtual machine:</span><span class="sxs-lookup"><span data-stu-id="22db7-138">Run the following command to get the public IP address of the virtual machine:</span></span>

```powershell
Get-AzureRmPublicIpAddress `
  -ResourceGroupName $ResourceGroupName | Select IpAddress
```

<span data-ttu-id="22db7-139">Use the following command to create a Remote Desktop session with the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-139">Use the following command to create a Remote Desktop session with the virtual machine.</span></span> <span data-ttu-id="22db7-140">Replace the IP address with the publicIPAddress of your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-140">Replace the IP address with the publicIPAddress of your virtual machine.</span></span> <span data-ttu-id="22db7-141">When prompted, enter the username and password that you used when creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-141">When prompted, enter the username and password that you used when creating the virtual machine.</span></span>

```powershell
mstsc /v <publicIpAddress>
```

## <a name="install-iis-via-powershell"></a><span data-ttu-id="22db7-142">Install IIS via PowerShell</span><span class="sxs-lookup"><span data-stu-id="22db7-142">Install IIS via PowerShell</span></span>

<span data-ttu-id="22db7-143">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span><span class="sxs-lookup"><span data-stu-id="22db7-143">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="22db7-144">Open a PowerShell prompt and run the following command:</span><span class="sxs-lookup"><span data-stu-id="22db7-144">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="22db7-145">View the IIS welcome page</span><span class="sxs-lookup"><span data-stu-id="22db7-145">View the IIS welcome page</span></span>

<span data-ttu-id="22db7-146">With IIS installed, and with port 80 open on your VM, you can use a web browser of your choice to view the default IIS welcome page.</span><span class="sxs-lookup"><span data-stu-id="22db7-146">With IIS installed, and with port 80 open on your VM, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="22db7-147">Use the *publicIpAddress* you documented in the previous section to visit the default page.</span><span class="sxs-lookup"><span data-stu-id="22db7-147">Use the *publicIpAddress* you documented in the previous section to visit the default page.</span></span>

![IIS default site](./media/azure-stack-quick-create-vm-windows-powershell/default-iis-website.png)

## <a name="delete-the-virtual-machine"></a><span data-ttu-id="22db7-149">Delete the virtual machine</span><span class="sxs-lookup"><span data-stu-id="22db7-149">Delete the virtual machine</span></span>

<span data-ttu-id="22db7-150">When no longer needed, use the following command to remove the resource group that contains the virtual machine and its related resources:</span><span class="sxs-lookup"><span data-stu-id="22db7-150">When no longer needed, use the following command to remove the resource group that contains the virtual machine and its related resources:</span></span>

```powershell
Remove-AzureRmResourceGroup `
  -Name $ResourceGroupName
```

## <a name="next-steps"></a><span data-ttu-id="22db7-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="22db7-151">Next steps</span></span>

<span data-ttu-id="22db7-152">In this quickstart, you’ve deployed a simple Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="22db7-152">In this quickstart, you’ve deployed a simple Windows virtual machine.</span></span> <span data-ttu-id="22db7-153">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span><span class="sxs-lookup"><span data-stu-id="22db7-153">To learn more about Azure Stack virtual machines, continue to [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md).</span></span>
