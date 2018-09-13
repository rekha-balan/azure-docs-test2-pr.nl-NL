---
title: 'Connect your on-premises network to an Azure virtual network: Site-to-Site VPN: Portal | Microsoft Docs'
description: Steps to create an IPsec connection from your on-premises network to an Azure virtual network over the public Internet. These steps will help you create a cross-premises Site-to-Site VPN Gateway connection using the portal.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 827a4db7-7fa5-4eaf-b7e1-e1518c51c815
ms.service: vpn-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/04/2017
ms.author: cherylmc
ms.openlocfilehash: 67a886ec215ea372e8f5ce67ed9abf060c1c6b92
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661559"
---
# <a name="create-a-site-to-site-connection-in-the-azure-portal"></a><span data-ttu-id="49c06-104">Create a Site-to-Site connection in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="49c06-104">Create a Site-to-Site connection in the Azure portal</span></span>

<span data-ttu-id="49c06-105">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="49c06-105">A Site-to-Site (S2S) VPN gateway connection is a connection over IPsec/IKE (IKEv1 or IKEv2) VPN tunnel.</span></span> <span data-ttu-id="49c06-106">This type of connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="49c06-106">This type of connection requires a VPN device located on-premises that has a public IP address assigned to it and is not located behind a NAT.</span></span> <span data-ttu-id="49c06-107">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span><span class="sxs-lookup"><span data-stu-id="49c06-107">Site-to-Site connections can be used for cross-premises and hybrid configurations.</span></span>

![Site-to-Site VPN Gateway cross-premises connection diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-site-to-site-resource-manager-portal/site-to-site-diagram.png)

<span data-ttu-id="49c06-109">This article walks you through creating a virtual network and a Site-to-Site VPN gateway connection to your on-premises network using the Azure Resource Manager deployment model and the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="49c06-109">This article walks you through creating a virtual network and a Site-to-Site VPN gateway connection to your on-premises network using the Azure Resource Manager deployment model and the Azure portal.</span></span> <span data-ttu-id="49c06-110">You can also create this configuration by using different deployment tools, or for the classic deployment model, by selecting a different option from the following list:</span><span class="sxs-lookup"><span data-stu-id="49c06-110">You can also create this configuration by using different deployment tools, or for the classic deployment model, by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-howto-site-to-site-resource-manager-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-create-site-to-site-rm-powershell.md)
> * [Classic - Azure portal](vpn-gateway-howto-site-to-site-classic-portal.md)
> * [Classic - classic portal](vpn-gateway-site-to-site-create.md)
>
>


#### <a name="additional-configurations"></a><span data-ttu-id="49c06-115">Additional configurations</span><span class="sxs-lookup"><span data-stu-id="49c06-115">Additional configurations</span></span>
<span data-ttu-id="49c06-116">If you want to connect VNets together, but are not creating a connection to an on-premises location, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="49c06-116">If you want to connect VNets together, but are not creating a connection to an on-premises location, see [Configure a VNet-to-VNet connection](vpn-gateway-vnet-vnet-rm-ps.md).</span></span> <span data-ttu-id="49c06-117">If you want to add a Site-to-Site connection to a VNet that already has a connection, see [Add a S2S connection to a VNet with an existing VPN gateway connection](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="49c06-117">If you want to add a Site-to-Site connection to a VNet that already has a connection, see [Add a S2S connection to a VNet with an existing VPN gateway connection](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md).</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="49c06-118">Before you begin</span><span class="sxs-lookup"><span data-stu-id="49c06-118">Before you begin</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-deployment-models-include.md)]

<span data-ttu-id="49c06-119">Verify that you have the following items before beginning your configuration:</span><span class="sxs-lookup"><span data-stu-id="49c06-119">Verify that you have the following items before beginning your configuration:</span></span>

