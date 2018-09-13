---
title: Spark Streaming in Azure HDInsight
description: How to use Spark Streaming applications on HDInsight Spark clusters.
services: hdinsight
ms.service: hdinsight
author: maxluk
ms.author: maxluk
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/05/2018
ms.openlocfilehash: 229c3eff0db4f3689f4e2e3fd457410ecccb8ba7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966648"
---
# <a name="overview-of-spark-streaming"></a><span data-ttu-id="ad946-103">Overview of Spark Streaming</span><span class="sxs-lookup"><span data-stu-id="ad946-103">Overview of Spark Streaming</span></span>

<span data-ttu-id="ad946-104">Spark Streaming provides data stream processing on HDInsight Spark clusters, with a guarantee that any input event is processed exactly once, even if a node failure occurs.</span><span class="sxs-lookup"><span data-stu-id="ad946-104">Spark Streaming provides data stream processing on HDInsight Spark clusters, with a guarantee that any input event is processed exactly once, even if a node failure occurs.</span></span> <span data-ttu-id="ad946-105">A Spark Stream is a long-running job that receives input data from a wide variety of sources, including Azure Event Hubs, an Azure IoT Hub, Kafka, Flume, Twitter, ZeroMQ, raw TCP sockets, or from monitoring HDFS filesystems.</span><span class="sxs-lookup"><span data-stu-id="ad946-105">A Spark Stream is a long-running job that receives input data from a wide variety of sources, including Azure Event Hubs, an Azure IoT Hub, Kafka, Flume, Twitter, ZeroMQ, raw TCP sockets, or from monitoring HDFS filesystems.</span></span> <span data-ttu-id="ad946-106">Unlike a solely event-driven process, a Spark Stream batches input data into time windows, such as a 2-second slice, and then transforms each batch of data using map, reduce, join, and extract operations.</span><span class="sxs-lookup"><span data-stu-id="ad946-106">Unlike a solely event-driven process, a Spark Stream batches input data into time windows, such as a 2-second slice, and then transforms each batch of data using map, reduce, join, and extract operations.</span></span> <span data-ttu-id="ad946-107">The Spark Stream then writes the transformed data out to filesystems, databases, dashboards, and the console.</span><span class="sxs-lookup"><span data-stu-id="ad946-107">The Spark Stream then writes the transformed data out to filesystems, databases, dashboards, and the console.</span></span>

![Stream Processing with HDInsight and Spark Streaming](./media/apache-spark-streaming-overview/hdinsight-spark-streaming.png)

<span data-ttu-id="ad946-109">Spark Streaming applications must wait a fraction of a second to collect each *micro-batch* of events before sending that batch on for processing.</span><span class="sxs-lookup"><span data-stu-id="ad946-109">Spark Streaming applications must wait a fraction of a second to collect each *micro-batch* of events before sending that batch on for processing.</span></span> <span data-ttu-id="ad946-110">In contrast, an event-driven application processes each event immediately.</span><span class="sxs-lookup"><span data-stu-id="ad946-110">In contrast, an event-driven application processes each event immediately.</span></span> <span data-ttu-id="ad946-111">Spark Streaming latency is typically under a few seconds.</span><span class="sxs-lookup"><span data-stu-id="ad946-111">Spark Streaming latency is typically under a few seconds.</span></span> <span data-ttu-id="ad946-112">The benefits of the micro-batch approach are more efficient data processing and simpler aggregate calculations.</span><span class="sxs-lookup"><span data-stu-id="ad946-112">The benefits of the micro-batch approach are more efficient data processing and simpler aggregate calculations.</span></span>

## <a name="introducing-the-dstream"></a><span data-ttu-id="ad946-113">Introducing the DStream</span><span class="sxs-lookup"><span data-stu-id="ad946-113">Introducing the DStream</span></span>

<span data-ttu-id="ad946-114">Spark Streaming represents a continuous stream of incoming data using a *discretized stream* called a DStream.</span><span class="sxs-lookup"><span data-stu-id="ad946-114">Spark Streaming represents a continuous stream of incoming data using a *discretized stream* called a DStream.</span></span> <span data-ttu-id="ad946-115">A DStream can be created from input sources such as Event Hubs or Kafka, or by applying transformations on another DStream.</span><span class="sxs-lookup"><span data-stu-id="ad946-115">A DStream can be created from input sources such as Event Hubs or Kafka, or by applying transformations on another DStream.</span></span>

