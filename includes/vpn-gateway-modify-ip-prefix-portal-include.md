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
ms.openlocfilehash: 3b8049515f753cbcf8ca068c1790f716f02d30b6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969410"
---
### <a name="noconnection"></a><span data-ttu-id="b8423-103">To modify local network gateway IP address prefixes - no gateway connection</span><span class="sxs-lookup"><span data-stu-id="b8423-103">To modify local network gateway IP address prefixes - no gateway connection</span></span>

#### <a name="to-add-additional-address-prefixes"></a><span data-ttu-id="b8423-104">To add additional address prefixes:</span><span class="sxs-lookup"><span data-stu-id="b8423-104">To add additional address prefixes:</span></span>

1. <span data-ttu-id="b8423-105">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b8423-105">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="b8423-106">Add the IP address space in the *Add additional address range* box.</span><span class="sxs-lookup"><span data-stu-id="b8423-106">Add the IP address space in the *Add additional address range* box.</span></span>
3. <span data-ttu-id="b8423-107">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="b8423-107">Click **Save** to save your settings.</span></span>

#### <a name="to-remove-address-prefixes"></a><span data-ttu-id="b8423-108">To remove address prefixes:</span><span class="sxs-lookup"><span data-stu-id="b8423-108">To remove address prefixes:</span></span>

1. <span data-ttu-id="b8423-109">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b8423-109">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="b8423-110">Click the **'...'** on the line containing the prefix you want to remove.</span><span class="sxs-lookup"><span data-stu-id="b8423-110">Click the **'...'** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="b8423-111">Click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="b8423-111">Click **Remove**.</span></span>
4. <span data-ttu-id="b8423-112">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="b8423-112">Click **Save** to save your settings.</span></span>

### <a name="withconnection"></a><span data-ttu-id="b8423-113">To modify local network gateway IP address prefixes - existing gateway connection</span><span class="sxs-lookup"><span data-stu-id="b8423-113">To modify local network gateway IP address prefixes - existing gateway connection</span></span>

<span data-ttu-id="b8423-114">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span><span class="sxs-lookup"><span data-stu-id="b8423-114">If you have a gateway connection and want to add or remove the IP address prefixes contained in your local network gateway, you need to do the following steps, in order.</span></span> <span data-ttu-id="b8423-115">This results in some downtime for your VPN connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-115">This results in some downtime for your VPN connection.</span></span> <span data-ttu-id="b8423-116">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span><span class="sxs-lookup"><span data-stu-id="b8423-116">When modifying IP address prefixes, you don't need to delete the VPN gateway.</span></span> <span data-ttu-id="b8423-117">You only need to remove the connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-117">You only need to remove the connection.</span></span>

#### <a name="1-remove-the-connection"></a><span data-ttu-id="b8423-118">1. Remove the connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-118">1. Remove the connection.</span></span>

1. <span data-ttu-id="b8423-119">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="b8423-119">On the Local Network Gateway resource, in the **Settings** section, click **Connections**.</span></span>
2. <span data-ttu-id="b8423-120">Click the **...** on the line for each connection, then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b8423-120">Click the **...** on the line for each connection, then click **Delete**.</span></span>
3. <span data-ttu-id="b8423-121">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="b8423-121">Click **Save** to save your settings.</span></span>

#### <a name="2-modify-the-address-prefixes"></a><span data-ttu-id="b8423-122">2. Modify the address prefixes.</span><span class="sxs-lookup"><span data-stu-id="b8423-122">2. Modify the address prefixes.</span></span>

<span data-ttu-id="b8423-123">To add additional address prefixes:</span><span class="sxs-lookup"><span data-stu-id="b8423-123">To add additional address prefixes:</span></span>

1. <span data-ttu-id="b8423-124">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b8423-124">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="b8423-125">Add the IP address space.</span><span class="sxs-lookup"><span data-stu-id="b8423-125">Add the IP address space.</span></span>
3. <span data-ttu-id="b8423-126">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="b8423-126">Click **Save** to save your settings.</span></span>

<span data-ttu-id="b8423-127">To remove address prefixes:</span><span class="sxs-lookup"><span data-stu-id="b8423-127">To remove address prefixes:</span></span>

1. <span data-ttu-id="b8423-128">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span><span class="sxs-lookup"><span data-stu-id="b8423-128">On the Local Network Gateway resource, in the **Settings** section, click **Configuration**.</span></span>
2. <span data-ttu-id="b8423-129">Click the **...** on the line containing the prefix you want to remove.</span><span class="sxs-lookup"><span data-stu-id="b8423-129">Click the **...** on the line containing the prefix you want to remove.</span></span>
3. <span data-ttu-id="b8423-130">Click **Remove**.</span><span class="sxs-lookup"><span data-stu-id="b8423-130">Click **Remove**.</span></span>
4. <span data-ttu-id="b8423-131">Click **Save** to save your settings.</span><span class="sxs-lookup"><span data-stu-id="b8423-131">Click **Save** to save your settings.</span></span>

#### <a name="3-recreate-the-connection"></a><span data-ttu-id="b8423-132">3. Recreate the connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-132">3. Recreate the connection.</span></span>

1. <span data-ttu-id="b8423-133">Navigate to the Virtual Network Gateway for your VNet.</span><span class="sxs-lookup"><span data-stu-id="b8423-133">Navigate to the Virtual Network Gateway for your VNet.</span></span> <span data-ttu-id="b8423-134">(Not the Local Network Gateway.)</span><span class="sxs-lookup"><span data-stu-id="b8423-134">(Not the Local Network Gateway.)</span></span>
2. <span data-ttu-id="b8423-135">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span><span class="sxs-lookup"><span data-stu-id="b8423-135">On the Virtual Network Gateway, in the **Settings** section, click **Connections**.</span></span>
3. <span data-ttu-id="b8423-136">Click the **+ Add** to open the **Add connection** blade.</span><span class="sxs-lookup"><span data-stu-id="b8423-136">Click the **+ Add** to open the **Add connection** blade.</span></span>
4. <span data-ttu-id="b8423-137">Recreate your connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-137">Recreate your connection.</span></span>
5. <span data-ttu-id="b8423-138">Click **OK** to create the connection.</span><span class="sxs-lookup"><span data-stu-id="b8423-138">Click **OK** to create the connection.</span></span>