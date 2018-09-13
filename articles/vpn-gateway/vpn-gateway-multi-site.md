---
title: Connect a virtual network to multiple sites using VPN Gateway and PowerShell | Microsoft Docs
description: This article will walk you through connecting multiple local on-premises sites to a virtual network using a VPN Gateway for the classic deployment model.
services: vpn-gateway
documentationcenter: na
author: yushwang
manager: rossort
editor: ''
tags: azure-service-management
ms.assetid: b043df6e-f1e8-4a4d-8467-c06079e2c093
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/11/2016
ms.author: yushwang
ms.openlocfilehash: 47285a2ce9b1280387d5c353598d8fc8d8e602c7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552997"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="5a69f-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span><span class="sxs-lookup"><span data-stu-id="5a69f-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [Classic - PowerShell](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="5a69f-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span><span class="sxs-lookup"><span data-stu-id="5a69f-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="5a69f-107">This type of connection is often referred to as a "multi-site" configuration.</span><span class="sxs-lookup"><span data-stu-id="5a69f-107">This type of connection is often referred to as a "multi-site" configuration.</span></span>

<span data-ttu-id="5a69f-108">This article applies to virtual networks created using the classic deployment model (also known as Service Management).</span><span class="sxs-lookup"><span data-stu-id="5a69f-108">This article applies to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="5a69f-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span><span class="sxs-lookup"><span data-stu-id="5a69f-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="5a69f-110">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-classic.md) for information about coexisting connections.</span><span class="sxs-lookup"><span data-stu-id="5a69f-110">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-classic.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="5a69f-111">Deployment models and methods</span><span class="sxs-lookup"><span data-stu-id="5a69f-111">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="5a69f-112">We update this table as new articles and additional tools become available for this configuration.</span><span class="sxs-lookup"><span data-stu-id="5a69f-112">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="5a69f-113">When an article is available, we link directly to it from this table.</span><span class="sxs-lookup"><span data-stu-id="5a69f-113">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="5a69f-114">About connecting</span><span class="sxs-lookup"><span data-stu-id="5a69f-114">About connecting</span></span>
<span data-ttu-id="5a69f-115">You can connect multiple on-premises sites to a single virtual network.</span><span class="sxs-lookup"><span data-stu-id="5a69f-115">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="5a69f-116">This is especially attractive for building hybrid cloud solutions.</span><span class="sxs-lookup"><span data-stu-id="5a69f-116">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="5a69f-117">Creating a multi-site connection to your Azure virtual network gateway is very similar to creating other Site-to-Site connections.</span><span class="sxs-lookup"><span data-stu-id="5a69f-117">Creating a multi-site connection to your Azure virtual network gateway is very similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="5a69f-118">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span><span class="sxs-lookup"><span data-stu-id="5a69f-118">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="5a69f-119">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span><span class="sxs-lookup"><span data-stu-id="5a69f-119">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="5a69f-120">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span><span class="sxs-lookup"><span data-stu-id="5a69f-120">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="5a69f-121">![multi-site diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-multi-site/multisite.png "multi-site")</span><span class="sxs-lookup"><span data-stu-id="5a69f-121">![multi-site diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="5a69f-122">Points to consider</span><span class="sxs-lookup"><span data-stu-id="5a69f-122">Points to consider</span></span>
<span data-ttu-id="5a69f-123">**You won't be able to use the Azure Classic Portal to make changes to this virtual network.**</span><span class="sxs-lookup"><span data-stu-id="5a69f-123">**You won't be able to use the Azure Classic Portal to make changes to this virtual network.**</span></span> <span data-ttu-id="5a69f-124">For this release, you'll need to make changes to the network configuration file instead of using the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="5a69f-124">For this release, you'll need to make changes to the network configuration file instead of using the Azure Classic Portal.</span></span> <span data-ttu-id="5a69f-125">If you make changes in the Azure Classic Portal, they'll overwrite your multi-site reference settings for this virtual network.</span><span class="sxs-lookup"><span data-stu-id="5a69f-125">If you make changes in the Azure Classic Portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="5a69f-126">You should feel pretty comfortable using the network configuration file by the time you've completed the multi-site procedure.</span><span class="sxs-lookup"><span data-stu-id="5a69f-126">You should feel pretty comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="5a69f-127">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span><span class="sxs-lookup"><span data-stu-id="5a69f-127">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="5a69f-128">This doesn't mean that you can't use the Azure Classic Portal at all.</span><span class="sxs-lookup"><span data-stu-id="5a69f-128">This doesn't mean that you can't use the Azure Classic Portal at all.</span></span> <span data-ttu-id="5a69f-129">You can use it for everything else, except making configuration changes to this particular virtual network.</span><span class="sxs-lookup"><span data-stu-id="5a69f-129">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5a69f-130">Before you begin</span><span class="sxs-lookup"><span data-stu-id="5a69f-130">Before you begin</span></span>
<span data-ttu-id="5a69f-131">Before you begin configuration, verify that you have the following:</span><span class="sxs-lookup"><span data-stu-id="5a69f-131">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="5a69f-132">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5a69f-132">An Azure subscription.</span></span> <span data-ttu-id="5a69f-133">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a69f-133">If you don't already have an Azure subscription, you can activate your [MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) or sign up for a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5a69f-134">Compatible VPN hardware for each on-premises location.</span><span class="sxs-lookup"><span data-stu-id="5a69f-134">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="5a69f-135">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span><span class="sxs-lookup"><span data-stu-id="5a69f-135">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="5a69f-136">An externally facing public IPv4 IP address for each VPN device.</span><span class="sxs-lookup"><span data-stu-id="5a69f-136">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="5a69f-137">The IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="5a69f-137">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="5a69f-138">This is requirement.</span><span class="sxs-lookup"><span data-stu-id="5a69f-138">This is requirement.</span></span>
* <span data-ttu-id="5a69f-139">You'll need to install the latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a69f-139">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5a69f-140">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5a69f-140">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for more information about installing the PowerShell cmdlets.</span></span>
* <span data-ttu-id="5a69f-141">Someone who is proficient at configuring your VPN hardware.</span><span class="sxs-lookup"><span data-stu-id="5a69f-141">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="5a69f-142">You won't be able to use the auto-generated VPN scripts from the Azure Classic Portal to configure your VPN devices.</span><span class="sxs-lookup"><span data-stu-id="5a69f-142">You won't be able to use the auto-generated VPN scripts from the Azure Classic Portal to configure your VPN devices.</span></span> <span data-ttu-id="5a69f-143">This means you'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span><span class="sxs-lookup"><span data-stu-id="5a69f-143">This means you'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="5a69f-144">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span><span class="sxs-lookup"><span data-stu-id="5a69f-144">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="5a69f-145">The IP address ranges for each of the local network sites that you'll be connecting to.</span><span class="sxs-lookup"><span data-stu-id="5a69f-145">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="5a69f-146">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span><span class="sxs-lookup"><span data-stu-id="5a69f-146">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="5a69f-147">Otherwise, the Azure Classic Portal or the REST API will reject the configuration being uploaded.</span><span class="sxs-lookup"><span data-stu-id="5a69f-147">Otherwise, the Azure Classic Portal or the REST API will reject the configuration being uploaded.</span></span>

    <span data-ttu-id="5a69f-148">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span><span class="sxs-lookup"><span data-stu-id="5a69f-148">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="5a69f-149">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span><span class="sxs-lookup"><span data-stu-id="5a69f-149">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="5a69f-150">1. Create a Site-to-Site VPN</span><span class="sxs-lookup"><span data-stu-id="5a69f-150">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="5a69f-151">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span><span class="sxs-lookup"><span data-stu-id="5a69f-151">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="5a69f-152">You can proceed to [Export the virtual network configuration settings](#export).</span><span class="sxs-lookup"><span data-stu-id="5a69f-152">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="5a69f-153">If not, do the following:</span><span class="sxs-lookup"><span data-stu-id="5a69f-153">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="5a69f-154">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span><span class="sxs-lookup"><span data-stu-id="5a69f-154">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="5a69f-155">Change your gateway type to dynamic routing.</span><span class="sxs-lookup"><span data-stu-id="5a69f-155">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="5a69f-156">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span><span class="sxs-lookup"><span data-stu-id="5a69f-156">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="5a69f-157">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span><span class="sxs-lookup"><span data-stu-id="5a69f-157">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span> <span data-ttu-id="5a69f-158">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md#how-to-change-the-vpn-routing-type-for-your-gateway).</span><span class="sxs-lookup"><span data-stu-id="5a69f-158">For instructions, see [How to change the VPN routing type for your gateway](vpn-gateway-configure-vpn-gateway-mp.md#how-to-change-the-vpn-routing-type-for-your-gateway).</span></span>  
2. <span data-ttu-id="5a69f-159">Configure your new gateway and create your VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a69f-159">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="5a69f-160">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="5a69f-160">For instructions, see [Configure a VPN Gateway in the Azure Classic Portal](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="5a69f-161">First, change your gateway type to dynamic routing.</span><span class="sxs-lookup"><span data-stu-id="5a69f-161">First, change your gateway type to dynamic routing.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="5a69f-162">If you don't have a Site-to-Site virtual network:</span><span class="sxs-lookup"><span data-stu-id="5a69f-162">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="5a69f-163">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="5a69f-163">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection in the Azure Classic Portal](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="5a69f-164">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="5a69f-164">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="5a69f-165">Be sure to select **dynamic routing** for your gateway type.</span><span class="sxs-lookup"><span data-stu-id="5a69f-165">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <a name="export"></a><span data-ttu-id="5a69f-166">2. Export the network configuration file</span><span class="sxs-lookup"><span data-stu-id="5a69f-166">2. Export the network configuration file</span></span>
<span data-ttu-id="5a69f-167">Export your network configuration file.</span><span class="sxs-lookup"><span data-stu-id="5a69f-167">Export your network configuration file.</span></span> <span data-ttu-id="5a69f-168">The file that you export will be used to configure your new multi-site settings.</span><span class="sxs-lookup"><span data-stu-id="5a69f-168">The file that you export will be used to configure your new multi-site settings.</span></span> <span data-ttu-id="5a69f-169">If you need instructions on how to export a file, see the section in the article: [How to create a classic VNet in the Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md#how-to-create-a-classic-vnet-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="5a69f-169">If you need instructions on how to export a file, see the section in the article: [How to create a classic VNet in the Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md#how-to-create-a-classic-vnet-in-the-azure-portal).</span></span>

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="5a69f-170">3. Open the network configuration file</span><span class="sxs-lookup"><span data-stu-id="5a69f-170">3. Open the network configuration file</span></span>
<span data-ttu-id="5a69f-171">Open the network configuration file that you downloaded in the last step.</span><span class="sxs-lookup"><span data-stu-id="5a69f-171">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="5a69f-172">Use any xml editor that you like.</span><span class="sxs-lookup"><span data-stu-id="5a69f-172">Use any xml editor that you like.</span></span> <span data-ttu-id="5a69f-173">The file should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="5a69f-173">The file should look similar to the following:</span></span>

        <NetworkConfiguration xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <LocalNetworkSites>
              <LocalNetworkSite name="Site1">
                <AddressSpace>
                  <AddressPrefix>10.0.0.0/16</AddressPrefix>
                  <AddressPrefix>10.1.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.2.3.4</VPNGatewayAddress>
              </LocalNetworkSite>
              <LocalNetworkSite name="Site2">
                <AddressSpace>
                  <AddressPrefix>10.2.0.0/16</AddressPrefix>
                  <AddressPrefix>10.3.0.0/16</AddressPrefix>
                </AddressSpace>
                <VPNGatewayAddress>131.4.5.6</VPNGatewayAddress>
              </LocalNetworkSite>
            </LocalNetworkSites>
            <VirtualNetworkSites>
              <VirtualNetworkSite name="VNet1" AffinityGroup="USWest">
                <AddressSpace>
                  <AddressPrefix>10.20.0.0/16</AddressPrefix>
                  <AddressPrefix>10.21.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="FE">
                    <AddressPrefix>10.20.0.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="BE">
                    <AddressPrefix>10.20.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="GatewaySubnet">
                    <AddressPrefix>10.20.2.0/29</AddressPrefix>
                  </Subnet>
                </Subnets>
                <Gateway>
                  <ConnectionsToLocalNetwork>
                    <LocalNetworkSiteRef name="Site1">
                      <Connection type="IPsec" />
                    </LocalNetworkSiteRef>
                  </ConnectionsToLocalNetwork>
                </Gateway>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="5a69f-174">4. Add multiple site references</span><span class="sxs-lookup"><span data-stu-id="5a69f-174">4. Add multiple site references</span></span>
<span data-ttu-id="5a69f-175">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="5a69f-175">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="5a69f-176">Adding a new local site reference triggers Azure to create a new tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a69f-176">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="5a69f-177">In the example below, the network configuration is for a single-site connection.</span><span class="sxs-lookup"><span data-stu-id="5a69f-177">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="5a69f-178">Save the file once you have finished making your changes.</span><span class="sxs-lookup"><span data-stu-id="5a69f-178">Save the file once you have finished making your changes.</span></span>

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

    To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:

        <Gateway>
          <ConnectionsToLocalNetwork>
            <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
            <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
          </ConnectionsToLocalNetwork>
        </Gateway>

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="5a69f-179">5. Import the network configuration file</span><span class="sxs-lookup"><span data-stu-id="5a69f-179">5. Import the network configuration file</span></span>
<span data-ttu-id="5a69f-180">Import the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="5a69f-180">Import the network configuration file.</span></span> <span data-ttu-id="5a69f-181">When you import this file with the changes, the new tunnels will be added.</span><span class="sxs-lookup"><span data-stu-id="5a69f-181">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="5a69f-182">The tunnels will use the dynamic gateway that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="5a69f-182">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="5a69f-183">If you need instructions on how to import the file, see the section in the article: [How to create a classic VNet in the Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md#how-to-create-a-classic-vnet-in-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="5a69f-183">If you need instructions on how to import the file, see the section in the article: [How to create a classic VNet in the Azure Portal](../virtual-network/virtual-networks-create-vnet-classic-pportal.md#how-to-create-a-classic-vnet-in-the-azure-portal).</span></span>  

## <a name="6-download-keys"></a><span data-ttu-id="5a69f-184">6. Download keys</span><span class="sxs-lookup"><span data-stu-id="5a69f-184">6. Download keys</span></span>
<span data-ttu-id="5a69f-185">Once your new tunnels have been added, use the PowerShell cmdlet `Get-AzureVNetGatewayKey` to get the IPsec/IKE pre-shared keys for each tunnel.</span><span class="sxs-lookup"><span data-stu-id="5a69f-185">Once your new tunnels have been added, use the PowerShell cmdlet `Get-AzureVNetGatewayKey` to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="5a69f-186">For example:</span><span class="sxs-lookup"><span data-stu-id="5a69f-186">For example:</span></span>

    Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"

    Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"

<span data-ttu-id="5a69f-187">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span><span class="sxs-lookup"><span data-stu-id="5a69f-187">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="5a69f-188">7. Verify your connections</span><span class="sxs-lookup"><span data-stu-id="5a69f-188">7. Verify your connections</span></span>
<span data-ttu-id="5a69f-189">Check the multi-site tunnel status.</span><span class="sxs-lookup"><span data-stu-id="5a69f-189">Check the multi-site tunnel status.</span></span> <span data-ttu-id="5a69f-190">After downloading the keys for each tunnel, you'll want to verify connections.</span><span class="sxs-lookup"><span data-stu-id="5a69f-190">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="5a69f-191">Use `Get-AzureVnetConnection` to get a list of virtual network tunnels, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="5a69f-191">Use `Get-AzureVnetConnection` to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="5a69f-192">VNet1 is the name of the VNet.</span><span class="sxs-lookup"><span data-stu-id="5a69f-192">VNet1 is the name of the VNet.</span></span>

    Get-AzureVnetConnection -VNetName VNET1

    ConnectivityState         : Connected
    EgressBytesTransferred    : 661530
    IngressBytesTransferred   : 519207
    LastConnectionEstablished : 5/2/2014 2:51:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site1' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site1
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7f68a8e6-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

    ConnectivityState         : Connected
    EgressBytesTransferred    : 789398
    IngressBytesTransferred   : 143908
    LastConnectionEstablished : 5/2/2014 3:20:40 PM
    LastEventID               : 23401
    LastEventMessage          : The connectivity state for the local network site 'Site2' changed from Not Connected to Connected.
    LastEventTimeStamp        : 5/2/2014 2:51:40 PM
    LocalNetworkSiteName      : Site2
    OperationDescription      : Get-AzureVNetConnection
    OperationId               : 7893b329-51e9-9db4-88c2-16b8067fed7f
    OperationStatus           : Succeeded

## <a name="next-steps"></a><span data-ttu-id="5a69f-193">Next steps</span><span class="sxs-lookup"><span data-stu-id="5a69f-193">Next steps</span></span>
<span data-ttu-id="5a69f-194">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="5a69f-194">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>

