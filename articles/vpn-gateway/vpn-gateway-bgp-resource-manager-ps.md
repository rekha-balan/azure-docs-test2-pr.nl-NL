---
title: 'Configure BGP on Azure VPN Gateways: Resource Manager: PowerShell | Microsoft Docs'
description: This article walks you through configuring BGP with Azure VPN Gateways using Azure Resource Manager and PowerShell.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: azure-resource-manager
ms.assetid: 905b11a7-1333-482c-820b-0fd0f44238e5
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/12/2017
ms.author: yushwang
ms.openlocfilehash: d3130a891b8aae2c98ef508cb2572e7d577d67c0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670761"
---
# <a name="how-to-configure-bgp-on-azure-vpn-gateways-using-powershell"></a><span data-ttu-id="9e3d9-103">How to configure BGP on Azure VPN Gateways using PowerShell</span><span class="sxs-lookup"><span data-stu-id="9e3d9-103">How to configure BGP on Azure VPN Gateways using PowerShell</span></span>
<span data-ttu-id="9e3d9-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-104">This article walks you through the steps to enable BGP on a cross-premises Site-to-Site (S2S) VPN connection and a VNet-to-VNet connection using the Resource Manager deployment model and PowerShell.</span></span>

## <a name="about-bgp"></a><span data-ttu-id="9e3d9-105">About BGP</span><span class="sxs-lookup"><span data-stu-id="9e3d9-105">About BGP</span></span>
<span data-ttu-id="9e3d9-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-106">BGP is the standard routing protocol commonly used in the Internet to exchange routing and reachability information between two or more networks.</span></span> <span data-ttu-id="9e3d9-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-107">BGP enables the Azure VPN Gateways and your on-premises VPN devices, called BGP peers or neighbors, to exchange "routes" that will inform both gateways on the availability and reachability for those prefixes to go through the gateways or routers involved.</span></span> <span data-ttu-id="9e3d9-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-108">BGP can also enable transit routing among multiple networks by propagating routes a BGP gateway learns from one BGP peer to all other BGP peers.</span></span>

