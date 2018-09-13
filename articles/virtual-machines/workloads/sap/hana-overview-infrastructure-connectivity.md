---
title: Infrastructure and Connectivity to SAP HANA on Azure (Large Instances) | Microsoft Docs
description: Configure required connectivity infrastructure to use SAP HANA on Azure (Large Instances).
services: virtual-machines-linux
documentationcenter: ''
author: RicksterCDN
manager: timlt
editor: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b5b3347ea73e939196f4bca778c2abd67f0737c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552067"
---
# <a name="sap-hana-large-instances-infrastructure-and-connectivity-on-azure"></a><span data-ttu-id="124ad-103">SAP HANA (large instances) infrastructure and connectivity on Azure</span><span class="sxs-lookup"><span data-stu-id="124ad-103">SAP HANA (large instances) infrastructure and connectivity on Azure</span></span> 

<span data-ttu-id="124ad-104">After the purchase of SAP HANA on Azure (Large Instances) is finalized between you and the Microsoft enterprise account team, the following information is required:</span><span class="sxs-lookup"><span data-stu-id="124ad-104">After the purchase of SAP HANA on Azure (Large Instances) is finalized between you and the Microsoft enterprise account team, the following information is required:</span></span>

- <span data-ttu-id="124ad-105">Customer name</span><span class="sxs-lookup"><span data-stu-id="124ad-105">Customer name</span></span>
- <span data-ttu-id="124ad-106">Business contact information (including e-mail address and phone number)</span><span class="sxs-lookup"><span data-stu-id="124ad-106">Business contact information (including e-mail address and phone number)</span></span>
- <span data-ttu-id="124ad-107">Technical contact information (including e-mail address and phone number)</span><span class="sxs-lookup"><span data-stu-id="124ad-107">Technical contact information (including e-mail address and phone number)</span></span>
- <span data-ttu-id="124ad-108">Technical networking contact information (including e-mail address and phone number)</span><span class="sxs-lookup"><span data-stu-id="124ad-108">Technical networking contact information (including e-mail address and phone number)</span></span>
- <span data-ttu-id="124ad-109">Azure deployment region (West US or East US as of September 2016)</span><span class="sxs-lookup"><span data-stu-id="124ad-109">Azure deployment region (West US or East US as of September 2016)</span></span>
- <span data-ttu-id="124ad-110">Confirm SAP HANA on Azure (Large Instances) SKU (configuration)</span><span class="sxs-lookup"><span data-stu-id="124ad-110">Confirm SAP HANA on Azure (Large Instances) SKU (configuration)</span></span>
- <span data-ttu-id="124ad-111">For every Azure Region being deployed to:</span><span class="sxs-lookup"><span data-stu-id="124ad-111">For every Azure Region being deployed to:</span></span>
  - <span data-ttu-id="124ad-112">A /29 IP address range for P2P Connections</span><span class="sxs-lookup"><span data-stu-id="124ad-112">A /29 IP address range for P2P Connections</span></span>
  - <span data-ttu-id="124ad-113">A CIDR Block (used for the HANA Large Instances NAT pool; /24 recommended)</span><span class="sxs-lookup"><span data-stu-id="124ad-113">A CIDR Block (used for the HANA Large Instances NAT pool; /24 recommended)</span></span>
- <span data-ttu-id="124ad-114">For every Azure VNet connecting to HANA Large Instances, independent of the Azure region:</span><span class="sxs-lookup"><span data-stu-id="124ad-114">For every Azure VNet connecting to HANA Large Instances, independent of the Azure region:</span></span>
  - <span data-ttu-id="124ad-115">One or more /28s or /27 IP address ranges (for customer VNet gateway subnet)</span><span class="sxs-lookup"><span data-stu-id="124ad-115">One or more /28s or /27 IP address ranges (for customer VNet gateway subnet)</span></span>
  - <span data-ttu-id="124ad-116">One or more CIDR blocks (for customer VNet tenant subnet; /24 recommended)</span><span class="sxs-lookup"><span data-stu-id="124ad-116">One or more CIDR blocks (for customer VNet tenant subnet; /24 recommended)</span></span>
