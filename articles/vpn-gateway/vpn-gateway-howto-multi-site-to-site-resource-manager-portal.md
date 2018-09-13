---
title: 'Add multiple VPN gateway Site-to-Site connections to a VNet: Azure Portal: Resource Manager| Microsoft Docs'
description: Add multi-site S2S connections to a VPN gateway that has an existing connection
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: jpconnock
editor: ''
tags: azure-resource-manager
ms.assetid: f3e8b165-f20a-42ab-afbb-bf60974bb4b1
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/14/2018
ms.author: cherylmc
ms.openlocfilehash: 4e7d2acecfe94401d7ce3b608ad20857c2ba4061
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44819018"
---
# <a name="add-a-site-to-site-connection-to-a-vnet-with-an-existing-vpn-gateway-connection"></a><span data-ttu-id="bfab9-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span><span class="sxs-lookup"><span data-stu-id="bfab9-103">Add a Site-to-Site connection to a VNet with an existing VPN gateway connection</span></span>

> [!div class="op_single_selector"]
> * [Azure portal](vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)
> * [PowerShell (classic)](vpn-gateway-multi-site.md)
>
> 

<span data-ttu-id="bfab9-106">This article helps you add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="bfab9-106">This article helps you add Site-to-Site (S2S) connections to a VPN gateway that has an existing connection by using the Azure portal.</span></span> <span data-ttu-id="bfab9-107">This type of connection is often referred to as a "multi-site" configuration.</span><span class="sxs-lookup"><span data-stu-id="bfab9-107">This type of connection is often referred to as a "multi-site" configuration.</span></span> <span data-ttu-id="bfab9-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span><span class="sxs-lookup"><span data-stu-id="bfab9-108">You can add a S2S connection to a VNet that already has a S2S connection, Point-to-Site connection, or VNet-to-VNet connection.</span></span> <span data-ttu-id="bfab9-109">There are some limitations when adding connections.</span><span class="sxs-lookup"><span data-stu-id="bfab9-109">There are some limitations when adding connections.</span></span> <span data-ttu-id="bfab9-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span><span class="sxs-lookup"><span data-stu-id="bfab9-110">Check the [Before you begin](#before) section in this article to verify before you start your configuration.</span></span> 

<span data-ttu-id="bfab9-111">This article applies to Resource Manager VNets that have a RouteBased VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="bfab9-111">This article applies to Resource Manager VNets that have a RouteBased VPN gateway.</span></span> <span data-ttu-id="bfab9-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span><span class="sxs-lookup"><span data-stu-id="bfab9-112">These steps do not apply to ExpressRoute/Site-to-Site coexisting connection configurations.</span></span> <span data-ttu-id="bfab9-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span><span class="sxs-lookup"><span data-stu-id="bfab9-113">See [ExpressRoute/S2S coexisting connections](../expressroute/expressroute-howto-coexist-resource-manager.md) for information about coexisting connections.</span></span>

### <a name="deployment-models-and-methods"></a><span data-ttu-id="bfab9-114">Deployment models and methods</span><span class="sxs-lookup"><span data-stu-id="bfab9-114">Deployment models and methods</span></span>
[!INCLUDE [vpn-gateway-clasic-rm](../../includes/vpn-gateway-classic-rm-include.md)]

<span data-ttu-id="bfab9-115">We update this table as new articles and additional tools become available for this configuration.</span><span class="sxs-lookup"><span data-stu-id="bfab9-115">We update this table as new articles and additional tools become available for this configuration.</span></span> <span data-ttu-id="bfab9-116">When an article is available, we link directly to it from this table.</span><span class="sxs-lookup"><span data-stu-id="bfab9-116">When an article is available, we link directly to it from this table.</span></span>

[!INCLUDE [vpn-gateway-table-multi-site](../../includes/vpn-gateway-table-multisite-include.md)]

## <a name="before"></a><span data-ttu-id="bfab9-117">Before you begin</span><span class="sxs-lookup"><span data-stu-id="bfab9-117">Before you begin</span></span>
<span data-ttu-id="bfab9-118">Verify the following items:</span><span class="sxs-lookup"><span data-stu-id="bfab9-118">Verify the following items:</span></span>

* <span data-ttu-id="bfab9-119">You are not creating an ExpressRoute/S2S coexisting connection.</span><span class="sxs-lookup"><span data-stu-id="bfab9-119">You are not creating an ExpressRoute/S2S coexisting connection.</span></span>
* <span data-ttu-id="bfab9-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span><span class="sxs-lookup"><span data-stu-id="bfab9-120">You have a virtual network that was created using the Resource Manager deployment model with an existing connection.</span></span>
* <span data-ttu-id="bfab9-121">The virtual network gateway for your VNet is RouteBased.</span><span class="sxs-lookup"><span data-stu-id="bfab9-121">The virtual network gateway for your VNet is RouteBased.</span></span> <span data-ttu-id="bfab9-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span><span class="sxs-lookup"><span data-stu-id="bfab9-122">If you have a PolicyBased VPN gateway, you must delete the virtual network gateway and create a new VPN gateway as RouteBased.</span></span>
* <span data-ttu-id="bfab9-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span><span class="sxs-lookup"><span data-stu-id="bfab9-123">None of the address ranges overlap for any of the VNets that this VNet is connecting to.</span></span>
* <span data-ttu-id="bfab9-124">You have compatible VPN device and someone who is able to configure it.</span><span class="sxs-lookup"><span data-stu-id="bfab9-124">You have compatible VPN device and someone who is able to configure it.</span></span> <span data-ttu-id="bfab9-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span><span class="sxs-lookup"><span data-stu-id="bfab9-125">See [About VPN Devices](vpn-gateway-about-vpn-devices.md).</span></span> <span data-ttu-id="bfab9-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span><span class="sxs-lookup"><span data-stu-id="bfab9-126">If you aren't familiar with configuring your VPN device, or are unfamiliar with the IP address ranges located in your on-premises network configuration, you need to coordinate with someone who can provide those details for you.</span></span>
* <span data-ttu-id="bfab9-127">You have an externally facing public IP address for your VPN device.</span><span class="sxs-lookup"><span data-stu-id="bfab9-127">You have an externally facing public IP address for your VPN device.</span></span> <span data-ttu-id="bfab9-128">This IP address cannot be located behind a NAT.</span><span class="sxs-lookup"><span data-stu-id="bfab9-128">This IP address cannot be located behind a NAT.</span></span>

## <a name="part1"></a><span data-ttu-id="bfab9-129">Part 1 - Configure a connection</span><span class="sxs-lookup"><span data-stu-id="bfab9-129">Part 1 - Configure a connection</span></span>
1. <span data-ttu-id="bfab9-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span><span class="sxs-lookup"><span data-stu-id="bfab9-130">From a browser, navigate to the [Azure portal](http://portal.azure.com) and, if necessary, sign in with your Azure account.</span></span>
2. <span data-ttu-id="bfab9-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span><span class="sxs-lookup"><span data-stu-id="bfab9-131">Click **All resources** and locate your **virtual network gateway** from the list of resources and click it.</span></span>
3. <span data-ttu-id="bfab9-132">On the **Virtual network gateway** page, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="bfab9-132">On the **Virtual network gateway** page, click **Connections**.</span></span>
   
    <span data-ttu-id="bfab9-133">![Connections page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections page")</span><span class="sxs-lookup"><span data-stu-id="bfab9-133">![Connections page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/connectionsblade.png "Connections page")</span></span><br>
4. <span data-ttu-id="bfab9-134">On the **Connections** page, click **+Add**.</span><span class="sxs-lookup"><span data-stu-id="bfab9-134">On the **Connections** page, click **+Add**.</span></span>
   
    <span data-ttu-id="bfab9-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span><span class="sxs-lookup"><span data-stu-id="bfab9-135">![Add connection button](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addbutton.png "Add connection button")</span></span><br>
5. <span data-ttu-id="bfab9-136">On the **Add connection** page, fill out the following fields:</span><span class="sxs-lookup"><span data-stu-id="bfab9-136">On the **Add connection** page, fill out the following fields:</span></span>
   
   * <span data-ttu-id="bfab9-137">**Name:** The name you want to give to the site you are creating the connection to.</span><span class="sxs-lookup"><span data-stu-id="bfab9-137">**Name:** The name you want to give to the site you are creating the connection to.</span></span>
   * <span data-ttu-id="bfab9-138">**Connection type:** Select **Site-to-site (IPsec)**.</span><span class="sxs-lookup"><span data-stu-id="bfab9-138">**Connection type:** Select **Site-to-site (IPsec)**.</span></span>
     
     <span data-ttu-id="bfab9-139">![Add connection page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection page")</span><span class="sxs-lookup"><span data-stu-id="bfab9-139">![Add connection page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/addconnectionblade.png "Add connection page")</span></span><br>

## <a name="part2"></a><span data-ttu-id="bfab9-140">Part 2 - Add a local network gateway</span><span class="sxs-lookup"><span data-stu-id="bfab9-140">Part 2 - Add a local network gateway</span></span>
1. <span data-ttu-id="bfab9-141">Click **Local network gateway** ***Choose a local network gateway***.</span><span class="sxs-lookup"><span data-stu-id="bfab9-141">Click **Local network gateway** ***Choose a local network gateway***.</span></span> <span data-ttu-id="bfab9-142">This will open the **Choose local network gateway** page.</span><span class="sxs-lookup"><span data-stu-id="bfab9-142">This will open the **Choose local network gateway** page.</span></span>
   
    <span data-ttu-id="bfab9-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span><span class="sxs-lookup"><span data-stu-id="bfab9-143">![Choose local network gateway](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/chooselng.png "Choose local network gateway")</span></span><br>
2. <span data-ttu-id="bfab9-144">Click **Create new** to open the **Create local network gateway** page.</span><span class="sxs-lookup"><span data-stu-id="bfab9-144">Click **Create new** to open the **Create local network gateway** page.</span></span>
   
    <span data-ttu-id="bfab9-145">![Create local network gateway page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span><span class="sxs-lookup"><span data-stu-id="bfab9-145">![Create local network gateway page](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/createlngblade.png "Create local network gateway")</span></span><br>
3. <span data-ttu-id="bfab9-146">On the **Create local network gateway** page, fill out the following fields:</span><span class="sxs-lookup"><span data-stu-id="bfab9-146">On the **Create local network gateway** page, fill out the following fields:</span></span>
   
   * <span data-ttu-id="bfab9-147">**Name:** The name you want to give to the local network gateway resource.</span><span class="sxs-lookup"><span data-stu-id="bfab9-147">**Name:** The name you want to give to the local network gateway resource.</span></span>
   * <span data-ttu-id="bfab9-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span><span class="sxs-lookup"><span data-stu-id="bfab9-148">**IP address:** The public IP address of the VPN device on the site that you want to connect to.</span></span>
   * <span data-ttu-id="bfab9-149">**Address space:** The address space that you want to be routed to the new local network site.</span><span class="sxs-lookup"><span data-stu-id="bfab9-149">**Address space:** The address space that you want to be routed to the new local network site.</span></span>
4. <span data-ttu-id="bfab9-150">Click **OK** on the **Create local network gateway** page to save the changes.</span><span class="sxs-lookup"><span data-stu-id="bfab9-150">Click **OK** on the **Create local network gateway** page to save the changes.</span></span>

## <a name="part3"></a><span data-ttu-id="bfab9-151">Part 3 - Add the shared key and create the connection</span><span class="sxs-lookup"><span data-stu-id="bfab9-151">Part 3 - Add the shared key and create the connection</span></span>
1. <span data-ttu-id="bfab9-152">On the **Add connection** page, add the shared key that you want to use to create your connection.</span><span class="sxs-lookup"><span data-stu-id="bfab9-152">On the **Add connection** page, add the shared key that you want to use to create your connection.</span></span> <span data-ttu-id="bfab9-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span><span class="sxs-lookup"><span data-stu-id="bfab9-153">You can either get the shared key from your VPN device, or make one up here and then configure your VPN device to use the same shared key.</span></span> <span data-ttu-id="bfab9-154">The important thing is that the keys are exactly the same.</span><span class="sxs-lookup"><span data-stu-id="bfab9-154">The important thing is that the keys are exactly the same.</span></span>
   
    <span data-ttu-id="bfab9-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span><span class="sxs-lookup"><span data-stu-id="bfab9-155">![Shared key](./media/vpn-gateway-howto-multi-site-to-site-resource-manager-portal/sharedkey.png "Shared key")</span></span><br>
2. <span data-ttu-id="bfab9-156">At the bottom of the page, click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="bfab9-156">At the bottom of the page, click **OK** to create the connection.</span></span>

## <a name="part4"></a><span data-ttu-id="bfab9-157">Part 4 - Verify the VPN connection</span><span class="sxs-lookup"><span data-stu-id="bfab9-157">Part 4 - Verify the VPN connection</span></span>


[!INCLUDE [vpn-gateway-verify-connection-ps-rm](../../includes/vpn-gateway-verify-connection-ps-rm-include.md)]

## <a name="next-steps"></a><span data-ttu-id="bfab9-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="bfab9-158">Next steps</span></span>

<span data-ttu-id="bfab9-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span><span class="sxs-lookup"><span data-stu-id="bfab9-159">Once your connection is complete, you can add virtual machines to your virtual networks.</span></span> <span data-ttu-id="bfab9-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span><span class="sxs-lookup"><span data-stu-id="bfab9-160">See the virtual machines [learning path](https://azure.microsoft.com/documentation/learning-paths/virtual-machines) for more information.</span></span>
