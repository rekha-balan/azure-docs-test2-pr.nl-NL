---
title: Azure Cosmos DB scale and performance testing | Microsoft Docs
description: Learn how to perform scale and performance testing with Azure Cosmos DB
keywords: performance testing
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 08/29/2017
ms.author: sngun
ms.openlocfilehash: ce2c0ddcce3813990bf819477f7db425d70e3595
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866049"
---
# <a name="performance-and-scale-testing-with-azure-cosmos-db"></a><span data-ttu-id="c9c12-104">Performance and scale testing with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9c12-104">Performance and scale testing with Azure Cosmos DB</span></span>

<span data-ttu-id="c9c12-105">Performance and scale testing is a key step in application development.</span><span class="sxs-lookup"><span data-stu-id="c9c12-105">Performance and scale testing is a key step in application development.</span></span> <span data-ttu-id="c9c12-106">For many applications, the database tier has a significant impact on overall performance and scalability.</span><span class="sxs-lookup"><span data-stu-id="c9c12-106">For many applications, the database tier has a significant impact on overall performance and scalability.</span></span> <span data-ttu-id="c9c12-107">Therefore, it's a critical component of performance testing.</span><span class="sxs-lookup"><span data-stu-id="c9c12-107">Therefore, it's a critical component of performance testing.</span></span> <span data-ttu-id="c9c12-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance.</span><span class="sxs-lookup"><span data-stu-id="c9c12-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is purpose-built for elastic scale and predictable performance.</span></span> <span data-ttu-id="c9c12-109">These capabilities make it a great fit for applications that need a high-performance database tier.</span><span class="sxs-lookup"><span data-stu-id="c9c12-109">These capabilities make it a great fit for applications that need a high-performance database tier.</span></span> 

<span data-ttu-id="c9c12-110">This article is a reference for developers implementing performance test suites for their Azure Cosmos DB workloads.</span><span class="sxs-lookup"><span data-stu-id="c9c12-110">This article is a reference for developers implementing performance test suites for their Azure Cosmos DB workloads.</span></span> <span data-ttu-id="c9c12-111">It also can be used to evaluate Azure Cosmos DB for high-performance application scenarios.</span><span class="sxs-lookup"><span data-stu-id="c9c12-111">It also can be used to evaluate Azure Cosmos DB for high-performance application scenarios.</span></span> <span data-ttu-id="c9c12-112">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span><span class="sxs-lookup"><span data-stu-id="c9c12-112">It focuses primarily on isolated performance testing of the database, but also includes best practices for production applications.</span></span>

<span data-ttu-id="c9c12-113">After reading this article, you'll be able to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="c9c12-113">After reading this article, you'll be able to answer the following questions:</span></span> 

* <span data-ttu-id="c9c12-114">Where can I find a sample .NET client application for performance testing of Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="c9c12-114">Where can I find a sample .NET client application for performance testing of Azure Cosmos DB?</span></span> 
* <span data-ttu-id="c9c12-115">How do I achieve high throughput levels with Azure Cosmos DB from my client application?</span><span class="sxs-lookup"><span data-stu-id="c9c12-115">How do I achieve high throughput levels with Azure Cosmos DB from my client application?</span></span>

