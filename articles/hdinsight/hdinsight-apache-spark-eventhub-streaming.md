---
title: Stream data from Event Hubs with Apache Spark in Azure HDInsight | Microsoft Docs
description: Step-by-step instructions on how to send a data stream to Azure Event Hub and then receive those events in HDInsight Spark using a scala application
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: nitinme
ms.openlocfilehash: 460fe2f2538096e2aa94e591cfcafebab32d845f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549354"
---
# <a name="spark-streaming-process-events-from-azure-event-hubs-with-apache-spark-cluster-on-hdinsight"></a><span data-ttu-id="5ade0-103">Spark Streaming: Process events from Azure Event Hubs with Apache Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-103">Spark Streaming: Process events from Azure Event Hubs with Apache Spark cluster on HDInsight</span></span>

<span data-ttu-id="5ade0-104">In this article, you understand some concepts related to streaming using Apache Spark and then create a streaming solution that involves the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ade0-104">In this article, you understand some concepts related to streaming using Apache Spark and then create a streaming solution that involves the following steps:</span></span>

1. <span data-ttu-id="5ade0-105">You use a standalone application to ingest messages into an Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade0-105">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="5ade0-106">You retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ade0-106">You retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="5ade0-107">You route the data to different outputs such as Azure Storage Blob, Hive table, or a SQL table.</span><span class="sxs-lookup"><span data-stu-id="5ade0-107">You route the data to different outputs such as Azure Storage Blob, Hive table, or a SQL table.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="5ade0-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5ade0-108">Prerequisites</span></span>

* <span data-ttu-id="5ade0-109">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5ade0-109">An Azure subscription.</span></span> <span data-ttu-id="5ade0-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5ade0-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="5ade0-111">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5ade0-111">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5ade0-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-112">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="5ade0-113">Spark streaming concepts</span><span class="sxs-lookup"><span data-stu-id="5ade0-113">Spark streaming concepts</span></span>

