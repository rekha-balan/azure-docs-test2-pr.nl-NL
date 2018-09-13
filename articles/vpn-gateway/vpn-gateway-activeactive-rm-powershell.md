---
title: 'Configure active-active S2S VPN connections for VPN Gateways: Azure Resource Manager: PowerShell | Microsoft Docs'
description: This article walks you through configuring active-active connections with Azure VPN Gateways using Azure Resource Manager and PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: azure-resource-manager
ms.assetid: 238cd9b3-f1ce-4341-b18e-7390935604fa
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2018
ms.author: yushwang, cherylmc
ms.openlocfilehash: 01f25df117eddaaf640a8bd2ef184fe685c5bc75
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44805459"
---
# <a name="configure-active-active-s2s-vpn-connections-with-azure-vpn-gateways"></a><span data-ttu-id="e5e83-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span><span class="sxs-lookup"><span data-stu-id="e5e83-103">Configure active-active S2S VPN connections with Azure VPN Gateways</span></span>

<span data-ttu-id="e5e83-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e5e83-104">This article walks you through the steps to create active-active cross-premises and VNet-to-VNet connections using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-highly-available-cross-premises-connections"></a><span data-ttu-id="e5e83-105">About highly available cross-premises connections</span><span class="sxs-lookup"><span data-stu-id="e5e83-105">About highly available cross-premises connections</span></span>
<span data-ttu-id="e5e83-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span><span class="sxs-lookup"><span data-stu-id="e5e83-106">To achieve high availability for cross-premises and VNet-to-VNet connectivity, you should deploy multiple VPN gateways and establish multiple parallel connections between your networks and Azure.</span></span> <span data-ttu-id="e5e83-107">See [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span><span class="sxs-lookup"><span data-stu-id="e5e83-107">See [Highly Available Cross-Premises and VNet-to-VNet Connectivity](vpn-gateway-highlyavailable.md) for an overview of connectivity options and topology.</span></span>

<span data-ttu-id="e5e83-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks.</span><span class="sxs-lookup"><span data-stu-id="e5e83-108">This article provides the instructions to set up an active-active cross-premises VPN connection, and active-active connection between two virtual networks.</span></span>

