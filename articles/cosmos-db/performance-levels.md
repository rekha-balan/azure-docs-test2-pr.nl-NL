---
title: Retired Azure Cosmos DB performance levels | Microsoft Docs
description: Learn about the S1, S2, and S3 performance levels previously available in Azure Cosmos DB.
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 06/04/2018
ms.author: sngun
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d1bb7551e6dfb6c42853ab95096f17f5285c69c1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871106"
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels"></a><span data-ttu-id="9bfe4-103">Retiring the S1, S2, and S3 performance levels</span><span class="sxs-lookup"><span data-stu-id="9bfe4-103">Retiring the S1, S2, and S3 performance levels</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="9bfe4-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new Azure Cosmos DB accounts.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new Azure Cosmos DB accounts.</span></span>
>

<span data-ttu-id="9bfe4-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels can be migrated to single partitioned collections.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels can be migrated to single partitioned collections.</span></span> <span data-ttu-id="9bfe4-106">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="9bfe4-107">Why are the S1, S2, and S3 performance levels are being retired?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-107">Why are the S1, S2, and S3 performance levels are being retired?</span></span>](#why-retired)
- [<span data-ttu-id="9bfe4-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="9bfe4-109">What do I need to do to ensure uninterrupted access to my data?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="9bfe4-110">How will my collection change after the migration?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="9bfe4-111">How will my billing change after I’m migrated to single partition collections?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="9bfe4-112">What if I need more than 10 GB of storage?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="9bfe4-113">Can I change between the S1, S2, and S3 performance levels before the planned migration?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-113">Can I change between the S1, S2, and S3 performance levels before the planned migration?</span></span>](#change-before)
- [<span data-ttu-id="9bfe4-114">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-114">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="9bfe4-115">How am I impacted if I'm an EA customer?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-115">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="9bfe4-116">Why are the S1, S2, and S3 performance levels being retired?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-116">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="9bfe4-117">The S1, S2, and S3 performance levels do not offer the flexibility that the standard Azure Cosmos DB offer provides.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-117">The S1, S2, and S3 performance levels do not offer the flexibility that the standard Azure Cosmos DB offer provides.</span></span> <span data-ttu-id="9bfe4-118">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-118">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set and did not offer elasticity.</span></span> <span data-ttu-id="9bfe4-119">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-119">Azure Cosmos DB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="9bfe4-120">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-120">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="9bfe4-121">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-121">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="9bfe4-122">Here is an example for US East 2 region:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-122">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="9bfe4-123">Partitioned collection</span><span class="sxs-lookup"><span data-stu-id="9bfe4-123">Partitioned collection</span></span>|<span data-ttu-id="9bfe4-124">Single partition collection</span><span class="sxs-lookup"><span data-stu-id="9bfe4-124">Single partition collection</span></span>|<span data-ttu-id="9bfe4-125">S1</span><span class="sxs-lookup"><span data-stu-id="9bfe4-125">S1</span></span>|<span data-ttu-id="9bfe4-126">S2</span><span class="sxs-lookup"><span data-stu-id="9bfe4-126">S2</span></span>|<span data-ttu-id="9bfe4-127">S3</span><span class="sxs-lookup"><span data-stu-id="9bfe4-127">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="9bfe4-128">Maximum throughput</span><span class="sxs-lookup"><span data-stu-id="9bfe4-128">Maximum throughput</span></span>|<span data-ttu-id="9bfe4-129">Unlimited</span><span class="sxs-lookup"><span data-stu-id="9bfe4-129">Unlimited</span></span>|<span data-ttu-id="9bfe4-130">10K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-130">10K RU/s</span></span>|<span data-ttu-id="9bfe4-131">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-131">250 RU/s</span></span>|<span data-ttu-id="9bfe4-132">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-132">1 K RU/s</span></span>|<span data-ttu-id="9bfe4-133">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-133">2.5 K RU/s</span></span>|
|<span data-ttu-id="9bfe4-134">Minimum throughput</span><span class="sxs-lookup"><span data-stu-id="9bfe4-134">Minimum throughput</span></span>|<span data-ttu-id="9bfe4-135">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-135">2.5 K RU/s</span></span>|<span data-ttu-id="9bfe4-136">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-136">400 RU/s</span></span>|<span data-ttu-id="9bfe4-137">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-137">250 RU/s</span></span>|<span data-ttu-id="9bfe4-138">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-138">1 K RU/s</span></span>|<span data-ttu-id="9bfe4-139">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-139">2.5 K RU/s</span></span>|
|<span data-ttu-id="9bfe4-140">Maximum storage</span><span class="sxs-lookup"><span data-stu-id="9bfe4-140">Maximum storage</span></span>|<span data-ttu-id="9bfe4-141">Unlimited</span><span class="sxs-lookup"><span data-stu-id="9bfe4-141">Unlimited</span></span>|<span data-ttu-id="9bfe4-142">10 GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-142">10 GB</span></span>|<span data-ttu-id="9bfe4-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-143">10 GB</span></span>|<span data-ttu-id="9bfe4-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-144">10 GB</span></span>|<span data-ttu-id="9bfe4-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-145">10 GB</span></span>|
|<span data-ttu-id="9bfe4-146">Price (monthly)</span><span class="sxs-lookup"><span data-stu-id="9bfe4-146">Price (monthly)</span></span>|<span data-ttu-id="9bfe4-147">Throughput: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-147">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="9bfe4-148">Storage: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-148">Storage: $0.25/GB</span></span>|<span data-ttu-id="9bfe4-149">Throughput: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="9bfe4-149">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="9bfe4-150">Storage: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="9bfe4-150">Storage: $0.25/GB</span></span>|<span data-ttu-id="9bfe4-151">$25 USD</span><span class="sxs-lookup"><span data-stu-id="9bfe4-151">$25 USD</span></span>|<span data-ttu-id="9bfe4-152">$50 USD</span><span class="sxs-lookup"><span data-stu-id="9bfe4-152">$50 USD</span></span>|<span data-ttu-id="9bfe4-153">$100 USD</span><span class="sxs-lookup"><span data-stu-id="9bfe4-153">$100 USD</span></span>|

<span data-ttu-id="9bfe4-154">Are you an EA customer?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-154">Are you an EA customer?</span></span> <span data-ttu-id="9bfe4-155">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="9bfe4-155">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="9bfe4-156">What do I need to do to ensure uninterrupted access to my data?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-156">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="9bfe4-157">If you have an S1, S2, or S3 collection, you should migrate the collection to a single partition collection programmatically [by using the .NET SDK](#migrate-diy).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-157">If you have an S1, S2, or S3 collection, you should migrate the collection to a single partition collection programmatically [by using the .NET SDK](#migrate-diy).</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="9bfe4-158">How will my collection change after the migration?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-158">How will my collection change after the migration?</span></span>

<span data-ttu-id="9bfe4-159">If you have an S1 collection, you can migrate them to a single partition collection with 400 RU/s throughput.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-159">If you have an S1 collection, you can migrate them to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="9bfe4-160">400 RU/s is the lowest throughput available with single partition collections.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-160">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="9bfe4-161">However, the cost for 400 RU/s in a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-161">However, the cost for 400 RU/s in a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="9bfe4-162">If you have an S2 collection, you can migrate them to a single partition collection with 1 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-162">If you have an S2 collection, you can migrate them to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="9bfe4-163">You will see no change to your throughput level.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-163">You will see no change to your throughput level.</span></span>

<span data-ttu-id="9bfe4-164">If you have an S3 collection, you can migrate them to a single partition collection with 2.5 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-164">If you have an S3 collection, you can migrate them to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="9bfe4-165">You will see no change to your throughput level.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="9bfe4-166">In each of these cases, after you migrate the collection, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-166">In each of these cases, after you migrate the collection, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> 

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-i-migrated-to-the-single-partition-collections"></a><span data-ttu-id="9bfe4-167">How will my billing change after I migrated to the single partition collections?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-167">How will my billing change after I migrated to the single partition collections?</span></span>

<span data-ttu-id="9bfe4-168">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-168">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="9bfe4-169">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-169">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![How S1 pricing for 10 collections compares to 10 collections using pricing for a single partition collection](./media/performance-levels/s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="9bfe4-171">What if I need more than 10 GB of storage?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-171">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="9bfe4-172">Whether you have a collection with S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Azure Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-172">Whether you have a collection with S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the Azure Cosmos DB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="9bfe4-173">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](sql-api-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-173">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure Cosmos DB](sql-api-partition-data.md).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-the-planned-migration"></a><span data-ttu-id="9bfe4-174">Can I change between the S1, S2, and S3 performance levels before the planned migration?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-174">Can I change between the S1, S2, and S3 performance levels before the planned migration?</span></span>

<span data-ttu-id="9bfe4-175">Only existing accounts with S1, S2, and S3 performance can be changed and alter performance level tiers programmatically [by using the .NET SDK](#migrate-diy).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-175">Only existing accounts with S1, S2, and S3 performance can be changed and alter performance level tiers programmatically [by using the .NET SDK](#migrate-diy).</span></span> <span data-ttu-id="9bfe4-176">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-176">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="9bfe4-177">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-177">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="9bfe4-178">You can migrate from the S1, S2, and S3 performance levels to single partition collections programmatically [by using the .NET SDK](#migrate-diy).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-178">You can migrate from the S1, S2, and S3 performance levels to single partition collections programmatically [by using the .NET SDK](#migrate-diy).</span></span> <span data-ttu-id="9bfe4-179">You can do this on your own before the planned migration to benefit from the flexible throughput options available with single partition collections.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-179">You can do this on your own before the planned migration to benefit from the flexible throughput options available with single partition collections.</span></span>

### <a name="migrate-to-single-partition-collections-by-using-the-net-sdk"></a><span data-ttu-id="9bfe4-180">Migrate to single partition collections by using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9bfe4-180">Migrate to single partition collections by using the .NET SDK</span></span>

<span data-ttu-id="9bfe4-181">This section only covers changing a collection's performance level using the [SQL .NET API](sql-api-sdk-dotnet.md), but the process is similar for our other SDKs.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-181">This section only covers changing a collection's performance level using the [SQL .NET API](sql-api-sdk-dotnet.md), but the process is similar for our other SDKs.</span></span>

<span data-ttu-id="9bfe4-182">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-182">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```csharp
    //Fetch the resource to be updated
    Offer offer = client.CreateOfferQuery()
                      .Where(r => r.ResourceLink == collection.SelfLink)    
                      .AsEnumerable()
                      .SingleOrDefault();

    // Set the throughput to 5000 request units per second
    offer = new OfferV2(offer, 5000);

    //Now persist these changes to the database by replacing the original resource
    await client.ReplaceOfferAsync(offer);
```

<span data-ttu-id="9bfe4-183">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-183">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="9bfe4-184">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="9bfe4-184">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="9bfe4-185">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="9bfe4-185">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="9bfe4-186">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="9bfe4-186">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="9bfe4-187">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="9bfe4-187">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="9bfe4-188">How am I impacted if I'm an EA customer?</span><span class="sxs-lookup"><span data-stu-id="9bfe4-188">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="9bfe4-189">EA customers will be price protected until the end of their current contract.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-189">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9bfe4-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bfe4-190">Next steps</span></span>
<span data-ttu-id="9bfe4-191">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="9bfe4-191">To learn more about pricing and managing data with Azure Cosmos DB, explore these resources:</span></span>

1.  <span data-ttu-id="9bfe4-192">[Partitioning data in Cosmos DB](sql-api-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-192">[Partitioning data in Cosmos DB](sql-api-partition-data.md).</span></span> <span data-ttu-id="9bfe4-193">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-193">Understand the difference between single partition container and partitioned containers, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="9bfe4-194">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-194">[Cosmos DB pricing](https://azure.microsoft.com/pricing/details/cosmos-db/).</span></span> <span data-ttu-id="9bfe4-195">Learn about the cost of provisioning throughput and consuming storage.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-195">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="9bfe4-196">[Request units](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="9bfe4-196">[Request units](request-units.md).</span></span> <span data-ttu-id="9bfe4-197">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span><span class="sxs-lookup"><span data-stu-id="9bfe4-197">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
