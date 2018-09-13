---
title: 'Connect your on-premises network to an Azure virtual network: Site-to-Site VPN: PowerShell | Microsoft Docs'
description: Steps to create an IPsec connection from your on-premises network to an Azure virtual network over the public Internet. These steps will help you create a cross-premises Site-to-Site VPN Gateway connection using PowerShell.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: fcc2fda5-4493-4c15-9436-84d35adbda8e
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/11/2017
ms.author: cherylmc
ms.openlocfilehash: 8108c2a18bcbf698bd59a4280fb9b5ab8a19342a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552996"
---
# <a name="create-a-vnet-with-a-site-to-site-vpn-connection-using-powershell"></a><span data-ttu-id="87a7e-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="87a7e-104">Create a VNet with a Site-to-Site VPN connection using PowerShell</span></span>

<span data-ttu-id="87a7e-105">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="87a7e-105">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="87a7e-106">This type of connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="87a7e-106">This type of connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT.</span></span> <span data-ttu-id="87a7e-107">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span><span class="sxs-lookup"><span data-stu-id="87a7e-107">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span></span>

![Site-to-Site VPN Gateway cross-premises connection diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-create-site-to-site-rm-powershell/site-to-site-connection-diagram.png)

<span data-ttu-id="87a7e-109">This article walks you through creating a virtual network and a Site-to-Site VPN gateway connection to your on-premises network using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="87a7e-109">This article walks you through creating a virtual network and a Site-to-Site VPN gateway connection to your on-premises network using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="87a7e-110">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span><span class="sxs-lookup"><span data-stu-id="87a7e-110">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span></span> <span data-ttu-id="87a7e-111">You can also create this configuration by using different deployment tools, or for the classic deployment model, by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="87a7e-111">You can also create this configuration by using different deployment tools, or for the classic deployment model, by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Classic - Azure portal](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Classic - classic portal](vpn-gateway-site-to-site-create.md)
>
>

#### <a name="additional-configurations"></a><span data-ttu-id="87a7e-116">Additional configurations</span><span class="sxs-lookup"><span data-stu-id="87a7e-116">Additional configurations</span></span>
<span data-ttu-id="87a7e-117">If you want to connect VNets together, but are not creating a connection to an on-premises location, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-117">If you want to connect VNets together, but are not creating a connection to an on-premises location, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="87a7e-118">If you want to add a Site-to-Site connection to a VNet that already has a connection, see [Add a S2S connection to a VNet with an existing VPN gateway connection](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-118">If you want to add a Site-to-Site connection to a VNet that already has a connection, see [Add a S2S connection to a VNet with an existing VPN gateway connection](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="87a7e-119">Before you begin</span><span class="sxs-lookup"><span data-stu-id="87a7e-119">Before you begin</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)]

<span data-ttu-id="87a7e-120">Verify that you have the following items before beginning configuration:</span><span class="sxs-lookup"><span data-stu-id="87a7e-120">Verify that you have the following items before beginning configuration:</span></span>

* <span data-ttu-id="87a7e-121">A compatible VPN device and someone who is able to configure it.</span><span class="sxs-lookup"><span data-stu-id="87a7e-121">A compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="87a7e-122">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-122">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="87a7e-123">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span><span class="sxs-lookup"><span data-stu-id="87a7e-123">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="87a7e-124">An externally facing public IP address for your VPN device.</span><span class="sxs-lookup"><span data-stu-id="87a7e-124">An externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="87a7e-125">This IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="87a7e-125">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="87a7e-126">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="87a7e-126">An Azure subscription.</span></span> <span data-ttu-id="87a7e-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="87a7e-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="87a7e-128">The latest version of the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87a7e-128">The latest version of the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="87a7e-129">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87a7e-129">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

