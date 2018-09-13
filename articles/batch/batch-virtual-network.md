---
title: Provision Azure Batch pool in a virtual network | Microsoft Docs
description: You can create a Batch pool in a virtual network so that compute nodes can communicate securely with other VMs in the network, such as a file server.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.topic: article
ms.date: 08/15/2018
ms.author: danlep
ms.openlocfilehash: 9e8bd6819601cc4436e3432ee390f2ae82a0d94a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870814"
---
# <a name="create-an-azure-batch-pool-in-a-virtual-network"></a><span data-ttu-id="9e01d-103">Create an Azure Batch pool in a virtual network</span><span class="sxs-lookup"><span data-stu-id="9e01d-103">Create an Azure Batch pool in a virtual network</span></span>


<span data-ttu-id="9e01d-104">When you create an Azure Batch pool, you can provision the pool in a subnet of an [Azure virtual network](../virtual-network/virtual-networks-overview.md) (VNet) that you specify.</span><span class="sxs-lookup"><span data-stu-id="9e01d-104">When you create an Azure Batch pool, you can provision the pool in a subnet of an [Azure virtual network](../virtual-network/virtual-networks-overview.md) (VNet) that you specify.</span></span> <span data-ttu-id="9e01d-105">This article explains how to set up a Batch pool in a VNet.</span><span class="sxs-lookup"><span data-stu-id="9e01d-105">This article explains how to set up a Batch pool in a VNet.</span></span> 



## <a name="why-use-a-vnet"></a><span data-ttu-id="9e01d-106">Why use a VNet?</span><span class="sxs-lookup"><span data-stu-id="9e01d-106">Why use a VNet?</span></span>


<span data-ttu-id="9e01d-107">An Azure Batch pool has settings to allow compute nodes to communicate with each other - for example, to run multi-instance tasks.</span><span class="sxs-lookup"><span data-stu-id="9e01d-107">An Azure Batch pool has settings to allow compute nodes to communicate with each other - for example, to run multi-instance tasks.</span></span> <span data-ttu-id="9e01d-108">These settings do not require a separate VNet.</span><span class="sxs-lookup"><span data-stu-id="9e01d-108">These settings do not require a separate VNet.</span></span> <span data-ttu-id="9e01d-109">However, by default, the nodes cannot communicate with virtual machines that are not part of the Batch pool, such as a license server or a file server.</span><span class="sxs-lookup"><span data-stu-id="9e01d-109">However, by default, the nodes cannot communicate with virtual machines that are not part of the Batch pool, such as a license server or a file server.</span></span> <span data-ttu-id="9e01d-110">To allow pool compute nodes to communicate securely with other virtual machines, or with an on-premises network, you can provision the pool in a subnet of an Azure VNet.</span><span class="sxs-lookup"><span data-stu-id="9e01d-110">To allow pool compute nodes to communicate securely with other virtual machines, or with an on-premises network, you can provision the pool in a subnet of an Azure VNet.</span></span> 



## <a name="prerequisites"></a><span data-ttu-id="9e01d-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9e01d-111">Prerequisites</span></span>

