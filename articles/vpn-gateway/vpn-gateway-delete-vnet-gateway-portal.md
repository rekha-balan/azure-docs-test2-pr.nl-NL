---
title: 'Delete a virtual network gateway: Azure portal: Resource Manager | Microsoft Docs'
description: Delete a virtual network gateway using PowerShell in the Resource Manager deployment model.
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: vpn-gateway
ms.devlang: na
ms.topic: ''
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/29/2017
ms.author: cherylmc
ms.openlocfilehash: 2944259927cd7806dbdebf8e2cf6a9708f11bcd5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553359"
---
# <a name="delete-a-virtual-network-gateway-using-the-portal"></a><span data-ttu-id="52c48-103">Delete a virtual network gateway using the portal</span><span class="sxs-lookup"><span data-stu-id="52c48-103">Delete a virtual network gateway using the portal</span></span>
> [!div class="op_single_selector"]
> * [Resource Manager - Azure portal](vpn-gateway-delete-vnet-gateway-portal.md)
> * [Resource Manager - PowerShell](vpn-gateway-delete-vnet-gateway-powershell.md)
> * [Classic - PowerShell](vpn-gateway-delete-vnet-gateway-classic-powershell.md)
>
>

<span data-ttu-id="52c48-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span><span class="sxs-lookup"><span data-stu-id="52c48-107">There are a couple of different approaches you can take when you want to delete a virtual network gateway for a VPN gateway configuration.</span></span>

- <span data-ttu-id="52c48-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span><span class="sxs-lookup"><span data-stu-id="52c48-108">If you want to delete everything and start over, as in the case of a test environment, you can delete the resource group.</span></span> <span data-ttu-id="52c48-109">When you delete a resource group, it deletes all the resources within the group.</span><span class="sxs-lookup"><span data-stu-id="52c48-109">When you delete a resource group, it deletes all the resources within the group.</span></span> <span data-ttu-id="52c48-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="52c48-110">This is method is only recommended if you don't want to keep any of the resources in the resource group.</span></span> <span data-ttu-id="52c48-111">You can't selectively delete only a few resources using this approach.</span><span class="sxs-lookup"><span data-stu-id="52c48-111">You can't selectively delete only a few resources using this approach.</span></span>

- <span data-ttu-id="52c48-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span><span class="sxs-lookup"><span data-stu-id="52c48-112">If you want to keep some of the resources in your resource group, deleting a virtual network gateway becomes slightly more complicated.</span></span> <span data-ttu-id="52c48-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span><span class="sxs-lookup"><span data-stu-id="52c48-113">Before you can delete the virtual network gateway, you must first delete any resources that are dependent on the gateway.</span></span> <span data-ttu-id="52c48-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span><span class="sxs-lookup"><span data-stu-id="52c48-114">The steps you follow depend on the type of connections that you created and the dependent resources for each connection.</span></span>

##<a name="deletegw"></a><span data-ttu-id="52c48-115">Delete a VPN gateway</span><span class="sxs-lookup"><span data-stu-id="52c48-115">Delete a VPN gateway</span></span>

<span data-ttu-id="52c48-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span><span class="sxs-lookup"><span data-stu-id="52c48-116">To delete a virtual network gateway, you must first delete each resource that pertains to the virtual network gateway.</span></span> <span data-ttu-id="52c48-117">Resources must be deleted in a certain order due to dependencies.</span><span class="sxs-lookup"><span data-stu-id="52c48-117">Resources must be deleted in a certain order due to dependencies.</span></span>

###<a name="step-1-navigate-to-the-virtual-network-gateway"></a><span data-ttu-id="52c48-118">Step 1: Navigate to the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="52c48-118">Step 1: Navigate to the virtual network gateway</span></span>