## <a name="Login"></a><span data-ttu-id="87a7e-130">1. Connect to your subscription</span><span class="sxs-lookup"><span data-stu-id="87a7e-130">1. Connect to your subscription</span></span>
<span data-ttu-id="87a7e-131">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="87a7e-131">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="87a7e-132">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-132">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="87a7e-133">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="87a7e-133">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="87a7e-134">Use the following sample to help you connect:</span><span class="sxs-lookup"><span data-stu-id="87a7e-134">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
```

<span data-ttu-id="87a7e-135">Check the subscriptions for the account.</span><span class="sxs-lookup"><span data-stu-id="87a7e-135">Check the subscriptions for the account.</span></span>

```powershell
Get-AzureRmSubscription
```

<span data-ttu-id="87a7e-136">Specify the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="87a7e-136">Specify the subscription that you want to use.</span></span>

```powershell
Select-AzureRmSubscription -SubscriptionName "Replace_with_your_subscription_name"
```

## <a name="VNet"></a><span data-ttu-id="87a7e-137">2. Create a virtual network and a gateway subnet</span><span class="sxs-lookup"><span data-stu-id="87a7e-137">2. Create a virtual network and a gateway subnet</span></span>
<span data-ttu-id="87a7e-138">The examples use a gateway subnet of /28.</span><span class="sxs-lookup"><span data-stu-id="87a7e-138">The examples use a gateway subnet of /28.</span></span> <span data-ttu-id="87a7e-139">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span><span class="sxs-lookup"><span data-stu-id="87a7e-139">While it is possible to create a gateway subnet as small as /29, we recommend that you create a larger subnet that includes more addresses by selecting at least /28 or /27.</span></span> <span data-ttu-id="87a7e-140">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span><span class="sxs-lookup"><span data-stu-id="87a7e-140">This will allow for enough addresses to accommodate possible additional configurations that you may want in the future.</span></span>

<span data-ttu-id="87a7e-141">If you already have a virtual network with a gateway subnet that is /29 or larger, you can jump ahead to [Add your local network gateway](#localnet).</span><span class="sxs-lookup"><span data-stu-id="87a7e-141">If you already have a virtual network with a gateway subnet that is /29 or larger, you can jump ahead to [Add your local network gateway](#localnet).</span></span>

[!INCLUDE [vpn-gateway-no-nsg](../../includes/vpn-gateway-no-nsg-include.md)]

### <a name="to-create-a-virtual-network-and-a-gateway-subnet"></a><span data-ttu-id="87a7e-142">To create a virtual network and a gateway subnet</span><span class="sxs-lookup"><span data-stu-id="87a7e-142">To create a virtual network and a gateway subnet</span></span>
<span data-ttu-id="87a7e-143">Use the following sample to create a virtual network and a gateway subnet:</span><span class="sxs-lookup"><span data-stu-id="87a7e-143">Use the following sample to create a virtual network and a gateway subnet:</span></span>

<span data-ttu-id="87a7e-144">First, create a resource group:</span><span class="sxs-lookup"><span data-stu-id="87a7e-144">First, create a resource group:</span></span>

```powershell
New-AzureRmResourceGroup -Name testrg -Location 'West US'
```

<span data-ttu-id="87a7e-145">Next, create your virtual network.</span><span class="sxs-lookup"><span data-stu-id="87a7e-145">Next, create your virtual network.</span></span> <span data-ttu-id="87a7e-146">Verify that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="87a7e-146">Verify that the address spaces you specify don't overlap any of the address spaces that you have on your on-premises network.</span></span>

<span data-ttu-id="87a7e-147">The following sample creates a virtual network named *testvnet* and two subnets, one called *GatewaySubnet* and the other called *Subnet1*.</span><span class="sxs-lookup"><span data-stu-id="87a7e-147">The following sample creates a virtual network named *testvnet* and two subnets, one called *GatewaySubnet* and the other called *Subnet1*.</span></span> <span data-ttu-id="87a7e-148">It's important to create one subnet named specifically *GatewaySubnet*.</span><span class="sxs-lookup"><span data-stu-id="87a7e-148">It's important to create one subnet named specifically *GatewaySubnet*.</span></span> <span data-ttu-id="87a7e-149">If you name it something else, your connection configuration will fail.</span><span class="sxs-lookup"><span data-stu-id="87a7e-149">If you name it something else, your connection configuration will fail.</span></span>

<span data-ttu-id="87a7e-150">Set the variables.</span><span class="sxs-lookup"><span data-stu-id="87a7e-150">Set the variables.</span></span>

```powershell
$subnet1 = New-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.0.0/28
$subnet2 = New-AzureRmVirtualNetworkSubnetConfig -Name 'Subnet1' -AddressPrefix '10.0.1.0/28'
```

<span data-ttu-id="87a7e-151">Create the VNet.</span><span class="sxs-lookup"><span data-stu-id="87a7e-151">Create the VNet.</span></span>

```powershell
New-AzureRmVirtualNetwork -Name testvnet -ResourceGroupName testrg `
-Location 'West US' -AddressPrefix 10.0.0.0/16 -Subnet $subnet1, $subnet2
```