* <span data-ttu-id="9e01d-112">**Authentication**.</span><span class="sxs-lookup"><span data-stu-id="9e01d-112">**Authentication**.</span></span> <span data-ttu-id="9e01d-113">To use an Azure VNet, the Batch client API must use Azure Active Directory (AD) authentication.</span><span class="sxs-lookup"><span data-stu-id="9e01d-113">To use an Azure VNet, the Batch client API must use Azure Active Directory (AD) authentication.</span></span> <span data-ttu-id="9e01d-114">Azure Batch support for Azure AD is documented in [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="9e01d-114">Azure Batch support for Azure AD is documented in [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 

* <span data-ttu-id="9e01d-115">**An Azure VNet**.</span><span class="sxs-lookup"><span data-stu-id="9e01d-115">**An Azure VNet**.</span></span> <span data-ttu-id="9e01d-116">To prepare a VNet with one or more subnets in advance, you can use the Azure portal, Azure PowerShell, the Azure Command-Line Interface (CLI), or other methods.</span><span class="sxs-lookup"><span data-stu-id="9e01d-116">To prepare a VNet with one or more subnets in advance, you can use the Azure portal, Azure PowerShell, the Azure Command-Line Interface (CLI), or other methods.</span></span> <span data-ttu-id="9e01d-117">To create an Azure Resource Manager-based VNet, see [Create a virtual network](../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="9e01d-117">To create an Azure Resource Manager-based VNet, see [Create a virtual network](../virtual-network/manage-virtual-network.md#create-a-virtual-network).</span></span> <span data-ttu-id="9e01d-118">To create a classic VNet, see [Create a virtual network (classic) with multiple subnets](../virtual-network/create-virtual-network-classic.md).</span><span class="sxs-lookup"><span data-stu-id="9e01d-118">To create a classic VNet, see [Create a virtual network (classic) with multiple subnets](../virtual-network/create-virtual-network-classic.md).</span></span>

### <a name="vnet-requirements"></a><span data-ttu-id="9e01d-119">VNet requirements</span><span class="sxs-lookup"><span data-stu-id="9e01d-119">VNet requirements</span></span>
[!INCLUDE [batch-virtual-network-ports](../../includes/batch-virtual-network-ports.md)]
    
## <a name="create-a-pool-with-a-vnet-in-the-portal"></a><span data-ttu-id="9e01d-120">Create a pool with a VNet in the portal</span><span class="sxs-lookup"><span data-stu-id="9e01d-120">Create a pool with a VNet in the portal</span></span>

<span data-ttu-id="9e01d-121">Once you have created your VNet and assigned a subnet to it, you can create a Batch pool with that VNet.</span><span class="sxs-lookup"><span data-stu-id="9e01d-121">Once you have created your VNet and assigned a subnet to it, you can create a Batch pool with that VNet.</span></span> <span data-ttu-id="9e01d-122">Follow these steps to create a pool from the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="9e01d-122">Follow these steps to create a pool from the Azure portal:</span></span> 



1. <span data-ttu-id="9e01d-123">Navigate to your Batch account in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="9e01d-123">Navigate to your Batch account in the Azure portal.</span></span> <span data-ttu-id="9e01d-124">This account must be in the same subscription and region as the resource group containing the VNet you intend to use.</span><span class="sxs-lookup"><span data-stu-id="9e01d-124">This account must be in the same subscription and region as the resource group containing the VNet you intend to use.</span></span> 
2. <span data-ttu-id="9e01d-125">In the **Settings** window on the left, select the **Pools** menu item.</span><span class="sxs-lookup"><span data-stu-id="9e01d-125">In the **Settings** window on the left, select the **Pools** menu item.</span></span>
3. <span data-ttu-id="9e01d-126">In the **Pools** window, select the **Add** command.</span><span class="sxs-lookup"><span data-stu-id="9e01d-126">In the **Pools** window, select the **Add** command.</span></span>
4. <span data-ttu-id="9e01d-127">On the **Add Pool** window, select the option you intend to use from the **Image Type** dropdown.</span><span class="sxs-lookup"><span data-stu-id="9e01d-127">On the **Add Pool** window, select the option you intend to use from the **Image Type** dropdown.</span></span> 
5. <span data-ttu-id="9e01d-128">Select the correct **Publisher/Offer/Sku** for your custom image.</span><span class="sxs-lookup"><span data-stu-id="9e01d-128">Select the correct **Publisher/Offer/Sku** for your custom image.</span></span>
6. <span data-ttu-id="9e01d-129">Specify the remaining required settings, including the **Node size**, **Target dedicated nodes**, and **Low priority nodes**, as well as any desired optional settings.</span><span class="sxs-lookup"><span data-stu-id="9e01d-129">Specify the remaining required settings, including the **Node size**, **Target dedicated nodes**, and **Low priority nodes**, as well as any desired optional settings.</span></span>
7. <span data-ttu-id="9e01d-130">In **Virtual Network**, select the virtual network and subnet you wish to use.</span><span class="sxs-lookup"><span data-stu-id="9e01d-130">In **Virtual Network**, select the virtual network and subnet you wish to use.</span></span>
  
  ![Add pool with virtual network](./media/batch-virtual-network/add-vnet-pool.png)

## <a name="user-defined-routes-for-forced-tunneling"></a><span data-ttu-id="9e01d-132">User-defined routes for forced tunneling</span><span class="sxs-lookup"><span data-stu-id="9e01d-132">User-defined routes for forced tunneling</span></span>

<span data-ttu-id="9e01d-133">You might have requirements in your organization to redirect (force) Internet-bound traffic from the subnet back to your on-premises location for inspection and logging.</span><span class="sxs-lookup"><span data-stu-id="9e01d-133">You might have requirements in your organization to redirect (force) Internet-bound traffic from the subnet back to your on-premises location for inspection and logging.</span></span> <span data-ttu-id="9e01d-134">You may have enabled forced tunneling for the subnets in your VNet.</span><span class="sxs-lookup"><span data-stu-id="9e01d-134">You may have enabled forced tunneling for the subnets in your VNet.</span></span> 

<span data-ttu-id="9e01d-135">To ensure that your Azure Batch pool compute nodes work in a VNet that has forced tunneling enabled, you must add the following [user-defined routes](../virtual-network/virtual-networks-udr-overview.md) for that subnet:</span><span class="sxs-lookup"><span data-stu-id="9e01d-135">To ensure that your Azure Batch pool compute nodes work in a VNet that has forced tunneling enabled, you must add the following [user-defined routes](../virtual-network/virtual-networks-udr-overview.md) for that subnet:</span></span>

* <span data-ttu-id="9e01d-136">The Batch service needs to communicate with pool compute nodes for scheduling tasks.</span><span class="sxs-lookup"><span data-stu-id="9e01d-136">The Batch service needs to communicate with pool compute nodes for scheduling tasks.</span></span> <span data-ttu-id="9e01d-137">To enable this communication, add a user-defined route for each IP address used by the Batch service in the region where your Batch account exists.</span><span class="sxs-lookup"><span data-stu-id="9e01d-137">To enable this communication, add a user-defined route for each IP address used by the Batch service in the region where your Batch account exists.</span></span> <span data-ttu-id="9e01d-138">To obtain the list of IP addresses of the Batch service, please contact Azure Support.</span><span class="sxs-lookup"><span data-stu-id="9e01d-138">To obtain the list of IP addresses of the Batch service, please contact Azure Support.</span></span>

* <span data-ttu-id="9e01d-139">Ensure that outbound traffic to Azure Storage (specifically, URLs of the form `<account>.table.core.windows.net`, `<account>.queue.core.windows.net`, and `<account>.blob.core.windows.net`) is not blocked via your on-premises network appliance.</span><span class="sxs-lookup"><span data-stu-id="9e01d-139">Ensure that outbound traffic to Azure Storage (specifically, URLs of the form `<account>.table.core.windows.net`, `<account>.queue.core.windows.net`, and `<account>.blob.core.windows.net`) is not blocked via your on-premises network appliance.</span></span>

<span data-ttu-id="9e01d-140">When you add a user-defined route, define the route for each related Batch IP address prefix, and set **Next hop type** to **Internet**.</span><span class="sxs-lookup"><span data-stu-id="9e01d-140">When you add a user-defined route, define the route for each related Batch IP address prefix, and set **Next hop type** to **Internet**.</span></span> <span data-ttu-id="9e01d-141">See the following example:</span><span class="sxs-lookup"><span data-stu-id="9e01d-141">See the following example:</span></span>

![User-defined route](./media/batch-virtual-network/user-defined-route.png)

## <a name="next-steps"></a><span data-ttu-id="9e01d-143">Next steps</span><span class="sxs-lookup"><span data-stu-id="9e01d-143">Next steps</span></span>

- <span data-ttu-id="9e01d-144">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="9e01d-144">For an in-depth overview of Batch, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md).</span></span>
- <span data-ttu-id="9e01d-145">For more about creating a user-defined route, see [Create a user-defined route - Azure portal](../virtual-network/tutorial-create-route-table-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9e01d-145">For more about creating a user-defined route, see [Create a user-defined route - Azure portal](../virtual-network/tutorial-create-route-table-portal.md).</span></span>
