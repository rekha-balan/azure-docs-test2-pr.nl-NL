---
title: 'Connect a virtual network to multiple sites using VPN Gateway and PowerShell : Classic | Microsoft Docs'
description: Connect multiple local on-premises sites to a classic virtual network using a VPN Gateway.
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
ms.date: 02/14/2018
ms.author: yushwang
ms.openlocfilehash: 3c733e125b860fd7fb3d593ba79395d0ba467990
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819005"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection-classic"></a><span data-ttu-id="7efd1-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span><span class="sxs-lookup"><span data-stu-id="7efd1-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection (classic)</span></span>

[!INCLUDE [deployment models](../../includes/vpn-gateway-classic-deployment-model-include.md)]

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classic)](vpn-gateway-multi-site.md)
>
>

<span data-ttu-id="7efd1-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span><span class="sxs-lookup"><span data-stu-id="7efd1-106">This article walks you through using PowerShell to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="7efd1-107">This type of connection is often referred to as a "multi-site" configuration.</span><span class="sxs-lookup"><span data-stu-id="7efd1-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="7efd1-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span><span class="sxs-lookup"><span data-stu-id="7efd1-108">The steps in this article apply to virtual networks created using the classic deployment model (also known as Service Management).</span></span> <span data-ttu-id="7efd1-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span><span class="sxs-lookup"><span data-stu-id="7efd1-109">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="7efd1-110">Deployment models and methods</span><span class="sxs-lookup"><span data-stu-id="7efd1-110">Deployment models and methods</span></span>