### <a name="gatewaysubnet"></a><span data-ttu-id="87a7e-152">To add a gateway subnet to a virtual network you have already created</span><span class="sxs-lookup"><span data-stu-id="87a7e-152">To add a gateway subnet to a virtual network you have already created</span></span>
<span data-ttu-id="87a7e-153">This step is required only if you need to add a gateway subnet to a VNet that you previously created.</span><span class="sxs-lookup"><span data-stu-id="87a7e-153">This step is required only if you need to add a gateway subnet to a VNet that you previously created.</span></span>

<span data-ttu-id="87a7e-154">You can create your gateway subnet by using the following sample.</span><span class="sxs-lookup"><span data-stu-id="87a7e-154">You can create your gateway subnet by using the following sample.</span></span> <span data-ttu-id="87a7e-155">Be sure to name the gateway subnet 'GatewaySubnet'.</span><span class="sxs-lookup"><span data-stu-id="87a7e-155">Be sure to name the gateway subnet 'GatewaySubnet'.</span></span> <span data-ttu-id="87a7e-156">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="87a7e-156">If you name it something else, you create a subnet, but Azure won't treat it as a gateway subnet.</span></span>

<span data-ttu-id="87a7e-157">Set the variables.</span><span class="sxs-lookup"><span data-stu-id="87a7e-157">Set the variables.</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName testrg -Name testvnet
```

<span data-ttu-id="87a7e-158">Create the gateway subnet.\\</span><span class="sxs-lookup"><span data-stu-id="87a7e-158">Create the gateway subnet.\\</span></span>

```powershell
Add-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -AddressPrefix 10.0.3.0/28 -VirtualNetwork $vnet
```

<span data-ttu-id="87a7e-159">Set the configuration.</span><span class="sxs-lookup"><span data-stu-id="87a7e-159">Set the configuration.</span></span>

```powershell
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

## <span data-ttu-id="87a7e-160">3. <a name="localnet"></a>Add your local network gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-160">3. <a name="localnet"></a>Add your local network gateway</span></span>
<span data-ttu-id="87a7e-161">In a virtual network, the local network gateway typically refers to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="87a7e-161">In a virtual network, the local network gateway typically refers to your on-premises location.</span></span> <span data-ttu-id="87a7e-162">You give the site a name by which Azure can refer to it, and also specify the address space prefix for the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-162">You give the site a name by which Azure can refer to it, and also specify the address space prefix for the local network gateway.</span></span>

<span data-ttu-id="87a7e-163">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="87a7e-163">Azure uses the IP address prefix you specify to identify which traffic to send to your on-premises location.</span></span> <span data-ttu-id="87a7e-164">This means that you have to specify each address prefix that you want to be associated with your local network gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-164">This means that you have to specify each address prefix that you want to be associated with your local network gateway.</span></span> <span data-ttu-id="87a7e-165">You can easily update these prefixes if your on-premises network changes.</span><span class="sxs-lookup"><span data-stu-id="87a7e-165">You can easily update these prefixes if your on-premises network changes.</span></span>

<span data-ttu-id="87a7e-166">When using the PowerShell examples, note the following:</span><span class="sxs-lookup"><span data-stu-id="87a7e-166">When using the PowerShell examples, note the following:</span></span>

* <span data-ttu-id="87a7e-167">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span><span class="sxs-lookup"><span data-stu-id="87a7e-167">The *GatewayIPAddress* is the IP address of your on-premises VPN device.</span></span> <span data-ttu-id="87a7e-168">Your VPN device cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="87a7e-168">Your VPN device cannot be located behind a NAT.</span></span>
* <span data-ttu-id="87a7e-169">The *AddressPrefix* is your on-premises address space.</span><span class="sxs-lookup"><span data-stu-id="87a7e-169">The *AddressPrefix* is your on-premises address space.</span></span>

