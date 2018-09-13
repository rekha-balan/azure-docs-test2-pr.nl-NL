---
title: Disable or Enable a Traffic Manager endpoint | Microsoft Docs
description: This article will help disable or enable your Traffic Manager profile endpoints.
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 9b2264ce-be06-43b2-a00b-5c724e5d71fd
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: kumud
ms.openlocfilehash: b09ef7842d628c68439fbb9215c97429b4956f71
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551284"
---
<!-- repub for nofollow -->

# <a name="disable-or-enable-a-traffic-manager-endpoint"></a><span data-ttu-id="19b31-103">Disable or Enable a Traffic Manager Endpoint</span><span class="sxs-lookup"><span data-stu-id="19b31-103">Disable or Enable a Traffic Manager Endpoint</span></span>
<span data-ttu-id="19b31-104">You can also disable individual endpoints that are part of a Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="19b31-104">You can also disable individual endpoints that are part of a Traffic Manager profile.</span></span> <span data-ttu-id="19b31-105">Endpoints include both cloud services and websites.</span><span class="sxs-lookup"><span data-stu-id="19b31-105">Endpoints include both cloud services and websites.</span></span> <span data-ttu-id="19b31-106">Disabling an endpoint leaves it as part of the profile, but the profile acts as if the endpoint is not included in it.</span><span class="sxs-lookup"><span data-stu-id="19b31-106">Disabling an endpoint leaves it as part of the profile, but the profile acts as if the endpoint is not included in it.</span></span> <span data-ttu-id="19b31-107">This action is very useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span><span class="sxs-lookup"><span data-stu-id="19b31-107">This action is very useful for temporarily removing an endpoint that is in maintenance mode or being redeployed.</span></span> <span data-ttu-id="19b31-108">Once the endpoint is up and running again, it can be enabled</span><span class="sxs-lookup"><span data-stu-id="19b31-108">Once the endpoint is up and running again, it can be enabled</span></span>

> [!NOTE]
> <span data-ttu-id="19b31-109">**Disabling an endpoint has nothing to do with its deployment state in Azure. A healthy endpoint will remain up and able to receive traffic even when disabled in Traffic Manager. Additionally, disabling an endpoint in one profile does not affect its status in another profile.**</span><span class="sxs-lookup"><span data-stu-id="19b31-109">**Disabling an endpoint has nothing to do with its deployment state in Azure. A healthy endpoint will remain up and able to receive traffic even when disabled in Traffic Manager. Additionally, disabling an endpoint in one profile does not affect its status in another profile.**</span></span>
> 
> 

## <a name="to-disable-an-endpoint"></a><span data-ttu-id="19b31-110">To disable an endpoint</span><span class="sxs-lookup"><span data-stu-id="19b31-110">To disable an endpoint</span></span>
1. <span data-ttu-id="19b31-111">On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name.</span><span class="sxs-lookup"><span data-stu-id="19b31-111">On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name.</span></span> <span data-ttu-id="19b31-112">This will open the settings page for the profile.</span><span class="sxs-lookup"><span data-stu-id="19b31-112">This will open the settings page for the profile.</span></span>
2. <span data-ttu-id="19b31-113">At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.</span><span class="sxs-lookup"><span data-stu-id="19b31-113">At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.</span></span>
3. <span data-ttu-id="19b31-114">Click the endpoint that you want to disable, and then click **Disable** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19b31-114">Click the endpoint that you want to disable, and then click **Disable** at the bottom of the page.</span></span>
4. <span data-ttu-id="19b31-115">Traffic will stop flowing to the endpoint based on the DNS Time-to-Live (TTL) configured for the Traffic Manager domain name.</span><span class="sxs-lookup"><span data-stu-id="19b31-115">Traffic will stop flowing to the endpoint based on the DNS Time-to-Live (TTL) configured for the Traffic Manager domain name.</span></span> <span data-ttu-id="19b31-116">You can change the TTL from the Configuration page of the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="19b31-116">You can change the TTL from the Configuration page of the Traffic Manager profile.</span></span>

## <a name="to-enable-an-endpoint"></a><span data-ttu-id="19b31-117">To enable an endpoint</span><span class="sxs-lookup"><span data-stu-id="19b31-117">To enable an endpoint</span></span>
1. <span data-ttu-id="19b31-118">On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name.</span><span class="sxs-lookup"><span data-stu-id="19b31-118">On the Traffic Manager pane in the Azure classic portal, locate the Traffic Manager profile that contains the endpoint settings that you want to modify, and then click the arrow to the right of the profile name.</span></span> <span data-ttu-id="19b31-119">This will open the settings page for the profile.</span><span class="sxs-lookup"><span data-stu-id="19b31-119">This will open the settings page for the profile.</span></span>
2. <span data-ttu-id="19b31-120">At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.</span><span class="sxs-lookup"><span data-stu-id="19b31-120">At the top of the page, click **Endpoints** to view the endpoints that are included in your configuration.</span></span>
3. <span data-ttu-id="19b31-121">Click the endpoint that you want to enable, and then click **Enable** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="19b31-121">Click the endpoint that you want to enable, and then click **Enable** at the bottom of the page.</span></span>
4. <span data-ttu-id="19b31-122">Traffic will start flowing to the service again as dictated by the profile.</span><span class="sxs-lookup"><span data-stu-id="19b31-122">Traffic will start flowing to the service again as dictated by the profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="19b31-123">Next Steps</span><span class="sxs-lookup"><span data-stu-id="19b31-123">Next Steps</span></span>
[<span data-ttu-id="19b31-124">Traffic Manager - Disable, enable or delete a profile</span><span class="sxs-lookup"><span data-stu-id="19b31-124">Traffic Manager - Disable, enable or delete a profile</span></span>](disable-enable-or-delete-a-profile.md)

[<span data-ttu-id="19b31-125">Troubleshooting Traffic Manager degraded state</span><span class="sxs-lookup"><span data-stu-id="19b31-125">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)

[<span data-ttu-id="19b31-126">Traffic Manager performance considerations</span><span class="sxs-lookup"><span data-stu-id="19b31-126">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)

