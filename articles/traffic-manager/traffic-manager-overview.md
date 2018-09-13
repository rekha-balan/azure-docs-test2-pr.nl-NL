---
title: Azure Traffic Manager | Microsoft Docs
description: This article provides an overview of Azure Traffic Manager. Find out if it is the right choice for load balancing user traffic for your application.
services: traffic-manager
documentationcenter: ''
author: kumudd
manager: jeconnoc
editor: ''
ms.service: traffic-manager
customer intent: As an IT admin, I want to learn about Traffic Manager and what I can use it for.
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/25/2018
ms.author: kumud
ms.openlocfilehash: 236137b87351e3c3a95c1103f7464256f41b9159
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44780525"
---
# <a name="what-is-traffic-manager"></a><span data-ttu-id="a805b-104">What is Traffic Manager?</span><span class="sxs-lookup"><span data-stu-id="a805b-104">What is Traffic Manager?</span></span>
<span data-ttu-id="a805b-105">Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness.</span><span class="sxs-lookup"><span data-stu-id="a805b-105">Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness.</span></span>

<span data-ttu-id="a805b-106">Traffic Manager uses DNS to direct client requests to the most appropriate service endpoint based on a traffic-routing method and the health of the endpoints.</span><span class="sxs-lookup"><span data-stu-id="a805b-106">Traffic Manager uses DNS to direct client requests to the most appropriate service endpoint based on a traffic-routing method and the health of the endpoints.</span></span> <span data-ttu-id="a805b-107">An endpoint is any Internet-facing service hosted inside or outside of Azure.</span><span class="sxs-lookup"><span data-stu-id="a805b-107">An endpoint is any Internet-facing service hosted inside or outside of Azure.</span></span> <span data-ttu-id="a805b-108">Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) to suit different application needs and automatic failover models.</span><span class="sxs-lookup"><span data-stu-id="a805b-108">Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) to suit different application needs and automatic failover models.</span></span> <span data-ttu-id="a805b-109">Traffic Manager is resilient to failure, including the failure of an entire Azure region.</span><span class="sxs-lookup"><span data-stu-id="a805b-109">Traffic Manager is resilient to failure, including the failure of an entire Azure region.</span></span>

