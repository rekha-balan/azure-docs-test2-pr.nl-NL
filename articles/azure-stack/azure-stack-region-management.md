---
title: Region management in Azure Stack | Microsoft Docs
description: Overview of region management in Azure Stack.
services: azure-stack
documentationcenter: ''
author: efemmano
manager: dsavage
editor: ''
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: efemmano
ms.openlocfilehash: 14730fb39bdb16fa7b0fd9f8b2adcd497ac5412b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540995"
---
# <a name="region-management-in-azure-stack"></a>Region management in Azure Stack
Azure Stack has the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure. Inside Region Management, you can find all resources that are required to successfully operate the Azure Stack infrastructure lifecycle.

The Azure Stack Proof of Concept (POC) is a single-node deployment, and equals one region. If you set up another instance of Azure Stack POC on separate hardware, this instance is a different region.

## <a name="information-available-through-the-region-management-tile"></a>Information available through the Region Management tile
This preview release of Azure Stack has a set of region management capabilities available in the **Region Management** tile. This tile is available to a cloud administrator on the default dashboard in the administrator portal. Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.

 ![The region management tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-region/Image1.png)

 If you click a region in the Region Management tile, you can access the following information:

  ![Description of panes on the Region Management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-region/image2.PNG)

1. **The resource menu**. Here, you can access specific infrastructure management areas, view and manage tenant resources such as storage accounts and virtual networks, and find links to Azure Stack-related documentation (through **Quick start**).

2. **Alerts**. This tile lists system-wide alerts and provides details on each of those alerts.

3. **Updates**. In this tile, you can view the update status of your Azure Stack infrastructure, including version, update availability, and updates history.

4. **Resource providers**. Resource providers is the place to manage the tenant functionality offered by the components required to run Azure Stack. Each resource provider comes with an administrative experience. This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.
 
   >[!NOTE]
   In Azure Stack Technical Preview 3, only Storage, Compute, and Network resource providers offer an associated administrative experience.

5. **Infrastructure roles**. Infrastructure roles are the components necessary to run Azure Stack. By clicking a role, you can view the alerts associated with the specific role and the role instances where this role is running. Starting in Technical Preview 3, you can start, restart, or shut down an infrastructure role instance.

   >[!NOTE]
   In Azure Stack Technical Preview 3, not all infrastructure roles surface alerts in this journey.

## <a name="next-steps"></a>Next steps
[Monitor health and alerts in Azure Stack](azure-stack-monitor-health.md)

[Manage updates in Azure Stack](azure-stack-updates.md)








