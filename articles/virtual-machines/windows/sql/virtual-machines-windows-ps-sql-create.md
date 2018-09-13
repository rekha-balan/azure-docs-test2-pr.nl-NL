---
title: Create a SQL Server Virtual Machine in Azure PowerShell (Resource Manager) | Microsoft Docs
description: Provides steps and PowerShell scripts for creating an Azure VM with SQL Server virtual machine gallery images.
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: ''
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 218d7dcf14ebbb28ac043e50e6f9248ecb942aaa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552975"
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="70eca-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="70eca-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [Portal](virtual-machines-windows-portal-sql-server-provision.md)
> * [PowerShell](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="70eca-106">Overview</span><span class="sxs-lookup"><span data-stu-id="70eca-106">Overview</span></span>
<span data-ttu-id="70eca-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="70eca-107">This tutorial shows you how to create a single Azure virtual machine using the **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="70eca-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span><span class="sxs-lookup"><span data-stu-id="70eca-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in the SQL Gallery.</span></span> <span data-ttu-id="70eca-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-109">We will create new providers for the storage, network, and compute resources that will be used by the virtual machine.</span></span> <span data-ttu-id="70eca-110">If you have existing providers for any of these resources, you can use those providers instead.</span><span class="sxs-lookup"><span data-stu-id="70eca-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="70eca-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-111">If you need the classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70eca-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="70eca-112">Prerequisites</span></span>
<span data-ttu-id="70eca-113">For this tutorial you'll need:</span><span class="sxs-lookup"><span data-stu-id="70eca-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="70eca-114">An Azure account and subscription before you start.</span><span class="sxs-lookup"><span data-stu-id="70eca-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="70eca-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="70eca-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="70eca-116">[Azure PowerShell)](/powershell/azureps-cmdlets-docs), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span><span class="sxs-lookup"><span data-stu-id="70eca-116">[Azure PowerShell)](/powershell/azureps-cmdlets-docs), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="70eca-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span><span class="sxs-lookup"><span data-stu-id="70eca-117">To retrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="70eca-118">Configure your subscription</span><span class="sxs-lookup"><span data-stu-id="70eca-118">Configure your subscription</span></span>
<span data-ttu-id="70eca-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70eca-119">Open Windows PowerShell and establish access to your Azure account by running the following cmdlet.</span></span> <span data-ttu-id="70eca-120">You will be presented with a sign in screen to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="70eca-120">You will be presented with a sign in screen to enter your credentials.</span></span> <span data-ttu-id="70eca-121">Use the same email and password that you use to sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="70eca-121">Use the same email and password that you use to sign in to the Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="70eca-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span><span class="sxs-lookup"><span data-stu-id="70eca-122">After successfully signing in you will see some information on screen that includes the SubscriptionId with which you signed in.</span></span> <span data-ttu-id="70eca-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span><span class="sxs-lookup"><span data-stu-id="70eca-123">This is the subscription in which the resources for this tutorial will be created unless you change to a different subscription.</span></span> <span data-ttu-id="70eca-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span><span class="sxs-lookup"><span data-stu-id="70eca-124">If you have multiple SubscriptionIds, run the following cmdlet to return a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="70eca-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span><span class="sxs-lookup"><span data-stu-id="70eca-125">To change to another SubscriptionID, run the following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="70eca-126">Define image variables</span><span class="sxs-lookup"><span data-stu-id="70eca-126">Define image variables</span></span>
<span data-ttu-id="70eca-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-127">To simplify usability and understanding of the completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="70eca-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span><span class="sxs-lookup"><span data-stu-id="70eca-128">Change the parameter values as you see fit, but beware of naming restrictions related to name lengths and special characters when modifying the values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="70eca-129">Location and Resource Group</span><span class="sxs-lookup"><span data-stu-id="70eca-129">Location and Resource Group</span></span>
<span data-ttu-id="70eca-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-130">Use two variables to define the data region and the resource group into which you will create the other resources for the virtual machine.</span></span>

<span data-ttu-id="70eca-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-131">Modify as desired and then execute the following cmdlets to initialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="70eca-132">Storage properties</span><span class="sxs-lookup"><span data-stu-id="70eca-132">Storage properties</span></span>
<span data-ttu-id="70eca-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-133">Use the following variables to define the storage account and the type of storage to be used by the virtual machine.</span></span>

<span data-ttu-id="70eca-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-134">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span> <span data-ttu-id="70eca-135">Note that in this example, we are using [Premium Storage](../../../storage/storage-premium-storage.md), which is recommended for production workloads.</span><span class="sxs-lookup"><span data-stu-id="70eca-135">Note that in this example, we are using [Premium Storage](../../../storage/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="70eca-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="70eca-137">Network properties</span><span class="sxs-lookup"><span data-stu-id="70eca-137">Network properties</span></span>
<span data-ttu-id="70eca-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-138">Use the following variables to define the network interface, the TCP/IP allocation method, the virtual network name, the virtual subnet name, the range of IP addresses for the virtual network, the range of IP addresses for the subnet, and the public domain name label to be used by the network in the virtual machine.</span></span>

<span data-ttu-id="70eca-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-139">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="70eca-140">Virtual machine properties</span><span class="sxs-lookup"><span data-stu-id="70eca-140">Virtual machine properties</span></span>
<span data-ttu-id="70eca-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-141">Use the following variables to define the virtual machine name, the computer name, the virtual machine size, and the operating system disk name for the virtual machine.</span></span>

<span data-ttu-id="70eca-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-142">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="70eca-143">Image properties</span><span class="sxs-lookup"><span data-stu-id="70eca-143">Image properties</span></span>
<span data-ttu-id="70eca-144">Use the following variables to define the image to use for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-144">Use the following variables to define the image to use for the virtual machine.</span></span> <span data-ttu-id="70eca-145">In this example, the SQL Server 2016 Enterprise image is used.</span><span class="sxs-lookup"><span data-stu-id="70eca-145">In this example, the SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="70eca-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span><span class="sxs-lookup"><span data-stu-id="70eca-146">Modify as desired and then execute the following cmdlet to initialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="70eca-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span><span class="sxs-lookup"><span data-stu-id="70eca-147">Note that you can get a full list of SQL Server image offerings with the Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="70eca-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span><span class="sxs-lookup"><span data-stu-id="70eca-148">And you can see the Skus available for an offering with the Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="70eca-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span><span class="sxs-lookup"><span data-stu-id="70eca-149">The following command shows all Skus available for the **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="70eca-150">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="70eca-150">Create a resource group</span></span>
<span data-ttu-id="70eca-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span><span class="sxs-lookup"><span data-stu-id="70eca-151">With the Resource Manager deployment model, the first object that you create is the resource group.</span></span> <span data-ttu-id="70eca-152">We will use the [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt759837.aspx) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-152">We will use the [New-AzureRmResourceGroup](https://msdn.microsoft.com/library/mt759837.aspx) cmdlet to create an Azure resource group and its resources with the resource group name and location defined by the variables that you previously initialized.</span></span>

<span data-ttu-id="70eca-153">Execute the following cmdlet to create your new resource group.</span><span class="sxs-lookup"><span data-stu-id="70eca-153">Execute the following cmdlet to create your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="70eca-154">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="70eca-154">Create a storage account</span></span>
<span data-ttu-id="70eca-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span><span class="sxs-lookup"><span data-stu-id="70eca-155">The virtual machine requires storage resources for the operating system disk and for the SQL Server data and log files.</span></span> <span data-ttu-id="70eca-156">For simplicity, we will create a single disk for both.</span><span class="sxs-lookup"><span data-stu-id="70eca-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="70eca-157">You can attach additional disks later using the [Add-Azure Disk](https://msdn.microsoft.com/library/azure/dn495252.aspx) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span><span class="sxs-lookup"><span data-stu-id="70eca-157">You can attach additional disks later using the [Add-Azure Disk](https://msdn.microsoft.com/library/azure/dn495252.aspx) cmdlet in order to place your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="70eca-158">We will use the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-158">We will use the [New-AzureRmStorageAccount](https://msdn.microsoft.com/library/mt607148.aspx) cmdlet to create a standard storage account in your new resource group and with the storage account name, storage Sku name, and location defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="70eca-159">Execute the following cmdlet to create your new storage account.</span><span class="sxs-lookup"><span data-stu-id="70eca-159">Execute the following cmdlet to create your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="70eca-160">Create network resources</span><span class="sxs-lookup"><span data-stu-id="70eca-160">Create network resources</span></span>
<span data-ttu-id="70eca-161">The virtual machine requires a number of network resources for network connectivity.</span><span class="sxs-lookup"><span data-stu-id="70eca-161">The virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="70eca-162">Each virtual machine requires a virtual network.</span><span class="sxs-lookup"><span data-stu-id="70eca-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="70eca-163">A virtual network must have at least one subnet defined.</span><span class="sxs-lookup"><span data-stu-id="70eca-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="70eca-164">A network interface must be defined with either a public or a private IP address.</span><span class="sxs-lookup"><span data-stu-id="70eca-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="70eca-165">Create a virtual network subnet configuration</span><span class="sxs-lookup"><span data-stu-id="70eca-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="70eca-166">We will start by creating a subnet configuration for our virtual network.</span><span class="sxs-lookup"><span data-stu-id="70eca-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="70eca-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](https://msdn.microsoft.com/library/mt619412.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70eca-167">For our tutorial, we will create a default subnet using the [New-AzureRmVirtualNetworkSubnetConfig](https://msdn.microsoft.com/library/mt619412.aspx) cmdlet.</span></span> <span data-ttu-id="70eca-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-168">We will create our virtual network subnet configuration with the subnet name and address prefix defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> You can define additional properties of the virtual network subnet configuration using this cmdlet, but that is beyond the scope of this tutorial.
>
>

<span data-ttu-id="70eca-170">Execute the following cmdlet to create your virtual subnet configuration.</span><span class="sxs-lookup"><span data-stu-id="70eca-170">Execute the following cmdlet to create your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="70eca-171">Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="70eca-171">Create a virtual network</span></span>
<span data-ttu-id="70eca-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70eca-172">Next, we will create our virtual network using the [New-AzureRmVirtualNetwork](https://msdn.microsoft.com/library/mt603657.aspx) cmdlet.</span></span> <span data-ttu-id="70eca-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span><span class="sxs-lookup"><span data-stu-id="70eca-173">We will create our virtual network in your new resource group, with the name, location, and address prefix defined using the variables that you previously initialized, and using the subnet configuration that you defined in the previous step.</span></span>

<span data-ttu-id="70eca-174">Execute the following cmdlet to create your virtual network.</span><span class="sxs-lookup"><span data-stu-id="70eca-174">Execute the following cmdlet to create your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-the-public-ip-address"></a><span data-ttu-id="70eca-175">Create the public IP address</span><span class="sxs-lookup"><span data-stu-id="70eca-175">Create the public IP address</span></span>
<span data-ttu-id="70eca-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-176">Now that we have our virtual network defined, we need to configure an IP address for connectivity to the virtual machine.</span></span> <span data-ttu-id="70eca-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span><span class="sxs-lookup"><span data-stu-id="70eca-177">For this tutorial, we will create a public IP address using dynamic IP addressing to support Internet connectivity.</span></span> <span data-ttu-id="70eca-178">We will use the [New-AzureRmPublicIpAddress](https://msdn.microsoft.com/library/mt603620.aspx) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-178">We will use the [New-AzureRmPublicIpAddress](https://msdn.microsoft.com/library/mt603620.aspx) cmdlet to create the public IP address in the resource group created prevously and with the name, location, allocation method, and DNS domain name label defined using the variables that you previously initialized.</span></span>

> [!NOTE]
> You can define additional properties of the public IP address using this cmdlet, but that is beyond the scope of this initial tutorial. You could also create a private address or an address with a static address, but that is also beyond the scope of this tutorial.
>
>

<span data-ttu-id="70eca-181">Execute the following cmdlet to create your public IP address.</span><span class="sxs-lookup"><span data-stu-id="70eca-181">Execute the following cmdlet to create your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-the-network-interface"></a><span data-ttu-id="70eca-182">Create the network interface</span><span class="sxs-lookup"><span data-stu-id="70eca-182">Create the network interface</span></span>
<span data-ttu-id="70eca-183">We are now ready to create the network interface that our virtual machine will use.</span><span class="sxs-lookup"><span data-stu-id="70eca-183">We are now ready to create the network interface that our virtual machine will use.</span></span> <span data-ttu-id="70eca-184">We will use the [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span><span class="sxs-lookup"><span data-stu-id="70eca-184">We will use the [New-AzureRmNetworkInterface](https://msdn.microsoft.com/library/mt619370.aspx) cmdlet to create our network interface in the resource group created earlier and with the name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="70eca-185">Execute the following cmdlet to create your network interface.</span><span class="sxs-lookup"><span data-stu-id="70eca-185">Execute the following cmdlet to create your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="70eca-186">Configure a VM object</span><span class="sxs-lookup"><span data-stu-id="70eca-186">Configure a VM object</span></span>
<span data-ttu-id="70eca-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-187">Now that we have storage and network resources defined, we are ready to define compute resources for the virtual machine.</span></span> <span data-ttu-id="70eca-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span><span class="sxs-lookup"><span data-stu-id="70eca-188">For our tutorial, we will specify the virtual machine size and various operating system properties, specify the network interface that we previously created, define blob storage, and then specify the operating system disk.</span></span>

### <a name="create-the-vm-object"></a><span data-ttu-id="70eca-189">Create the VM object</span><span class="sxs-lookup"><span data-stu-id="70eca-189">Create the VM object</span></span>
<span data-ttu-id="70eca-190">We will start by specifying the virtual machine size.</span><span class="sxs-lookup"><span data-stu-id="70eca-190">We will start by specifying the virtual machine size.</span></span> <span data-ttu-id="70eca-191">For this tutorial, we are specifying a DS13.</span><span class="sxs-lookup"><span data-stu-id="70eca-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="70eca-192">We will use the [New-AzureRmVMConfig](https://msdn.microsoft.com/library/mt603727.aspx) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-192">We will use the [New-AzureRmVMConfig](https://msdn.microsoft.com/library/mt603727.aspx) cmdlet to create a configurable virtual machine object with the name and size defined using the variables that you previously initialized.</span></span>

<span data-ttu-id="70eca-193">Execute the following cmdlet to create the virtual machine object.</span><span class="sxs-lookup"><span data-stu-id="70eca-193">Execute the following cmdlet to create the virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-to-hold-the-name-and-password-for-the-local-administrator-credentials"></a><span data-ttu-id="70eca-194">Create a credential object to hold the name and password for the local administrator credentials</span><span class="sxs-lookup"><span data-stu-id="70eca-194">Create a credential object to hold the name and password for the local administrator credentials</span></span>
<span data-ttu-id="70eca-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span><span class="sxs-lookup"><span data-stu-id="70eca-195">Before we can set the operating system properties for the virtual machine, we need to supply the credentials for the local administrator account as a secure string.</span></span> <span data-ttu-id="70eca-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="70eca-196">To accomplish this, we will use the [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="70eca-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-197">Execute the following cmdlet and, in the Windows PowerShell credential request window, type the name and password to use for the local administrator account in the Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."

### <a name="set-the-operating-system-properties-for-the-virtual-machine"></a><span data-ttu-id="70eca-198">Set the operating system properties for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70eca-198">Set the operating system properties for the virtual machine</span></span>
<span data-ttu-id="70eca-199">Now we are ready to set the virtual machine's operating system properties.</span><span class="sxs-lookup"><span data-stu-id="70eca-199">Now we are ready to set the virtual machine's operating system properties.</span></span> <span data-ttu-id="70eca-200">We will use the [Set-AzureRmVMOperatingSystem](https://msdn.microsoft.com/library/mt603843.aspx) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span><span class="sxs-lookup"><span data-stu-id="70eca-200">We will use the [Set-AzureRmVMOperatingSystem](https://msdn.microsoft.com/library/mt603843.aspx) cmdlet to set the type of operating system as Windows, require the [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) to be installed, specify that the cmdlet enables auto update and set the virtual machine name, the computer name, and the credential using the variables that you previously initialized.</span></span>

<span data-ttu-id="70eca-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-201">Execute the following cmdlet to set the operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-the-network-interface-to-the-virtual-machine"></a><span data-ttu-id="70eca-202">Add the network interface to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70eca-202">Add the network interface to the virtual machine</span></span>
<span data-ttu-id="70eca-203">Next, we will add the network interface that we created previously to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-203">Next, we will add the network interface that we created previously to the virtual machine.</span></span> <span data-ttu-id="70eca-204">We will use the [Add-AzureRmVMNetworkInterface](https://msdn.microsoft.com/library/mt619351.aspx) cmdlet to add the network interface using the network interface variable that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="70eca-204">We will use the [Add-AzureRmVMNetworkInterface](https://msdn.microsoft.com/library/mt619351.aspx) cmdlet to add the network interface using the network interface variable that you defined earlier.</span></span>

<span data-ttu-id="70eca-205">Execute the following cmdlet to set the network interface for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-205">Execute the following cmdlet to set the network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-the-blob-storage-location-for-the-disk-to-be-used-by-the-virtual-machine"></a><span data-ttu-id="70eca-206">Set the blob storage location for the disk to be used by the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70eca-206">Set the blob storage location for the disk to be used by the virtual machine</span></span>
<span data-ttu-id="70eca-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="70eca-207">Next, we will set the blob storage location for the disk to be used by the virtual machine using the variables that you defined earlier.</span></span>

<span data-ttu-id="70eca-208">Execute the following cmdlet to set the blob storage location.</span><span class="sxs-lookup"><span data-stu-id="70eca-208">Execute the following cmdlet to set the blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-the-operating-system-disk-properties-for-the-virtual-machine"></a><span data-ttu-id="70eca-209">Set the operating system disk properties for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70eca-209">Set the operating system disk properties for the virtual machine</span></span>
<span data-ttu-id="70eca-210">Next, we will set the operating system disk properties for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-210">Next, we will set the operating system disk properties for the virtual machine.</span></span> <span data-ttu-id="70eca-211">We will use the [Set-AzureRmVMOSDisk](https://msdn.microsoft.com/library/mt603746.aspx) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span><span class="sxs-lookup"><span data-stu-id="70eca-211">We will use the [Set-AzureRmVMOSDisk](https://msdn.microsoft.com/library/mt603746.aspx) cmdlet to specify that the operating system for the virtual machine will come from an image, to set caching to read only (because SQL Server is being installed on the same disk) and define the virtual machine name and the operating system disk defined using the variables that we defined earlier.</span></span>

<span data-ttu-id="70eca-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-212">Execute the following cmdlet to set the operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-the-platform-image-for-the-virtual-machine"></a><span data-ttu-id="70eca-213">Specify the platform image for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="70eca-213">Specify the platform image for the virtual machine</span></span>
<span data-ttu-id="70eca-214">Our last configuration step is to specify the platform image for our virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-214">Our last configuration step is to specify the platform image for our virtual machine.</span></span> <span data-ttu-id="70eca-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span><span class="sxs-lookup"><span data-stu-id="70eca-215">For our tutorial, we are using the latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="70eca-216">We will use the [Set-AzureRmVMSourceImage](https://msdn.microsoft.com/library/mt619344.aspx) cmdlet to use this image as defined by the variables that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="70eca-216">We will use the [Set-AzureRmVMSourceImage](https://msdn.microsoft.com/library/mt619344.aspx) cmdlet to use this image as defined by the variables that you defined earlier.</span></span>

<span data-ttu-id="70eca-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-217">Execute the following cmdlet to specify the platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-the-sql-vm"></a><span data-ttu-id="70eca-218">Create the SQL VM</span><span class="sxs-lookup"><span data-stu-id="70eca-218">Create the SQL VM</span></span>
<span data-ttu-id="70eca-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-219">Now that you have finished the configuration steps, you are ready to create the virtual machine.</span></span> <span data-ttu-id="70eca-220">We will use the [New-AzureRmVM](https://msdn.microsoft.com/library/mt603754.aspx) cmdlet to create the virtual machine using the variables that we have defined.</span><span class="sxs-lookup"><span data-stu-id="70eca-220">We will use the [New-AzureRmVM](https://msdn.microsoft.com/library/mt603754.aspx) cmdlet to create the virtual machine using the variables that we have defined.</span></span>

<span data-ttu-id="70eca-221">Execute the following cmdlet to create your virtual machine.</span><span class="sxs-lookup"><span data-stu-id="70eca-221">Execute the following cmdlet to create your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="70eca-222">The virtual machine is created.</span><span class="sxs-lookup"><span data-stu-id="70eca-222">The virtual machine is created.</span></span> <span data-ttu-id="70eca-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span><span class="sxs-lookup"><span data-stu-id="70eca-223">Notice that a standard storage account is created for boot diagnostics because the specified storage account for the virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="70eca-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-224">You can now view this machine in the Azure Portal to see [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="70eca-225">Example script</span><span class="sxs-lookup"><span data-stu-id="70eca-225">Example script</span></span>
<span data-ttu-id="70eca-226">The following script contains the complete PowerShell script for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="70eca-226">The following script contains the complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="70eca-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span><span class="sxs-lookup"><span data-stu-id="70eca-227">It assumes that you have already setup the Azure subscription to use with the **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type the name and password of the local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create the VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="70eca-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="70eca-228">Next steps</span></span>
<span data-ttu-id="70eca-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span><span class="sxs-lookup"><span data-stu-id="70eca-229">After the virtual machine is created, you are ready to connect to the virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="70eca-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span><span class="sxs-lookup"><span data-stu-id="70eca-230">For more information, see [Connect to a SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