<span data-ttu-id="9e3d9-109">Please see [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-109">Please see [Overview of BGP with Azure VPN Gateways](vpn-gateway-bgp-overview.md) for more discussion on benefits of BGP and to understand the technical requirements and considerations of using BGP.</span></span>

## <a name="getting-started-with-bgp-on-azure-vpn-gateways"></a><span data-ttu-id="9e3d9-110">Getting started with BGP on Azure VPN gateways</span><span class="sxs-lookup"><span data-stu-id="9e3d9-110">Getting started with BGP on Azure VPN gateways</span></span>
<span data-ttu-id="9e3d9-111">This article will walk you through the steps to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-111">This article will walk you through the steps to do the following tasks:</span></span>

* [<span data-ttu-id="9e3d9-112">Part 1 - Enable BGP on your Azure VPN gateway</span><span class="sxs-lookup"><span data-stu-id="9e3d9-112">Part 1 - Enable BGP on your Azure VPN gateway</span></span>](#enablebgp)
* [<span data-ttu-id="9e3d9-113">Part 2 - Establish a cross-premises connection with BGP</span><span class="sxs-lookup"><span data-stu-id="9e3d9-113">Part 2 - Establish a cross-premises connection with BGP</span></span>](#crossprembgp)
* [<span data-ttu-id="9e3d9-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span><span class="sxs-lookup"><span data-stu-id="9e3d9-114">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>](#v2vbgp)

<span data-ttu-id="9e3d9-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-115">Each part of the instructions forms a basic building block for enabling BGP in your network connectivity.</span></span> <span data-ttu-id="9e3d9-116">If you complete all three parts, you will build the topology as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-116">If you complete all three parts, you will build the topology as shown in the following diagram:</span></span>

![BGP topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

<span data-ttu-id="9e3d9-118">You can combine these together to build a more complex, multi-hope, transit network that meet your needs.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-118">You can combine these together to build a more complex, multi-hope, transit network that meet your needs.</span></span>

## <a name ="enablebgp"></a><span data-ttu-id="9e3d9-119">Part 1 - Configure BGP on the Azure VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="9e3d9-119">Part 1 - Configure BGP on the Azure VPN Gateway</span></span>
<span data-ttu-id="9e3d9-120">The following configuration steps will setup the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-120">The following configuration steps will setup the BGP parameters of the Azure VPN gateway as shown in the following diagram:</span></span>

![BGP Gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-bgp-resource-manager-ps/bgp-gateway.png)

### <a name="before-you-begin"></a><span data-ttu-id="9e3d9-122">Before you begin</span><span class="sxs-lookup"><span data-stu-id="9e3d9-122">Before you begin</span></span>
* <span data-ttu-id="9e3d9-123">Verify that you have an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-123">Verify that you have an Azure subscription.</span></span> <span data-ttu-id="9e3d9-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9e3d9-124">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="9e3d9-125">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-125">You'll need to install the Azure Resource Manager PowerShell cmdlets.</span></span> <span data-ttu-id="9e3d9-126">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-126">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>

### <a name="step-1---create-and-configure-vnet1"></a><span data-ttu-id="9e3d9-127">Step 1 - Create and configure VNet1</span><span class="sxs-lookup"><span data-stu-id="9e3d9-127">Step 1 - Create and configure VNet1</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="9e3d9-128">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="9e3d9-128">1. Declare your variables</span></span>
<span data-ttu-id="9e3d9-129">For this exercise, we'll start by declaring our variables.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-129">For this exercise, we'll start by declaring our variables.</span></span> <span data-ttu-id="9e3d9-130">The example below declares the variables using the values for this exercise.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-130">The example below declares the variables using the values for this exercise.</span></span> <span data-ttu-id="9e3d9-131">Be sure to replace the values with your own when configuring for production.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-131">Be sure to replace the values with your own when configuring for production.</span></span> <span data-ttu-id="9e3d9-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-132">You can use these variables if you are running through the steps to become familiar with this type of configuration.</span></span> <span data-ttu-id="9e3d9-133">Modify the variables, and then copy and paste into your PowerShell console.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-133">Modify the variables, and then copy and paste into your PowerShell console.</span></span>

```powershell
$Sub1 = "Replace_With_Your_Subcription_Name"
$RG1 = "TestBGPRG1"
$Location1 = "East US"
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
$GWIPName1 = "VNet1GWIP"
$GWIPconfName1 = "gwipconf1"
$Connection12 = "VNet1toVNet2"
$Connection15 = "VNet1toSite5"
```

#### <a name="2-connect-to-your-subscription-and-create-a-new-resource-group"></a><span data-ttu-id="9e3d9-134">2. Connect to your subscription and create a new resource group</span><span class="sxs-lookup"><span data-stu-id="9e3d9-134">2. Connect to your subscription and create a new resource group</span></span>
<span data-ttu-id="9e3d9-135">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-135">Make sure you switch to PowerShell mode to use the Resource Manager cmdlets.</span></span> <span data-ttu-id="9e3d9-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9e3d9-136">For more information, see [Using Windows PowerShell with Resource Manager](../powershell-azure-resource-manager.md).</span></span>

<span data-ttu-id="9e3d9-137">Open your PowerShell console and connect to your account.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-137">Open your PowerShell console and connect to your account.</span></span> <span data-ttu-id="9e3d9-138">Use the following sample to help you connect:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-138">Use the following sample to help you connect:</span></span>

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $Sub1
New-AzureRmResourceGroup -Name $RG1 -Location $Location1
```

#### <a name="3-create-testvnet1"></a><span data-ttu-id="9e3d9-139">3. Create TestVNet1</span><span class="sxs-lookup"><span data-stu-id="9e3d9-139">3. Create TestVNet1</span></span>
<span data-ttu-id="9e3d9-140">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-140">The sample below creates a virtual network named TestVNet1 and three subnets, one called GatewaySubnet, one called FrontEnd, and one called Backend.</span></span> <span data-ttu-id="9e3d9-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-141">When substituting values, it's important that you always name your gateway subnet specifically GatewaySubnet.</span></span> <span data-ttu-id="9e3d9-142">If you name it something else, your gateway creation will fail.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-142">If you name it something else, your gateway creation will fail.</span></span>

```powershell
$fesub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName1 -AddressPrefix $FESubPrefix1 $besub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName1 -AddressPrefix $BESubPrefix1
$gwsub1 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName1 -AddressPrefix $GWSubPrefix1

New-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1 -Location $Location1 -AddressPrefix $VNetPrefix11,$VNetPrefix12 -Subnet $fesub1,$besub1,$gwsub1
```

### <a name="step-2---create-the-vpn-gateway-for-testvnet1-with-bgp-parameters"></a><span data-ttu-id="9e3d9-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span><span class="sxs-lookup"><span data-stu-id="9e3d9-143">Step 2 - Create the VPN Gateway for TestVNet1 with BGP parameters</span></span>
#### <a name="1-create-the-ip-and-subnet-configurations"></a><span data-ttu-id="9e3d9-144">1. Create the IP and subnet configurations</span><span class="sxs-lookup"><span data-stu-id="9e3d9-144">1. Create the IP and subnet configurations</span></span>
<span data-ttu-id="9e3d9-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-145">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="9e3d9-146">You'll also define the subnet and IP configurations required.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-146">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gwpip1 = New-AzureRmPublicIpAddress -Name $GWIPName1 -ResourceGroupName $RG1 -Location $Location1 -AllocationMethod Dynamic

$vnet1 = Get-AzureRmVirtualNetwork -Name $VNetName1 -ResourceGroupName $RG1
$subnet1 = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet1
$gwipconf1 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName1 -Subnet $subnet1 -PublicIpAddress $gwpip1
```

#### <a name="2-create-the-vpn-gateway-with-the-as-number"></a><span data-ttu-id="9e3d9-147">2. Create the VPN gateway with the AS number</span><span class="sxs-lookup"><span data-stu-id="9e3d9-147">2. Create the VPN gateway with the AS number</span></span>
<span data-ttu-id="9e3d9-148">Create the virtual network gateway for TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-148">Create the virtual network gateway for TestVNet1.</span></span> <span data-ttu-id="9e3d9-149">Note that BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-149">Note that BGP requires a Route-Based VPN gateway, and also the addition parameter, -Asn, to set the ASN (AS Number) for TestVNet1.</span></span> <span data-ttu-id="9e3d9-150">Creating a gateway can take a while (30 minutes or more to complete).</span><span class="sxs-lookup"><span data-stu-id="9e3d9-150">Creating a gateway can take a while (30 minutes or more to complete).</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1 -Location $Location1 -IpConfigurations $gwipconf1 -GatewayType Vpn -VpnType RouteBased -GatewaySku HighPerformance -Asn $VNet1ASN
```

#### <a name="3-obtain-the-azure-bgp-peer-ip-address"></a><span data-ttu-id="9e3d9-151">3. Obtain the Azure BGP Peer IP address</span><span class="sxs-lookup"><span data-stu-id="9e3d9-151">3. Obtain the Azure BGP Peer IP address</span></span>
<span data-ttu-id="9e3d9-152">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-152">Once the gateway is created, you will need to obtain the BGP Peer IP address on the Azure VPN Gateway.</span></span> <span data-ttu-id="9e3d9-153">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-153">This address is needed to configure the Azure VPN Gateway as a BGP Peer for your on-premises VPN devices.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet1gw.BgpSettingsText
```

<span data-ttu-id="9e3d9-154">The last command will show the corresponding BGP configurations on the Azure VPN Gateway; for example:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-154">The last command will show the corresponding BGP configurations on the Azure VPN Gateway; for example:</span></span>

```powershell
    $vnet1gw.BgpSettingsText
    {
        "Asn": 65010,
        "BgpPeeringAddress": "10.12.255.30",
        "PeerWeight": 0
    }
```

<span data-ttu-id="9e3d9-155">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-155">Once the gateway is created, you can use this gateway to establish cross-premises connection or VNet-to-VNet connection with BGP.</span></span> <span data-ttu-id="9e3d9-156">The following sections will walk through the steps to complete the exercise.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-156">The following sections will walk through the steps to complete the exercise.</span></span>

## <a name ="crossprembbgp"></a><span data-ttu-id="9e3d9-157">Part 2 - Establish a cross-premises connection with BGP</span><span class="sxs-lookup"><span data-stu-id="9e3d9-157">Part 2 - Establish a cross-premises connection with BGP</span></span>
<span data-ttu-id="9e3d9-158">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-158">To establish a cross-premises connection, you need to create a Local Network Gateway to represent your on-premises VPN device, and a Connection to connect the Azure VPN gateway with the local network gateway.</span></span> <span data-ttu-id="9e3d9-159">The difference between the instructions in this article is the additional properties required to specify the BGP configuration parameters.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-159">The difference between the instructions in this article is the additional properties required to specify the BGP configuration parameters.</span></span>

![BGP for Cross-Premises](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-bgp-resource-manager-ps/bgp-crossprem.png)

<span data-ttu-id="9e3d9-161">Before proceeding, please make sure you have completed [Part 1](#enablebgp) of this exercise.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-161">Before proceeding, please make sure you have completed [Part 1](#enablebgp) of this exercise.</span></span>

### <a name="step-1---create-and-configure-the-local-network-gateway"></a><span data-ttu-id="9e3d9-162">Step 1 - Create and configure the local network gateway</span><span class="sxs-lookup"><span data-stu-id="9e3d9-162">Step 1 - Create and configure the local network gateway</span></span>
#### <a name="1-declare-your-variables"></a><span data-ttu-id="9e3d9-163">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="9e3d9-163">1. Declare your variables</span></span>
<span data-ttu-id="9e3d9-164">This exercise will continue to build the configuration shown in the diagram.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-164">This exercise will continue to build the configuration shown in the diagram.</span></span> <span data-ttu-id="9e3d9-165">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-165">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG5 = "TestBGPRG5"
$Location5 = "East US 2"
$LNGName5 = "Site5"
$LNGPrefix50 = "10.52.255.254/32"
$LNGIP5 = "Your_VPN_Device_IP"
$LNGASN5 = 65050
$BGPPeerIP5 = "10.52.255.254"
```

<span data-ttu-id="9e3d9-166">A couple of things to note regarding the local network gateway parameters:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-166">A couple of things to note regarding the local network gateway parameters:</span></span>

* <span data-ttu-id="9e3d9-167">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-167">The local network gateway can be in the same or different location and resource group as the VPN gateway.</span></span> <span data-ttu-id="9e3d9-168">This example shows them in different resource groups in different locations.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-168">This example shows them in different resource groups in different locations.</span></span>
* <span data-ttu-id="9e3d9-169">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-169">The minimum prefix you need to declare for the local network gateway is the host address of your BGP Peer IP address on your VPN device.</span></span> <span data-ttu-id="9e3d9-170">In this case, it's a /32 prefix of "10.52.255.254/32".</span><span class="sxs-lookup"><span data-stu-id="9e3d9-170">In this case, it's a /32 prefix of "10.52.255.254/32".</span></span>
* <span data-ttu-id="9e3d9-171">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-171">As a reminder, you must use different BGP ASNs between your on-premises networks and Azure VNet.</span></span> <span data-ttu-id="9e3d9-172">If they are the same, you need to change your VNet ASN if your on-premises VPN device already use the ASN to peer with other BGP neighbors.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-172">If they are the same, you need to change your VNet ASN if your on-premises VPN device already use the ASN to peer with other BGP neighbors.</span></span>

<span data-ttu-id="9e3d9-173">Before you continue, please make sure you are still connected to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-173">Before you continue, please make sure you are still connected to Subscription 1.</span></span>

#### <a name="2-create-the-local-network-gateway-for-site5"></a><span data-ttu-id="9e3d9-174">2. Create the local network gateway for Site5</span><span class="sxs-lookup"><span data-stu-id="9e3d9-174">2. Create the local network gateway for Site5</span></span>
<span data-ttu-id="9e3d9-175">Be sure to create the resource group if it is not created, before you create the local network gateway.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-175">Be sure to create the resource group if it is not created, before you create the local network gateway.</span></span> <span data-ttu-id="9e3d9-176">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-176">Notice the two additional parameters for the local network gateway: Asn and BgpPeerAddress.</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG5 -Location $Location5

New-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5 -Location $Location5 -GatewayIpAddress $LNGIP5 -AddressPrefix $LNGPrefix50 -Asn $LNGASN5 -BgpPeeringAddress $BGPPeerIP5
```

### <a name="step-2---connect-the-vnet-gateway-and-local-network-gateway"></a><span data-ttu-id="9e3d9-177">Step 2 - Connect the VNet gateway and local network gateway</span><span class="sxs-lookup"><span data-stu-id="9e3d9-177">Step 2 - Connect the VNet gateway and local network gateway</span></span>
#### <a name="1-get-the-two-gateways"></a><span data-ttu-id="9e3d9-178">1. Get the two gateways</span><span class="sxs-lookup"><span data-stu-id="9e3d9-178">1. Get the two gateways</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1  -ResourceGroupName $RG1
$lng5gw  = Get-AzureRmLocalNetworkGateway -Name $LNGName5 -ResourceGroupName $RG5
```

#### <a name="2-create-the-testvnet1-to-site5-connection"></a><span data-ttu-id="9e3d9-179">2. Create the TestVNet1 to Site5 connection</span><span class="sxs-lookup"><span data-stu-id="9e3d9-179">2. Create the TestVNet1 to Site5 connection</span></span>
<span data-ttu-id="9e3d9-180">In this step, you will create the connection from TestVNet1 to Site5.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-180">In this step, you will create the connection from TestVNet1 to Site5.</span></span> <span data-ttu-id="9e3d9-181">You must specify "-EnableBGP $True" to enable BGP for this connection.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-181">You must specify "-EnableBGP $True" to enable BGP for this connection.</span></span> <span data-ttu-id="9e3d9-182">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-182">As discussed earlier, it is possible to have both BGP and non-BGP connections for the same Azure VPN Gateway.</span></span> <span data-ttu-id="9e3d9-183">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-183">Unless BGP is enabled in the connection property, Azure will not enable BGP for this connection even though BGP parameters are already configured on both gateways.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection15 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -LocalNetworkGateway2 $lng5gw -Location $Location1 -ConnectionType IPsec -SharedKey 'AzureA1b2C3' -EnableBGP $True
```


<span data-ttu-id="9e3d9-184">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-184">The example below lists the parameters you will enter into the BGP configuration section on your on-premises VPN device for this exercise:</span></span>

    - <span data-ttu-id="9e3d9-185">Site5 ASN            : 65050</span><span class="sxs-lookup"><span data-stu-id="9e3d9-185">Site5 ASN            : 65050</span></span>
    - <span data-ttu-id="9e3d9-186">Site5 BGP IP         : 10.52.255.254</span><span class="sxs-lookup"><span data-stu-id="9e3d9-186">Site5 BGP IP         : 10.52.255.254</span></span>
    - <span data-ttu-id="9e3d9-187">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span><span class="sxs-lookup"><span data-stu-id="9e3d9-187">Prefixes to announce : (for example) 10.51.0.0/16 and 10.52.0.0/16</span></span>
    - <span data-ttu-id="9e3d9-188">Azure VNet ASN       : 65010</span><span class="sxs-lookup"><span data-stu-id="9e3d9-188">Azure VNet ASN       : 65010</span></span>
    - <span data-ttu-id="9e3d9-189">Azure VNet BGP IP    : 10.12.255.30</span><span class="sxs-lookup"><span data-stu-id="9e3d9-189">Azure VNet BGP IP    : 10.12.255.30</span></span>
    - <span data-ttu-id="9e3d9-190">Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device</span><span class="sxs-lookup"><span data-stu-id="9e3d9-190">Static route         : Add a route for 10.12.255.30/32, with nexthop being the VPN tunnel interface on your device</span></span>
    - <span data-ttu-id="9e3d9-191">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span><span class="sxs-lookup"><span data-stu-id="9e3d9-191">eBGP Multihop        : Ensure the "multihop" option for eBGP is enabled on your device if needed</span></span>

<span data-ttu-id="9e3d9-192">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-192">The connection should be established after a few minutes, and the BGP peering session will start once the IPsec connection is established.</span></span>

## <a name ="v2vbgp"></a><span data-ttu-id="9e3d9-193">Part 3 - Establish a VNet-to-VNet connection with BGP</span><span class="sxs-lookup"><span data-stu-id="9e3d9-193">Part 3 - Establish a VNet-to-VNet connection with BGP</span></span>
<span data-ttu-id="9e3d9-194">This section adds a VNet-to-VNet connection with BGP, as shown in the diagram below.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-194">This section adds a VNet-to-VNet connection with BGP, as shown in the diagram below.</span></span> 

![BGP for VNet-to-VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-bgp-resource-manager-ps/bgp-vnet2vnet.png)

<span data-ttu-id="9e3d9-196">The instructions below continue from the previous steps listed above.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-196">The instructions below continue from the previous steps listed above.</span></span> <span data-ttu-id="9e3d9-197">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-197">You must complete [Part I](#enablebgp) to create and configure TestVNet1 and the VPN Gateway with BGP.</span></span> 

### <a name="step-1---create-testvnet2-and-the-vpn-gateway"></a><span data-ttu-id="9e3d9-198">Step 1 - Create TestVNet2 and the VPN gateway</span><span class="sxs-lookup"><span data-stu-id="9e3d9-198">Step 1 - Create TestVNet2 and the VPN gateway</span></span>
<span data-ttu-id="9e3d9-199">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-199">It is important to make sure that the IP address space of the new virtual network, TestVNet2, does not overlap with any of your VNet ranges.</span></span>

<span data-ttu-id="9e3d9-200">In this example, the virtual networks belong to the same subscription.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-200">In this example, the virtual networks belong to the same subscription.</span></span> <span data-ttu-id="9e3d9-201">You can setup VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-201">You can setup VNet-to-VNet connections between different subscriptions; please refer to [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md) to learn more details.</span></span> <span data-ttu-id="9e3d9-202">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-202">Make sure you add the "-EnableBgp $True" when creating the connections to enable BGP.</span></span>

#### <a name="1-declare-your-variables"></a><span data-ttu-id="9e3d9-203">1. Declare your variables</span><span class="sxs-lookup"><span data-stu-id="9e3d9-203">1. Declare your variables</span></span>
<span data-ttu-id="9e3d9-204">Be sure to replace the values with the ones that you want to use for your configuration.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-204">Be sure to replace the values with the ones that you want to use for your configuration.</span></span>

```powershell
$RG2 = "TestBGPRG2"
$Location2 = "West US"
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
$GWIPName2 = "VNet2GWIP"
$GWIPconfName2 = "gwipconf2"
$Connection21 = "VNet2toVNet1"
$Connection12 = "VNet1toVNet2"
```

#### <a name="2-create-testvnet2-in-the-new-resource-group"></a><span data-ttu-id="9e3d9-205">2. Create TestVNet2 in the new resource group</span><span class="sxs-lookup"><span data-stu-id="9e3d9-205">2. Create TestVNet2 in the new resource group</span></span>

```powershell
New-AzureRmResourceGroup -Name $RG2 -Location $Location2

$fesub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $FESubName2 -AddressPrefix $FESubPrefix2
$besub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $BESubName2 -AddressPrefix $BESubPrefix2
$gwsub2 = New-AzureRmVirtualNetworkSubnetConfig -Name $GWSubName2 -AddressPrefix $GWSubPrefix2

New-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2 -Location $Location2 -AddressPrefix $VNetPrefix21,$VNetPrefix22 -Subnet $fesub2,$besub2,$gwsub2
```

#### <a name="3-create-the-vpn-gateway-for-testvnet2-with-bgp-parameters"></a><span data-ttu-id="9e3d9-206">3. Create the VPN gateway for TestVNet2 with BGP parameters</span><span class="sxs-lookup"><span data-stu-id="9e3d9-206">3. Create the VPN gateway for TestVNet2 with BGP parameters</span></span>
<span data-ttu-id="9e3d9-207">Request a public IP address to be allocated to the gateway you will create for your VNet.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-207">Request a public IP address to be allocated to the gateway you will create for your VNet.</span></span> <span data-ttu-id="9e3d9-208">You'll also define the subnet and IP configurations required.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-208">You'll also define the subnet and IP configurations required.</span></span>

```powershell
$gwpip2    = New-AzureRmPublicIpAddress -Name $GWIPName2 -ResourceGroupName $RG2 -Location $Location2 -AllocationMethod Dynamic

$vnet2     = Get-AzureRmVirtualNetwork -Name $VNetName2 -ResourceGroupName $RG2
$subnet2   = Get-AzureRmVirtualNetworkSubnetConfig -Name "GatewaySubnet" -VirtualNetwork $vnet2
$gwipconf2 = New-AzureRmVirtualNetworkGatewayIpConfig -Name $GWIPconfName2 -Subnet $subnet2 -PublicIpAddress $gwpip2
```

<span data-ttu-id="9e3d9-209">Create the VPN gateway with the AS number.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-209">Create the VPN gateway with the AS number.</span></span> <span data-ttu-id="9e3d9-210">Note that you must override the default ASN on your Azure VPN gateways.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-210">Note that you must override the default ASN on your Azure VPN gateways.</span></span> <span data-ttu-id="9e3d9-211">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-211">The ASNs for the connected VNets must be different to enable BGP and transit routing.</span></span>

```powershell
New-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2 -Location $Location2 -IpConfigurations $gwipconf2 -GatewayType Vpn -VpnType RouteBased -GatewaySku Standard -Asn $VNet2ASN
```

### <a name="step-2---connect-the-testvnet1-and-testvnet2-gateways"></a><span data-ttu-id="9e3d9-212">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span><span class="sxs-lookup"><span data-stu-id="9e3d9-212">Step 2 - Connect the TestVNet1 and TestVNet2 gateways</span></span>
<span data-ttu-id="9e3d9-213">In this example, both gateways are in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-213">In this example, both gateways are in the same subscription.</span></span> <span data-ttu-id="9e3d9-214">You can complete this step in the same PowerShell session.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-214">You can complete this step in the same PowerShell session.</span></span>

#### <a name="1-get-both-gateways"></a><span data-ttu-id="9e3d9-215">1. Get both gateways</span><span class="sxs-lookup"><span data-stu-id="9e3d9-215">1. Get both gateways</span></span>
<span data-ttu-id="9e3d9-216">Make sure you login and connect to Subscription 1.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-216">Make sure you login and connect to Subscription 1.</span></span>

```powershell
$vnet1gw = Get-AzureRmVirtualNetworkGateway -Name $GWName1 -ResourceGroupName $RG1
$vnet2gw = Get-AzureRmVirtualNetworkGateway -Name $GWName2 -ResourceGroupName $RG2
```

#### <a name="2-create-both-connections"></a><span data-ttu-id="9e3d9-217">2. Create both connections</span><span class="sxs-lookup"><span data-stu-id="9e3d9-217">2. Create both connections</span></span>
<span data-ttu-id="9e3d9-218">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-218">In this step, you will create the connection from TestVNet1 to TestVNet2, and the connection from TestVNet2 to TestVNet1.</span></span>

```powershell
New-AzureRmVirtualNetworkGatewayConnection -Name $Connection12 -ResourceGroupName $RG1 -VirtualNetworkGateway1 $vnet1gw -VirtualNetworkGateway2 $vnet2gw -Location $Location1 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True

New-AzureRmVirtualNetworkGatewayConnection -Name $Connection21 -ResourceGroupName $RG2 -VirtualNetworkGateway1 $vnet2gw -VirtualNetworkGateway2 $vnet1gw -Location $Location2 -ConnectionType Vnet2Vnet -SharedKey 'AzureA1b2C3' -EnableBgp $True
```

> [!IMPORTANT]
> <span data-ttu-id="9e3d9-219">Be sure to enable BGP for BOTH connections.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-219">Be sure to enable BGP for BOTH connections.</span></span>
> 
> 

<span data-ttu-id="9e3d9-220">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-220">After completing these steps, the connection will be establish in a few minutes, and the BGP peering session will be up once the VNet-to-VNet connection is completed.</span></span>

<span data-ttu-id="9e3d9-221">If you have completed all three parts of this exercise, you will have established a network topology as shown below:</span><span class="sxs-lookup"><span data-stu-id="9e3d9-221">If you have completed all three parts of this exercise, you will have established a network topology as shown below:</span></span>

![BGP for VNet-to-VNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-bgp-resource-manager-ps/bgp-crosspremv2v.png)

## <a name="next-steps"></a><span data-ttu-id="9e3d9-223">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e3d9-223">Next steps</span></span>
<span data-ttu-id="9e3d9-224">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-224">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="9e3d9-225">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span><span class="sxs-lookup"><span data-stu-id="9e3d9-225">See [Create a Virtual Machine](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) for steps.</span></span>






