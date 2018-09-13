---
title: Disable, enable, or delete a Traffic Manager profile | Microsoft Docs
description: This article will help you work with your Traffic Manager profiles.
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: f19143e2-2f4f-4ead-bb00-89b95ac92cb4
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/18/2016
ms.author: kumud
ms.openlocfilehash: ec2374347fdb93174f30d7bf4c57869d9d66004f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540826"
---
<!-- repub for nofollow -->

# <a name="disable-enable-or-delete-a-profile"></a><span data-ttu-id="ba529-103">Disable, Enable, or Delete a Profile</span><span class="sxs-lookup"><span data-stu-id="ba529-103">Disable, Enable, or Delete a Profile</span></span>
<span data-ttu-id="ba529-104">You can disable an existing Traffic Manager profile so that it will not refer user requests to its configured endpoints.</span><span class="sxs-lookup"><span data-stu-id="ba529-104">You can disable an existing Traffic Manager profile so that it will not refer user requests to its configured endpoints.</span></span> <span data-ttu-id="ba529-105">When you disable a Traffic Manager profile, the profile itself and the information contained in the profile will remain intact and can be edited in the Traffic Manager interface.</span><span class="sxs-lookup"><span data-stu-id="ba529-105">When you disable a Traffic Manager profile, the profile itself and the information contained in the profile will remain intact and can be edited in the Traffic Manager interface.</span></span> <span data-ttu-id="ba529-106">When you want to re-enable the profile, you can easily do so in the Azure portal and referrals will resume.</span><span class="sxs-lookup"><span data-stu-id="ba529-106">When you want to re-enable the profile, you can easily do so in the Azure portal and referrals will resume.</span></span> <span data-ttu-id="ba529-107">When you create a Traffic Manager profile in the Azure portal, it’s automatically enabled.</span><span class="sxs-lookup"><span data-stu-id="ba529-107">When you create a Traffic Manager profile in the Azure portal, it’s automatically enabled.</span></span>

## <a name="to-disable-a-profile"></a><span data-ttu-id="ba529-108">To disable a profile</span><span class="sxs-lookup"><span data-stu-id="ba529-108">To disable a profile</span></span>
1. <span data-ttu-id="ba529-109">Modify the DNS resource record on your Internet DNS server to use the appropriate record type and pointer to either another name or the IP address of a specific location on the Internet.</span><span class="sxs-lookup"><span data-stu-id="ba529-109">Modify the DNS resource record on your Internet DNS server to use the appropriate record type and pointer to either another name or the IP address of a specific location on the Internet.</span></span> <span data-ttu-id="ba529-110">In other words, change the DNS resource record on your Internet DNS server so that it no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-110">In other words, change the DNS resource record on your Internet DNS server so that it no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="ba529-111">Traffic will stop being directed to the endpoints through the Traffic Manager profile settings.</span><span class="sxs-lookup"><span data-stu-id="ba529-111">Traffic will stop being directed to the endpoints through the Traffic Manager profile settings.</span></span>
3. <span data-ttu-id="ba529-112">Select the profile that you want to disable.</span><span class="sxs-lookup"><span data-stu-id="ba529-112">Select the profile that you want to disable.</span></span> <span data-ttu-id="ba529-113">To select the profile, on the Traffic Manager page, highlight the profile by clicking the column next to the profile name.</span><span class="sxs-lookup"><span data-stu-id="ba529-113">To select the profile, on the Traffic Manager page, highlight the profile by clicking the column next to the profile name.</span></span> <span data-ttu-id="ba529-114">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-114">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span></span>
4. <span data-ttu-id="ba529-115">After selecting the profile, click Disable at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ba529-115">After selecting the profile, click Disable at the bottom of the page.</span></span>

