---
title: Internal load balancer Overview | Microsoft Docs
description: Overview for internal load balancer and its features.How a load balancer works for Azure and possible scenarios to configure internal endpoints
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: tysonn
ms.assetid: 36065bfe-0ef1-46f9-a9e1-80b229105c85
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 10/24/2016
ms.author: kumud
ms.openlocfilehash: 36c5652e9842a62b77991e798ad0c92a09cd59fe
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551331"
---
# <a name="internal-load-balancer-overview"></a><span data-ttu-id="bbbed-103">Internal load balancer overview</span><span class="sxs-lookup"><span data-stu-id="bbbed-103">Internal load balancer overview</span></span>

<span data-ttu-id="bbbed-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="bbbed-104">Unlike the Internet facing load balancer, the internal load balancer (ILB) directs traffic only to resources inside the cloud service or using VPN to access the Azure infrastructure.</span></span> <span data-ttu-id="bbbed-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span><span class="sxs-lookup"><span data-stu-id="bbbed-105">The infrastructure restricts access to the load balanced virtual IP addresses (VIPs) of a Cloud Service or a Virtual Network so that they will never be directly exposed to an Internet endpoint.</span></span> <span data-ttu-id="bbbed-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span><span class="sxs-lookup"><span data-stu-id="bbbed-106">This enables internal line of business (LOB) applications to run in Azure and be accessed from within the cloud or from resources on-premises.</span></span>

## <a name="why-you-may-need-an-internal-load-balancer"></a><span data-ttu-id="bbbed-107">Why you may need an internal load balancer</span><span class="sxs-lookup"><span data-stu-id="bbbed-107">Why you may need an internal load balancer</span></span>