>[!NOTE]
> <span data-ttu-id="a805b-110">Azure provides a suite of fully managed load-balancing solutions for your scenarios.</span><span class="sxs-lookup"><span data-stu-id="a805b-110">Azure provides a suite of fully managed load-balancing solutions for your scenarios.</span></span> <span data-ttu-id="a805b-111">If you are looking for Transport Layer Security (TLS) protocol termination ("SSL offload") or per-HTTP/HTTPS request, application-layer processing, review [Application Gateway](../application-gateway/application-gateway-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="a805b-111">If you are looking for Transport Layer Security (TLS) protocol termination ("SSL offload") or per-HTTP/HTTPS request, application-layer processing, review [Application Gateway](../application-gateway/application-gateway-introduction.md).</span></span> <span data-ttu-id="a805b-112">If you are looking for regional balancing, review [Load Balancer](../load-balancer/load-balancer-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a805b-112">If you are looking for regional balancing, review [Load Balancer](../load-balancer/load-balancer-overview.md).</span></span> <span data-ttu-id="a805b-113">Your end-to-end scenarios might benefit from combining these solutions as needed.</span><span class="sxs-lookup"><span data-stu-id="a805b-113">Your end-to-end scenarios might benefit from combining these solutions as needed.</span></span>

<span data-ttu-id="a805b-114">The following features are included with Traffic Manager:</span><span class="sxs-lookup"><span data-stu-id="a805b-114">The following features are included with Traffic Manager:</span></span>

## <a name="increase-application-availability"></a><span data-ttu-id="a805b-115">Increase application availability</span><span class="sxs-lookup"><span data-stu-id="a805b-115">Increase application availability</span></span>

<span data-ttu-id="a805b-116">Traffic Manager delivers high availability for your critical applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.</span><span class="sxs-lookup"><span data-stu-id="a805b-116">Traffic Manager delivers high availability for your critical applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.</span></span>
    
## <a name="improve-application-performance"></a><span data-ttu-id="a805b-117">Improve application performance</span><span class="sxs-lookup"><span data-stu-id="a805b-117">Improve application performance</span></span>

<span data-ttu-id="a805b-118">Azure allows you to run cloud services or websites in datacenters located around the world.</span><span class="sxs-lookup"><span data-stu-id="a805b-118">Azure allows you to run cloud services or websites in datacenters located around the world.</span></span> <span data-ttu-id="a805b-119">Traffic Manager improves application responsiveness by directing traffic to the endpoint with the lowest network latency for the client.</span><span class="sxs-lookup"><span data-stu-id="a805b-119">Traffic Manager improves application responsiveness by directing traffic to the endpoint with the lowest network latency for the client.</span></span>

## <a name="perform-service-maintenance-without-downtime"></a><span data-ttu-id="a805b-120">Perform service maintenance without downtime</span><span class="sxs-lookup"><span data-stu-id="a805b-120">Perform service maintenance without downtime</span></span>

<span data-ttu-id="a805b-121">You can perform planned maintenance operations on your applications without downtime.</span><span class="sxs-lookup"><span data-stu-id="a805b-121">You can perform planned maintenance operations on your applications without downtime.</span></span> <span data-ttu-id="a805b-122">Traffic Manager directs traffic to alternative endpoints while the maintenance is in progress.</span><span class="sxs-lookup"><span data-stu-id="a805b-122">Traffic Manager directs traffic to alternative endpoints while the maintenance is in progress.</span></span>

## <a name="combine-hybrid-applications"></a><span data-ttu-id="a805b-123">Combine hybrid applications</span><span class="sxs-lookup"><span data-stu-id="a805b-123">Combine hybrid applications</span></span>

<span data-ttu-id="a805b-124">Traffic Manager supports external, non-Azure endpoints enabling it to be used with hybrid cloud and on-premises deployments, including the "[burst-to-cloud](https://azure.microsoft.com/overview/what-is-cloud-bursting/)," "migrate-to-cloud," and "failover-to-cloud" scenarios.</span><span class="sxs-lookup"><span data-stu-id="a805b-124">Traffic Manager supports external, non-Azure endpoints enabling it to be used with hybrid cloud and on-premises deployments, including the "[burst-to-cloud](https://azure.microsoft.com/overview/what-is-cloud-bursting/)," "migrate-to-cloud," and "failover-to-cloud" scenarios.</span></span>

## <a name="distribute-traffic-for-complex-deployments"></a><span data-ttu-id="a805b-125">Distribute traffic for complex deployments</span><span class="sxs-lookup"><span data-stu-id="a805b-125">Distribute traffic for complex deployments</span></span>

<span data-ttu-id="a805b-126">Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined to create sophisticated and flexible rules to scale to the needs of larger, more complex deployments.</span><span class="sxs-lookup"><span data-stu-id="a805b-126">Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined to create sophisticated and flexible rules to scale to the needs of larger, more complex deployments.</span></span>

## <a name="pricing"></a><span data-ttu-id="a805b-127">Pricing</span><span class="sxs-lookup"><span data-stu-id="a805b-127">Pricing</span></span>

<span data-ttu-id="a805b-128">For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="a805b-128">For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a805b-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="a805b-129">Next steps</span></span>

- <span data-ttu-id="a805b-130">Learn how to [create a Traffic Manager profile](traffic-manager-create-profile.md).</span><span class="sxs-lookup"><span data-stu-id="a805b-130">Learn how to [create a Traffic Manager profile](traffic-manager-create-profile.md).</span></span>
- <span data-ttu-id="a805b-131">Learn [how Traffic Manager Works](traffic-manager-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="a805b-131">Learn [how Traffic Manager Works](traffic-manager-how-it-works.md).</span></span>
- <span data-ttu-id="a805b-132">View [frequently asked questions](traffic-manager-FAQs.md) about Traffic Manager.</span><span class="sxs-lookup"><span data-stu-id="a805b-132">View [frequently asked questions](traffic-manager-FAQs.md) about Traffic Manager.</span></span>




