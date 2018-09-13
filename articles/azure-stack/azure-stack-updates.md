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
# <a name="manage-updates-in-azure-stack-overview"></a><span data-ttu-id="6e31b-103">Manage updates in Azure Stack overview</span><span class="sxs-lookup"><span data-stu-id="6e31b-103">Manage updates in Azure Stack overview</span></span>

<span data-ttu-id="6e31b-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="6e31b-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="6e31b-105">Microsoft update packages for Azure Stack integrated systems typically release around the fourth Tuesday of each month.</span><span class="sxs-lookup"><span data-stu-id="6e31b-105">Microsoft update packages for Azure Stack integrated systems typically release around the fourth Tuesday of each month.</span></span> <span data-ttu-id="6e31b-106">Ask your OEM about their specific notification process to ensure update notifications reach your organization.</span><span class="sxs-lookup"><span data-stu-id="6e31b-106">Ask your OEM about their specific notification process to ensure update notifications reach your organization.</span></span> <span data-ttu-id="6e31b-107">You can also check in this documentation library under **Overview** > **Release notes** for information about releases that are in active support.</span><span class="sxs-lookup"><span data-stu-id="6e31b-107">You can also check in this documentation library under **Overview** > **Release notes** for information about releases that are in active support.</span></span> 

<span data-ttu-id="6e31b-108">Each release of Microsoft software updates is bundled as a single update package.</span><span class="sxs-lookup"><span data-stu-id="6e31b-108">Each release of Microsoft software updates is bundled as a single update package.</span></span> <span data-ttu-id="6e31b-109">As an Azure Stack operator, you can import, install, and monitor the installation progress of these update packages from the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="6e31b-109">As an Azure Stack operator, you can import, install, and monitor the installation progress of these update packages from the administrator portal.</span></span> 

<span data-ttu-id="6e31b-110">Your original equipment manufacturer (OEM) hardware vendor will also release updates, such as driver and firmware updates.</span><span class="sxs-lookup"><span data-stu-id="6e31b-110">Your original equipment manufacturer (OEM) hardware vendor will also release updates, such as driver and firmware updates.</span></span> <span data-ttu-id="6e31b-111">While these updates are delivered as separate packages by your OEM hardware vendor, they are imported, installed, and managed the same way update packages from Microsoft update packages are imported, installed, and managed.</span><span class="sxs-lookup"><span data-stu-id="6e31b-111">While these updates are delivered as separate packages by your OEM hardware vendor, they are imported, installed, and managed the same way update packages from Microsoft update packages are imported, installed, and managed.</span></span>