<span data-ttu-id="bbbed-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span><span class="sxs-lookup"><span data-stu-id="bbbed-108">Azure Internal Load Balancing (ILB) provides load balancing between virtual machines that reside inside of a cloud service or a virtual network with a regional scope.</span></span> <span data-ttu-id="bbbed-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span><span class="sxs-lookup"><span data-stu-id="bbbed-109">For information about the use and configuration of virtual networks with a regional scope, see [Regional Virtual Networks](https://azure.microsoft.com/blog/2014/05/14/regional-virtual-networks/) in the Azure blog.</span></span> <span data-ttu-id="bbbed-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span><span class="sxs-lookup"><span data-stu-id="bbbed-110">Existing virtual networks that have been configured for an affinity group cannot use ILB.</span></span>

<span data-ttu-id="bbbed-111">ILB enables the following types of load balancing:</span><span class="sxs-lookup"><span data-stu-id="bbbed-111">ILB enables the following types of load balancing:</span></span>

* <span data-ttu-id="bbbed-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span><span class="sxs-lookup"><span data-stu-id="bbbed-112">Within a cloud service, from virtual machines to a set of virtual machines that reside within the same cloud service (see Figure 1).</span></span>
* <span data-ttu-id="bbbed-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span><span class="sxs-lookup"><span data-stu-id="bbbed-113">Within a virtual network, from virtual machines in the virtual network to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 2).</span></span>
* <span data-ttu-id="bbbed-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span><span class="sxs-lookup"><span data-stu-id="bbbed-114">For a cross-premises virtual network, from on-premises computers to a set of virtual machines that reside within the same cloud service of the virtual network (see Figure 3).</span></span>
* <span data-ttu-id="bbbed-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span><span class="sxs-lookup"><span data-stu-id="bbbed-115">Internet-facing, multi-tier applications in which the back-end tiers are not Internet-facing but require load balancing for traffic from the Internet-facing tier.</span></span>
* <span data-ttu-id="bbbed-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span><span class="sxs-lookup"><span data-stu-id="bbbed-116">Load balancing for LOB applications hosted in Azure without requiring additional load balancer hardware or software.</span></span> <span data-ttu-id="bbbed-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span><span class="sxs-lookup"><span data-stu-id="bbbed-117">Including on-premises servers in the set of computers whose traffic is load balanced.</span></span>

## <a name="internet-facing-multi-tier-applications"></a><span data-ttu-id="bbbed-118">Internet facing multi-tier applications</span><span class="sxs-lookup"><span data-stu-id="bbbed-118">Internet facing multi-tier applications</span></span>

<span data-ttu-id="bbbed-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span><span class="sxs-lookup"><span data-stu-id="bbbed-119">The web tier has Internet facing endpoints for Internet clients and is part of a load-balanced set.</span></span> <span data-ttu-id="bbbed-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span><span class="sxs-lookup"><span data-stu-id="bbbed-120">The load balancer  distributes incoming traffic from web clients for TCP port 443 (HTTPS) to the web servers.</span></span>

<span data-ttu-id="bbbed-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span><span class="sxs-lookup"><span data-stu-id="bbbed-121">The database servers are behind an ILB endpoint which the web servers use for storage.</span></span> <span data-ttu-id="bbbed-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span><span class="sxs-lookup"><span data-stu-id="bbbed-122">This database service load balanced endpoint, which traffic is load balanced across the database servers in the ILB set.</span></span>

<span data-ttu-id="bbbed-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span><span class="sxs-lookup"><span data-stu-id="bbbed-123">The following image shows the Internet facing multi-tier application within the same cloud service.</span></span>

![Internal load balancing single cloud service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internal-overview/IC736321.png)

<span data-ttu-id="bbbed-125">Figure 1 - Internet facing multi-tier application</span><span class="sxs-lookup"><span data-stu-id="bbbed-125">Figure 1 - Internet facing multi-tier application</span></span>

<span data-ttu-id="bbbed-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span><span class="sxs-lookup"><span data-stu-id="bbbed-126">Another possible use for a multi-tier application is when the ILB deployed to a different cloud service than the one consuming the service for the ILB.</span></span>

<span data-ttu-id="bbbed-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span><span class="sxs-lookup"><span data-stu-id="bbbed-127">Cloud services using the same virtual network will have access to the ILB endpoint.</span></span> <span data-ttu-id="bbbed-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="bbbed-128">The following image shows front-end web servers are in a different cloud service from the database back-end and using the ILB endpoint within the same virtual network.</span></span>

![Internal load balancing between cloud services](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internal-overview/IC744147.png)

<span data-ttu-id="bbbed-130">Figure 2 - Front-end servers in a different cloud service</span><span class="sxs-lookup"><span data-stu-id="bbbed-130">Figure 2 - Front-end servers in a different cloud service</span></span>

## <a name="intranet-line-of-business-applications"></a><span data-ttu-id="bbbed-131">Intranet line of business applications</span><span class="sxs-lookup"><span data-stu-id="bbbed-131">Intranet line of business applications</span></span>

<span data-ttu-id="bbbed-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span><span class="sxs-lookup"><span data-stu-id="bbbed-132">Traffic from clients on the on-premises network get load-balanced across the set of LOB servers using VPN connection to Azure network.</span></span>

<span data-ttu-id="bbbed-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span><span class="sxs-lookup"><span data-stu-id="bbbed-133">The client machine will have access to an IP address from Azure VPN service using point to site VPN.</span></span> <span data-ttu-id="bbbed-134">It allows the use the LOB application hosted behind the ILB endpoint.</span><span class="sxs-lookup"><span data-stu-id="bbbed-134">It allows the use the LOB application hosted behind the ILB endpoint.</span></span>

![Internal load balancing using point to site VPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internal-overview/IC744148.png)

<span data-ttu-id="bbbed-136">Figure 3 - LOB applications hosted behind the LB endpoint</span><span class="sxs-lookup"><span data-stu-id="bbbed-136">Figure 3 - LOB applications hosted behind the LB endpoint</span></span>

<span data-ttu-id="bbbed-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span><span class="sxs-lookup"><span data-stu-id="bbbed-137">Another scenario for the LOB is to have a site to site VPN to the virtual network where the ILB endpoint is configured.</span></span> <span data-ttu-id="bbbed-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span><span class="sxs-lookup"><span data-stu-id="bbbed-138">This allows on-premises network traffic to be routed to the ILB endpoint.</span></span>

![Internal load balancing using site to site VPN](https://docstestmedia1.blob.core.windows.net/azure-media/articles/load-balancer/media/load-balancer-internal-overview/IC744150.png)

<span data-ttu-id="bbbed-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span><span class="sxs-lookup"><span data-stu-id="bbbed-140">Figure 4 - On-premises network traffic routed to the ILB endpoint</span></span>

## <a name="limitations"></a><span data-ttu-id="bbbed-141">Limitations</span><span class="sxs-lookup"><span data-stu-id="bbbed-141">Limitations</span></span>

<span data-ttu-id="bbbed-142">Internal Load Balancer configurations do not support SNAT.</span><span class="sxs-lookup"><span data-stu-id="bbbed-142">Internal Load Balancer configurations do not support SNAT.</span></span> <span data-ttu-id="bbbed-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span><span class="sxs-lookup"><span data-stu-id="bbbed-143">In the context of this document, SNAT refers to port masquerading source  network address translation.</span></span>  <span data-ttu-id="bbbed-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span><span class="sxs-lookup"><span data-stu-id="bbbed-144">This applies to scenarios where a VM in a load balancer pool needs to reach the respective internal Load Balancer's frontend IP address.</span></span> <span data-ttu-id="bbbed-145">This scenario is not supported for internal Load Balancer.</span><span class="sxs-lookup"><span data-stu-id="bbbed-145">This scenario is not supported for internal Load Balancer.</span></span> <span data-ttu-id="bbbed-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span><span class="sxs-lookup"><span data-stu-id="bbbed-146">Connection failures will occur when the flow is load balanced to the VM which originated the flow.</span></span> <span data-ttu-id="bbbed-147">You must use a proxy style load balancer for such scenarios.</span><span class="sxs-lookup"><span data-stu-id="bbbed-147">You must use a proxy style load balancer for such scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbbed-148">Next Steps</span><span class="sxs-lookup"><span data-stu-id="bbbed-148">Next Steps</span></span>

[<span data-ttu-id="bbbed-149">Azure Resource Manager support for Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="bbbed-149">Azure Resource Manager support for Azure Load Balancer</span></span>](load-balancer-arm.md)

[<span data-ttu-id="bbbed-150">Get started configuring an Internet facing load balancer</span><span class="sxs-lookup"><span data-stu-id="bbbed-150">Get started configuring an Internet facing load balancer</span></span>](load-balancer-get-started-internet-arm-ps.md)

[<span data-ttu-id="bbbed-151">Get started configuring an Internal load balancer</span><span class="sxs-lookup"><span data-stu-id="bbbed-151">Get started configuring an Internal load balancer</span></span>](load-balancer-get-started-ilb-arm-ps.md)

[<span data-ttu-id="bbbed-152">Configure a Load balancer distribution mode</span><span class="sxs-lookup"><span data-stu-id="bbbed-152">Configure a Load balancer distribution mode</span></span>](load-balancer-distribution-mode.md)

[<span data-ttu-id="bbbed-153">Configure idle TCP timeout settings for your load balancer</span><span class="sxs-lookup"><span data-stu-id="bbbed-153">Configure idle TCP timeout settings for your load balancer</span></span>](load-balancer-tcp-idle-timeout.md)




