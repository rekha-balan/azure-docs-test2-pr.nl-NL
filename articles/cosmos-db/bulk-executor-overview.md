---
title: Azure Cosmos DB bulk executor library overview | Microsoft Docs
description: Learn about Azure Cosmos DB bulk executor library, benifits of using the library, and its architecture.
keywords: Java bulk executor
services: cosmos-db
author: tknandu
manager: kfile
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 05/07/2018
ms.author: ramkris
ms.openlocfilehash: 7c490aa958cf9e78c260dd0fbcf7952b55d8d88c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866876"
---
# <a name="azure-cosmos-db-bulk-executor-library-overview"></a><span data-ttu-id="4ff50-104">Azure Cosmos DB bulk executor library overview</span><span class="sxs-lookup"><span data-stu-id="4ff50-104">Azure Cosmos DB bulk executor library overview</span></span>
 
<span data-ttu-id="4ff50-105">Azure Cosmos DB is a fast, flexible, and globally distributed database service that is designed to elastically scale out to support:</span><span class="sxs-lookup"><span data-stu-id="4ff50-105">Azure Cosmos DB is a fast, flexible, and globally distributed database service that is designed to elastically scale out to support:</span></span> 

* <span data-ttu-id="4ff50-106">Large read and write throughputs (millions of operations per second).</span><span class="sxs-lookup"><span data-stu-id="4ff50-106">Large read and write throughputs (millions of operations per second).</span></span>  
* <span data-ttu-id="4ff50-107">Storing high volumes of (hundreds of terabytes, or even more) transactional and operational data with predictable millisecond latency.</span><span class="sxs-lookup"><span data-stu-id="4ff50-107">Storing high volumes of (hundreds of terabytes, or even more) transactional and operational data with predictable millisecond latency.</span></span>  

<span data-ttu-id="4ff50-108">The bulk executor library helps you leverage this massive throughput and storage, The bulk executor library allows you to perform bulk operations in Azure Cosmos DB through bulk import and bulk update APIs.</span><span class="sxs-lookup"><span data-stu-id="4ff50-108">The bulk executor library helps you leverage this massive throughput and storage, The bulk executor library allows you to perform bulk operations in Azure Cosmos DB through bulk import and bulk update APIs.</span></span> <span data-ttu-id="4ff50-109">You can read more about the features of bulk executor library in the following sections.</span><span class="sxs-lookup"><span data-stu-id="4ff50-109">You can read more about the features of bulk executor library in the following sections.</span></span> 

> [!NOTE] 
> <span data-ttu-id="4ff50-110">Currently, bulk executor library supports import and update operations and this library is supported by Azure Cosmos DB SQL API accounts only.</span><span class="sxs-lookup"><span data-stu-id="4ff50-110">Currently, bulk executor library supports import and update operations and this library is supported by Azure Cosmos DB SQL API accounts only.</span></span> <span data-ttu-id="4ff50-111">See [.NET](sql-api-sdk-bulk-executor-dot-net.md) and [Java](sql-api-sdk-bulk-executor-java.md) release notes for any updates to the library.</span><span class="sxs-lookup"><span data-stu-id="4ff50-111">See [.NET](sql-api-sdk-bulk-executor-dot-net.md) and [Java](sql-api-sdk-bulk-executor-java.md) release notes for any updates to the library.</span></span>
 
## <a name="key-features-of-the-bulk-executor-library"></a><span data-ttu-id="4ff50-112">Key features of the bulk executor library</span><span class="sxs-lookup"><span data-stu-id="4ff50-112">Key features of the bulk executor library</span></span>  
 
* <span data-ttu-id="4ff50-113">It significantly reduces the client-side compute resources needed to saturate the throughput allocated to a container.</span><span class="sxs-lookup"><span data-stu-id="4ff50-113">It significantly reduces the client-side compute resources needed to saturate the throughput allocated to a container.</span></span> <span data-ttu-id="4ff50-114">A single threaded application that writes data using the bulk import API achieves 10 times greater write throughput when compared to a multi-threaded application that writes data in parallel while saturating the client machine's CPU.</span><span class="sxs-lookup"><span data-stu-id="4ff50-114">A single threaded application that writes data using the bulk import API achieves 10 times greater write throughput when compared to a multi-threaded application that writes data in parallel while saturating the client machine's CPU.</span></span>  

* <span data-ttu-id="4ff50-115">It abstracts away the tedious tasks of writing application logic to handle rate limiting of request, request timeouts, and other transient exceptions by efficiently handling them within the library.</span><span class="sxs-lookup"><span data-stu-id="4ff50-115">It abstracts away the tedious tasks of writing application logic to handle rate limiting of request, request timeouts, and other transient exceptions by efficiently handling them within the library.</span></span>  

* <span data-ttu-id="4ff50-116">It provides a simplified mechanism for applications performing bulk operations to scale out. A single bulk executor instance running on an Azure VM can consume greater than 500 K RU/s and you can achieve a higher throughput rate by adding additional instances on individual client VMs.</span><span class="sxs-lookup"><span data-stu-id="4ff50-116">It provides a simplified mechanism for applications performing bulk operations to scale out. A single bulk executor instance running on an Azure VM can consume greater than 500 K RU/s and you can achieve a higher throughput rate by adding additional instances on individual client VMs.</span></span>  
 