* [<span data-ttu-id="e5e83-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span><span class="sxs-lookup"><span data-stu-id="e5e83-109">Part 1 - Create and configure your Azure VPN gateway in active-active mode</span></span>](#aagateway)
* [<span data-ttu-id="e5e83-110">Part 2 - Establish active-active cross-premises connections</span><span class="sxs-lookup"><span data-stu-id="e5e83-110">Part 2 - Establish active-active cross-premises connections</span></span>](#aacrossprem)
* [<span data-ttu-id="e5e83-111">Part 3 - Establish active-active VNet-to-VNet connections</span><span class="sxs-lookup"><span data-stu-id="e5e83-111">Part 3 - Establish active-active VNet-to-VNet connections</span></span>](#aav2v)

<span data-ttu-id="e5e83-112">If you already have a VPN gateway, you can:</span><span class="sxs-lookup"><span data-stu-id="e5e83-112">If you already have a VPN gateway, you can:</span></span>
* [<span data-ttu-id="e5e83-113">Update an existing VPN gateway from active-standby to active-active, or vice versa</span><span class="sxs-lookup"><span data-stu-id="e5e83-113">Update an existing VPN gateway from active-standby to active-active, or vice versa</span></span>](#aaupdate)

<span data-ttu-id="e5e83-114">You can combine these together to build a more complex, highly available network topology that meets your needs.</span><span class="sxs-lookup"><span data-stu-id="e5e83-114">You can combine these together to build a more complex, highly available network topology that meets your needs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e5e83-115">The active-active mode uses only the following SKUs:</span><span class="sxs-lookup"><span data-stu-id="e5e83-115">The active-active mode uses only the following SKUs:</span></span> 
  * <span data-ttu-id="e5e83-116">VpnGw1, VpnGw2, VpnGw3</span><span class="sxs-lookup"><span data-stu-id="e5e83-116">VpnGw1, VpnGw2, VpnGw3</span></span>
  * <span data-ttu-id="e5e83-117">HighPerformance (for old legacy SKUs)</span><span class="sxs-lookup"><span data-stu-id="e5e83-117">HighPerformance (for old legacy SKUs)</span></span>
> 
> 

## <a name ="aagateway"></a><span data-ttu-id="e5e83-118">Part 1 - Create and configure active-active VPN gateways</span><span class="sxs-lookup"><span data-stu-id="e5e83-118">Part 1 - Create and configure active-active VPN gateways</span></span>
<span data-ttu-id="e5e83-119">The following steps will configure your Azure VPN gateway in active-active modes.</span><span class="sxs-lookup"><span data-stu-id="e5e83-119">The following steps will configure your Azure VPN gateway in active-active modes.</span></span> <span data-ttu-id="e5e83-120">The key differences between the active-active and active-standby gateways:</span><span class="sxs-lookup"><span data-stu-id="e5e83-120">The key differences between the active-active and active-standby gateways:</span></span>

* <span data-ttu-id="e5e83-121">You need to create two Gateway IP configurations with two public IP addresses</span><span class="sxs-lookup"><span data-stu-id="e5e83-121">You need to create two Gateway IP configurations with two public IP addresses</span></span>
* <span data-ttu-id="e5e83-122">You need set the EnableActiveActiveFeature flag</span><span class="sxs-lookup"><span data-stu-id="e5e83-122">You need set the EnableActiveActiveFeature flag</span></span>
* <span data-ttu-id="e5e83-123">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span><span class="sxs-lookup"><span data-stu-id="e5e83-123">The gateway SKU must be VpnGw1, VpnGw2, VpnGw3, or HighPerformance (legacy SKU).</span></span>

<span data-ttu-id="e5e83-124">The other properties are the same as the non-active-active gateways.</span><span class="sxs-lookup"><span data-stu-id="e5e83-124">The other properties are the same as the non-active-active gateways.</span></span> 

### <a name="before-you-begin"></a><span data-ttu-id="e5e83-125">Before you begin</span><span class="sxs-lookup"><span data-stu-id="e5e83-125">Before you begin</span></span>
* <span data-ttu-id="e5e83-126">Verify that you have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e5e83-126">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="e5e83-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e5e83-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="e5e83-128">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e5e83-128">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="e5e83-129">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e5e83-129">See [Overview of Azure PowerShell](/powershell/azure/overview) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="e5e83-130">Step 1 - Create and configure VNet1</span><span class="sxs-lookup"><span data-stu-id="e5e83-130">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="e5e83-131">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="e5e83-131">1. Declare your variables</span></span>
<span data-ttu-id="e5e83-132">For this exercise, we'll start by declaring our variables.</span><span class="sxs-lookup"><span data-stu-id="e5e83-132">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="e5e83-133">The example below declares the variables using the values for this exercise.</span><span class="sxs-lookup"><span data-stu-id="e5e83-133">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="e5e83-134">Be sure to replace the values with your own when configuring for production.</span><span class="sxs-lookup"><span data-stu-id="e5e83-134">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="e5e83-135">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span><span class="sxs-lookup"><span data-stu-id="e5e83-135">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="e5e83-136">Modify the variables, and then copy and paste into your PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="e5e83-136">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Ross"
$RG1 = "TestAARG1"
$Location1 = "West US"
$VNetName1 = "TestVNet1"
$FESubName1 = "FrontEnd"
$BESubName1 = "Backend"
$GWSubName1 = "GatewaySubnet"
$VNetPrefix11 = "10.11.0.0/16"
$VNetPrefix12 = "10.12.0.0/16"
$FESubPrefix1 = "10.11.0.0/24"
$BESubPrefix1 = "10.12.0.0/24"
$GWSubPrefix1 = "10.12.255.0/27"
$VNet1ASN = 65010
$DNS1 = "8.8.8.8"
$GWName1 = "VNet1GW"
$GW1IPName1 = "VNet1GWIP1"
$GW1IPName2 = "VNet1GWIP2"
$GW1IPconf1 = "gw1ipconf1"
$GW1IPconf2 = "gw1ipconf2"
$Connection12 = "VNet1toVNet2"
$Connection151 = "VNet1toSite5_1"
$Connection152 = "VNet1toSite5_2"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="e5e83-137">2. Connect to your subscription and create a new resource group</span><span class="sxs-lookup"><span data-stu-id="e5e83-137">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="e5e83-138">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="e5e83-138">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="e5e83-139">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e5e83-139">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="e5e83-140">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="e5e83-140">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="e5e83-141">Use the following sample to help you connect:</span><span class="sxs-lookup"><span data-stu-id="e5e83-141">Use the following sample to help you connect:</span></span>

```powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="e5e83-142">3. Create TestVNet1</span><span class="sxs-lookup"><span data-stu-id="e5e83-142">3. Create TestVNet1</span></span>
<span data-ttu-id="e5e83-143">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span><span class="sxs-lookup"><span data-stu-id="e5e83-143">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="e5e83-144">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="e5e83-144">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="e5e83-145">If you name it something else, your gateway creation fails.</span><span class="sxs-lookup"><span data-stu-id="e5e83-145">If you name it something else, your gateway creation fails.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1
$besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-active-active-mode"></a><span data-ttu-id="e5e83-146">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span><span class="sxs-lookup"><span data-stu-id="e5e83-146">Step 2 - Create the VPN gateway for TestVNet1 with active-active mode</span></span>
#### <a name="1-create-the-public-ip-addresses-and-gateway-ip-configurations"></a><span data-ttu-id="e5e83-147">1. Create the public IP addresses and gateway IP configurations</span><span class="sxs-lookup"><span data-stu-id="e5e83-147">1. Create the public IP addresses and gateway IP configurations</span></span>
<span data-ttu-id="e5e83-148">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span><span class="sxs-lookup"><span data-stu-id="e5e83-148">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="e5e83-149">You'll also define the subnet and IP configurations required.</span><span class="sxs-lookup"><span data-stu-id="e5e83-149">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw1pip1 = New-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic
$gw1pip2 = New-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gw1ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf1 -Subnet $subnet1 -PublicIpAddress $gw1pip1
$gw1ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW1IPconf2 -Subnet $subnet1 -PublicIpAddress $gw1pip2
```

#### <a name="2-create-the-vpn-gateway-with-active-active-configuration"></a><span data-ttu-id="e5e83-150">2. Create the VPN gateway with active-active configuration</span><span class="sxs-lookup"><span data-stu-id="e5e83-150">2. Create the VPN gateway with active-active configuration</span></span>
<span data-ttu-id="e5e83-151">Create the virtual network gateway for TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e5e83-151">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="e5e83-152">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span><span class="sxs-lookup"><span data-stu-id="e5e83-152">Note that there are two GatewayIpConfig entries, and the EnableActiveActiveFeature flag is set.</span></span> <span data-ttu-id="e5e83-153">Creating a gateway can take a while (45 minutes or more to complete).</span><span class="sxs-lookup"><span data-stu-id="e5e83-153">Creating a gateway can take a while (45 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gw1ipconf1,$gw1ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet1ASN -EnableActiveActiveFeature -Debug
```

#### <a name="3-obtain-the-gateway-public-ip-addresses-and-the-bgp-peer-ip-address"></a><span data-ttu-id="e5e83-154">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span><span class="sxs-lookup"><span data-stu-id="e5e83-154">3. Obtain the gateway public IP addresses and the BGP Peer IP address</span></span>
<span data-ttu-id="e5e83-155">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-155">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="e5e83-156">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span><span class="sxs-lookup"><span data-stu-id="e5e83-156">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$gw1pip1 = Get-AzureRmPublicIpAddress -Name $GW1IPName1 -ResourceGroupName $RG1
$gw1pip2 = Get-AzureRmPublicIpAddress -Name $GW1IPName2 -ResourceGroupName $RG1
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
```

<span data-ttu-id="e5e83-157">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span><span class="sxs-lookup"><span data-stu-id="e5e83-157">Use the following cmdlets to show the two public IP addresses allocated for your VPN gateway, and their corresponding BGP Peer IP addresses for each gateway instance:</span></span>

```powershell
PS D:\> $gw1pip1.IpAddress
40.112.190.5

PS D:\> $gw1pip2.IpAddress
138.91.156.129

PS D:\> $vnet1gw.BgpSettingsText
{
  "Asn": 65010,
  "BgpPeeringAddress": "10.12.255.4,10.12.255.5",
  "PeerWeight": 0
}
```

<span data-ttu-id="e5e83-158">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span><span class="sxs-lookup"><span data-stu-id="e5e83-158">The order of the public IP addresses for the gateway instances and the corresponding BGP Peering Addresses are the same.</span></span> <span data-ttu-id="e5e83-159">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span><span class="sxs-lookup"><span data-stu-id="e5e83-159">In this example, the gateway VM with public IP of 40.112.190.5 will use 10.12.255.4 as its BGP Peering Address, and the gateway with 138.91.156.129 will use 10.12.255.5.</span></span> <span data-ttu-id="e5e83-160">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-160">This information is needed when you set up your on premises VPN devices connecting to the active-active gateway.</span></span> <span data-ttu-id="e5e83-161">The gateway is shown in the diagram below with all addresses:</span><span class="sxs-lookup"><span data-stu-id="e5e83-161">The gateway is shown in the diagram below with all addresses:</span></span>

![active-active gateway](./media/vpn-gateway-activeactive-rm-powershell/active-active-gw.png)

<span data-ttu-id="e5e83-163">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span><span class="sxs-lookup"><span data-stu-id="e5e83-163">Once the gateway is created, you can use this gateway to establish active-active cross-premises or VNet-to-VNet connection.</span></span> <span data-ttu-id="e5e83-164">The following sections walk through the steps to complete the exercise.</span><span class="sxs-lookup"><span data-stu-id="e5e83-164">The following sections walk through the steps to complete the exercise.</span></span>

## <a name ="aacrossprem"></a><span data-ttu-id="e5e83-165">Part 2 - Establish an active-active cross-premises connection</span><span class="sxs-lookup"><span data-stu-id="e5e83-165">Part 2 - Establish an active-active cross-premises connection</span></span>
<span data-ttu-id="e5e83-166">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-166">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="e5e83-167">In this example, the Azure VPN gateway is in active-active mode.</span><span class="sxs-lookup"><span data-stu-id="e5e83-167">In this example, the Azure VPN gateway is in active-active mode.</span></span> <span data-ttu-id="e5e83-168">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span><span class="sxs-lookup"><span data-stu-id="e5e83-168">As a result, even though there is only one on-premises VPN device (local network gateway) and one connection resource, both Azure VPN gateway instances will establish S2S VPN tunnels with the on-premises device.</span></span>

<span data-ttu-id="e5e83-169">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span><span class="sxs-lookup"><span data-stu-id="e5e83-169">Before proceeding, please make sure you have completed [Part 1](#aagateway) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="e5e83-170">Step 1 - Create and configure the local network gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-170">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="e5e83-171">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="e5e83-171">1. Declare your variables</span></span>
<span data-ttu-id="e5e83-172">This exercise will continue to build the configuration shown in the diagram.</span><span class="sxs-lookup"><span data-stu-id="e5e83-172">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="e5e83-173">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="e5e83-173">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestAARG5"
$Location5 = "West US"
$LNGName51 = "Site5_1"
$LNGPrefix51 = "10.52.255.253/32"
$LNGIP51 = "131.107.72.22"
$LNGASN5 = 65050
$BGPPeerIP51 = "10.52.255.253"
```

<span data-ttu-id="e5e83-174">A couple of things to note regarding the local network gateway parameters:</span><span class="sxs-lookup"><span data-stu-id="e5e83-174">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="e5e83-175">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-175">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="e5e83-176">This example shows them in different resource groups but in the same Azure location.</span><span class="sxs-lookup"><span data-stu-id="e5e83-176">This example shows them in different resource groups but in the same Azure location.</span></span>
* <span data-ttu-id="e5e83-177">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span><span class="sxs-lookup"><span data-stu-id="e5e83-177">If there is only one on-premises VPN device as shown above, the active-active connection can work with or without BGP protocol.</span></span> <span data-ttu-id="e5e83-178">This example uses BGP for the cross-premises connection.</span><span class="sxs-lookup"><span data-stu-id="e5e83-178">This example uses BGP for the cross-premises connection.</span></span>
* <span data-ttu-id="e5e83-179">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span><span class="sxs-lookup"><span data-stu-id="e5e83-179">If BGP is enabled, the prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="e5e83-180">In this case, it's a /32 prefix of "10.52.255.253/32".</span><span class="sxs-lookup"><span data-stu-id="e5e83-180">In this case, it's a /32 prefix of "10.52.255.253/32".</span></span>
* <span data-ttu-id="e5e83-181">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="e5e83-181">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="e5e83-182">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span><span class="sxs-lookup"><span data-stu-id="e5e83-182">If they are the same, you need to change your VNet ASN if your on-premises VPN device already uses the ASN to peer with other BGP neighbors.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="e5e83-183">2. Create the local network gateway for Site5</span><span class="sxs-lookup"><span data-stu-id="e5e83-183">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="e5e83-184">Before you continue, please make sure you are still connected to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="e5e83-184">Before you continue, please make sure you are still connected to Subscription 1.</span></span> <span data-ttu-id="e5e83-185">Create the resource group if it is not yet created.</span><span class="sxs-lookup"><span data-stu-id="e5e83-185">Create the resource group if it is not yet created.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5
New-AzureRmLocalNetworkGateway -Name $LNGName51 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP51 -AddressPrefix $LNGPrefix51 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP51
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="e5e83-186">Step 2 - Connect the VNet gateway and local network gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-186">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="e5e83-187">1. Get the two gateways</span><span class="sxs-lookup"><span data-stu-id="e5e83-187">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw1 = Get-AzureRmLocalNetworkGateway  -Name $LNGName51 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="e5e83-188">2. Create the TestVNet1 to Site5 connection</span><span class="sxs-lookup"><span data-stu-id="e5e83-188">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="e5e83-189">In this step, you create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span><span class="sxs-lookup"><span data-stu-id="e5e83-189">In this step, you create the connection from TestVNet1 to Site5_1 with "EnableBGP" set to $True.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection151 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw1 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-on-premises-vpn-device"></a><span data-ttu-id="e5e83-190">3. VPN and BGP parameters for your on-premises VPN device</span><span class="sxs-lookup"><span data-stu-id="e5e83-190">3. VPN and BGP parameters for your on-premises VPN device</span></span>
<span data-ttu-id="e5e83-191">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span><span class="sxs-lookup"><span data-stu-id="e5e83-191">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.253
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="e5e83-192">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span><span class="sxs-lookup"><span data-stu-id="e5e83-192">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span> <span data-ttu-id="e5e83-193">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span><span class="sxs-lookup"><span data-stu-id="e5e83-193">This example so far has configured only one on-premises VPN device, resulting in the diagram shown below:</span></span>

![active-active-crossprem](./media/vpn-gateway-activeactive-rm-powershell/active-active.png)

### <a name="step-3---connect-two-on-premises-vpn-devices-to-the-active-active-vpn-gateway"></a><span data-ttu-id="e5e83-195">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-195">Step 3 - Connect two on-premises VPN devices to the active-active VPN gateway</span></span>
<span data-ttu-id="e5e83-196">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span><span class="sxs-lookup"><span data-stu-id="e5e83-196">If you have two VPN devices at the same on-premises network, you can achieve dual redundancy by connecting the Azure VPN gateway to the second VPN device.</span></span>

#### <a name="1-create-the-second-local-network-gateway-for-site5"></a><span data-ttu-id="e5e83-197">1. Create the second local network gateway for Site5</span><span class="sxs-lookup"><span data-stu-id="e5e83-197">1. Create the second local network gateway for Site5</span></span>
<span data-ttu-id="e5e83-198">The gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span><span class="sxs-lookup"><span data-stu-id="e5e83-198">The gateway IP address, address prefix, and BGP peering address for the second local network gateway must not overlap with the previous local network gateway for the same on-premises network.</span></span>

```powershell
$LNGName52 = "Site5_2"
$LNGPrefix52 = "10.52.255.254/32"
$LNGIP52 = "131.107.72.23"
$BGPPeerIP52 = "10.52.255.254"
```

```powershell
New-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP52 -AddressPrefix $LNGPrefix52 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP52
```

#### <a name="2-connect-the-vnet-gateway-and-the-second-local-network-gateway"></a><span data-ttu-id="e5e83-199">2. Connect the VNet gateway and the second local network gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-199">2. Connect the VNet gateway and the second local network gateway</span></span>
<span data-ttu-id="e5e83-200">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span><span class="sxs-lookup"><span data-stu-id="e5e83-200">Create the connection from TestVNet1 to Site5_2 with "EnableBGP" set to $True</span></span>

```powershell
$lng5gw2 = Get-AzureRmLocalNetworkGateway -Name $LNGName52 -ResourceGroupName $RG5
```

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection152 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw2 -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```

#### <a name="3-vpn-and-bgp-parameters-for-your-second-on-premises-vpn-device"></a><span data-ttu-id="e5e83-201">3. VPN and BGP parameters for your second on-premises VPN device</span><span class="sxs-lookup"><span data-stu-id="e5e83-201">3. VPN and BGP parameters for your second on-premises VPN device</span></span>
<span data-ttu-id="e5e83-202">Similarly, below lists the parameters you will enter into the second VPN device:</span><span class="sxs-lookup"><span data-stu-id="e5e83-202">Similarly, below lists the parameters you will enter into the second VPN device:</span></span>

```
- Site5 ASN            : 65050
- Site5 BGP IP         : 10.52.255.254
- Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16
- Azure VNet ASN       : 65010
- Azure VNet BGP IP 1  : 10.12.255.4 for tunnel to 40.112.190.5
- Azure VNet BGP IP 2  : 10.12.255.5 for tunnel to 138.91.156.129
- Static routes        : Destination 10.12.255.4/32, nexthop the VPN tunnel interface to 40.112.190.5
                         Destination 10.12.255.5/32, nexthop the VPN tunnel interface to 138.91.156.129
- eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed
```

<span data-ttu-id="e5e83-203">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span><span class="sxs-lookup"><span data-stu-id="e5e83-203">Once the connection (tunnels) are established, you will have dual redundant VPN devices and tunnels connecting your on-premises network and Azure:</span></span>

![dual-redundancy-crossprem](./media/vpn-gateway-activeactive-rm-powershell/dual-redundancy.png)

## <a name ="aav2v"></a><span data-ttu-id="e5e83-205">Part 3 - Establish an active-active VNet-to-VNet connection</span><span class="sxs-lookup"><span data-stu-id="e5e83-205">Part 3 - Establish an active-active VNet-to-VNet connection</span></span>
<span data-ttu-id="e5e83-206">This section creates an active-active VNet-to-VNet connection with BGP.</span><span class="sxs-lookup"><span data-stu-id="e5e83-206">This section creates an active-active VNet-to-VNet connection with BGP.</span></span> 

<span data-ttu-id="e5e83-207">The instructions below continue from the previous steps listed above.</span><span class="sxs-lookup"><span data-stu-id="e5e83-207">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="e5e83-208">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span><span class="sxs-lookup"><span data-stu-id="e5e83-208">You must complete [Part 1](#aagateway) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="e5e83-209">Step 1 - Create TestVNet2 and the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-209">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="e5e83-210">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span><span class="sxs-lookup"><span data-stu-id="e5e83-210">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="e5e83-211">In this example, the virtual networks belong to the same subscription.</span><span class="sxs-lookup"><span data-stu-id="e5e83-211">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="e5e83-212">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span><span class="sxs-lookup"><span data-stu-id="e5e83-212">You can set up VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="e5e83-213">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span><span class="sxs-lookup"><span data-stu-id="e5e83-213">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="e5e83-214">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="e5e83-214">1. Declare your variables</span></span>
<span data-ttu-id="e5e83-215">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="e5e83-215">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestAARG2"
$Location2 = "East US"
$VNetName2 = "TestVNet2"
$FESubName2 = "FrontEnd"
$BESubName2 = "Backend"
$GWSubName2 = "GatewaySubnet"
$VNetPrefix21 = "10.21.0.0/16"
$VNetPrefix22 = "10.22.0.0/16"
$FESubPrefix2 = "10.21.0.0/24"
$BESubPrefix2 = "10.22.0.0/24"
$GWSubPrefix2 = "10.22.255.0/27"
$VNet2ASN = 65020
$DNS2 = "8.8.8.8"
$GWName2 = "VNet2GW"
$GW2IPName1 = "VNet2GWIP1"
$GW2IPconf1 = "gw2ipconf1"
$GW2IPName2 = "VNet2GWIP2"
$GW2IPconf2 = "gw2ipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="e5e83-216">2. Create TestVNet2 in the new resource group</span><span class="sxs-lookup"><span data-stu-id="e5e83-216">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-active-active-vpn-gateway-for-testvnet2"></a><span data-ttu-id="e5e83-217">3. Create the active-active VPN gateway for TestVNet2</span><span class="sxs-lookup"><span data-stu-id="e5e83-217">3. Create the active-active VPN gateway for TestVNet2</span></span>
<span data-ttu-id="e5e83-218">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span><span class="sxs-lookup"><span data-stu-id="e5e83-218">Request two public IP addresses to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="e5e83-219">You'll also define the subnet and IP configurations required.</span><span class="sxs-lookup"><span data-stu-id="e5e83-219">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gw2pip1 = New-AzureRmPublicIpAddress -Name $GW2IPName1 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic
$gw2pip2 = New-AzureRmPublicIpAddress -Name $GW2IPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2 = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gw2ipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf1 -Subnet $subnet2 -PublicIpAddress $gw2pip1
$gw2ipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GW2IPconf2 -Subnet $subnet2 -PublicIpAddress $gw2pip2
```

<span data-ttu-id="e5e83-220">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span><span class="sxs-lookup"><span data-stu-id="e5e83-220">Create the VPN gateway with the AS number and the "EnableActiveActiveFeature" flag.</span></span> <span data-ttu-id="e5e83-221">Note that you must override the default ASN on your Azure VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="e5e83-221">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="e5e83-222">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span><span class="sxs-lookup"><span data-stu-id="e5e83-222">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gw2ipconf1,$gw2ipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku VpnGw1 -Asn $VNet2ASN -EnableActiveActiveFeature
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="e5e83-223">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span><span class="sxs-lookup"><span data-stu-id="e5e83-223">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="e5e83-224">In this example, both gateways are in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="e5e83-224">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="e5e83-225">You can complete this step in the same PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="e5e83-225">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="e5e83-226">1. Get both gateways</span><span class="sxs-lookup"><span data-stu-id="e5e83-226">1. Get both gateways</span></span>
<span data-ttu-id="e5e83-227">Make sure you log in and connect to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="e5e83-227">Make sure you log in and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="e5e83-228">2. Create both connections</span><span class="sxs-lookup"><span data-stu-id="e5e83-228">2. Create both connections</span></span>
<span data-ttu-id="e5e83-229">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="e5e83-229">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="e5e83-230">Be sure to enable BGP for BOTH connections.</span><span class="sxs-lookup"><span data-stu-id="e5e83-230">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="e5e83-231">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span><span class="sxs-lookup"><span data-stu-id="e5e83-231">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed with dual redundancy:</span></span>

![active-active-v2v](./media/vpn-gateway-activeactive-rm-powershell/vnet-to-vnet.png)

## <a name ="aaupdate"></a><span data-ttu-id="e5e83-233">Update an existing VPN gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-233">Update an existing VPN gateway</span></span>

<span data-ttu-id="e5e83-234">This section helps you change an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span><span class="sxs-lookup"><span data-stu-id="e5e83-234">This section helps you change an existing Azure VPN gateway from active-standby to active-active mode, or vice versa.</span></span>

### <a name="change-an-active-standby-gateway-to-an-active-active-gateway"></a><span data-ttu-id="e5e83-235">Change an active-standby gateway to an active-active gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-235">Change an active-standby gateway to an active-active gateway</span></span>

<span data-ttu-id="e5e83-236">The following example converts an active-standby gateway into an active-active gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-236">The following example converts an active-standby gateway into an active-active gateway.</span></span> <span data-ttu-id="e5e83-237">When you change an active-standby gateway to active-active, you create another public IP address, then add a second Gateway IP configuration.</span><span class="sxs-lookup"><span data-stu-id="e5e83-237">When you change an active-standby gateway to active-active, you create another public IP address, then add a second Gateway IP configuration.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="e5e83-238">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="e5e83-238">1. Declare your variables</span></span>

<span data-ttu-id="e5e83-239">Replace the following parameters used for the examples with the settings that you require for your own configuration, then declare these variables.</span><span class="sxs-lookup"><span data-stu-id="e5e83-239">Replace the following parameters used for the examples with the settings that you require for your own configuration, then declare these variables.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$VNetName = "TestVNetAA1"
$RG = "TestVPNActiveActive01"
$GWIPName2 = "gwpip2"
$GWIPconf2 = "gw1ipconf2"
```

<span data-ttu-id="e5e83-240">After declaring the variables, you can copy and paste this example to your PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="e5e83-240">After declaring the variables, you can copy and paste this example to your PowerShell console.</span></span>

```powershell
$vnet = Get-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $RG
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$location = $gw.Location
```

#### <a name="2-create-the-public-ip-address-then-add-the-second-gateway-ip-configuration"></a><span data-ttu-id="e5e83-241">2. Create the public IP address, then add the second gateway IP configuration</span><span class="sxs-lookup"><span data-stu-id="e5e83-241">2. Create the public IP address, then add the second gateway IP configuration</span></span>

```powershell
$gwpip2 = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG -Location $location -AllocationMethod Dynamic
Add-AzureRmVirtualNetworkGatewayIpConfig -VirtualNetworkGateway $gw -Name $GWIPconf2 -Subnet $subnet -PublicIpAddress $gwpip2
```

#### <a name="3-enable-active-active-mode-and-update-the-gateway"></a><span data-ttu-id="e5e83-242">3. Enable active-active mode and update the gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-242">3. Enable active-active mode and update the gateway</span></span>

<span data-ttu-id="e5e83-243">In this step, you enable active-active mode and update the gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-243">In this step, you enable active-active mode and update the gateway.</span></span> <span data-ttu-id="e5e83-244">In the example, the VPN gateway is currently using a legacy Standard SKU.</span><span class="sxs-lookup"><span data-stu-id="e5e83-244">In the example, the VPN gateway is currently using a legacy Standard SKU.</span></span> <span data-ttu-id="e5e83-245">However, active-active does not support the Standard SKU.</span><span class="sxs-lookup"><span data-stu-id="e5e83-245">However, active-active does not support the Standard SKU.</span></span> <span data-ttu-id="e5e83-246">To resize the legacy SKU to one that is supported (in this case, HighPerformance), you simply specify the supported legacy SKU that you want to use.</span><span class="sxs-lookup"><span data-stu-id="e5e83-246">To resize the legacy SKU to one that is supported (in this case, HighPerformance), you simply specify the supported legacy SKU that you want to use.</span></span>

* <span data-ttu-id="e5e83-247">You can't change a legacy SKU to one of the new SKUs using this step.</span><span class="sxs-lookup"><span data-stu-id="e5e83-247">You can't change a legacy SKU to one of the new SKUs using this step.</span></span> <span data-ttu-id="e5e83-248">You can only resize a legacy SKU to another supported legacy SKU.</span><span class="sxs-lookup"><span data-stu-id="e5e83-248">You can only resize a legacy SKU to another supported legacy SKU.</span></span> <span data-ttu-id="e5e83-249">For example, you can't change the SKU from Standard to VpnGw1 (even though VpnGw1 is supported for active-active) because Standard is a legacy SKU and VpnGw1 is a current SKU.</span><span class="sxs-lookup"><span data-stu-id="e5e83-249">For example, you can't change the SKU from Standard to VpnGw1 (even though VpnGw1 is supported for active-active) because Standard is a legacy SKU and VpnGw1 is a current SKU.</span></span> <span data-ttu-id="e5e83-250">For more information about resizing and migrating SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span><span class="sxs-lookup"><span data-stu-id="e5e83-250">For more information about resizing and migrating SKUs, see [Gateway SKUs](vpn-gateway-about-vpngateways.md#gwsku).</span></span>

* <span data-ttu-id="e5e83-251">If you want to resize a current SKU, for example VpnGw1 to VpnGw3, you can do so using this step because the SKUs are in the same SKU family.</span><span class="sxs-lookup"><span data-stu-id="e5e83-251">If you want to resize a current SKU, for example VpnGw1 to VpnGw3, you can do so using this step because the SKUs are in the same SKU family.</span></span> <span data-ttu-id="e5e83-252">To do so, you would use the value: ```-GatewaySku VpnGw3```</span><span class="sxs-lookup"><span data-stu-id="e5e83-252">To do so, you would use the value: ```-GatewaySku VpnGw3```</span></span>

<span data-ttu-id="e5e83-253">When you are using this in your environment, if you don't need to resize the gateway, you won't need to specify the -GatewaySku.</span><span class="sxs-lookup"><span data-stu-id="e5e83-253">When you are using this in your environment, if you don't need to resize the gateway, you won't need to specify the -GatewaySku.</span></span> <span data-ttu-id="e5e83-254">Notice that in this step, you must set the gateway object in PowerShell to trigger the actual update.</span><span class="sxs-lookup"><span data-stu-id="e5e83-254">Notice that in this step, you must set the gateway object in PowerShell to trigger the actual update.</span></span> <span data-ttu-id="e5e83-255">This update can take 30 to 45 minutes, even if you are not resizing your gateway.</span><span class="sxs-lookup"><span data-stu-id="e5e83-255">This update can take 30 to 45 minutes, even if you are not resizing your gateway.</span></span>

```powershell
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -EnableActiveActiveFeature -GatewaySku HighPerformance
```

### <a name="change-an-active-active-gateway-to-an-active-standby-gateway"></a><span data-ttu-id="e5e83-256">Change an active-active gateway to an active-standby gateway</span><span class="sxs-lookup"><span data-stu-id="e5e83-256">Change an active-active gateway to an active-standby gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="e5e83-257">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="e5e83-257">1. Declare your variables</span></span>

<span data-ttu-id="e5e83-258">Replace the following parameters used for the examples with the settings that you require for your own configuration, then declare these variables.</span><span class="sxs-lookup"><span data-stu-id="e5e83-258">Replace the following parameters used for the examples with the settings that you require for your own configuration, then declare these variables.</span></span>

```powershell
$GWName = "TestVNetAA1GW"
$RG = "TestVPNActiveActive01"
```

<span data-ttu-id="e5e83-259">After declaring the variables, get the name of the IP configuration you want to remove.</span><span class="sxs-lookup"><span data-stu-id="e5e83-259">After declaring the variables, get the name of the IP configuration you want to remove.</span></span>

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name $GWName -ResourceGroupName $RG
$ipconfname = $gw.IpConfigurations[1].Name
```

#### <a name="2-remove-the-gateway-ip-configuration-and-disable-the-active-active-mode"></a><span data-ttu-id="e5e83-260">2. Remove the gateway IP configuration and disable the active-active mode</span><span class="sxs-lookup"><span data-stu-id="e5e83-260">2. Remove the gateway IP configuration and disable the active-active mode</span></span>

<span data-ttu-id="e5e83-261">Use this example to remove the gateway IP configuration and disable active-active mode.</span><span class="sxs-lookup"><span data-stu-id="e5e83-261">Use this example to remove the gateway IP configuration and disable active-active mode.</span></span> <span data-ttu-id="e5e83-262">Notice that you  must set the gateway object in PowerShell to trigger the actual update.</span><span class="sxs-lookup"><span data-stu-id="e5e83-262">Notice that you  must set the gateway object in PowerShell to trigger the actual update.</span></span>

```powershell
Remove-AzureRmVirtualNetworkGatewayIpConfig -Name $ipconfname -VirtualNetworkGateway $gw
Set-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw -DisableActiveActiveFeature
```

<span data-ttu-id="e5e83-263">This update can take up to 30 to  45 minutes.</span><span class="sxs-lookup"><span data-stu-id="e5e83-263">This update can take up to 30 to  45 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5e83-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="e5e83-264">Next steps</span></span>
<span data-ttu-id="e5e83-265">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="e5e83-265">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="e5e83-266">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span><span class="sxs-lookup"><span data-stu-id="e5e83-266">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>