[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="7efd1-111">We update this table as new articles and additional tools become available for this configuration.</span><span class="sxs-lookup"><span data-stu-id="7efd1-111">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="7efd1-112">When an article is available, we link directly to it from this table.</span><span class="sxs-lookup"><span data-stu-id="7efd1-112">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="about-connecting"></a><span data-ttu-id="7efd1-113">About connecting</span><span class="sxs-lookup"><span data-stu-id="7efd1-113">About connecting</span></span>

<span data-ttu-id="7efd1-114">You can connect multiple on-premises sites to a single virtual network.</span><span class="sxs-lookup"><span data-stu-id="7efd1-114">You can connect multiple on-premises sites to a single virtual network.</span></span> <span data-ttu-id="7efd1-115">This is especially attractive for building hybrid cloud solutions.</span><span class="sxs-lookup"><span data-stu-id="7efd1-115">This is especially attractive for building hybrid cloud solutions.</span></span> <span data-ttu-id="7efd1-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span><span class="sxs-lookup"><span data-stu-id="7efd1-116">Creating a multi-site connection to your Azure virtual network gateway is similar to creating other Site-to-Site connections.</span></span> <span data-ttu-id="7efd1-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span><span class="sxs-lookup"><span data-stu-id="7efd1-117">In fact, you can use an existing Azure VPN gateway, as long as the gateway is dynamic (route-based).</span></span>

<span data-ttu-id="7efd1-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span><span class="sxs-lookup"><span data-stu-id="7efd1-118">If you already have a static gateway connected to your virtual network, you can change the gateway type to dynamic without needing to rebuild the virtual network in order to accommodate multi-site.</span></span> <span data-ttu-id="7efd1-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span><span class="sxs-lookup"><span data-stu-id="7efd1-119">Before changing the routing type, make sure that your on-premises VPN gateway supports route-based VPN configurations.</span></span>

<span data-ttu-id="7efd1-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span><span class="sxs-lookup"><span data-stu-id="7efd1-120">![multi-site diagram](./media/vpn-gateway-multi-site/multisite.png "multi-site")</span></span>

## <a name="points-to-consider"></a><span data-ttu-id="7efd1-121">Points to consider</span><span class="sxs-lookup"><span data-stu-id="7efd1-121">Points to consider</span></span>

<span data-ttu-id="7efd1-122">**You won't be able to use the portal to make changes to this virtual network.**</span><span class="sxs-lookup"><span data-stu-id="7efd1-122">**You won't be able to use the portal to make changes to this virtual network.**</span></span> <span data-ttu-id="7efd1-123">You need to make changes to the network configuration file instead of using the portal.</span><span class="sxs-lookup"><span data-stu-id="7efd1-123">You need to make changes to the network configuration file instead of using the portal.</span></span> <span data-ttu-id="7efd1-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span><span class="sxs-lookup"><span data-stu-id="7efd1-124">If you make changes in the portal, they'll overwrite your multi-site reference settings for this virtual network.</span></span>

<span data-ttu-id="7efd1-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span><span class="sxs-lookup"><span data-stu-id="7efd1-125">You should feel comfortable using the network configuration file by the time you've completed the multi-site procedure.</span></span> <span data-ttu-id="7efd1-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span><span class="sxs-lookup"><span data-stu-id="7efd1-126">However, if you have multiple people working on your network configuration, you'll need to make sure that everyone knows about this limitation.</span></span> <span data-ttu-id="7efd1-127">This doesn't mean that you can't use the portal at all.</span><span class="sxs-lookup"><span data-stu-id="7efd1-127">This doesn't mean that you can't use the portal at all.</span></span> <span data-ttu-id="7efd1-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span><span class="sxs-lookup"><span data-stu-id="7efd1-128">You can use it for everything else, except making configuration changes to this particular virtual network.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7efd1-129">Before you begin</span><span class="sxs-lookup"><span data-stu-id="7efd1-129">Before you begin</span></span>

<span data-ttu-id="7efd1-130">Before you begin configuration, verify that you have the following:</span><span class="sxs-lookup"><span data-stu-id="7efd1-130">Before you begin configuration, verify that you have the following:</span></span>

* <span data-ttu-id="7efd1-131">Compatible VPN hardware for each on-premises location.</span><span class="sxs-lookup"><span data-stu-id="7efd1-131">Compatible VPN hardware for each on-premises location.</span></span> <span data-ttu-id="7efd1-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span><span class="sxs-lookup"><span data-stu-id="7efd1-132">Check [About VPN Devices for Virtual Network Connectivity](vpn-gateway-about-vpn-devices.md) to verify if the device that you want to use is something that is known to be compatible.</span></span>
* <span data-ttu-id="7efd1-133">An externally facing public IPv4 IP address for each VPN device.</span><span class="sxs-lookup"><span data-stu-id="7efd1-133">An externally facing public IPv4 IP address for each VPN device.</span></span> <span data-ttu-id="7efd1-134">The IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="7efd1-134">The IP address cannot be located behind a NAT.</span></span> <span data-ttu-id="7efd1-135">This is requirement.</span><span class="sxs-lookup"><span data-stu-id="7efd1-135">This is requirement.</span></span>
* <span data-ttu-id="7efd1-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="7efd1-136">You'll need to install the latest version of the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="7efd1-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span><span class="sxs-lookup"><span data-stu-id="7efd1-137">Make sure you install the Service Management (SM) version in addition to the Resource Manager version.</span></span> <span data-ttu-id="7efd1-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span><span class="sxs-lookup"><span data-stu-id="7efd1-138">See [How to install and configure Azure PowerShell](/powershell/azure/overview) for more information.</span></span>
* <span data-ttu-id="7efd1-139">Someone who is proficient at configuring your VPN hardware.</span><span class="sxs-lookup"><span data-stu-id="7efd1-139">Someone who is proficient at configuring your VPN hardware.</span></span> <span data-ttu-id="7efd1-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span><span class="sxs-lookup"><span data-stu-id="7efd1-140">You'll have to have a strong understanding of how to configure your VPN device, or work with someone who does.</span></span>
* <span data-ttu-id="7efd1-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span><span class="sxs-lookup"><span data-stu-id="7efd1-141">The IP address ranges that you want to use for your virtual network (if you haven't already created one).</span></span>
* <span data-ttu-id="7efd1-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span><span class="sxs-lookup"><span data-stu-id="7efd1-142">The IP address ranges for each of the local network sites that you'll be connecting to.</span></span> <span data-ttu-id="7efd1-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span><span class="sxs-lookup"><span data-stu-id="7efd1-143">You'll need to make sure that the IP address ranges for each of the local network sites that you want to connect to do not overlap.</span></span> <span data-ttu-id="7efd1-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span><span class="sxs-lookup"><span data-stu-id="7efd1-144">Otherwise, the portal or the REST API will reject the configuration being uploaded.</span></span><br><span data-ttu-id="7efd1-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span><span class="sxs-lookup"><span data-stu-id="7efd1-145">For example, if you have two local network sites that both contain the IP address range 10.2.3.0/24 and you have a package with a destination address 10.2.3.3, Azure wouldn't know which site you want to send the package to because the address ranges are overlapping.</span></span> <span data-ttu-id="7efd1-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span><span class="sxs-lookup"><span data-stu-id="7efd1-146">To prevent routing issues, Azure doesn't allow you to upload a configuration file that has overlapping ranges.</span></span>

## <a name="1-create-a-site-to-site-vpn"></a><span data-ttu-id="7efd1-147">1. Create a Site-to-Site VPN</span><span class="sxs-lookup"><span data-stu-id="7efd1-147">1. Create a Site-to-Site VPN</span></span>
<span data-ttu-id="7efd1-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span><span class="sxs-lookup"><span data-stu-id="7efd1-148">If you already have a Site-to-Site VPN with a dynamic routing gateway, great!</span></span> <span data-ttu-id="7efd1-149">You can proceed to [Export the virtual network configuration settings](#export).</span><span class="sxs-lookup"><span data-stu-id="7efd1-149">You can proceed to [Export the virtual network configuration settings](#export).</span></span> <span data-ttu-id="7efd1-150">If not, do the following:</span><span class="sxs-lookup"><span data-stu-id="7efd1-150">If not, do the following:</span></span>

### <a name="if-you-already-have-a-site-to-site-virtual-network-but-it-has-a-static-policy-based-routing-gateway"></a><span data-ttu-id="7efd1-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span><span class="sxs-lookup"><span data-stu-id="7efd1-151">If you already have a Site-to-Site virtual network, but it has a static (policy-based) routing gateway:</span></span>
1. <span data-ttu-id="7efd1-152">Change your gateway type to dynamic routing.</span><span class="sxs-lookup"><span data-stu-id="7efd1-152">Change your gateway type to dynamic routing.</span></span> <span data-ttu-id="7efd1-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span><span class="sxs-lookup"><span data-stu-id="7efd1-153">A multi-site VPN requires a dynamic (also known as route-based) routing gateway.</span></span> <span data-ttu-id="7efd1-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span><span class="sxs-lookup"><span data-stu-id="7efd1-154">To change your gateway type, you'll need to first delete the existing gateway, then create a new one.</span></span>
2. <span data-ttu-id="7efd1-155">Configure your new gateway and create your VPN tunnel.</span><span class="sxs-lookup"><span data-stu-id="7efd1-155">Configure your new gateway and create your VPN tunnel.</span></span> <span data-ttu-id="7efd1-156">For instructions, For instructions, see [Specify the SKU and VPN type](vpn-gateway-howto-site-to-site-classic-portal.md#sku).</span><span class="sxs-lookup"><span data-stu-id="7efd1-156">For instructions, For instructions, see [Specify the SKU and VPN type](vpn-gateway-howto-site-to-site-classic-portal.md#sku).</span></span> <span data-ttu-id="7efd1-157">Make sure you specify the Routing Type as 'Dynamic'.</span><span class="sxs-lookup"><span data-stu-id="7efd1-157">Make sure you specify the Routing Type as 'Dynamic'.</span></span>

### <a name="if-you-dont-have-a-site-to-site-virtual-network"></a><span data-ttu-id="7efd1-158">If you don't have a Site-to-Site virtual network:</span><span class="sxs-lookup"><span data-stu-id="7efd1-158">If you don't have a Site-to-Site virtual network:</span></span>
1. <span data-ttu-id="7efd1-159">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection](vpn-gateway-site-to-site-create.md).</span><span class="sxs-lookup"><span data-stu-id="7efd1-159">Create your Site-to-Site virtual network using these instructions: [Create a Virtual Network with a Site-to-Site VPN Connection](vpn-gateway-site-to-site-create.md).</span></span>  
2. <span data-ttu-id="7efd1-160">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span><span class="sxs-lookup"><span data-stu-id="7efd1-160">Configure a dynamic routing gateway using these instructions: [Configure a VPN Gateway](vpn-gateway-configure-vpn-gateway-mp.md).</span></span> <span data-ttu-id="7efd1-161">Be sure to select **dynamic routing** for your gateway type.</span><span class="sxs-lookup"><span data-stu-id="7efd1-161">Be sure to select **dynamic routing** for your gateway type.</span></span>

## <a name="export"></a><span data-ttu-id="7efd1-162">2. Export the network configuration file</span><span class="sxs-lookup"><span data-stu-id="7efd1-162">2. Export the network configuration file</span></span>
<span data-ttu-id="7efd1-163">Export your Azure network configuration file by running the following command.</span><span class="sxs-lookup"><span data-stu-id="7efd1-163">Export your Azure network configuration file by running the following command.</span></span> <span data-ttu-id="7efd1-164">You can change the location of the file to export to a different location if necessary.</span><span class="sxs-lookup"><span data-stu-id="7efd1-164">You can change the location of the file to export to a different location if necessary.</span></span>

```powershell
Get-AzureVNetConfig -ExportToFile C:\AzureNet\NetworkConfig.xml
```

## <a name="3-open-the-network-configuration-file"></a><span data-ttu-id="7efd1-165">3. Open the network configuration file</span><span class="sxs-lookup"><span data-stu-id="7efd1-165">3. Open the network configuration file</span></span>
<span data-ttu-id="7efd1-166">Open the network configuration file that you downloaded in the last step.</span><span class="sxs-lookup"><span data-stu-id="7efd1-166">Open the network configuration file that you downloaded in the last step.</span></span> <span data-ttu-id="7efd1-167">Use any xml editor that you like.</span><span class="sxs-lookup"><span data-stu-id="7efd1-167">Use any xml editor that you like.</span></span> <span data-ttu-id="7efd1-168">The file should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7efd1-168">The file should look similar to the following:</span></span>

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

## <a name="4-add-multiple-site-references"></a><span data-ttu-id="7efd1-169">4. Add multiple site references</span><span class="sxs-lookup"><span data-stu-id="7efd1-169">4. Add multiple site references</span></span>
<span data-ttu-id="7efd1-170">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span><span class="sxs-lookup"><span data-stu-id="7efd1-170">When you add or remove site reference information, you'll make configuration changes to the ConnectionsToLocalNetwork/LocalNetworkSiteRef.</span></span> <span data-ttu-id="7efd1-171">Adding a new local site reference triggers Azure to create a new tunnel.</span><span class="sxs-lookup"><span data-stu-id="7efd1-171">Adding a new local site reference triggers Azure to create a new tunnel.</span></span> <span data-ttu-id="7efd1-172">In the example below, the network configuration is for a single-site connection.</span><span class="sxs-lookup"><span data-stu-id="7efd1-172">In the example below, the network configuration is for a single-site connection.</span></span> <span data-ttu-id="7efd1-173">Save the file once you have finished making your changes.</span><span class="sxs-lookup"><span data-stu-id="7efd1-173">Save the file once you have finished making your changes.</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

<span data-ttu-id="7efd1-174">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span><span class="sxs-lookup"><span data-stu-id="7efd1-174">To add additional site references (create a multi-site configuration), simply add additional "LocalNetworkSiteRef" lines, as shown in the example below:</span></span>

```
  <Gateway>
    <ConnectionsToLocalNetwork>
      <LocalNetworkSiteRef name="Site1"><Connection type="IPsec" /></LocalNetworkSiteRef>
      <LocalNetworkSiteRef name="Site2"><Connection type="IPsec" /></LocalNetworkSiteRef>
    </ConnectionsToLocalNetwork>
  </Gateway>
```

## <a name="5-import-the-network-configuration-file"></a><span data-ttu-id="7efd1-175">5. Import the network configuration file</span><span class="sxs-lookup"><span data-stu-id="7efd1-175">5. Import the network configuration file</span></span>
<span data-ttu-id="7efd1-176">Import the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="7efd1-176">Import the network configuration file.</span></span> <span data-ttu-id="7efd1-177">When you import this file with the changes, the new tunnels will be added.</span><span class="sxs-lookup"><span data-stu-id="7efd1-177">When you import this file with the changes, the new tunnels will be added.</span></span> <span data-ttu-id="7efd1-178">The tunnels will use the dynamic gateway that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7efd1-178">The tunnels will use the dynamic gateway that you created earlier.</span></span> <span data-ttu-id="7efd1-179">You can use PowerShell to import the file.</span><span class="sxs-lookup"><span data-stu-id="7efd1-179">You can use PowerShell to import the file.</span></span>

## <a name="6-download-keys"></a><span data-ttu-id="7efd1-180">6. Download keys</span><span class="sxs-lookup"><span data-stu-id="7efd1-180">6. Download keys</span></span>
<span data-ttu-id="7efd1-181">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span><span class="sxs-lookup"><span data-stu-id="7efd1-181">Once your new tunnels have been added, use the PowerShell cmdlet 'Get-AzureVNetGatewayKey' to get the IPsec/IKE pre-shared keys for each tunnel.</span></span>

<span data-ttu-id="7efd1-182">For example:</span><span class="sxs-lookup"><span data-stu-id="7efd1-182">For example:</span></span>

```powershell
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site1"
Get-AzureVNetGatewayKey –VNetName "VNet1" –LocalNetworkSiteName "Site2"
```

<span data-ttu-id="7efd1-183">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span><span class="sxs-lookup"><span data-stu-id="7efd1-183">If you prefer, you can also use the *Get Virtual Network Gateway Shared Key* REST API to get the pre-shared keys.</span></span>

## <a name="7-verify-your-connections"></a><span data-ttu-id="7efd1-184">7. Verify your connections</span><span class="sxs-lookup"><span data-stu-id="7efd1-184">7. Verify your connections</span></span>
<span data-ttu-id="7efd1-185">Check the multi-site tunnel status.</span><span class="sxs-lookup"><span data-stu-id="7efd1-185">Check the multi-site tunnel status.</span></span> <span data-ttu-id="7efd1-186">After downloading the keys for each tunnel, you'll want to verify connections.</span><span class="sxs-lookup"><span data-stu-id="7efd1-186">After downloading the keys for each tunnel, you'll want to verify connections.</span></span> <span data-ttu-id="7efd1-187">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span><span class="sxs-lookup"><span data-stu-id="7efd1-187">Use 'Get-AzureVnetConnection' to get a list of virtual network tunnels, as shown in the example below.</span></span> <span data-ttu-id="7efd1-188">VNet1 is the name of the VNet.</span><span class="sxs-lookup"><span data-stu-id="7efd1-188">VNet1 is the name of the VNet.</span></span>

```powershell
Get-AzureVnetConnection -VNetName VNET1
```

<span data-ttu-id="7efd1-189">Example return:</span><span class="sxs-lookup"><span data-stu-id="7efd1-189">Example return:</span></span>

```
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
```

## <a name="next-steps"></a><span data-ttu-id="7efd1-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="7efd1-190">Next steps</span></span>

<span data-ttu-id="7efd1-191">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span><span class="sxs-lookup"><span data-stu-id="7efd1-191">To learn more about VPN Gateways, see [About VPN Gateways](vpn-gateway-about-vpngateways.md).</span></span>