* <span data-ttu-id="49c06-120">A compatible VPN device and someone who is able to configure it.</span><span class="sxs-lookup"><span data-stu-id="49c06-120">A compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="49c06-121">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="49c06-121">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span>
* <span data-ttu-id="49c06-122">If you aren't familiar with the IP address spaces located in your on-premises network, you need to coordinate with someone who can provide those details for you.</span><span class="sxs-lookup"><span data-stu-id="49c06-122">If you aren't familiar with the IP address spaces located in your on-premises network, you need to coordinate with someone who can provide those details for you.</span></span> <span data-ttu-id="49c06-123">Site-to-Site connections cannot have overlapping address spaces.</span><span class="sxs-lookup"><span data-stu-id="49c06-123">Site-to-Site connections cannot have overlapping address spaces.</span></span>
* <span data-ttu-id="49c06-124">An externally facing public IP address for your VPN device.</span><span class="sxs-lookup"><span data-stu-id="49c06-124">An externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="49c06-125">This IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="49c06-125">This IP address cannot be located behind a NAT.</span></span>
* <span data-ttu-id="49c06-126">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="49c06-126">An Azure subscription.</span></span> <span data-ttu-id="49c06-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](http://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](http://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="49c06-127">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](http://azure.microsoft.com/pricing/member-offers/msdn-benefits-details) or sign up for a [free account](http://azure.microsoft.com/pricing/free-trial).</span></span>

### <a name="values"></a><span data-ttu-id="49c06-128">Example values</span><span class="sxs-lookup"><span data-stu-id="49c06-128">Example values</span></span>
<span data-ttu-id="49c06-129">When using these steps as an exercise, you can use the following example values:</span><span class="sxs-lookup"><span data-stu-id="49c06-129">When using these steps as an exercise, you can use the following example values:</span></span>

* <span data-ttu-id="49c06-130">**VNet Name:** TestVNet1</span><span class="sxs-lookup"><span data-stu-id="49c06-130">**VNet Name:** TestVNet1</span></span>
* <span data-ttu-id="49c06-131">**Address Space:**</span><span class="sxs-lookup"><span data-stu-id="49c06-131">**Address Space:**</span></span> 
    * <span data-ttu-id="49c06-132">10.11.0.0/16</span><span class="sxs-lookup"><span data-stu-id="49c06-132">10.11.0.0/16</span></span>
    * <span data-ttu-id="49c06-133">10.12.0.0/16 (optional for this exercise)</span><span class="sxs-lookup"><span data-stu-id="49c06-133">10.12.0.0/16 (optional for this exercise)</span></span>
* <span data-ttu-id="49c06-134">**Subnets:**</span><span class="sxs-lookup"><span data-stu-id="49c06-134">**Subnets:**</span></span>
  * <span data-ttu-id="49c06-135">FrontEnd: 10.11.0.0/24</span><span class="sxs-lookup"><span data-stu-id="49c06-135">FrontEnd: 10.11.0.0/24</span></span>
  * <span data-ttu-id="49c06-136">BackEnd: 10.12.0.0/24 (optional for this exercise)</span><span class="sxs-lookup"><span data-stu-id="49c06-136">BackEnd: 10.12.0.0/24 (optional for this exercise)</span></span>
  * <span data-ttu-id="49c06-137">GatewaySubnet: 10.11.255.0/27</span><span class="sxs-lookup"><span data-stu-id="49c06-137">GatewaySubnet: 10.11.255.0/27</span></span>
