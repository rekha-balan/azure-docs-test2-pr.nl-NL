---
title: What to do in the event of an Azure service disruption that impacts Azure Cloud Services | Microsoft Docs
description: Learn what to do in the event of an Azure service disruption that impacts Azure Cloud Services.
services: cloud-services
documentationcenter: ''
author: mmccrory
manager: drewm
editor: ''
ms.assetid: e52634ab-003d-4f1e-85fa-794f6cd12ce4
ms.service: cloud-services
ms.workload: cloud-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: mmccrory
ms.openlocfilehash: 2a46eb16ca95dc86e93950b99f6219c24b8219a4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540962"
---
# <a name="what-to-do-in-the-event-of-an-azure-service-disruption-that-impacts-azure-cloud-services"></a>What to do in the event of an Azure service disruption that impacts Azure Cloud Services
At Microsoft, we work hard to make sure that our services are always available to you when you need them. Forces beyond our control sometimes impact us in ways that cause unplanned service disruptions.

Microsoft provides a Service Level Agreement (SLA) for its services as a commitment for uptime and connectivity. The SLA for individual Azure services can be found at [Azure Service Level Agreements](https://azure.microsoft.com/support/legal/sla/).

Azure already has many built-in platform features that support highly available applications. For more about these services, read [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

This article covers a true disaster recovery scenario, when a whole region experiences an outage due to major natural disaster or widespread service interruption. These are rare occurrences, but you must prepare for the possibility that there is an outage of an entire region. If an entire region experiences a service disruption, the locally redundant copies of your data would temporarily be unavailable. If you have enabled geo-replication, three additional copies of your Azure Storage blobs and tables are stored in a different region. In the event of a complete regional outage or a disaster in which the primary region is not recoverable, Azure remaps all of the DNS entries to the geo-replicated region.

> [!NOTE]
> Be aware that you do not have any control over this process, and it will only occur for datacenter-wide service disruptions. Because of this, you must also rely on other application-specific backup strategies to achieve the highest level of availability. For more information, see [Disaster recovery and high availability for applications built on Microsoft Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md). If you would like to be able to affect your own failover, you might want to consider the use of [read-access geo-redundant storage (RA-GRS)](../storage/storage-redundancy.md#read-access-geo-redundant-storage), which creates a read-only copy of your data in another region.
>
>


## <a name="option-1-use-a-backup-deployment-through-azure-traffic-manager"></a>Option 1: Use a backup deployment through Azure Traffic Manager
The most robust disaster recovery solution involves maintaining multiple deployments of your application in different regions, then using [Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md) to direct traffic between them. Azure Traffic Manager provides multiple [routing methods](../traffic-manager/traffic-manager-routing-methods.md), so you can choose whether to manage your deployments using a primary/backup model or to split traffic between them.

![Balancing Azure Cloud Services across regions with Azure Traffic Manager](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cloud-services/media/cloud-services-disaster-recovery-guidance/using-azure-traffic-manager.png)

For the fastest response to the loss of a region, it is important that you configure Traffic Manager's [endpoint monitoring](../traffic-manager/traffic-manager-monitoring.md).

## <a name="option-2-deploy-your-application-to-a-new-region"></a>Option 2: Deploy your application to a new region
Maintaining multiple active deployments as described in the previous option incurs additional ongoing costs. If your recovery time objective (RTO) is flexible enough and you have the original code or compiled Cloud Services package, you can create a new instance of your application in another region and update your DNS records to point to the new deployment.

For more detail about how to create and deploy a cloud service application, see [How to create and deploy a cloud service](cloud-services-how-to-create-deploy-portal.md).

Depending on your application data sources, you may need to check the recovery procedures for your application data source.

* For Azure Storage data sources, see [Azure Storage replication](../storage/storage-redundancy.md#read-access-geo-redundant-storage) to check on the options that are available based on the chose replication model for your application.
* For SQL Database sources, read [Overview: Cloud business continuity and database disaster recovery with SQL Database](../sql-database/sql-database-business-continuity.md) to check on the options that are available based on the chosen replication model for your application.


## <a name="option-3-wait-for-recovery"></a>Option 3: Wait for recovery
In this case, no action on your part is required, but your service will be unavailable until the region is restored. You can see the current service status on the [Azure Service Health Dashboard](https://azure.microsoft.com/status/).

## <a name="next-steps"></a>Next steps
To learn more about how to implement a disaster recovery and high availability strategy, see [Disaster recovery and high availability for Azure applications](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md).

To develop a detailed technical understanding of a cloud platform’s capabilities, see [Azure resiliency technical guidance](../resiliency/resiliency-technical-guidance.md).
