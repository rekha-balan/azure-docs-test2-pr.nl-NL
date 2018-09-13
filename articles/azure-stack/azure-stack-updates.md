---
title: Manage updates in Azure Stack overview | Microsoft Docs
description: Learn about update management for Azure Stack integrated systems.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: 9b0781f4-2cd5-4619-a9b1-59182b4a6e43
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: 4d8a79862dac53429acda14f81818f92a96df529
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828698"
---
# <a name="manage-updates-in-azure-stack-overview"></a>Manage updates in Azure Stack overview

*Applies to: Azure Stack integrated systems*

Microsoft update packages for Azure Stack integrated systems typically release around the fourth Tuesday of each month. Ask your OEM about their specific notification process to ensure update notifications reach your organization. You can also check in this documentation library under **Overview** > **Release notes** for information about releases that are in active support. 

Each release of Microsoft software updates is bundled as a single update package. As an Azure Stack operator, you can import, install, and monitor the installation progress of these update packages from the administrator portal. 

Your original equipment manufacturer (OEM) hardware vendor will also release updates, such as driver and firmware updates. While these updates are delivered as separate packages by your OEM hardware vendor, they are imported, installed, and managed the same way update packages from Microsoft update packages are imported, installed, and managed.

To keep your system under support, you must keep Azure Stack updated to a specific version level. Make sure that you review the [Azure Stack servicing policy](azure-stack-servicing-policy.md).

> [!NOTE]
> You can't apply Azure Stack update packages to Azure Stack Development Kit. The update packages are designed for integrated systems. For information, see [Redeploy the ASDK](https://docs.microsoft.com/en-us/azure/azure-stack/asdk).

## <a name="the-update-resource-provider"></a>The Update resource provider

Azure Stack includes an Update resource provider that orchestrates the application of Microsoft software updates. This resource provider ensures that updates are applied across all physical hosts, Service Fabric applications and runtimes, and all infrastructure virtual machines and their associated services.

As updates install, you can view high-level status as the update process targets the various subsystems in Azure Stack (for example, physical hosts, and infrastructure virtual machines).

## <a name="plan-for-updates"></a>Plan for updates

We strongly recommend that you notify users of any maintenance operations, and that you schedule normal maintenance windows during non-business hours if possible. Maintenance operations can affect both tenant workloads and portal operations.

## <a name="using-the-update-tile-to-manage-updates"></a>Using the Update tile to manage updates
You manage updates from the administrator portal. As an Azure Stack operator you can use the Update tile in the dashboard to:

- view important information such as the current version.
- install updates, and monitor progress.
- review update history for previously installed updates.
 
## <a name="determine-the-current-version"></a>Determine the current version

The Update tile shows the current version of Azure Stack. You can get to the Update tile by using either of the following methods in the administrator portal:

- On the dashboard, view the current version in the **Update** tile.
 
   ![Updates tile on default dashboard](./media/azure-stack-updates/image1.png)
 
- On the **Region management** tile, click the region name. View the current version in the **Update** tile.

## <a name="next-steps"></a>Next steps

- [Azure Stack servicing policy](azure-stack-servicing-policy.md) 
- [Region management in Azure Stack](azure-stack-region-management.md)     