- <span data-ttu-id="124ad-117">Data for each of HANA Large Instances system:</span><span class="sxs-lookup"><span data-stu-id="124ad-117">Data for each of HANA Large Instances system:</span></span>
  - <span data-ttu-id="124ad-118">Desired hostname</span><span class="sxs-lookup"><span data-stu-id="124ad-118">Desired hostname</span></span>
  - <span data-ttu-id="124ad-119">Desired IP address from the NAT pool</span><span class="sxs-lookup"><span data-stu-id="124ad-119">Desired IP address from the NAT pool</span></span>
- <span data-ttu-id="124ad-120">Azure subscription number for the Azure subscription to which SAP HANA on Azure HANA Large Instances will be directly connected</span><span class="sxs-lookup"><span data-stu-id="124ad-120">Azure subscription number for the Azure subscription to which SAP HANA on Azure HANA Large Instances will be directly connected</span></span>
- <span data-ttu-id="124ad-121">SAP HANA SID name for the SAP HANA instance (required to create the necessary SAP HANA-related disk volumes)</span><span class="sxs-lookup"><span data-stu-id="124ad-121">SAP HANA SID name for the SAP HANA instance (required to create the necessary SAP HANA-related disk volumes)</span></span>

<span data-ttu-id="124ad-122">After you provide the information, Microsoft provisions SAP HANA on Azure (Large Instances).</span><span class="sxs-lookup"><span data-stu-id="124ad-122">After you provide the information, Microsoft provisions SAP HANA on Azure (Large Instances).</span></span>

<span data-ttu-id="124ad-123">Networking setup information is then provided to you for:</span><span class="sxs-lookup"><span data-stu-id="124ad-123">Networking setup information is then provided to you for:</span></span>

- <span data-ttu-id="124ad-124">Connecting your Azure VNet(s) to the ExpressRoute circuit that connects Azure VNets to HANA Large Instances</span><span class="sxs-lookup"><span data-stu-id="124ad-124">Connecting your Azure VNet(s) to the ExpressRoute circuit that connects Azure VNets to HANA Large Instances</span></span>
  - <span data-ttu-id="124ad-125">For Azure Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="124ad-125">For Azure Resource Manager:</span></span>
     - <span data-ttu-id="124ad-126">Authorization key(s)</span><span class="sxs-lookup"><span data-stu-id="124ad-126">Authorization key(s)</span></span>
     - <span data-ttu-id="124ad-127">ExpressRoute PeerID</span><span class="sxs-lookup"><span data-stu-id="124ad-127">ExpressRoute PeerID</span></span>
- <span data-ttu-id="124ad-128">Accessing HANA Large Instances with the established ExpressRoute circuit and Azure VNet</span><span class="sxs-lookup"><span data-stu-id="124ad-128">Accessing HANA Large Instances with the established ExpressRoute circuit and Azure VNet</span></span>

## <a name="creating-an-azure-vnet"></a><span data-ttu-id="124ad-129">Creating an Azure VNet</span><span class="sxs-lookup"><span data-stu-id="124ad-129">Creating an Azure VNet</span></span>

<span data-ttu-id="124ad-130">This Azure VNet should be created using the Azure Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="124ad-130">This Azure VNet should be created using the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="124ad-131">The old Azure deployment model, commonly known as ASM, is not supported for this solution.</span><span class="sxs-lookup"><span data-stu-id="124ad-131">The old Azure deployment model, commonly known as ASM, is not supported for this solution.</span></span>

<span data-ttu-id="124ad-132">The Azure VNet that&#39;s created should have at least one tenant subnet and a gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="124ad-132">The Azure VNet that&#39;s created should have at least one tenant subnet and a gateway subnet.</span></span> <span data-ttu-id="124ad-133">These should be assigned the IP address ranges as specified, and submitted to Microsoft.</span><span class="sxs-lookup"><span data-stu-id="124ad-133">These should be assigned the IP address ranges as specified, and submitted to Microsoft.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="124ad-134">Only tenant and gateway address blocks should be assigned to the VNet in the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="124ad-134">Only tenant and gateway address blocks should be assigned to the VNet in the Azure subscription.</span></span> <span data-ttu-id="124ad-135">P2P and NAT pool address blocks must be separate from the VNet and Subnet address spaces as they exist outside of the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="124ad-135">P2P and NAT pool address blocks must be separate from the VNet and Subnet address spaces as they exist outside of the Azure subscription.</span></span>