<span data-ttu-id="ad946-116">A DStream provides a layer of abstraction on top of the raw event data.</span><span class="sxs-lookup"><span data-stu-id="ad946-116">A DStream provides a layer of abstraction on top of the raw event data.</span></span> 

<span data-ttu-id="ad946-117">Start with a single event, say a temperature reading from a connected thermostat.</span><span class="sxs-lookup"><span data-stu-id="ad946-117">Start with a single event, say a temperature reading from a connected thermostat.</span></span> <span data-ttu-id="ad946-118">When this event arrives at your Spark Streaming application, the event is stored in a reliable way, where it is replicated on multiple nodes.</span><span class="sxs-lookup"><span data-stu-id="ad946-118">When this event arrives at your Spark Streaming application, the event is stored in a reliable way, where it is replicated on multiple nodes.</span></span> <span data-ttu-id="ad946-119">This fault-tolerance ensures that the failure of any single node will not result in the loss of your event.</span><span class="sxs-lookup"><span data-stu-id="ad946-119">This fault-tolerance ensures that the failure of any single node will not result in the loss of your event.</span></span> <span data-ttu-id="ad946-120">The Spark core uses a data structure that distributes data across multiple nodes in the cluster, where each node generally maintains its own data in-memory for best performance.</span><span class="sxs-lookup"><span data-stu-id="ad946-120">The Spark core uses a data structure that distributes data across multiple nodes in the cluster, where each node generally maintains its own data in-memory for best performance.</span></span> <span data-ttu-id="ad946-121">This data structure is called a *resilient distributed dataset* (RDD).</span><span class="sxs-lookup"><span data-stu-id="ad946-121">This data structure is called a *resilient distributed dataset* (RDD).</span></span>

<span data-ttu-id="ad946-122">Each RDD represents events collected over a user-defined timeframe called the *batch interval*.</span><span class="sxs-lookup"><span data-stu-id="ad946-122">Each RDD represents events collected over a user-defined timeframe called the *batch interval*.</span></span> <span data-ttu-id="ad946-123">As each batch interval elapses, a new RDD is produced that contains all the data from that interval.</span><span class="sxs-lookup"><span data-stu-id="ad946-123">As each batch interval elapses, a new RDD is produced that contains all the data from that interval.</span></span> <span data-ttu-id="ad946-124">The continuous set of RDDs are collected into a DStream.</span><span class="sxs-lookup"><span data-stu-id="ad946-124">The continuous set of RDDs are collected into a DStream.</span></span> <span data-ttu-id="ad946-125">For example, if the batch interval is one second long, your DStream emits a batch every second containing one RDD that contains all the data ingested during that second.</span><span class="sxs-lookup"><span data-stu-id="ad946-125">For example, if the batch interval is one second long, your DStream emits a batch every second containing one RDD that contains all the data ingested during that second.</span></span> <span data-ttu-id="ad946-126">When processing the DStream, the temperature event appears in one of these batches.</span><span class="sxs-lookup"><span data-stu-id="ad946-126">When processing the DStream, the temperature event appears in one of these batches.</span></span> <span data-ttu-id="ad946-127">A Spark Streaming application processes the batches that contain the events and ultimately acts on the data stored in each RDD.</span><span class="sxs-lookup"><span data-stu-id="ad946-127">A Spark Streaming application processes the batches that contain the events and ultimately acts on the data stored in each RDD.</span></span>

![<span data-ttu-id="ad946-128">Example DStream with Temperature Events</span><span class="sxs-lookup"><span data-stu-id="ad946-128">Example DStream with Temperature Events</span></span> ](./media/apache-spark-streaming-overview/hdinsight-spark-streaming-example.png)

## <a name="structure-of-a-spark-streaming-application"></a><span data-ttu-id="ad946-129">Structure of a Spark Streaming application</span><span class="sxs-lookup"><span data-stu-id="ad946-129">Structure of a Spark Streaming application</span></span>

