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
# <a name="what-is-traffic-manager"></a>What is Traffic Manager?
Azure Traffic Manager is a DNS-based traffic load balancer that enables you to distribute traffic optimally to services across global Azure regions, while providing high availability and responsiveness.

Traffic Manager uses DNS to direct client requests to the most appropriate service endpoint based on a traffic-routing method and the health of the endpoints. An endpoint is any Internet-facing service hosted inside or outside of Azure. Traffic Manager provides a range of [traffic-routing methods](traffic-manager-routing-methods.md) and [endpoint monitoring options](traffic-manager-monitoring.md) to suit different application needs and automatic failover models. Traffic Manager is resilient to failure, including the failure of an entire Azure region.

>[!NOTE]
> Azure provides a suite of fully managed load-balancing solutions for your scenarios. If you are looking for Transport Layer Security (TLS) protocol termination ("SSL offload") or per-HTTP/HTTPS request, application-layer processing, review [Application Gateway](../application-gateway/application-gateway-introduction.md). If you are looking for regional balancing, review [Load Balancer](../load-balancer/load-balancer-overview.md). Your end-to-end scenarios might benefit from combining these solutions as needed.

The following features are included with Traffic Manager:

## <a name="increase-application-availability"></a>Increase application availability

Traffic Manager delivers high availability for your critical applications by monitoring your endpoints and providing automatic failover when an endpoint goes down.
    
## <a name="improve-application-performance"></a>Improve application performance

Azure allows you to run cloud services or websites in datacenters located around the world. Traffic Manager improves application responsiveness by directing traffic to the endpoint with the lowest network latency for the client.

## <a name="perform-service-maintenance-without-downtime"></a>Perform service maintenance without downtime

You can perform planned maintenance operations on your applications without downtime. Traffic Manager directs traffic to alternative endpoints while the maintenance is in progress.

## <a name="combine-hybrid-applications"></a>Combine hybrid applications

Traffic Manager supports external, non-Azure endpoints enabling it to be used with hybrid cloud and on-premises deployments, including the "[burst-to-cloud](https://azure.microsoft.com/overview/what-is-cloud-bursting/)," "migrate-to-cloud," and "failover-to-cloud" scenarios.

## <a name="distribute-traffic-for-complex-deployments"></a>Distribute traffic for complex deployments

Using [nested Traffic Manager profiles](traffic-manager-nested-profiles.md), traffic-routing methods can be combined to create sophisticated and flexible rules to scale to the needs of larger, more complex deployments.

## <a name="pricing"></a>Pricing

For pricing information, see [Traffic Manager Pricing](https://azure.microsoft.com/pricing/details/traffic-manager/).


## <a name="next-steps"></a>Next steps

- Learn how to [create a Traffic Manager profile](traffic-manager-create-profile.md).
- Learn [how Traffic Manager Works](traffic-manager-how-it-works.md).
- View [frequently asked questions](traffic-manager-FAQs.md) about Traffic Manager.