<span data-ttu-id="124ad-136">Multiple tenant subnets may be used (even utilizing non-contiguous address ranges), but as mentioned previously, these address ranges must be submitted to Microsoft beforehand.</span><span class="sxs-lookup"><span data-stu-id="124ad-136">Multiple tenant subnets may be used (even utilizing non-contiguous address ranges), but as mentioned previously, these address ranges must be submitted to Microsoft beforehand.</span></span>

<span data-ttu-id="124ad-137">You can use any naming standard you like for these tenant subnets.</span><span class="sxs-lookup"><span data-stu-id="124ad-137">You can use any naming standard you like for these tenant subnets.</span></span> <span data-ttu-id="124ad-138">However, **there must always be one, and only one, gateway subnet for each VNet** that connects to the SAP HANA on Azure (Large Instances) ExpressRoute circuit, and **this gateway subnet must always be named &quot;GatewaySubnet&quot;** to ensure proper placement of the ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="124ad-138">However, **there must always be one, and only one, gateway subnet for each VNet** that connects to the SAP HANA on Azure (Large Instances) ExpressRoute circuit, and **this gateway subnet must always be named &quot;GatewaySubnet&quot;** to ensure proper placement of the ExpressRoute gateway.</span></span>

> [!WARNING] 
> <span data-ttu-id="124ad-139">It is critical that the gateway subnet always be named &quot;GatewaySubnet&quot;.</span><span class="sxs-lookup"><span data-stu-id="124ad-139">It is critical that the gateway subnet always be named &quot;GatewaySubnet&quot;.</span></span>

