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
# <a name="region-management-in-azure-stack"></a><span data-ttu-id="88dbe-103">Region management in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="88dbe-103">Region management in Azure Stack</span></span>
<span data-ttu-id="88dbe-104">Azure Stack has the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure.</span><span class="sxs-lookup"><span data-stu-id="88dbe-104">Azure Stack has the concept of regions, which are logical entities comprised of the hardware resources that make up the Azure Stack infrastructure.</span></span> <span data-ttu-id="88dbe-105">Inside Region Management, you can find all resources that are required to successfully operate the Azure Stack infrastructure lifecycle.</span><span class="sxs-lookup"><span data-stu-id="88dbe-105">Inside Region Management, you can find all resources that are required to successfully operate the Azure Stack infrastructure lifecycle.</span></span>

<span data-ttu-id="88dbe-106">The Azure Stack Proof of Concept (POC) is a single-node deployment, and equals one region.</span><span class="sxs-lookup"><span data-stu-id="88dbe-106">The Azure Stack Proof of Concept (POC) is a single-node deployment, and equals one region.</span></span> <span data-ttu-id="88dbe-107">If you set up another instance of Azure Stack POC on separate hardware, this instance is a different region.</span><span class="sxs-lookup"><span data-stu-id="88dbe-107">If you set up another instance of Azure Stack POC on separate hardware, this instance is a different region.</span></span>

## <a name="information-available-through-the-region-management-tile"></a><span data-ttu-id="88dbe-108">Information available through the Region Management tile</span><span class="sxs-lookup"><span data-stu-id="88dbe-108">Information available through the Region Management tile</span></span>
<span data-ttu-id="88dbe-109">This preview release of Azure Stack has a set of region management capabilities available in the **Region Management** tile.</span><span class="sxs-lookup"><span data-stu-id="88dbe-109">This preview release of Azure Stack has a set of region management capabilities available in the **Region Management** tile.</span></span> <span data-ttu-id="88dbe-110">This tile is available to a cloud administrator on the default dashboard in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="88dbe-110">This tile is available to a cloud administrator on the default dashboard in the administrator portal.</span></span> <span data-ttu-id="88dbe-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span><span class="sxs-lookup"><span data-stu-id="88dbe-111">Through this tile, you can monitor and update your Azure Stack region and its components, which are region-specific.</span></span>

 ![The region management tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-region/Image1.png)

 <span data-ttu-id="88dbe-113">If you click a region in the Region Management tile, you can access the following information:</span><span class="sxs-lookup"><span data-stu-id="88dbe-113">If you click a region in the Region Management tile, you can access the following information:</span></span>

  ![Description of panes on the Region Management blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-region/image2.PNG)

1. <span data-ttu-id="88dbe-115">**The resource menu**.</span><span class="sxs-lookup"><span data-stu-id="88dbe-115">**The resource menu**.</span></span> <span data-ttu-id="88dbe-116">Here, you can access specific infrastructure management areas, view and manage tenant resources such as storage accounts and virtual networks, and find links to Azure Stack-related documentation (through **Quick start**).</span><span class="sxs-lookup"><span data-stu-id="88dbe-116">Here, you can access specific infrastructure management areas, view and manage tenant resources such as storage accounts and virtual networks, and find links to Azure Stack-related documentation (through **Quick start**).</span></span>

2. <span data-ttu-id="88dbe-117">**Alerts**.</span><span class="sxs-lookup"><span data-stu-id="88dbe-117">**Alerts**.</span></span> <span data-ttu-id="88dbe-118">This tile lists system-wide alerts and provides details on each of those alerts.</span><span class="sxs-lookup"><span data-stu-id="88dbe-118">This tile lists system-wide alerts and provides details on each of those alerts.</span></span>

3. <span data-ttu-id="88dbe-119">**Updates**.</span><span class="sxs-lookup"><span data-stu-id="88dbe-119">**Updates**.</span></span> <span data-ttu-id="88dbe-120">In this tile, you can view the update status of your Azure Stack infrastructure, including version, update availability, and updates history.</span><span class="sxs-lookup"><span data-stu-id="88dbe-120">In this tile, you can view the update status of your Azure Stack infrastructure, including version, update availability, and updates history.</span></span>

4. <span data-ttu-id="88dbe-121">**Resource providers**.</span><span class="sxs-lookup"><span data-stu-id="88dbe-121">**Resource providers**.</span></span> <span data-ttu-id="88dbe-122">Resource providers is the place to manage the tenant functionality offered by the components required to run Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="88dbe-122">Resource providers is the place to manage the tenant functionality offered by the components required to run Azure Stack.</span></span> <span data-ttu-id="88dbe-123">Each resource provider comes with an administrative experience.</span><span class="sxs-lookup"><span data-stu-id="88dbe-123">Each resource provider comes with an administrative experience.</span></span> <span data-ttu-id="88dbe-124">This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.</span><span class="sxs-lookup"><span data-stu-id="88dbe-124">This experience can include alerts for the specific provider, metrics, and other management capabilities specific to the resource provider.</span></span>
 
   >[!NOTE]
   <span data-ttu-id="88dbe-125">In Azure Stack Technical Preview 3, only Storage, Compute, and Network resource providers offer an associated administrative experience.</span><span class="sxs-lookup"><span data-stu-id="88dbe-125">In Azure Stack Technical Preview 3, only Storage, Compute, and Network resource providers offer an associated administrative experience.</span></span>

5. <span data-ttu-id="88dbe-126">**Infrastructure roles**.</span><span class="sxs-lookup"><span data-stu-id="88dbe-126">**Infrastructure roles**.</span></span> <span data-ttu-id="88dbe-127">Infrastructure roles are the components necessary to run Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="88dbe-127">Infrastructure roles are the components necessary to run Azure Stack.</span></span> <span data-ttu-id="88dbe-128">By clicking a role, you can view the alerts associated with the specific role and the role instances where this role is running.</span><span class="sxs-lookup"><span data-stu-id="88dbe-128">By clicking a role, you can view the alerts associated with the specific role and the role instances where this role is running.</span></span> <span data-ttu-id="88dbe-129">Starting in Technical Preview 3, you can start, restart, or shut down an infrastructure role instance.</span><span class="sxs-lookup"><span data-stu-id="88dbe-129">Starting in Technical Preview 3, you can start, restart, or shut down an infrastructure role instance.</span></span>

   >[!NOTE]
   <span data-ttu-id="88dbe-130">In Azure Stack Technical Preview 3, not all infrastructure roles surface alerts in this journey.</span><span class="sxs-lookup"><span data-stu-id="88dbe-130">In Azure Stack Technical Preview 3, not all infrastructure roles surface alerts in this journey.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88dbe-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="88dbe-131">Next steps</span></span>
[<span data-ttu-id="88dbe-132">Monitor health and alerts in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="88dbe-132">Monitor health and alerts in Azure Stack</span></span>](azure-stack-monitor-health.md)

[<span data-ttu-id="88dbe-133">Manage updates in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="88dbe-133">Manage updates in Azure Stack</span></span>](azure-stack-updates.md)








