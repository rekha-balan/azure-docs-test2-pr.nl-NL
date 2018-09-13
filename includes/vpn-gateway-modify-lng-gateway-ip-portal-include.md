---
title: include file
description: include file
services: vpn-gateway
author: cherylmc
ms.service: vpn-gateway
ms.topic: include
ms.date: 03/21/2018
ms.author: cherylmc
ms.custom: include file
ms.openlocfilehash: a79184a5e08aa43a4675194adf5f10b9807418db
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868201"
---
### <a name="gwipnoconnection"></a> <span data-ttu-id="37f08-103">To modify the local network gateway IP address - no gateway connection</span><span class="sxs-lookup"><span data-stu-id="37f08-103">To modify the local network gateway IP address - no gateway connection</span></span>

<span data-ttu-id="37f08-104">Use the example to modify a local network gateway that does not have a gateway connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-104">Use the example to modify a local network gateway that does not have a gateway connection.</span></span> <span data-ttu-id="37f08-105">When modifying this value, you can also modify the address prefixes at the same time.</span><span class="sxs-lookup"><span data-stu-id="37f08-105">When modifying this value, you can also modify the address prefixes at the same time.</span></span>

1. <span data-ttu-id="37f08-106">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="37f08-106">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="37f08-107">In the **IP address** box, modify the IP address.</span><span class="sxs-lookup"><span data-stu-id="37f08-107">In the **IP address** box, modify the IP address.</span></span>
3. <span data-ttu-id="37f08-108">Click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="37f08-108">Click **Save** to save the settings.</span></span>

### <a name="gwipwithconnection"></a><span data-ttu-id="37f08-109">To modify the local network gateway IP address - existing gateway connection</span><span class="sxs-lookup"><span data-stu-id="37f08-109">To modify the local network gateway IP address - existing gateway connection</span></span>

<span data-ttu-id="37f08-110">To modify a local network gateway that has a connection, you need to first remove the connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-110">To modify a local network gateway that has a connection, you need to first remove the connection.</span></span> <span data-ttu-id="37f08-111">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-111">After the connection is removed, you can modify the gateway IP address and recreate a new connection.</span></span> <span data-ttu-id="37f08-112">You can also modify the address prefixes at the same time.</span><span class="sxs-lookup"><span data-stu-id="37f08-112">You can also modify the address prefixes at the same time.</span></span> <span data-ttu-id="37f08-113">This results in some downtime for your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-113">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="37f08-114">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="37f08-114">When modifying the gateway IP address, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="37f08-115">You only need to remove the connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-115">You only need to remove the connection.</span></span>
 
#### <a name="1-remove-the-connection"></a><span data-ttu-id="37f08-116">1. Remove the connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-116">1. Remove the connection.</span></span>

1. <span data-ttu-id="37f08-117">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="37f08-117">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="37f08-118">Click the **...** on the line for the connection, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="37f08-118">Click the **...** on the line for the connection, then click **Delete**.</span></span>
3. <span data-ttu-id="37f08-119">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="37f08-119">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-ip-address"></a><span data-ttu-id="37f08-120">2. Modify the IP address.</span><span class="sxs-lookup"><span data-stu-id="37f08-120">2. Modify the IP address.</span></span>

<span data-ttu-id="37f08-121">You can also modify the address prefixes at the same time.</span><span class="sxs-lookup"><span data-stu-id="37f08-121">You can also modify the address prefixes at the same time.</span></span>

1. <span data-ttu-id="37f08-122">In the **IP address** box, modify the IP address.</span><span class="sxs-lookup"><span data-stu-id="37f08-122">In the **IP address** box, modify the IP address.</span></span>
2. <span data-ttu-id="37f08-123">Click **Save** to save the settings.</span><span class="sxs-lookup"><span data-stu-id="37f08-123">Click **Save** to save the settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="37f08-124">3. Recreate the connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-124">3. Recreate the connection.</span></span>

1. <span data-ttu-id="37f08-125">Navigate to the Virtual Network Gateway for your VNet.</span><span class="sxs-lookup"><span data-stu-id="37f08-125">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="37f08-126">(Not the Local Network Gateway.)</span><span class="sxs-lookup"><span data-stu-id="37f08-126">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="37f08-127">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="37f08-127">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="37f08-128">Click the **+ Add** to open the **Add connection** blade.</span><span class="sxs-lookup"><span data-stu-id="37f08-128">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="37f08-129">Recreate your connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-129">Recreate your connection.</span></span>
5. <span data-ttu-id="37f08-130">Click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="37f08-130">Click **OK** to create the connection.</span></span>