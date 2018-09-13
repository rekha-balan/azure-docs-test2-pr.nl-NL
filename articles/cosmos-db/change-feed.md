---
title: Working with the change feed support in Azure Cosmos DB | Microsoft Docs
description: Use Azure Cosmos DB change feed support to track changes in documents and perform event-based processing like triggers and keeping caches and analytics systems up-to-date.
keywords: change feed
services: cosmos-db
author: rafats
manager: kfile
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: conceptual
ms.date: 03/26/2018
ms.author: rafats
ms.openlocfilehash: 3aeef8aff33cf19eb8f9c7037c56d04e38b9ed23
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871646"
---
# <a name="working-with-the-change-feed-support-in-azure-cosmos-db"></a><span data-ttu-id="fc019-104">Working with the change feed support in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="fc019-104">Working with the change feed support in Azure Cosmos DB</span></span>

<span data-ttu-id="fc019-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database, well-suited for IoT, gaming, retail, and operational logging applications.</span><span class="sxs-lookup"><span data-stu-id="fc019-105">[Azure Cosmos DB](../cosmos-db/introduction.md) is a fast and flexible globally replicated database, well-suited for IoT, gaming, retail, and operational logging applications.</span></span> <span data-ttu-id="fc019-106">A common design pattern in these applications is to use changes to the data to kick off additional actions.</span><span class="sxs-lookup"><span data-stu-id="fc019-106">A common design pattern in these applications is to use changes to the data to kick off additional actions.</span></span> <span data-ttu-id="fc019-107">These additional actions could be any of the following:</span><span class="sxs-lookup"><span data-stu-id="fc019-107">These additional actions could be any of the following:</span></span> 

* <span data-ttu-id="fc019-108">Triggering a notification or a call to an API when a document is inserted or modified.</span><span class="sxs-lookup"><span data-stu-id="fc019-108">Triggering a notification or a call to an API when a document is inserted or modified.</span></span>
* <span data-ttu-id="fc019-109">Stream processing for IoT or performing analytics.</span><span class="sxs-lookup"><span data-stu-id="fc019-109">Stream processing for IoT or performing analytics.</span></span>
* <span data-ttu-id="fc019-110">Additional data movement by synchronizing with a cache, search engine, or data warehouse, or archiving data to cold storage.</span><span class="sxs-lookup"><span data-stu-id="fc019-110">Additional data movement by synchronizing with a cache, search engine, or data warehouse, or archiving data to cold storage.</span></span>

<span data-ttu-id="fc019-111">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="fc019-111">The **change feed support** in Azure Cosmos DB enables you to build efficient and scalable solutions for each of these patterns, as shown in the following image:</span></span>

![Using Azure Cosmos DB change feed to power real-time analytics and event-driven computing scenarios](./media/change-feed/changefeedoverview.png)

> [!NOTE]
> <span data-ttu-id="fc019-113">Change feed support is provided for all data models and containers in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fc019-113">Change feed support is provided for all data models and containers in Azure Cosmos DB.</span></span> <span data-ttu-id="fc019-114">However, the change feed is read using the SQL client and serializes items into JSON format.</span><span class="sxs-lookup"><span data-stu-id="fc019-114">However, the change feed is read using the SQL client and serializes items into JSON format.</span></span> <span data-ttu-id="fc019-115">Because of the JSON formatting, MongoDB clients will experience a mismatch between BSON formatted documents and the JSON formatted change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-115">Because of the JSON formatting, MongoDB clients will experience a mismatch between BSON formatted documents and the JSON formatted change feed.</span></span>

## <a name="how-does-change-feed-work"></a><span data-ttu-id="fc019-116">How does change feed work?</span><span class="sxs-lookup"><span data-stu-id="fc019-116">How does change feed work?</span></span>

<span data-ttu-id="fc019-117">Change feed support in Azure Cosmos DB works by listening to an Azure Cosmos DB collection for any changes.</span><span class="sxs-lookup"><span data-stu-id="fc019-117">Change feed support in Azure Cosmos DB works by listening to an Azure Cosmos DB collection for any changes.</span></span> <span data-ttu-id="fc019-118">It then outputs the sorted list of documents that were changed in the order in which they were modified.</span><span class="sxs-lookup"><span data-stu-id="fc019-118">It then outputs the sorted list of documents that were changed in the order in which they were modified.</span></span> <span data-ttu-id="fc019-119">The changes are persisted, can be processed asynchronously and incrementally, and the output can be distributed across one or more consumers for parallel processing.</span><span class="sxs-lookup"><span data-stu-id="fc019-119">The changes are persisted, can be processed asynchronously and incrementally, and the output can be distributed across one or more consumers for parallel processing.</span></span> 

<span data-ttu-id="fc019-120">You can read the change feed in three different ways, as discussed later in this article:</span><span class="sxs-lookup"><span data-stu-id="fc019-120">You can read the change feed in three different ways, as discussed later in this article:</span></span>

