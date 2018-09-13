---
title: Choosing capacity for your QnA Maker deployment - Microsoft Cognitive Services | Microsoft Docs
titleSuffix: Azure
description: a guide to choosing capacity for your QnA Maker deployment
services: cognitive-services
author: nstulasi
manager: sangitap
ms.service: cognitive-services
ms.component: QnAMaker
ms.topic: article
ms.date: 05/07/2018
ms.author: saneppal
ms.openlocfilehash: b0219b9f7dbbee52406dab9d808134fa2e2a689d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864557"
---
# <a name="choosing-capacity-for-your-qna-maker-deployment"></a><span data-ttu-id="a3d8f-103">Choosing capacity for your QnA Maker deployment</span><span class="sxs-lookup"><span data-stu-id="a3d8f-103">Choosing capacity for your QnA Maker deployment</span></span>

<span data-ttu-id="a3d8f-104">The QnA Maker service, takes a dependency on three Azure resources:</span><span class="sxs-lookup"><span data-stu-id="a3d8f-104">The QnA Maker service, takes a dependency on three Azure resources:</span></span>
1.  <span data-ttu-id="a3d8f-105">App Service (for the runtime)</span><span class="sxs-lookup"><span data-stu-id="a3d8f-105">App Service (for the runtime)</span></span>
2.  <span data-ttu-id="a3d8f-106">Azure Search (for storing QnAs)</span><span class="sxs-lookup"><span data-stu-id="a3d8f-106">Azure Search (for storing QnAs)</span></span>
3.  <span data-ttu-id="a3d8f-107">App Insights (optional, for storing chatlogs and telemetry)</span><span class="sxs-lookup"><span data-stu-id="a3d8f-107">App Insights (optional, for storing chatlogs and telemetry)</span></span>

<span data-ttu-id="a3d8f-108">Before you create your QnA Maker service, you should decide which tiers of the above services is appropriate for you.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-108">Before you create your QnA Maker service, you should decide which tiers of the above services is appropriate for you.</span></span> 