<span data-ttu-id="ad946-130">A Spark Streaming application is a long-running application that receives data from ingest sources, applies transformations to process the data, and then pushes the data out to one or more destinations.</span><span class="sxs-lookup"><span data-stu-id="ad946-130">A Spark Streaming application is a long-running application that receives data from ingest sources, applies transformations to process the data, and then pushes the data out to one or more destinations.</span></span> <span data-ttu-id="ad946-131">The structure of a Spark Streaming application has a static part and a dynamic part.</span><span class="sxs-lookup"><span data-stu-id="ad946-131">The structure of a Spark Streaming application has a static part and a dynamic part.</span></span> <span data-ttu-id="ad946-132">The static part  defines where the data comes from, what processing to do on the data, and where the results should go.</span><span class="sxs-lookup"><span data-stu-id="ad946-132">The static part  defines where the data comes from, what processing to do on the data, and where the results should go.</span></span> <span data-ttu-id="ad946-133">The dynamic part is running  the application indefinitely, waiting for a stop signal.</span><span class="sxs-lookup"><span data-stu-id="ad946-133">The dynamic part is running  the application indefinitely, waiting for a stop signal.</span></span>

<span data-ttu-id="ad946-134">For example, the following simple application  receives a line of text over a TCP socket and counts the number of times each word appears.</span><span class="sxs-lookup"><span data-stu-id="ad946-134">For example, the following simple application  receives a line of text over a TCP socket and counts the number of times each word appears.</span></span>

### <a name="define-the-application"></a><span data-ttu-id="ad946-135">Define the application</span><span class="sxs-lookup"><span data-stu-id="ad946-135">Define the application</span></span>

<span data-ttu-id="ad946-136">The application logic definition has four steps:</span><span class="sxs-lookup"><span data-stu-id="ad946-136">The application logic definition has four steps:</span></span>

1. <span data-ttu-id="ad946-137">Create a StreamingContext.</span><span class="sxs-lookup"><span data-stu-id="ad946-137">Create a StreamingContext.</span></span>
2. <span data-ttu-id="ad946-138">Create a DStream from the StreamingContext.</span><span class="sxs-lookup"><span data-stu-id="ad946-138">Create a DStream from the StreamingContext.</span></span>
3. <span data-ttu-id="ad946-139">Apply transformations to the DStream.</span><span class="sxs-lookup"><span data-stu-id="ad946-139">Apply transformations to the DStream.</span></span>
4. <span data-ttu-id="ad946-140">Output the results.</span><span class="sxs-lookup"><span data-stu-id="ad946-140">Output the results.</span></span>

<span data-ttu-id="ad946-141">This definition is static, and no data is processed until you run the application.</span><span class="sxs-lookup"><span data-stu-id="ad946-141">This definition is static, and no data is processed until you run the application.</span></span>

#### <a name="create-a-streamingcontext"></a><span data-ttu-id="ad946-142">Create a StreamingContext</span><span class="sxs-lookup"><span data-stu-id="ad946-142">Create a StreamingContext</span></span>

<span data-ttu-id="ad946-143">Create a StreamingContext from the SparkContext that points to your cluster.</span><span class="sxs-lookup"><span data-stu-id="ad946-143">Create a StreamingContext from the SparkContext that points to your cluster.</span></span> <span data-ttu-id="ad946-144">When creating a StreamingContext, you specify the size of the batch in seconds, for example:</span><span class="sxs-lookup"><span data-stu-id="ad946-144">When creating a StreamingContext, you specify the size of the batch in seconds, for example:</span></span>

    val ssc = new StreamingContext(spark, Seconds(1))

#### <a name="create-a-dstream"></a><span data-ttu-id="ad946-145">Create a DStream</span><span class="sxs-lookup"><span data-stu-id="ad946-145">Create a DStream</span></span>

<span data-ttu-id="ad946-146">With the StreamingContext instance, create an input DStream for your input source.</span><span class="sxs-lookup"><span data-stu-id="ad946-146">With the StreamingContext instance, create an input DStream for your input source.</span></span> <span data-ttu-id="ad946-147">In this case, the application is watching for the appearance of new files in the default storage attached to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ad946-147">In this case, the application is watching for the appearance of new files in the default storage attached to the HDInsight cluster.</span></span>

    val lines = ssc.textFileStream("/uploads/2017/01/")