*   [<span data-ttu-id="fc019-121">Using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fc019-121">Using Azure Functions</span></span>](#azure-functions)
*   [<span data-ttu-id="fc019-122">Using the Azure Cosmos DB SDK</span><span class="sxs-lookup"><span data-stu-id="fc019-122">Using the Azure Cosmos DB SDK</span></span>](#sql-sdk)
*   [<span data-ttu-id="fc019-123">Using the Azure Cosmos DB change feed processor library</span><span class="sxs-lookup"><span data-stu-id="fc019-123">Using the Azure Cosmos DB change feed processor library</span></span>](#change-feed-processor)

<span data-ttu-id="fc019-124">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="fc019-124">The change feed is available for each partition key range within the document collection, and thus can be distributed across one or more consumers for parallel processing as shown in the following image.</span></span>

![Distributed processing of Azure Cosmos DB change feed](./media/change-feed/changefeedvisual.png)

<span data-ttu-id="fc019-126">Additional details:</span><span class="sxs-lookup"><span data-stu-id="fc019-126">Additional details:</span></span>
* <span data-ttu-id="fc019-127">Change feed is enabled by default for all accounts.</span><span class="sxs-lookup"><span data-stu-id="fc019-127">Change feed is enabled by default for all accounts.</span></span>
* <span data-ttu-id="fc019-128">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other Azure Cosmos DB operation.</span><span class="sxs-lookup"><span data-stu-id="fc019-128">You can use your [provisioned throughput](request-units.md) in your write region or any [read region](distribute-data-globally.md) to read from the change feed, just like any other Azure Cosmos DB operation.</span></span>
* <span data-ttu-id="fc019-129">The change feed includes inserts and update operations made to documents within the collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-129">The change feed includes inserts and update operations made to documents within the collection.</span></span> <span data-ttu-id="fc019-130">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span><span class="sxs-lookup"><span data-stu-id="fc019-130">You can capture deletes by setting a "soft-delete" flag within your documents in place of deletes.</span></span> <span data-ttu-id="fc019-131">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span><span class="sxs-lookup"><span data-stu-id="fc019-131">Alternatively, you can set a finite expiration period for your documents via the [TTL capability](time-to-live.md), for example, 24 hours and use the value of that property to capture deletes.</span></span> <span data-ttu-id="fc019-132">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span><span class="sxs-lookup"><span data-stu-id="fc019-132">With this solution, you have to process changes within a shorter time interval than the TTL expiration period.</span></span>
* <span data-ttu-id="fc019-133">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span><span class="sxs-lookup"><span data-stu-id="fc019-133">Each change to a document appears exactly once in the change feed, and clients manage their checkpointing logic.</span></span> <span data-ttu-id="fc019-134">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span><span class="sxs-lookup"><span data-stu-id="fc019-134">The change feed processor library provides automatic checkpointing and "at least once" semantics.</span></span>
* <span data-ttu-id="fc019-135">Only the most recent change for a given document is included in the change log.</span><span class="sxs-lookup"><span data-stu-id="fc019-135">Only the most recent change for a given document is included in the change log.</span></span> <span data-ttu-id="fc019-136">Intermediate changes may not be available.</span><span class="sxs-lookup"><span data-stu-id="fc019-136">Intermediate changes may not be available.</span></span>
* <span data-ttu-id="fc019-137">The change feed is sorted by order of modification within each partition key value.</span><span class="sxs-lookup"><span data-stu-id="fc019-137">The change feed is sorted by order of modification within each partition key value.</span></span> <span data-ttu-id="fc019-138">There is no guaranteed order across partition-key values.</span><span class="sxs-lookup"><span data-stu-id="fc019-138">There is no guaranteed order across partition-key values.</span></span>
* <span data-ttu-id="fc019-139">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span><span class="sxs-lookup"><span data-stu-id="fc019-139">Changes can be synchronized from any point-in-time, that is, there is no fixed data retention period for which changes are available.</span></span>
* <span data-ttu-id="fc019-140">Changes are available in chunks of partition key ranges.</span><span class="sxs-lookup"><span data-stu-id="fc019-140">Changes are available in chunks of partition key ranges.</span></span> <span data-ttu-id="fc019-141">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span><span class="sxs-lookup"><span data-stu-id="fc019-141">This capability allows changes from large collections to be processed in parallel by multiple consumers/servers.</span></span>
* <span data-ttu-id="fc019-142">Applications can request multiple change feeds simultaneously on the same collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-142">Applications can request multiple change feeds simultaneously on the same collection.</span></span>
* <span data-ttu-id="fc019-143">ChangeFeedOptions.StartTime can be used to provide an initial starting point, for example, to find the continuation token corresponding to given clock time.</span><span class="sxs-lookup"><span data-stu-id="fc019-143">ChangeFeedOptions.StartTime can be used to provide an initial starting point, for example, to find the continuation token corresponding to given clock time.</span></span> <span data-ttu-id="fc019-144">The ContinuationToken, if specified, wins over the StartTime and StartFromBeginning values.</span><span class="sxs-lookup"><span data-stu-id="fc019-144">The ContinuationToken, if specified, wins over the StartTime and StartFromBeginning values.</span></span> <span data-ttu-id="fc019-145">The precision of ChangeFeedOptions.StartTime is ~5 secs.</span><span class="sxs-lookup"><span data-stu-id="fc019-145">The precision of ChangeFeedOptions.StartTime is ~5 secs.</span></span> 

## <a name="use-cases-and-scenarios"></a><span data-ttu-id="fc019-146">Use cases and scenarios</span><span class="sxs-lookup"><span data-stu-id="fc019-146">Use cases and scenarios</span></span>

<span data-ttu-id="fc019-147">The change feed enables efficient processing of large datasets with a high volume of writes, and offers an alternative to querying an entire dataset to identify what has changed.</span><span class="sxs-lookup"><span data-stu-id="fc019-147">The change feed enables efficient processing of large datasets with a high volume of writes, and offers an alternative to querying an entire dataset to identify what has changed.</span></span> 

<span data-ttu-id="fc019-148">For example, with a change feed, you can perform the following tasks efficiently:</span><span class="sxs-lookup"><span data-stu-id="fc019-148">For example, with a change feed, you can perform the following tasks efficiently:</span></span>

* <span data-ttu-id="fc019-149">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fc019-149">Update a cache, search index, or a data warehouse with data stored in Azure Cosmos DB.</span></span>
* <span data-ttu-id="fc019-150">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-150">Implement application-level data tiering and archival, that is, store "hot data" in Azure Cosmos DB, and age out "cold data" to [Azure Blob Storage](../storage/common/storage-introduction.md) or [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md).</span></span>
* <span data-ttu-id="fc019-151">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span><span class="sxs-lookup"><span data-stu-id="fc019-151">Perform zero down-time migrations to another Azure Cosmos DB account with a different partitioning scheme.</span></span>
* <span data-ttu-id="fc019-152">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fc019-152">Implement [lambda pipelines on Azure](https://blogs.technet.microsoft.com/msuspartner/2016/01/27/azure-partner-community-big-data-advanced-analytics-and-lambda-architecture/) with Azure Cosmos DB.</span></span> <span data-ttu-id="fc019-153">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span><span class="sxs-lookup"><span data-stu-id="fc019-153">Azure Cosmos DB provides a scalable database solution that can handle both ingestion and query, and implement lambda architectures with low TCO.</span></span> 
* <span data-ttu-id="fc019-154">Receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/storm/apache-storm-overview.md), or [Apache Spark](../hdinsight/spark/apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-154">Receive and store event data from devices, sensors, infrastructure, and applications, and process these events in real time with [Azure Stream Analytics](../stream-analytics/stream-analytics-documentdb-output.md), [Apache Storm](../hdinsight/storm/apache-storm-overview.md), or [Apache Spark](../hdinsight/spark/apache-spark-overview.md).</span></span> 

<span data-ttu-id="fc019-155">The following image shows how lambda pipelines that both ingest and query using Azure Cosmos DB can use change feed support:</span><span class="sxs-lookup"><span data-stu-id="fc019-155">The following image shows how lambda pipelines that both ingest and query using Azure Cosmos DB can use change feed support:</span></span> 

![Azure Cosmos DB-based lambda pipeline for ingestion and query](./media/change-feed/lambda.png)

<span data-ttu-id="fc019-157">Also, within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](#azure-functions).</span><span class="sxs-lookup"><span data-stu-id="fc019-157">Also, within your [serverless](http://azure.com/serverless) web and mobile apps, you can track events such as changes to your customer's profile, preferences, or location to trigger certain actions like sending push notifications to their devices using [Azure Functions](#azure-functions).</span></span> <span data-ttu-id="fc019-158">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span><span class="sxs-lookup"><span data-stu-id="fc019-158">If you're using Azure Cosmos DB to build a game, you can, for example, use change feed to implement real-time leaderboards based on scores from completed games.</span></span>

<a id="azure-functions"></a>
## <a name="using-azure-functions"></a><span data-ttu-id="fc019-159">Using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="fc019-159">Using Azure Functions</span></span> 

<span data-ttu-id="fc019-160">If you're using Azure Functions, the simplest way to connect to an Azure Cosmos DB change feed is to add an Azure Cosmos DB trigger to your Azure Functions app.</span><span class="sxs-lookup"><span data-stu-id="fc019-160">If you're using Azure Functions, the simplest way to connect to an Azure Cosmos DB change feed is to add an Azure Cosmos DB trigger to your Azure Functions app.</span></span> <span data-ttu-id="fc019-161">When you create an Azure Cosmos DB trigger in an Azure Functions app, you select the Azure Cosmos DB collection to connect to, and the function is triggered whenever a change to the collection is made.</span><span class="sxs-lookup"><span data-stu-id="fc019-161">When you create an Azure Cosmos DB trigger in an Azure Functions app, you select the Azure Cosmos DB collection to connect to, and the function is triggered whenever a change to the collection is made.</span></span> 

<span data-ttu-id="fc019-162">Triggers can be created in the Azure Functions portal, in the Azure Cosmos DB portal, or programmatically.</span><span class="sxs-lookup"><span data-stu-id="fc019-162">Triggers can be created in the Azure Functions portal, in the Azure Cosmos DB portal, or programmatically.</span></span> <span data-ttu-id="fc019-163">For more information, see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-163">For more information, see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md).</span></span>

<a id="sql-sdk"></a>
## <a name="using-the-sdk"></a><span data-ttu-id="fc019-164">Using the SDK</span><span class="sxs-lookup"><span data-stu-id="fc019-164">Using the SDK</span></span>

<span data-ttu-id="fc019-165">The [SQL SDK](sql-api-sdk-dotnet.md) for Azure Cosmos DB gives you all the power to read and manage a change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-165">The [SQL SDK](sql-api-sdk-dotnet.md) for Azure Cosmos DB gives you all the power to read and manage a change feed.</span></span> <span data-ttu-id="fc019-166">But with great power comes lots of responsibilities, too.</span><span class="sxs-lookup"><span data-stu-id="fc019-166">But with great power comes lots of responsibilities, too.</span></span> <span data-ttu-id="fc019-167">If you want to manage checkpoints, deal with document sequence numbers, and have granular control over partition keys, then using the SDK may be the right approach.</span><span class="sxs-lookup"><span data-stu-id="fc019-167">If you want to manage checkpoints, deal with document sequence numbers, and have granular control over partition keys, then using the SDK may be the right approach.</span></span>

<span data-ttu-id="fc019-168">This section walks through how to use the SQL SDK to work with a change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-168">This section walks through how to use the SQL SDK to work with a change feed.</span></span>

1. <span data-ttu-id="fc019-169">Start by reading the following resources from appconfig.</span><span class="sxs-lookup"><span data-stu-id="fc019-169">Start by reading the following resources from appconfig.</span></span> <span data-ttu-id="fc019-170">Instructions on retrieving the endpoint and authorization key are available in [Update your connection string](create-sql-api-dotnet.md#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="fc019-170">Instructions on retrieving the endpoint and authorization key are available in [Update your connection string](create-sql-api-dotnet.md#update-your-connection-string).</span></span>

    ``` csharp
    DocumentClient client;
    string DatabaseName = ConfigurationManager.AppSettings["database"];
    string CollectionName = ConfigurationManager.AppSettings["collection"];
    string endpointUrl = ConfigurationManager.AppSettings["endpoint"];
    string authorizationKey = ConfigurationManager.AppSettings["authKey"];
    ```

2. <span data-ttu-id="fc019-171">Create the client as follows:</span><span class="sxs-lookup"><span data-stu-id="fc019-171">Create the client as follows:</span></span>

    ```csharp
    using (client = new DocumentClient(new Uri(endpointUrl), authorizationKey,
    new ConnectionPolicy { ConnectionMode = ConnectionMode.Direct, ConnectionProtocol = Protocol.Tcp }))
    {
    }
    ```

3. <span data-ttu-id="fc019-172">Get the partition key ranges:</span><span class="sxs-lookup"><span data-stu-id="fc019-172">Get the partition key ranges:</span></span>

    ```csharp
    FeedResponse pkRangesResponse = await client.ReadPartitionKeyRangeFeedAsync(
        collectionUri,
        new FeedOptions
            {RequestContinuation = pkRangesResponseContinuation });
     
    partitionKeyRanges.AddRange(pkRangesResponse);
    pkRangesResponseContinuation = pkRangesResponse.ResponseContinuation;
    ```

4. <span data-ttu-id="fc019-173">Call ExecuteNextAsync for every partition key range:</span><span class="sxs-lookup"><span data-stu-id="fc019-173">Call ExecuteNextAsync for every partition key range:</span></span>

    ```csharp
    foreach (PartitionKeyRange pkRange in partitionKeyRanges){
        string continuation = null;
        checkpoints.TryGetValue(pkRange.Id, out continuation);
        IDocumentQuery<Document> query = client.CreateDocumentChangeFeedQuery(
            collectionUri,
            new ChangeFeedOptions
            {
                PartitionKeyRangeId = pkRange.Id,
                StartFromBeginning = true,
                RequestContinuation = continuation,
                MaxItemCount = -1,
                // Set reading time: only show change feed results modified since StartTime
                StartTime = DateTime.Now - TimeSpan.FromSeconds(30)
            });
        while (query.HasMoreResults)
            {
                FeedResponse<dynamic> readChangesResponse = query.ExecuteNextAsync<dynamic>().Result;
    
                foreach (dynamic changedDocument in readChangesResponse)
                    {
                         Console.WriteLine("document: {0}", changedDocument);
                    }
                checkpoints[pkRange.Id] = readChangesResponse.ResponseContinuation;
            }
    }
    ```

> [!NOTE]
> <span data-ttu-id="fc019-174">Instead of `ChangeFeedOptions.PartitionKeyRangeId`, you can use `ChangeFeedOptions.PartitionKey` to specify a single partition key for which to get a change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-174">Instead of `ChangeFeedOptions.PartitionKeyRangeId`, you can use `ChangeFeedOptions.PartitionKey` to specify a single partition key for which to get a change feed.</span></span> <span data-ttu-id="fc019-175">For example, `PartitionKey = new PartitionKey("D8CFA2FD-486A-4F3E-8EA6-F3AA94E5BD44")`.</span><span class="sxs-lookup"><span data-stu-id="fc019-175">For example, `PartitionKey = new PartitionKey("D8CFA2FD-486A-4F3E-8EA6-F3AA94E5BD44")`.</span></span>
> 
>

<span data-ttu-id="fc019-176">If you have multiple readers, you can use **ChangeFeedOptions** to distribute read load to different threads or different clients.</span><span class="sxs-lookup"><span data-stu-id="fc019-176">If you have multiple readers, you can use **ChangeFeedOptions** to distribute read load to different threads or different clients.</span></span>

<span data-ttu-id="fc019-177">And that's it, with these few lines of code you can start reading the change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-177">And that's it, with these few lines of code you can start reading the change feed.</span></span> <span data-ttu-id="fc019-178">You can get the complete code used in this article from the [GitHub repo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed).</span><span class="sxs-lookup"><span data-stu-id="fc019-178">You can get the complete code used in this article from the [GitHub repo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeed).</span></span>

<span data-ttu-id="fc019-179">In the code in step 4 above, the **ResponseContinuation** in the last line has the last logical sequence number (LSN) of the document, which you will use the next time you read new documents after this sequence number.</span><span class="sxs-lookup"><span data-stu-id="fc019-179">In the code in step 4 above, the **ResponseContinuation** in the last line has the last logical sequence number (LSN) of the document, which you will use the next time you read new documents after this sequence number.</span></span> <span data-ttu-id="fc019-180">By using the **StartTime** of the **ChangeFeedOption** you can widen your net to get the documents.</span><span class="sxs-lookup"><span data-stu-id="fc019-180">By using the **StartTime** of the **ChangeFeedOption** you can widen your net to get the documents.</span></span> <span data-ttu-id="fc019-181">So, if your **ResponseContinuation** is null, but your **StartTime** goes back in time then you will get all the documents that changed since the **StartTime**.</span><span class="sxs-lookup"><span data-stu-id="fc019-181">So, if your **ResponseContinuation** is null, but your **StartTime** goes back in time then you will get all the documents that changed since the **StartTime**.</span></span> <span data-ttu-id="fc019-182">But, if your **ResponseContinuation** has a value then system will get you all the documents since that LSN.</span><span class="sxs-lookup"><span data-stu-id="fc019-182">But, if your **ResponseContinuation** has a value then system will get you all the documents since that LSN.</span></span>

<span data-ttu-id="fc019-183">So, your checkpoint array is just keeping the LSN for each partition.</span><span class="sxs-lookup"><span data-stu-id="fc019-183">So, your checkpoint array is just keeping the LSN for each partition.</span></span> <span data-ttu-id="fc019-184">But if you don’t want to deal with the partitions, checkpoints, LSN, start time, etc. the simpler option is to use the change feed processor library.</span><span class="sxs-lookup"><span data-stu-id="fc019-184">But if you don’t want to deal with the partitions, checkpoints, LSN, start time, etc. the simpler option is to use the change feed processor library.</span></span>

<a id="change-feed-processor"></a>
## <a name="using-the-change-feed-processor-library"></a><span data-ttu-id="fc019-185">Using the change feed processor library</span><span class="sxs-lookup"><span data-stu-id="fc019-185">Using the change feed processor library</span></span> 

<span data-ttu-id="fc019-186">The [Azure Cosmos DB change feed processor library](https://docs.microsoft.com/azure/cosmos-db/sql-api-sdk-dotnet-changefeed) can help you easily distribute event processing across multiple consumers.</span><span class="sxs-lookup"><span data-stu-id="fc019-186">The [Azure Cosmos DB change feed processor library](https://docs.microsoft.com/azure/cosmos-db/sql-api-sdk-dotnet-changefeed) can help you easily distribute event processing across multiple consumers.</span></span> <span data-ttu-id="fc019-187">This library simplifies reading changes across partitions and multiple threads working in parallel.</span><span class="sxs-lookup"><span data-stu-id="fc019-187">This library simplifies reading changes across partitions and multiple threads working in parallel.</span></span>

<span data-ttu-id="fc019-188">The main benefit of change feed processor library is that you don’t have to manage each partition and continuation token and you don’t have to poll each collection manually.</span><span class="sxs-lookup"><span data-stu-id="fc019-188">The main benefit of change feed processor library is that you don’t have to manage each partition and continuation token and you don’t have to poll each collection manually.</span></span>

<span data-ttu-id="fc019-189">The change feed processor library simplifies reading changes across partitions and multiple threads working in parallel.</span><span class="sxs-lookup"><span data-stu-id="fc019-189">The change feed processor library simplifies reading changes across partitions and multiple threads working in parallel.</span></span>  <span data-ttu-id="fc019-190">It automatically manages reading changes across partitions using a lease mechanism.</span><span class="sxs-lookup"><span data-stu-id="fc019-190">It automatically manages reading changes across partitions using a lease mechanism.</span></span> <span data-ttu-id="fc019-191">As you can see in the following image, if you start two clients that are using the change feed processor library, they divide the work among themselves.</span><span class="sxs-lookup"><span data-stu-id="fc019-191">As you can see in the following image, if you start two clients that are using the change feed processor library, they divide the work among themselves.</span></span> <span data-ttu-id="fc019-192">As you continue to increase the clients, they keep dividing the work among themselves.</span><span class="sxs-lookup"><span data-stu-id="fc019-192">As you continue to increase the clients, they keep dividing the work among themselves.</span></span>

![Distributed processing of Azure Cosmos DB change feed](./media/change-feed/change-feed-output.png)

<span data-ttu-id="fc019-194">The left client was started first and it started monitoring all the partitions, then the second client was started, and then the first let go of some of the leases to second client.</span><span class="sxs-lookup"><span data-stu-id="fc019-194">The left client was started first and it started monitoring all the partitions, then the second client was started, and then the first let go of some of the leases to second client.</span></span> <span data-ttu-id="fc019-195">As you can see this is the nice way to distribute the work between different machines and clients.</span><span class="sxs-lookup"><span data-stu-id="fc019-195">As you can see this is the nice way to distribute the work between different machines and clients.</span></span>

<span data-ttu-id="fc019-196">Note that if you have two serverless Azure funtions monitoring the same collection and using the same lease then the two functions may get different documents depending upon how the processor library decides to processs the partitions.</span><span class="sxs-lookup"><span data-stu-id="fc019-196">Note that if you have two serverless Azure funtions monitoring the same collection and using the same lease then the two functions may get different documents depending upon how the processor library decides to processs the partitions.</span></span>

<a id="understand-cf"></a>
### <a name="understanding-the-change-feed-processor-library"></a><span data-ttu-id="fc019-197">Understanding the change feed processor library</span><span class="sxs-lookup"><span data-stu-id="fc019-197">Understanding the change feed processor library</span></span>

<span data-ttu-id="fc019-198">There are four main components of implementing the change feed processor library: the monitored collection, the lease collection, the processor host, and the consumers.</span><span class="sxs-lookup"><span data-stu-id="fc019-198">There are four main components of implementing the change feed processor library: the monitored collection, the lease collection, the processor host, and the consumers.</span></span> 

> [!WARNING]
> <span data-ttu-id="fc019-199">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fc019-199">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="fc019-200">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span><span class="sxs-lookup"><span data-stu-id="fc019-200">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

<span data-ttu-id="fc019-201">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span><span class="sxs-lookup"><span data-stu-id="fc019-201">**Monitored Collection:** The monitored collection is the data from which the change feed is generated.</span></span> <span data-ttu-id="fc019-202">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-202">Any inserts and changes to the monitored collection are reflected in the change feed of the collection.</span></span> 

<span data-ttu-id="fc019-203">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span><span class="sxs-lookup"><span data-stu-id="fc019-203">**Lease Collection:** The lease collection coordinates processing the change feed across multiple workers.</span></span> <span data-ttu-id="fc019-204">A separate collection is used to store the leases with one lease per partition.</span><span class="sxs-lookup"><span data-stu-id="fc019-204">A separate collection is used to store the leases with one lease per partition.</span></span> <span data-ttu-id="fc019-205">It is advantageous to store this lease collection on a different account with the write region closer to where the change feed processor is running.</span><span class="sxs-lookup"><span data-stu-id="fc019-205">It is advantageous to store this lease collection on a different account with the write region closer to where the change feed processor is running.</span></span> <span data-ttu-id="fc019-206">A lease object contains the following attributes:</span><span class="sxs-lookup"><span data-stu-id="fc019-206">A lease object contains the following attributes:</span></span> 
* <span data-ttu-id="fc019-207">Owner: Specifies the host that owns the lease</span><span class="sxs-lookup"><span data-stu-id="fc019-207">Owner: Specifies the host that owns the lease</span></span>
* <span data-ttu-id="fc019-208">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span><span class="sxs-lookup"><span data-stu-id="fc019-208">Continuation: Specifies the position (continuation token) in the change feed for a particular partition</span></span>
* <span data-ttu-id="fc019-209">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span><span class="sxs-lookup"><span data-stu-id="fc019-209">Timestamp: Last time lease was updated; the timestamp can be used to check whether the lease is considered expired</span></span> 

<span data-ttu-id="fc019-210">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span><span class="sxs-lookup"><span data-stu-id="fc019-210">**Processor Host:** Each host determines how many partitions to process based on how many other instances of hosts have active leases.</span></span> 
1.  <span data-ttu-id="fc019-211">When a host starts up, it acquires leases to balance the workload across all hosts.</span><span class="sxs-lookup"><span data-stu-id="fc019-211">When a host starts up, it acquires leases to balance the workload across all hosts.</span></span> <span data-ttu-id="fc019-212">A host periodically renews leases, so leases remain active.</span><span class="sxs-lookup"><span data-stu-id="fc019-212">A host periodically renews leases, so leases remain active.</span></span> 
2.  <span data-ttu-id="fc019-213">A host checkpoints the last continuation token to its lease for each read.</span><span class="sxs-lookup"><span data-stu-id="fc019-213">A host checkpoints the last continuation token to its lease for each read.</span></span> <span data-ttu-id="fc019-214">To ensure concurrency safety, a host checks the ETag for each lease update.</span><span class="sxs-lookup"><span data-stu-id="fc019-214">To ensure concurrency safety, a host checks the ETag for each lease update.</span></span> <span data-ttu-id="fc019-215">Other checkpoint strategies are also supported.</span><span class="sxs-lookup"><span data-stu-id="fc019-215">Other checkpoint strategies are also supported.</span></span>  
3.  <span data-ttu-id="fc019-216">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span><span class="sxs-lookup"><span data-stu-id="fc019-216">Upon shutdown, a host releases all leases but keeps the continuation information, so it can resume reading from the stored checkpoint later.</span></span> 

<span data-ttu-id="fc019-217">At this time the number of hosts cannot be greater than the number of partitions (leases).</span><span class="sxs-lookup"><span data-stu-id="fc019-217">At this time the number of hosts cannot be greater than the number of partitions (leases).</span></span>

<span data-ttu-id="fc019-218">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span><span class="sxs-lookup"><span data-stu-id="fc019-218">**Consumers:** Consumers, or workers, are threads that perform the change feed processing initiated by each host.</span></span> <span data-ttu-id="fc019-219">Each processor host can have multiple consumers.</span><span class="sxs-lookup"><span data-stu-id="fc019-219">Each processor host can have multiple consumers.</span></span> <span data-ttu-id="fc019-220">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span><span class="sxs-lookup"><span data-stu-id="fc019-220">Each consumer reads the change feed from the partition it is assigned to and notifies its host of changes and expired leases.</span></span>

<span data-ttu-id="fc019-221">To further understand how these four elements of change feed processor work together, let's look at an example in the following diagram.</span><span class="sxs-lookup"><span data-stu-id="fc019-221">To further understand how these four elements of change feed processor work together, let's look at an example in the following diagram.</span></span> <span data-ttu-id="fc019-222">The monitored collection stores documents and uses the "city" as the partition key.</span><span class="sxs-lookup"><span data-stu-id="fc019-222">The monitored collection stores documents and uses the "city" as the partition key.</span></span> <span data-ttu-id="fc019-223">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span><span class="sxs-lookup"><span data-stu-id="fc019-223">We see that the blue partition contains documents with the "city" field from "A-E" and so on.</span></span> <span data-ttu-id="fc019-224">There are two hosts, each with two consumers reading from the four partitions in parallel.</span><span class="sxs-lookup"><span data-stu-id="fc019-224">There are two hosts, each with two consumers reading from the four partitions in parallel.</span></span> <span data-ttu-id="fc019-225">The arrows show the consumers reading from a specific spot in the change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-225">The arrows show the consumers reading from a specific spot in the change feed.</span></span> <span data-ttu-id="fc019-226">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-226">In the first partition, the darker blue represents unread changes while the light blue represents the already read changes on the change feed.</span></span> <span data-ttu-id="fc019-227">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span><span class="sxs-lookup"><span data-stu-id="fc019-227">The hosts use the lease collection to store a "continuation" value to keep track of the current reading position for each consumer.</span></span> 

![Using the Azure Cosmos DB change feed processor host](./media/change-feed/changefeedprocessornew.png)

### <a name="working-with-the-change-feed-processor-library"></a><span data-ttu-id="fc019-229">Working with the change feed processor library</span><span class="sxs-lookup"><span data-stu-id="fc019-229">Working with the change feed processor library</span></span>

<span data-ttu-id="fc019-230">Before installing change feed processor NuGet package, first install:</span><span class="sxs-lookup"><span data-stu-id="fc019-230">Before installing change feed processor NuGet package, first install:</span></span> 

* <span data-ttu-id="fc019-231">Microsoft.Azure.DocumentDB, latest version.</span><span class="sxs-lookup"><span data-stu-id="fc019-231">Microsoft.Azure.DocumentDB, latest version.</span></span>
* <span data-ttu-id="fc019-232">Newtonsoft.Json, latest version</span><span class="sxs-lookup"><span data-stu-id="fc019-232">Newtonsoft.Json, latest version</span></span>

<span data-ttu-id="fc019-233">Then install the [Microsoft.Azure.DocumentDB.ChangeFeedProcessor Nuget package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and include it as a reference.</span><span class="sxs-lookup"><span data-stu-id="fc019-233">Then install the [Microsoft.Azure.DocumentDB.ChangeFeedProcessor Nuget package](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/) and include it as a reference.</span></span>

<span data-ttu-id="fc019-234">To implement the change feed processor library you have to do following:</span><span class="sxs-lookup"><span data-stu-id="fc019-234">To implement the change feed processor library you have to do following:</span></span>

1. <span data-ttu-id="fc019-235">Implement a **DocumentFeedObserver** object, which implements **IChangeFeedObserver**.</span><span class="sxs-lookup"><span data-stu-id="fc019-235">Implement a **DocumentFeedObserver** object, which implements **IChangeFeedObserver**.</span></span>
    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Threading;
    using System.Threading.Tasks;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.ChangeFeedProcessor.FeedProcessing;
    using Microsoft.Azure.Documents.Client;

    /// <summary>
    /// This class implements the IChangeFeedObserver interface and is used to observe 
    /// changes on change feed. ChangeFeedEventHost will create as many instances of 
    /// this class as needed. 
    /// </summary>
    public class DocumentFeedObserver : IChangeFeedObserver
    {
    private static int totalDocs = 0;

        /// <summary>
        /// Initializes a new instance of the <see cref="DocumentFeedObserver" /> class.
        /// Saves input DocumentClient and DocumentCollectionInfo parameters to class fields
        /// </summary>
        /// <param name="client"> Client connected to destination collection </param>
        /// <param name="destCollInfo"> Destination collection information </param>
        public DocumentFeedObserver()
        {
            
        }

        /// <summary>
        /// Called when change feed observer is opened; 
        /// this function prints out observer partition key id. 
        /// </summary>
        /// <param name="context">The context specifying partition for this observer, etc.</param>
        /// <returns>A Task to allow asynchronous execution</returns>
        public Task OpenAsync(IChangeFeedObserverContext context)
        {
            Console.ForegroundColor = ConsoleColor.Magenta;
            Console.WriteLine("Observer opened for partition Key Range: {0}", context.PartitionKeyRangeId);
            return Task.CompletedTask;
        }

        /// <summary>
        /// Called when change feed observer is closed; 
        /// this function prints out observer partition key id and reason for shut down. 
        /// </summary>
        /// <param name="context">The context specifying partition for this observer, etc.</param>
        /// <param name="reason">Specifies the reason the observer is closed.</param>
        /// <returns>A Task to allow asynchronous execution</returns>
        public Task CloseAsync(IChangeFeedObserverContext context, ChangeFeedObserverCloseReason reason)
        {
            Console.ForegroundColor = ConsoleColor.Cyan;
            Console.WriteLine("Observer closed, {0}", context.PartitionKeyRangeId);
            Console.WriteLine("Reason for shutdown, {0}", reason);
            return Task.CompletedTask;
        }

        public Task ProcessChangesAsync(IChangeFeedObserverContext context, IReadOnlyList<Document> docs, CancellationToken cancellationToken)
        {
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("Change feed: PartitionId {0} total {1} doc(s)", context.PartitionKeyRangeId, Interlocked.Add(ref totalDocs, docs.Count));
            foreach (Document doc in docs)
            {
                Console.ForegroundColor = ConsoleColor.Yellow;
                Console.WriteLine(doc.Id.ToString());
            }

            return Task.CompletedTask;
        }
    }
    ```

2. <span data-ttu-id="fc019-236">Implement a **DocumentFeedObserverFactory**, which implements a **IChangeFeedObserverFactory**.</span><span class="sxs-lookup"><span data-stu-id="fc019-236">Implement a **DocumentFeedObserverFactory**, which implements a **IChangeFeedObserverFactory**.</span></span>
    ```csharp
     using Microsoft.Azure.Documents.ChangeFeedProcessor.FeedProcessing;

    /// <summary>
    /// Factory class to create instance of document feed observer. 
    /// </summary>
    public class DocumentFeedObserverFactory : IChangeFeedObserverFactory
    {
        /// <summary>
        /// Initializes a new instance of the <see cref="DocumentFeedObserverFactory" /> class.
        /// Saves input DocumentClient and DocumentCollectionInfo parameters to class fields
        /// </summary>
        public DocumentFeedObserverFactory()
        {
        }

        /// <summary>
        /// Creates document observer instance with client and destination collection information
        /// </summary>
        /// <returns>DocumentFeedObserver with client and destination collection information</returns>
        public IChangeFeedObserver CreateObserver()
        {
            DocumentFeedObserver newObserver = new DocumentFeedObserver();
            return newObserver as IChangeFeedObserver;
        }
    }
    ```

3. <span data-ttu-id="fc019-237">Define *CancellationTokenSource* and *ChangeFeedProcessorBuilder*</span><span class="sxs-lookup"><span data-stu-id="fc019-237">Define *CancellationTokenSource* and *ChangeFeedProcessorBuilder*</span></span>

    ```csharp
    private readonly CancellationTokenSource cancellationTokenSource = new CancellationTokenSource();
    private readonly ChangeFeedProcessorBuilder builder = new ChangeFeedProcessorBuilder();
    ```

5. <span data-ttu-id="fc019-238">build the **ChangeFeedProcessorBuilder** after defining the relevant objects</span><span class="sxs-lookup"><span data-stu-id="fc019-238">build the **ChangeFeedProcessorBuilder** after defining the relevant objects</span></span> 

    ```csharp
            string hostName = Guid.NewGuid().ToString();
      
            // monitored collection info 
            DocumentCollectionInfo documentCollectionInfo = new DocumentCollectionInfo
            {
                Uri = new Uri(this.monitoredUri),
                MasterKey = this.monitoredSecretKey,
                DatabaseName = this.monitoredDbName,
                CollectionName = this.monitoredCollectionName
            };
            
            DocumentCollectionInfo leaseCollectionInfo = new DocumentCollectionInfo
                {
                    Uri = new Uri(this.leaseUri),
                    MasterKey = this.leaseSecretKey,
                    DatabaseName = this.leaseDbName,
                    CollectionName = this.leaseCollectionName
                };
            DocumentFeedObserverFactory docObserverFactory = new DocumentFeedObserverFactory();
            ChangeFeedOptions feedOptions = new ChangeFeedOptions();

            /* ie customize StartFromBeginning so change feed reads from beginning
                can customize MaxItemCount, PartitonKeyRangeId, RequestContinuation, SessionToken and StartFromBeginning
            */

            feedOptions.StartFromBeginning = true;
        
            ChangeFeedProcessorOptions feedProcessorOptions = new ChangeFeedProcessorOptions();

            // ie. customizing lease renewal interval to 15 seconds
            // can customize LeaseRenewInterval, LeaseAcquireInterval, LeaseExpirationInterval, FeedPollDelay 
            feedProcessorOptions.LeaseRenewInterval = TimeSpan.FromSeconds(15);

            this.builder
                .WithHostName(hostName)
                .WithFeedCollection(documentCollectionInfo)
                .WithLeaseCollection(leaseCollectionInfo)
                .WithProcessorOptions (feedProcessorOptions)
                .WithObserverFactory(new DocumentFeedObserverFactory());               
                //.WithObserver<DocumentFeedObserver>();  If no factory then just pass an observer

            var result =  await this.builder.BuildAsync();
            await result.StartAsync();
            Console.Read();
            await result.StopAsync();    
    ```

<span data-ttu-id="fc019-239">That’s it.</span><span class="sxs-lookup"><span data-stu-id="fc019-239">That’s it.</span></span> <span data-ttu-id="fc019-240">After these few steps documents will start showing up into the **DocumentFeedObserver.ProcessChangesAsync** method.</span><span class="sxs-lookup"><span data-stu-id="fc019-240">After these few steps documents will start showing up into the **DocumentFeedObserver.ProcessChangesAsync** method.</span></span>

<span data-ttu-id="fc019-241">Above code is for illustration purpose to show different kind of objects and their interaction.</span><span class="sxs-lookup"><span data-stu-id="fc019-241">Above code is for illustration purpose to show different kind of objects and their interaction.</span></span> <span data-ttu-id="fc019-242">You have to define proper variables and initiate them with correct values.</span><span class="sxs-lookup"><span data-stu-id="fc019-242">You have to define proper variables and initiate them with correct values.</span></span> <span data-ttu-id="fc019-243">You can get the complete code used in this article from the [GitHub repo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeedProcessorV2).</span><span class="sxs-lookup"><span data-stu-id="fc019-243">You can get the complete code used in this article from the [GitHub repo](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeedProcessorV2).</span></span>

> [!NOTE]
> <span data-ttu-id="fc019-244">You should never have a master key in your code or in config file as shown in above code.</span><span class="sxs-lookup"><span data-stu-id="fc019-244">You should never have a master key in your code or in config file as shown in above code.</span></span> <span data-ttu-id="fc019-245">Please see [how to use Key-Vault to retrive the keys](https://sarosh.wordpress.com/2017/11/23/cosmos-db-and-key-vault/).</span><span class="sxs-lookup"><span data-stu-id="fc019-245">Please see [how to use Key-Vault to retrive the keys](https://sarosh.wordpress.com/2017/11/23/cosmos-db-and-key-vault/).</span></span>


## <a name="faq"></a><span data-ttu-id="fc019-246">FAQ</span><span class="sxs-lookup"><span data-stu-id="fc019-246">FAQ</span></span>

### <a name="what-are-the-different-ways-you-can-read-change-feed-and-when-to-use-each-method"></a><span data-ttu-id="fc019-247">What are the different ways you can read Change Feed? and when to use each method?</span><span class="sxs-lookup"><span data-stu-id="fc019-247">What are the different ways you can read Change Feed? and when to use each method?</span></span>

<span data-ttu-id="fc019-248">There are three options for you to read change feed:</span><span class="sxs-lookup"><span data-stu-id="fc019-248">There are three options for you to read change feed:</span></span>

* <span data-ttu-id="fc019-249">**[Using Azure Cosmos DB SQL API .NET SDK](#sql-sdk)**</span><span class="sxs-lookup"><span data-stu-id="fc019-249">**[Using Azure Cosmos DB SQL API .NET SDK](#sql-sdk)**</span></span>
   
   <span data-ttu-id="fc019-250">By using this method, you get low level of control on change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-250">By using this method, you get low level of control on change feed.</span></span> <span data-ttu-id="fc019-251">You can manage the checkpoint, you can access a particular partition key etc. If you have multiple readers, you can use [ChangeFeedOptions](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) to distribute read load to different threads or different clients.</span><span class="sxs-lookup"><span data-stu-id="fc019-251">You can manage the checkpoint, you can access a particular partition key etc. If you have multiple readers, you can use [ChangeFeedOptions](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.changefeedoptions?view=azure-dotnet) to distribute read load to different threads or different clients.</span></span> <span data-ttu-id="fc019-252">.</span><span class="sxs-lookup"><span data-stu-id="fc019-252">.</span></span>

* <span data-ttu-id="fc019-253">**[Using the Azure Cosmos DB change feed processor library](#change-feed-processor)**</span><span class="sxs-lookup"><span data-stu-id="fc019-253">**[Using the Azure Cosmos DB change feed processor library](#change-feed-processor)**</span></span>

   <span data-ttu-id="fc019-254">If you want to outsource lot of complexity of change feed then you can use change feed processor library.</span><span class="sxs-lookup"><span data-stu-id="fc019-254">If you want to outsource lot of complexity of change feed then you can use change feed processor library.</span></span> <span data-ttu-id="fc019-255">This library hides lot of complexity, but still gives you complete control on change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-255">This library hides lot of complexity, but still gives you complete control on change feed.</span></span> <span data-ttu-id="fc019-256">This library follows an [observer pattern](https://en.wikipedia.org/wiki/Observer_pattern), your processing function is called by the SDK.</span><span class="sxs-lookup"><span data-stu-id="fc019-256">This library follows an [observer pattern](https://en.wikipedia.org/wiki/Observer_pattern), your processing function is called by the SDK.</span></span> 

   <span data-ttu-id="fc019-257">If you have a high throughput change feed, you can instantiate multiple clients to read the change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-257">If you have a high throughput change feed, you can instantiate multiple clients to read the change feed.</span></span> <span data-ttu-id="fc019-258">Because you are using "change feed processor library", it will automatically divide the load among different clients.</span><span class="sxs-lookup"><span data-stu-id="fc019-258">Because you are using "change feed processor library", it will automatically divide the load among different clients.</span></span> <span data-ttu-id="fc019-259">You do not have to do anything.</span><span class="sxs-lookup"><span data-stu-id="fc019-259">You do not have to do anything.</span></span> <span data-ttu-id="fc019-260">All the complexity is handled by SDK.</span><span class="sxs-lookup"><span data-stu-id="fc019-260">All the complexity is handled by SDK.</span></span> <span data-ttu-id="fc019-261">However, if you want to have your own load balancer, then you can implement IParitionLoadBalancingStrategy for custom partition strategy.</span><span class="sxs-lookup"><span data-stu-id="fc019-261">However, if you want to have your own load balancer, then you can implement IParitionLoadBalancingStrategy for custom partition strategy.</span></span> <span data-ttu-id="fc019-262">Implement IPartitionProcessor – for custom processing changes on a partition.</span><span class="sxs-lookup"><span data-stu-id="fc019-262">Implement IPartitionProcessor – for custom processing changes on a partition.</span></span> <span data-ttu-id="fc019-263">However, with SDK, you can process a partition range but if you want to process a particular partition key then you have to use SDK for SQL API.</span><span class="sxs-lookup"><span data-stu-id="fc019-263">However, with SDK, you can process a partition range but if you want to process a particular partition key then you have to use SDK for SQL API.</span></span>

* <span data-ttu-id="fc019-264">**[Using Azure Functions](#azure-functions)**</span><span class="sxs-lookup"><span data-stu-id="fc019-264">**[Using Azure Functions](#azure-functions)**</span></span> 
   
   <span data-ttu-id="fc019-265">The last option Azure Function is the simplest option.</span><span class="sxs-lookup"><span data-stu-id="fc019-265">The last option Azure Function is the simplest option.</span></span> <span data-ttu-id="fc019-266">We recommend using this option.</span><span class="sxs-lookup"><span data-stu-id="fc019-266">We recommend using this option.</span></span> <span data-ttu-id="fc019-267">When you create an Azure Cosmos DB trigger in an Azure Functions app, you select the Azure Cosmos DB collection to connect to and the function is triggered whenever a change to the collection is made.</span><span class="sxs-lookup"><span data-stu-id="fc019-267">When you create an Azure Cosmos DB trigger in an Azure Functions app, you select the Azure Cosmos DB collection to connect to and the function is triggered whenever a change to the collection is made.</span></span> <span data-ttu-id="fc019-268">watch a [screen cast](https://www.youtube.com/watch?v=Mnq0O91i-0s&t=14s) of using Azure function and change feed</span><span class="sxs-lookup"><span data-stu-id="fc019-268">watch a [screen cast](https://www.youtube.com/watch?v=Mnq0O91i-0s&t=14s) of using Azure function and change feed</span></span>

   <span data-ttu-id="fc019-269">Triggers can be created in the Azure Functions portal, in the Azure Cosmos DB portal, or programmatically.</span><span class="sxs-lookup"><span data-stu-id="fc019-269">Triggers can be created in the Azure Functions portal, in the Azure Cosmos DB portal, or programmatically.</span></span> <span data-ttu-id="fc019-270">Visual Studio and VS Code has great support to write Azure Function.</span><span class="sxs-lookup"><span data-stu-id="fc019-270">Visual Studio and VS Code has great support to write Azure Function.</span></span> <span data-ttu-id="fc019-271">You can write and debug the code on your desktop, and then deploy the function with one click.</span><span class="sxs-lookup"><span data-stu-id="fc019-271">You can write and debug the code on your desktop, and then deploy the function with one click.</span></span> <span data-ttu-id="fc019-272">For more information, see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md) article.</span><span class="sxs-lookup"><span data-stu-id="fc019-272">For more information, see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md) article.</span></span>

### <a name="what-is-the-sort-order-of-documents-in-change-feed"></a><span data-ttu-id="fc019-273">What is the sort order of documents in change feed?</span><span class="sxs-lookup"><span data-stu-id="fc019-273">What is the sort order of documents in change feed?</span></span>

<span data-ttu-id="fc019-274">Change feed documents comes in order of their modification time.</span><span class="sxs-lookup"><span data-stu-id="fc019-274">Change feed documents comes in order of their modification time.</span></span> <span data-ttu-id="fc019-275">This sort order is guaranteed only per partition.</span><span class="sxs-lookup"><span data-stu-id="fc019-275">This sort order is guaranteed only per partition.</span></span>

### <a name="for-a-multi-region-account-what-happens-to-the-change-feed-when-the-write-region-fails-over-does-the-change-feed-also-failover-would-the-change-feed-still-appear-contiguous-or-would-the-fail-over-cause-change-feed-to-reset"></a><span data-ttu-id="fc019-276">For a multi-region account, what happens to the change feed when the write-region fails-over?</span><span class="sxs-lookup"><span data-stu-id="fc019-276">For a multi-region account, what happens to the change feed when the write-region fails-over?</span></span> <span data-ttu-id="fc019-277">Does the change feed also failover?</span><span class="sxs-lookup"><span data-stu-id="fc019-277">Does the change feed also failover?</span></span> <span data-ttu-id="fc019-278">Would the change feed still appear contiguous or would the fail-over cause change feed to reset?</span><span class="sxs-lookup"><span data-stu-id="fc019-278">Would the change feed still appear contiguous or would the fail-over cause change feed to reset?</span></span>

<span data-ttu-id="fc019-279">Yes, change feed will work across the manual failover operation and it will be contiguous.</span><span class="sxs-lookup"><span data-stu-id="fc019-279">Yes, change feed will work across the manual failover operation and it will be contiguous.</span></span>

### <a name="how-long-change-feed-persist-the-changed-data-if-i-set-the-ttl-time-to-live-property-for-the-document-to--1"></a><span data-ttu-id="fc019-280">How long change feed persist the changed data if I set the TTL (Time to Live) property for the document to -1?</span><span class="sxs-lookup"><span data-stu-id="fc019-280">How long change feed persist the changed data if I set the TTL (Time to Live) property for the document to -1?</span></span>

<span data-ttu-id="fc019-281">Change feed will persist forever.</span><span class="sxs-lookup"><span data-stu-id="fc019-281">Change feed will persist forever.</span></span> <span data-ttu-id="fc019-282">If data is not deleted, it will remain in change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-282">If data is not deleted, it will remain in change feed.</span></span>

### <a name="how-can-i-configure-azure-functions-to-read-from-a-particular-region-as-change-feed-is-available-in-all-the-read-regions-by-default"></a><span data-ttu-id="fc019-283">How can I configure Azure functions to read from a particular region, as change feed is available in all the read regions by default?</span><span class="sxs-lookup"><span data-stu-id="fc019-283">How can I configure Azure functions to read from a particular region, as change feed is available in all the read regions by default?</span></span>

<span data-ttu-id="fc019-284">Currently it’s not possible to configure Azure Functions to read from a particular region.</span><span class="sxs-lookup"><span data-stu-id="fc019-284">Currently it’s not possible to configure Azure Functions to read from a particular region.</span></span> <span data-ttu-id="fc019-285">There is a GitHub issue in the Azure Functions repo to set the preferred regions of any Azure Cosmos DB binding and trigger.</span><span class="sxs-lookup"><span data-stu-id="fc019-285">There is a GitHub issue in the Azure Functions repo to set the preferred regions of any Azure Cosmos DB binding and trigger.</span></span>

<span data-ttu-id="fc019-286">Azure Functions uses the default connection policy.</span><span class="sxs-lookup"><span data-stu-id="fc019-286">Azure Functions uses the default connection policy.</span></span> <span data-ttu-id="fc019-287">You can configure connection mode in Azure Functions and by default, it reads from the write region, so it is best to co-locate Azure Functions on the same region.</span><span class="sxs-lookup"><span data-stu-id="fc019-287">You can configure connection mode in Azure Functions and by default, it reads from the write region, so it is best to co-locate Azure Functions on the same region.</span></span>

### <a name="what-is-the-default-size-of-batches-in-azure-functions"></a><span data-ttu-id="fc019-288">What is the default size of batches in Azure Functions?</span><span class="sxs-lookup"><span data-stu-id="fc019-288">What is the default size of batches in Azure Functions?</span></span>

<span data-ttu-id="fc019-289">100 documents at every invocation of Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="fc019-289">100 documents at every invocation of Azure Functions.</span></span> <span data-ttu-id="fc019-290">However, this number is configurable within the function.json file.</span><span class="sxs-lookup"><span data-stu-id="fc019-290">However, this number is configurable within the function.json file.</span></span> <span data-ttu-id="fc019-291">Here is complete [list of configuration options](../azure-functions/functions-run-local.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-291">Here is complete [list of configuration options](../azure-functions/functions-run-local.md).</span></span> <span data-ttu-id="fc019-292">If you are developing locally, update the application settings within the [local.settings.json](../azure-functions/functions-run-local.md) file.</span><span class="sxs-lookup"><span data-stu-id="fc019-292">If you are developing locally, update the application settings within the [local.settings.json](../azure-functions/functions-run-local.md) file.</span></span>

### <a name="i-am-monitoring-a-collection-and-reading-its-change-feed-however-i-see-i-am-not-getting-all-the-inserted-document-some-documents-are-missing-what-is-going-on-here"></a><span data-ttu-id="fc019-293">I am monitoring a collection and reading its change feed, however I see I am not getting all the inserted document, some documents are missing.</span><span class="sxs-lookup"><span data-stu-id="fc019-293">I am monitoring a collection and reading its change feed, however I see I am not getting all the inserted document, some documents are missing.</span></span> <span data-ttu-id="fc019-294">What is going on here?</span><span class="sxs-lookup"><span data-stu-id="fc019-294">What is going on here?</span></span>

<span data-ttu-id="fc019-295">Please make sure that there is no other function reading the same collection with the same lease collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-295">Please make sure that there is no other function reading the same collection with the same lease collection.</span></span> <span data-ttu-id="fc019-296">It happened to me, and later I realized the missing documents are processed by my other Azure functions, which is also using the same lease.</span><span class="sxs-lookup"><span data-stu-id="fc019-296">It happened to me, and later I realized the missing documents are processed by my other Azure functions, which is also using the same lease.</span></span>

<span data-ttu-id="fc019-297">Therefore, if you are creating multiple Azure Functions to read the same change feed then they must use different lease collection or use the "leasePrefix" configuration to share the same collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-297">Therefore, if you are creating multiple Azure Functions to read the same change feed then they must use different lease collection or use the "leasePrefix" configuration to share the same collection.</span></span> <span data-ttu-id="fc019-298">However, when you use change feed processor library you can start multiple instances of your function and SDK will divide the documents between different instances automatically for you.</span><span class="sxs-lookup"><span data-stu-id="fc019-298">However, when you use change feed processor library you can start multiple instances of your function and SDK will divide the documents between different instances automatically for you.</span></span>

### <a name="my-document-is-updated-every-second-and-i-am-not-getting-all-the-changes-in-azure-functions-listening-to-change-feed"></a><span data-ttu-id="fc019-299">My document is updated every second, and I am not getting all the changes in Azure Functions listening to change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-299">My document is updated every second, and I am not getting all the changes in Azure Functions listening to change feed.</span></span>

<span data-ttu-id="fc019-300">Azure Functions polls change feed for every 5 seconds, so any changes made between 5 seconds are lost.</span><span class="sxs-lookup"><span data-stu-id="fc019-300">Azure Functions polls change feed for every 5 seconds, so any changes made between 5 seconds are lost.</span></span> <span data-ttu-id="fc019-301">Azure Cosmos DB stores just one version for every 5 seconds so you will get the 5th change on the document.</span><span class="sxs-lookup"><span data-stu-id="fc019-301">Azure Cosmos DB stores just one version for every 5 seconds so you will get the 5th change on the document.</span></span> <span data-ttu-id="fc019-302">However, if you want to go below 5 second, and want to poll change Feed every second, You can configure the polling time "feedPollTime", see [Azure Cosmos DB bindings](../azure-functions/functions-bindings-cosmosdb.md#trigger---configuration).</span><span class="sxs-lookup"><span data-stu-id="fc019-302">However, if you want to go below 5 second, and want to poll change Feed every second, You can configure the polling time "feedPollTime", see [Azure Cosmos DB bindings](../azure-functions/functions-bindings-cosmosdb.md#trigger---configuration).</span></span> <span data-ttu-id="fc019-303">It is defined in milliseconds with a default of 5000.</span><span class="sxs-lookup"><span data-stu-id="fc019-303">It is defined in milliseconds with a default of 5000.</span></span> <span data-ttu-id="fc019-304">Below 1 second is possible but not advisable, as you will start burning more CPU.</span><span class="sxs-lookup"><span data-stu-id="fc019-304">Below 1 second is possible but not advisable, as you will start burning more CPU.</span></span>

### <a name="i-inserted-a-document-in-the-mongo-api-collection-but-when-i-get-the-document-in-change-feed-it-shows-a-different-id-value-what-is-wrong-here"></a><span data-ttu-id="fc019-305">I inserted a document in the Mongo API collection, but when I get the document in change feed, it shows a different id value.</span><span class="sxs-lookup"><span data-stu-id="fc019-305">I inserted a document in the Mongo API collection, but when I get the document in change feed, it shows a different id value.</span></span> <span data-ttu-id="fc019-306">What is wrong here?</span><span class="sxs-lookup"><span data-stu-id="fc019-306">What is wrong here?</span></span>

<span data-ttu-id="fc019-307">Your collection is Mongo API collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-307">Your collection is Mongo API collection.</span></span> <span data-ttu-id="fc019-308">Remember, change feed is read using the SQL client and serializes items into JSON format.</span><span class="sxs-lookup"><span data-stu-id="fc019-308">Remember, change feed is read using the SQL client and serializes items into JSON format.</span></span> <span data-ttu-id="fc019-309">Because of the JSON formatting, MongoDB clients will experience a mismatch between BSON formatted documents and the JSON formatted change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-309">Because of the JSON formatting, MongoDB clients will experience a mismatch between BSON formatted documents and the JSON formatted change feed.</span></span> <span data-ttu-id="fc019-310">You are seeing is the representation of a BSON document in JSON.</span><span class="sxs-lookup"><span data-stu-id="fc019-310">You are seeing is the representation of a BSON document in JSON.</span></span> <span data-ttu-id="fc019-311">If you use binary attributes in a Mongo accounts, they are converted to JSON.</span><span class="sxs-lookup"><span data-stu-id="fc019-311">If you use binary attributes in a Mongo accounts, they are converted to JSON.</span></span>

### <a name="is-there-a-way-to-control-change-feed-for-updates-only-and-not-inserts"></a><span data-ttu-id="fc019-312">Is there a way to control change feed for updates only and not inserts?</span><span class="sxs-lookup"><span data-stu-id="fc019-312">Is there a way to control change feed for updates only and not inserts?</span></span>

<span data-ttu-id="fc019-313">Not today, but this functionality is on roadmap.</span><span class="sxs-lookup"><span data-stu-id="fc019-313">Not today, but this functionality is on roadmap.</span></span> <span data-ttu-id="fc019-314">Today, you can add a soft marker on the document for updates.</span><span class="sxs-lookup"><span data-stu-id="fc019-314">Today, you can add a soft marker on the document for updates.</span></span>

### <a name="is-there-a-way-to-get-deletes-in-change-feed"></a><span data-ttu-id="fc019-315">Is there a way to get deletes in change feed?</span><span class="sxs-lookup"><span data-stu-id="fc019-315">Is there a way to get deletes in change feed?</span></span>

<span data-ttu-id="fc019-316">Currently change feed doesn’t log deletes.</span><span class="sxs-lookup"><span data-stu-id="fc019-316">Currently change feed doesn’t log deletes.</span></span> <span data-ttu-id="fc019-317">Change feed is continuously improving, and this functionality is on roadmap.</span><span class="sxs-lookup"><span data-stu-id="fc019-317">Change feed is continuously improving, and this functionality is on roadmap.</span></span> <span data-ttu-id="fc019-318">Today, you can add a soft marker on the document for delete.</span><span class="sxs-lookup"><span data-stu-id="fc019-318">Today, you can add a soft marker on the document for delete.</span></span> <span data-ttu-id="fc019-319">Add an attribute on the document called "deleted" and set it to "true" and set a TTL on the document so that it can be automatically deleted.</span><span class="sxs-lookup"><span data-stu-id="fc019-319">Add an attribute on the document called "deleted" and set it to "true" and set a TTL on the document so that it can be automatically deleted.</span></span>

### <a name="can-i-read-change-feed-for-historic-documentsfor-example-documents-that-were-added-5-years-back-"></a><span data-ttu-id="fc019-320">Can I read change feed for historic documents(for example, documents that were added 5 years back) ?</span><span class="sxs-lookup"><span data-stu-id="fc019-320">Can I read change feed for historic documents(for example, documents that were added 5 years back) ?</span></span>

<span data-ttu-id="fc019-321">Yes, if the document is not deleted you can read the change feed as far as the origin of your collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-321">Yes, if the document is not deleted you can read the change feed as far as the origin of your collection.</span></span>

### <a name="can-i-read-change-feed-using-javascript"></a><span data-ttu-id="fc019-322">Can I read change feed using JavaScript?</span><span class="sxs-lookup"><span data-stu-id="fc019-322">Can I read change feed using JavaScript?</span></span>

<span data-ttu-id="fc019-323">Yes, Node.js SDK initial support for change feed is recently added.</span><span class="sxs-lookup"><span data-stu-id="fc019-323">Yes, Node.js SDK initial support for change feed is recently added.</span></span> <span data-ttu-id="fc019-324">It can be used as shown in the following example, please update documentdb module to current version before you run the code:</span><span class="sxs-lookup"><span data-stu-id="fc019-324">It can be used as shown in the following example, please update documentdb module to current version before you run the code:</span></span>

```js

var DocumentDBClient = require('documentdb').DocumentClient;
const host = "https://your_host:443/";
const masterKey = "your_master_key==";
const databaseId = "db";
const collectionId = "c1";
const dbLink = 'dbs/' + databaseId;
const collLink = dbLink + '/colls/' + collectionId;
var client = new DocumentDBClient(host, { masterKey: masterKey });
let options = {
    a_im: "Incremental feed",
    accessCondition: {
        type: "IfNoneMatch",        // Use: - empty condition (or remove accessCondition entirely) to start from beginning.
        //      - '*' to start from current.
        //      - specific etag value to start from specific continuation.
        condition: ""
    }
};
 
var query = client.readDocuments(collLink, options);
query.executeNext((err, results, headers) =&gt; {
    // Now we have headers.etag, which can be used in next readDocuments in accessCondition option.
    console.log(results);
    console.log(headers.etag);
    console.log(results.length);
    options.accessCondition = { type: "IfNoneMatch", condition: headers.etag };
    var query = client.readDocuments(collLink, options);
    query.executeNext((err, results, headers) =&gt; {
        console.log("next one:", results[0]);
    });
});<span id="mce_SELREST_start" style="overflow:hidden;line-height:0;"></span>

```

### <a name="can-i-read-change-feed-using-java"></a><span data-ttu-id="fc019-325">Can I read change feed using Java?</span><span class="sxs-lookup"><span data-stu-id="fc019-325">Can I read change feed using Java?</span></span>

<span data-ttu-id="fc019-326">Java library to read change feed is available in [Github repository](https://github.com/Azure/azure-documentdb-changefeedprocessor-java).</span><span class="sxs-lookup"><span data-stu-id="fc019-326">Java library to read change feed is available in [Github repository](https://github.com/Azure/azure-documentdb-changefeedprocessor-java).</span></span> <span data-ttu-id="fc019-327">However, currently Java library is few versions behind .NET library.</span><span class="sxs-lookup"><span data-stu-id="fc019-327">However, currently Java library is few versions behind .NET library.</span></span> <span data-ttu-id="fc019-328">Soon both the libraries will be in sync.</span><span class="sxs-lookup"><span data-stu-id="fc019-328">Soon both the libraries will be in sync.</span></span>

### <a name="can-i-use-etag-lsn-or-ts-for-internal-bookkeeping-which-i-get-in-response"></a><span data-ttu-id="fc019-329">Can I use _etag, _lsn or _ts for internal bookkeeping, which I get in response?</span><span class="sxs-lookup"><span data-stu-id="fc019-329">Can I use _etag, _lsn or _ts for internal bookkeeping, which I get in response?</span></span>

<span data-ttu-id="fc019-330">_etag format is internal and you should not depend on it (do not parse it) because it can change anytime.</span><span class="sxs-lookup"><span data-stu-id="fc019-330">_etag format is internal and you should not depend on it (do not parse it) because it can change anytime.</span></span>
<span data-ttu-id="fc019-331">_ts is modification or creation time stamp.</span><span class="sxs-lookup"><span data-stu-id="fc019-331">_ts is modification or creation time stamp.</span></span> <span data-ttu-id="fc019-332">You can use _ts for chronological comparison.</span><span class="sxs-lookup"><span data-stu-id="fc019-332">You can use _ts for chronological comparison.</span></span>
<span data-ttu-id="fc019-333">_lsn is a batch id that is added only for change feed, it represents the transaction id from the store..</span><span class="sxs-lookup"><span data-stu-id="fc019-333">_lsn is a batch id that is added only for change feed, it represents the transaction id from the store..</span></span> <span data-ttu-id="fc019-334">Many documents may have same _lsn.</span><span class="sxs-lookup"><span data-stu-id="fc019-334">Many documents may have same _lsn.</span></span>
<span data-ttu-id="fc019-335">One more thing to note, ETag on FeedResponse is different than the _etag you see on the document.</span><span class="sxs-lookup"><span data-stu-id="fc019-335">One more thing to note, ETag on FeedResponse is different than the _etag you see on the document.</span></span> <span data-ttu-id="fc019-336">_etag is an internal identifier and used to concurrency, it tells about the version of the document and ETag is used for sequencing the feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-336">_etag is an internal identifier and used to concurrency, it tells about the version of the document and ETag is used for sequencing the feed.</span></span>

### <a name="does-reading-change-feed-add-any-additional-cost-"></a><span data-ttu-id="fc019-337">Does reading change feed add any additional cost ?</span><span class="sxs-lookup"><span data-stu-id="fc019-337">Does reading change feed add any additional cost ?</span></span>

<span data-ttu-id="fc019-338">You are charged for the RU’s consumed i.e. data movement in and out of Azure Cosmos DB collections always consume RU.</span><span class="sxs-lookup"><span data-stu-id="fc019-338">You are charged for the RU’s consumed i.e. data movement in and out of Azure Cosmos DB collections always consume RU.</span></span> <span data-ttu-id="fc019-339">Users will be charged for RU consumed by the lease collection.</span><span class="sxs-lookup"><span data-stu-id="fc019-339">Users will be charged for RU consumed by the lease collection.</span></span>

### <a name="can-multiple-azure-functions-read-one-collections-change-feed"></a><span data-ttu-id="fc019-340">Can multiple Azure Functions read one collection’s change feed?</span><span class="sxs-lookup"><span data-stu-id="fc019-340">Can multiple Azure Functions read one collection’s change feed?</span></span>

<span data-ttu-id="fc019-341">Yes.</span><span class="sxs-lookup"><span data-stu-id="fc019-341">Yes.</span></span> <span data-ttu-id="fc019-342">Multiple Azure Functions can read the same collection’s change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-342">Multiple Azure Functions can read the same collection’s change feed.</span></span> <span data-ttu-id="fc019-343">However, the Azure Functions need to have a separate leaseCollectionPrefix defined.</span><span class="sxs-lookup"><span data-stu-id="fc019-343">However, the Azure Functions need to have a separate leaseCollectionPrefix defined.</span></span>

### <a name="should-the-lease-collection-be-partitioned"></a><span data-ttu-id="fc019-344">Should the lease collection be partitioned?</span><span class="sxs-lookup"><span data-stu-id="fc019-344">Should the lease collection be partitioned?</span></span>

<span data-ttu-id="fc019-345">No, lease collection can be Fixed.</span><span class="sxs-lookup"><span data-stu-id="fc019-345">No, lease collection can be Fixed.</span></span> <span data-ttu-id="fc019-346">Partitioned lease collection is not needed and it’s not currently supported.</span><span class="sxs-lookup"><span data-stu-id="fc019-346">Partitioned lease collection is not needed and it’s not currently supported.</span></span>

### <a name="can-i-read-change-feed-from-spark"></a><span data-ttu-id="fc019-347">Can I read change feed from Spark?</span><span class="sxs-lookup"><span data-stu-id="fc019-347">Can I read change feed from Spark?</span></span>

<span data-ttu-id="fc019-348">Yes, you can.</span><span class="sxs-lookup"><span data-stu-id="fc019-348">Yes, you can.</span></span> <span data-ttu-id="fc019-349">Please see [Azure Cosmos DB Spark Connector](spark-connector.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-349">Please see [Azure Cosmos DB Spark Connector](spark-connector.md).</span></span> <span data-ttu-id="fc019-350">Here is a [screen cast](https://www.youtube.com/watch?v=P9Qz4pwKm_0&t=1519s) showing how you can process change feed as a structured stream.</span><span class="sxs-lookup"><span data-stu-id="fc019-350">Here is a [screen cast](https://www.youtube.com/watch?v=P9Qz4pwKm_0&t=1519s) showing how you can process change feed as a structured stream.</span></span>

### <a name="if-i-am-processing-change-feed-by-using-azure-functions-say-a-batch-of-10-documents-and-i-get-an-error-at-7th-document-in-that-case-the-last-three-documents-are-not-processed-how-can-i-start-processing-from-the-failed-documentie-7th-document-in-my-next-feed"></a><span data-ttu-id="fc019-351">If I am processing change feed by using Azure Functions, say a batch of 10 documents, and I get an error at 7th Document.</span><span class="sxs-lookup"><span data-stu-id="fc019-351">If I am processing change feed by using Azure Functions, say a batch of 10 documents, and I get an error at 7th Document.</span></span> <span data-ttu-id="fc019-352">In that case the last three documents are not processed how can I start processing from the failed document(i.e</span><span class="sxs-lookup"><span data-stu-id="fc019-352">In that case the last three documents are not processed how can I start processing from the failed document(i.e</span></span> <span data-ttu-id="fc019-353">7th document) in my next feed?</span><span class="sxs-lookup"><span data-stu-id="fc019-353">7th document) in my next feed?</span></span>

<span data-ttu-id="fc019-354">To handle the error, the recommended pattern is to wrap your code with try-catch block.</span><span class="sxs-lookup"><span data-stu-id="fc019-354">To handle the error, the recommended pattern is to wrap your code with try-catch block.</span></span> <span data-ttu-id="fc019-355">Catch the error and put that document on a queue (dead-letter)and then define logic to deal with the documents that produced the error.</span><span class="sxs-lookup"><span data-stu-id="fc019-355">Catch the error and put that document on a queue (dead-letter)and then define logic to deal with the documents that produced the error.</span></span> <span data-ttu-id="fc019-356">With this method if you have a 200-document batch, and just one document failed, you do not have to throw away the whole batch.</span><span class="sxs-lookup"><span data-stu-id="fc019-356">With this method if you have a 200-document batch, and just one document failed, you do not have to throw away the whole batch.</span></span>

<span data-ttu-id="fc019-357">In case of error you should not rewind the check point back to beginning else you will can keep getting those documents from change feed.</span><span class="sxs-lookup"><span data-stu-id="fc019-357">In case of error you should not rewind the check point back to beginning else you will can keep getting those documents from change feed.</span></span> <span data-ttu-id="fc019-358">Remember, change feed keeps the last final snap shot of the documents, because of this you may lose the previous snapshot on the document.</span><span class="sxs-lookup"><span data-stu-id="fc019-358">Remember, change feed keeps the last final snap shot of the documents, because of this you may lose the previous snapshot on the document.</span></span> <span data-ttu-id="fc019-359">change feed keeps only one last version of the document, and in between other processes can come and change the document.</span><span class="sxs-lookup"><span data-stu-id="fc019-359">change feed keeps only one last version of the document, and in between other processes can come and change the document.</span></span>

<span data-ttu-id="fc019-360">As you keep fixing your code, you will soon find no documents on dead-letter queue.</span><span class="sxs-lookup"><span data-stu-id="fc019-360">As you keep fixing your code, you will soon find no documents on dead-letter queue.</span></span>
<span data-ttu-id="fc019-361">Azure Functions is automatically called by change feed system and check point etc is maintained internally by Azure Function.</span><span class="sxs-lookup"><span data-stu-id="fc019-361">Azure Functions is automatically called by change feed system and check point etc is maintained internally by Azure Function.</span></span> <span data-ttu-id="fc019-362">If you want to roll back the check point and control every aspect of it, you should consider using change feed Processor SDK.</span><span class="sxs-lookup"><span data-stu-id="fc019-362">If you want to roll back the check point and control every aspect of it, you should consider using change feed Processor SDK.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fc019-363">Next steps</span><span class="sxs-lookup"><span data-stu-id="fc019-363">Next steps</span></span>

<span data-ttu-id="fc019-364">For more information about using Azure Cosmos DB with Azure Functions see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md).</span><span class="sxs-lookup"><span data-stu-id="fc019-364">For more information about using Azure Cosmos DB with Azure Functions see [Azure Cosmos DB: Serverless database computing using Azure Functions](serverless-computing-database.md).</span></span>

<span data-ttu-id="fc019-365">For more information on using the change feed processor library, use the following resources:</span><span class="sxs-lookup"><span data-stu-id="fc019-365">For more information on using the change feed processor library, use the following resources:</span></span>

* [<span data-ttu-id="fc019-366">Information page</span><span class="sxs-lookup"><span data-stu-id="fc019-366">Information page</span></span>](sql-api-sdk-dotnet-changefeed.md) 
* [<span data-ttu-id="fc019-367">Nuget package</span><span class="sxs-lookup"><span data-stu-id="fc019-367">Nuget package</span></span>](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.ChangeFeedProcessor/)
* [<span data-ttu-id="fc019-368">Sample code showing steps 1-6 above</span><span class="sxs-lookup"><span data-stu-id="fc019-368">Sample code showing steps 1-6 above</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/code-samples/ChangeFeedProcessor)
* [<span data-ttu-id="fc019-369">Additional samples on GitHub</span><span class="sxs-lookup"><span data-stu-id="fc019-369">Additional samples on GitHub</span></span>](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/ChangeFeedProcessor)

<span data-ttu-id="fc019-370">For more information on using the change feed via the SDK, use the following resources:</span><span class="sxs-lookup"><span data-stu-id="fc019-370">For more information on using the change feed via the SDK, use the following resources:</span></span>

* [<span data-ttu-id="fc019-371">SDK information page</span><span class="sxs-lookup"><span data-stu-id="fc019-371">SDK information page</span></span>](sql-api-sdk-dotnet.md)