<span data-ttu-id="52c48-119">In the [Azure portal](https://portal.azure.com), in **All resources**, click the virtual network gateway that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="52c48-119">In the [Azure portal](https://portal.azure.com), in **All resources**, click the virtual network gateway that you want to delete.</span></span> <span data-ttu-id="52c48-120">The graphic for a gateway is:</span><span class="sxs-lookup"><span data-stu-id="52c48-120">The graphic for a gateway is:</span></span>

![Locate virtual network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/gw.png)

###<a name="step-2-delete-connections"></a><span data-ttu-id="52c48-122">Step 2: Delete connections</span><span class="sxs-lookup"><span data-stu-id="52c48-122">Step 2: Delete connections</span></span>

1. <span data-ttu-id="52c48-123">On the blade for your virtual network gateway, click **Connections** to view all connections to the gateway.</span><span class="sxs-lookup"><span data-stu-id="52c48-123">On the blade for your virtual network gateway, click **Connections** to view all connections to the gateway.</span></span>
2. <span data-ttu-id="52c48-124">Click the **...** on the row of the name of the connection, then select **Delete** from the dropdown.</span><span class="sxs-lookup"><span data-stu-id="52c48-124">Click the **...** on the row of the name of the connection, then select **Delete** from the dropdown.</span></span>
3. <span data-ttu-id="52c48-125">Click **Yes** to confirm that you want to delete the connection.</span><span class="sxs-lookup"><span data-stu-id="52c48-125">Click **Yes** to confirm that you want to delete the connection.</span></span> <span data-ttu-id="52c48-126">If you have multiple connections, delete each connection.</span><span class="sxs-lookup"><span data-stu-id="52c48-126">If you have multiple connections, delete each connection.</span></span>

###<a name="step-3-delete-the-local-network-gateways"></a><span data-ttu-id="52c48-127">Step 3: Delete the local network gateways</span><span class="sxs-lookup"><span data-stu-id="52c48-127">Step 3: Delete the local network gateways</span></span>
1. <span data-ttu-id="52c48-128">In **All resources**, locate the local network gateways that were associated with each connection.</span><span class="sxs-lookup"><span data-stu-id="52c48-128">In **All resources**, locate the local network gateways that were associated with each connection.</span></span> <span data-ttu-id="52c48-129">The graphic for a local network gateway is:</span><span class="sxs-lookup"><span data-stu-id="52c48-129">The graphic for a local network gateway is:</span></span>

    ![Locate local network gateway](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/lng.png)
2. <span data-ttu-id="52c48-131">On the **Overview** blade for the local network gateway, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="52c48-131">On the **Overview** blade for the local network gateway, click **Delete**.</span></span>

###<a name="step-4-delete-the-virtual-network-gateway"></a><span data-ttu-id="52c48-132">Step 4: Delete the virtual network gateway</span><span class="sxs-lookup"><span data-stu-id="52c48-132">Step 4: Delete the virtual network gateway</span></span>
1. <span data-ttu-id="52c48-133">In **All resources**, locate the virtual network gateway that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="52c48-133">In **All resources**, locate the virtual network gateway that you want to delete.</span></span>
2. <span data-ttu-id="52c48-134">On the **Overview** blade, click **Delete** to delete the gateway.</span><span class="sxs-lookup"><span data-stu-id="52c48-134">On the **Overview** blade, click **Delete** to delete the gateway.</span></span>

>[!NOTE]
> If you have a P2S configuration to this VNet in addition to your S2S configuration, deleting the virtual network gateway will automatically disconnect all P2S clients without warning.
>
>

###<a name="step-5-delete-the-public-ip-address-for-the-gateway"></a><span data-ttu-id="52c48-136">Step 5: Delete the Public IP address for the gateway</span><span class="sxs-lookup"><span data-stu-id="52c48-136">Step 5: Delete the Public IP address for the gateway</span></span>

1. <span data-ttu-id="52c48-137">In **All resources**, locate the Public IP address that was assigned to the gateway.</span><span class="sxs-lookup"><span data-stu-id="52c48-137">In **All resources**, locate the Public IP address that was assigned to the gateway.</span></span> <span data-ttu-id="52c48-138">If the virtual network gateway was active-active, you will see two Public IP addresses.</span><span class="sxs-lookup"><span data-stu-id="52c48-138">If the virtual network gateway was active-active, you will see two Public IP addresses.</span></span> <span data-ttu-id="52c48-139">The graphic for a Public IP address is:</span><span class="sxs-lookup"><span data-stu-id="52c48-139">The graphic for a Public IP address is:</span></span>

    ![Public IP address](https://docstestmedia1.blob.core.windows.net/azure-media/articles/vpn-gateway/media/vpn-gateway-delete-vnet-gateway-portal/pip.png)

2. <span data-ttu-id="52c48-141">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span><span class="sxs-lookup"><span data-stu-id="52c48-141">On the **Overview** page for the Public IP address, click **Delete**, then **Yes** to confirm.</span></span>

###<a name="step-6-delete-the-gateway-subnet"></a><span data-ttu-id="52c48-142">Step 6: Delete the gateway subnet</span><span class="sxs-lookup"><span data-stu-id="52c48-142">Step 6: Delete the gateway subnet</span></span>

1. <span data-ttu-id="52c48-143">In **All resources**, locate the virtual network.</span><span class="sxs-lookup"><span data-stu-id="52c48-143">In **All resources**, locate the virtual network.</span></span> 
2. <span data-ttu-id="52c48-144">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="52c48-144">On the **Subnets** blade, click the **GatewaySubnet**, then click **Delete**.</span></span> 
3. <span data-ttu-id="52c48-145">Click **Yes** to confirm that you want to delete the gateway subnet.</span><span class="sxs-lookup"><span data-stu-id="52c48-145">Click **Yes** to confirm that you want to delete the gateway subnet.</span></span>

##<a name="deleterg"></a><span data-ttu-id="52c48-146">Delete a VPN gateway by deleting the resource group</span><span class="sxs-lookup"><span data-stu-id="52c48-146">Delete a VPN gateway by deleting the resource group</span></span>

<span data-ttu-id="52c48-147">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span><span class="sxs-lookup"><span data-stu-id="52c48-147">If you are not concerned about keeping any of your resources in the resource group and you just want to start over, you can delete an entire resource group.</span></span> <span data-ttu-id="52c48-148">This is a quick way to remove everything.</span><span class="sxs-lookup"><span data-stu-id="52c48-148">This is a quick way to remove everything.</span></span> <span data-ttu-id="52c48-149">The following steps apply only to the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="52c48-149">The following steps apply only to the Resource Manager deployment model.</span></span>

1. <span data-ttu-id="52c48-150">In **All resources**, locate the resource group and click to open the blade.</span><span class="sxs-lookup"><span data-stu-id="52c48-150">In **All resources**, locate the resource group and click to open the blade.</span></span>
2. <span data-ttu-id="52c48-151">Click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="52c48-151">Click **Delete**.</span></span> <span data-ttu-id="52c48-152">On the Delete blade, view the affected resources.</span><span class="sxs-lookup"><span data-stu-id="52c48-152">On the Delete blade, view the affected resources.</span></span> <span data-ttu-id="52c48-153">Make sure that you want to delete all of these resources.</span><span class="sxs-lookup"><span data-stu-id="52c48-153">Make sure that you want to delete all of these resources.</span></span> <span data-ttu-id="52c48-154">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span><span class="sxs-lookup"><span data-stu-id="52c48-154">If not, use the steps in [Delete a VPN gateway](#deletegw) at the top of this article.</span></span>
3. <span data-ttu-id="52c48-155">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="52c48-155">To proceed, type the name of the resource group that you want to delete, then click **Delete**.</span></span>


