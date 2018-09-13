---
title: Integrating Apache Spark with Azure Event Hubs | Microsoft Docs
description: Integrate with Apache Spark to enable Structured Streaming with Event Hubs
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: ''
ms.service: event-hubs
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/21/2018
ms.author: shvija
ms.openlocfilehash: 688daedf29bbd68c7451be66b47ac90e404d4093
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864576"
---
# <a name="integrating-apache-spark-with-azure-event-hubs"></a><span data-ttu-id="39eaa-103">Integrating Apache Spark with Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="39eaa-103">Integrating Apache Spark with Azure Event Hubs</span></span>

<span data-ttu-id="39eaa-104">Azure Event Hubs seamlessly integrates with [Apache Spark](https://spark.apache.org/) to enable building distributed streaming applications.</span><span class="sxs-lookup"><span data-stu-id="39eaa-104">Azure Event Hubs seamlessly integrates with [Apache Spark](https://spark.apache.org/) to enable building distributed streaming applications.</span></span> <span data-ttu-id="39eaa-105">This integration supports [Spark Core](http://spark.apache.org/docs/latest/rdd-programming-guide.html), [Spark Streaming](http://spark.apache.org/docs/latest/streaming-programming-guide.html), and [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html).</span><span class="sxs-lookup"><span data-stu-id="39eaa-105">This integration supports [Spark Core](http://spark.apache.org/docs/latest/rdd-programming-guide.html), [Spark Streaming](http://spark.apache.org/docs/latest/streaming-programming-guide.html), and [Structured Streaming](https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html).</span></span> <span data-ttu-id="39eaa-106">The Event Hubs connector for Apache Spark is available on [GitHub](https://github.com/Azure/azure-event-hubs-spark).</span><span class="sxs-lookup"><span data-stu-id="39eaa-106">The Event Hubs connector for Apache Spark is available on [GitHub](https://github.com/Azure/azure-event-hubs-spark).</span></span> <span data-ttu-id="39eaa-107">This library is also available for use in Maven projects from the [Maven Central Repository](http://search.maven.org/#artifactdetails%7Ccom.microsoft.azure%7Cazure-eventhubs-spark_2.11%7C2.1.6%7C).</span><span class="sxs-lookup"><span data-stu-id="39eaa-107">This library is also available for use in Maven projects from the [Maven Central Repository](http://search.maven.org/#artifactdetails%7Ccom.microsoft.azure%7Cazure-eventhubs-spark_2.11%7C2.1.6%7C).</span></span>

<span data-ttu-id="39eaa-108">This article describes how to create a continuous application in [Azure Databricks](https://azure.microsoft.com/services/databricks/).</span><span class="sxs-lookup"><span data-stu-id="39eaa-108">This article describes how to create a continuous application in [Azure Databricks](https://azure.microsoft.com/services/databricks/).</span></span> <span data-ttu-id="39eaa-109">While this article uses Azure Databricks, Spark clusters are also available with [HDInsight](../hdinsight/spark/apache-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="39eaa-109">While this article uses Azure Databricks, Spark clusters are also available with [HDInsight](../hdinsight/spark/apache-spark-overview.md).</span></span>

<span data-ttu-id="39eaa-110">The example in this article uses two Scala notebooks: one for streaming events from an event hub and another for sending events back to it.</span><span class="sxs-lookup"><span data-stu-id="39eaa-110">The example in this article uses two Scala notebooks: one for streaming events from an event hub and another for sending events back to it.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39eaa-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="39eaa-111">Prerequisites</span></span>

* <span data-ttu-id="39eaa-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="39eaa-112">An Azure subscription.</span></span> <span data-ttu-id="39eaa-113">If you do not have one, [create a free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span><span class="sxs-lookup"><span data-stu-id="39eaa-113">If you do not have one, [create a free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio).</span></span>
* <span data-ttu-id="39eaa-114">An Event Hubs instance.</span><span class="sxs-lookup"><span data-stu-id="39eaa-114">An Event Hubs instance.</span></span> <span data-ttu-id="39eaa-115">If you do not have one, [create one](event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="39eaa-115">If you do not have one, [create one](event-hubs-create.md).</span></span>
* <span data-ttu-id="39eaa-116">An [Azure Databricks](https://azure.microsoft.com/services/databricks/) instance.</span><span class="sxs-lookup"><span data-stu-id="39eaa-116">An [Azure Databricks](https://azure.microsoft.com/services/databricks/) instance.</span></span> <span data-ttu-id="39eaa-117">If you do not have one, [create one](../azure-databricks/quickstart-create-databricks-workspace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="39eaa-117">If you do not have one, [create one](../azure-databricks/quickstart-create-databricks-workspace-portal.md).</span></span>
* <span data-ttu-id="39eaa-118">[Create a library using maven coordinates](https://docs.databricks.com/user-guide/libraries.html#upload-a-maven-package-or-spark-package): `com.microsoft.azure:azure‐eventhubs‐spark_2.11:2.3.1`.</span><span class="sxs-lookup"><span data-stu-id="39eaa-118">[Create a library using maven coordinates](https://docs.databricks.com/user-guide/libraries.html#upload-a-maven-package-or-spark-package): `com.microsoft.azure:azure‐eventhubs‐spark_2.11:2.3.1`.</span></span>

<span data-ttu-id="39eaa-119">Stream events from your event hub using the following code:</span><span class="sxs-lookup"><span data-stu-id="39eaa-119">Stream events from your event hub using the following code:</span></span>

```scala
import org.apache.spark.eventhubs._

// To connect to an event hub, EntityPath is required as part of the connection string.
// Here, we assume that the connection string from the Azure portal does not have the EntityPath part.
val connectionString = ConnectionStringBuilder("{EVENT HUB CONNECTION STRING FROM AZURE PORTAL}")
  .setEventHubName("{EVENT HUB NAME}")
  .build 
val ehConf = EventHubsConf(connectionString)
  .setStartingPosition(EventPosition.fromEndOfStream)

// Create a stream that reads data from the specified Event Hub.
val reader = spark.readStream
  .format("eventhubs")
  .options(ehConf.toMap)
  .load()
val eventhubs = reader.select($"body" cast "string")

eventhubs.writeStream
  .format("console")
  .outputMode("append")
  .start()
  .awaitTermination()
```
<span data-ttu-id="39eaa-120">The following code sends events to your event hub with the Spark batch APIs.</span><span class="sxs-lookup"><span data-stu-id="39eaa-120">The following code sends events to your event hub with the Spark batch APIs.</span></span> <span data-ttu-id="39eaa-121">You can also write a streaming query to send events to the event hub:</span><span class="sxs-lookup"><span data-stu-id="39eaa-121">You can also write a streaming query to send events to the event hub:</span></span>

```scala
import org.apache.spark.eventhubs._
import org.apache.spark.sql.functions._

// To connect to an event hub, EntityPath is required as part of the connection string.
// Here, we assume that the connection string from the Azure portal does not have the EntityPath part.
val connectionString = ConnectionStringBuilder("{EVENT HUB CONNECTION STRING FROM AZURE PORTAL}")
  .setEventHubName("{EVENT HUB NAME}")
  .build
val ehConf = EventHubsConf(connectionString)

// Create random strings as the body of the message.
val bodyColumn = concat(lit("random nunmber: "), rand()).as("body")

// Write 200 rows to the specified event hub.
val df = spark.range(200).select(bodyColumn)
df.write
  .format("eventhubs")
  .options(ehConf.toMap)
  .save() 
```

## <a name="next-steps"></a><span data-ttu-id="39eaa-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="39eaa-122">Next steps</span></span>

<span data-ttu-id="39eaa-123">Now you know how to set up a scalable, fault-tolerant stream using the Event Hubs Connector for Apache Spark.</span><span class="sxs-lookup"><span data-stu-id="39eaa-123">Now you know how to set up a scalable, fault-tolerant stream using the Event Hubs Connector for Apache Spark.</span></span> <span data-ttu-id="39eaa-124">Learn more about using Event Hubs with Structured Streaming and Spark Streaming by following these links:</span><span class="sxs-lookup"><span data-stu-id="39eaa-124">Learn more about using Event Hubs with Structured Streaming and Spark Streaming by following these links:</span></span>

* [<span data-ttu-id="39eaa-125">Structured Streaming + Azure Event Hubs Integration Guide</span><span class="sxs-lookup"><span data-stu-id="39eaa-125">Structured Streaming + Azure Event Hubs Integration Guide</span></span>](https://github.com/Azure/azure-event-hubs-spark/blob/master/docs/structured-streaming-eventhubs-integration.md)
* [<span data-ttu-id="39eaa-126">Spark Streaming + Event Hubs Integration Guide</span><span class="sxs-lookup"><span data-stu-id="39eaa-126">Spark Streaming + Event Hubs Integration Guide</span></span>](https://github.com/Azure/azure-event-hubs-spark/blob/master/docs/spark-streaming-eventhubs-integration.md)
