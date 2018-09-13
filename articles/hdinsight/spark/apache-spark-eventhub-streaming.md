---
title: 'Tutorial: Process data from Azure Event Hubs with Apache Spark in Azure HDInsight '
description: Connect Apache Spark in Azure HDInsight to Azure Event Hubs and process the streaming data.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive,mvc
ms.topic: conceptual
ms.date: 06/14/2018
ms.openlocfilehash: 9cdb5ae31e2743b5ebe877ddd8d6680423e3d9b2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857064"
---
# <a name="tutorial-process-tweets-using-azure-event-hubs-and-spark-in-hdinsight"></a><span data-ttu-id="b9539-103">Tutorial: Process tweets using Azure Event Hubs and Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b9539-103">Tutorial: Process tweets using Azure Event Hubs and Spark in HDInsight</span></span>

<span data-ttu-id="b9539-104">In this tutorial, you Learn how to create an Apache Spark streaming application to send tweets to an Azure event hub, and create another application to read the tweets from the event hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-104">In this tutorial, you Learn how to create an Apache Spark streaming application to send tweets to an Azure event hub, and create another application to read the tweets from the event hub.</span></span> <span data-ttu-id="b9539-105">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="b9539-105">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="b9539-106">HDInsight brings the same streaming features to a Spark cluster on Azure.</span><span class="sxs-lookup"><span data-stu-id="b9539-106">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>

<span data-ttu-id="b9539-107">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="b9539-107">In this tutorial, you learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="b9539-108">Send messages to Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="b9539-108">Send messages to Azure Event Hub</span></span>
> * <span data-ttu-id="b9539-109">Read messages from Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="b9539-109">Read messages from Azure Event Hub</span></span>

<span data-ttu-id="b9539-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b9539-110">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b9539-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b9539-111">Prerequisites</span></span>

* <span data-ttu-id="b9539-112">**Complete the article [Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight](./apache-spark-load-data-run-query.md)**.</span><span class="sxs-lookup"><span data-stu-id="b9539-112">**Complete the article [Tutorial: Load data and run queries on an Apache Spark cluster in Azure HDInsight](./apache-spark-load-data-run-query.md)**.</span></span>

## <a name="create-a-twitter-application"></a><span data-ttu-id="b9539-113">Create a Twitter application</span><span class="sxs-lookup"><span data-stu-id="b9539-113">Create a Twitter application</span></span>

<span data-ttu-id="b9539-114">To receive a stream of tweets, you create an application in Twitter.</span><span class="sxs-lookup"><span data-stu-id="b9539-114">To receive a stream of tweets, you create an application in Twitter.</span></span> <span data-ttu-id="b9539-115">Follow the instructions create a Twitter application and write down the values that you need to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9539-115">Follow the instructions create a Twitter application and write down the values that you need to complete this tutorial.</span></span>