<span data-ttu-id="87a7e-170">To add a local network gateway with a single address prefix:</span><span class="sxs-lookup"><span data-stu-id="87a7e-170">To add a local network gateway with a single address prefix:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix '10.5.51.0/24'
```

<span data-ttu-id="87a7e-171">To add a local network gateway with multiple address prefixes:</span><span class="sxs-lookup"><span data-stu-id="87a7e-171">To add a local network gateway with multiple address prefixes:</span></span>

```powershell
New-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg `
-Location 'West US' -GatewayIpAddress '23.99.221.164' -AddressPrefix @('10.0.0.0/24','20.0.0.0/24')
```

### <a name="to-modify-ip-address-prefixes-for-your-local-network-gateway"></a><span data-ttu-id="87a7e-172">To modify IP address prefixes for your local network gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-172">To modify IP address prefixes for your local network gateway</span></span>
<span data-ttu-id="87a7e-173">Sometimes your local network gateway prefixes change.</span><span class="sxs-lookup"><span data-stu-id="87a7e-173">Sometimes your local network gateway prefixes change.</span></span> <span data-ttu-id="87a7e-174">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span><span class="sxs-lookup"><span data-stu-id="87a7e-174">The steps you take to modify your IP address prefixes depend on whether you have created a VPN gateway connection.</span></span> <span data-ttu-id="87a7e-175">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span><span class="sxs-lookup"><span data-stu-id="87a7e-175">See the [Modify IP address prefixes for a local network gateway](#modify) section of this article.</span></span>

## <a name="PublicIP"></a><span data-ttu-id="87a7e-176">4. Request a public IP address for the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-176">4. Request a public IP address for the VPN gateway</span></span>
<span data-ttu-id="87a7e-177">Next, request a public IP address to be allocated to your Azure VNet VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-177">Next, request a public IP address to be allocated to your Azure VNet VPN gateway.</span></span> <span data-ttu-id="87a7e-178">This is not the same IP address that is assigned to your VPN device; rather it's assigned to the Azure VPN gateway itself.</span><span class="sxs-lookup"><span data-stu-id="87a7e-178">This is not the same IP address that is assigned to your VPN device; rather it's assigned to the Azure VPN gateway itself.</span></span> <span data-ttu-id="87a7e-179">You can't specify the IP address that you want to use.</span><span class="sxs-lookup"><span data-stu-id="87a7e-179">You can't specify the IP address that you want to use.</span></span> <span data-ttu-id="87a7e-180">It is dynamically allocated to your gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-180">It is dynamically allocated to your gateway.</span></span> <span data-ttu-id="87a7e-181">You use this IP address when configuring your on-premises VPN device to connect to the gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-181">You use this IP address when configuring your on-premises VPN device to connect to the gateway.</span></span>

<span data-ttu-id="87a7e-182">The Azure VPN gateway for the Resource Manager deployment model currently only supports public IP addresses by using the Dynamic Allocation method.</span><span class="sxs-lookup"><span data-stu-id="87a7e-182">The Azure VPN gateway for the Resource Manager deployment model currently only supports public IP addresses by using the Dynamic Allocation method.</span></span> <span data-ttu-id="87a7e-183">However, this does not mean the IP address changes.</span><span class="sxs-lookup"><span data-stu-id="87a7e-183">However, this does not mean the IP address changes.</span></span> <span data-ttu-id="87a7e-184">The only time the Azure VPN gateway IP address changes is when the gateway is deleted and re-created.</span><span class="sxs-lookup"><span data-stu-id="87a7e-184">The only time the Azure VPN gateway IP address changes is when the gateway is deleted and re-created.</span></span> <span data-ttu-id="87a7e-185">The gateway public IP address doesn't change across resizing, resetting, or other internal maintenance/upgrades of your Azure VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-185">The gateway public IP address doesn't change across resizing, resetting, or other internal maintenance/upgrades of your Azure VPN gateway.</span></span>

<span data-ttu-id="87a7e-186">Use the following PowerShell sample:</span><span class="sxs-lookup"><span data-stu-id="87a7e-186">Use the following PowerShell sample:</span></span>

```powershell
$gwpip= New-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName testrg -Location 'West US' -AllocationMethod Dynamic
```

## <a name="GatewayIPConfig"></a><span data-ttu-id="87a7e-187">5. Create the gateway IP addressing configuration</span><span class="sxs-lookup"><span data-stu-id="87a7e-187">5. Create the gateway IP addressing configuration</span></span>
<span data-ttu-id="87a7e-188">The gateway configuration defines the subnet and the public IP address to use.</span><span class="sxs-lookup"><span data-stu-id="87a7e-188">The gateway configuration defines the subnet and the public IP address to use.</span></span> <span data-ttu-id="87a7e-189">Use the following sample to create your gateway configuration:</span><span class="sxs-lookup"><span data-stu-id="87a7e-189">Use the following sample to create your gateway configuration:</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name testvnet -ResourceGroupName testrg
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name gwipconfig1 -SubnetId $subnet.Id -PublicIpAddressId $gwpip.Id
```

## <a name="CreateGateway"></a><span data-ttu-id="87a7e-190">6. Create the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-190">6. Create the virtual network gateway</span></span>
<span data-ttu-id="87a7e-191">In this step, you create the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="87a7e-191">In this step, you create the virtual network gateway.</span></span> <span data-ttu-id="87a7e-192">Creating a gateway can take a long time to complete.</span><span class="sxs-lookup"><span data-stu-id="87a7e-192">Creating a gateway can take a long time to complete.</span></span> <span data-ttu-id="87a7e-193">Often 45 minutes or more.</span><span class="sxs-lookup"><span data-stu-id="87a7e-193">Often 45 minutes or more.</span></span>

<span data-ttu-id="87a7e-194">Use the following values:</span><span class="sxs-lookup"><span data-stu-id="87a7e-194">Use the following values:</span></span>

* <span data-ttu-id="87a7e-195">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span><span class="sxs-lookup"><span data-stu-id="87a7e-195">The *-GatewayType* for a Site-to-Site configuration is *Vpn*.</span></span> <span data-ttu-id="87a7e-196">The gateway type is always specific to the configuration that you are implementing.</span><span class="sxs-lookup"><span data-stu-id="87a7e-196">The gateway type is always specific to the configuration that you are implementing.</span></span> <span data-ttu-id="87a7e-197">For example, other gateway configurations may require -GatewayType ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="87a7e-197">For example, other gateway configurations may require -GatewayType ExpressRoute.</span></span>
* <span data-ttu-id="87a7e-198">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span><span class="sxs-lookup"><span data-stu-id="87a7e-198">The *-VpnType* can be *RouteBased* (referred to as a Dynamic Gateway in some documentation), or *PolicyBased* (referred to as a Static Gateway in some documentation).</span></span> <span data-ttu-id="87a7e-199">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-199">For more information about VPN gateway types, see [About VPN Gateway](vpn-gateway-about-vpngateways.md).</span></span>
* <span data-ttu-id="87a7e-200">The *-GatewaySku* can be *Basic*, *Standard*, or *HighPerformance*.</span><span class="sxs-lookup"><span data-stu-id="87a7e-200">The *-GatewaySku* can be *Basic*, *Standard*, or *HighPerformance*.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg `
-Location 'West US' -IpConfigurations $gwipconfig -GatewayType Vpn `
-VpnType RouteBased -GatewaySku Standard
```

## <a name="ConfigureVPNDevice"></a><span data-ttu-id="87a7e-201">7. Configure your VPN device</span><span class="sxs-lookup"><span data-stu-id="87a7e-201">7. Configure your VPN device</span></span>
<span data-ttu-id="87a7e-202">At this point, you need the public IP address of the virtual network gateway for configuring your on-premises VPN device.</span><span class="sxs-lookup"><span data-stu-id="87a7e-202">At this point, you need the public IP address of the virtual network gateway for configuring your on-premises VPN device.</span></span> <span data-ttu-id="87a7e-203">Work with your device manufacturer for specific configuration information.</span><span class="sxs-lookup"><span data-stu-id="87a7e-203">Work with your device manufacturer for specific configuration information.</span></span> <span data-ttu-id="87a7e-204">You can refer to the [VPN Devices](vpn-gateway-about-vpn-devices.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="87a7e-204">You can refer to the [VPN Devices](vpn-gateway-about-vpn-devices.md) for more information.</span></span>

<span data-ttu-id="87a7e-205">To find the public IP address of your virtual network gateway, use the following sample:</span><span class="sxs-lookup"><span data-stu-id="87a7e-205">To find the public IP address of your virtual network gateway, use the following sample:</span></span>

```powershell
Get-AzureRmPublicIpAddress -Name gwpip -ResourceGroupName testrg
```

## <a name="CreateConnection"></a><span data-ttu-id="87a7e-206">8. Create the VPN connection</span><span class="sxs-lookup"><span data-stu-id="87a7e-206">8. Create the VPN connection</span></span>
<span data-ttu-id="87a7e-207">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span><span class="sxs-lookup"><span data-stu-id="87a7e-207">Next, create the Site-to-Site VPN connection between your virtual network gateway and your VPN device.</span></span> <span data-ttu-id="87a7e-208">Be sure to replace the values with your own.</span><span class="sxs-lookup"><span data-stu-id="87a7e-208">Be sure to replace the values with your own.</span></span> <span data-ttu-id="87a7e-209">The shared key must match the value you used for your VPN device configuration.</span><span class="sxs-lookup"><span data-stu-id="87a7e-209">The shared key must match the value you used for your VPN device configuration.</span></span> <span data-ttu-id="87a7e-210">Notice that the `-ConnectionType` for Site-to-Site is *IPsec*.</span><span class="sxs-lookup"><span data-stu-id="87a7e-210">Notice that the `-ConnectionType` for Site-to-Site is *IPsec*.</span></span>

<span data-ttu-id="87a7e-211">Set the variables.</span><span class="sxs-lookup"><span data-stu-id="87a7e-211">Set the variables.</span></span>

```powershell
$gateway1 = Get-AzureRmVirtualNetworkGateway -Name vnetgw1 -ResourceGroupName testrg
$local = Get-AzureRmLocalNetworkGateway -Name LocalSite -ResourceGroupName testrg
```

<span data-ttu-id="87a7e-212">Create the connection.</span><span class="sxs-lookup"><span data-stu-id="87a7e-212">Create the connection.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name localtovon -ResourceGroupName testrg `
-Location 'West US' -VirtualNetworkGateway1 $gateway1 -LocalNetworkGateway2 $local `
-ConnectionType IPsec -RoutingWeight 10 -SharedKey 'abc123'
```

<span data-ttu-id="87a7e-213">After a short while, the connection will be established.</span><span class="sxs-lookup"><span data-stu-id="87a7e-213">After a short while, the connection will be established.</span></span>

## <a name="toverify"></a><span data-ttu-id="87a7e-214">To verify a VPN connection</span><span class="sxs-lookup"><span data-stu-id="87a7e-214">To verify a VPN connection</span></span>
<span data-ttu-id="87a7e-215">There are a few different ways to verify your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="87a7e-215">There are a few different ways to verify your VPN connection.</span></span>

[!INCLUDE [vpn-gateway-verify-connection-rm](../../includes/vpn-gateway-verify-connection-rm-include.md)]

## <a name="modify"></a><span data-ttu-id="87a7e-216">To modify IP address prefixes for a local network gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-216">To modify IP address prefixes for a local network gateway</span></span>
<span data-ttu-id="87a7e-217">If you need to change the prefixes for your local network gateway, use the following instructions.</span><span class="sxs-lookup"><span data-stu-id="87a7e-217">If you need to change the prefixes for your local network gateway, use the following instructions.</span></span> <span data-ttu-id="87a7e-218">Two sets of instructions are provided.</span><span class="sxs-lookup"><span data-stu-id="87a7e-218">Two sets of instructions are provided.</span></span> <span data-ttu-id="87a7e-219">The instructions you choose depend on whether you have already created your gateway connection.</span><span class="sxs-lookup"><span data-stu-id="87a7e-219">The instructions you choose depend on whether you have already created your gateway connection.</span></span>

[!INCLUDE [vpn-gateway-modify-ip-prefix-rm](../../includes/vpn-gateway-modify-ip-prefix-rm-include.md)]

## <a name="modifygwipaddress"></a><span data-ttu-id="87a7e-220">To modify the gateway IP address for a local network gateway</span><span class="sxs-lookup"><span data-stu-id="87a7e-220">To modify the gateway IP address for a local network gateway</span></span>
[!INCLUDE [vpn-gateway-modify-lng-gateway-ip-rm](../../includes/vpn-gateway-modify-lng-gateway-ip-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="87a7e-221">Next steps</span><span class="sxs-lookup"><span data-stu-id="87a7e-221">Next steps</span></span>
*  <span data-ttu-id="87a7e-222">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="87a7e-222">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="87a7e-223">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="87a7e-223">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
* <span data-ttu-id="87a7e-224">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="87a7e-224">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>

