---
title: Configure performance traffic routing method using Azure Traffic Manager | Microsoft Docs
description: This article explains how to configure Traffic Manager to route traffic to the endpoint with lowest latency
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: timlt
editor: ''
ms.assetid: 6dca6de1-18f7-4962-bd98-6055771fab22
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/20/2017
ms.author: kumud
ms.openlocfilehash: 705f9111a045646a188a4bb990d77cdddd98c59f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563276"
---
# <a name="configure-the-performance-traffic-routing-method"></a><span data-ttu-id="4bcb6-103">Configure the performance traffic routing method</span><span class="sxs-lookup"><span data-stu-id="4bcb6-103">Configure the performance traffic routing method</span></span>

<span data-ttu-id="4bcb6-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-104">The Performance traffic routing method allows you to direct traffic to the endpoint with the lowest latency from the client's network.</span></span> <span data-ttu-id="4bcb6-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-105">Typically, the datacenter with the lowest latency is the closest in geographic distance.</span></span> <span data-ttu-id="4bcb6-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-106">This traffic routing method cannot account for real-time changes in network configuration or load.</span></span>

##  <a name="to-configure-performance-routing-method"></a><span data-ttu-id="4bcb6-107">To configure performance routing method</span><span class="sxs-lookup"><span data-stu-id="4bcb6-107">To configure performance routing method</span></span>

1. <span data-ttu-id="4bcb6-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-108">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="4bcb6-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-109">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="4bcb6-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-110">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="4bcb6-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-111">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="4bcb6-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span><span class="sxs-lookup"><span data-stu-id="4bcb6-112">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="4bcb6-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-113">For **traffic routing method settings**, for **Routing method** select **Performance**.</span></span>
    2. <span data-ttu-id="4bcb6-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span><span class="sxs-lookup"><span data-stu-id="4bcb6-114">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="4bcb6-115">Select the appropriate **Protocol**, and specify the **Port** number.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-115">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="4bcb6-116">For **Path** type a forward slash */*.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-116">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="4bcb6-117">To monitor endpoints, you must specify a path and filename.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-117">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="4bcb6-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-118">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="4bcb6-119">At the top of the page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-119">At the top of the page, click **Save**.</span></span>
5.  <span data-ttu-id="4bcb6-120">Test the changes in your configuration as follows:</span><span class="sxs-lookup"><span data-stu-id="4bcb6-120">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="4bcb6-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-121">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="4bcb6-122">In the **Traffic Manager** profile blade, click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-122">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="4bcb6-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-123">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="4bcb6-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-124">This can be used by any clients (for example, by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="4bcb6-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-125">In this case all requests are routed to the endpoint with the lowest latency from the client's network.</span></span>
6. <span data-ttu-id="4bcb6-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span><span class="sxs-lookup"><span data-stu-id="4bcb6-126">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configuring performance traffic routing method using Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="4bcb6-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="4bcb6-128">Next steps</span></span>

- <span data-ttu-id="4bcb6-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-129">Learn about [weighted traffic routing method](traffic-manager-configure-weighted-routing-method.md).</span></span>
- <span data-ttu-id="4bcb6-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-130">Learn about [priority routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="4bcb6-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-131">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="4bcb6-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="4bcb6-132">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-performance-routing-method/traffic-manager-performance-routing-method.png