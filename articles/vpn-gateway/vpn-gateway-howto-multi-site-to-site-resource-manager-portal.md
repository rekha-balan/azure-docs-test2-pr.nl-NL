---
title: How to add multiple VPN gateway Site-to-Site connections to a virtual network for the Resource Manager deployment model using the Azure portal | Microsoft Docs
description: Add multi-site S2S connections to a VPN gateway that has an existing connection
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: carmonm
editor: ''
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/10/2016
ms.author: cherylmc
ms.openlocfilehash: 39fb4590a35bbcf818d08d929386465a303bd9c4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556029"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="a1235-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span><span class="sxs-lookup"><span data-stu-id="a1235-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [Classic - PowerShell](vpn-gateway-multi-site.md)
> 
> 

<span data-ttu-id="a1235-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-106">This article walks you through using the Azure portal to add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection.</span></span> <span data-ttu-id="a1235-107">This type of connection is often referred to as a "multi-site" configuration.</span><span class="sxs-lookup"><span data-stu-id="a1235-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> 

<span data-ttu-id="a1235-108">You can use this article to add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-108">You can use this article to add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="a1235-109">There are some limitations when adding connections.</span><span class="sxs-lookup"><span data-stu-id="a1235-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="a1235-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span><span class="sxs-lookup"><span data-stu-id="a1235-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="a1235-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="a1235-111">This article applies to VNets created using the Resource Manager deployment model that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="a1235-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span><span class="sxs-lookup"><span data-stu-id="a1235-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="a1235-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span><span class="sxs-lookup"><span data-stu-id="a1235-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="a1235-114">Deployment models and methods</span><span class="sxs-lookup"><span data-stu-id="a1235-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="a1235-115">We update this table as new articles and additional tools become available for this configuration.</span><span class="sxs-lookup"><span data-stu-id="a1235-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="a1235-116">When an article is available, we link directly to it from this table.</span><span class="sxs-lookup"><span data-stu-id="a1235-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a><span data-ttu-id="a1235-117">Before you begin</span><span class="sxs-lookup"><span data-stu-id="a1235-117">Before you begin</span></span>
<span data-ttu-id="a1235-118">Verify the following items:</span><span class="sxs-lookup"><span data-stu-id="a1235-118">Verify the following items:</span></span>

* <span data-ttu-id="a1235-119">You are not creating an ExpressRoute/S2S coexisting connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="a1235-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="a1235-121">The virtual network gateway for your VNet is RouteBased.</span><span class="sxs-lookup"><span data-stu-id="a1235-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="a1235-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RoutBased.</span><span class="sxs-lookup"><span data-stu-id="a1235-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RoutBased.</span></span>
* <span data-ttu-id="a1235-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span><span class="sxs-lookup"><span data-stu-id="a1235-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="a1235-124">You have compatible VPN device and someone who is able to configure it.</span><span class="sxs-lookup"><span data-stu-id="a1235-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="a1235-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="a1235-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="a1235-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span><span class="sxs-lookup"><span data-stu-id="a1235-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="a1235-127">You have an externally facing public IP address for your VPN device.</span><span class="sxs-lookup"><span data-stu-id="a1235-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="a1235-128">This IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="a1235-128">This IP address cannot be located behind a NAT.</span></span>

## <a name="part1"></a><span data-ttu-id="a1235-129">Part 1 - Configure a connection</span><span class="sxs-lookup"><span data-stu-id="a1235-129">Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="a1235-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="a1235-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="a1235-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span><span class="sxs-lookup"><span data-stu-id="a1235-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="a1235-132">On the **Virtual network gateway** blade, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="a1235-132">On the **Virtual network gateway** blade, click **Connections**.</span></span>
   
    <span data-ttu-id="a1235-133">![Connections blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span><span class="sxs-lookup"><span data-stu-id="a1235-133">![Connections blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections blade")</span></span><br>
4. <span data-ttu-id="a1235-134">On the **Connections** blade, click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="a1235-134">On the **Connections** blade, click **+Add**.</span></span>
   
    <span data-ttu-id="a1235-135">![Add connection button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="a1235-135">![Add connection button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="a1235-136">On the **Add connection** blade, fill out the following fields:</span><span class="sxs-lookup"><span data-stu-id="a1235-136">On the **Add connection** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="a1235-137">**Name:** The name you want to give to the site you are creating the connection to.</span><span class="sxs-lookup"><span data-stu-id="a1235-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="a1235-138">**Connection type:** Select **Site-to-site (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="a1235-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="a1235-139">![Add connection blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span><span class="sxs-lookup"><span data-stu-id="a1235-139">![Add connection blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection blade")</span></span><br>

## <a name="part2"></a><span data-ttu-id="a1235-140">Part 2 - Add a local network gateway</span><span class="sxs-lookup"><span data-stu-id="a1235-140">Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="a1235-141">Click **Local network gateway** ***Choose a local network gateway***.</span><span class="sxs-lookup"><span data-stu-id="a1235-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="a1235-142">This will open the **Choose local network gateway** blade.</span><span class="sxs-lookup"><span data-stu-id="a1235-142">This will open the **Choose local network gateway** blade.</span></span>
   
    <span data-ttu-id="a1235-143">![Choose local network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="a1235-143">![Choose local network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="a1235-144">Click **Create new** to open the **Create local network gateway** blade.</span><span class="sxs-lookup"><span data-stu-id="a1235-144">Click **Create new** to open the **Create local network gateway** blade.</span></span>
   
    <span data-ttu-id="a1235-145">![Create local network gateway blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="a1235-145">![Create local network gateway blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="a1235-146">On the **Create local network gateway** blade, fill out the following fields:</span><span class="sxs-lookup"><span data-stu-id="a1235-146">On the **Create local network gateway** blade, fill out the following fields:</span></span>
   
   * <span data-ttu-id="a1235-147">**Name:** The name you want to give to the local network gateway resource.</span><span class="sxs-lookup"><span data-stu-id="a1235-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="a1235-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="a1235-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="a1235-149">**Address space:** The address space that you want to be routed to the new local network site.</span><span class="sxs-lookup"><span data-stu-id="a1235-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="a1235-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span><span class="sxs-lookup"><span data-stu-id="a1235-150">Click **OK** on the **Create local network gateway** blade to save the changes.</span></span>

## <a name="part3"></a><span data-ttu-id="a1235-151">Part 3 - Add the shared key and create the connection</span><span class="sxs-lookup"><span data-stu-id="a1235-151">Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="a1235-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-152">On the **Add connection** blade, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="a1235-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span><span class="sxs-lookup"><span data-stu-id="a1235-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="a1235-154">The important thing is that the keys are exactly the same.</span><span class="sxs-lookup"><span data-stu-id="a1235-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="a1235-155">![Shared key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="a1235-155">![Shared key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="a1235-156">At the bottom of the blade, click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="a1235-156">At the bottom of the blade, click **OK** to create the connection.</span></span>

## <a name="part4"></a><span data-ttu-id="a1235-157">Part 4 - Verify the VPN connection</span><span class="sxs-lookup"><span data-stu-id="a1235-157">Part 4 - Verify the VPN connection</span></span>
<span data-ttu-id="a1235-158">You can verify your VPN connection either in the portal, or by using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a1235-158">You can verify your VPN connection either in the portal, or by using PowerShell.</span></span>

[!INCLUDE [vpn-gateway-verify-connection-rm](../../includes/vpn-gateway-verify-connection-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="a1235-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1235-159">Next steps</span></span>
* <span data-ttu-id="a1235-160">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="a1235-160">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="a1235-161">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span><span class="sxs-lookup"><span data-stu-id="a1235-161">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>