## <a name="to-enable-a-profile"></a><span data-ttu-id="ba529-116">To enable a profile</span><span class="sxs-lookup"><span data-stu-id="ba529-116">To enable a profile</span></span>
1. <span data-ttu-id="ba529-117">Select the profile that you want to enable.</span><span class="sxs-lookup"><span data-stu-id="ba529-117">Select the profile that you want to enable.</span></span> <span data-ttu-id="ba529-118">To select the profile, on the Traffic Manager page, highlight the profile by clicking the column next to the profile name.</span><span class="sxs-lookup"><span data-stu-id="ba529-118">To select the profile, on the Traffic Manager page, highlight the profile by clicking the column next to the profile name.</span></span> <span data-ttu-id="ba529-119">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-119">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span></span>
2. <span data-ttu-id="ba529-120">After selecting the profile, click Enable at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ba529-120">After selecting the profile, click Enable at the bottom of the page.</span></span>
3. <span data-ttu-id="ba529-121">Modify the DNS resource record on your Internet DNS server to use the CNAME record type, which maps your company domain name to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-121">Modify the DNS resource record on your Internet DNS server to use the CNAME record type, which maps your company domain name to the domain name of your Traffic Manager profile.</span></span> <span data-ttu-id="ba529-122">For more information, see [Point a Company Internet Domain to a Traffic Manager Domain](traffic-manager-point-internet-domain.md).</span><span class="sxs-lookup"><span data-stu-id="ba529-122">For more information, see [Point a Company Internet Domain to a Traffic Manager Domain](traffic-manager-point-internet-domain.md).</span></span>
4. <span data-ttu-id="ba529-123">Traffic will start being directed to the endpoints again.</span><span class="sxs-lookup"><span data-stu-id="ba529-123">Traffic will start being directed to the endpoints again.</span></span>

## <a name="delete-a-profile"></a><span data-ttu-id="ba529-124">Delete a profile</span><span class="sxs-lookup"><span data-stu-id="ba529-124">Delete a profile</span></span>
1. <span data-ttu-id="ba529-125">Ensure that the DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-125">Ensure that the DNS resource record on your Internet DNS server no longer uses a CNAME resource record that points to the domain name of your Traffic Manager profile.</span></span>
2. <span data-ttu-id="ba529-126">Select the profile that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="ba529-126">Select the profile that you want to delete.</span></span> <span data-ttu-id="ba529-127">To select the profile, on the Traffic Manager page, highlight the profile by</span><span class="sxs-lookup"><span data-stu-id="ba529-127">To select the profile, on the Traffic Manager page, highlight the profile by</span></span>
3. <span data-ttu-id="ba529-128">clicking the column next to the profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-128">clicking the column next to the profile.</span></span> <span data-ttu-id="ba529-129">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span><span class="sxs-lookup"><span data-stu-id="ba529-129">Do not click the name of the profile or the arrow next to the name, as this will take you to the settings page for the profile.</span></span>
4. <span data-ttu-id="ba529-130">After selecting the profile, click Delete at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="ba529-130">After selecting the profile, click Delete at the bottom of the page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba529-131">Next Steps</span><span class="sxs-lookup"><span data-stu-id="ba529-131">Next Steps</span></span>
[<span data-ttu-id="ba529-132">Traffic Manager - Disable or enable an endpoint</span><span class="sxs-lookup"><span data-stu-id="ba529-132">Traffic Manager - Disable or enable an endpoint</span></span>](disable-or-enable-an-endpoint.md)

[<span data-ttu-id="ba529-133">Configure failover routing method</span><span class="sxs-lookup"><span data-stu-id="ba529-133">Configure failover routing method</span></span>](traffic-manager-configure-failover-routing-method.md)

[<span data-ttu-id="ba529-134">Configure round robin routing method</span><span class="sxs-lookup"><span data-stu-id="ba529-134">Configure round robin routing method</span></span>](traffic-manager-configure-round-robin-routing-method.md)

[<span data-ttu-id="ba529-135">Configure performance routing method</span><span class="sxs-lookup"><span data-stu-id="ba529-135">Configure performance routing method</span></span>](traffic-manager-configure-performance-routing-method.md)

[<span data-ttu-id="ba529-136">Troubleshooting Traffic Manager degraded state</span><span class="sxs-lookup"><span data-stu-id="ba529-136">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)