* <span data-ttu-id="49c06-138">**Resource Group:** TestRG1</span><span class="sxs-lookup"><span data-stu-id="49c06-138">**Resource Group:** TestRG1</span></span>
* <span data-ttu-id="49c06-139">**Location:** East US</span><span class="sxs-lookup"><span data-stu-id="49c06-139">**Location:** East US</span></span>
* <span data-ttu-id="49c06-140">**DNS Server:** The IP address of your DNS server</span><span class="sxs-lookup"><span data-stu-id="49c06-140">**DNS Server:** The IP address of your DNS server</span></span>
* <span data-ttu-id="49c06-141">**Virtual Network Gateway Name:** VNet1GW</span><span class="sxs-lookup"><span data-stu-id="49c06-141">**Virtual Network Gateway Name:** VNet1GW</span></span>
* <span data-ttu-id="49c06-142">**Public IP:** VNet1GWIP</span><span class="sxs-lookup"><span data-stu-id="49c06-142">**Public IP:** VNet1GWIP</span></span>
* <span data-ttu-id="49c06-143">**VPN Type:** Route-based</span><span class="sxs-lookup"><span data-stu-id="49c06-143">**VPN Type:** Route-based</span></span>
* <span data-ttu-id="49c06-144">**Connection Type:** Site-to-site (IPsec)</span><span class="sxs-lookup"><span data-stu-id="49c06-144">**Connection Type:** Site-to-site (IPsec)</span></span>
* <span data-ttu-id="49c06-145">**Gateway Type:** VPN</span><span class="sxs-lookup"><span data-stu-id="49c06-145">**Gateway Type:** VPN</span></span>
* <span data-ttu-id="49c06-146">**Local Network Gateway Name:** Site2</span><span class="sxs-lookup"><span data-stu-id="49c06-146">**Local Network Gateway Name:** Site2</span></span>
* <span data-ttu-id="49c06-147">**Connection Name:** VNet1toSite2</span><span class="sxs-lookup"><span data-stu-id="49c06-147">**Connection Name:** VNet1toSite2</span></span>

## <a name="CreatVNet"></a><span data-ttu-id="49c06-148">1. Create a virtual network</span><span class="sxs-lookup"><span data-stu-id="49c06-148">1. Create a virtual network</span></span>

[!INCLUDE [vpn-gateway-basic-vnet-rm-portal](../../includes/vpn-gateway-basic-vnet-s2s-rm-portal-include.md)]

## <a name="dns"></a><span data-ttu-id="49c06-149">2. Specify a DNS server</span><span class="sxs-lookup"><span data-stu-id="49c06-149">2. Specify a DNS server</span></span>
<span data-ttu-id="49c06-150">DNS is not required for Site-to-Site connections.</span><span class="sxs-lookup"><span data-stu-id="49c06-150">DNS is not required for Site-to-Site connections.</span></span> <span data-ttu-id="49c06-151">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span><span class="sxs-lookup"><span data-stu-id="49c06-151">However, if you want to have name resolution for resources that are deployed to your virtual network, you should specify a DNS server.</span></span> <span data-ttu-id="49c06-152">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span><span class="sxs-lookup"><span data-stu-id="49c06-152">This setting lets you specify the DNS server that you want to use for name resolution for this virtual network.</span></span> <span data-ttu-id="49c06-153">It does not create a DNS server.</span><span class="sxs-lookup"><span data-stu-id="49c06-153">It does not create a DNS server.</span></span>

[!INCLUDE [vpn-gateway-add-dns-rm-portal](../../includes/vpn-gateway-add-dns-rm-portal-include.md)]

## <a name="gatewaysubnet"></a><span data-ttu-id="49c06-154">3. Create a gateway subnet</span><span class="sxs-lookup"><span data-stu-id="49c06-154">3. Create a gateway subnet</span></span>
<span data-ttu-id="49c06-155">You must create a gateway subnet for your VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="49c06-155">You must create a gateway subnet for your VPN gateway.</span></span> <span data-ttu-id="49c06-156">The gateway subnet contains the IP addresses that the VPN gateway services use.</span><span class="sxs-lookup"><span data-stu-id="49c06-156">The gateway subnet contains the IP addresses that the VPN gateway services use.</span></span> <span data-ttu-id="49c06-157">If possible, create a gateway subnet using a CIDR block of /28 or /27.</span><span class="sxs-lookup"><span data-stu-id="49c06-157">If possible, create a gateway subnet using a CIDR block of /28 or /27.</span></span> <span data-ttu-id="49c06-158">This will ensure that you have enough IP addresses to accommodate possible future gateway features.</span><span class="sxs-lookup"><span data-stu-id="49c06-158">This will ensure that you have enough IP addresses to accommodate possible future gateway features.</span></span>