#### <a name="apply-transformations"></a><span data-ttu-id="ad946-148">Apply transformations</span><span class="sxs-lookup"><span data-stu-id="ad946-148">Apply transformations</span></span>

<span data-ttu-id="ad946-149">You implement the processing by applying transformations on the DStream.</span><span class="sxs-lookup"><span data-stu-id="ad946-149">You implement the processing by applying transformations on the DStream.</span></span> <span data-ttu-id="ad946-150">This application receives one line of text at a time from the file, splits each line into words, and then uses a map-reduce pattern to count the number of times each word appears.</span><span class="sxs-lookup"><span data-stu-id="ad946-150">This application receives one line of text at a time from the file, splits each line into words, and then uses a map-reduce pattern to count the number of times each word appears.</span></span>

    val words = lines.flatMap(_.split(" "))
    val pairs = words.map(word => (word, 1))
    val wordCounts = pairs.reduceByKey(_ + _)

#### <a name="output-results"></a><span data-ttu-id="ad946-151">Output results</span><span class="sxs-lookup"><span data-stu-id="ad946-151">Output results</span></span>

<span data-ttu-id="ad946-152">Push the transformation results out to the destination systems by applying output operations.</span><span class="sxs-lookup"><span data-stu-id="ad946-152">Push the transformation results out to the destination systems by applying output operations.</span></span> <span data-ttu-id="ad946-153">In this case,  the result of each run through the computation is printed in the console output.</span><span class="sxs-lookup"><span data-stu-id="ad946-153">In this case,  the result of each run through the computation is printed in the console output.</span></span>

    wordCounts.print()

### <a name="run-the-application"></a><span data-ttu-id="ad946-154">Run the application</span><span class="sxs-lookup"><span data-stu-id="ad946-154">Run the application</span></span>

<span data-ttu-id="ad946-155">Start the streaming application and run until a termination signal is received.</span><span class="sxs-lookup"><span data-stu-id="ad946-155">Start the streaming application and run until a termination signal is received.</span></span>

    ssc.start()            
    ssc.awaitTermination()