* <span data-ttu-id="4ff50-117">It can bulk import more than a terabyte of data within an hour by using a scale-out architecture.</span><span class="sxs-lookup"><span data-stu-id="4ff50-117">It can bulk import more than a terabyte of data within an hour by using a scale-out architecture.</span></span>  

* <span data-ttu-id="4ff50-118">It can bulk update existing data in Azure Cosmos DB containers as patches.</span><span class="sxs-lookup"><span data-stu-id="4ff50-118">It can bulk update existing data in Azure Cosmos DB containers as patches.</span></span> 
 
## <a name="how-does-the-bulk-executor-operate"></a><span data-ttu-id="4ff50-119">How does the Bulk Executor operate?</span><span class="sxs-lookup"><span data-stu-id="4ff50-119">How does the Bulk Executor operate?</span></span> 

<span data-ttu-id="4ff50-120">When a bulk operation to import or update documents is triggered with a batch of entities, they are initially shuffled into buckets corresponding to their Azure Cosmos DB partition key range.</span><span class="sxs-lookup"><span data-stu-id="4ff50-120">When a bulk operation to import or update documents is triggered with a batch of entities, they are initially shuffled into buckets corresponding to their Azure Cosmos DB partition key range.</span></span> <span data-ttu-id="4ff50-121">Within each bucket that corresponds to a partition key range, they are broken down into mini-batches and each mini-batch act as a payload that is committed on the server-side.</span><span class="sxs-lookup"><span data-stu-id="4ff50-121">Within each bucket that corresponds to a partition key range, they are broken down into mini-batches and each mini-batch act as a payload that is committed on the server-side.</span></span> <span data-ttu-id="4ff50-122">The bulk executor library has built in optimizations for concurrent execution of these mini-batches both within and across partition key ranges.</span><span class="sxs-lookup"><span data-stu-id="4ff50-122">The bulk executor library has built in optimizations for concurrent execution of these mini-batches both within and across partition key ranges.</span></span> <span data-ttu-id="4ff50-123">Following image illustrates how bulk executor batches data into different partition keys:</span><span class="sxs-lookup"><span data-stu-id="4ff50-123">Following image illustrates how bulk executor batches data into different partition keys:</span></span>  

![Bulk executor architecture](./media/bulk-executor-overview/bulk-executor-architecture.png)

<span data-ttu-id="4ff50-125">The Bulk Executor library makes sure to maximally utilize the throughput allocated to a collection.</span><span class="sxs-lookup"><span data-stu-id="4ff50-125">The Bulk Executor library makes sure to maximally utilize the throughput allocated to a collection.</span></span> <span data-ttu-id="4ff50-126">It uses an [AIMD-style congestion control mechanism](https://tools.ietf.org/html/rfc5681) for each Azure Cosmos DB partition key range to efficiently handle rate limiting and timeouts.</span><span class="sxs-lookup"><span data-stu-id="4ff50-126">It uses an [AIMD-style congestion control mechanism](https://tools.ietf.org/html/rfc5681) for each Azure Cosmos DB partition key range to efficiently handle rate limiting and timeouts.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="4ff50-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="4ff50-127">Next Steps</span></span> 
  
* <span data-ttu-id="4ff50-128">Learn more by trying out the sample applications consuming the Bulk Executor library in [.NET](bulk-executor-dot-net.md) and [Java](bulk-executor-java.md).</span><span class="sxs-lookup"><span data-stu-id="4ff50-128">Learn more by trying out the sample applications consuming the Bulk Executor library in [.NET](bulk-executor-dot-net.md) and [Java](bulk-executor-java.md).</span></span>  
* <span data-ttu-id="4ff50-129">Check out the bulk executor SDK information and release notes in [.NET](sql-api-sdk-bulk-executor-dot-net.md) and [Java](sql-api-sdk-bulk-executor-java.md).</span><span class="sxs-lookup"><span data-stu-id="4ff50-129">Check out the bulk executor SDK information and release notes in [.NET](sql-api-sdk-bulk-executor-dot-net.md) and [Java](sql-api-sdk-bulk-executor-java.md).</span></span>
* <span data-ttu-id="4ff50-130">The Bulk Executor library is integrated into the Cosmos DB Spark connector, to learn more, see [Azure Cosmos DB Spark connector](spark-connector.md) article.</span><span class="sxs-lookup"><span data-stu-id="4ff50-130">The Bulk Executor library is integrated into the Cosmos DB Spark connector, to learn more, see [Azure Cosmos DB Spark connector](spark-connector.md) article.</span></span>  
* <span data-ttu-id="4ff50-131">The bulk executor library is also integrated into a new version of [Azure Cosmos DB connector](https://aka.ms/bulkexecutor-adf-v2) for Azure Data Factory to copy data.</span><span class="sxs-lookup"><span data-stu-id="4ff50-131">The bulk executor library is also integrated into a new version of [Azure Cosmos DB connector](https://aka.ms/bulkexecutor-adf-v2) for Azure Data Factory to copy data.</span></span>
