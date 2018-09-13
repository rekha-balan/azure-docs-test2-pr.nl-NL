---
title: Lambda architecture with Azure Cosmos DB and HDInsight (Apache Spark) | Microsoft Docs
description: This article describes how to implement a lambda architecture using Azure Cosmos DB, HDInsight, and Spark
keywords: lambda-architecture
services: cosmos-db
author: tknandu
manager: kfile
editor: ''
ms.service: cosmos-db
ms.devlang: na
ms.topic: conceptual
ms.date: 01/19/2018
ms.author: ramkris
ms.openlocfilehash: c926c67a330648e09c1fd8133164f64582ad9a34
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868706"
---
# <a name="azure-cosmos-db-implement-a-lambda-architecture-on-the-azure-platform"></a><span data-ttu-id="aa145-104">Azure Cosmos DB: Implement a lambda architecture on the Azure platform</span><span class="sxs-lookup"><span data-stu-id="aa145-104">Azure Cosmos DB: Implement a lambda architecture on the Azure platform</span></span> 

<span data-ttu-id="aa145-105">Lambda architectures enable efficient data processing of massive data sets.</span><span class="sxs-lookup"><span data-stu-id="aa145-105">Lambda architectures enable efficient data processing of massive data sets.</span></span> <span data-ttu-id="aa145-106">Lambda architectures use batch-processing, stream-processing, and a serving layer to minimize the latency involved in querying big data.</span><span class="sxs-lookup"><span data-stu-id="aa145-106">Lambda architectures use batch-processing, stream-processing, and a serving layer to minimize the latency involved in querying big data.</span></span> 

