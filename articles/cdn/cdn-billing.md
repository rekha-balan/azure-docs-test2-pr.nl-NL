---
title: Understanding Azure CDN billing | Microsoft Docs
description: This FAQ describes how Azure CDN billing works.
services: cdn
documentationcenter: ''
author: dksimpson
manager: akucer
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2018
ms.author: v-deasim
ms.openlocfilehash: 218c493c772dc8fd212efaf60a0599fa2e896411
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866796"
---
# <a name="understanding-azure-cdn-billing"></a><span data-ttu-id="0f6b6-103">Understanding Azure CDN billing</span><span class="sxs-lookup"><span data-stu-id="0f6b6-103">Understanding Azure CDN billing</span></span>

<span data-ttu-id="0f6b6-104">This FAQ describes the billing structure for content hosted by Azure Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="0f6b6-104">This FAQ describes the billing structure for content hosted by Azure Content Delivery Network (CDN).</span></span>

## <a name="what-is-a-billing-region"></a><span data-ttu-id="0f6b6-105">What is a billing region?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-105">What is a billing region?</span></span>
<span data-ttu-id="0f6b6-106">A billing region is a geographic area used to determine what rate is charged for delivery of objects from Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-106">A billing region is a geographic area used to determine what rate is charged for delivery of objects from Azure CDN.</span></span> <span data-ttu-id="0f6b6-107">The current billing zones and their regions are as follows:</span><span class="sxs-lookup"><span data-stu-id="0f6b6-107">The current billing zones and their regions are as follows:</span></span>

- <span data-ttu-id="0f6b6-108">Zone 1: North America, Europe, Middle East, and Africa</span><span class="sxs-lookup"><span data-stu-id="0f6b6-108">Zone 1: North America, Europe, Middle East, and Africa</span></span>

- <span data-ttu-id="0f6b6-109">Zone 2: Asia Pacific (including Japan)</span><span class="sxs-lookup"><span data-stu-id="0f6b6-109">Zone 2: Asia Pacific (including Japan)</span></span>

- <span data-ttu-id="0f6b6-110">Zone 3: South America</span><span class="sxs-lookup"><span data-stu-id="0f6b6-110">Zone 3: South America</span></span>

- <span data-ttu-id="0f6b6-111">Zone 4: Australia and New Zealand</span><span class="sxs-lookup"><span data-stu-id="0f6b6-111">Zone 4: Australia and New Zealand</span></span>

- <span data-ttu-id="0f6b6-112">Zone 5: India</span><span class="sxs-lookup"><span data-stu-id="0f6b6-112">Zone 5: India</span></span>

