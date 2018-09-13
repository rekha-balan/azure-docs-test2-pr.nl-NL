---
title: Quotas and limitations in Azure Media Services v3 | Microsoft Docs
description: This topic describes quotas and limitations in Azure Media Services v3
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 08/26/2018
ms.author: juliako
ms.openlocfilehash: 49b834325ce819f20978e06d85ee308955510ac1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866073"
---
# <a name="quotas-and-limitations-in-azure-media-services-v3"></a><span data-ttu-id="b179f-103">Quotas and limitations in Azure Media Services v3</span><span class="sxs-lookup"><span data-stu-id="b179f-103">Quotas and limitations in Azure Media Services v3</span></span>

<span data-ttu-id="b179f-104">This article describes quotas and limitations in Azure Media Services v3.</span><span class="sxs-lookup"><span data-stu-id="b179f-104">This article describes quotas and limitations in Azure Media Services v3.</span></span>

| <span data-ttu-id="b179f-105">Resource</span><span class="sxs-lookup"><span data-stu-id="b179f-105">Resource</span></span> | <span data-ttu-id="b179f-106">Default Limit</span><span class="sxs-lookup"><span data-stu-id="b179f-106">Default Limit</span></span> | 
| --- | --- | 
| <span data-ttu-id="b179f-107">Assets per Azure Media Services account</span><span class="sxs-lookup"><span data-stu-id="b179f-107">Assets per Azure Media Services account</span></span> | <span data-ttu-id="b179f-108">1,000,000</span><span class="sxs-lookup"><span data-stu-id="b179f-108">1,000,000</span></span>|
| <span data-ttu-id="b179f-109">Dynamic Manifest Filters</span><span class="sxs-lookup"><span data-stu-id="b179f-109">Dynamic Manifest Filters</span></span>|<span data-ttu-id="b179f-110">100</span><span class="sxs-lookup"><span data-stu-id="b179f-110">100</span></span>|
| <span data-ttu-id="b179f-111">JobInputs per Job</span><span class="sxs-lookup"><span data-stu-id="b179f-111">JobInputs per Job</span></span> | <span data-ttu-id="b179f-112">50  (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-112">50  (fixed)</span></span>|
| <span data-ttu-id="b179f-113">JobOutputs per Job/TransformOutputs in a Transform</span><span class="sxs-lookup"><span data-stu-id="b179f-113">JobOutputs per Job/TransformOutputs in a Transform</span></span> | <span data-ttu-id="b179f-114">20 (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-114">20 (fixed)</span></span> |
| <span data-ttu-id="b179f-115">Files per JobInput</span><span class="sxs-lookup"><span data-stu-id="b179f-115">Files per JobInput</span></span>|<span data-ttu-id="b179f-116">10 (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-116">10 (fixed)</span></span>|
| <span data-ttu-id="b179f-117">File size</span><span class="sxs-lookup"><span data-stu-id="b179f-117">File size</span></span>| <span data-ttu-id="b179f-118">In some scenarios, there is a limit on the maximum file size supported for processing in Media Services.</span><span class="sxs-lookup"><span data-stu-id="b179f-118">In some scenarios, there is a limit on the maximum file size supported for processing in Media Services.</span></span> <span data-ttu-id="b179f-119"><sup>(1)</sup></span><span class="sxs-lookup"><span data-stu-id="b179f-119"><sup>(1)</sup></span></span> |
| <span data-ttu-id="b179f-120">Jobs per Media Services account</span><span class="sxs-lookup"><span data-stu-id="b179f-120">Jobs per Media Services account</span></span> | <span data-ttu-id="b179f-121">500,000 <sup>(2)</sup> (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-121">500,000 <sup>(2)</sup> (fixed)</span></span>|
| <span data-ttu-id="b179f-122">Listing Transforms</span><span class="sxs-lookup"><span data-stu-id="b179f-122">Listing Transforms</span></span>|<span data-ttu-id="b179f-123">Paginate the response, with 1000 Transforms per page</span><span class="sxs-lookup"><span data-stu-id="b179f-123">Paginate the response, with 1000 Transforms per page</span></span>|
| <span data-ttu-id="b179f-124">Listing Jobs</span><span class="sxs-lookup"><span data-stu-id="b179f-124">Listing Jobs</span></span>|<span data-ttu-id="b179f-125">Paginate the response, with 500 Jobs per page</span><span class="sxs-lookup"><span data-stu-id="b179f-125">Paginate the response, with 500 Jobs per page</span></span>|
| <span data-ttu-id="b179f-126">LiveEvents per Media Services account</span><span class="sxs-lookup"><span data-stu-id="b179f-126">LiveEvents per Media Services account</span></span> |<span data-ttu-id="b179f-127">5</span><span class="sxs-lookup"><span data-stu-id="b179f-127">5</span></span>|
| <span data-ttu-id="b179f-128">Media Services accounts in a single subscription</span><span class="sxs-lookup"><span data-stu-id="b179f-128">Media Services accounts in a single subscription</span></span> | <span data-ttu-id="b179f-129">25 (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-129">25 (fixed)</span></span> |
| <span data-ttu-id="b179f-130">LiveOutputs in running state per LiveEvent</span><span class="sxs-lookup"><span data-stu-id="b179f-130">LiveOutputs in running state per LiveEvent</span></span> |<span data-ttu-id="b179f-131">3</span><span class="sxs-lookup"><span data-stu-id="b179f-131">3</span></span>|
| <span data-ttu-id="b179f-132">Storage accounts</span><span class="sxs-lookup"><span data-stu-id="b179f-132">Storage accounts</span></span> | <span data-ttu-id="b179f-133">100<sup>(4)</sup> (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-133">100<sup>(4)</sup> (fixed)</span></span> |
| <span data-ttu-id="b179f-134">Streaming Endpoints in running state per Media Services account</span><span class="sxs-lookup"><span data-stu-id="b179f-134">Streaming Endpoints in running state per Media Services account</span></span>|<span data-ttu-id="b179f-135">2</span><span class="sxs-lookup"><span data-stu-id="b179f-135">2</span></span>|
| <span data-ttu-id="b179f-136">StreamingPolicies</span><span class="sxs-lookup"><span data-stu-id="b179f-136">StreamingPolicies</span></span> | <span data-ttu-id="b179f-137">100 <sup>(3)</sup></span><span class="sxs-lookup"><span data-stu-id="b179f-137">100 <sup>(3)</sup></span></span> |
| <span data-ttu-id="b179f-138">Transforms per Media Services account</span><span class="sxs-lookup"><span data-stu-id="b179f-138">Transforms per Media Services account</span></span> | <span data-ttu-id="b179f-139">100  (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-139">100  (fixed)</span></span>|
| <span data-ttu-id="b179f-140">Unique StreamingLocators associated with an Asset at one time</span><span class="sxs-lookup"><span data-stu-id="b179f-140">Unique StreamingLocators associated with an Asset at one time</span></span> | <span data-ttu-id="b179f-141">100<sup>(5)</sup> (fixed)</span><span class="sxs-lookup"><span data-stu-id="b179f-141">100<sup>(5)</sup> (fixed)</span></span> |

<span data-ttu-id="b179f-142"><sup>1</sup> The maximum size supported for a single blob is currently up to 5 TB in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="b179f-142"><sup>1</sup> The maximum size supported for a single blob is currently up to 5 TB in Azure Blob Storage.</span></span> <span data-ttu-id="b179f-143">However, additional limits apply in Azure Media Services based on the VM sizes that are used by the service.</span><span class="sxs-lookup"><span data-stu-id="b179f-143">However, additional limits apply in Azure Media Services based on the VM sizes that are used by the service.</span></span> <span data-ttu-id="b179f-144">If your source file is larger than 260-GB, your Job will likely fail.</span><span class="sxs-lookup"><span data-stu-id="b179f-144">If your source file is larger than 260-GB, your Job will likely fail.</span></span> <span data-ttu-id="b179f-145">If you have 4K content that is larger than 260-GB limit, contact us at amshelp@microsoft.com for potential mitigations to support your scenario.</span><span class="sxs-lookup"><span data-stu-id="b179f-145">If you have 4K content that is larger than 260-GB limit, contact us at amshelp@microsoft.com for potential mitigations to support your scenario.</span></span>

<span data-ttu-id="b179f-146"><sup>2</sup> This number includes queued, finished, active, and canceled Jobs.</span><span class="sxs-lookup"><span data-stu-id="b179f-146"><sup>2</sup> This number includes queued, finished, active, and canceled Jobs.</span></span> <span data-ttu-id="b179f-147">It does not include deleted Jobs.</span><span class="sxs-lookup"><span data-stu-id="b179f-147">It does not include deleted Jobs.</span></span> 

<span data-ttu-id="b179f-148">Any Job record in your account older than 90 days will be automatically deleted, even if the total number of records is below the maximum quota.</span><span class="sxs-lookup"><span data-stu-id="b179f-148">Any Job record in your account older than 90 days will be automatically deleted, even if the total number of records is below the maximum quota.</span></span> 

<span data-ttu-id="b179f-149"><sup>3</sup> When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span><span class="sxs-lookup"><span data-stu-id="b179f-149"><sup>3</sup> When using a custom [StreamingPolicy](https://docs.microsoft.com/rest/api/media/streamingpolicies), you should design a limited set of such policies for your Media Service account, and re-use them for your StreamingLocators whenever the same encryption options and protocols are needed.</span></span> <span data-ttu-id="b179f-150">You should not be creating a new StreamingPolicy for each StreamingLocator.</span><span class="sxs-lookup"><span data-stu-id="b179f-150">You should not be creating a new StreamingPolicy for each StreamingLocator.</span></span>

<span data-ttu-id="b179f-151"><sup>4</sup> The storage accounts must be from the same Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b179f-151"><sup>4</sup> The storage accounts must be from the same Azure subscription.</span></span>

<span data-ttu-id="b179f-152"><sup>5</sup> StreamingLocators are not designed for managing per-user access control.</span><span class="sxs-lookup"><span data-stu-id="b179f-152"><sup>5</sup> StreamingLocators are not designed for managing per-user access control.</span></span> <span data-ttu-id="b179f-153">To give different access rights to individual users, use Digital Rights Management (DRM) solutions.</span><span class="sxs-lookup"><span data-stu-id="b179f-153">To give different access rights to individual users, use Digital Rights Management (DRM) solutions.</span></span>

## <a name="support-ticket"></a><span data-ttu-id="b179f-154">Support ticket</span><span class="sxs-lookup"><span data-stu-id="b179f-154">Support ticket</span></span>

<span data-ttu-id="b179f-155">For resources that are not fixed, you may ask for the quotas to be raised, by opening a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).</span><span class="sxs-lookup"><span data-stu-id="b179f-155">For resources that are not fixed, you may ask for the quotas to be raised, by opening a [support ticket](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest).</span></span> <span data-ttu-id="b179f-156">Include detailed information in the request on the desired quota changes, use-case scenarios, and regions required.</span><span class="sxs-lookup"><span data-stu-id="b179f-156">Include detailed information in the request on the desired quota changes, use-case scenarios, and regions required.</span></span> <br/><span data-ttu-id="b179f-157">Do **not** create additional Azure Media Services accounts in an attempt to obtain higher limits.</span><span class="sxs-lookup"><span data-stu-id="b179f-157">Do **not** create additional Azure Media Services accounts in an attempt to obtain higher limits.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b179f-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="b179f-158">Next steps</span></span>

[<span data-ttu-id="b179f-159">Overview</span><span class="sxs-lookup"><span data-stu-id="b179f-159">Overview</span></span>](media-services-overview.md)
