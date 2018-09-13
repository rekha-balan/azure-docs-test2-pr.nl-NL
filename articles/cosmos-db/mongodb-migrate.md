---
title: Use mongoimport and mongorestore with the Azure Cosmos DB API for MongoDB | Microsoft Docs
description: Learn how to use mongoimport and mongorestore to import data to an API for MongoDB account
keywords: mongoimport, mongorestore
services: cosmos-db
author: SnehaGunda
manager: slyons
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: tutorial
ms.date: 05/07/2018
ms.author: sclyon
ms.custom: mvc
ms.openlocfilehash: e133dde4defdec51d33fda70c0ac6d6fbeff18fe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965477"
---
# <a name="migrate-your-data-to-azure-cosmos-db-mongodb-api-account"></a><span data-ttu-id="91185-104">Migrate your data to Azure Cosmos DB MongoDB API account</span><span class="sxs-lookup"><span data-stu-id="91185-104">Migrate your data to Azure Cosmos DB MongoDB API account</span></span>

<span data-ttu-id="91185-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span><span class="sxs-lookup"><span data-stu-id="91185-105">To migrate data from MongoDB to an Azure Cosmos DB account for use with the API for MongoDB, you must:</span></span>

* <span data-ttu-id="91185-106">Download the community server from the [MongoDB Download Center](https://www.mongodb.com/download-center) and install it.</span><span class="sxs-lookup"><span data-stu-id="91185-106">Download the community server from the [MongoDB Download Center](https://www.mongodb.com/download-center) and install it.</span></span>
* <span data-ttu-id="91185-107">Use the mongoimport.exe or mongorestore.exe file that are installed in the "installation folder/bin" directory.</span><span class="sxs-lookup"><span data-stu-id="91185-107">Use the mongoimport.exe or mongorestore.exe file that are installed in the "installation folder/bin" directory.</span></span> 
* <span data-ttu-id="91185-108">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="91185-108">Get your [API for MongoDB connection string](connect-mongodb-account.md).</span></span>

<span data-ttu-id="91185-109">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB SQL API, you should use the [Data Migration tool](import-data.md) to import data.</span><span class="sxs-lookup"><span data-stu-id="91185-109">If you are importing data from MongoDB and plan to use it with the Azure Cosmos DB SQL API, you should use the [Data Migration tool](import-data.md) to import data.</span></span>

<span data-ttu-id="91185-110">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="91185-110">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="91185-111">Retrieving your connection string</span><span class="sxs-lookup"><span data-stu-id="91185-111">Retrieving your connection string</span></span>
> * <span data-ttu-id="91185-112">Importing MongoDB data by using mongoimport</span><span class="sxs-lookup"><span data-stu-id="91185-112">Importing MongoDB data by using mongoimport</span></span>
> * <span data-ttu-id="91185-113">Importing MongoDB data by using mongorestore</span><span class="sxs-lookup"><span data-stu-id="91185-113">Importing MongoDB data by using mongorestore</span></span>

## <a name="prerequisites"></a><span data-ttu-id="91185-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="91185-114">Prerequisites</span></span>

* <span data-ttu-id="91185-115">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual collection or a set of collections.</span><span class="sxs-lookup"><span data-stu-id="91185-115">Increase throughput: The duration of your data migration depends on the amount of throughput you set up for an individual collection or a set of collections.</span></span> <span data-ttu-id="91185-116">Be sure to increase the throughput for larger data migrations.</span><span class="sxs-lookup"><span data-stu-id="91185-116">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="91185-117">After you've completed the migration, decrease the throughput to save costs.</span><span class="sxs-lookup"><span data-stu-id="91185-117">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="91185-118">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span><span class="sxs-lookup"><span data-stu-id="91185-118">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Performance levels and pricing tiers in Azure Cosmos DB](performance-levels.md).</span></span>

* <span data-ttu-id="91185-119">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span><span class="sxs-lookup"><span data-stu-id="91185-119">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="91185-120">Be sure to enable SSL when you interact with your account.</span><span class="sxs-lookup"><span data-stu-id="91185-120">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="91185-121">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span><span class="sxs-lookup"><span data-stu-id="91185-121">The procedures in the rest of the article include how to enable SSL for mongoimport and mongorestore.</span></span>

## <a name="get-your-connection-string"></a><span data-ttu-id="91185-122">Get your connection string</span><span class="sxs-lookup"><span data-stu-id="91185-122">Get your connection string</span></span> 

1. <span data-ttu-id="91185-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span><span class="sxs-lookup"><span data-stu-id="91185-123">In the [Azure portal](https://portal.azure.com), in the left pane, click the **Azure Cosmos DB** entry.</span></span>
1. <span data-ttu-id="91185-124">In the **Subscriptions** pane, select your account name.</span><span class="sxs-lookup"><span data-stu-id="91185-124">In the **Subscriptions** pane, select your account name.</span></span>
1. <span data-ttu-id="91185-125">In the **Connection String** blade, click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="91185-125">In the **Connection String** blade, click **Connection String**.</span></span>

   <span data-ttu-id="91185-126">The right pane contains all the information that you need to successfully connect to your account.</span><span class="sxs-lookup"><span data-stu-id="91185-126">The right pane contains all the information that you need to successfully connect to your account.</span></span>

   ![Connection String blade](./media/mongodb-migrate/ConnectionStringBlade.png)

## <a name="migrate-data-by-using-mongoimport"></a><span data-ttu-id="91185-128">Migrate data by using mongoimport</span><span class="sxs-lookup"><span data-stu-id="91185-128">Migrate data by using mongoimport</span></span>

<span data-ttu-id="91185-129">To import data to your Azure Cosmos DB account, use the following template.</span><span class="sxs-lookup"><span data-stu-id="91185-129">To import data to your Azure Cosmos DB account, use the following template.</span></span> <span data-ttu-id="91185-130">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span><span class="sxs-lookup"><span data-stu-id="91185-130">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>  

<span data-ttu-id="91185-131">Template:</span><span class="sxs-lookup"><span data-stu-id="91185-131">Template:</span></span>

```bash
    mongoimport.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates --type json --file "C:\sample.json"
```

<span data-ttu-id="91185-132">Example:</span><span class="sxs-lookup"><span data-stu-id="91185-132">Example:</span></span>  

```bash
    mongoimport.exe --host cosmosdb-mongodb-account.documents.azure.com:10255 -u cosmosdb-mongodb-account -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates --db sampleDB --collection sampleColl --type json --file "C:\Users\admin\Desktop\*.json"
```

## <a name="migrate-data-by-using-mongorestore"></a><span data-ttu-id="91185-133">Migrate data by using mongorestore</span><span class="sxs-lookup"><span data-stu-id="91185-133">Migrate data by using mongorestore</span></span>

<span data-ttu-id="91185-134">To restore data to your API for MongoDB account, use the following template to execute the import.</span><span class="sxs-lookup"><span data-stu-id="91185-134">To restore data to your API for MongoDB account, use the following template to execute the import.</span></span> <span data-ttu-id="91185-135">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span><span class="sxs-lookup"><span data-stu-id="91185-135">Fill in *host*, *username*, and *password* with the values that are specific to your account.</span></span>

<span data-ttu-id="91185-136">Template:</span><span class="sxs-lookup"><span data-stu-id="91185-136">Template:</span></span>

```bash
    mongorestore.exe --host <your_hostname>:10255 -u <your_username> -p <your_password> --db <your_database> --collection <your_collection> --ssl --sslAllowInvalidCertificates <path_to_backup>
```

<span data-ttu-id="91185-137">Example:</span><span class="sxs-lookup"><span data-stu-id="91185-137">Example:</span></span>

```bash
    mongorestore.exe --host cosmosdb-mongodb-account.documents.azure.com:10255 -u cosmosdb-mongodb-account -p tkvaVkp4Nnaoirnouenrgisuner2435qwefBH0z256Na24frio34LNQasfaefarfernoimczciqisAXw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07
```
    
## <a name="steps-for-a-successful-migration"></a><span data-ttu-id="91185-138">Steps for a successful migration</span><span class="sxs-lookup"><span data-stu-id="91185-138">Steps for a successful migration</span></span>

1. <span data-ttu-id="91185-139">Pre-create and scale your collections:</span><span class="sxs-lookup"><span data-stu-id="91185-139">Pre-create and scale your collections:</span></span>
        
    * <span data-ttu-id="91185-140">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units per second (RU/sec).</span><span class="sxs-lookup"><span data-stu-id="91185-140">By default, Azure Cosmos DB provisions a new MongoDB collection with 1,000 request units per second (RU/sec).</span></span> <span data-ttu-id="91185-141">Before you start the migration by using mongoimport, mongorestore, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span><span class="sxs-lookup"><span data-stu-id="91185-141">Before you start the migration by using mongoimport, mongorestore, pre-create all your collections from the [Azure portal](https://portal.azure.com) or from MongoDB drivers and tools.</span></span> <span data-ttu-id="91185-142">If the data size is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span><span class="sxs-lookup"><span data-stu-id="91185-142">If the data size is greater than 10 GB, make sure to create a [sharded/partitioned collection](partition-data.md) with an appropriate shard key.</span></span>

    * <span data-ttu-id="91185-143">From the [Azure portal](https://portal.azure.com), increase your collections throughput from 1000 RUs/sec for a single partition collection and 2,500 RUs/sec for a sharded collection just for the migration.</span><span class="sxs-lookup"><span data-stu-id="91185-143">From the [Azure portal](https://portal.azure.com), increase your collections throughput from 1000 RUs/sec for a single partition collection and 2,500 RUs/sec for a sharded collection just for the migration.</span></span> <span data-ttu-id="91185-144">With the higher throughput, you can avoid rate limiting and migrate in less time.</span><span class="sxs-lookup"><span data-stu-id="91185-144">With the higher throughput, you can avoid rate limiting and migrate in less time.</span></span> <span data-ttu-id="91185-145">You can reduce the throughput immediately after the migration to save costs.</span><span class="sxs-lookup"><span data-stu-id="91185-145">You can reduce the throughput immediately after the migration to save costs.</span></span>

    * <span data-ttu-id="91185-146">In addition to provisioning RUs/sec at the collection level, you may also provision RU/sec for a set of collections at the parent database level.</span><span class="sxs-lookup"><span data-stu-id="91185-146">In addition to provisioning RUs/sec at the collection level, you may also provision RU/sec for a set of collections at the parent database level.</span></span> <span data-ttu-id="91185-147">This requires pre-creating the database and collections, as well as defining a shard key for each collection.</span><span class="sxs-lookup"><span data-stu-id="91185-147">This requires pre-creating the database and collections, as well as defining a shard key for each collection.</span></span>

    * <span data-ttu-id="91185-148">You can create sharded collections through your favorite tool, driver, or SDK.</span><span class="sxs-lookup"><span data-stu-id="91185-148">You can create sharded collections through your favorite tool, driver, or SDK.</span></span> <span data-ttu-id="91185-149">In this example, we use the Mongo Shell to create a sharded collection:</span><span class="sxs-lookup"><span data-stu-id="91185-149">In this example, we use the Mongo Shell to create a sharded collection:</span></span>

        ```bash
        db.runCommand( { shardCollection: "admin.people", key: { region: "hashed" } } )
        ```
    
        <span data-ttu-id="91185-150">Results:</span><span class="sxs-lookup"><span data-stu-id="91185-150">Results:</span></span>

        ```JSON
        {
            "_t" : "ShardCollectionResponse",
            "ok" : 1,
            "collectionsharded" : "admin.people"
        }
        ```

1. <span data-ttu-id="91185-151">Calculate the approximate RU charge for a single document write:</span><span class="sxs-lookup"><span data-stu-id="91185-151">Calculate the approximate RU charge for a single document write:</span></span>

   <span data-ttu-id="91185-152">a.</span><span class="sxs-lookup"><span data-stu-id="91185-152">a.</span></span> <span data-ttu-id="91185-153">Connect to your Azure Cosmos DB MongoDB API account from the MongoDB Shell.</span><span class="sxs-lookup"><span data-stu-id="91185-153">Connect to your Azure Cosmos DB MongoDB API account from the MongoDB Shell.</span></span> <span data-ttu-id="91185-154">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="91185-154">You can find instructions in [Connect a MongoDB application to Azure Cosmos DB](connect-mongodb-account.md).</span></span>
    
   <span data-ttu-id="91185-155">b.</span><span class="sxs-lookup"><span data-stu-id="91185-155">b.</span></span> <span data-ttu-id="91185-156">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span><span class="sxs-lookup"><span data-stu-id="91185-156">Run a sample insert command by using one of your sample documents from the MongoDB Shell:</span></span>
   
      ```bash
      db.coll.insert({ "playerId": "a067ff", "hashedid": "bb0091", "countryCode": "hk" })
      ```
        
   <span data-ttu-id="91185-157">c.</span><span class="sxs-lookup"><span data-stu-id="91185-157">c.</span></span> <span data-ttu-id="91185-158">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you'll receive a response like the following:</span><span class="sxs-lookup"><span data-stu-id="91185-158">Run ```db.runCommand({getLastRequestStatistics: 1})``` and you'll receive a response like the following:</span></span>
     
      ```bash
        globaldb:PRIMARY> db.runCommand({getLastRequestStatistics: 1})
        {
            "_t": "GetRequestStatisticsResponse",
            "ok": 1,
            "CommandName": "insert",
            "RequestCharge": 10,
            "RequestDurationInMilliSeconds": NumberLong(50)
        }
      ```
        
    <span data-ttu-id="91185-159">d.</span><span class="sxs-lookup"><span data-stu-id="91185-159">d.</span></span> <span data-ttu-id="91185-160">Take note of the request charge.</span><span class="sxs-lookup"><span data-stu-id="91185-160">Take note of the request charge.</span></span>
    
1. <span data-ttu-id="91185-161">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span><span class="sxs-lookup"><span data-stu-id="91185-161">Determine the latency from your machine to the Azure Cosmos DB cloud service:</span></span>
    
    <span data-ttu-id="91185-162">a.</span><span class="sxs-lookup"><span data-stu-id="91185-162">a.</span></span> <span data-ttu-id="91185-163">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span><span class="sxs-lookup"><span data-stu-id="91185-163">Enable verbose logging from the MongoDB Shell by using this command: ```setVerboseShell(true)```</span></span>
    
    <span data-ttu-id="91185-164">b.</span><span class="sxs-lookup"><span data-stu-id="91185-164">b.</span></span> <span data-ttu-id="91185-165">Run a simple query against the database: ```db.coll.find().limit(1)```.</span><span class="sxs-lookup"><span data-stu-id="91185-165">Run a simple query against the database: ```db.coll.find().limit(1)```.</span></span> <span data-ttu-id="91185-166">You'll receive a response like the following:</span><span class="sxs-lookup"><span data-stu-id="91185-166">You'll receive a response like the following:</span></span>

        ```
        Fetched 1 record(s) in 100(ms)
        ```
        
1. <span data-ttu-id="91185-167">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span><span class="sxs-lookup"><span data-stu-id="91185-167">Remove the inserted document before the migration to ensure that there are no duplicate documents.</span></span> <span data-ttu-id="91185-168">You can remove documents by using this command: ```db.coll.remove({})```</span><span class="sxs-lookup"><span data-stu-id="91185-168">You can remove documents by using this command: ```db.coll.remove({})```</span></span>

1. <span data-ttu-id="91185-169">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span><span class="sxs-lookup"><span data-stu-id="91185-169">Calculate the approximate *batchSize* and *numInsertionWorkers* values:</span></span>

    * <span data-ttu-id="91185-170">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span><span class="sxs-lookup"><span data-stu-id="91185-170">For *batchSize*, divide the total provisioned RUs by the RUs consumed from your single document write in step 3.</span></span>
    
    * <span data-ttu-id="91185-171">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span><span class="sxs-lookup"><span data-stu-id="91185-171">If the calculated *batchSize* <= 24, use that number as your *batchSize* value.</span></span>
    
    * <span data-ttu-id="91185-172">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span><span class="sxs-lookup"><span data-stu-id="91185-172">If the calculated *batchSize* > 24, set the *batchSize* value to 24.</span></span>
    
    * <span data-ttu-id="91185-173">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput \* latency in seconds) / (batch size \* consumed RUs for a single write)*.</span><span class="sxs-lookup"><span data-stu-id="91185-173">For *numInsertionWorkers*, use this equation:   *numInsertionWorkers =  (provisioned throughput \* latency in seconds) / (batch size \* consumed RUs for a single write)*.</span></span>
        
    |<span data-ttu-id="91185-174">Property</span><span class="sxs-lookup"><span data-stu-id="91185-174">Property</span></span>|<span data-ttu-id="91185-175">Value</span><span class="sxs-lookup"><span data-stu-id="91185-175">Value</span></span>|
    |--------|-----|
    |<span data-ttu-id="91185-176">batchSize</span><span class="sxs-lookup"><span data-stu-id="91185-176">batchSize</span></span>| <span data-ttu-id="91185-177">24</span><span class="sxs-lookup"><span data-stu-id="91185-177">24</span></span> |
    |<span data-ttu-id="91185-178">RUs provisioned</span><span class="sxs-lookup"><span data-stu-id="91185-178">RUs provisioned</span></span> | <span data-ttu-id="91185-179">10000</span><span class="sxs-lookup"><span data-stu-id="91185-179">10000</span></span> |
    |<span data-ttu-id="91185-180">Latency</span><span class="sxs-lookup"><span data-stu-id="91185-180">Latency</span></span> | <span data-ttu-id="91185-181">0.100 s</span><span class="sxs-lookup"><span data-stu-id="91185-181">0.100 s</span></span> |
    |<span data-ttu-id="91185-182">RU charged for 1 doc write</span><span class="sxs-lookup"><span data-stu-id="91185-182">RU charged for 1 doc write</span></span> | <span data-ttu-id="91185-183">10 RUs</span><span class="sxs-lookup"><span data-stu-id="91185-183">10 RUs</span></span> |
    |<span data-ttu-id="91185-184">numInsertionWorkers</span><span class="sxs-lookup"><span data-stu-id="91185-184">numInsertionWorkers</span></span> | <span data-ttu-id="91185-185">?</span><span class="sxs-lookup"><span data-stu-id="91185-185">?</span></span> |
    
    <span data-ttu-id="91185-186">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span><span class="sxs-lookup"><span data-stu-id="91185-186">*numInsertionWorkers = (10000 RUs x 0.1 s) / (24 x 10 RUs) = 4.1666*</span></span>

1. <span data-ttu-id="91185-187">Run the final migration command:</span><span class="sxs-lookup"><span data-stu-id="91185-187">Run the final migration command:</span></span>

   ```bash
   mongoimport.exe --host cosmosdb-mongodb-account.documents.azure.com:10255 -u cosmosdb-mongodb-account -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates --jsonArray --db dabasename --collection collectionName --file "C:\sample.json" --numInsertionWorkers 4 --batchSize 24
   ```
   <span data-ttu-id="91185-188">Or with mongorestore (make sure all collections have the throughput set at or above the amount of RUs used in previous calculations):</span><span class="sxs-lookup"><span data-stu-id="91185-188">Or with mongorestore (make sure all collections have the throughput set at or above the amount of RUs used in previous calculations):</span></span>
   
   ```bash
   mongorestore.exe --host cosmosdb-mongodb-account.documents.azure.com:10255 -u cosmosdb-mongodb-account -p wzRJCyjtLPNuhm53yTwaefawuiefhbauwebhfuabweifbiauweb2YVdl2ZFNZNv8IU89LqFVm5U0bw== --ssl --sslAllowInvalidCertificates ./dumps/dump-2016-12-07 --numInsertionWorkersPerCollection 4 --batchSize 24
   ```

## <a name="next-steps"></a><span data-ttu-id="91185-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="91185-189">Next steps</span></span>

<span data-ttu-id="91185-190">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="91185-190">You can proceed to the next tutorial and learn how to query MongoDB data by using Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="91185-191">How to query MongoDB data?</span><span class="sxs-lookup"><span data-stu-id="91185-191">How to query MongoDB data?</span></span>](../cosmos-db/tutorial-query-mongodb.md)