<span data-ttu-id="aa145-107">To implement a lambda architecture on Azure, you can combine the following technologies to accelerate real-time big data analytics:</span><span class="sxs-lookup"><span data-stu-id="aa145-107">To implement a lambda architecture on Azure, you can combine the following technologies to accelerate real-time big data analytics:</span></span>
* <span data-ttu-id="aa145-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), the industry's first globally distributed, multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="aa145-108">[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/), the industry's first globally distributed, multi-model database service.</span></span> 
* <span data-ttu-id="aa145-109">[Apache Spark for Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/), a processing framework that runs large-scale data analytics applications</span><span class="sxs-lookup"><span data-stu-id="aa145-109">[Apache Spark for Azure HDInsight](https://azure.microsoft.com/services/hdinsight/apache-spark/), a processing framework that runs large-scale data analytics applications</span></span>
* <span data-ttu-id="aa145-110">Azure Cosmos DB [change feed](change-feed.md), which streams new data to the batch layer for HDInsight to process</span><span class="sxs-lookup"><span data-stu-id="aa145-110">Azure Cosmos DB [change feed](change-feed.md), which streams new data to the batch layer for HDInsight to process</span></span>
* <span data-ttu-id="aa145-111">The [Spark to Azure Cosmos DB Connector](spark-connector.md)</span><span class="sxs-lookup"><span data-stu-id="aa145-111">The [Spark to Azure Cosmos DB Connector](spark-connector.md)</span></span>

<span data-ttu-id="aa145-112">This article describes the fundamentals of a lambda architecture based on the original multi-layer design and the benefits of a "rearchitected" lambda architecture that simplifies operations.</span><span class="sxs-lookup"><span data-stu-id="aa145-112">This article describes the fundamentals of a lambda architecture based on the original multi-layer design and the benefits of a "rearchitected" lambda architecture that simplifies operations.</span></span>  

## <a name="what-is-a-lambda-architecture"></a><span data-ttu-id="aa145-113">What is a lambda architecture?</span><span class="sxs-lookup"><span data-stu-id="aa145-113">What is a lambda architecture?</span></span>
<span data-ttu-id="aa145-114">A lambda architecture is a generic, scalable, and fault-tolerant data processing architecture to address batch and speed latency scenarios as described by [Nathan Marz](https://twitter.com/nathanmarz).</span><span class="sxs-lookup"><span data-stu-id="aa145-114">A lambda architecture is a generic, scalable, and fault-tolerant data processing architecture to address batch and speed latency scenarios as described by [Nathan Marz](https://twitter.com/nathanmarz).</span></span>

![Diagram showing a lambda architecture](./media/lambda-architecture/lambda-architecture-intro.png)

<span data-ttu-id="aa145-116">Source: http://lambda-architecture.net/</span><span class="sxs-lookup"><span data-stu-id="aa145-116">Source: http://lambda-architecture.net/</span></span>

<span data-ttu-id="aa145-117">The basic principles of a lambda architecture are described in the preceding diagram as per [https://lambda-architecture.net](http://lambda-architecture.net/).</span><span class="sxs-lookup"><span data-stu-id="aa145-117">The basic principles of a lambda architecture are described in the preceding diagram as per [https://lambda-architecture.net](http://lambda-architecture.net/).</span></span>

 1. <span data-ttu-id="aa145-118">All **data** is pushed into *both* the *batch layer* and *speed layer*.</span><span class="sxs-lookup"><span data-stu-id="aa145-118">All **data** is pushed into *both* the *batch layer* and *speed layer*.</span></span>
 2. <span data-ttu-id="aa145-119">The **batch layer** has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views.</span><span class="sxs-lookup"><span data-stu-id="aa145-119">The **batch layer** has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views.</span></span>
 3. <span data-ttu-id="aa145-120">The **serving layer** has batch views for fast queries.</span><span class="sxs-lookup"><span data-stu-id="aa145-120">The **serving layer** has batch views for fast queries.</span></span> 
 4. <span data-ttu-id="aa145-121">The **speed layer** compensates for processing time (to the serving layer) and deals with recent data only.</span><span class="sxs-lookup"><span data-stu-id="aa145-121">The **speed layer** compensates for processing time (to the serving layer) and deals with recent data only.</span></span>
 5. <span data-ttu-id="aa145-122">All queries can be answered by merging results from batch views and real-time views or pinging them individually.</span><span class="sxs-lookup"><span data-stu-id="aa145-122">All queries can be answered by merging results from batch views and real-time views or pinging them individually.</span></span>

<span data-ttu-id="aa145-123">Upon further reading, we will be able to implement this architecture using only the following:</span><span class="sxs-lookup"><span data-stu-id="aa145-123">Upon further reading, we will be able to implement this architecture using only the following:</span></span>

* <span data-ttu-id="aa145-124">Azure Cosmos DB collection(s)</span><span class="sxs-lookup"><span data-stu-id="aa145-124">Azure Cosmos DB collection(s)</span></span>
* <span data-ttu-id="aa145-125">HDInsight (Apache Spark 2.1) cluster</span><span class="sxs-lookup"><span data-stu-id="aa145-125">HDInsight (Apache Spark 2.1) cluster</span></span>
* <span data-ttu-id="aa145-126">Spark Connector [1.0](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark_2.1.0_2.11-1.0.0)</span><span class="sxs-lookup"><span data-stu-id="aa145-126">Spark Connector [1.0](https://github.com/Azure/azure-cosmosdb-spark/tree/master/releases/azure-cosmosdb-spark_2.1.0_2.11-1.0.0)</span></span>

## <a name="speed-layer"></a><span data-ttu-id="aa145-127">Speed layer</span><span class="sxs-lookup"><span data-stu-id="aa145-127">Speed layer</span></span>

<span data-ttu-id="aa145-128">From an operations perspective, maintaining two streams of data while ensuring the correct state of the data can be a complicated endeavor.</span><span class="sxs-lookup"><span data-stu-id="aa145-128">From an operations perspective, maintaining two streams of data while ensuring the correct state of the data can be a complicated endeavor.</span></span> <span data-ttu-id="aa145-129">To simplify operations, utilize the [Azure Cosmos DB change feed support](change-feed.md) to keep the state for the *batch layer* while revealing the Azure Cosmos DB change log via the *Change Feed API* for your *speed layer*.</span><span class="sxs-lookup"><span data-stu-id="aa145-129">To simplify operations, utilize the [Azure Cosmos DB change feed support](change-feed.md) to keep the state for the *batch layer* while revealing the Azure Cosmos DB change log via the *Change Feed API* for your *speed layer*.</span></span>  
<span data-ttu-id="aa145-130">![Diagram highlighting the new data, speed layer, and master dataset portion of the lambda architecture](./media/lambda-architecture/lambda-architecture-change-feed.png)</span><span class="sxs-lookup"><span data-stu-id="aa145-130">![Diagram highlighting the new data, speed layer, and master dataset portion of the lambda architecture](./media/lambda-architecture/lambda-architecture-change-feed.png)</span></span>

<span data-ttu-id="aa145-131">What's important in these layers:</span><span class="sxs-lookup"><span data-stu-id="aa145-131">What's important in these layers:</span></span>

 1. <span data-ttu-id="aa145-132">All **data** is pushed *only* into Azure Cosmos DB, thus you can avoid multi-casting issues.</span><span class="sxs-lookup"><span data-stu-id="aa145-132">All **data** is pushed *only* into Azure Cosmos DB, thus you can avoid multi-casting issues.</span></span>
 2. <span data-ttu-id="aa145-133">The **batch layer** has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views.</span><span class="sxs-lookup"><span data-stu-id="aa145-133">The **batch layer** has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views.</span></span>
 3. <span data-ttu-id="aa145-134">The **serving layer** is discussed in the next section.</span><span class="sxs-lookup"><span data-stu-id="aa145-134">The **serving layer** is discussed in the next section.</span></span>
 4. <span data-ttu-id="aa145-135">The **speed layer** utilizes HDInsight (Apache Spark) to read the Azure Cosmos DB change feed.</span><span class="sxs-lookup"><span data-stu-id="aa145-135">The **speed layer** utilizes HDInsight (Apache Spark) to read the Azure Cosmos DB change feed.</span></span> <span data-ttu-id="aa145-136">This enables you to persist your data as well as to query and process it concurrently.</span><span class="sxs-lookup"><span data-stu-id="aa145-136">This enables you to persist your data as well as to query and process it concurrently.</span></span>
 5. <span data-ttu-id="aa145-137">All queries can be answered by merging results from batch views and real-time views or pinging them individually.</span><span class="sxs-lookup"><span data-stu-id="aa145-137">All queries can be answered by merging results from batch views and real-time views or pinging them individually.</span></span>
 
### <a name="code-example-spark-structured-streaming-to-an-azure-cosmos-db-change-feed"></a><span data-ttu-id="aa145-138">Code Example: Spark structured streaming to an Azure Cosmos DB change feed</span><span class="sxs-lookup"><span data-stu-id="aa145-138">Code Example: Spark structured streaming to an Azure Cosmos DB change feed</span></span>
<span data-ttu-id="aa145-139">To run a quick prototype of the Azure Cosmos DB change feed as part of the **speed layer**, can test it out using Twitter data as part of the [Stream Processing Changes using Azure Cosmos DB Change Feed and Apache Spark](https://github.com/Azure/azure-cosmosdb-spark/wiki/Stream-Processing-Changes-using-Azure-Cosmos-DB-Change-Feed-and-Apache-Spark) example.</span><span class="sxs-lookup"><span data-stu-id="aa145-139">To run a quick prototype of the Azure Cosmos DB change feed as part of the **speed layer**, can test it out using Twitter data as part of the [Stream Processing Changes using Azure Cosmos DB Change Feed and Apache Spark](https://github.com/Azure/azure-cosmosdb-spark/wiki/Stream-Processing-Changes-using-Azure-Cosmos-DB-Change-Feed-and-Apache-Spark) example.</span></span> <span data-ttu-id="aa145-140">To jump-start your Twitter output, see the code sample in [Stream feed from Twitter to Cosmos DB](https://github.com/tknandu/TwitterCosmosDBFeed).</span><span class="sxs-lookup"><span data-stu-id="aa145-140">To jump-start your Twitter output, see the code sample in [Stream feed from Twitter to Cosmos DB](https://github.com/tknandu/TwitterCosmosDBFeed).</span></span> <span data-ttu-id="aa145-141">With the preceding example, you're loading Twitter data into Azure Cosmos DB and you can then set up your HDInsight (Apache Spark) cluster to connect to the change feed.</span><span class="sxs-lookup"><span data-stu-id="aa145-141">With the preceding example, you're loading Twitter data into Azure Cosmos DB and you can then set up your HDInsight (Apache Spark) cluster to connect to the change feed.</span></span> <span data-ttu-id="aa145-142">For more information on how to set up this configuration, see [Apache Spark to Azure Cosmos DB Connector Setup](https://github.com/Azure/azure-cosmosdb-spark/wiki/Spark-to-Cosmos-DB-Connector-Setup).</span><span class="sxs-lookup"><span data-stu-id="aa145-142">For more information on how to set up this configuration, see [Apache Spark to Azure Cosmos DB Connector Setup](https://github.com/Azure/azure-cosmosdb-spark/wiki/Spark-to-Cosmos-DB-Connector-Setup).</span></span>  

<span data-ttu-id="aa145-143">The following code snippet shows how to configure `spark-shell` to run a structured streaming job to connect to an Azure Cosmos DB change feed, which reviews the real-time Twitter data stream, to perform a running interval count.</span><span class="sxs-lookup"><span data-stu-id="aa145-143">The following code snippet shows how to configure `spark-shell` to run a structured streaming job to connect to an Azure Cosmos DB change feed, which reviews the real-time Twitter data stream, to perform a running interval count.</span></span>

```
// Import Libraries
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark.config.Config
import org.codehaus.jackson.map.ObjectMapper
import com.microsoft.azure.cosmosdb.spark.streaming._
import java.time._


// Configure connection to Azure Cosmos DB Change Feed
val sourceConfigMap = Map(
"Endpoint" -> "[COSMOSDB ENDPOINT]",
"Masterkey" -> "[MASTER KEY]",
"Database" -> "[DATABASE]",
"Collection" -> "[COLLECTION]",
"ConnectionMode" -> "Gateway",
"ChangeFeedCheckpointLocation" -> "checkpointlocation",
"changefeedqueryname" -> "Streaming Query from Cosmos DB Change Feed Interval Count")

// Start reading change feed as a stream
var streamData = spark.readStream.format(classOf[CosmosDBSourceProvider].getName).options(sourceConfigMap).load()

// Start streaming query to console sink
val query = streamData.withColumn("countcol", streamData.col("id").substr(0, 0)).groupBy("countcol").count().writeStream.outputMode("complete").format("console").start()
```

<span data-ttu-id="aa145-144">For complete code samples, see [azure-cosmosdb-spark/lambda/samples](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples/lambda), including:</span><span class="sxs-lookup"><span data-stu-id="aa145-144">For complete code samples, see [azure-cosmosdb-spark/lambda/samples](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples/lambda), including:</span></span>
* [<span data-ttu-id="aa145-145">Streaming Query from Cosmos DB Change Feed.scala</span><span class="sxs-lookup"><span data-stu-id="aa145-145">Streaming Query from Cosmos DB Change Feed.scala</span></span>](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Query%20from%20Cosmos%20DB%20Change%20Feed.scala)
* [<span data-ttu-id="aa145-146">Streaming Tags Query from Cosmos DB Change Feed.scala</span><span class="sxs-lookup"><span data-stu-id="aa145-146">Streaming Tags Query from Cosmos DB Change Feed.scala</span></span>](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Tags%20Query%20from%20Cosmos%20DB%20Change%20Feed%20.scala)

<span data-ttu-id="aa145-147">The output of this is a `spark-shell` console, which continuously runs a structured streaming job that performs an interval count against the Twitter data from the Azure Cosmos DB change feed.</span><span class="sxs-lookup"><span data-stu-id="aa145-147">The output of this is a `spark-shell` console, which continuously runs a structured streaming job that performs an interval count against the Twitter data from the Azure Cosmos DB change feed.</span></span> <span data-ttu-id="aa145-148">The following image shows the output of the stream job and the interval counts.</span><span class="sxs-lookup"><span data-stu-id="aa145-148">The following image shows the output of the stream job and the interval counts.</span></span>

![Streaming output showing the interval count against the Twitter data from the Azure Cosmos DB change feed](./media/lambda-architecture/lambda-architecture-speed-layer-twitter-count.png) 

<span data-ttu-id="aa145-150">For more information on Azure Cosmos DB change feed, see:</span><span class="sxs-lookup"><span data-stu-id="aa145-150">For more information on Azure Cosmos DB change feed, see:</span></span>

* [<span data-ttu-id="aa145-151">Working with the change feed support in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa145-151">Working with the change feed support in Azure Cosmos DB</span></span>](change-feed.md)
* [<span data-ttu-id="aa145-152">Introducing the Azure CosmosDB Change Feed Processor Library</span><span class="sxs-lookup"><span data-stu-id="aa145-152">Introducing the Azure CosmosDB Change Feed Processor Library</span></span>](https://azure.microsoft.com/blog/introducing-the-azure-cosmosdb-change-feed-processor-library/)
* [<span data-ttu-id="aa145-153">Stream Processing Changes: Azure CosmosDB change feed + Apache Spark</span><span class="sxs-lookup"><span data-stu-id="aa145-153">Stream Processing Changes: Azure CosmosDB change feed + Apache Spark</span></span>](https://azure.microsoft.com/blog/stream-processing-changes-azure-cosmosdb-change-feed-apache-spark/)

## <a name="batch-and-serving-layers"></a><span data-ttu-id="aa145-154">Batch and serving layers</span><span class="sxs-lookup"><span data-stu-id="aa145-154">Batch and serving layers</span></span>
<span data-ttu-id="aa145-155">Since the new data is loaded into Azure Cosmos DB (where the change feed is being used for the speed layer), this is where the **master dataset** (an immutable, append-only set of raw data) resides.</span><span class="sxs-lookup"><span data-stu-id="aa145-155">Since the new data is loaded into Azure Cosmos DB (where the change feed is being used for the speed layer), this is where the **master dataset** (an immutable, append-only set of raw data) resides.</span></span> <span data-ttu-id="aa145-156">From this point onwards, use HDInsight (Apache Spark) to perform the pre-compute functions from the **batch layer** to **serving layer**, as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="aa145-156">From this point onwards, use HDInsight (Apache Spark) to perform the pre-compute functions from the **batch layer** to **serving layer**, as shown in the following image:</span></span>

![Diagram highlighting the batch layer and serving layer of the lambda architecture](./media/lambda-architecture/lambda-architecture-batch-serve.png)

<span data-ttu-id="aa145-158">What's important in these layers:</span><span class="sxs-lookup"><span data-stu-id="aa145-158">What's important in these layers:</span></span>

 1. <span data-ttu-id="aa145-159">All **data** is pushed only into Azure Cosmos DB (to avoid multi-cast issues).</span><span class="sxs-lookup"><span data-stu-id="aa145-159">All **data** is pushed only into Azure Cosmos DB (to avoid multi-cast issues).</span></span>
 2. <span data-ttu-id="aa145-160">The **batch layer** has a master dataset (immutable, append-only set of raw data) stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa145-160">The **batch layer** has a master dataset (immutable, append-only set of raw data) stored in Azure Cosmos DB.</span></span> <span data-ttu-id="aa145-161">Using HDI Spark, you can pre-compute your aggregations to be stored in your computed batch views.</span><span class="sxs-lookup"><span data-stu-id="aa145-161">Using HDI Spark, you can pre-compute your aggregations to be stored in your computed batch views.</span></span>
 3. <span data-ttu-id="aa145-162">The **serving layer** is an Azure Cosmos DB database with collections for the master dataset and computed batch view.</span><span class="sxs-lookup"><span data-stu-id="aa145-162">The **serving layer** is an Azure Cosmos DB database with collections for the master dataset and computed batch view.</span></span>
 4. <span data-ttu-id="aa145-163">The **speed layer** is discussed later in this article.</span><span class="sxs-lookup"><span data-stu-id="aa145-163">The **speed layer** is discussed later in this article.</span></span>
 5. <span data-ttu-id="aa145-164">All queries can be answered by merging results from the batch views and real-time views, or pinging them individually.</span><span class="sxs-lookup"><span data-stu-id="aa145-164">All queries can be answered by merging results from the batch views and real-time views, or pinging them individually.</span></span>

### <a name="code-example-pre-computing-batch-views"></a><span data-ttu-id="aa145-165">Code example: Pre-computing batch views</span><span class="sxs-lookup"><span data-stu-id="aa145-165">Code example: Pre-computing batch views</span></span>
<span data-ttu-id="aa145-166">To showcase how to execute pre-calculated views against your **master dataset** from Apache Spark to Azure Cosmos DB, use the following code snippets from the notebooks [Lambda Architecture Rearchitected - Batch Layer](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb) and [Lambda Architecture Rearchitected - Batch to Serving Layer](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb).</span><span class="sxs-lookup"><span data-stu-id="aa145-166">To showcase how to execute pre-calculated views against your **master dataset** from Apache Spark to Azure Cosmos DB, use the following code snippets from the notebooks [Lambda Architecture Rearchitected - Batch Layer](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb) and [Lambda Architecture Rearchitected - Batch to Serving Layer](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb).</span></span> <span data-ttu-id="aa145-167">In this scenario, use the Twitter data stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa145-167">In this scenario, use the Twitter data stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="aa145-168">Let's start by creating the configuration connection to the Twitter data within Azure Cosmos DB using the PySpark code below.</span><span class="sxs-lookup"><span data-stu-id="aa145-168">Let's start by creating the configuration connection to the Twitter data within Azure Cosmos DB using the PySpark code below.</span></span>

```
# Configuration to connect to Azure Cosmos DB
tweetsConfig = {
  "Endpoint" : "[Endpoint URL]",
  "Masterkey" : "[Master Key]",
  "Database" : "[Database]",
  "Collection" : "[Collection]", 
  "preferredRegions" : "[Preferred Regions]",
  "SamplingRatio" : "1.0",
  "schema_samplesize" : "200000",
  "query_custom" : "[Cosmos DB SQL Query]"
}

# Create DataFrame
tweets = spark.read.format("com.microsoft.azure.cosmosdb.spark").options(**tweetsConfig).load()

# Create Temp View (to run Spark SQL statements)
tweets.createOrReplaceTempView("tweets")
```

<span data-ttu-id="aa145-169">Next, let's run the following Spark SQL statement to determine the top 10 hashtags of the set of tweets.</span><span class="sxs-lookup"><span data-stu-id="aa145-169">Next, let's run the following Spark SQL statement to determine the top 10 hashtags of the set of tweets.</span></span> <span data-ttu-id="aa145-170">For this Spark SQL query, we're running this in a Jupyter notebook without the output bar chart directly following this code snippet.</span><span class="sxs-lookup"><span data-stu-id="aa145-170">For this Spark SQL query, we're running this in a Jupyter notebook without the output bar chart directly following this code snippet.</span></span>

```
%%sql
select hashtags.text, count(distinct id) as tweets
from (
  select 
    explode(hashtags) as hashtags,
    id
  from tweets
) a
group by hashtags.text
order by tweets desc
limit 10
```

![Chart showing the number of tweets per hashtag](./media/lambda-architecture/lambda-architecture-batch-hashtags-bar-chart.png)

<span data-ttu-id="aa145-172">Now that you have your query, let's save it back to a collection by using the Spark Connector to save the output data into a different collection.</span><span class="sxs-lookup"><span data-stu-id="aa145-172">Now that you have your query, let's save it back to a collection by using the Spark Connector to save the output data into a different collection.</span></span>  <span data-ttu-id="aa145-173">In this example, use Scala to showcase the connection.</span><span class="sxs-lookup"><span data-stu-id="aa145-173">In this example, use Scala to showcase the connection.</span></span> <span data-ttu-id="aa145-174">Similar to the previous example, create the configuration connection to save the Apache Spark DataFrame to a different Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="aa145-174">Similar to the previous example, create the configuration connection to save the Apache Spark DataFrame to a different Azure Cosmos DB collection.</span></span>

```
val writeConfigMap = Map(
    "Endpoint" -> "[Endpoint URL]",
    "Masterkey" -> "[Master Key]",
    "Database" -> "[Database]",
    "Collection" -> "[New Collection]", 
    "preferredRegions" -> "[Preferred Regions]",
    "SamplingRatio" -> "1.0",
    "schema_samplesize" -> "200000"
)

// Configuration to write
val writeConfig = Config(writeConfigMap)

```

<span data-ttu-id="aa145-175">After specifying the `SaveMode` (indicating whether to `Overwrite` or `Append` documents), create a `tweets_bytags` DataFrame similar to the Spark SQL query in the previous example.</span><span class="sxs-lookup"><span data-stu-id="aa145-175">After specifying the `SaveMode` (indicating whether to `Overwrite` or `Append` documents), create a `tweets_bytags` DataFrame similar to the Spark SQL query in the previous example.</span></span>  <span data-ttu-id="aa145-176">With the `tweets_bytags` DataFrame created, you can save it using the `write` method using the previously specified `writeConfig`.</span><span class="sxs-lookup"><span data-stu-id="aa145-176">With the `tweets_bytags` DataFrame created, you can save it using the `write` method using the previously specified `writeConfig`.</span></span>

```
// Import SaveMode so you can Overwrite, Append, ErrorIfExists, Ignore
import org.apache.spark.sql.{Row, SaveMode, SparkSession}

// Create new DataFrame of tweets tags
val tweets_bytags = spark.sql("select hashtags.text as hashtags, count(distinct id) as tweets from ( select explode(hashtags) as hashtags, id from tweets ) a group by hashtags.text order by tweets desc")

// Save to Cosmos DB (using Append in this case)
tweets_bytags.write.mode(SaveMode.Overwrite).cosmosDB(writeConfig)
```

<span data-ttu-id="aa145-177">This last statement now has saved your Spark DataFrame into a new Azure Cosmos DB collection; from a lambda architecture perspective, this is your **batch view** within the **serving layer**.</span><span class="sxs-lookup"><span data-stu-id="aa145-177">This last statement now has saved your Spark DataFrame into a new Azure Cosmos DB collection; from a lambda architecture perspective, this is your **batch view** within the **serving layer**.</span></span>
 
#### <a name="resources"></a><span data-ttu-id="aa145-178">Resources</span><span class="sxs-lookup"><span data-stu-id="aa145-178">Resources</span></span>

<span data-ttu-id="aa145-179">For complete code samples, see [azure-cosmosdb-spark/lambda/samples](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples/lambda) including:</span><span class="sxs-lookup"><span data-stu-id="aa145-179">For complete code samples, see [azure-cosmosdb-spark/lambda/samples](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples/lambda) including:</span></span>
* <span data-ttu-id="aa145-180">Lambda Architecture Rearchitected - Batch Layer [HTML](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.html) | [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb)</span><span class="sxs-lookup"><span data-stu-id="aa145-180">Lambda Architecture Rearchitected - Batch Layer [HTML](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.html) | [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb)</span></span>
* <span data-ttu-id="aa145-181">Lambda Architecture Rearchitected - Batch to Serving Layer [HTML](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.html) | [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb)</span><span class="sxs-lookup"><span data-stu-id="aa145-181">Lambda Architecture Rearchitected - Batch to Serving Layer [HTML](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.html) | [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb)</span></span>

## <a name="speed-layer"></a><span data-ttu-id="aa145-182">Speed layer</span><span class="sxs-lookup"><span data-stu-id="aa145-182">Speed layer</span></span>
<span data-ttu-id="aa145-183">As previously noted, using the Azure Cosmos DB Change Feed Library allows you to simplify the operations between the batch and speed layers.</span><span class="sxs-lookup"><span data-stu-id="aa145-183">As previously noted, using the Azure Cosmos DB Change Feed Library allows you to simplify the operations between the batch and speed layers.</span></span> <span data-ttu-id="aa145-184">In this architecture, use Apache Spark (via HDInsight) to perform the *structured streaming* queries against the data.</span><span class="sxs-lookup"><span data-stu-id="aa145-184">In this architecture, use Apache Spark (via HDInsight) to perform the *structured streaming* queries against the data.</span></span> <span data-ttu-id="aa145-185">You may also want to temporarily persist the results of your structured streaming queries so other systems can access this data.</span><span class="sxs-lookup"><span data-stu-id="aa145-185">You may also want to temporarily persist the results of your structured streaming queries so other systems can access this data.</span></span>

![Diagram highlighting the speed layer of the lambda architecture](./media/lambda-architecture/lambda-architecture-speed.png)

<span data-ttu-id="aa145-187">To do this, create a separate Azure Cosmos DB collection to save the results of your structured streaming queries.</span><span class="sxs-lookup"><span data-stu-id="aa145-187">To do this, create a separate Azure Cosmos DB collection to save the results of your structured streaming queries.</span></span>  <span data-ttu-id="aa145-188">This allows you to have other systems access this information not just Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="aa145-188">This allows you to have other systems access this information not just Apache Spark.</span></span> <span data-ttu-id="aa145-189">As well with the Cosmos DB Time-to-Live (TTL) feature, you can configure your documents to be automatically deleted after a set duration.</span><span class="sxs-lookup"><span data-stu-id="aa145-189">As well with the Cosmos DB Time-to-Live (TTL) feature, you can configure your documents to be automatically deleted after a set duration.</span></span>  <span data-ttu-id="aa145-190">For more information on the Azure Cosmos DB TTL feature, see [Expire data in Azure Cosmos DB collections automatically with time to live](time-to-live.md)</span><span class="sxs-lookup"><span data-stu-id="aa145-190">For more information on the Azure Cosmos DB TTL feature, see [Expire data in Azure Cosmos DB collections automatically with time to live](time-to-live.md)</span></span>

```
// Import Libraries
import com.microsoft.azure.cosmosdb.spark._
import com.microsoft.azure.cosmosdb.spark.schema._
import com.microsoft.azure.cosmosdb.spark.config.Config
import org.codehaus.jackson.map.ObjectMapper
import com.microsoft.azure.cosmosdb.spark.streaming._
import java.time._


// Configure connection to Azure Cosmos DB Change Feed
val sourceCollectionName = "[SOURCE COLLECTION NAME]"
val sinkCollectionName = "[SINK COLLECTION NAME]"

val configMap = Map(
"Endpoint" -> "[COSMOSDB ENDPOINT]",
"Masterkey" -> "[COSMOSDB MASTER KEY]",
"Database" -> "[DATABASE NAME]",
"Collection" -> sourceCollectionName,
"ChangeFeedCheckpointLocation" -> "changefeedcheckpointlocation")

val sourceConfigMap = configMap.+(("changefeedqueryname", "Structured Stream replication streaming test"))

// Start to read the stream
var streamData = spark.readStream.format(classOf[CosmosDBSourceProvider].getName).options(sourceConfigMap).load()
val sinkConfigMap = configMap.-("collection").+(("collection", sinkCollectionName))

// Start the stream writer to new collection
val streamingQueryWriter = streamData.writeStream.format(classOf[CosmosDBSinkProvider].getName).outputMode("append").options(sinkConfigMap).option("checkpointLocation", "streamingcheckpointlocation")
var streamingQuery = streamingQueryWriter.start()

```

## <a name="lambda-architecture-rearchitected"></a><span data-ttu-id="aa145-191">Lambda architecture: Rearchitected</span><span class="sxs-lookup"><span data-stu-id="aa145-191">Lambda architecture: Rearchitected</span></span>
<span data-ttu-id="aa145-192">As noted in the previous sections, you can simplify the original lambda architecture by using the following components:</span><span class="sxs-lookup"><span data-stu-id="aa145-192">As noted in the previous sections, you can simplify the original lambda architecture by using the following components:</span></span>
* <span data-ttu-id="aa145-193">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa145-193">Azure Cosmos DB</span></span>
* <span data-ttu-id="aa145-194">The Azure Cosmos DB Change Feed Library to avoid the need to multi-cast your data between the batch and speed layers</span><span class="sxs-lookup"><span data-stu-id="aa145-194">The Azure Cosmos DB Change Feed Library to avoid the need to multi-cast your data between the batch and speed layers</span></span>
* <span data-ttu-id="aa145-195">Apache Spark on HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa145-195">Apache Spark on HDInsight</span></span>
* <span data-ttu-id="aa145-196">The Spark Connector for Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aa145-196">The Spark Connector for Azure Cosmos DB</span></span>

![Diagram showing the rearchitecture of the lambda architecture using Azure Cosmos DB, Spark, and the Azure Cosmos DB Change Feed API](./media/lambda-architecture/lambda-architecture-re-architected.png)

<span data-ttu-id="aa145-198">With this design, you only need two managed services, Azure Cosmos DB and HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aa145-198">With this design, you only need two managed services, Azure Cosmos DB and HDInsight.</span></span> <span data-ttu-id="aa145-199">Together, they address the batch, serving, and speed layers of the lambda architecture.</span><span class="sxs-lookup"><span data-stu-id="aa145-199">Together, they address the batch, serving, and speed layers of the lambda architecture.</span></span> <span data-ttu-id="aa145-200">This simplifies not only the operations but also the data flow.</span><span class="sxs-lookup"><span data-stu-id="aa145-200">This simplifies not only the operations but also the data flow.</span></span> 
 1. <span data-ttu-id="aa145-201">All data is pushed into Azure Cosmos DB for processing</span><span class="sxs-lookup"><span data-stu-id="aa145-201">All data is pushed into Azure Cosmos DB for processing</span></span>
 2. <span data-ttu-id="aa145-202">The batch layer has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views</span><span class="sxs-lookup"><span data-stu-id="aa145-202">The batch layer has a master dataset (immutable, append-only set of raw data) and pre-computes the batch views</span></span>
 3. <span data-ttu-id="aa145-203">The serving layer has batch views of data for fast queries.</span><span class="sxs-lookup"><span data-stu-id="aa145-203">The serving layer has batch views of data for fast queries.</span></span>
 4. <span data-ttu-id="aa145-204">The speed layer compensates for processing time (to the serving layer) and deals with recent data only.</span><span class="sxs-lookup"><span data-stu-id="aa145-204">The speed layer compensates for processing time (to the serving layer) and deals with recent data only.</span></span>
 5. <span data-ttu-id="aa145-205">All queries can be answered by merging results from batch views and real-time views.</span><span class="sxs-lookup"><span data-stu-id="aa145-205">All queries can be answered by merging results from batch views and real-time views.</span></span>

### <a name="resources"></a><span data-ttu-id="aa145-206">Resources</span><span class="sxs-lookup"><span data-stu-id="aa145-206">Resources</span></span>

 * <span data-ttu-id="aa145-207">**New data**: The [stream feed from Twitter to CosmosDB](https://github.com/tknandu/TwitterCosmosDBFeed), which is the mechanism to push new data into Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aa145-207">**New data**: The [stream feed from Twitter to CosmosDB](https://github.com/tknandu/TwitterCosmosDBFeed), which is the mechanism to push new data into Azure Cosmos DB.</span></span>
 * <span data-ttu-id="aa145-208">**Batch layer:** The batch layer is composed of the *master dataset* (an immutable, append-only set of raw data) and the ability to pre-compute batch views of the data that are pushed into the **serving layer**.</span><span class="sxs-lookup"><span data-stu-id="aa145-208">**Batch layer:** The batch layer is composed of the *master dataset* (an immutable, append-only set of raw data) and the ability to pre-compute batch views of the data that are pushed into the **serving layer**.</span></span>
    * <span data-ttu-id="aa145-209">The **Lambda Architecture Rearchitected - Batch Layer** notebook [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb) | [html](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.html) queries the *master dataset* set of batch views.</span><span class="sxs-lookup"><span data-stu-id="aa145-209">The **Lambda Architecture Rearchitected - Batch Layer** notebook [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.ipynb) | [html](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20Layer.html) queries the *master dataset* set of batch views.</span></span>
 * <span data-ttu-id="aa145-210">**Serving layer:** The **serving layer** is composed of pre-computed data resulting in batch views (for example aggregations, specific slicers, etc.) for fast queries.</span><span class="sxs-lookup"><span data-stu-id="aa145-210">**Serving layer:** The **serving layer** is composed of pre-computed data resulting in batch views (for example aggregations, specific slicers, etc.) for fast queries.</span></span>
    * <span data-ttu-id="aa145-211">The **Lambda Architecture Rearchitected - Batch to Serving Layer** notebook [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb) | [html](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.html) pushes the batch data to the serving layer; that is, Spark queries a batch collection of tweets, processes it, and stores it into another collection (a computed batch).</span><span class="sxs-lookup"><span data-stu-id="aa145-211">The **Lambda Architecture Rearchitected - Batch to Serving Layer** notebook [ipynb](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.ipynb) | [html](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Lambda%20Architecture%20Re-architected%20-%20Batch%20to%20Serving%20Layer.html) pushes the batch data to the serving layer; that is, Spark queries a batch collection of tweets, processes it, and stores it into another collection (a computed batch).</span></span>
* <span data-ttu-id="aa145-212">**Speed layer:** The **speed layer** is composed of Spark utilizing the Azure Cosmos DB change feed to read and act on immediately.</span><span class="sxs-lookup"><span data-stu-id="aa145-212">**Speed layer:** The **speed layer** is composed of Spark utilizing the Azure Cosmos DB change feed to read and act on immediately.</span></span> <span data-ttu-id="aa145-213">The data can also be saved to *computed RT* so that other systems can query the processed real-time data as opposed to running a real-time query themselves.</span><span class="sxs-lookup"><span data-stu-id="aa145-213">The data can also be saved to *computed RT* so that other systems can query the processed real-time data as opposed to running a real-time query themselves.</span></span>
    * <span data-ttu-id="aa145-214">The [Streaming Query from Cosmos DB Change Feed](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Query%20from%20Cosmos%20DB%20Change%20Feed.scala) scala script executes a streaming query from the Azure Cosmos DB change feed to compute an interval count from the spark-shell.</span><span class="sxs-lookup"><span data-stu-id="aa145-214">The [Streaming Query from Cosmos DB Change Feed](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Query%20from%20Cosmos%20DB%20Change%20Feed.scala) scala script executes a streaming query from the Azure Cosmos DB change feed to compute an interval count from the spark-shell.</span></span>
    * <span data-ttu-id="aa145-215">The [Streaming Tags Query from Cosmos DB Change Feed](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Tags%20Query%20from%20Cosmos%20DB%20Change%20Feed%20.scala) scala script executes a streaming query from the Azure Cosmos DB change feed to compute an interval count of tags from the spark-shell.</span><span class="sxs-lookup"><span data-stu-id="aa145-215">The [Streaming Tags Query from Cosmos DB Change Feed](https://github.com/Azure/azure-cosmosdb-spark/blob/master/samples/lambda/Streaming%20Tags%20Query%20from%20Cosmos%20DB%20Change%20Feed%20.scala) scala script executes a streaming query from the Azure Cosmos DB change feed to compute an interval count of tags from the spark-shell.</span></span>
  
## <a name="next-steps"></a><span data-ttu-id="aa145-216">Next steps</span><span class="sxs-lookup"><span data-stu-id="aa145-216">Next steps</span></span>
<span data-ttu-id="aa145-217">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span><span class="sxs-lookup"><span data-stu-id="aa145-217">If you haven't already, download the Spark to Azure Cosmos DB connector from the [azure-cosmosdb-spark](https://github.com/Azure/azure-cosmosdb-spark) GitHub repository and explore the additional resources in the repo:</span></span>
* [<span data-ttu-id="aa145-218">Lambda architecture</span><span class="sxs-lookup"><span data-stu-id="aa145-218">Lambda architecture</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples/lambda)
* [<span data-ttu-id="aa145-219">Distributed aggregations examples</span><span class="sxs-lookup"><span data-stu-id="aa145-219">Distributed aggregations examples</span></span>](https://github.com/Azure/azure-documentdb-spark/wiki/Aggregations-Examples)
* [<span data-ttu-id="aa145-220">Sample scripts and notebooks</span><span class="sxs-lookup"><span data-stu-id="aa145-220">Sample scripts and notebooks</span></span>](https://github.com/Azure/azure-cosmosdb-spark/tree/master/samples)
* [<span data-ttu-id="aa145-221">Structured streaming demos</span><span class="sxs-lookup"><span data-stu-id="aa145-221">Structured streaming demos</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Structured-Stream-demos)
* [<span data-ttu-id="aa145-222">Change feed demos</span><span class="sxs-lookup"><span data-stu-id="aa145-222">Change feed demos</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Change-Feed-demos)
* [<span data-ttu-id="aa145-223">Stream processing changes using Azure Cosmos DB Change Feed and Apache Spark</span><span class="sxs-lookup"><span data-stu-id="aa145-223">Stream processing changes using Azure Cosmos DB Change Feed and Apache Spark</span></span>](https://github.com/Azure/azure-cosmosdb-spark/wiki/Stream-Processing-Changes-using-Azure-Cosmos-DB-Change-Feed-and-Apache-Spark)

<span data-ttu-id="aa145-224">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/spark/apache-spark-jupyter-spark-sql.md) article.</span><span class="sxs-lookup"><span data-stu-id="aa145-224">You might also want to review the [Apache Spark SQL, DataFrames, and Datasets Guide](http://spark.apache.org/docs/latest/sql-programming-guide.html) and the [Apache Spark on Azure HDInsight](../hdinsight/spark/apache-spark-jupyter-spark-sql.md) article.</span></span>