[!INCLUDE [vpn-gateway-add-gwsubnet-rm-portal](../../includes/vpn-gateway-add-gwsubnet-s2s-rm-portal-include.md)]

## <a name="VNetGateway"></a><span data-ttu-id="49c06-159">4. Create a virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="49c06-159">4. Create a virtual network gateway</span></span>

[!INCLUDE [vpn-gateway-add-gw-s2s-rm-portal](../../includes/vpn-gateway-add-gw-s2s-rm-portal-include.md)]

## <a name="LocalNetworkGateway"></a><span data-ttu-id="49c06-160">5. Create a local network gateway</span><span class="sxs-lookup"><span data-stu-id="49c06-160">5. Create a local network gateway</span></span>
<span data-ttu-id="49c06-161">The local network gateway refers to your on-premises location.</span><span class="sxs-lookup"><span data-stu-id="49c06-161">The local network gateway refers to your on-premises location.</span></span> <span data-ttu-id="49c06-162">The settings that you specify for the local network gateway determine the address spaces that are routed to your on-premises VPN device.</span><span class="sxs-lookup"><span data-stu-id="49c06-162">The settings that you specify for the local network gateway determine the address spaces that are routed to your on-premises VPN device.</span></span>

[!INCLUDE [vpn-gateway-add-lng-s2s-rm-portal](../../includes/vpn-gateway-add-lng-s2s-rm-portal-include.md)]

## <a name="VPNDevice"></a><span data-ttu-id="49c06-163">6. Configure your VPN device</span><span class="sxs-lookup"><span data-stu-id="49c06-163">6. Configure your VPN device</span></span>
[!INCLUDE [vpn-gateway-configure-vpn-device-rm](../../includes/vpn-gateway-configure-vpn-device-rm-include.md)]

## <a name="CreateConnection"></a><span data-ttu-id="49c06-164">7. Create a Site-to-Site VPN connection</span><span class="sxs-lookup"><span data-stu-id="49c06-164">7. Create a Site-to-Site VPN connection</span></span>

<span data-ttu-id="49c06-165">In this step, you create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span><span class="sxs-lookup"><span data-stu-id="49c06-165">In this step, you create the Site-to-Site VPN connection between your virtual network gateway and your on-premises VPN device.</span></span> <span data-ttu-id="49c06-166">Before beginning this section, verify that your virtual network gateway and local network gateways have finished creating.</span><span class="sxs-lookup"><span data-stu-id="49c06-166">Before beginning this section, verify that your virtual network gateway and local network gateways have finished creating.</span></span>

[!INCLUDE [vpn-gateway-add-site-to-site-connection-rm-portal](../../includes/vpn-gateway-add-site-to-site-connection-s2s-rm-portal-include.md)]

## <a name="VerifyConnection"></a><span data-ttu-id="49c06-167">8. Verify the VPN connection</span><span class="sxs-lookup"><span data-stu-id="49c06-167">8. Verify the VPN connection</span></span>

[!INCLUDE [Azure portal](../../includes/vpn-gateway-verify-connection-portal-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="49c06-168">Next steps</span><span class="sxs-lookup"><span data-stu-id="49c06-168">Next steps</span></span>
*  <span data-ttu-id="49c06-169">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="49c06-169">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="49c06-170">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span><span class="sxs-lookup"><span data-stu-id="49c06-170">For more information, see [Virtual Machines](https://docs.microsoft.com/azure/#pivot=services&panel=Compute).</span></span>
*  <span data-ttu-id="49c06-171">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span><span class="sxs-lookup"><span data-stu-id="49c06-171">For information about BGP, see the [BGP Overview](vpn-gateway-bgp-overview.md) and [How to configure BGP](vpn-gateway-bgp-resource-manager-ps.md).</span></span>


