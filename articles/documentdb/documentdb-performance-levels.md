---
title: Performance levels in DocumentDB | Microsoft Docs
description: Learn about how performance levels in DocumentDB enable you to reserve throughput on a per collection basis.
services: documentdb
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: ''
ms.assetid: 7dc21c71-47e2-4e06-aa21-e84af52866f4
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: mimig
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 20ee04771b1bc13d4f79b416202bf91c1fa30bd3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563613"
---
# <a name="retiring-the-s1-s2-and-s3-performance-levels-in-documentdb"></a><span data-ttu-id="32ee5-103">Retiring the S1, S2, and S3 performance levels in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="32ee5-103">Retiring the S1, S2, and S3 performance levels in DocumentDB</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="32ee5-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB collections.</span><span class="sxs-lookup"><span data-stu-id="32ee5-104">The S1, S2, and S3 performance levels discussed in this article are being retired and are no longer available for new DocumentDB collections.</span></span>
>

<span data-ttu-id="32ee5-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span><span class="sxs-lookup"><span data-stu-id="32ee5-105">This article provides an overview of S1, S2, and S3 performance levels, and discusses how the collections that use these performance levels will be migrated to single partition collections on August 1st, 2017.</span></span> <span data-ttu-id="32ee5-106">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="32ee5-106">After reading this article, you'll be able to answer the following questions:</span></span>