<span data-ttu-id="124ad-140">The VNet can be created using the Azure Portal, PowerShell, Azure template, or Azure CLI (see [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span><span class="sxs-lookup"><span data-stu-id="124ad-140">The VNet can be created using the Azure Portal, PowerShell, Azure template, or Azure CLI (see [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)).</span></span>

## <a name="creating-a-gateway-subnet"></a><span data-ttu-id="124ad-141">Creating a gateway subnet</span><span class="sxs-lookup"><span data-stu-id="124ad-141">Creating a gateway subnet</span></span>

<span data-ttu-id="124ad-142">Once the Azure VNet is created, an ExpressRoute gateway must be created on the VNet to link the VNet to the ExpressRoute circuit that connects to the customer tenant on the Large Instance stamp.</span><span class="sxs-lookup"><span data-stu-id="124ad-142">Once the Azure VNet is created, an ExpressRoute gateway must be created on the VNet to link the VNet to the ExpressRoute circuit that connects to the customer tenant on the Large Instance stamp.</span></span>

> [!NOTE] 
> <span data-ttu-id="124ad-143">This step can take up to 30 minutes to complete, as the new gateway is created in the designated Azure subscription and then connected to the specified Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="124ad-143">This step can take up to 30 minutes to complete, as the new gateway is created in the designated Azure subscription and then connected to the specified Azure VNet.</span></span>

<span data-ttu-id="124ad-144">If a gateway already exists, check whether it is an ExpressRoute gateway or not.</span><span class="sxs-lookup"><span data-stu-id="124ad-144">If a gateway already exists, check whether it is an ExpressRoute gateway or not.</span></span> <span data-ttu-id="124ad-145">If not, the gateway must be deleted and recreated as an ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="124ad-145">If not, the gateway must be deleted and recreated as an ExpressRoute gateway.</span></span> <span data-ttu-id="124ad-146">If an ExpressRoute gateway is already established, since the Azure VNet is already connected to the ExpressRoute circuit for on-premises connectivity, proceed to the Linking VNets section below.</span><span class="sxs-lookup"><span data-stu-id="124ad-146">If an ExpressRoute gateway is already established, since the Azure VNet is already connected to the ExpressRoute circuit for on-premises connectivity, proceed to the Linking VNets section below.</span></span>

- <span data-ttu-id="124ad-147">Use either the (new) [Azure Portal](https://portal.azure.com/) or PowerShell to create an ExpressRoute VPN gateway connected to your VNet.</span><span class="sxs-lookup"><span data-stu-id="124ad-147">Use either the (new) [Azure Portal](https://portal.azure.com/) or PowerShell to create an ExpressRoute VPN gateway connected to your VNet.</span></span>
  - <span data-ttu-id="124ad-148">If you use Azure Portal, add a new **Virtual Network Gateway** and then select **ExpressRoute** as the gateway type.</span><span class="sxs-lookup"><span data-stu-id="124ad-148">If you use Azure Portal, add a new **Virtual Network Gateway** and then select **ExpressRoute** as the gateway type.</span></span>
  - <span data-ttu-id="124ad-149">If you chose PowerShell instead, first download and use the latest [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) to ensure an optimal experience.</span><span class="sxs-lookup"><span data-stu-id="124ad-149">If you chose PowerShell instead, first download and use the latest [Azure PowerShell SDK](https://azure.microsoft.com/downloads/) to ensure an optimal experience.</span></span> <span data-ttu-id="124ad-150">The following commands create an ExpressRoute gateway.</span><span class="sxs-lookup"><span data-stu-id="124ad-150">The following commands create an ExpressRoute gateway.</span></span> <span data-ttu-id="124ad-151">The text preceded by a _$_ are user defined variables that need to be updated with your specific information.</span><span class="sxs-lookup"><span data-stu-id="124ad-151">The text preceded by a _$_ are user defined variables that need to be updated with your specific information.</span></span>

```
# These Values should already exist, update to match your environment
$myAzureRegion = "eastus"
$myGroupName = "SAP-East-Coast"
$myVNetName = "VNet01"

# These values are used to create the gateway, update for how you wish the GW components to be named
$myGWName = "VNet01GW"
$myGWConfig = "VNet01GWConfig"
$myGWPIPName = "VNet01GWPIP"
$myGWSku = "HighPerformance" # Supported values for HANA Large Instances are: HighPerformance or UltraPerformance

# These Commands create the Public IP and ExpressRoute Gateway
$vnet = Get-AzureRmVirtualNetwork -Name $myVNetName -ResourceGroupName $myGroupName
$subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name 'GatewaySubnet' -VirtualNetwork $vnet
New-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName `
-Location $myAzureRegion -AllocationMethod Dynamic
$gwpip = Get-AzureRmPublicIpAddress -Name $myGWPIPName -ResourceGroupName $myGroupName
$gwipconfig = New-AzureRmVirtualNetworkGatewayIpConfig -Name $myGWConfig -SubnetId $subnet.Id `
-PublicIpAddressId $gwpip.Id

New-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName -Location $myAzureRegion `
-IpConfigurations $gwipconfig -GatewayType ExpressRoute `
-GatewaySku $myGWSku -VpnType PolicyBased -EnableBgp $true
```

<span data-ttu-id="124ad-152">In this example, HighPerformance gateway SKU was used.</span><span class="sxs-lookup"><span data-stu-id="124ad-152">In this example, HighPerformance gateway SKU was used.</span></span> <span data-ttu-id="124ad-153">Your options are HighPerformance or UltraPerformance—the only gateway SKUs that are supported for SAP HANA on Azure (Large Instances).</span><span class="sxs-lookup"><span data-stu-id="124ad-153">Your options are HighPerformance or UltraPerformance—the only gateway SKUs that are supported for SAP HANA on Azure (Large Instances).</span></span>

## <a name="linking-vnets"></a><span data-ttu-id="124ad-154">Linking VNets</span><span class="sxs-lookup"><span data-stu-id="124ad-154">Linking VNets</span></span>

<span data-ttu-id="124ad-155">Now that the Azure VNet has an ExpressRoute gateway, you use the authorization information provided by Microsoft to connect the ExpressRoute gateway to the SAP HANA on Azure (Large Instances) ExpressRoute circuit created for this connectivity.</span><span class="sxs-lookup"><span data-stu-id="124ad-155">Now that the Azure VNet has an ExpressRoute gateway, you use the authorization information provided by Microsoft to connect the ExpressRoute gateway to the SAP HANA on Azure (Large Instances) ExpressRoute circuit created for this connectivity.</span></span> <span data-ttu-id="124ad-156">This can only be performed using PowerShell (it is not currently supported through the Azure Portal).</span><span class="sxs-lookup"><span data-stu-id="124ad-156">This can only be performed using PowerShell (it is not currently supported through the Azure Portal).</span></span>

- <span data-ttu-id="124ad-157">You do the following for each VNet gateway using a different AuthGUID for each connection.</span><span class="sxs-lookup"><span data-stu-id="124ad-157">You do the following for each VNet gateway using a different AuthGUID for each connection.</span></span> <span data-ttu-id="124ad-158">The first two entries shown below come from the information provided by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="124ad-158">The first two entries shown below come from the information provided by Microsoft.</span></span> <span data-ttu-id="124ad-159">Also, the AuthGUID is specific for every VNet and its gateway.</span><span class="sxs-lookup"><span data-stu-id="124ad-159">Also, the AuthGUID is specific for every VNet and its gateway.</span></span>

```
# Populate with information provided by Microsoft Onboarding team
$PeerID = "/subscriptions/9cb43037-9195-4420-a798-f87681a0e380/resourceGroups/Customer-USE-Circuits/providers/Microsoft.Network/expressRouteCircuits/Customer-USE01-5Gb"
$AuthGUID = "76d40466-c458-4d14-adcf-3d1b56d1cd61"

# Your ExpressRoute Gateway Information
$myGroupName = "SAP-East-Coast"
$myGWName = "VNet01GW"
$myGWLocation = "East US"

# Define the name for your connection
$myConnectionName = "VNet01GWConnection"

# Create a new connection between the ER Circuit and your Gateway using the Authorization
$gw = Get-AzureRmVirtualNetworkGateway -Name $myGWName -ResourceGroupName $myGroupName
    
New-AzureRmVirtualNetworkGatewayConnection -Name $myConnectionName `
-ResourceGroupName $myGroupName -Location $myGWLocation -VirtualNetworkGateway1 $gw `
-PeerId $PeerID -ConnectionType ExpressRoute -AuthorizationKey $AuthGUID
```

<span data-ttu-id="124ad-160">You may need to execute this step more than once if you want to connect the gateway to multiple different ExpressRoute circuits that are associated with your subscription.</span><span class="sxs-lookup"><span data-stu-id="124ad-160">You may need to execute this step more than once if you want to connect the gateway to multiple different ExpressRoute circuits that are associated with your subscription.</span></span>

## <a name="adding-more-ip-addresses-or-subnets"></a><span data-ttu-id="124ad-161">Adding more IP addresses or subnets</span><span class="sxs-lookup"><span data-stu-id="124ad-161">Adding more IP addresses or subnets</span></span>

<span data-ttu-id="124ad-162">Use either the Azure Portal, PowerShell or CLI when adding more IP addresses or subnets.</span><span class="sxs-lookup"><span data-stu-id="124ad-162">Use either the Azure Portal, PowerShell or CLI when adding more IP addresses or subnets.</span></span>

<span data-ttu-id="124ad-163">If you have not yet declared the additional IP address space range with SAP HANA on Azure Service Management, open an Azure support request to get it added.</span><span class="sxs-lookup"><span data-stu-id="124ad-163">If you have not yet declared the additional IP address space range with SAP HANA on Azure Service Management, open an Azure support request to get it added.</span></span> <span data-ttu-id="124ad-164">After you receive confirmation, perform the next steps.</span><span class="sxs-lookup"><span data-stu-id="124ad-164">After you receive confirmation, perform the next steps.</span></span>

<span data-ttu-id="124ad-165">To create an additional subnet from the Azure portal, see the article [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), and to create from PowerShell, see [Create a virtual network using PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="124ad-165">To create an additional subnet from the Azure portal, see the article [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), and to create from PowerShell, see [Create a virtual network using PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

## <a name="adding-vnets"></a><span data-ttu-id="124ad-166">Adding VNets</span><span class="sxs-lookup"><span data-stu-id="124ad-166">Adding VNets</span></span>

<span data-ttu-id="124ad-167">After initially connecting one or more Azure VNets, you might want to add additional ones that access SAP HANA on Azure (Large Instances).</span><span class="sxs-lookup"><span data-stu-id="124ad-167">After initially connecting one or more Azure VNets, you might want to add additional ones that access SAP HANA on Azure (Large Instances).</span></span> <span data-ttu-id="124ad-168">First, submit an Azure support request, in that request include both the specific information identifying the particular Azure deployment, and the IP address space ranges for the tenant subnet(s) and the gateway subnet(s) of the additional Azure VNets.</span><span class="sxs-lookup"><span data-stu-id="124ad-168">First, submit an Azure support request, in that request include both the specific information identifying the particular Azure deployment, and the IP address space ranges for the tenant subnet(s) and the gateway subnet(s) of the additional Azure VNets.</span></span> <span data-ttu-id="124ad-169">SAP HANA on Azure Service Management then provides the necessary information you need to connect the additional VNets and ExpressRoute.</span><span class="sxs-lookup"><span data-stu-id="124ad-169">SAP HANA on Azure Service Management then provides the necessary information you need to connect the additional VNets and ExpressRoute.</span></span>

<span data-ttu-id="124ad-170">Steps to add a new Azure VNet:</span><span class="sxs-lookup"><span data-stu-id="124ad-170">Steps to add a new Azure VNet:</span></span>

1. <span data-ttu-id="124ad-171">Complete the first step in the onboarding process, see the _Creating Azure VNet_ section above.</span><span class="sxs-lookup"><span data-stu-id="124ad-171">Complete the first step in the onboarding process, see the _Creating Azure VNet_ section above.</span></span>
2. <span data-ttu-id="124ad-172">Complete the second step in the onboarding process, see the _Creating gateway subnet_ section above.</span><span class="sxs-lookup"><span data-stu-id="124ad-172">Complete the second step in the onboarding process, see the _Creating gateway subnet_ section above.</span></span>
3. <span data-ttu-id="124ad-173">Open an Azure support request with information on the new VNet and request a new Authorization Key to connect your additional VNets to the HANA Large Instance ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="124ad-173">Open an Azure support request with information on the new VNet and request a new Authorization Key to connect your additional VNets to the HANA Large Instance ExpressRoute circuit.</span></span>
4. <span data-ttu-id="124ad-174">Once notified that the authorization is complete, use the Microsoft-provided authorization information to complete the third step in the onboarding process, see the _Linking VNets_ section above.</span><span class="sxs-lookup"><span data-stu-id="124ad-174">Once notified that the authorization is complete, use the Microsoft-provided authorization information to complete the third step in the onboarding process, see the _Linking VNets_ section above.</span></span>

## <a name="increasing-expressroute-circuit-bandwidth"></a><span data-ttu-id="124ad-175">Increasing ExpressRoute circuit bandwidth</span><span class="sxs-lookup"><span data-stu-id="124ad-175">Increasing ExpressRoute circuit bandwidth</span></span>

<span data-ttu-id="124ad-176">Consult with SAP HANA on Azure Service Management.</span><span class="sxs-lookup"><span data-stu-id="124ad-176">Consult with SAP HANA on Azure Service Management.</span></span> <span data-ttu-id="124ad-177">If you are advised to increase the bandwidth of the SAP HANA on Azure (Large Instances) ExpressRoute circuit, create an Azure support request.</span><span class="sxs-lookup"><span data-stu-id="124ad-177">If you are advised to increase the bandwidth of the SAP HANA on Azure (Large Instances) ExpressRoute circuit, create an Azure support request.</span></span> <span data-ttu-id="124ad-178">(You can request an increase for a single circuit bandwidth up to a maximum of 10 Gbps.) You then receive notification after the operation is complete; no additional action needed to enable this higher speed in Azure.</span><span class="sxs-lookup"><span data-stu-id="124ad-178">(You can request an increase for a single circuit bandwidth up to a maximum of 10 Gbps.) You then receive notification after the operation is complete; no additional action needed to enable this higher speed in Azure.</span></span>

## <a name="adding-an-additional-expressroute-circuit"></a><span data-ttu-id="124ad-179">Adding an additional ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="124ad-179">Adding an additional ExpressRoute circuit</span></span>

<span data-ttu-id="124ad-180">Consult with SAP HANA on Azure Service Management, if you are advised that an additional ExpressRoute circuit is needed, make an Azure support request to create a new ExpressRoute circuit (and to get authorization information to connect to it).</span><span class="sxs-lookup"><span data-stu-id="124ad-180">Consult with SAP HANA on Azure Service Management, if you are advised that an additional ExpressRoute circuit is needed, make an Azure support request to create a new ExpressRoute circuit (and to get authorization information to connect to it).</span></span> <span data-ttu-id="124ad-181">The address space that will be used on the VNets must be defined before making the request, in order for SAP HANA on Azure Service Management to provide authorization.</span><span class="sxs-lookup"><span data-stu-id="124ad-181">The address space that will be used on the VNets must be defined before making the request, in order for SAP HANA on Azure Service Management to provide authorization.</span></span>

<span data-ttu-id="124ad-182">Once the new circuit is created and the SAP HANA on Azure Service Management configuration is complete, you will receive notification with the information you need to proceed.</span><span class="sxs-lookup"><span data-stu-id="124ad-182">Once the new circuit is created and the SAP HANA on Azure Service Management configuration is complete, you will receive notification with the information you need to proceed.</span></span> <span data-ttu-id="124ad-183">Follow the steps provided above for creating and connecting the new VNet to this additional circuit.</span><span class="sxs-lookup"><span data-stu-id="124ad-183">Follow the steps provided above for creating and connecting the new VNet to this additional circuit.</span></span> <span data-ttu-id="124ad-184">You will not be able to connect Azure VNets to this additional circuit if they already connected to another ExpressRoute circuit.</span><span class="sxs-lookup"><span data-stu-id="124ad-184">You will not be able to connect Azure VNets to this additional circuit if they already connected to another ExpressRoute circuit.</span></span>

## <a name="deleting-a-subnet"></a><span data-ttu-id="124ad-185">Deleting a subnet</span><span class="sxs-lookup"><span data-stu-id="124ad-185">Deleting a subnet</span></span>

<span data-ttu-id="124ad-186">To remove a VNet subnet, either the Azure Portal, PowerShell or CLI can be used.</span><span class="sxs-lookup"><span data-stu-id="124ad-186">To remove a VNet subnet, either the Azure Portal, PowerShell or CLI can be used.</span></span> <span data-ttu-id="124ad-187">If an address space is removed, SAP HANA on Azure Service Management should be notified about the address space change in order to remove it from the ranges that SAP HANA on Azure (Large Instances) is allowed to communicate with.</span><span class="sxs-lookup"><span data-stu-id="124ad-187">If an address space is removed, SAP HANA on Azure Service Management should be notified about the address space change in order to remove it from the ranges that SAP HANA on Azure (Large Instances) is allowed to communicate with.</span></span>

<span data-ttu-id="124ad-188">While there isn&#39;t yet specific, dedicated Azure.com guidance on removing subnets, the process for removing subnets is the reverse of the process for adding them.</span><span class="sxs-lookup"><span data-stu-id="124ad-188">While there isn&#39;t yet specific, dedicated Azure.com guidance on removing subnets, the process for removing subnets is the reverse of the process for adding them.</span></span> <span data-ttu-id="124ad-189">See the article Azure portal [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information on creating subnets.</span><span class="sxs-lookup"><span data-stu-id="124ad-189">See the article Azure portal [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information on creating subnets.</span></span>

## <a name="deleting-a-vnet"></a><span data-ttu-id="124ad-190">Deleting a VNet</span><span class="sxs-lookup"><span data-stu-id="124ad-190">Deleting a VNet</span></span>

<span data-ttu-id="124ad-191">Use either the Azure Portal, PowerShell or CLI when deleting a VNet.</span><span class="sxs-lookup"><span data-stu-id="124ad-191">Use either the Azure Portal, PowerShell or CLI when deleting a VNet.</span></span> <span data-ttu-id="124ad-192">SAP HANA on Azure Service Management removes the existing authorizations on the SAP HANA on Azure (Large Instances) ExpressRoute circuit and remove the IP address ranges (both the tenant and gateway ranges) for the communication with HANA Large Instances.</span><span class="sxs-lookup"><span data-stu-id="124ad-192">SAP HANA on Azure Service Management removes the existing authorizations on the SAP HANA on Azure (Large Instances) ExpressRoute circuit and remove the IP address ranges (both the tenant and gateway ranges) for the communication with HANA Large Instances.</span></span>

<span data-ttu-id="124ad-193">Once the VNet has been removed, open an Azure support request to provide the IP address space ranges to be removed.</span><span class="sxs-lookup"><span data-stu-id="124ad-193">Once the VNet has been removed, open an Azure support request to provide the IP address space ranges to be removed.</span></span>

<span data-ttu-id="124ad-194">While there isn&#39;t yet specific, dedicated Azure.com guidance on removing VNets, the process for removing VNets is the reverse of the process for adding them, which is described above.</span><span class="sxs-lookup"><span data-stu-id="124ad-194">While there isn&#39;t yet specific, dedicated Azure.com guidance on removing VNets, the process for removing VNets is the reverse of the process for adding them, which is described above.</span></span> <span data-ttu-id="124ad-195">See the articles [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Create a virtual network using PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information on creating VNets.</span><span class="sxs-lookup"><span data-stu-id="124ad-195">See the articles [Create a virtual network using the Azure portal](../../../virtual-network/virtual-networks-create-vnet-arm-pportal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Create a virtual network using PowerShell](../../../virtual-network/virtual-networks-create-vnet-arm-ps.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more information on creating VNets.</span></span>

<span data-ttu-id="124ad-196">To ensure everything is removed, delete the following items:</span><span class="sxs-lookup"><span data-stu-id="124ad-196">To ensure everything is removed, delete the following items:</span></span>

- <span data-ttu-id="124ad-197">**For Azure Resource Manager:** The ExpressRoute connection, VNet Gateway, VNet Gateway Public IP and VNet</span><span class="sxs-lookup"><span data-stu-id="124ad-197">**For Azure Resource Manager:** The ExpressRoute connection, VNet Gateway, VNet Gateway Public IP and VNet</span></span>
- <span data-ttu-id="124ad-198">**For Classic VM:** The VNet Gateway and VNet</span><span class="sxs-lookup"><span data-stu-id="124ad-198">**For Classic VM:** The VNet Gateway and VNet</span></span>

## <a name="deleting-an-expressroute-circuit"></a><span data-ttu-id="124ad-199">Deleting an ExpressRoute circuit</span><span class="sxs-lookup"><span data-stu-id="124ad-199">Deleting an ExpressRoute circuit</span></span>

<span data-ttu-id="124ad-200">To remove an additional SAP HANA on Azure (Large Instances) ExpressRoute circuit, open an Azure support request with SAP HANA on Azure Service Management and request that the circuit be deleted.</span><span class="sxs-lookup"><span data-stu-id="124ad-200">To remove an additional SAP HANA on Azure (Large Instances) ExpressRoute circuit, open an Azure support request with SAP HANA on Azure Service Management and request that the circuit be deleted.</span></span> <span data-ttu-id="124ad-201">Within the Azure subscription, you may delete or keep the VNet as necessary.</span><span class="sxs-lookup"><span data-stu-id="124ad-201">Within the Azure subscription, you may delete or keep the VNet as necessary.</span></span> <span data-ttu-id="124ad-202">However, you must either delete the connection (if Azure Resource Manager), or unlink the connection (if Classic) between the HANA Large Instances ExpressRoute circuit and the linked VNet gateway.</span><span class="sxs-lookup"><span data-stu-id="124ad-202">However, you must either delete the connection (if Azure Resource Manager), or unlink the connection (if Classic) between the HANA Large Instances ExpressRoute circuit and the linked VNet gateway.</span></span>

<span data-ttu-id="124ad-203">If you also want to remove a VNet, follow the guidance on Deleting a VNet in the section above.</span><span class="sxs-lookup"><span data-stu-id="124ad-203">If you also want to remove a VNet, follow the guidance on Deleting a VNet in the section above.</span></span>


