---
title: Manage DNS zones in Azure DNS - Azure portal | Microsoft Docs
description: You can manage DNS zones using the Azure portal. This article describes how to update, delete and create DNS zones on Azure DNS
services: dns
documentationcenter: na
author: vhorne
manager: timlt
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/18/2017
ms.author: victorh
ms.openlocfilehash: ca9d03cb14e79b23ccc2021e0a31650eb9bbd95b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866222"
---
# <a name="how-to-manage-dns-zones-in-the-azure-portal"></a><span data-ttu-id="6694d-104">How to manage DNS Zones in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6694d-104">How to manage DNS Zones in the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [Portal](dns-operations-dnszones-portal.md)
> * [PowerShell](dns-operations-dnszones.md)
> * [Azure CLI 1.0](dns-operations-dnszones-cli-nodejs.md)
> * [Azure CLI 2.0](dns-operations-dnszones-cli.md)

<span data-ttu-id="6694d-109">This article shows you how to manage your DNS zones by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6694d-109">This article shows you how to manage your DNS zones by using the Azure portal.</span></span> <span data-ttu-id="6694d-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span><span class="sxs-lookup"><span data-stu-id="6694d-110">You can also manage your DNS zones using the cross-platform [Azure CLI](dns-operations-dnszones-cli.md) or the Azure [PowerShell](dns-operations-dnszones.md).</span></span>

## <a name="create-a-dns-zone"></a><span data-ttu-id="6694d-111">Create a DNS zone</span><span class="sxs-lookup"><span data-stu-id="6694d-111">Create a DNS zone</span></span>

1. <span data-ttu-id="6694d-112">Sign in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6694d-112">Sign in to the Azure portal</span></span>
2. <span data-ttu-id="6694d-113">On the Hub menu, click and click **Create a resource > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span><span class="sxs-lookup"><span data-stu-id="6694d-113">On the Hub menu, click and click **Create a resource > Networking >** and then click **DNS zone** to open the Create DNS zone blade.</span></span>

    ![DNS zone](./media/dns-operations-dnszones-portal/openzone650.png)

4. <span data-ttu-id="6694d-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span><span class="sxs-lookup"><span data-stu-id="6694d-115">On the **Create DNS zone** blade enter the following values, then click **Create**:</span></span>


   | <span data-ttu-id="6694d-116">**Setting**</span><span class="sxs-lookup"><span data-stu-id="6694d-116">**Setting**</span></span> | <span data-ttu-id="6694d-117">**Value**</span><span class="sxs-lookup"><span data-stu-id="6694d-117">**Value**</span></span> | <span data-ttu-id="6694d-118">**Details**</span><span class="sxs-lookup"><span data-stu-id="6694d-118">**Details**</span></span> |
   |---|---|---|
   |<span data-ttu-id="6694d-119">**Name**</span><span class="sxs-lookup"><span data-stu-id="6694d-119">**Name**</span></span>|<span data-ttu-id="6694d-120">contoso.com</span><span class="sxs-lookup"><span data-stu-id="6694d-120">contoso.com</span></span>|<span data-ttu-id="6694d-121">The name of the DNS zone</span><span class="sxs-lookup"><span data-stu-id="6694d-121">The name of the DNS zone</span></span>|
   |<span data-ttu-id="6694d-122">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="6694d-122">**Subscription**</span></span>|<span data-ttu-id="6694d-123">[Your subscription]</span><span class="sxs-lookup"><span data-stu-id="6694d-123">[Your subscription]</span></span>|<span data-ttu-id="6694d-124">Select a subscription to create the DNS zone in.</span><span class="sxs-lookup"><span data-stu-id="6694d-124">Select a subscription to create the DNS zone in.</span></span>|
   |<span data-ttu-id="6694d-125">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="6694d-125">**Resource group**</span></span>|<span data-ttu-id="6694d-126">**Create new:** contosoDNSRG</span><span class="sxs-lookup"><span data-stu-id="6694d-126">**Create new:** contosoDNSRG</span></span>|<span data-ttu-id="6694d-127">Create a resource group.</span><span class="sxs-lookup"><span data-stu-id="6694d-127">Create a resource group.</span></span> <span data-ttu-id="6694d-128">The resource group name must be unique within the subscription you selected.</span><span class="sxs-lookup"><span data-stu-id="6694d-128">The resource group name must be unique within the subscription you selected.</span></span> <span data-ttu-id="6694d-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span><span class="sxs-lookup"><span data-stu-id="6694d-129">To learn more about resource groups, read the [Resource Manager](../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fdns%2ftoc.json#resource-groups) overview article.</span></span>|
   |<span data-ttu-id="6694d-130">**Location**</span><span class="sxs-lookup"><span data-stu-id="6694d-130">**Location**</span></span>|<span data-ttu-id="6694d-131">West US</span><span class="sxs-lookup"><span data-stu-id="6694d-131">West US</span></span>||

> [!NOTE]
> The resource group refers to the location of the resource group, and has no impact on the DNS zone. The DNS zone location is always "global", and is not shown.

## <a name="list-dns-zones"></a><span data-ttu-id="6694d-134">List DNS zones</span><span class="sxs-lookup"><span data-stu-id="6694d-134">List DNS zones</span></span>

<span data-ttu-id="6694d-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span><span class="sxs-lookup"><span data-stu-id="6694d-135">In the Azure portal, navigate to **More services** > **Networking** > **DNS zones**.</span></span> <span data-ttu-id="6694d-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span><span class="sxs-lookup"><span data-stu-id="6694d-136">Each DNS zone is it's own resource, information such as number of record-sets and name servers are viewable from this view.</span></span> <span data-ttu-id="6694d-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span><span class="sxs-lookup"><span data-stu-id="6694d-137">The column **NAME SERVERS** is not in the default view, to add it click **Columns**, select **Name servers** and click **Done**.</span></span>

![listing DNS zones](./media/dns-operations-dnszones-portal/listzones.png)

## <a name="delete-a-dns-zone"></a><span data-ttu-id="6694d-139">Delete a DNS zone</span><span class="sxs-lookup"><span data-stu-id="6694d-139">Delete a DNS zone</span></span>

<span data-ttu-id="6694d-140">Navigate to a DNS zone in the portal.</span><span class="sxs-lookup"><span data-stu-id="6694d-140">Navigate to a DNS zone in the portal.</span></span> <span data-ttu-id="6694d-141">On the **DNS zone** blade, click **Delete zone**.</span><span class="sxs-lookup"><span data-stu-id="6694d-141">On the **DNS zone** blade, click **Delete zone**.</span></span> <span data-ttu-id="6694d-142">You are prompted to confirm you are wanting to delete the DNS zone.</span><span class="sxs-lookup"><span data-stu-id="6694d-142">You are prompted to confirm you are wanting to delete the DNS zone.</span></span> <span data-ttu-id="6694d-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span><span class="sxs-lookup"><span data-stu-id="6694d-143">Deleting a DNS zone also deletes all the records that are contained in the zone.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6694d-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="6694d-144">Next steps</span></span>

<span data-ttu-id="6694d-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6694d-145">Learn how to work with your DNS Zone and records by visiting [Get started with Azure DNS using the Azure portal](dns-getstarted-portal.md).</span></span>