---
title: DocumentDB scale and performance testing | Microsoft Docs
description: Learn how to perform scale and performance testing with Azure DocumentDB
keywords: performance testing
services: documentdb
author: arramac
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: f4c96ebd-f53c-427d-a500-3f28fe7b11d0
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/19/2017
ms.author: arramac
ms.openlocfilehash: 86bd591c26a58200dab9872e07e6e8bdf2522df9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549356"
---
# <a name="performance-and-scale-testing-with-azure-documentdb"></a><span data-ttu-id="a27eb-104">Performance and scale testing with Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a27eb-104">Performance and scale testing with Azure DocumentDB</span></span>
<span data-ttu-id="a27eb-105">Performance and scale testing is a key step in application development.</span><span class="sxs-lookup"><span data-stu-id="a27eb-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="a27eb-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span><span class="sxs-lookup"><span data-stu-id="a27eb-106">For many applications, the database tier has a significant impact on the overall performance and scalability, and is therefore a critical component of performance testing.</span></span> <span data-ttu-id="a27eb-107">[Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span><span class="sxs-lookup"><span data-stu-id="a27eb-107">[Azure DocumentDB](https://azure.microsoft.com/services/documentdb/) is purpose-built for elastic scale and predictable performance, and therefore a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="a27eb-108">This article is a reference for developers implementing performance test suites for their DocumentDB workloads, or evaluating DocumentDB for high-performance application scenarios.</span><span class="sxs-lookup"><span data-stu-id="a27eb-108">This article is a reference for developers implementing performance test suites for their DocumentDB workloads, or evaluating DocumentDB for high-performance application scenarios.</span></span> <span data-ttu-id="a27eb-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span><span class="sxs-lookup"><span data-stu-id="a27eb-109">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="a27eb-110">After reading this article, you will be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="a27eb-110">After reading this article, you will be able to answer the following questions:</span></span>   

* <span data-ttu-id="a27eb-111">Where can I find a sample .NET client application for performance testing of Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="a27eb-111">Where can I find a sample .NET client application for performance testing of Azure DocumentDB?</span></span> 
* <span data-ttu-id="a27eb-112">How do I achieve high throughput levels with Azure DocumentDB from my client application?</span><span class="sxs-lookup"><span data-stu-id="a27eb-112">How do I achieve high throughput levels with Azure DocumentDB from my client application?</span></span>

<span data-ttu-id="a27eb-113">To get started with code, please download the project from [DocumentDB Performance Testing  Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="a27eb-113">To get started with code, please download the project from [DocumentDB Performance Testing  Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="a27eb-114">The goal of this application is to demonstrate best practices for extracting better performance out of DocumentDB with a small number of client machines.</span><span class="sxs-lookup"><span data-stu-id="a27eb-114">The goal of this application is to demonstrate best practices for extracting better performance out of DocumentDB with a small number of client machines.</span></span> <span data-ttu-id="a27eb-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span><span class="sxs-lookup"><span data-stu-id="a27eb-115">This was not made to demonstrate the peak capacity of the service, which can scale limitlessly.</span></span>
> 
> 

<span data-ttu-id="a27eb-116">If you're looking for client-side configuration options to improve DocumentDB performance, see [DocumentDB performance tips](documentdb-performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="a27eb-116">If you're looking for client-side configuration options to improve DocumentDB performance, see [DocumentDB performance tips](documentdb-performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="a27eb-117">Run the performance testing application</span><span class="sxs-lookup"><span data-stu-id="a27eb-117">Run the performance testing application</span></span>
<span data-ttu-id="a27eb-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span><span class="sxs-lookup"><span data-stu-id="a27eb-118">The quickest way to get started is to compile and run the .NET sample below, as described in the steps below.</span></span> <span data-ttu-id="a27eb-119">You can also review the source code and implement similar configurations to your own client applications.</span><span class="sxs-lookup"><span data-stu-id="a27eb-119">You can also review the source code and implement similar configurations to your own client applications.</span></span>

<span data-ttu-id="a27eb-120">**Step 1:** Download the project from [DocumentDB Performance Testing  Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="a27eb-120">**Step 1:** Download the project from [DocumentDB Performance Testing  Sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="a27eb-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span><span class="sxs-lookup"><span data-stu-id="a27eb-121">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="a27eb-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/documentdb/) to estimate the costs per collection.</span><span class="sxs-lookup"><span data-stu-id="a27eb-122">Before provisioning collections with high throughput, please refer to the [Pricing Page](https://azure.microsoft.com/pricing/details/documentdb/) to estimate the costs per collection.</span></span> <span data-ttu-id="a27eb-123">DocumentDB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your DocumentDB collections after testing.</span><span class="sxs-lookup"><span data-stu-id="a27eb-123">DocumentDB bills storage and throughput independently on an hourly basis, so you can save costs by deleting or lowering the throughput of your DocumentDB collections after testing.</span></span>
> 
> 

<span data-ttu-id="a27eb-124">**Step 3:** Compile and run the console app from the command line.</span><span class="sxs-lookup"><span data-stu-id="a27eb-124">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="a27eb-125">You should see output like the following:</span><span class="sxs-lookup"><span data-stu-id="a27eb-125">You should see output like the following:</span></span>

    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://docdb-scale-demo.documents.azure.com:443/
    Collection : db.testdata at 50000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: 500
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Creating database db
    Creating collection testdata
    Creating metric collection metrics
    Retrying after sleeping for 00:03:34.1720000
    Starting Inserts with 500 tasks
    Inserted 661 docs @ 656 writes/s, 6860 RU/s (18B max monthly 1KB reads)
    Inserted 6505 docs @ 2668 writes/s, 27962 RU/s (72B max monthly 1KB reads)
    Inserted 11756 docs @ 3240 writes/s, 33957 RU/s (88B max monthly 1KB reads)
    Inserted 17076 docs @ 3590 writes/s, 37627 RU/s (98B max monthly 1KB reads)
    Inserted 22106 docs @ 3748 writes/s, 39281 RU/s (102B max monthly 1KB reads)
    Inserted 28430 docs @ 3902 writes/s, 40897 RU/s (106B max monthly 1KB reads)
    Inserted 33492 docs @ 3928 writes/s, 41168 RU/s (107B max monthly 1KB reads)
    Inserted 38392 docs @ 3963 writes/s, 41528 RU/s (108B max monthly 1KB reads)
    Inserted 43371 docs @ 4012 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 48477 docs @ 4035 writes/s, 42282 RU/s (110B max monthly 1KB reads)
    Inserted 53845 docs @ 4088 writes/s, 42845 RU/s (111B max monthly 1KB reads)
    Inserted 59267 docs @ 4138 writes/s, 43364 RU/s (112B max monthly 1KB reads)
    Inserted 64703 docs @ 4197 writes/s, 43981 RU/s (114B max monthly 1KB reads)
    Inserted 70428 docs @ 4216 writes/s, 44181 RU/s (115B max monthly 1KB reads)
    Inserted 75868 docs @ 4247 writes/s, 44505 RU/s (115B max monthly 1KB reads)
    Inserted 81571 docs @ 4280 writes/s, 44852 RU/s (116B max monthly 1KB reads)
    Inserted 86271 docs @ 4273 writes/s, 44783 RU/s (116B max monthly 1KB reads)
    Inserted 91993 docs @ 4299 writes/s, 45056 RU/s (117B max monthly 1KB reads)
    Inserted 97469 docs @ 4292 writes/s, 44984 RU/s (117B max monthly 1KB reads)
    Inserted 99736 docs @ 4192 writes/s, 43930 RU/s (114B max monthly 1KB reads)
    Inserted 99997 docs @ 4013 writes/s, 42051 RU/s (109B max monthly 1KB reads)
    Inserted 100000 docs @ 3846 writes/s, 40304 RU/s (104B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 100000 docs @ 3834 writes/s, 40180 RU/s (104B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.


<span data-ttu-id="a27eb-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span><span class="sxs-lookup"><span data-stu-id="a27eb-126">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection.</span></span> <span data-ttu-id="a27eb-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span><span class="sxs-lookup"><span data-stu-id="a27eb-127">If not, increasing the DegreeOfParallelism in small increments may help you reach the limit.</span></span> <span data-ttu-id="a27eb-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span><span class="sxs-lookup"><span data-stu-id="a27eb-128">If the throughput from your client app plateaus, launching multiple instances of the app on the same or different machines will help you reach the provisioned limit across the different instances.</span></span> <span data-ttu-id="a27eb-129">If you need help with this step, please, write an email to askdocdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="a27eb-129">If you need help with this step, please, write an email to askdocdb@microsoft.com or file a support ticket from the [Azure Portal](https://portal.azure.com).</span></span>

<span data-ttu-id="a27eb-130">Once you have the app running, you can try different [Indexing policies](documentdb-indexing-policies.md) and [Consistency levels](documentdb-consistency-levels.md) to understand their impact on throughput and latency.</span><span class="sxs-lookup"><span data-stu-id="a27eb-130">Once you have the app running, you can try different [Indexing policies](documentdb-indexing-policies.md) and [Consistency levels](documentdb-consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="a27eb-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span><span class="sxs-lookup"><span data-stu-id="a27eb-131">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a27eb-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="a27eb-132">Next steps</span></span>
<span data-ttu-id="a27eb-133">In this article, we looked at how you can perform performance and scale testing with DocumentDB using a .NET console app.</span><span class="sxs-lookup"><span data-stu-id="a27eb-133">In this article, we looked at how you can perform performance and scale testing with DocumentDB using a .NET console app.</span></span> <span data-ttu-id="a27eb-134">Please refer to the links below for additional information on working with DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a27eb-134">Please refer to the links below for additional information on working with DocumentDB.</span></span>

* [<span data-ttu-id="a27eb-135">DocumentDB performance testing sample</span><span class="sxs-lookup"><span data-stu-id="a27eb-135">DocumentDB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="a27eb-136">Client configuration options to improve DocumentDB performance</span><span class="sxs-lookup"><span data-stu-id="a27eb-136">Client configuration options to improve DocumentDB performance</span></span>](documentdb-performance-tips.md)
* [<span data-ttu-id="a27eb-137">Server-side partitioning in DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a27eb-137">Server-side partitioning in DocumentDB</span></span>](documentdb-partition-data.md)
* [<span data-ttu-id="a27eb-138">DocumentDB collections and performance levels</span><span class="sxs-lookup"><span data-stu-id="a27eb-138">DocumentDB collections and performance levels</span></span>](documentdb-performance-levels.md)
* [<span data-ttu-id="a27eb-139">DocumentDB .NET SDK documentation on MSDN</span><span class="sxs-lookup"><span data-stu-id="a27eb-139">DocumentDB .NET SDK documentation on MSDN</span></span>](https://msdn.microsoft.com/library/azure/dn948556.aspx)
* [<span data-ttu-id="a27eb-140">DocumentDB .NET samples</span><span class="sxs-lookup"><span data-stu-id="a27eb-140">DocumentDB .NET samples</span></span>](https://github.com/Azure/azure-documentdb-net)
* [<span data-ttu-id="a27eb-141">DocumentDB blog on performance tips</span><span class="sxs-lookup"><span data-stu-id="a27eb-141">DocumentDB blog on performance tips</span></span>](https://azure.microsoft.com/blog/2015/01/20/performance-tips-for-azure-documentdb-part-1-2/)

