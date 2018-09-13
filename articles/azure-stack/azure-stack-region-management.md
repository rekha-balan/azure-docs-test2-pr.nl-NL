---
title: Region management in Azure Stack | Microsoft Docs
description: Overview of region management in Azure Stack.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: e94775d5-d473-4c03-9f4e-ae2eada67c6c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/05/2018
ms.author: brenduns
ms.reviewer: efemmano
ms.openlocfilehash: 0286ed9c7b3fe320b936d33fe3beaddccd6ac0fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44825890"
---
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="b907f-103">Region management in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b907f-103">Region management in Azure Stack</span></span>

<span data-ttu-id="b907f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="b907f-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="b907f-105">Azure Stack uses the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b907f-105">Azure Stack uses the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure.</span></span> <span data-ttu-id="b907f-106">Inside Region management, you can find all resources that are required to successfully operate the Azure Stack infrastructure.</span><span class="sxs-lookup"><span data-stu-id="b907f-106">Inside Region management, you can find all resources that are required to successfully operate the Azure Stack infrastructure.</span></span>

<span data-ttu-id="b907f-107">One integrated system deployment (referred to as an *Azure Stack cloud*) makes up a single region.</span><span class="sxs-lookup"><span data-stu-id="b907f-107">One integrated system deployment (referred to as an *Azure Stack cloud*) makes up a single region.</span></span> <span data-ttu-id="b907f-108">Each Azure Stack Development Kit has one region, named **local**.</span><span class="sxs-lookup"><span data-stu-id="b907f-108">Each Azure Stack Development Kit has one region, named **local**.</span></span> <span data-ttu-id="b907f-109">If you deploy a second Azure Stack integrated system, or you set up another instance of the development kit on separate hardware, this Azure Stack cloud is a different region.</span><span class="sxs-lookup"><span data-stu-id="b907f-109">If you deploy a second Azure Stack integrated system, or you set up another instance of the development kit on separate hardware, this Azure Stack cloud is a different region.</span></span>

## <a name="information-available-through-the-region-management-tile"></a><span data-ttu-id="b907f-110">Information available through the Region management tile</span><span class="sxs-lookup"><span data-stu-id="b907f-110">Information available through the Region management tile</span></span>

<span data-ttu-id="b907f-111">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span><span class="sxs-lookup"><span data-stu-id="b907f-111">Azure Stack has a set of region management capabilities available in the **Region management** tile.</span></span> <span data-ttu-id="b907f-112">This tile is available to an Azure Stack operator on the default dashboard in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="b907f-112">This tile is available to an Azure Stack operator on the default dashboard in the administrator portal.</span></span> <span data-ttu-id="b907f-113">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span><span class="sxs-lookup"><span data-stu-id="b907f-113">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![The region management tile](media/azure-stack-manage-region/image1.png)

 <span data-ttu-id="b907f-115">If you click a region in the Region management tile, you can access the following information:</span><span class="sxs-lookup"><span data-stu-id="b907f-115">If you click a region in the Region management tile, you can access the following information:</span></span>

  ![Description of panes on the Region management blade](media/azure-stack-manage-region/image2.png)

1. <span data-ttu-id="b907f-117">**The resource menu**.</span><span class="sxs-lookup"><span data-stu-id="b907f-117">**The resource menu**.</span></span> <span data-ttu-id="b907f-118">Here, you can access specific infrastructure management areas, and view and manage user resources such as storage accounts and virtual networks.</span><span class="sxs-lookup"><span data-stu-id="b907f-118">Here, you can access specific infrastructure management areas, and view and manage user resources such as storage accounts and virtual networks.</span></span>

2. <span data-ttu-id="b907f-119">**Alerts**.</span><span class="sxs-lookup"><span data-stu-id="b907f-119">**Alerts**.</span></span> <span data-ttu-id="b907f-120">This lists system-wide alerts and provides details on each of those alerts.</span><span class="sxs-lookup"><span data-stu-id="b907f-120">This lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="b907f-121">**Updates**.</span><span class="sxs-lookup"><span data-stu-id="b907f-121">**Updates**.</span></span> <span data-ttu-id="b907f-122">Here you can view the current version of your Azure Stack infrastructure, available updates, and the update history.</span><span class="sxs-lookup"><span data-stu-id="b907f-122">Here you can view the current version of your Azure Stack infrastructure, available updates, and the update history.</span></span> <span data-ttu-id="b907f-123">You can also update your integrated system.</span><span class="sxs-lookup"><span data-stu-id="b907f-123">You can also update your integrated system.</span></span>

4. <span data-ttu-id="b907f-124">**Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="b907f-124">**Resource providers**.</span></span> <span data-ttu-id="b907f-125">Resource providers is the place to manage the user functionality offered by the components required to run Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b907f-125">Resource providers is the place to manage the user functionality offered by the components required to run Azure Stack.</span></span> <span data-ttu-id="b907f-126">Each resource provider comes with an administrative experience.</span><span class="sxs-lookup"><span data-stu-id="b907f-126">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="b907f-127">This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="b907f-127">This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.</span></span>

5. <span data-ttu-id="b907f-128">**Infrastructure roles**.</span><span class="sxs-lookup"><span data-stu-id="b907f-128">**Infrastructure roles**.</span></span> <span data-ttu-id="b907f-129">Infrastructure roles are the components necessary to run Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="b907f-129">Infrastructure roles are the components necessary to run Azure Stack.</span></span> <span data-ttu-id="b907f-130">Only the infrastructure roles that report alerts are listed.</span><span class="sxs-lookup"><span data-stu-id="b907f-130">Only the infrastructure roles that report alerts are listed.</span></span> <span data-ttu-id="b907f-131">By selecting a role, you can view the alerts associated with the role and the role instances where this role is running.</span><span class="sxs-lookup"><span data-stu-id="b907f-131">By selecting a role, you can view the alerts associated with the role and the role instances where this role is running.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b907f-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="b907f-132">Next steps</span></span>

- [<span data-ttu-id="b907f-133">Monitor health and alerts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b907f-133">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)
- [<span data-ttu-id="b907f-134">Manage updates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b907f-134">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)