<span data-ttu-id="ad946-156">For details on the Spark Stream API, along with the event sources, transformations, and output operations it supports, see [Spark Streaming Programming Guide](https://people.apache.org/~pwendell/spark-releases/latest/streaming-programming-guide.html).</span><span class="sxs-lookup"><span data-stu-id="ad946-156">For details on the Spark Stream API, along with the event sources, transformations, and output operations it supports, see [Spark Streaming Programming Guide](https://people.apache.org/~pwendell/spark-releases/latest/streaming-programming-guide.html).</span></span>

<span data-ttu-id="ad946-157">The following sample application is self-contained, so you can run it inside a [Jupyter Notebook](apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="ad946-157">The following sample application is self-contained, so you can run it inside a [Jupyter Notebook](apache-spark-jupyter-notebook-kernels.md).</span></span> <span data-ttu-id="ad946-158">This example creates a mock data source in the class DummySource that outputs the value of a counter and the current time in milliseconds every five seconds.</span><span class="sxs-lookup"><span data-stu-id="ad946-158">This example creates a mock data source in the class DummySource that outputs the value of a counter and the current time in milliseconds every five seconds.</span></span> <span data-ttu-id="ad946-159">A  new StreamingContext object  has a batch interval of 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="ad946-159">A  new StreamingContext object  has a batch interval of 30 seconds.</span></span> <span data-ttu-id="ad946-160">Every time a batch is created, the streaming application examines the RDD produced, converts the RDD to a Spark DataFrame, and creates a temporary table over the DataFrame.</span><span class="sxs-lookup"><span data-stu-id="ad946-160">Every time a batch is created, the streaming application examines the RDD produced, converts the RDD to a Spark DataFrame, and creates a temporary table over the DataFrame.</span></span>

    class DummySource extends org.apache.spark.streaming.receiver.Receiver[(Int, Long)](org.apache.spark.storage.StorageLevel.MEMORY_AND_DISK_2) {

        /** Start the thread that simulates receiving data */
        def onStart() {
            new Thread("Dummy Source") { override def run() { receive() } }.start()
        }

        def onStop() {  }

        /** Periodically generate a random number from 0 to 9, and the timestamp */
        private def receive() {
            var counter = 0  
            while(!isStopped()) {
                store(Iterator((counter, System.currentTimeMillis)))
                counter += 1
                Thread.sleep(5000)
            }
        }
    }

    // A batch is created every 30 seconds
    val ssc = new org.apache.spark.streaming.StreamingContext(spark.sparkContext, org.apache.spark.streaming.Seconds(30))

    // Set the active SQLContext so that we can access it statically within the foreachRDD
    org.apache.spark.sql.SQLContext.setActive(spark.sqlContext)

    // Create the stream
    val stream = ssc.receiverStream(new DummySource())

    // Process RDDs in the batch
    stream.foreachRDD { rdd =>

        // Access the SQLContext and create a table called demo_numbers we can query
        val _sqlContext = org.apache.spark.sql.SQLContext.getOrCreate(rdd.sparkContext)
        _sqlContext.createDataFrame(rdd).toDF("value", "time")
            .registerTempTable("demo_numbers")
    } 

    // Start the stream processing
    ssc.start()

<span data-ttu-id="ad946-161">You can then query the DataFrame periodically to see the current set of values present in the batch, for example using this SQL query:</span><span class="sxs-lookup"><span data-stu-id="ad946-161">You can then query the DataFrame periodically to see the current set of values present in the batch, for example using this SQL query:</span></span>

    %%sql
    SELECT * FROM demo_numbers

<span data-ttu-id="ad946-162">The resulting output looks like the following:</span><span class="sxs-lookup"><span data-stu-id="ad946-162">The resulting output looks like the following:</span></span>

| <span data-ttu-id="ad946-163">value</span><span class="sxs-lookup"><span data-stu-id="ad946-163">value</span></span> | <span data-ttu-id="ad946-164">time</span><span class="sxs-lookup"><span data-stu-id="ad946-164">time</span></span> |
| --- | --- |
|<span data-ttu-id="ad946-165">10</span><span class="sxs-lookup"><span data-stu-id="ad946-165">10</span></span> | <span data-ttu-id="ad946-166">1497314465256</span><span class="sxs-lookup"><span data-stu-id="ad946-166">1497314465256</span></span> |
|<span data-ttu-id="ad946-167">11</span><span class="sxs-lookup"><span data-stu-id="ad946-167">11</span></span> | <span data-ttu-id="ad946-168">1497314470272</span><span class="sxs-lookup"><span data-stu-id="ad946-168">1497314470272</span></span> |
|<span data-ttu-id="ad946-169">12</span><span class="sxs-lookup"><span data-stu-id="ad946-169">12</span></span> | <span data-ttu-id="ad946-170">1497314475289</span><span class="sxs-lookup"><span data-stu-id="ad946-170">1497314475289</span></span> |
|<span data-ttu-id="ad946-171">13</span><span class="sxs-lookup"><span data-stu-id="ad946-171">13</span></span> | <span data-ttu-id="ad946-172">1497314480310</span><span class="sxs-lookup"><span data-stu-id="ad946-172">1497314480310</span></span> |
|<span data-ttu-id="ad946-173">14</span><span class="sxs-lookup"><span data-stu-id="ad946-173">14</span></span> | <span data-ttu-id="ad946-174">1497314485327</span><span class="sxs-lookup"><span data-stu-id="ad946-174">1497314485327</span></span> |
|<span data-ttu-id="ad946-175">15</span><span class="sxs-lookup"><span data-stu-id="ad946-175">15</span></span> | <span data-ttu-id="ad946-176">1497314490346</span><span class="sxs-lookup"><span data-stu-id="ad946-176">1497314490346</span></span> |

<span data-ttu-id="ad946-177">There are six values, since the DummySource creates a value every 5 seconds and the application emits a batch every 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="ad946-177">There are six values, since the DummySource creates a value every 5 seconds and the application emits a batch every 30 seconds.</span></span>

## <a name="sliding-windows"></a><span data-ttu-id="ad946-178">Sliding windows</span><span class="sxs-lookup"><span data-stu-id="ad946-178">Sliding windows</span></span>

<span data-ttu-id="ad946-179">To perform aggregate calculations on your DStream over some time period, for example to get an average temperature over the last two seconds, you can use the *sliding window* operations included with Spark Streaming.</span><span class="sxs-lookup"><span data-stu-id="ad946-179">To perform aggregate calculations on your DStream over some time period, for example to get an average temperature over the last two seconds, you can use the *sliding window* operations included with Spark Streaming.</span></span> <span data-ttu-id="ad946-180">A sliding window has a duration (the window length) and the interval during which the window's contents are evaluated (the slide interval).</span><span class="sxs-lookup"><span data-stu-id="ad946-180">A sliding window has a duration (the window length) and the interval during which the window's contents are evaluated (the slide interval).</span></span>

<span data-ttu-id="ad946-181">Sliding windows can overlap, for example, you can define a window with a length of two seconds, that slides every one second.</span><span class="sxs-lookup"><span data-stu-id="ad946-181">Sliding windows can overlap, for example, you can define a window with a length of two seconds, that slides every one second.</span></span> <span data-ttu-id="ad946-182">This means every time you perform an aggregation calculation, the window will include data from the last one second of the previous window as well as any new data in the next one second.</span><span class="sxs-lookup"><span data-stu-id="ad946-182">This means every time you perform an aggregation calculation, the window will include data from the last one second of the previous window as well as any new data in the next one second.</span></span>

![Example Initial Window with Temperature Events](./media/apache-spark-streaming-overview/hdinsight-spark-streaming-window-01.png)

![Example Window with Temperature Events After Sliding](./media/apache-spark-streaming-overview/hdinsight-spark-streaming-window-02.png)

<span data-ttu-id="ad946-185">The following example  updates the code that uses the DummySource, to collect the batches into a window with a one-minute duration and a one-minute slide.</span><span class="sxs-lookup"><span data-stu-id="ad946-185">The following example  updates the code that uses the DummySource, to collect the batches into a window with a one-minute duration and a one-minute slide.</span></span>

    // A batch is created every 30 seconds
    val ssc = new org.apache.spark.streaming.StreamingContext(spark.sparkContext, org.apache.spark.streaming.Seconds(30))

    // Set the active SQLContext so that we can access it statically within the foreachRDD
    org.apache.spark.sql.SQLContext.setActive(spark.sqlContext)

    // Create the stream
    val stream = ssc.receiverStream(new DummySource())

    // Process batches in 1 minute windows
    stream.window(org.apache.spark.streaming.Minutes(1)).foreachRDD { rdd =>

        // Access the SQLContext and create a table called demo_numbers we can query
        val _sqlContext = org.apache.spark.sql.SQLContext.getOrCreate(rdd.sparkContext)
        _sqlContext.createDataFrame(rdd).toDF("value", "time")
        .registerTempTable("demo_numbers")
    } 

    // Start the stream processing
    ssc.start()

<span data-ttu-id="ad946-186">After the first minute, there are 12 entries - six entries from each of the two batches collected in the window.</span><span class="sxs-lookup"><span data-stu-id="ad946-186">After the first minute, there are 12 entries - six entries from each of the two batches collected in the window.</span></span>

| <span data-ttu-id="ad946-187">value</span><span class="sxs-lookup"><span data-stu-id="ad946-187">value</span></span> | <span data-ttu-id="ad946-188">time</span><span class="sxs-lookup"><span data-stu-id="ad946-188">time</span></span> |
| --- | --- |
| <span data-ttu-id="ad946-189">1</span><span class="sxs-lookup"><span data-stu-id="ad946-189">1</span></span> | <span data-ttu-id="ad946-190">1497316294139</span><span class="sxs-lookup"><span data-stu-id="ad946-190">1497316294139</span></span> |
| <span data-ttu-id="ad946-191">2</span><span class="sxs-lookup"><span data-stu-id="ad946-191">2</span></span> | <span data-ttu-id="ad946-192">1497316299158</span><span class="sxs-lookup"><span data-stu-id="ad946-192">1497316299158</span></span>
| <span data-ttu-id="ad946-193">3</span><span class="sxs-lookup"><span data-stu-id="ad946-193">3</span></span> | <span data-ttu-id="ad946-194">1497316304178</span><span class="sxs-lookup"><span data-stu-id="ad946-194">1497316304178</span></span>
| <span data-ttu-id="ad946-195">4</span><span class="sxs-lookup"><span data-stu-id="ad946-195">4</span></span> | <span data-ttu-id="ad946-196">1497316309204</span><span class="sxs-lookup"><span data-stu-id="ad946-196">1497316309204</span></span>
| <span data-ttu-id="ad946-197">5</span><span class="sxs-lookup"><span data-stu-id="ad946-197">5</span></span> | <span data-ttu-id="ad946-198">1497316314224</span><span class="sxs-lookup"><span data-stu-id="ad946-198">1497316314224</span></span>
| <span data-ttu-id="ad946-199">6</span><span class="sxs-lookup"><span data-stu-id="ad946-199">6</span></span> | <span data-ttu-id="ad946-200">1497316319243</span><span class="sxs-lookup"><span data-stu-id="ad946-200">1497316319243</span></span>
| <span data-ttu-id="ad946-201">7</span><span class="sxs-lookup"><span data-stu-id="ad946-201">7</span></span> | <span data-ttu-id="ad946-202">1497316324260</span><span class="sxs-lookup"><span data-stu-id="ad946-202">1497316324260</span></span>
| <span data-ttu-id="ad946-203">8</span><span class="sxs-lookup"><span data-stu-id="ad946-203">8</span></span> | <span data-ttu-id="ad946-204">1497316329278</span><span class="sxs-lookup"><span data-stu-id="ad946-204">1497316329278</span></span>
| <span data-ttu-id="ad946-205">9</span><span class="sxs-lookup"><span data-stu-id="ad946-205">9</span></span> | <span data-ttu-id="ad946-206">1497316334293</span><span class="sxs-lookup"><span data-stu-id="ad946-206">1497316334293</span></span>
| <span data-ttu-id="ad946-207">10</span><span class="sxs-lookup"><span data-stu-id="ad946-207">10</span></span> | <span data-ttu-id="ad946-208">1497316339314</span><span class="sxs-lookup"><span data-stu-id="ad946-208">1497316339314</span></span>
| <span data-ttu-id="ad946-209">11</span><span class="sxs-lookup"><span data-stu-id="ad946-209">11</span></span> | <span data-ttu-id="ad946-210">1497316344339</span><span class="sxs-lookup"><span data-stu-id="ad946-210">1497316344339</span></span>
| <span data-ttu-id="ad946-211">12</span><span class="sxs-lookup"><span data-stu-id="ad946-211">12</span></span> | <span data-ttu-id="ad946-212">1497316349361</span><span class="sxs-lookup"><span data-stu-id="ad946-212">1497316349361</span></span>

<span data-ttu-id="ad946-213">The sliding window functions available in the Spark Streaming API include window, countByWindow, reduceByWindow, and countByValueAndWindow.</span><span class="sxs-lookup"><span data-stu-id="ad946-213">The sliding window functions available in the Spark Streaming API include window, countByWindow, reduceByWindow, and countByValueAndWindow.</span></span> <span data-ttu-id="ad946-214">For details on these functions, see [Transformations on DStreams](https://people.apache.org/~pwendell/spark-releases/latest/streaming-programming-guide.html#transformations-on-dstreams).</span><span class="sxs-lookup"><span data-stu-id="ad946-214">For details on these functions, see [Transformations on DStreams](https://people.apache.org/~pwendell/spark-releases/latest/streaming-programming-guide.html#transformations-on-dstreams).</span></span>

## <a name="checkpointing"></a><span data-ttu-id="ad946-215">Checkpointing</span><span class="sxs-lookup"><span data-stu-id="ad946-215">Checkpointing</span></span>

<span data-ttu-id="ad946-216">To deliver resiliency and fault tolerance, Spark Streaming relies on checkpointing to ensure that stream processing can continue uninterrupted, even in the face of node failures.</span><span class="sxs-lookup"><span data-stu-id="ad946-216">To deliver resiliency and fault tolerance, Spark Streaming relies on checkpointing to ensure that stream processing can continue uninterrupted, even in the face of node failures.</span></span> <span data-ttu-id="ad946-217">In HDInsight, Spark creates checkpoints to durable storage (Azure Storage or Data Lake Store).</span><span class="sxs-lookup"><span data-stu-id="ad946-217">In HDInsight, Spark creates checkpoints to durable storage (Azure Storage or Data Lake Store).</span></span> <span data-ttu-id="ad946-218">These checkpoints store the metadata about the streaming application such as the configuration, the operations defined by the application, and any batches that were queued but not yet processed.</span><span class="sxs-lookup"><span data-stu-id="ad946-218">These checkpoints store the metadata about the streaming application such as the configuration, the operations defined by the application, and any batches that were queued but not yet processed.</span></span> <span data-ttu-id="ad946-219">In some cases, the checkpoints will also include saving the data in the RDDs to more quickly rebuild the state of the data from what is present in the RDDs managed by Spark.</span><span class="sxs-lookup"><span data-stu-id="ad946-219">In some cases, the checkpoints will also include saving the data in the RDDs to more quickly rebuild the state of the data from what is present in the RDDs managed by Spark.</span></span>

## <a name="deploying-spark-streaming-applications"></a><span data-ttu-id="ad946-220">Deploying Spark Streaming applications</span><span class="sxs-lookup"><span data-stu-id="ad946-220">Deploying Spark Streaming applications</span></span>

<span data-ttu-id="ad946-221">You typically build a Spark Streaming application locally into a JAR file and then deploy it to Spark on HDInsight by copying the JAR file  to the default storage attached to your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ad946-221">You typically build a Spark Streaming application locally into a JAR file and then deploy it to Spark on HDInsight by copying the JAR file  to the default storage attached to your HDInsight cluster.</span></span> <span data-ttu-id="ad946-222">You can start your application  with the LIVY REST APIs available from your cluster using  a POST operation.</span><span class="sxs-lookup"><span data-stu-id="ad946-222">You can start your application  with the LIVY REST APIs available from your cluster using  a POST operation.</span></span> <span data-ttu-id="ad946-223">The body of the POST includes a JSON document that provides the path to your JAR, the name of the class whose main method defines and runs the streaming application, and optionally the resource requirements of the job (such as the number of executors, memory and cores), and any configuration settings your application code requires.</span><span class="sxs-lookup"><span data-stu-id="ad946-223">The body of the POST includes a JSON document that provides the path to your JAR, the name of the class whose main method defines and runs the streaming application, and optionally the resource requirements of the job (such as the number of executors, memory and cores), and any configuration settings your application code requires.</span></span>

![Deploying a Spark Streaming application](./media/apache-spark-streaming-overview/hdinsight-spark-streaming-livy.png)

<span data-ttu-id="ad946-225">The status of all applications can also be checked with a GET request against a LIVY endpoint.</span><span class="sxs-lookup"><span data-stu-id="ad946-225">The status of all applications can also be checked with a GET request against a LIVY endpoint.</span></span> <span data-ttu-id="ad946-226">Finally, you can terminate a running application by issuing a DELETE request against the LIVY endpoint.</span><span class="sxs-lookup"><span data-stu-id="ad946-226">Finally, you can terminate a running application by issuing a DELETE request against the LIVY endpoint.</span></span> <span data-ttu-id="ad946-227">For details on the LIVY API, see [Remote jobs with LIVY](apache-spark-livy-rest-interface.md)</span><span class="sxs-lookup"><span data-stu-id="ad946-227">For details on the LIVY API, see [Remote jobs with LIVY](apache-spark-livy-rest-interface.md)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ad946-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad946-228">Next steps</span></span>

* [<span data-ttu-id="ad946-229">Create an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ad946-229">Create an Apache Spark cluster in HDInsight</span></span>](../hdinsight-hadoop-create-linux-clusters-portal.md)
* [<span data-ttu-id="ad946-230">Spark Streaming Programming Guide</span><span class="sxs-lookup"><span data-stu-id="ad946-230">Spark Streaming Programming Guide</span></span>](https://people.apache.org/~pwendell/spark-releases/latest/streaming-programming-guide.html)
* [<span data-ttu-id="ad946-231">Launch Spark jobs remotely with LIVY</span><span class="sxs-lookup"><span data-stu-id="ad946-231">Launch Spark jobs remotely with LIVY</span></span>](apache-spark-livy-rest-interface.md)
