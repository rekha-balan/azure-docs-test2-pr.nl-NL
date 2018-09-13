---
title: Import Cassandra data into Azure Cosmos DB | Microsoft Docs
description: Learn how to use the CQL Copy command to copy Cassandra data into Azure Cosmos DB.
services: cosmos-db
author: kanshiG
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 11/15/2017
ms.author: govindk
ms.custom: mvc
ms.openlocfilehash: f8c84cc501ea6a979d90d254abeceea8fcc6bddf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864573"
---
# <a name="migrate-your-data-to-azure-cosmos-db-cassandra-api-account"></a><span data-ttu-id="31973-103">Migrate your data to Azure Cosmos DB Cassandra API account</span><span class="sxs-lookup"><span data-stu-id="31973-103">Migrate your data to Azure Cosmos DB Cassandra API account</span></span>

<span data-ttu-id="31973-104">This tutorial provides instructions on importing Cassandra data into Azure Cosmos DB by using the Cassandra Query Language (CQL) COPY command.</span><span class="sxs-lookup"><span data-stu-id="31973-104">This tutorial provides instructions on importing Cassandra data into Azure Cosmos DB by using the Cassandra Query Language (CQL) COPY command.</span></span> 

<span data-ttu-id="31973-105">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="31973-105">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31973-106">Retrieving your connection string</span><span class="sxs-lookup"><span data-stu-id="31973-106">Retrieving your connection string</span></span>
> * <span data-ttu-id="31973-107">Importing data by using the cqlsh COPY command</span><span class="sxs-lookup"><span data-stu-id="31973-107">Importing data by using the cqlsh COPY command</span></span>
> * <span data-ttu-id="31973-108">Importing using the Spark connector</span><span class="sxs-lookup"><span data-stu-id="31973-108">Importing using the Spark connector</span></span> 

# <a name="prerequisites"></a><span data-ttu-id="31973-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31973-109">Prerequisites</span></span>