<span data-ttu-id="a3d8f-109">Typically there are three parameters you need to consider:</span><span class="sxs-lookup"><span data-stu-id="a3d8f-109">Typically there are three parameters you need to consider:</span></span>
1. <span data-ttu-id="a3d8f-110">**The throughput you need from the service**: Select the appropriate [App Plan](https://azure.microsoft.com/en-in/pricing/details/app-service/plans/) for your App service based on your needs.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-110">**The throughput you need from the service**: Select the appropriate [App Plan](https://azure.microsoft.com/en-in/pricing/details/app-service/plans/) for your App service based on your needs.</span></span> <span data-ttu-id="a3d8f-111">You can [scale up](https://docs.microsoft.com/en-us/azure/app-service/web-sites-scale) or down the App.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-111">You can [scale up](https://docs.microsoft.com/en-us/azure/app-service/web-sites-scale) or down the App.</span></span> <span data-ttu-id="a3d8f-112">This should also influence your Azure Search SKU selection, see more details [here](https://docs.microsoft.com/en-us/azure/search/search-sku-tier).</span><span class="sxs-lookup"><span data-stu-id="a3d8f-112">This should also influence your Azure Search SKU selection, see more details [here](https://docs.microsoft.com/en-us/azure/search/search-sku-tier).</span></span>

2. <span data-ttu-id="a3d8f-113">**Size and the number of knowledge bases**: Choose the appropriate [Azure search SKU](https://azure.microsoft.com/en-in/pricing/details/search/) for your scenario.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-113">**Size and the number of knowledge bases**: Choose the appropriate [Azure search SKU](https://azure.microsoft.com/en-in/pricing/details/search/) for your scenario.</span></span> <span data-ttu-id="a3d8f-114">You can publish N-1 knowledge bases in a particular tier, where N is the maximum indexes allowed in the tier.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-114">You can publish N-1 knowledge bases in a particular tier, where N is the maximum indexes allowed in the tier.</span></span> <span data-ttu-id="a3d8f-115">Also check the maximum size and the number of documents allowed per tier.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-115">Also check the maximum size and the number of documents allowed per tier.</span></span>

3. <span data-ttu-id="a3d8f-116">**Number of documents as sources**: The free SKU of the QnA Maker management service limits the number of documents you can manage via the portal and the APIs to 3 (of 1MB size each).</span><span class="sxs-lookup"><span data-stu-id="a3d8f-116">**Number of documents as sources**: The free SKU of the QnA Maker management service limits the number of documents you can manage via the portal and the APIs to 3 (of 1MB size each).</span></span> <span data-ttu-id="a3d8f-117">The standard SKU has no limits to the number of documents you can manage.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-117">The standard SKU has no limits to the number of documents you can manage.</span></span> <span data-ttu-id="a3d8f-118">See more details [here](https://aka.ms/qnamaker-pricing).</span><span class="sxs-lookup"><span data-stu-id="a3d8f-118">See more details [here](https://aka.ms/qnamaker-pricing).</span></span>

<span data-ttu-id="a3d8f-119">The following table gives you some high-level guidelines.</span><span class="sxs-lookup"><span data-stu-id="a3d8f-119">The following table gives you some high-level guidelines.</span></span>

|                        | <span data-ttu-id="a3d8f-120">QnA Maker Management</span><span class="sxs-lookup"><span data-stu-id="a3d8f-120">QnA Maker Management</span></span> | <span data-ttu-id="a3d8f-121">App Service</span><span class="sxs-lookup"><span data-stu-id="a3d8f-121">App Service</span></span> | <span data-ttu-id="a3d8f-122">Azure Search</span><span class="sxs-lookup"><span data-stu-id="a3d8f-122">Azure Search</span></span> | <span data-ttu-id="a3d8f-123">Limitations</span><span class="sxs-lookup"><span data-stu-id="a3d8f-123">Limitations</span></span>                      |
| ---------------------- | -------------------- | ----------- | ------------ | -------------------------------- |
| <span data-ttu-id="a3d8f-124">Experimentation</span><span class="sxs-lookup"><span data-stu-id="a3d8f-124">Experimentation</span></span>        | <span data-ttu-id="a3d8f-125">Free SKU</span><span class="sxs-lookup"><span data-stu-id="a3d8f-125">Free SKU</span></span>             | <span data-ttu-id="a3d8f-126">Free Tier</span><span class="sxs-lookup"><span data-stu-id="a3d8f-126">Free Tier</span></span>   | <span data-ttu-id="a3d8f-127">Free Tier</span><span class="sxs-lookup"><span data-stu-id="a3d8f-127">Free Tier</span></span>    | <span data-ttu-id="a3d8f-128">Publish Up to 2 KBs, 50 MB size</span><span class="sxs-lookup"><span data-stu-id="a3d8f-128">Publish Up to 2 KBs, 50 MB size</span></span>  |
| <span data-ttu-id="a3d8f-129">Dev/Test Environment</span><span class="sxs-lookup"><span data-stu-id="a3d8f-129">Dev/Test Environment</span></span>   | <span data-ttu-id="a3d8f-130">Standard SKU</span><span class="sxs-lookup"><span data-stu-id="a3d8f-130">Standard SKU</span></span>         | <span data-ttu-id="a3d8f-131">Shared</span><span class="sxs-lookup"><span data-stu-id="a3d8f-131">Shared</span></span>      | <span data-ttu-id="a3d8f-132">Basic</span><span class="sxs-lookup"><span data-stu-id="a3d8f-132">Basic</span></span>        | <span data-ttu-id="a3d8f-133">Publish Up to 4 KBs, 2GB size</span><span class="sxs-lookup"><span data-stu-id="a3d8f-133">Publish Up to 4 KBs, 2GB size</span></span>    |
| <span data-ttu-id="a3d8f-134">Production Environment</span><span class="sxs-lookup"><span data-stu-id="a3d8f-134">Production Environment</span></span> | <span data-ttu-id="a3d8f-135">Standard SKU</span><span class="sxs-lookup"><span data-stu-id="a3d8f-135">Standard SKU</span></span>         | <span data-ttu-id="a3d8f-136">Basic</span><span class="sxs-lookup"><span data-stu-id="a3d8f-136">Basic</span></span>       | <span data-ttu-id="a3d8f-137">Standard</span><span class="sxs-lookup"><span data-stu-id="a3d8f-137">Standard</span></span>     | <span data-ttu-id="a3d8f-138">Publish Up to 49 KBs, 25 GB size</span><span class="sxs-lookup"><span data-stu-id="a3d8f-138">Publish Up to 49 KBs, 25 GB size</span></span> |

<span data-ttu-id="a3d8f-139">For upgrading your QnA Maker stack, see [Upgrade your QnA Maker service](../How-To/upgrade-qnamaker-service.md).</span><span class="sxs-lookup"><span data-stu-id="a3d8f-139">For upgrading your QnA Maker stack, see [Upgrade your QnA Maker service](../How-To/upgrade-qnamaker-service.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d8f-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3d8f-140">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a3d8f-141">Upgrade your QnA Maker service</span><span class="sxs-lookup"><span data-stu-id="a3d8f-141">Upgrade your QnA Maker service</span></span>](../How-To/upgrade-qnamaker-service.md)