- [<span data-ttu-id="32ee5-107">Why are the S1, S2, and S3 performance levels being retired?</span><span class="sxs-lookup"><span data-stu-id="32ee5-107">Why are the S1, S2, and S3 performance levels being retired?</span></span>](#why-retired)
- [<span data-ttu-id="32ee5-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span><span class="sxs-lookup"><span data-stu-id="32ee5-108">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>](#compare)
- [<span data-ttu-id="32ee5-109">What do I need to do to ensure uninterrupted access to my data?</span><span class="sxs-lookup"><span data-stu-id="32ee5-109">What do I need to do to ensure uninterrupted access to my data?</span></span>](#uninterrupted-access)
- [<span data-ttu-id="32ee5-110">How will my collection change after the migration?</span><span class="sxs-lookup"><span data-stu-id="32ee5-110">How will my collection change after the migration?</span></span>](#collection-change)
- [<span data-ttu-id="32ee5-111">How will my billing change after I’m migrated to single partition collections?</span><span class="sxs-lookup"><span data-stu-id="32ee5-111">How will my billing change after I’m migrated to single partition collections?</span></span>](#billing-change)
- [<span data-ttu-id="32ee5-112">What if I need more than 10 GB of storage?</span><span class="sxs-lookup"><span data-stu-id="32ee5-112">What if I need more than 10 GB of storage?</span></span>](#more-storage-needed)
- [<span data-ttu-id="32ee5-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span><span class="sxs-lookup"><span data-stu-id="32ee5-113">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>](#change-before)
- [<span data-ttu-id="32ee5-114">How will I know when my collection has migrated?</span><span class="sxs-lookup"><span data-stu-id="32ee5-114">How will I know when my collection has migrated?</span></span>](#when-migrated)
- [<span data-ttu-id="32ee5-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span><span class="sxs-lookup"><span data-stu-id="32ee5-115">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>](#migrate-diy)
- [<span data-ttu-id="32ee5-116">How am I impacted if I'm an EA customer?</span><span class="sxs-lookup"><span data-stu-id="32ee5-116">How am I impacted if I'm an EA customer?</span></span>](#ea-customer)

<a name="why-retired"></a>

## <a name="why-are-the-s1-s2-and-s3-performance-levels-being-retired"></a><span data-ttu-id="32ee5-117">Why are the S1, S2, and S3 performance levels being retired?</span><span class="sxs-lookup"><span data-stu-id="32ee5-117">Why are the S1, S2, and S3 performance levels being retired?</span></span>

<span data-ttu-id="32ee5-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB single partition collections offers.</span><span class="sxs-lookup"><span data-stu-id="32ee5-118">The S1, S2, and S3 performance levels do not offer the flexibility that DocumentDB single partition collections offers.</span></span> <span data-ttu-id="32ee5-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set.</span><span class="sxs-lookup"><span data-stu-id="32ee5-119">With the S1, S2, S3 performance levels, both the throughput and storage capacity were pre-set.</span></span> <span data-ttu-id="32ee5-120">DocumentDB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span><span class="sxs-lookup"><span data-stu-id="32ee5-120">DocumentDB now offers the ability to customize your throughput and storage, offering you much more flexibility in your ability to scale as your needs change.</span></span>

<a name="compare"></a>

## <a name="how-do-single-partition-collections-and-partitioned-collections-compare-to-the-s1-s2-s3-performance-levels"></a><span data-ttu-id="32ee5-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span><span class="sxs-lookup"><span data-stu-id="32ee5-121">How do single partition collections and partitioned collections compare to the S1, S2, S3 performance levels?</span></span>

<span data-ttu-id="32ee5-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span><span class="sxs-lookup"><span data-stu-id="32ee5-122">The following table compares the throughput and storage options available in single partition collections, partitioned collections, and S1, S2, S3 performance levels.</span></span> <span data-ttu-id="32ee5-123">Here is an example for US East 2 region:</span><span class="sxs-lookup"><span data-stu-id="32ee5-123">Here is an example for US East 2 region:</span></span>

|   |<span data-ttu-id="32ee5-124">Partitioned collection</span><span class="sxs-lookup"><span data-stu-id="32ee5-124">Partitioned collection</span></span>|<span data-ttu-id="32ee5-125">Single partition collection</span><span class="sxs-lookup"><span data-stu-id="32ee5-125">Single partition collection</span></span>|<span data-ttu-id="32ee5-126">S1</span><span class="sxs-lookup"><span data-stu-id="32ee5-126">S1</span></span>|<span data-ttu-id="32ee5-127">S2</span><span class="sxs-lookup"><span data-stu-id="32ee5-127">S2</span></span>|<span data-ttu-id="32ee5-128">S3</span><span class="sxs-lookup"><span data-stu-id="32ee5-128">S3</span></span>|
|---|---|---|---|---|---|
|<span data-ttu-id="32ee5-129">Maximum throughput</span><span class="sxs-lookup"><span data-stu-id="32ee5-129">Maximum throughput</span></span>|<span data-ttu-id="32ee5-130">Unlimited</span><span class="sxs-lookup"><span data-stu-id="32ee5-130">Unlimited</span></span>|<span data-ttu-id="32ee5-131">10K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-131">10K RU/s</span></span>|<span data-ttu-id="32ee5-132">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-132">250 RU/s</span></span>|<span data-ttu-id="32ee5-133">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-133">1 K RU/s</span></span>|<span data-ttu-id="32ee5-134">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-134">2.5 K RU/s</span></span>|
|<span data-ttu-id="32ee5-135">Minimum throughput</span><span class="sxs-lookup"><span data-stu-id="32ee5-135">Minimum throughput</span></span>|<span data-ttu-id="32ee5-136">2.5K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-136">2.5K RU/s</span></span>|<span data-ttu-id="32ee5-137">400 RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-137">400 RU/s</span></span>|<span data-ttu-id="32ee5-138">250 RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-138">250 RU/s</span></span>|<span data-ttu-id="32ee5-139">1 K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-139">1 K RU/s</span></span>|<span data-ttu-id="32ee5-140">2.5 K RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-140">2.5 K RU/s</span></span>|
|<span data-ttu-id="32ee5-141">Maximum storage</span><span class="sxs-lookup"><span data-stu-id="32ee5-141">Maximum storage</span></span>|<span data-ttu-id="32ee5-142">Unlimited</span><span class="sxs-lookup"><span data-stu-id="32ee5-142">Unlimited</span></span>|<span data-ttu-id="32ee5-143">10 GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-143">10 GB</span></span>|<span data-ttu-id="32ee5-144">10 GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-144">10 GB</span></span>|<span data-ttu-id="32ee5-145">10 GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-145">10 GB</span></span>|<span data-ttu-id="32ee5-146">10 GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-146">10 GB</span></span>|
|<span data-ttu-id="32ee5-147">Price</span><span class="sxs-lookup"><span data-stu-id="32ee5-147">Price</span></span>|<span data-ttu-id="32ee5-148">Throughput: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-148">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="32ee5-149">Storage: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-149">Storage: $0.25/GB</span></span>|<span data-ttu-id="32ee5-150">Throughput: $6 / 100 RU/s</span><span class="sxs-lookup"><span data-stu-id="32ee5-150">Throughput: $6 / 100 RU/s</span></span><br><br><span data-ttu-id="32ee5-151">Storage: $0.25/GB</span><span class="sxs-lookup"><span data-stu-id="32ee5-151">Storage: $0.25/GB</span></span>|<span data-ttu-id="32ee5-152">$25 USD</span><span class="sxs-lookup"><span data-stu-id="32ee5-152">$25 USD</span></span>|<span data-ttu-id="32ee5-153">$50 USD</span><span class="sxs-lookup"><span data-stu-id="32ee5-153">$50 USD</span></span>|<span data-ttu-id="32ee5-154">$100 USD</span><span class="sxs-lookup"><span data-stu-id="32ee5-154">$100 USD</span></span>|

<span data-ttu-id="32ee5-155">Are you an EA customer?</span><span class="sxs-lookup"><span data-stu-id="32ee5-155">Are you an EA customer?</span></span> <span data-ttu-id="32ee5-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span><span class="sxs-lookup"><span data-stu-id="32ee5-156">If so, see [How am I impacted if I'm an EA customer?](#ea-customer)</span></span>

<a name="uninterrupted-access"></a>

## <a name="what-do-i-need-to-do-to-ensure-uninterrupted-access-to-my-data"></a><span data-ttu-id="32ee5-157">What do I need to do to ensure uninterrupted access to my data?</span><span class="sxs-lookup"><span data-stu-id="32ee5-157">What do I need to do to ensure uninterrupted access to my data?</span></span>

<span data-ttu-id="32ee5-158">Nothing, DocumentDB handles the migration for you.</span><span class="sxs-lookup"><span data-stu-id="32ee5-158">Nothing, DocumentDB handles the migration for you.</span></span> <span data-ttu-id="32ee5-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="32ee5-159">If you have an S1, S2, or S3 collection, your current collection will be migrated to a single partition collection on July 31, 2017.</span></span> 

<a name="collection-change"></a>

## <a name="how-will-my-collection-change-after-the-migration"></a><span data-ttu-id="32ee5-160">How will my collection change after the migration?</span><span class="sxs-lookup"><span data-stu-id="32ee5-160">How will my collection change after the migration?</span></span>

<span data-ttu-id="32ee5-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span><span class="sxs-lookup"><span data-stu-id="32ee5-161">If you have an S1 collection, you will be migrated to a single partition collection with 400 RU/s throughput.</span></span> <span data-ttu-id="32ee5-162">400 RU/s is the lowest throughput available with single partition collections.</span><span class="sxs-lookup"><span data-stu-id="32ee5-162">400 RU/s is the lowest throughput available with single partition collections.</span></span> <span data-ttu-id="32ee5-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span><span class="sxs-lookup"><span data-stu-id="32ee5-163">However, the cost for 400 RU/s in the a single partition collection is approximately the same as you were paying with your S1 collection and 250 RU/s – so you are not paying for the extra 150 RU/s available to you.</span></span>

<span data-ttu-id="32ee5-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="32ee5-164">If you have an S2 collection, you will be migrated to a single partition collection with 1 K RU/s.</span></span> <span data-ttu-id="32ee5-165">You will see no change to your throughput level.</span><span class="sxs-lookup"><span data-stu-id="32ee5-165">You will see no change to your throughput level.</span></span>

<span data-ttu-id="32ee5-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span><span class="sxs-lookup"><span data-stu-id="32ee5-166">If you have an S3 collection, you will be migrated to a single partition collection with 2.5 K RU/s.</span></span> <span data-ttu-id="32ee5-167">You will see no change to your throughput level.</span><span class="sxs-lookup"><span data-stu-id="32ee5-167">You will see no change to your throughput level.</span></span>

<span data-ttu-id="32ee5-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span><span class="sxs-lookup"><span data-stu-id="32ee5-168">In each of these cases, after your collection is migrated, you will be able to customize your throughput level, or scale it up and down as needed to provide low-latency access to your users.</span></span> <span data-ttu-id="32ee5-169">To change the throughput level after your collection has migrated, simply open your DocumentDB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="32ee5-169">To change the throughput level after your collection has migrated, simply open your DocumentDB account in the Azure portal, click Scale, choose your collection, and then adjust the throughput level, as shown in the following screenshot:</span></span>

![How to scale throughput in the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-levels/azure-documentdb-portal-scale-throughput.png)

<a name="billing-change"></a>

## <a name="how-will-my-billing-change-after-im-migrated-to-the-single-partition-collections"></a><span data-ttu-id="32ee5-171">How will my billing change after I’m migrated to the single partition collections?</span><span class="sxs-lookup"><span data-stu-id="32ee5-171">How will my billing change after I’m migrated to the single partition collections?</span></span>

<span data-ttu-id="32ee5-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span><span class="sxs-lookup"><span data-stu-id="32ee5-172">Assuming you have 10 S1 collections, 1 GB of storage for each, in the US East region, and you migrate these 10 S1 collections to 10 single partition collections at 400 RU/sec (the minimum level).</span></span> <span data-ttu-id="32ee5-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span><span class="sxs-lookup"><span data-stu-id="32ee5-173">Your bill will look as follows if you keep the 10 single partition collections for a full month:</span></span>

![How S1 pricing for 10 collections compares to 10 collections using pricing for a single partition collection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-levels/documentdb-s1-vs-standard-pricing.png)

<a name="more-storage-needed"></a>

## <a name="what-if-i-need-more-than-10-gb-of-storage"></a><span data-ttu-id="32ee5-175">What if I need more than 10 GB of storage?</span><span class="sxs-lookup"><span data-stu-id="32ee5-175">What if I need more than 10 GB of storage?</span></span>

<span data-ttu-id="32ee5-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the DocumentDB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span><span class="sxs-lookup"><span data-stu-id="32ee5-176">Whether you have a collection with an S1, S2, or S3 performance level, or have a single partition collection, all of which have 10 GB of storage available, you can use the DocumentDB Data Migration tool to migrate your data to a partitioned collection with virtually unlimited storage.</span></span> <span data-ttu-id="32ee5-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="32ee5-177">For information about the benefits of a partitioned collection, see [Partitioning and scaling in Azure DocumentDB](documentdb-partition-data.md).</span></span> <span data-ttu-id="32ee5-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="32ee5-178">For information about how to migrate your S1, S2, S3, or single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span> 

<a name="change-before"></a>

## <a name="can-i-change-between-the-s1-s2-and-s3-performance-levels-before-august-1-2017"></a><span data-ttu-id="32ee5-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span><span class="sxs-lookup"><span data-stu-id="32ee5-179">Can I change between the S1, S2, and S3 performance levels before August 1, 2017?</span></span>

<span data-ttu-id="32ee5-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span><span class="sxs-lookup"><span data-stu-id="32ee5-180">Only existing accounts with S1, S2, and S3 performance will be able to change and alter performance level tiers through the portal or programmatically.</span></span> <span data-ttu-id="32ee5-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span><span class="sxs-lookup"><span data-stu-id="32ee5-181">By August 1, 2017, the S1, S2, and S3 performance levels will no longer be available.</span></span> <span data-ttu-id="32ee5-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span><span class="sxs-lookup"><span data-stu-id="32ee5-182">If you change from S1, S3, or S3 to a single partition collection, you cannot return to the S1, S2, or S3 performance levels.</span></span>

<a name="when-migrated"></a>

## <a name="how-will-i-know-when-my-collection-has-migrated"></a><span data-ttu-id="32ee5-183">How will I know when my collection has migrated?</span><span class="sxs-lookup"><span data-stu-id="32ee5-183">How will I know when my collection has migrated?</span></span>

<span data-ttu-id="32ee5-184">The migration will occur on July 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="32ee5-184">The migration will occur on July 31, 2017.</span></span> <span data-ttu-id="32ee5-185">If you have a collection that uses the S1, S2 or S3 performance levels, the DocumentDB team will contact you by email before the migration takes place.</span><span class="sxs-lookup"><span data-stu-id="32ee5-185">If you have a collection that uses the S1, S2 or S3 performance levels, the DocumentDB team will contact you by email before the migration takes place.</span></span> <span data-ttu-id="32ee5-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span><span class="sxs-lookup"><span data-stu-id="32ee5-186">Once the migration is complete, on August 1, 2017, the Azure portal will show that your collection uses Standard pricing.</span></span>

![How to confirm your collection has migrated to the Standard pricing tier](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-levels/documentdb-portal-standard-pricing-applied.png)

<a name="migrate-diy"></a>

## <a name="how-do-i-migrate-from-the-s1-s2-s3-performance-levels-to-single-partition-collections-on-my-own"></a><span data-ttu-id="32ee5-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span><span class="sxs-lookup"><span data-stu-id="32ee5-188">How do I migrate from the S1, S2, S3 performance levels to single partition collections on my own?</span></span>

<span data-ttu-id="32ee5-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span><span class="sxs-lookup"><span data-stu-id="32ee5-189">You can migrate from the S1, S2, and S3 performance levels to single partition collections using the Azure portal or programmatically.</span></span> <span data-ttu-id="32ee5-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="32ee5-190">You can do this on your own before August 1 to benefit from the flexible throughput options available with single partition collections, or we will migrate your collections for you on July 31, 2017.</span></span>

<span data-ttu-id="32ee5-191">**To migrate to single partition collections using the Azure portal**</span><span class="sxs-lookup"><span data-stu-id="32ee5-191">**To migrate to single partition collections using the Azure portal**</span></span>

1. <span data-ttu-id="32ee5-192">In the [**Azure portal**](https://portal.azure.com), click **NoSQL (DocumentDB)**, then select the DocumentDB account to modify.</span><span class="sxs-lookup"><span data-stu-id="32ee5-192">In the [**Azure portal**](https://portal.azure.com), click **NoSQL (DocumentDB)**, then select the DocumentDB account to modify.</span></span> 
 
    <span data-ttu-id="32ee5-193">If **NoSQL (DocumentDB)** is not on the Jumpbar, click >, scroll to **Databases**, select **NoSQL (DocumentDB)**, and then select the DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="32ee5-193">If **NoSQL (DocumentDB)** is not on the Jumpbar, click >, scroll to **Databases**, select **NoSQL (DocumentDB)**, and then select the DocumentDB account.</span></span>  

2. <span data-ttu-id="32ee5-194">On the resource menu, under **Collections**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span><span class="sxs-lookup"><span data-stu-id="32ee5-194">On the resource menu, under **Collections**, click **Scale**, select the collection to modify from the drop-down list, and then click **Pricing Tier**.</span></span> <span data-ttu-id="32ee5-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span><span class="sxs-lookup"><span data-stu-id="32ee5-195">Accounts using pre-defined throughput have a pricing tier of S1, S2, or S3.</span></span>  <span data-ttu-id="32ee5-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span><span class="sxs-lookup"><span data-stu-id="32ee5-196">In the **Choose your pricing tier** blade, click **Standard** to change to user-defined throughput, and then click **Select** to save your change.</span></span>

    ![Screen shot of the Settings blade showing where to change the throughput value](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-performance-levels/documentdb-change-performance-set-thoughput.png)

3. <span data-ttu-id="32ee5-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span><span class="sxs-lookup"><span data-stu-id="32ee5-198">Back in the **Scale** blade, the **Pricing Tier** is changed to **Standard** and the **Throughput (RU/s)** box is displayed with a default value of 400.</span></span> <span data-ttu-id="32ee5-199">Set the throughput between 400 and 10,000 [Request units](documentdb-request-units.md)/second (RU/s).</span><span class="sxs-lookup"><span data-stu-id="32ee5-199">Set the throughput between 400 and 10,000 [Request units](documentdb-request-units.md)/second (RU/s).</span></span> <span data-ttu-id="32ee5-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span><span class="sxs-lookup"><span data-stu-id="32ee5-200">The **Estimated Monthly Bill** at the bottom of the page updates automatically to provide an estimate of the monthly cost.</span></span> 

    >[!IMPORTANT] 
    > <span data-ttu-id="32ee5-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span><span class="sxs-lookup"><span data-stu-id="32ee5-201">Once you save your changes and move to the Standard pricing tier, you cannot roll back to the S1, S2, or S3 performance levels.</span></span>

4. <span data-ttu-id="32ee5-202">Click **Save** to save your changes.</span><span class="sxs-lookup"><span data-stu-id="32ee5-202">Click **Save** to save your changes.</span></span>

    <span data-ttu-id="32ee5-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span><span class="sxs-lookup"><span data-stu-id="32ee5-203">If you determine that you need more throughput (greater than 10,000 RU/s) or more storage (greater than 10GB) you can create a partitioned collection.</span></span> <span data-ttu-id="32ee5-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span><span class="sxs-lookup"><span data-stu-id="32ee5-204">To migrate a single partition collection to a partitioned collection, see [Migrating from single-partition to partitioned collections](documentdb-partition-data.md#migrating-from-single-partition).</span></span>

    > [!NOTE]
    > <span data-ttu-id="32ee5-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span><span class="sxs-lookup"><span data-stu-id="32ee5-205">Changing from S1, S2, or S3 to Standard may take up to 2 minutes.</span></span>
    > 
    > 

<span data-ttu-id="32ee5-206">**To migrate to single partition collections using the .NET SDK**</span><span class="sxs-lookup"><span data-stu-id="32ee5-206">**To migrate to single partition collections using the .NET SDK**</span></span>

<span data-ttu-id="32ee5-207">Another option for changing your collections' performance levels is through our SDKs.</span><span class="sxs-lookup"><span data-stu-id="32ee5-207">Another option for changing your collections' performance levels is through our SDKs.</span></span> <span data-ttu-id="32ee5-208">This section only covers changing a collection's performance level using our [.NET SDK](https://msdn.microsoft.com/library/azure/dn948556.aspx), but the process is similar for our other [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span><span class="sxs-lookup"><span data-stu-id="32ee5-208">This section only covers changing a collection's performance level using our [.NET SDK](https://msdn.microsoft.com/library/azure/dn948556.aspx), but the process is similar for our other [SDKs](https://msdn.microsoft.com/library/azure/dn781482.aspx).</span></span> <span data-ttu-id="32ee5-209">If you are new to our .NET SDK, visit our [getting started tutorial](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="32ee5-209">If you are new to our .NET SDK, visit our [getting started tutorial](documentdb-get-started.md).</span></span>

<span data-ttu-id="32ee5-210">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span><span class="sxs-lookup"><span data-stu-id="32ee5-210">Here is a code snippet for changing the collection throughput to 5,000 request units per second:</span></span>
    
```C#
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

<span data-ttu-id="32ee5-211">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span><span class="sxs-lookup"><span data-stu-id="32ee5-211">Visit [MSDN](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.aspx) to view additional examples and learn more about our offer methods:</span></span>

* [<span data-ttu-id="32ee5-212">**ReadOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="32ee5-212">**ReadOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readofferasync.aspx)
* [<span data-ttu-id="32ee5-213">**ReadOffersFeedAsync**</span><span class="sxs-lookup"><span data-stu-id="32ee5-213">**ReadOffersFeedAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.readoffersfeedasync.aspx)
* [<span data-ttu-id="32ee5-214">**ReplaceOfferAsync**</span><span class="sxs-lookup"><span data-stu-id="32ee5-214">**ReplaceOfferAsync**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.replaceofferasync.aspx)
* [<span data-ttu-id="32ee5-215">**CreateOfferQuery**</span><span class="sxs-lookup"><span data-stu-id="32ee5-215">**CreateOfferQuery**</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.documentqueryable.createofferquery.aspx)

<a name="ea-customer"></a>

## <a name="how-am-i-impacted-if-im-an-ea-customer"></a><span data-ttu-id="32ee5-216">How am I impacted if I'm an EA customer?</span><span class="sxs-lookup"><span data-stu-id="32ee5-216">How am I impacted if I'm an EA customer?</span></span>

<span data-ttu-id="32ee5-217">EA customers will be price protected until the end of their current contract.</span><span class="sxs-lookup"><span data-stu-id="32ee5-217">EA customers will be price protected until the end of their current contract.</span></span>

## <a name="next-steps"></a><span data-ttu-id="32ee5-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="32ee5-218">Next steps</span></span>
<span data-ttu-id="32ee5-219">To learn more about pricing and managing data with Azure DocumentDB, explore these resources:</span><span class="sxs-lookup"><span data-stu-id="32ee5-219">To learn more about pricing and managing data with Azure DocumentDB, explore these resources:</span></span>

1.  <span data-ttu-id="32ee5-220">[Partitioning data in DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="32ee5-220">[Partitioning data in DocumentDB](documentdb-partition-data.md).</span></span> <span data-ttu-id="32ee5-221">Understand the difference between single partition collections and partitioned collection, as well as tips on implementing a partitioning strategy to scale seamlessly.</span><span class="sxs-lookup"><span data-stu-id="32ee5-221">Understand the difference between single partition collections and partitioned collection, as well as tips on implementing a partitioning strategy to scale seamlessly.</span></span>
2.  <span data-ttu-id="32ee5-222">[DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="32ee5-222">[DocumentDB pricing](https://azure.microsoft.com/pricing/details/documentdb/).</span></span> <span data-ttu-id="32ee5-223">Learn about the cost of provisioning throughput and consuming storage.</span><span class="sxs-lookup"><span data-stu-id="32ee5-223">Learn about the cost of provisioning throughput and consuming storage.</span></span>
3.  <span data-ttu-id="32ee5-224">[Request units](documentdb-request-units.md).</span><span class="sxs-lookup"><span data-stu-id="32ee5-224">[Request units](documentdb-request-units.md).</span></span> <span data-ttu-id="32ee5-225">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span><span class="sxs-lookup"><span data-stu-id="32ee5-225">Understand the consumption of throughput for different operation types, for example Read, Write, Query.</span></span>
4.  <span data-ttu-id="32ee5-226">[Modeling data in DocumentDB](documentdb-modeling-data.md).</span><span class="sxs-lookup"><span data-stu-id="32ee5-226">[Modeling data in DocumentDB](documentdb-modeling-data.md).</span></span> <span data-ttu-id="32ee5-227">Learn how to model your data for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="32ee5-227">Learn how to model your data for DocumentDB.</span></span>