* <span data-ttu-id="31973-110">Install [Apache Cassandra](http://cassandra.apache.org/download/) and specifically ensure *cqlsh* is present.</span><span class="sxs-lookup"><span data-stu-id="31973-110">Install [Apache Cassandra](http://cassandra.apache.org/download/) and specifically ensure *cqlsh* is present.</span></span>  

* <span data-ttu-id="31973-111">Increase throughput: The duration of your data migration depends on the amount of throughput you provisioned for your Tables.</span><span class="sxs-lookup"><span data-stu-id="31973-111">Increase throughput: The duration of your data migration depends on the amount of throughput you provisioned for your Tables.</span></span> <span data-ttu-id="31973-112">Be sure to increase the throughput for larger data migrations.</span><span class="sxs-lookup"><span data-stu-id="31973-112">Be sure to increase the throughput for larger data migrations.</span></span> <span data-ttu-id="31973-113">After you've completed the migration, decrease the throughput to save costs.</span><span class="sxs-lookup"><span data-stu-id="31973-113">After you've completed the migration, decrease the throughput to save costs.</span></span> <span data-ttu-id="31973-114">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Set throughput for Azure Cosmos DB containers](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="31973-114">For more information about increasing throughput in the [Azure portal](https://portal.azure.com), see [Set throughput for Azure Cosmos DB containers](set-throughput.md).</span></span>  

* <span data-ttu-id="31973-115">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span><span class="sxs-lookup"><span data-stu-id="31973-115">Enable SSL: Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="31973-116">Be sure to enable SSL when you interact with your account.</span><span class="sxs-lookup"><span data-stu-id="31973-116">Be sure to enable SSL when you interact with your account.</span></span> <span data-ttu-id="31973-117">When you use CQL with SSH, you have an option to provide SSL information.</span><span class="sxs-lookup"><span data-stu-id="31973-117">When you use CQL with SSH, you have an option to provide SSL information.</span></span> 

## <a name="get-your-connection-string"></a><span data-ttu-id="31973-118">Get your connection string</span><span class="sxs-lookup"><span data-stu-id="31973-118">Get your connection string</span></span>

1. <span data-ttu-id="31973-119">In the [Azure portal](https://portal.azure.com), on the far left, click **Azure Cosmos DB**.</span><span class="sxs-lookup"><span data-stu-id="31973-119">In the [Azure portal](https://portal.azure.com), on the far left, click **Azure Cosmos DB**.</span></span>

2. <span data-ttu-id="31973-120">In the **Subscriptions** pane, select your account name.</span><span class="sxs-lookup"><span data-stu-id="31973-120">In the **Subscriptions** pane, select your account name.</span></span>

3. <span data-ttu-id="31973-121">Click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="31973-121">Click **Connection String**.</span></span> <span data-ttu-id="31973-122">The right pane contains all the information that you need to successfully connect to your account.</span><span class="sxs-lookup"><span data-stu-id="31973-122">The right pane contains all the information that you need to successfully connect to your account.</span></span>

    ![Connection string page](./media/cassandra-import-data/keys.png)

## <a name="migrate-data-by-using-cqlsh-copy"></a><span data-ttu-id="31973-124">Migrate data by using cqlsh COPY</span><span class="sxs-lookup"><span data-stu-id="31973-124">Migrate data by using cqlsh COPY</span></span>

<span data-ttu-id="31973-125">To import Cassandra data into Azure Cosmos DB for use with the Cassandra API, use the following guidance:</span><span class="sxs-lookup"><span data-stu-id="31973-125">To import Cassandra data into Azure Cosmos DB for use with the Cassandra API, use the following guidance:</span></span>

1. <span data-ttu-id="31973-126">Log in to cqhsh using the connection information from the portal.</span><span class="sxs-lookup"><span data-stu-id="31973-126">Log in to cqhsh using the connection information from the portal.</span></span>
2. <span data-ttu-id="31973-127">Use the [CQL COPY command](http://cassandra.apache.org/doc/latest/tools/cqlsh.html#cqlsh) to copy local data to the Apache Cassandra API endpoint.</span><span class="sxs-lookup"><span data-stu-id="31973-127">Use the [CQL COPY command](http://cassandra.apache.org/doc/latest/tools/cqlsh.html#cqlsh) to copy local data to the Apache Cassandra API endpoint.</span></span> <span data-ttu-id="31973-128">Ensure the source and target are in same datacenter to minimize latency issues.</span><span class="sxs-lookup"><span data-stu-id="31973-128">Ensure the source and target are in same datacenter to minimize latency issues.</span></span>

### <a name="steps-to-move-data-with-cqlsh"></a><span data-ttu-id="31973-129">Steps to move data with cqlsh</span><span class="sxs-lookup"><span data-stu-id="31973-129">Steps to move data with cqlsh</span></span>

1. <span data-ttu-id="31973-130">Pre-create and scale your table:</span><span class="sxs-lookup"><span data-stu-id="31973-130">Pre-create and scale your table:</span></span>
    * <span data-ttu-id="31973-131">By default, Azure Cosmos DB provisions a new Cassandra API table with 1,000 request units per second (RU/s) (CQL-based creation is provisioned with 400 RU/s).</span><span class="sxs-lookup"><span data-stu-id="31973-131">By default, Azure Cosmos DB provisions a new Cassandra API table with 1,000 request units per second (RU/s) (CQL-based creation is provisioned with 400 RU/s).</span></span> <span data-ttu-id="31973-132">Before you start the migration by using cqlsh, pre-create all your tables from the [Azure portal](https://portal.azure.com) or from cqlsh.</span><span class="sxs-lookup"><span data-stu-id="31973-132">Before you start the migration by using cqlsh, pre-create all your tables from the [Azure portal](https://portal.azure.com) or from cqlsh.</span></span> 

    * <span data-ttu-id="31973-133">From the [Azure portal](https://portal.azure.com), increase the throughput of your tables from the default throughput (400 or 1000 RU/s) to 10,000 RU/s for the duration of migration.</span><span class="sxs-lookup"><span data-stu-id="31973-133">From the [Azure portal](https://portal.azure.com), increase the throughput of your tables from the default throughput (400 or 1000 RU/s) to 10,000 RU/s for the duration of migration.</span></span> <span data-ttu-id="31973-134">With the higher throughput, you can avoid rate limiting and migrate in less time.</span><span class="sxs-lookup"><span data-stu-id="31973-134">With the higher throughput, you can avoid rate limiting and migrate in less time.</span></span> <span data-ttu-id="31973-135">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span><span class="sxs-lookup"><span data-stu-id="31973-135">With hourly billing in Azure Cosmos DB, you can reduce the throughput immediately after the migration to save costs.</span></span>

2. <span data-ttu-id="31973-136">Determine the RU charge for an operation.</span><span class="sxs-lookup"><span data-stu-id="31973-136">Determine the RU charge for an operation.</span></span> <span data-ttu-id="31973-137">You can do this using the Azure Cosmos DB Cassandra API SDK of your choice.</span><span class="sxs-lookup"><span data-stu-id="31973-137">You can do this using the Azure Cosmos DB Cassandra API SDK of your choice.</span></span> <span data-ttu-id="31973-138">This example shows the .NET version of getting RU charges.</span><span class="sxs-lookup"><span data-stu-id="31973-138">This example shows the .NET version of getting RU charges.</span></span> 

    ```csharp
    var tableInsertStatement = table.Insert(sampleEntity);
    var insertResult = await tableInsertStatement.ExecuteAsync();

    foreach (string key in insertResult.Info.IncomingPayload)
            {
                byte[] valueInBytes = customPayload[key];
                string value = Encoding.UTF8.GetString(valueInBytes);
                Console.WriteLine($"CustomPayload:  {key}: {value}");
            }
 
    ``` 

3. <span data-ttu-id="31973-139">Determine the latency from your machine to the Azure Cosmos DB service.</span><span class="sxs-lookup"><span data-stu-id="31973-139">Determine the latency from your machine to the Azure Cosmos DB service.</span></span> <span data-ttu-id="31973-140">If you are within an Azure Data center, the latency should be a low single digit millisecond number.</span><span class="sxs-lookup"><span data-stu-id="31973-140">If you are within an Azure Data center, the latency should be a low single digit millisecond number.</span></span> <span data-ttu-id="31973-141">If you are outside the Azure Datacenter, then you can use psping or azurespeed.com to get the approximate latency from your location.</span><span class="sxs-lookup"><span data-stu-id="31973-141">If you are outside the Azure Datacenter, then you can use psping or azurespeed.com to get the approximate latency from your location.</span></span>   

4. <span data-ttu-id="31973-142">Calculate the proper values for parameters (NUMPROCESS, INGESTRATE, MAXBATCHSIZE, or MINBATCHSIZE) that provide good performance.</span><span class="sxs-lookup"><span data-stu-id="31973-142">Calculate the proper values for parameters (NUMPROCESS, INGESTRATE, MAXBATCHSIZE, or MINBATCHSIZE) that provide good performance.</span></span> 

5. <span data-ttu-id="31973-143">Run the final migration command.</span><span class="sxs-lookup"><span data-stu-id="31973-143">Run the final migration command.</span></span> <span data-ttu-id="31973-144">Running this command assumes you have started cqlsh using the connection string information.</span><span class="sxs-lookup"><span data-stu-id="31973-144">Running this command assumes you have started cqlsh using the connection string information.</span></span>

   ```bash
   COPY exampleks.tablename FROM filefolderx/*.csv 
   ```

## <a name="migrate-data-by-using-spark"></a><span data-ttu-id="31973-145">Migrate data by using Spark</span><span class="sxs-lookup"><span data-stu-id="31973-145">Migrate data by using Spark</span></span>

<span data-ttu-id="31973-146">For data residing in an existing cluster in Azure virtual machines, importing data using Spark is also feasible option.</span><span class="sxs-lookup"><span data-stu-id="31973-146">For data residing in an existing cluster in Azure virtual machines, importing data using Spark is also feasible option.</span></span> <span data-ttu-id="31973-147">This requires Spark to be set up as intermediary for one time or regular ingestion.</span><span class="sxs-lookup"><span data-stu-id="31973-147">This requires Spark to be set up as intermediary for one time or regular ingestion.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="31973-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="31973-148">Next steps</span></span>

<span data-ttu-id="31973-149">In this tutorial, you've learned how to complete the following tasks:</span><span class="sxs-lookup"><span data-stu-id="31973-149">In this tutorial, you've learned how to complete the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="31973-150">Retrieve your connection string</span><span class="sxs-lookup"><span data-stu-id="31973-150">Retrieve your connection string</span></span>
> * <span data-ttu-id="31973-151">Import data by using cql copy command</span><span class="sxs-lookup"><span data-stu-id="31973-151">Import data by using cql copy command</span></span>
> * <span data-ttu-id="31973-152">Import using the Spark connector</span><span class="sxs-lookup"><span data-stu-id="31973-152">Import using the Spark connector</span></span> 

<span data-ttu-id="31973-153">You can now proceed to the Concepts section for more information about Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="31973-153">You can now proceed to the Concepts section for more information about Azure Cosmos DB.</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="31973-154">Tunable data consistency levels in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="31973-154">Tunable data consistency levels in Azure Cosmos DB</span></span>](../cosmos-db/consistency-levels.md)