<span data-ttu-id="6e31b-112">To keep your system under support, you must keep Azure Stack updated to a specific version level.</span><span class="sxs-lookup"><span data-stu-id="6e31b-112">To keep your system under support, you must keep Azure Stack updated to a specific version level.</span></span> <span data-ttu-id="6e31b-113">Make sure that you review the [Azure Stack servicing policy](azure-stack-servicing-policy.md).</span><span class="sxs-lookup"><span data-stu-id="6e31b-113">Make sure that you review the [Azure Stack servicing policy](azure-stack-servicing-policy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6e31b-114">You can't apply Azure Stack update packages to Azure Stack Development Kit.</span><span class="sxs-lookup"><span data-stu-id="6e31b-114">You can't apply Azure Stack update packages to Azure Stack Development Kit.</span></span> <span data-ttu-id="6e31b-115">The update packages are designed for integrated systems.</span><span class="sxs-lookup"><span data-stu-id="6e31b-115">The update packages are designed for integrated systems.</span></span> <span data-ttu-id="6e31b-116">For information, see [Redeploy the ASDK](https://docs.microsoft.com/en-us/azure/azure-stack/asdk).</span><span class="sxs-lookup"><span data-stu-id="6e31b-116">For information, see [Redeploy the ASDK](https://docs.microsoft.com/en-us/azure/azure-stack/asdk).</span></span>

## <a name="the-update-resource-provider"></a><span data-ttu-id="6e31b-117">The Update resource provider</span><span class="sxs-lookup"><span data-stu-id="6e31b-117">The Update resource provider</span></span>

<span data-ttu-id="6e31b-118">Azure Stack includes an Update resource provider that orchestrates the application of Microsoft software updates.</span><span class="sxs-lookup"><span data-stu-id="6e31b-118">Azure Stack includes an Update resource provider that orchestrates the application of Microsoft software updates.</span></span> <span data-ttu-id="6e31b-119">This resource provider ensures that updates are applied across all physical hosts, Service Fabric applications and runtimes, and all infrastructure virtual machines and their associated services.</span><span class="sxs-lookup"><span data-stu-id="6e31b-119">This resource provider ensures that updates are applied across all physical hosts, Service Fabric applications and runtimes, and all infrastructure virtual machines and their associated services.</span></span>

<span data-ttu-id="6e31b-120">As updates install, you can view high-level status as the update process targets the various subsystems in Azure Stack (for example, physical hosts, and infrastructure virtual machines).</span><span class="sxs-lookup"><span data-stu-id="6e31b-120">As updates install, you can view high-level status as the update process targets the various subsystems in Azure Stack (for example, physical hosts, and infrastructure virtual machines).</span></span>

## <a name="plan-for-updates"></a><span data-ttu-id="6e31b-121">Plan for updates</span><span class="sxs-lookup"><span data-stu-id="6e31b-121">Plan for updates</span></span>

<span data-ttu-id="6e31b-122">We strongly recommend that you notify users of any maintenance operations, and that you schedule normal maintenance windows during non-business hours if possible.</span><span class="sxs-lookup"><span data-stu-id="6e31b-122">We strongly recommend that you notify users of any maintenance operations, and that you schedule normal maintenance windows during non-business hours if possible.</span></span> <span data-ttu-id="6e31b-123">Maintenance operations can affect both tenant workloads and portal operations.</span><span class="sxs-lookup"><span data-stu-id="6e31b-123">Maintenance operations can affect both tenant workloads and portal operations.</span></span>

## <a name="using-the-update-tile-to-manage-updates"></a><span data-ttu-id="6e31b-124">Using the Update tile to manage updates</span><span class="sxs-lookup"><span data-stu-id="6e31b-124">Using the Update tile to manage updates</span></span>
<span data-ttu-id="6e31b-125">You manage updates from the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="6e31b-125">You manage updates from the administrator portal.</span></span> <span data-ttu-id="6e31b-126">As an Azure Stack operator you can use the Update tile in the dashboard to:</span><span class="sxs-lookup"><span data-stu-id="6e31b-126">As an Azure Stack operator you can use the Update tile in the dashboard to:</span></span>

- <span data-ttu-id="6e31b-127">view important information such as the current version.</span><span class="sxs-lookup"><span data-stu-id="6e31b-127">view important information such as the current version.</span></span>
- <span data-ttu-id="6e31b-128">install updates, and monitor progress.</span><span class="sxs-lookup"><span data-stu-id="6e31b-128">install updates, and monitor progress.</span></span>
- <span data-ttu-id="6e31b-129">review update history for previously installed updates.</span><span class="sxs-lookup"><span data-stu-id="6e31b-129">review update history for previously installed updates.</span></span>
 
## <a name="determine-the-current-version"></a><span data-ttu-id="6e31b-130">Determine the current version</span><span class="sxs-lookup"><span data-stu-id="6e31b-130">Determine the current version</span></span>

<span data-ttu-id="6e31b-131">The Update tile shows the current version of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="6e31b-131">The Update tile shows the current version of Azure Stack.</span></span> <span data-ttu-id="6e31b-132">You can get to the Update tile by using either of the following methods in the administrator portal:</span><span class="sxs-lookup"><span data-stu-id="6e31b-132">You can get to the Update tile by using either of the following methods in the administrator portal:</span></span>

- <span data-ttu-id="6e31b-133">On the dashboard, view the current version in the **Update** tile.</span><span class="sxs-lookup"><span data-stu-id="6e31b-133">On the dashboard, view the current version in the **Update** tile.</span></span>
 
   ![Updates tile on default dashboard](./media/azure-stack-updates/image1.png)
 
- <span data-ttu-id="6e31b-135">On the **Region management** tile, click the region name.</span><span class="sxs-lookup"><span data-stu-id="6e31b-135">On the **Region management** tile, click the region name.</span></span> <span data-ttu-id="6e31b-136">View the current version in the **Update** tile.</span><span class="sxs-lookup"><span data-stu-id="6e31b-136">View the current version in the **Update** tile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6e31b-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="6e31b-137">Next steps</span></span>

- [<span data-ttu-id="6e31b-138">Azure Stack servicing policy</span><span class="sxs-lookup"><span data-stu-id="6e31b-138">Azure Stack servicing policy</span></span>](azure-stack-servicing-policy.md) 
- [<span data-ttu-id="6e31b-139">Region management in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="6e31b-139">Region management in Azure Stack</span></span>](azure-stack-region-management.md)     