1. <span data-ttu-id="b9539-116">Browse to [Twitter Application Management](https://apps.twitter.com/).</span><span class="sxs-lookup"><span data-stu-id="b9539-116">Browse to [Twitter Application Management](https://apps.twitter.com/).</span></span>
2. <span data-ttu-id="b9539-117">Select **Create New App**.</span><span class="sxs-lookup"><span data-stu-id="b9539-117">Select **Create New App**.</span></span>
3. <span data-ttu-id="b9539-118">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="b9539-118">Provide the following values:</span></span>

    - <span data-ttu-id="b9539-119">Name: provide the application name.</span><span class="sxs-lookup"><span data-stu-id="b9539-119">Name: provide the application name.</span></span> <span data-ttu-id="b9539-120">The value used for this tutorial is **HDISparkStreamApp0423**.</span><span class="sxs-lookup"><span data-stu-id="b9539-120">The value used for this tutorial is **HDISparkStreamApp0423**.</span></span> <span data-ttu-id="b9539-121">This name has to be a unique name.</span><span class="sxs-lookup"><span data-stu-id="b9539-121">This name has to be a unique name.</span></span>
    - <span data-ttu-id="b9539-122">Description: provide a short description of the application.</span><span class="sxs-lookup"><span data-stu-id="b9539-122">Description: provide a short description of the application.</span></span> <span data-ttu-id="b9539-123">The value used for this tutorial is **A simple HDInsight Spark streaming application**.</span><span class="sxs-lookup"><span data-stu-id="b9539-123">The value used for this tutorial is **A simple HDInsight Spark streaming application**.</span></span>
    - <span data-ttu-id="b9539-124">Website: provide the application's website.</span><span class="sxs-lookup"><span data-stu-id="b9539-124">Website: provide the application's website.</span></span> <span data-ttu-id="b9539-125">It doesn't have to be a valid website.</span><span class="sxs-lookup"><span data-stu-id="b9539-125">It doesn't have to be a valid website.</span></span>  <span data-ttu-id="b9539-126">The value used for this tutorial is **http://www.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="b9539-126">The value used for this tutorial is **http://www.contoso.com**.</span></span>
    - <span data-ttu-id="b9539-127">Callback URL: you can leave it blank.</span><span class="sxs-lookup"><span data-stu-id="b9539-127">Callback URL: you can leave it blank.</span></span>

4. <span data-ttu-id="b9539-128">Select **Yes, I have read and agree to the Twitter Developer Agreement**, and then Select **Create your Twitter application**.</span><span class="sxs-lookup"><span data-stu-id="b9539-128">Select **Yes, I have read and agree to the Twitter Developer Agreement**, and then Select **Create your Twitter application**.</span></span>
5. <span data-ttu-id="b9539-129">Select the **Keys and Access Tokens** tab.</span><span class="sxs-lookup"><span data-stu-id="b9539-129">Select the **Keys and Access Tokens** tab.</span></span>
6. <span data-ttu-id="b9539-130">Select **Create my access token** at the end of the page.</span><span class="sxs-lookup"><span data-stu-id="b9539-130">Select **Create my access token** at the end of the page.</span></span>
7. <span data-ttu-id="b9539-131">Write down the following values from the page.</span><span class="sxs-lookup"><span data-stu-id="b9539-131">Write down the following values from the page.</span></span>  <span data-ttu-id="b9539-132">You need these values later in the tutorial:</span><span class="sxs-lookup"><span data-stu-id="b9539-132">You need these values later in the tutorial:</span></span>

    - <span data-ttu-id="b9539-133">**Consumer Key (API Key)**</span><span class="sxs-lookup"><span data-stu-id="b9539-133">**Consumer Key (API Key)**</span></span>    
    - <span data-ttu-id="b9539-134">**Consumer Secret (API Secret)**</span><span class="sxs-lookup"><span data-stu-id="b9539-134">**Consumer Secret (API Secret)**</span></span>  
    - <span data-ttu-id="b9539-135">**Access Token**</span><span class="sxs-lookup"><span data-stu-id="b9539-135">**Access Token**</span></span>
    - <span data-ttu-id="b9539-136">**Access Token Secret**</span><span class="sxs-lookup"><span data-stu-id="b9539-136">**Access Token Secret**</span></span>   

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="b9539-137">Create an Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="b9539-137">Create an Azure Event Hub</span></span>

<span data-ttu-id="b9539-138">You use this event hub to store tweets.</span><span class="sxs-lookup"><span data-stu-id="b9539-138">You use this event hub to store tweets.</span></span>

1. <span data-ttu-id="b9539-139">Sign in to the [Azure Portal](https://ms.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b9539-139">Sign in to the [Azure Portal](https://ms.portal.azure.com).</span></span>
2. <span data-ttu-id="b9539-140">Select **Create a resource** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="b9539-140">Select **Create a resource** at the top left of the screen.</span></span>
3. <span data-ttu-id="b9539-141">Select **Internet of Things**, then select **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="b9539-141">Select **Internet of Things**, then select **Event Hubs**.</span></span>

    <span data-ttu-id="b9539-142">![Create event hub for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="b9539-142">![Create event hub for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>
4. <span data-ttu-id="b9539-143">Enter the following values for the new event hub namespace:</span><span class="sxs-lookup"><span data-stu-id="b9539-143">Enter the following values for the new event hub namespace:</span></span>

    - <span data-ttu-id="b9539-144">**Name**: Enter a name for the event hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-144">**Name**: Enter a name for the event hub.</span></span>  <span data-ttu-id="b9539-145">The value used for this tutorial is **myeventhubns20180403**.</span><span class="sxs-lookup"><span data-stu-id="b9539-145">The value used for this tutorial is **myeventhubns20180403**.</span></span>
    - <span data-ttu-id="b9539-146">**Price tier**: Select **Standard**.</span><span class="sxs-lookup"><span data-stu-id="b9539-146">**Price tier**: Select **Standard**.</span></span>
    - <span data-ttu-id="b9539-147">**Resource group**: You have the option to create a new or select the resource group for the Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="b9539-147">**Resource group**: You have the option to create a new or select the resource group for the Spark cluster.</span></span> 
    - <span data-ttu-id="b9539-148">**Location**: Select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span><span class="sxs-lookup"><span data-stu-id="b9539-148">**Location**: Select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>

    <span data-ttu-id="b9539-149">![Provide an event hub name for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="b9539-149">![Provide an event hub name for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>
5. <span data-ttu-id="b9539-150">Select **Create** to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="b9539-150">Select **Create** to create the namespace.</span></span>

6. <span data-ttu-id="b9539-151">Open the event hub namespace using the following instructions:</span><span class="sxs-lookup"><span data-stu-id="b9539-151">Open the event hub namespace using the following instructions:</span></span>

    1. <span data-ttu-id="b9539-152">From the portal, select **All services**.</span><span class="sxs-lookup"><span data-stu-id="b9539-152">From the portal, select **All services**.</span></span>
    2. <span data-ttu-id="b9539-153">In the filter box, enter **event hubs**.</span><span class="sxs-lookup"><span data-stu-id="b9539-153">In the filter box, enter **event hubs**.</span></span>
    3. <span data-ttu-id="b9539-154">Double-click the namespace you created.</span><span class="sxs-lookup"><span data-stu-id="b9539-154">Double-click the namespace you created.</span></span>
    4. <span data-ttu-id="b9539-155">Select **+ Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="b9539-155">Select **+ Event Hub**.</span></span>

6. <span data-ttu-id="b9539-156">In the Event Hubs namespace list, Select the newly created namespace.</span><span class="sxs-lookup"><span data-stu-id="b9539-156">In the Event Hubs namespace list, Select the newly created namespace.</span></span>      
5. <span data-ttu-id="b9539-157">Select **Event Hubs**, and then Select **+ Event Hub** to create a new Event Hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-157">Select **Event Hubs**, and then Select **+ Event Hub** to create a new Event Hub.</span></span>
  

6. <span data-ttu-id="b9539-158">Enter the following values:</span><span class="sxs-lookup"><span data-stu-id="b9539-158">Enter the following values:</span></span>

    - <span data-ttu-id="b9539-159">Name: Give a name for your Event Hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-159">Name: Give a name for your Event Hub.</span></span>
    - <span data-ttu-id="b9539-160">Partition count: 10</span><span class="sxs-lookup"><span data-stu-id="b9539-160">Partition count: 10</span></span>
    - <span data-ttu-id="b9539-161">Message retention: 1.</span><span class="sxs-lookup"><span data-stu-id="b9539-161">Message retention: 1.</span></span> 
   
    <span data-ttu-id="b9539-162">![Provide event hub details for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="b9539-162">![Provide event hub details for Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="b9539-163">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="b9539-163">Select **Create**.</span></span>
8. <span data-ttu-id="b9539-164">Select **Shared access policies** for the namespace (Note it is not the event hub shared access policies), and then Select **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="b9539-164">Select **Shared access policies** for the namespace (Note it is not the event hub shared access policies), and then Select **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="b9539-165">![Set Event Hub policies for the Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="b9539-165">![Set Event Hub policies for the Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="b9539-166">Save the values of **Primary key** and **Connection string-primary key** to use later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="b9539-166">Save the values of **Primary key** and **Connection string-primary key** to use later in the tutorial.</span></span>

     <span data-ttu-id="b9539-167">![View Event Hub policy keys for the Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span><span class="sxs-lookup"><span data-stu-id="b9539-167">![View Event Hub policy keys for the Spark streaming example](./media/apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>


## <a name="send-tweets-to-the-event-hub"></a><span data-ttu-id="b9539-168">Send tweets to the event hub</span><span class="sxs-lookup"><span data-stu-id="b9539-168">Send tweets to the event hub</span></span>

<span data-ttu-id="b9539-169">You need to create a Jupyter notebook, and name it **SendTweetsToEventHub**.</span><span class="sxs-lookup"><span data-stu-id="b9539-169">You need to create a Jupyter notebook, and name it **SendTweetsToEventHub**.</span></span> 

1. <span data-ttu-id="b9539-170">Run the following code to add the external Maven libraries:</span><span class="sxs-lookup"><span data-stu-id="b9539-170">Run the following code to add the external Maven libraries:</span></span>

    ```
    %%configure
    {"conf":{"spark.jars.packages":"com.microsoft.azure:azure-eventhubs-spark_2.11:2.2.0,org.twitter4j:twitter4j-core:4.0.6"}}
    ```

2. <span data-ttu-id="b9539-171">Run the following code to send tweets to your event hub:</span><span class="sxs-lookup"><span data-stu-id="b9539-171">Run the following code to send tweets to your event hub:</span></span>

    ```
    import java.util._
    import scala.collection.JavaConverters._
    import java.util.concurrent._
    
    import org.apache.spark._
    import org.apache.spark.streaming._
    import org.apache.spark.eventhubs.ConnectionStringBuilder

    // Event hub configurations
    // Replace values below with yours        
    val eventHubName = "<Event hub name>"
    val eventHubNSConnStr = "<Event hub namespace connection string>"
    val connStr = ConnectionStringBuilder(eventHubNSConnStr).setEventHubName(eventHubName).build 
    
    import com.microsoft.azure.eventhubs._
    val pool = Executors.newFixedThreadPool(1)
    val eventHubClient = EventHubClient.create(connStr.toString(), pool)
    
    def sendEvent(message: String) = {
          val messageData = EventData.create(message.getBytes("UTF-8"))
          eventHubClient.get().send(messageData)
          println("Sent event: " + message + "\n")
    }
    
    import twitter4j._
    import twitter4j.TwitterFactory
    import twitter4j.Twitter
    import twitter4j.conf.ConfigurationBuilder

    // Twitter application configurations
    // Replace values below with yours   
    val twitterConsumerKey = "<CONSUMER KEY>"
    val twitterConsumerSecret = "<CONSUMER SECRET>"
    val twitterOauthAccessToken = "<ACCESS TOKEN>"
    val twitterOauthTokenSecret = "<TOKEN SECRET>"
    
    val cb = new ConfigurationBuilder()
    cb.setDebugEnabled(true).setOAuthConsumerKey(twitterConsumerKey).setOAuthConsumerSecret(twitterConsumerSecret).setOAuthAccessToken(twitterOauthAccessToken).setOAuthAccessTokenSecret(twitterOauthTokenSecret)
    
    val twitterFactory = new TwitterFactory(cb.build())
    val twitter = twitterFactory.getInstance()

    // Getting tweets with keyword "Azure" and sending them to the Event Hub in realtime!
    
    val query = new Query(" #Azure ")
    query.setCount(100)
    query.lang("en")
    var finished = false
    while (!finished) {
      val result = twitter.search(query)
      val statuses = result.getTweets()
      var lowestStatusId = Long.MaxValue
      for (status <- statuses.asScala) {
        if(!status.isRetweet()){
          sendEvent(status.getText())
        }
        lowestStatusId = Math.min(status.getId(), lowestStatusId)
        Thread.sleep(2000)
      }
      query.setMaxId(lowestStatusId - 1)
    }
    
    // Closing connection to the Event Hub
    eventHubClient.get().close()
    ```

3. <span data-ttu-id="b9539-172">Open the event hub in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="b9539-172">Open the event hub in the Azure portal.</span></span>  <span data-ttu-id="b9539-173">On **Overview**, you shall see some charts showing the messages sent to the event hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-173">On **Overview**, you shall see some charts showing the messages sent to the event hub.</span></span>

## <a name="read-tweets-from-the-event-hub"></a><span data-ttu-id="b9539-174">Read tweets from the event hub</span><span class="sxs-lookup"><span data-stu-id="b9539-174">Read tweets from the event hub</span></span>

<span data-ttu-id="b9539-175">You need to create another Jupyter notebook, and name it **ReadTweetsFromEventHub**.</span><span class="sxs-lookup"><span data-stu-id="b9539-175">You need to create another Jupyter notebook, and name it **ReadTweetsFromEventHub**.</span></span> 

1. <span data-ttu-id="b9539-176">Run the following code to add an external Maven library:</span><span class="sxs-lookup"><span data-stu-id="b9539-176">Run the following code to add an external Maven library:</span></span>

    ```
    %%configure -f
    {"conf":{"spark.jars.packages":"com.microsoft.azure:azure-eventhubs-spark_2.11:2.2.0"}}
    ```
2. <span data-ttu-id="b9539-177">Run the following code to read tweets from your event hub:</span><span class="sxs-lookup"><span data-stu-id="b9539-177">Run the following code to read tweets from your event hub:</span></span>

    ```
    import org.apache.spark.eventhubs._
    // Event hub configurations
    // Replace values below with yours        
    val eventHubName = "<Event hub name>"
    val eventHubNSConnStr = "<Event hub namespace connection string>"
    val connStr = ConnectionStringBuilder(eventHubNSConnStr).setEventHubName(eventHubName).build 
    
    val customEventhubParameters = EventHubsConf(connStr).setMaxEventsPerTrigger(5)
    val incomingStream = spark.readStream.format("eventhubs").options(customEventhubParameters.toMap).load()
    //incomingStream.printSchema    
    
    import org.apache.spark.sql.types._
    import org.apache.spark.sql.functions._
    
    // Event Hub message format is JSON and contains "body" field
    // Body is binary, so you cast it to string to see the actual content of the message
    val messages = incomingStream.withColumn("Offset", $"offset".cast(LongType)).withColumn("Time (readable)", $"enqueuedTime".cast(TimestampType)).withColumn("Timestamp", $"enqueuedTime".cast(LongType)).withColumn("Body", $"body".cast(StringType)).select("Offset", "Time (readable)", "Timestamp", "Body")
    
    messages.printSchema
    
    messages.writeStream.outputMode("append").format("console").option("truncate", false).start().awaitTermination()
    ```

## <a name="clean-up-resources"></a><span data-ttu-id="b9539-178">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b9539-178">Clean up resources</span></span>

<span data-ttu-id="b9539-179">With HDInsight, your data is stored in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="b9539-179">With HDInsight, your data is stored in Azure Storage or Azure Data Lake Store, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="b9539-180">You are also charged for an HDInsight cluster, even when it is not in use.</span><span class="sxs-lookup"><span data-stu-id="b9539-180">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="b9539-181">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span><span class="sxs-lookup"><span data-stu-id="b9539-181">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="b9539-182">If you plan to work on the next tutorial immediately, you might want to keep the cluster.</span><span class="sxs-lookup"><span data-stu-id="b9539-182">If you plan to work on the next tutorial immediately, you might want to keep the cluster.</span></span>

<span data-ttu-id="b9539-183">Open the cluster in the Azure portal, and select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b9539-183">Open the cluster in the Azure portal, and select **Delete**.</span></span>

<span data-ttu-id="b9539-184">![Delete HDInsight cluster](./media/apache-spark-load-data-run-query/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span><span class="sxs-lookup"><span data-stu-id="b9539-184">![Delete HDInsight cluster](./media/apache-spark-load-data-run-query/hdinsight-azure-portal-delete-cluster.png "Delete HDInsight cluster")</span></span>

<span data-ttu-id="b9539-185">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="b9539-185">You can also select the resource group name to open the resource group page, and then select **Delete resource group**.</span></span> <span data-ttu-id="b9539-186">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span><span class="sxs-lookup"><span data-stu-id="b9539-186">By deleting the resource group, you delete both the HDInsight Spark cluster, and the default storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b9539-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="b9539-187">Next steps</span></span>

<span data-ttu-id="b9539-188">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="b9539-188">In this tutorial, you learned how to:</span></span>

* <span data-ttu-id="b9539-189">Read message from an event hub.</span><span class="sxs-lookup"><span data-stu-id="b9539-189">Read message from an event hub.</span></span>
<span data-ttu-id="b9539-190">Advance to the next article to see you can create a machine learning application.</span><span class="sxs-lookup"><span data-stu-id="b9539-190">Advance to the next article to see you can create a machine learning application.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9539-191">Create a machine learning application</span><span class="sxs-lookup"><span data-stu-id="b9539-191">Create a machine learning application</span></span>](./apache-spark-ipython-notebook-machine-learning.md)