<span data-ttu-id="c9c12-116">To get started with code, download the project from [Azure Cosmos DB performance testing sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span><span class="sxs-lookup"><span data-stu-id="c9c12-116">To get started with code, download the project from [Azure Cosmos DB performance testing sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark).</span></span> 

> [!NOTE]
> <span data-ttu-id="c9c12-117">The goal of this application is to demonstrate how to get the best performance from Azure Cosmos DB with a small number of client machines.</span><span class="sxs-lookup"><span data-stu-id="c9c12-117">The goal of this application is to demonstrate how to get the best performance from Azure Cosmos DB with a small number of client machines.</span></span> <span data-ttu-id="c9c12-118">The goal of the sample is not to achieve the peak throughput capacity of Azure Cosmos DB (which can scale without any limits).</span><span class="sxs-lookup"><span data-stu-id="c9c12-118">The goal of the sample is not to achieve the peak throughput capacity of Azure Cosmos DB (which can scale without any limits).</span></span>
> 
> 

<span data-ttu-id="c9c12-119">If you're looking for client-side configuration options to improve Azure Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span><span class="sxs-lookup"><span data-stu-id="c9c12-119">If you're looking for client-side configuration options to improve Azure Cosmos DB performance, see [Azure Cosmos DB performance tips](performance-tips.md).</span></span>

## <a name="run-the-performance-testing-application"></a><span data-ttu-id="c9c12-120">Run the performance testing application</span><span class="sxs-lookup"><span data-stu-id="c9c12-120">Run the performance testing application</span></span>
<span data-ttu-id="c9c12-121">The quickest way to get started is to compile and run the .NET sample, as described in the following steps.</span><span class="sxs-lookup"><span data-stu-id="c9c12-121">The quickest way to get started is to compile and run the .NET sample, as described in the following steps.</span></span> <span data-ttu-id="c9c12-122">You can also review the source code and implement similar configurations on your own client applications.</span><span class="sxs-lookup"><span data-stu-id="c9c12-122">You can also review the source code and implement similar configurations on your own client applications.</span></span>

<span data-ttu-id="c9c12-123">**Step 1:** Download the project from [Azure Cosmos DB performance testing sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="c9c12-123">**Step 1:** Download the project from [Azure Cosmos DB performance testing sample](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark), or fork the GitHub repository.</span></span>

<span data-ttu-id="c9c12-124">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput, and DocumentTemplate (optional) in App.config.</span><span class="sxs-lookup"><span data-stu-id="c9c12-124">**Step 2:** Modify the settings for EndpointUrl, AuthorizationKey, CollectionThroughput, and DocumentTemplate (optional) in App.config.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c12-125">Before you provision collections with high throughput, refer to the [Pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span><span class="sxs-lookup"><span data-stu-id="c9c12-125">Before you provision collections with high throughput, refer to the [Pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/) to estimate the costs per collection.</span></span> <span data-ttu-id="c9c12-126">Azure Cosmos DB bills storage and throughput independently on an hourly basis.</span><span class="sxs-lookup"><span data-stu-id="c9c12-126">Azure Cosmos DB bills storage and throughput independently on an hourly basis.</span></span> <span data-ttu-id="c9c12-127">You can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span><span class="sxs-lookup"><span data-stu-id="c9c12-127">You can save costs by deleting or lowering the throughput of your Azure Cosmos DB collections after testing.</span></span>
> 
> 

<span data-ttu-id="c9c12-128">**Step 3:** Compile and run the console app from the command line.</span><span class="sxs-lookup"><span data-stu-id="c9c12-128">**Step 3:** Compile and run the console app from the command line.</span></span> <span data-ttu-id="c9c12-129">You should see output like the following:</span><span class="sxs-lookup"><span data-stu-id="c9c12-129">You should see output like the following:</span></span>

    C:\Users\cosmosdb\Desktop\Benchmark>DocumentDBBenchmark.exe
    Summary:
    ---------------------------------------------------------------------
    Endpoint: https://arramacquerymetrics.documents.azure.com:443/
    Collection : db.data at 100000 request units per second
    Document Template*: Player.json
    Degree of parallelism*: -1
    ---------------------------------------------------------------------

    DocumentDBBenchmark starting...
    Found collection data with 100000 RU/s
    Starting Inserts with 100 tasks
    Inserted 4503 docs @ 4491 writes/s, 47070 RU/s (122B max monthly 1KB reads)
    Inserted 17910 docs @ 8862 writes/s, 92878 RU/s (241B max monthly 1KB reads)
    Inserted 32339 docs @ 10531 writes/s, 110366 RU/s (286B max monthly 1KB reads)
    Inserted 47848 docs @ 11675 writes/s, 122357 RU/s (317B max monthly 1KB reads)
    Inserted 58857 docs @ 11545 writes/s, 120992 RU/s (314B max monthly 1KB reads)
    Inserted 69547 docs @ 11378 writes/s, 119237 RU/s (309B max monthly 1KB reads)
    Inserted 80687 docs @ 11345 writes/s, 118896 RU/s (308B max monthly 1KB reads)
    Inserted 91455 docs @ 11272 writes/s, 118131 RU/s (306B max monthly 1KB reads)
    Inserted 102129 docs @ 11208 writes/s, 117461 RU/s (304B max monthly 1KB reads)
    Inserted 112444 docs @ 11120 writes/s, 116538 RU/s (302B max monthly 1KB reads)
    Inserted 122927 docs @ 11063 writes/s, 115936 RU/s (301B max monthly 1KB reads)
    Inserted 133157 docs @ 10993 writes/s, 115208 RU/s (299B max monthly 1KB reads)
    Inserted 144078 docs @ 10988 writes/s, 115159 RU/s (298B max monthly 1KB reads)
    Inserted 155415 docs @ 11013 writes/s, 115415 RU/s (299B max monthly 1KB reads)
    Inserted 166126 docs @ 10992 writes/s, 115198 RU/s (299B max monthly 1KB reads)
    Inserted 173051 docs @ 10739 writes/s, 112544 RU/s (292B max monthly 1KB reads)
    Inserted 180169 docs @ 10527 writes/s, 110324 RU/s (286B max monthly 1KB reads)
    Inserted 192469 docs @ 10616 writes/s, 111256 RU/s (288B max monthly 1KB reads)
    Inserted 199107 docs @ 10406 writes/s, 109054 RU/s (283B max monthly 1KB reads)
    Inserted 200000 docs @ 9930 writes/s, 104065 RU/s (270B max monthly 1KB reads)

    Summary:
    ---------------------------------------------------------------------
    Inserted 200000 docs @ 9928 writes/s, 104063 RU/s (270B max monthly 1KB reads)
    ---------------------------------------------------------------------
    DocumentDBBenchmark completed successfully.
    Press any key to exit...


<span data-ttu-id="c9c12-130">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection or a set of collections.</span><span class="sxs-lookup"><span data-stu-id="c9c12-130">**Step 4 (if necessary):** The throughput reported (RU/s) from the tool should be the same or higher than the provisioned throughput of the collection or a set of collections.</span></span> <span data-ttu-id="c9c12-131">If it's not, increasing the DegreeOfParallelism in small increments might help you reach the limit.</span><span class="sxs-lookup"><span data-stu-id="c9c12-131">If it's not, increasing the DegreeOfParallelism in small increments might help you reach the limit.</span></span> <span data-ttu-id="c9c12-132">If the throughput from your client app plateaus, start multiple instances of the app on additional client machines.</span><span class="sxs-lookup"><span data-stu-id="c9c12-132">If the throughput from your client app plateaus, start multiple instances of the app on additional client machines.</span></span> <span data-ttu-id="c9c12-133">If you need help with this step, email askcosmosdb@microsoft.com or file a support ticket from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c9c12-133">If you need help with this step, email askcosmosdb@microsoft.com or file a support ticket from the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="c9c12-134">After you have the app running, you can try different [indexing policies](indexing-policies.md) and [consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span><span class="sxs-lookup"><span data-stu-id="c9c12-134">After you have the app running, you can try different [indexing policies](indexing-policies.md) and [consistency levels](consistency-levels.md) to understand their impact on throughput and latency.</span></span> <span data-ttu-id="c9c12-135">You can also review the source code and implement similar configurations to your own test suites or production applications.</span><span class="sxs-lookup"><span data-stu-id="c9c12-135">You can also review the source code and implement similar configurations to your own test suites or production applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c9c12-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="c9c12-136">Next steps</span></span>
<span data-ttu-id="c9c12-137">In this article, we looked at how you can perform performance and scale testing with Azure Cosmos DB by using a .NET console app.</span><span class="sxs-lookup"><span data-stu-id="c9c12-137">In this article, we looked at how you can perform performance and scale testing with Azure Cosmos DB by using a .NET console app.</span></span> <span data-ttu-id="c9c12-138">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="c9c12-138">For more information, see the following articles:</span></span>

* [<span data-ttu-id="c9c12-139">Azure Cosmos DB performance testing sample</span><span class="sxs-lookup"><span data-stu-id="c9c12-139">Azure Cosmos DB performance testing sample</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/documentdb-benchmark)
* [<span data-ttu-id="c9c12-140">Client configuration options to improve Azure Cosmos DB performance</span><span class="sxs-lookup"><span data-stu-id="c9c12-140">Client configuration options to improve Azure Cosmos DB performance</span></span>](performance-tips.md)
* [<span data-ttu-id="c9c12-141">Server-side partitioning in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c9c12-141">Server-side partitioning in Azure Cosmos DB</span></span>](partition-data.md)