<span data-ttu-id="0f6b6-113">For information about point-of-presence (POP) regions, see [Azure CDN POP locations by region](https://docs.microsoft.com/azure/cdn/cdn-pop-locations).</span><span class="sxs-lookup"><span data-stu-id="0f6b6-113">For information about point-of-presence (POP) regions, see [Azure CDN POP locations by region](https://docs.microsoft.com/azure/cdn/cdn-pop-locations).</span></span> <span data-ttu-id="0f6b6-114">For example, a POP located in Mexico is in the North America region and is therefore included in zone 1.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-114">For example, a POP located in Mexico is in the North America region and is therefore included in zone 1.</span></span> 

<span data-ttu-id="0f6b6-115">For information about Azure CDN pricing, see [Content Delivery Network pricing](https://azure.microsoft.com/is-is/pricing/details/cdn/).</span><span class="sxs-lookup"><span data-stu-id="0f6b6-115">For information about Azure CDN pricing, see [Content Delivery Network pricing](https://azure.microsoft.com/is-is/pricing/details/cdn/).</span></span>

## <a name="how-are-delivery-charges-calculated-by-region"></a><span data-ttu-id="0f6b6-116">How are delivery charges calculated by region?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-116">How are delivery charges calculated by region?</span></span>
<span data-ttu-id="0f6b6-117">The Azure CDN billing region is based on the location of the source server delivering the content to the end user.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-117">The Azure CDN billing region is based on the location of the source server delivering the content to the end user.</span></span> <span data-ttu-id="0f6b6-118">The destination (physical location) of the client is not considered the billing region.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-118">The destination (physical location) of the client is not considered the billing region.</span></span>

<span data-ttu-id="0f6b6-119">For example, if a user located in Mexico issues a request and this request is serviced by a server located in a United States POP due to peering or traffic conditions, the billing region will be the United States.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-119">For example, if a user located in Mexico issues a request and this request is serviced by a server located in a United States POP due to peering or traffic conditions, the billing region will be the United States.</span></span>

## <a name="what-is-a-billable-azure-cdn-transaction"></a><span data-ttu-id="0f6b6-120">What is a billable Azure CDN transaction?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-120">What is a billable Azure CDN transaction?</span></span>
<span data-ttu-id="0f6b6-121">Any HTTP(S) request that terminates at the CDN is a billable event, which includes all response types: success, failure, or other.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-121">Any HTTP(S) request that terminates at the CDN is a billable event, which includes all response types: success, failure, or other.</span></span> <span data-ttu-id="0f6b6-122">However, different responses may generate different traffic amounts.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-122">However, different responses may generate different traffic amounts.</span></span> <span data-ttu-id="0f6b6-123">For example, *304 Not Modified* and other header-only responses generate little traffic because they are a small header response; similarly, error responses (for example, *404 Not Found*) are billable but incur a small cost because of the tiny response payload.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-123">For example, *304 Not Modified* and other header-only responses generate little traffic because they are a small header response; similarly, error responses (for example, *404 Not Found*) are billable but incur a small cost because of the tiny response payload.</span></span>

## <a name="what-other-azure-costs-are-associated-with-azure-cdn-use"></a><span data-ttu-id="0f6b6-124">What other Azure costs are associated with Azure CDN use?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-124">What other Azure costs are associated with Azure CDN use?</span></span>
<span data-ttu-id="0f6b6-125">Using Azure CDN also incurs some usage charges on the services used as the origin for your objects.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-125">Using Azure CDN also incurs some usage charges on the services used as the origin for your objects.</span></span> <span data-ttu-id="0f6b6-126">These costs are typically a small fraction of the overall CDN usage cost.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-126">These costs are typically a small fraction of the overall CDN usage cost.</span></span>

<span data-ttu-id="0f6b6-127">If you are using Azure Blob storage as the origin for your content, you also incur the following storage charges for cache fills:</span><span class="sxs-lookup"><span data-stu-id="0f6b6-127">If you are using Azure Blob storage as the origin for your content, you also incur the following storage charges for cache fills:</span></span>

- <span data-ttu-id="0f6b6-128">Actual GB used: The actual storage of your source objects.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-128">Actual GB used: The actual storage of your source objects.</span></span>

- <span data-ttu-id="0f6b6-129">Transfers in GB: The amount of data transferred to fill the CDN caches.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-129">Transfers in GB: The amount of data transferred to fill the CDN caches.</span></span>

- <span data-ttu-id="0f6b6-130">Transactions: As needed to fill the cache.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-130">Transactions: As needed to fill the cache.</span></span>

<span data-ttu-id="0f6b6-131">For more information about Azure Storage billing, see [Understanding Azure Storage Billing – Bandwidth, Transactions, and Capacity](https://blogs.msdn.microsoft.com/windowsazurestorage/2010/07/08/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity/).</span><span class="sxs-lookup"><span data-stu-id="0f6b6-131">For more information about Azure Storage billing, see [Understanding Azure Storage Billing – Bandwidth, Transactions, and Capacity](https://blogs.msdn.microsoft.com/windowsazurestorage/2010/07/08/understanding-windows-azure-storage-billing-bandwidth-transactions-and-capacity/).</span></span>

<span data-ttu-id="0f6b6-132">If you are using *hosted service delivery*, you will incur charges as follows:</span><span class="sxs-lookup"><span data-stu-id="0f6b6-132">If you are using *hosted service delivery*, you will incur charges as follows:</span></span>

- <span data-ttu-id="0f6b6-133">Azure compute time: The compute instances that act as the origin.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-133">Azure compute time: The compute instances that act as the origin.</span></span>

- <span data-ttu-id="0f6b6-134">Azure compute transfer: The data transfers from the compute instances to fill the Azure CDN caches.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-134">Azure compute transfer: The data transfers from the compute instances to fill the Azure CDN caches.</span></span>

<span data-ttu-id="0f6b6-135">If your client uses byte-range requests (regardless of origin service), the following considerations apply:</span><span class="sxs-lookup"><span data-stu-id="0f6b6-135">If your client uses byte-range requests (regardless of origin service), the following considerations apply:</span></span>

- <span data-ttu-id="0f6b6-136">A *byte-range request* is a billable transaction at the CDN.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-136">A *byte-range request* is a billable transaction at the CDN.</span></span> <span data-ttu-id="0f6b6-137">When a client issues a byte-range request, this request is for a subset (range) of the object.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-137">When a client issues a byte-range request, this request is for a subset (range) of the object.</span></span> <span data-ttu-id="0f6b6-138">The CDN responds with only a partial portion of the content that is requested.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-138">The CDN responds with only a partial portion of the content that is requested.</span></span> <span data-ttu-id="0f6b6-139">This partial response is a billable transaction and the transfer amount is limited to the size of the range response (plus headers).</span><span class="sxs-lookup"><span data-stu-id="0f6b6-139">This partial response is a billable transaction and the transfer amount is limited to the size of the range response (plus headers).</span></span>

- <span data-ttu-id="0f6b6-140">When a request arrives for only part of an object (by specifying a byte-range header), the CDN may fetch the entire object into its cache.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-140">When a request arrives for only part of an object (by specifying a byte-range header), the CDN may fetch the entire object into its cache.</span></span> <span data-ttu-id="0f6b6-141">As a result, even though the billable transaction from the CDN is for a partial response, the billable transaction from the origin may involve the full size of the object.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-141">As a result, even though the billable transaction from the CDN is for a partial response, the billable transaction from the origin may involve the full size of the object.</span></span>

## <a name="how-much-transfer-activity-occurs-to-support-the-cache"></a><span data-ttu-id="0f6b6-142">How much transfer activity occurs to support the cache?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-142">How much transfer activity occurs to support the cache?</span></span>
<span data-ttu-id="0f6b6-143">Each time a CDN POP needs to fill its cache, it makes a request to the origin for the object being cached.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-143">Each time a CDN POP needs to fill its cache, it makes a request to the origin for the object being cached.</span></span> <span data-ttu-id="0f6b6-144">As a result, the origin incurs a billable transaction on every cache miss.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-144">As a result, the origin incurs a billable transaction on every cache miss.</span></span> <span data-ttu-id="0f6b6-145">The number of cache misses depends on a number of factors:</span><span class="sxs-lookup"><span data-stu-id="0f6b6-145">The number of cache misses depends on a number of factors:</span></span>

- <span data-ttu-id="0f6b6-146">How cacheable the content is: If the content has high TTL (time-to-live)/expiration values and is accessed frequently so it stays popular in cache, then the vast majority of the load is handled by the CDN.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-146">How cacheable the content is: If the content has high TTL (time-to-live)/expiration values and is accessed frequently so it stays popular in cache, then the vast majority of the load is handled by the CDN.</span></span> <span data-ttu-id="0f6b6-147">A typical good cache-hit ratio is well over 90%, meaning that less than 10% of client requests have to return to origin, either for a cache miss or object refresh.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-147">A typical good cache-hit ratio is well over 90%, meaning that less than 10% of client requests have to return to origin, either for a cache miss or object refresh.</span></span>

- <span data-ttu-id="0f6b6-148">How many nodes need to load the object: Each time a node loads an object from the origin, it incurs a billable transaction.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-148">How many nodes need to load the object: Each time a node loads an object from the origin, it incurs a billable transaction.</span></span> <span data-ttu-id="0f6b6-149">As a result, more global content (accessed from more nodes) results in more billable transactions.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-149">As a result, more global content (accessed from more nodes) results in more billable transactions.</span></span>

- <span data-ttu-id="0f6b6-150">TTL influence: A higher TTL for an object means it needs to be fetched from the origin less frequently.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-150">TTL influence: A higher TTL for an object means it needs to be fetched from the origin less frequently.</span></span> <span data-ttu-id="0f6b6-151">It also means clients, such as browsers, can cache the object longer, which can reduce the transactions to the CDN.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-151">It also means clients, such as browsers, can cache the object longer, which can reduce the transactions to the CDN.</span></span>

## <a name="how-do-i-manage-my-costs-most-effectively"></a><span data-ttu-id="0f6b6-152">How do I manage my costs most effectively?</span><span class="sxs-lookup"><span data-stu-id="0f6b6-152">How do I manage my costs most effectively?</span></span>
<span data-ttu-id="0f6b6-153">Set the longest TTL possible on your content.</span><span class="sxs-lookup"><span data-stu-id="0f6b6-153">Set the longest TTL possible on your content.</span></span> 