<span data-ttu-id="5ade0-114">For an in-depth explanation of how streaming is handled in Apache Spark, see [Apache Spark Streaming Overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="5ade0-114">For an in-depth explanation of how streaming is handled in Apache Spark, see [Apache Spark Streaming Overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="5ade0-115">HDInsight brings the same streaming functions to a Spark cluster on Azure.</span><span class="sxs-lookup"><span data-stu-id="5ade0-115">HDInsight brings the same streaming functions to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="5ade0-116">What does this solution do?</span><span class="sxs-lookup"><span data-stu-id="5ade0-116">What does this solution do?</span></span>

<span data-ttu-id="5ade0-117">In this article, to create a streaming solution, you do the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ade0-117">In this article, to create a streaming solution, you do the following steps:</span></span>

1. <span data-ttu-id="5ade0-118">Create an Azure Event Hub that will receive a stream of events.</span><span class="sxs-lookup"><span data-stu-id="5ade0-118">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="5ade0-119">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade0-119">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="5ade0-120">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="5ade0-120">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="5ade0-121">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and pushes it out to different locations (Azure Blob, Hive table, and SQL database table).</span><span class="sxs-lookup"><span data-stu-id="5ade0-121">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and pushes it out to different locations (Azure Blob, Hive table, and SQL database table).</span></span> 

## <a name="create-azure-event-hub"></a><span data-ttu-id="5ade0-122">Create Azure Event Hub</span><span class="sxs-lookup"><span data-stu-id="5ade0-122">Create Azure Event Hub</span></span>

1. <span data-ttu-id="5ade0-123">Log on to the [Azure Portal](https://manage.windowsazure.com), and click **New** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="5ade0-123">Log on to the [Azure Portal](https://manage.windowsazure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="5ade0-124">Click **Internet of Things**, then click **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-124">Click **Internet of Things**, then click **Event Hubs**.</span></span>
   
    ![Create event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub9.png)

3. <span data-ttu-id="5ade0-126">In the **Create namespace** blade, enter a namespace name.</span><span class="sxs-lookup"><span data-stu-id="5ade0-126">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="5ade0-127">choose the pricing tier (Basic or Standard).</span><span class="sxs-lookup"><span data-stu-id="5ade0-127">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="5ade0-128">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span><span class="sxs-lookup"><span data-stu-id="5ade0-128">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="5ade0-129">Click **Create** to create the namespace.</span><span class="sxs-lookup"><span data-stu-id="5ade0-129">Click **Create** to create the namespace.</span></span>
   
    ![Create event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub1.png)

    > [!NOTE]
    > <span data-ttu-id="5ade0-131">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span><span class="sxs-lookup"><span data-stu-id="5ade0-131">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    > 
    > 

4. <span data-ttu-id="5ade0-132">In the Event Hubs namespace list, click the newly-created namespace.</span><span class="sxs-lookup"><span data-stu-id="5ade0-132">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      
   
    
5. <span data-ttu-id="5ade0-133">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade0-133">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    ![Create event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub3.png)

6. <span data-ttu-id="5ade0-135">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span><span class="sxs-lookup"><span data-stu-id="5ade0-135">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="5ade0-136">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-136">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    ![Create event hub](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub5.png)

7. <span data-ttu-id="5ade0-138">The newly created Event Hub is listed in the Event Hub blade.</span><span class="sxs-lookup"><span data-stu-id="5ade0-138">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub6.png)

8. <span data-ttu-id="5ade0-139">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-139">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub7.png)

9. <span data-ttu-id="5ade0-140">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="5ade0-140">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="5ade0-141">Save these to use later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="5ade0-141">Save these to use later in the tutorial.</span></span>
    
     ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-event-hub8.png)

## <a name="send-messages-to-an-azure-event-hub-using-a-scala-application"></a><span data-ttu-id="5ade0-142">Send messages to an Azure Event Hub using a Scala application</span><span class="sxs-lookup"><span data-stu-id="5ade0-142">Send messages to an Azure Event Hub using a Scala application</span></span>

<span data-ttu-id="5ade0-143">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5ade0-143">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created in the previous step.</span></span> <span data-ttu-id="5ade0-144">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="5ade0-144">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="5ade0-145">The steps here assume that you have already forked this GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="5ade0-145">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="5ade0-146">Make sure you have the following installed on the computer where you are running this application.</span><span class="sxs-lookup"><span data-stu-id="5ade0-146">Make sure you have the following installed on the computer where you are running this application.</span></span>

    * <span data-ttu-id="5ade0-147">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="5ade0-147">Oracle Java Development kit.</span></span> <span data-ttu-id="5ade0-148">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="5ade0-148">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="5ade0-149">A Java IDE.</span><span class="sxs-lookup"><span data-stu-id="5ade0-149">A Java IDE.</span></span> <span data-ttu-id="5ade0-150">This article uses IntelliJ IDEA 15.0.1.</span><span class="sxs-lookup"><span data-stu-id="5ade0-150">This article uses IntelliJ IDEA 15.0.1.</span></span> <span data-ttu-id="5ade0-151">You can install it from [here](https://www.jetbrains.com/idea/download/).</span><span class="sxs-lookup"><span data-stu-id="5ade0-151">You can install it from [here](https://www.jetbrains.com/idea/download/).</span></span>


2. <span data-ttu-id="5ade0-152">Open the application, **EventhubsSampleEventProducer**, in IntelliJ IDEA.</span><span class="sxs-lookup"><span data-stu-id="5ade0-152">Open the application, **EventhubsSampleEventProducer**, in IntelliJ IDEA.</span></span>

3. <span data-ttu-id="5ade0-153">Build the project.</span><span class="sxs-lookup"><span data-stu-id="5ade0-153">Build the project.</span></span> <span data-ttu-id="5ade0-154">From the **Build** menu, click **Make Project**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-154">From the **Build** menu, click **Make Project**.</span></span> <span data-ttu-id="5ade0-155">Depending on your IntelliJ IDEA configuration, the output jar is created under **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-155">Depending on your IntelliJ IDEA configuration, the output jar is created under **\classes\artifacts**.</span></span>

    > [!TIP]
    > <span data-ttu-id="5ade0-156">You can also use an option available in IntelliJ IDEA to directly create the project from a GitHub repository.</span><span class="sxs-lookup"><span data-stu-id="5ade0-156">You can also use an option available in IntelliJ IDEA to directly create the project from a GitHub repository.</span></span> <span data-ttu-id="5ade0-157">To understand how to use that approach, use the instructions in the next section for guidance.</span><span class="sxs-lookup"><span data-stu-id="5ade0-157">To understand how to use that approach, use the instructions in the next section for guidance.</span></span> <span data-ttu-id="5ade0-158">Note that a lot of steps that are described in the next section will not be applicable for the Scala application that you create in this step.</span><span class="sxs-lookup"><span data-stu-id="5ade0-158">Note that a lot of steps that are described in the next section will not be applicable for the Scala application that you create in this step.</span></span> <span data-ttu-id="5ade0-159">For example:</span><span class="sxs-lookup"><span data-stu-id="5ade0-159">For example:</span></span>
    > 
    > * <span data-ttu-id="5ade0-160">You do not have to update the POM to include the Spark version.</span><span class="sxs-lookup"><span data-stu-id="5ade0-160">You do not have to update the POM to include the Spark version.</span></span> <span data-ttu-id="5ade0-161">That's because there is no dependency on Spark for creating this application</span><span class="sxs-lookup"><span data-stu-id="5ade0-161">That's because there is no dependency on Spark for creating this application</span></span>
    > * <span data-ttu-id="5ade0-162">You do not have to add some dependency jars to the project library.</span><span class="sxs-lookup"><span data-stu-id="5ade0-162">You do not have to add some dependency jars to the project library.</span></span> <span data-ttu-id="5ade0-163">Those jars are not required for this project.</span><span class="sxs-lookup"><span data-stu-id="5ade0-163">Those jars are not required for this project.</span></span>
    > 
    > 

## <a name="receive-messages-from-the-event-hub-using-a-streaming-application-running-on-spark-cluster"></a><span data-ttu-id="5ade0-164">Receive messages from the Event Hub using a streaming application running on Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5ade0-164">Receive messages from the Event Hub using a streaming application running on Spark cluster</span></span>

<span data-ttu-id="5ade0-165">A sample Scala application to receive the event and route it to different destinations is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="5ade0-165">A sample Scala application to receive the event and route it to different destinations is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="5ade0-166">Follow the steps below to update the application and create the output jar.</span><span class="sxs-lookup"><span data-stu-id="5ade0-166">Follow the steps below to update the application and create the output jar.</span></span>

1. <span data-ttu-id="5ade0-167">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-167">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    ![Get sources from Git](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/get-source-from-git.png)
2. <span data-ttu-id="5ade0-169">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-169">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    ![Clone from Git](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/clone-from-git.png)
3. <span data-ttu-id="5ade0-171">Follow the prompts till the project is completely cloned.</span><span class="sxs-lookup"><span data-stu-id="5ade0-171">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="5ade0-172">Press **Alt + 1** to open the **Project View**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-172">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="5ade0-173">It should resemble the following.</span><span class="sxs-lookup"><span data-stu-id="5ade0-173">It should resemble the following.</span></span>
   
    ![Project View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/project-view.png)
4. <span data-ttu-id="5ade0-175">Make sure the application code is compiled with Java8.</span><span class="sxs-lookup"><span data-stu-id="5ade0-175">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="5ade0-176">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-176">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    ![Project structure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/java-8-compiler.png)
5. <span data-ttu-id="5ade0-178">Open the **pom.xml** and make sure the Spark version is correct.</span><span class="sxs-lookup"><span data-stu-id="5ade0-178">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="5ade0-179">Under `<properties>` node, look for the following snippet and verify the Spark version.</span><span class="sxs-lookup"><span data-stu-id="5ade0-179">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>
   
        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="5ade0-180">The application requires a dependency jar called **JDBC driver jar**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-180">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="5ade0-181">This is required to write the messages received from Event Hub into an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="5ade0-181">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="5ade0-182">You can download v4.1 or later of this jar file from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ade0-182">You can download v4.1 or later of this jar file from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="5ade0-183">Add reference to this jar in the project library.</span><span class="sxs-lookup"><span data-stu-id="5ade0-183">Add reference to this jar in the project library.</span></span> <span data-ttu-id="5ade0-184">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="5ade0-184">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="5ade0-185">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-185">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="5ade0-186">Click the add icon (![add icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span><span class="sxs-lookup"><span data-stu-id="5ade0-186">Click the add icon (![add icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="5ade0-187">Follow the prompts to add the jar file to the project library.</span><span class="sxs-lookup"><span data-stu-id="5ade0-187">Follow the prompts to add the jar file to the project library.</span></span>
        
         <span data-ttu-id="5ade0-188">![add missing dependencies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span><span class="sxs-lookup"><span data-stu-id="5ade0-188">![add missing dependencies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="5ade0-189">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-189">Click **Apply**.</span></span>
7. <span data-ttu-id="5ade0-190">Create the output jar file.</span><span class="sxs-lookup"><span data-stu-id="5ade0-190">Create the output jar file.</span></span> <span data-ttu-id="5ade0-191">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="5ade0-191">Perform the following steps.</span></span>
   
   1. <span data-ttu-id="5ade0-192">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span><span class="sxs-lookup"><span data-stu-id="5ade0-192">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="5ade0-193">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-193">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-jar-1.png)
   2. <span data-ttu-id="5ade0-195">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-195">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="5ade0-196">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-196">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-jar-2.png)
   4. <span data-ttu-id="5ade0-198">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-198">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="5ade0-199">This creates a single JAR with all dependencies.</span><span class="sxs-lookup"><span data-stu-id="5ade0-199">This creates a single JAR with all dependencies.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/create-jar-3.png)
   5. <span data-ttu-id="5ade0-201">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span><span class="sxs-lookup"><span data-stu-id="5ade0-201">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="5ade0-202">You can select and delete the ones on which the Scala application has no direct dependency.</span><span class="sxs-lookup"><span data-stu-id="5ade0-202">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="5ade0-203">For the application we are creating here, you can remove all but the last one (**microsoft-spark-streaming-examples compile output**).</span><span class="sxs-lookup"><span data-stu-id="5ade0-203">For the application we are creating here, you can remove all but the last one (**microsoft-spark-streaming-examples compile output**).</span></span> <span data-ttu-id="5ade0-204">Select the jars to delete and then click the **Delete** icon (![delete icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="5ade0-204">Select the jars to delete and then click the **Delete** icon (![delete icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/delete-output-jars.png)
      
       <span data-ttu-id="5ade0-206">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span><span class="sxs-lookup"><span data-stu-id="5ade0-206">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="5ade0-207">Click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-207">Click **Apply**.</span></span>
   6. <span data-ttu-id="5ade0-208">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span><span class="sxs-lookup"><span data-stu-id="5ade0-208">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="5ade0-209">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-209">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       ![Extract dependency jar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/extract-dependency-jar.png)  
      
       <span data-ttu-id="5ade0-211">The **Output Layout** tab should now look like this.</span><span class="sxs-lookup"><span data-stu-id="5ade0-211">The **Output Layout** tab should now look like this.</span></span>
      
       ![Final output tab](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/final-output-tab.png)        
      
       <span data-ttu-id="5ade0-213">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-213">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="5ade0-214">From the menu bar, click **Build**, and then click **Make Project**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-214">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="5ade0-215">You can also click **Build Artifacts** to create the jar.</span><span class="sxs-lookup"><span data-stu-id="5ade0-215">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="5ade0-216">The output jar is created under **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-216">The output jar is created under **\classes\artifacts**.</span></span>
      
       ![Create JAR](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-spark-eventhub-streaming/output.png)

## <a name="run-the-applications-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="5ade0-218">Run the applications remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="5ade0-218">Run the applications remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="5ade0-219">We use Livy to run the streaming application remotely on a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="5ade0-219">We use Livy to run the streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="5ade0-220">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-220">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="5ade0-221">Before you can start running the remote jobs to stream events using Spark there are a couple of things you should do:</span><span class="sxs-lookup"><span data-stu-id="5ade0-221">Before you can start running the remote jobs to stream events using Spark there are a couple of things you should do:</span></span>

1. <span data-ttu-id="5ade0-222">Start the local standalone application to generate events and sent to Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5ade0-222">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="5ade0-223">Use the following command to do so:</span><span class="sxs-lookup"><span data-stu-id="5ade0-223">Use the following command to do so:</span></span>
   
        java -cp com-microsoft-azure-eventhubs-client-example.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="5ade0-224">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ade0-224">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="5ade0-225">This makes the jar accessible to Livy.</span><span class="sxs-lookup"><span data-stu-id="5ade0-225">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="5ade0-226">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span><span class="sxs-lookup"><span data-stu-id="5ade0-226">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="5ade0-227">There are a lot of other clients you can use to upload data.</span><span class="sxs-lookup"><span data-stu-id="5ade0-227">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="5ade0-228">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-228">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="5ade0-229">Install CURL on the computer where you are running these applications from.</span><span class="sxs-lookup"><span data-stu-id="5ade0-229">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="5ade0-230">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span><span class="sxs-lookup"><span data-stu-id="5ade0-230">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="5ade0-231">Run the applications to receive the events into an Azure Storage Blob as text</span><span class="sxs-lookup"><span data-stu-id="5ade0-231">Run the applications to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="5ade0-232">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span><span class="sxs-lookup"><span data-stu-id="5ade0-232">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5ade0-233">The parameters in the file **inputBlob.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="5ade0-233">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasbs:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5ade0-234">Let us understand what the parameters in the input file are:</span><span class="sxs-lookup"><span data-stu-id="5ade0-234">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="5ade0-235">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ade0-235">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="5ade0-236">**className** is the name of the class in the jar.</span><span class="sxs-lookup"><span data-stu-id="5ade0-236">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="5ade0-237">**args** is the list of arguments required by the class</span><span class="sxs-lookup"><span data-stu-id="5ade0-237">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="5ade0-238">**numExecutors** is the number of cores used by Spark to run the streaming application.</span><span class="sxs-lookup"><span data-stu-id="5ade0-238">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="5ade0-239">This should always be at least twice the number of Event Hub partitions.</span><span class="sxs-lookup"><span data-stu-id="5ade0-239">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="5ade0-240">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span><span class="sxs-lookup"><span data-stu-id="5ade0-240">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="5ade0-241">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span><span class="sxs-lookup"><span data-stu-id="5ade0-241">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="5ade0-242">The streaming application creates them for you.</span><span class="sxs-lookup"><span data-stu-id="5ade0-242">The streaming application creates them for you.</span></span>
> 
> 

<span data-ttu-id="5ade0-243">When you run the command, you should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="5ade0-243">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="5ade0-244">Make a note of the batch ID in the last line of the output (in this example it is '1').</span><span class="sxs-lookup"><span data-stu-id="5ade0-244">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="5ade0-245">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span><span class="sxs-lookup"><span data-stu-id="5ade0-245">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="5ade0-246">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span><span class="sxs-lookup"><span data-stu-id="5ade0-246">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="5ade0-247">The application will continue to run until you kill it.</span><span class="sxs-lookup"><span data-stu-id="5ade0-247">The application will continue to run until you kill it.</span></span> <span data-ttu-id="5ade0-248">To do so, use the following command:</span><span class="sxs-lookup"><span data-stu-id="5ade0-248">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="5ade0-249">Run the applications to receive the events into an Azure Storage Blob as JSON</span><span class="sxs-lookup"><span data-stu-id="5ade0-249">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="5ade0-250">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span><span class="sxs-lookup"><span data-stu-id="5ade0-250">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5ade0-251">The parameters in the file **inputJSON.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="5ade0-251">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasbs:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5ade0-252">The parameters are similar to what you specified for the text output, in the previous step.</span><span class="sxs-lookup"><span data-stu-id="5ade0-252">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="5ade0-253">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span><span class="sxs-lookup"><span data-stu-id="5ade0-253">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="5ade0-254">The streaming application creates them for you.</span><span class="sxs-lookup"><span data-stu-id="5ade0-254">The streaming application creates them for you.</span></span>

 <span data-ttu-id="5ade0-255">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span><span class="sxs-lookup"><span data-stu-id="5ade0-255">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="5ade0-256">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="5ade0-256">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="5ade0-257">Run the applications to receive the events into a Hive table</span><span class="sxs-lookup"><span data-stu-id="5ade0-257">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="5ade0-258">To run the application that streams events into a Hive table you need some additional components.</span><span class="sxs-lookup"><span data-stu-id="5ade0-258">To run the application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="5ade0-259">These are:</span><span class="sxs-lookup"><span data-stu-id="5ade0-259">These are:</span></span>

* <span data-ttu-id="5ade0-260">datanucleus-api-jdo-3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="5ade0-260">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="5ade0-261">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="5ade0-261">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="5ade0-262">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="5ade0-262">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="5ade0-263">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="5ade0-263">hive-site.xml</span></span>

<span data-ttu-id="5ade0-264">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="5ade0-264">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="5ade0-265">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="5ade0-265">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="5ade0-266">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span><span class="sxs-lookup"><span data-stu-id="5ade0-266">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="5ade0-267">You can then use tools to copy these files over to your storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5ade0-267">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="5ade0-268">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-268">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="5ade0-269">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span><span class="sxs-lookup"><span data-stu-id="5ade0-269">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5ade0-270">The parameters in the file **inputHive.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="5ade0-270">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasbs:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasbs:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasbs:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasbs:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasbs:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5ade0-271">The parameters are similar to what you specified for the text output, in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="5ade0-271">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="5ade0-272">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span><span class="sxs-lookup"><span data-stu-id="5ade0-272">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="5ade0-273">The streaming application creates them for you.</span><span class="sxs-lookup"><span data-stu-id="5ade0-273">The streaming application creates them for you.</span></span> <span data-ttu-id="5ade0-274">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span><span class="sxs-lookup"><span data-stu-id="5ade0-274">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="5ade0-275">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span><span class="sxs-lookup"><span data-stu-id="5ade0-275">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="5ade0-276">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-276">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="5ade0-277">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span><span class="sxs-lookup"><span data-stu-id="5ade0-277">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="5ade0-278">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="5ade0-278">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="5ade0-279">You can also run a SELECT query to view the contents of the table.</span><span class="sxs-lookup"><span data-stu-id="5ade0-279">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="5ade0-280">You should see an output like the following:</span><span class="sxs-lookup"><span data-stu-id="5ade0-280">You should see an output like the following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="5ade0-281">Run the applications to receive the events into an Azure SQL database table</span><span class="sxs-lookup"><span data-stu-id="5ade0-281">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="5ade0-282">Before running this step, make sure you have an Azure SQL database created.</span><span class="sxs-lookup"><span data-stu-id="5ade0-282">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="5ade0-283">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-283">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="5ade0-284">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span><span class="sxs-lookup"><span data-stu-id="5ade0-284">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="5ade0-285">You do not need to create the database table though.</span><span class="sxs-lookup"><span data-stu-id="5ade0-285">You do not need to create the database table though.</span></span> <span data-ttu-id="5ade0-286">The streaming application creates that for you.</span><span class="sxs-lookup"><span data-stu-id="5ade0-286">The streaming application creates that for you.</span></span>

<span data-ttu-id="5ade0-287">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span><span class="sxs-lookup"><span data-stu-id="5ade0-287">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5ade0-288">The parameters in the file **inputSQL.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="5ade0-288">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasbs:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5ade0-289">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5ade0-289">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="5ade0-290">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="5ade0-290">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="5ade0-291">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span><span class="sxs-lookup"><span data-stu-id="5ade0-291">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="5ade0-292">You can run a quick query to get the data from the table.</span><span class="sxs-lookup"><span data-stu-id="5ade0-292">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="5ade0-293">Run the following query:</span><span class="sxs-lookup"><span data-stu-id="5ade0-293">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="5ade0-294">You should see output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="5ade0-294">You should see output similar to the following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <a name="seealso"></a><span data-ttu-id="5ade0-295">See also</span><span class="sxs-lookup"><span data-stu-id="5ade0-295">See also</span></span>
* [<span data-ttu-id="5ade0-296">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-296">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5ade0-297">Scenarios</span><span class="sxs-lookup"><span data-stu-id="5ade0-297">Scenarios</span></span>
* [<span data-ttu-id="5ade0-298">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="5ade0-298">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5ade0-299">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="5ade0-299">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5ade0-300">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="5ade0-300">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5ade0-301">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-301">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5ade0-302">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="5ade0-302">Create and run applications</span></span>
* [<span data-ttu-id="5ade0-303">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="5ade0-303">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5ade0-304">Run jobs remotely on a Spark cluster using Livy</span><span class="sxs-lookup"><span data-stu-id="5ade0-304">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5ade0-305">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="5ade0-305">Tools and extensions</span></span>
* [<span data-ttu-id="5ade0-306">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="5ade0-306">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5ade0-307">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="5ade0-307">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5ade0-308">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-308">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="5ade0-309">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-309">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5ade0-310">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="5ade0-310">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5ade0-311">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="5ade0-311">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5ade0-312">Manage resources</span><span class="sxs-lookup"><span data-stu-id="5ade0-312">Manage resources</span></span>
* [<span data-ttu-id="5ade0-313">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-313">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5ade0-314">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5ade0-314">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://manage.windowsazure.com/
[azure-create-storageaccount]: ../storage-create-storage-account/ 






















