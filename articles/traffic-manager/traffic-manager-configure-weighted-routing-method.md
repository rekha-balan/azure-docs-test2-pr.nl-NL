---
title: Configure weighted round-robin traffic routing method using Azure Traffic Manager | Microsoft Docs
description: This article explains how to load balance traffic using a round-robin method in Traffic Manager
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
ms.openlocfilehash: 61dd854f0a792fc318d64d6ed4da5921a9ea2a95
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549748"
---
# <a name="configure-the-weighted-traffic-routing-method-in-traffic-manager"></a><span data-ttu-id="676b4-103">Configure the weighted traffic routing method in Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="676b4-103">Configure the weighted traffic routing method in Traffic Manager</span></span>

<span data-ttu-id="676b4-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="676b4-104">A common traffic routing method pattern is to provide a set of identical endpoints, which include cloud services and websites, and send traffic to each in a round-robin fashion.</span></span> <span data-ttu-id="676b4-105">The following steps outline how to configure this type of traffic routing method.</span><span class="sxs-lookup"><span data-stu-id="676b4-105">The following steps outline how to configure this type of traffic routing method.</span></span>

> [!NOTE]
> <span data-ttu-id="676b4-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span><span class="sxs-lookup"><span data-stu-id="676b4-106">Azure Websites already provide round-robin load balancing functionality for websites within a datacenter (also known as a region).</span></span> <span data-ttu-id="676b4-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span><span class="sxs-lookup"><span data-stu-id="676b4-107">Traffic Manager allows you to specify round-robin traffic routing method for websites in different datacenters.</span></span>

## <a name="to-configure-the-weighted-traffic-routing-method"></a><span data-ttu-id="676b4-108">To configure the weighted traffic routing method</span><span class="sxs-lookup"><span data-stu-id="676b4-108">To configure the weighted traffic routing method</span></span>

1. <span data-ttu-id="676b4-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="676b4-109">From a browser, sign in to the [Azure portal](http://portal.azure.com).</span></span> <span data-ttu-id="676b4-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="676b4-110">If you don’t already have an account, you can sign up for a [free one-month trial](https://azure.microsoft.com/free/).</span></span> 
2. <span data-ttu-id="676b4-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span><span class="sxs-lookup"><span data-stu-id="676b4-111">In the portal’s search bar, search for the **Traffic Manager profiles** and then click the profile name that you want to configure the routing method for.</span></span>
3. <span data-ttu-id="676b4-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span><span class="sxs-lookup"><span data-stu-id="676b4-112">In the **Traffic Manager profile** blade, verify that both the cloud services and websites that you want to include in your configuration are present.</span></span>
4. <span data-ttu-id="676b4-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span><span class="sxs-lookup"><span data-stu-id="676b4-113">In the **Settings** section, click **Configuration**, and in the **Configuration** blade, complete as follows:</span></span>
    1. <span data-ttu-id="676b4-114">For **traffic routing method settings**, verify that the traffic routing method is **Failover**.</span><span class="sxs-lookup"><span data-stu-id="676b4-114">For **traffic routing method settings**, verify that the traffic routing method is **Failover**.</span></span> <span data-ttu-id="676b4-115">If it is not, click **Failover** from the dropdown list.</span><span class="sxs-lookup"><span data-stu-id="676b4-115">If it is not, click **Failover** from the dropdown list.</span></span>
    2. <span data-ttu-id="676b4-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span><span class="sxs-lookup"><span data-stu-id="676b4-116">Set the **Endpoint monitor settings** identical for all every endpoint within this profile as follows:</span></span>
        1. <span data-ttu-id="676b4-117">Select the appropriate **Protocol**, and specify the **Port** number.</span><span class="sxs-lookup"><span data-stu-id="676b4-117">Select the appropriate **Protocol**, and specify the **Port** number.</span></span> 
        2. <span data-ttu-id="676b4-118">For **Path** type a forward slash */*.</span><span class="sxs-lookup"><span data-stu-id="676b4-118">For **Path** type a forward slash */*.</span></span> <span data-ttu-id="676b4-119">To monitor endpoints, you must specify a path and filename.</span><span class="sxs-lookup"><span data-stu-id="676b4-119">To monitor endpoints, you must specify a path and filename.</span></span> <span data-ttu-id="676b4-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span><span class="sxs-lookup"><span data-stu-id="676b4-120">A forward slash "/" is a valid entry for the relative path and implies that the file is in the root directory (default).</span></span>
        3. <span data-ttu-id="676b4-121">At the top of the page, click **Save**.</span><span class="sxs-lookup"><span data-stu-id="676b4-121">At the top of the page, click **Save**.</span></span>
5. <span data-ttu-id="676b4-122">Test the changes in your configuration as follows:</span><span class="sxs-lookup"><span data-stu-id="676b4-122">Test the changes in your configuration as follows:</span></span>
    1.  <span data-ttu-id="676b4-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span><span class="sxs-lookup"><span data-stu-id="676b4-123">In the portal’s search bar, search for the Traffic Manager profile name and click the Traffic Manager profile in the results that the displayed.</span></span>
    2.  <span data-ttu-id="676b4-124">In the **Traffic Manager** profile blade, click **Overview**.</span><span class="sxs-lookup"><span data-stu-id="676b4-124">In the **Traffic Manager** profile blade, click **Overview**.</span></span>
    3.  <span data-ttu-id="676b4-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="676b4-125">The **Traffic Manager profile** blade displays the DNS name of your newly created Traffic Manager profile.</span></span> <span data-ttu-id="676b4-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span><span class="sxs-lookup"><span data-stu-id="676b4-126">This can be used by any clients (for example,by navigating to it using a web browser) to get routed to the right endpoint as determined by the routing type.</span></span> <span data-ttu-id="676b4-127">In this case all requests are routed each endpoint in a round-robin fashion.</span><span class="sxs-lookup"><span data-stu-id="676b4-127">In this case all requests are routed each endpoint in a round-robin fashion.</span></span>
6. <span data-ttu-id="676b4-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span><span class="sxs-lookup"><span data-stu-id="676b4-128">Once your Traffic Manager profile is working, edit the DNS record on your authoritative DNS server to point your company domain name to the Traffic Manager domain name.</span></span>

![Configuring weighted traffic routing method using Traffic Manager][1]

## <a name="next-steps"></a><span data-ttu-id="676b4-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="676b4-130">Next steps</span></span>

- <span data-ttu-id="676b4-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="676b4-131">Learn about [priority traffic routing method](traffic-manager-configure-priority-routing-method.md).</span></span>
- <span data-ttu-id="676b4-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="676b4-132">Learn about [performance traffic routing method](traffic-manager-configure-performance-routing-method.md).</span></span>
- <span data-ttu-id="676b4-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span><span class="sxs-lookup"><span data-stu-id="676b4-133">Learn about [geographic routing method](traffic-manager-configure-geographic-routing-method.md).</span></span>
- <span data-ttu-id="676b4-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span><span class="sxs-lookup"><span data-stu-id="676b4-134">Learn how to [test Traffic Manager settings](traffic-manager-testing-settings.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/traffic-manager/media/traffic-manager-weighted-routing-method/traffic-manager-weighted-routing-method.png

