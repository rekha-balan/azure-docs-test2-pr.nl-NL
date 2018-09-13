---
title: Process Apache Kafka for Event Hubs events using Azure Stream analytics | Microsoft Docs
description: This article shows how to process Kafka events that are ingested through event hubs by using Azure Stream Analytics
services: event-hubs
documentationcenter: ''
author: spelluru
manager: ''
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.custom: mvc
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/29/2018
ms.author: spelluru
ms.openlocfilehash: a066d2a55f6949eea316eaf0a2956500667a996f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857183"
---
# <a name="process-apache-kafka-for-event-hubs-events-using-stream-analytics"></a><span data-ttu-id="789ab-103">Process Apache Kafka for Event Hubs events using Stream analytics</span><span class="sxs-lookup"><span data-stu-id="789ab-103">Process Apache Kafka for Event Hubs events using Stream analytics</span></span> 
<span data-ttu-id="789ab-104">This article shows how to stream data into Kafka-enabled Event Hubs and process it with Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="789ab-104">This article shows how to stream data into Kafka-enabled Event Hubs and process it with Azure Stream Analytics.</span></span> <span data-ttu-id="789ab-105">It walks you through the following steps:</span><span class="sxs-lookup"><span data-stu-id="789ab-105">It walks you through the following steps:</span></span> 

1. <span data-ttu-id="789ab-106">Create a Kafka enabled Event Hubs namespace.</span><span class="sxs-lookup"><span data-stu-id="789ab-106">Create a Kafka enabled Event Hubs namespace.</span></span>
2. <span data-ttu-id="789ab-107">Create a Kafka client that sends messages to the event hub.</span><span class="sxs-lookup"><span data-stu-id="789ab-107">Create a Kafka client that sends messages to the event hub.</span></span>
3. <span data-ttu-id="789ab-108">Create a Stream Analytics job that copies data from the event hub into an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="789ab-108">Create a Stream Analytics job that copies data from the event hub into an Azure blob storage.</span></span> 

<span data-ttu-id="789ab-109">You do not need to change your protocol clients or run your own clusters when you use the Kafka endpoint exposed by an event hub.</span><span class="sxs-lookup"><span data-stu-id="789ab-109">You do not need to change your protocol clients or run your own clusters when you use the Kafka endpoint exposed by an event hub.</span></span> <span data-ttu-id="789ab-110">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span><span class="sxs-lookup"><span data-stu-id="789ab-110">Azure Event Hubs supports [Apache Kafka version 1.0.](https://kafka.apache.org/10/documentation.html)</span></span> <span data-ttu-id="789ab-111">and above.</span><span class="sxs-lookup"><span data-stu-id="789ab-111">and above.</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="789ab-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="789ab-112">Prerequisites</span></span>

<span data-ttu-id="789ab-113">To complete this quickstart, make sure you have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="789ab-113">To complete this quickstart, make sure you have the following prerequisites:</span></span>

* <span data-ttu-id="789ab-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="789ab-114">An Azure subscription.</span></span> <span data-ttu-id="789ab-115">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span><span class="sxs-lookup"><span data-stu-id="789ab-115">If you do not have one, create a [free account](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) before you begin.</span></span>
* <span data-ttu-id="789ab-116">[Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="789ab-116">[Java Development Kit (JDK) 1.7+](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>
* <span data-ttu-id="789ab-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive.</span><span class="sxs-lookup"><span data-stu-id="789ab-117">[Download](http://maven.apache.org/download.cgi) and [install](http://maven.apache.org/install.html) a Maven binary archive.</span></span>
* [<span data-ttu-id="789ab-118">Git</span><span class="sxs-lookup"><span data-stu-id="789ab-118">Git</span></span>](https://www.git-scm.com/)
* <span data-ttu-id="789ab-119">An **Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="789ab-119">An **Azure Storage account**.</span></span> <span data-ttu-id="789ab-120">If you don't have one, [create one](../storage/common/storage-create-storage-account.md#create-a-storage-account) before proceeding further.</span><span class="sxs-lookup"><span data-stu-id="789ab-120">If you don't have one, [create one](../storage/common/storage-create-storage-account.md#create-a-storage-account) before proceeding further.</span></span> <span data-ttu-id="789ab-121">The Stream Analytics job in this walkthrough stores the output data in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="789ab-121">The Stream Analytics job in this walkthrough stores the output data in an Azure blob storage.</span></span> 


## <a name="create-a-kafka-enabled-event-hubs-namespace"></a><span data-ttu-id="789ab-122">Create a Kafka enabled Event Hubs namespace</span><span class="sxs-lookup"><span data-stu-id="789ab-122">Create a Kafka enabled Event Hubs namespace</span></span>

1. <span data-ttu-id="789ab-123">Sign in to the [Azure portal](https://portal.azure.com), and click **Create a resource** at the top left of the screen.</span><span class="sxs-lookup"><span data-stu-id="789ab-123">Sign in to the [Azure portal](https://portal.azure.com), and click **Create a resource** at the top left of the screen.</span></span>
2. <span data-ttu-id="789ab-124">Search for **Event Hubs** and select the options shown here:</span><span class="sxs-lookup"><span data-stu-id="789ab-124">Search for **Event Hubs** and select the options shown here:</span></span>
    
    ![Search for Event Hubs in the portal](./media/event-hubs-kafka-stream-analytics/select-event-hubs.png) 
3. <span data-ttu-id="789ab-126">On the **Event Hubs** page, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="789ab-126">On the **Event Hubs** page, select **Create**.</span></span>
4. <span data-ttu-id="789ab-127">On the **Create Namespace** page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="789ab-127">On the **Create Namespace** page, do the following actions:</span></span> 
    1. <span data-ttu-id="789ab-128">Provide a unique **name** for the namespace.</span><span class="sxs-lookup"><span data-stu-id="789ab-128">Provide a unique **name** for the namespace.</span></span> 
    2. <span data-ttu-id="789ab-129">Select a **pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="789ab-129">Select a **pricing tier**.</span></span> 
    3. <span data-ttu-id="789ab-130">Select **Enable Kafka**.</span><span class="sxs-lookup"><span data-stu-id="789ab-130">Select **Enable Kafka**.</span></span> <span data-ttu-id="789ab-131">This step is an **important** step.</span><span class="sxs-lookup"><span data-stu-id="789ab-131">This step is an **important** step.</span></span> 
    4. <span data-ttu-id="789ab-132">Select your **subscription** in which you want the event hub namespace to be created.</span><span class="sxs-lookup"><span data-stu-id="789ab-132">Select your **subscription** in which you want the event hub namespace to be created.</span></span> 
    5. <span data-ttu-id="789ab-133">Create a new **resource group** or select an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="789ab-133">Create a new **resource group** or select an existing resource group.</span></span> 
    6. <span data-ttu-id="789ab-134">Select a **location**.</span><span class="sxs-lookup"><span data-stu-id="789ab-134">Select a **location**.</span></span> 
    7. <span data-ttu-id="789ab-135">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="789ab-135">Click **Create**.</span></span>
    
        ![Create a namespace](./media/event-hubs-kafka-stream-analytics/create-event-hub-namespace-page.png) 
4. <span data-ttu-id="789ab-137">In the **notification message**, select the **resource group name**.</span><span class="sxs-lookup"><span data-stu-id="789ab-137">In the **notification message**, select the **resource group name**.</span></span> 

    ![Create a namespace](./media/event-hubs-kafka-stream-analytics/creation-station-message.png)
1. <span data-ttu-id="789ab-139">Select the **event hub namespace** in the resource group.</span><span class="sxs-lookup"><span data-stu-id="789ab-139">Select the **event hub namespace** in the resource group.</span></span> 
2. <span data-ttu-id="789ab-140">Once the namespace is created, select **Shared access policies** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="789ab-140">Once the namespace is created, select **Shared access policies** under **SETTINGS**.</span></span>

    ![Click Shared access policies](./media/event-hubs-kafka-stream-analytics/shared-access-policies.png)
5. <span data-ttu-id="789ab-142">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span><span class="sxs-lookup"><span data-stu-id="789ab-142">You can choose the default **RootManageSharedAccessKey**, or add a new policy.</span></span> <span data-ttu-id="789ab-143">Click the policy name and copy the **connection string**.</span><span class="sxs-lookup"><span data-stu-id="789ab-143">Click the policy name and copy the **connection string**.</span></span> <span data-ttu-id="789ab-144">You use the connection string to configure the Kafka client.</span><span class="sxs-lookup"><span data-stu-id="789ab-144">You use the connection string to configure the Kafka client.</span></span> 
    
    ![Select a policy](./media/event-hubs-kafka-stream-analytics/connection-string.png)  

<span data-ttu-id="789ab-146">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="789ab-146">You can now stream events from your applications that use the Kafka protocol into Event Hubs.</span></span>

## <a name="send-messages-with-kafka-in-event-hubs"></a><span data-ttu-id="789ab-147">Send messages with Kafka in Event Hubs</span><span class="sxs-lookup"><span data-stu-id="789ab-147">Send messages with Kafka in Event Hubs</span></span>

1. <span data-ttu-id="789ab-148">Clone the [Azure Event Hubs repository](https://github.com/Azure/azure-event-hubs) to your machine.</span><span class="sxs-lookup"><span data-stu-id="789ab-148">Clone the [Azure Event Hubs repository](https://github.com/Azure/azure-event-hubs) to your machine.</span></span>
2. <span data-ttu-id="789ab-149">Navigate to the folder: `azure-event-hubs/samples/kafka/quickstart/producer`.</span><span class="sxs-lookup"><span data-stu-id="789ab-149">Navigate to the folder: `azure-event-hubs/samples/kafka/quickstart/producer`.</span></span> 
4. <span data-ttu-id="789ab-150">Update the configuration details for the producer in `src/main/resources/producer.config`.</span><span class="sxs-lookup"><span data-stu-id="789ab-150">Update the configuration details for the producer in `src/main/resources/producer.config`.</span></span> <span data-ttu-id="789ab-151">Specify the **name** and **connection string** for the **event hub namespace**.</span><span class="sxs-lookup"><span data-stu-id="789ab-151">Specify the **name** and **connection string** for the **event hub namespace**.</span></span> 

    ```xml
    bootstrap.servers={EVENT HUB NAMESPACE}.servicebus.windows.net:9093
    security.protocol=SASL_SSL
    sasl.mechanism=PLAIN
    sasl.jaas.config=org.apache.kafka.common.security.plain.PlainLoginModule required username="$ConnectionString" password="{CONNECTION STRING for EVENT HUB NAMESPACE}";
    ```

5. <span data-ttu-id="789ab-152">Navigate to `azure-event-hubs/samples/kafka/quickstart/producer/src/main/java/com/example/app`, and open **TestDataReporter.java** file in an editor of your choice.</span><span class="sxs-lookup"><span data-stu-id="789ab-152">Navigate to `azure-event-hubs/samples/kafka/quickstart/producer/src/main/java/com/example/app`, and open **TestDataReporter.java** file in an editor of your choice.</span></span> 
6. <span data-ttu-id="789ab-153">Comment out the following line of code:</span><span class="sxs-lookup"><span data-stu-id="789ab-153">Comment out the following line of code:</span></span>

    ```java
                //final ProducerRecord<Long, String> record = new ProducerRecord<Long, String>(TOPIC, time, "Test Data " + i);
    ```
3. <span data-ttu-id="789ab-154">Add the following line of code in place of the commented code:</span><span class="sxs-lookup"><span data-stu-id="789ab-154">Add the following line of code in place of the commented code:</span></span> 

    ```java
                final ProducerRecord<Long, String> record = new ProducerRecord<Long, String>(TOPIC, time, "{ \"eventData\": \"Test Data " + i + "\" }");            
    ```

    <span data-ttu-id="789ab-155">This code sends the event data in **JSON** format.</span><span class="sxs-lookup"><span data-stu-id="789ab-155">This code sends the event data in **JSON** format.</span></span> <span data-ttu-id="789ab-156">When you configure input for a Stream Analytics job, you specify JSON as the format for the input data.</span><span class="sxs-lookup"><span data-stu-id="789ab-156">When you configure input for a Stream Analytics job, you specify JSON as the format for the input data.</span></span> 
7. <span data-ttu-id="789ab-157">**Run the producer** and stream into Kafka-enabled Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="789ab-157">**Run the producer** and stream into Kafka-enabled Event Hubs.</span></span> <span data-ttu-id="789ab-158">On a Windows machine, when using a **Node.js command prompt**, switch to the `azure-event-hubs/samples/kafka/quickstart/producer` folder before running these commands.</span><span class="sxs-lookup"><span data-stu-id="789ab-158">On a Windows machine, when using a **Node.js command prompt**, switch to the `azure-event-hubs/samples/kafka/quickstart/producer` folder before running these commands.</span></span> 
   
    ```shell
    mvn clean package
    mvn exec:java -Dexec.mainClass="TestProducer"                                    
    ```

## <a name="verify-that-event-hub-receives-the-data"></a><span data-ttu-id="789ab-159">Verify that event hub receives the data</span><span class="sxs-lookup"><span data-stu-id="789ab-159">Verify that event hub receives the data</span></span>

1. <span data-ttu-id="789ab-160">Select **Event Hubs** under **ENTITIES**.</span><span class="sxs-lookup"><span data-stu-id="789ab-160">Select **Event Hubs** under **ENTITIES**.</span></span> <span data-ttu-id="789ab-161">Confirm that you see an event hub named **test**.</span><span class="sxs-lookup"><span data-stu-id="789ab-161">Confirm that you see an event hub named **test**.</span></span> 

    ![Event hub - test](./media/event-hubs-kafka-stream-analytics/test-event-hub.png)
2. <span data-ttu-id="789ab-163">Confirm that you see messages coming in to the event hub.</span><span class="sxs-lookup"><span data-stu-id="789ab-163">Confirm that you see messages coming in to the event hub.</span></span> 

    ![Event hub - messages](./media/event-hubs-kafka-stream-analytics/confirm-event-hub-messages.png)

## <a name="process-event-data-using-a-stream-analytics-job"></a><span data-ttu-id="789ab-165">Process event data using a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="789ab-165">Process event data using a Stream Analytics job</span></span>
<span data-ttu-id="789ab-166">In this section, you create an Azure Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="789ab-166">In this section, you create an Azure Stream Analytics job.</span></span> <span data-ttu-id="789ab-167">The Kafka client sends events to the event hub.</span><span class="sxs-lookup"><span data-stu-id="789ab-167">The Kafka client sends events to the event hub.</span></span> <span data-ttu-id="789ab-168">You create a Stream Analytics job that takes event data as input and outputs it to an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="789ab-168">You create a Stream Analytics job that takes event data as input and outputs it to an Azure blob storage.</span></span> <span data-ttu-id="789ab-169">If you don't have  an **Azure Storage account**, [create one](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="789ab-169">If you don't have  an **Azure Storage account**, [create one](../storage/common/storage-create-storage-account.md#create-a-storage-account).</span></span>

<span data-ttu-id="789ab-170">The query in the Stream Analytics job passes through the data without performing any analytics.</span><span class="sxs-lookup"><span data-stu-id="789ab-170">The query in the Stream Analytics job passes through the data without performing any analytics.</span></span> <span data-ttu-id="789ab-171">You can create a query that transforms the input data to produce output data in a different format or with gained insights.</span><span class="sxs-lookup"><span data-stu-id="789ab-171">You can create a query that transforms the input data to produce output data in a different format or with gained insights.</span></span>  

### <a name="create-a-stream-analytics-job"></a><span data-ttu-id="789ab-172">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="789ab-172">Create a Stream Analytics job</span></span> 

1. <span data-ttu-id="789ab-173">Select **+ Create a resource** in the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="789ab-173">Select **+ Create a resource** in the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="789ab-174">Select **Analytics** in the **Azure Marketplace** menu, and select **Stream Analytics job**.</span><span class="sxs-lookup"><span data-stu-id="789ab-174">Select **Analytics** in the **Azure Marketplace** menu, and select **Stream Analytics job**.</span></span> 
3. <span data-ttu-id="789ab-175">On the **New Stream Analytics** page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="789ab-175">On the **New Stream Analytics** page, do the following actions:</span></span> 
    1. <span data-ttu-id="789ab-176">Enter a **name** for the job.</span><span class="sxs-lookup"><span data-stu-id="789ab-176">Enter a **name** for the job.</span></span> 
    2. <span data-ttu-id="789ab-177">Select your **subscription**.</span><span class="sxs-lookup"><span data-stu-id="789ab-177">Select your **subscription**.</span></span>
    3. <span data-ttu-id="789ab-178">Select **Create new** for the **resource group** and enter the name.</span><span class="sxs-lookup"><span data-stu-id="789ab-178">Select **Create new** for the **resource group** and enter the name.</span></span> <span data-ttu-id="789ab-179">You can also **use an existing** resource group.</span><span class="sxs-lookup"><span data-stu-id="789ab-179">You can also **use an existing** resource group.</span></span> 
    4. <span data-ttu-id="789ab-180">Select a **location** for the job.</span><span class="sxs-lookup"><span data-stu-id="789ab-180">Select a **location** for the job.</span></span>
    5. <span data-ttu-id="789ab-181">Select **Create** to create the job.</span><span class="sxs-lookup"><span data-stu-id="789ab-181">Select **Create** to create the job.</span></span> 

        ![New Stream Analytics job](./media/event-hubs-kafka-stream-analytics/new-stream-analytics-job.png)

### <a name="configure-job-input"></a><span data-ttu-id="789ab-183">Configure job input</span><span class="sxs-lookup"><span data-stu-id="789ab-183">Configure job input</span></span>

1. <span data-ttu-id="789ab-184">In the notification message, select \*\* Go to resource\*\* to see the **Stream Analytics job** page.</span><span class="sxs-lookup"><span data-stu-id="789ab-184">In the notification message, select \*\* Go to resource\*\* to see the **Stream Analytics job** page.</span></span> 
2. <span data-ttu-id="789ab-185">Select **Inputs** in the **JOB TOPOLOGY** section on the left menu.</span><span class="sxs-lookup"><span data-stu-id="789ab-185">Select **Inputs** in the **JOB TOPOLOGY** section on the left menu.</span></span>
3. <span data-ttu-id="789ab-186">Select **Add stream input**, and then select **Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="789ab-186">Select **Add stream input**, and then select **Event Hub**.</span></span> 

    ![Add event hub as an input](./media/event-hubs-kafka-stream-analytics/select-event-hub-input.png)
4. <span data-ttu-id="789ab-188">On the **Event Hub input** configuration page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="789ab-188">On the **Event Hub input** configuration page, do the following actions:</span></span> 

    1. <span data-ttu-id="789ab-189">Specify an **alias** for the input.</span><span class="sxs-lookup"><span data-stu-id="789ab-189">Specify an **alias** for the input.</span></span> 
    2. <span data-ttu-id="789ab-190">Select your **Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="789ab-190">Select your **Azure subscription**.</span></span>
    3. <span data-ttu-id="789ab-191">Select the **event hub namespace** your created earlier.</span><span class="sxs-lookup"><span data-stu-id="789ab-191">Select the **event hub namespace** your created earlier.</span></span> 
    4. <span data-ttu-id="789ab-192">Select **test** for the **event hub**.</span><span class="sxs-lookup"><span data-stu-id="789ab-192">Select **test** for the **event hub**.</span></span> 
    5. <span data-ttu-id="789ab-193">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="789ab-193">Select **Save**.</span></span> 

        ![Event hub input configuration](./media/event-hubs-kafka-stream-analytics/event-hub-input-configuration.png)

### <a name="configure-job-output"></a><span data-ttu-id="789ab-195">Configure job output</span><span class="sxs-lookup"><span data-stu-id="789ab-195">Configure job output</span></span> 

1. <span data-ttu-id="789ab-196">Select **Outputs** in the **JOB TOPOLOGY** section on the menu.</span><span class="sxs-lookup"><span data-stu-id="789ab-196">Select **Outputs** in the **JOB TOPOLOGY** section on the menu.</span></span> 
2. <span data-ttu-id="789ab-197">Select **+ Add** on the toolbar, and select **Blob storage**</span><span class="sxs-lookup"><span data-stu-id="789ab-197">Select **+ Add** on the toolbar, and select **Blob storage**</span></span>
3. <span data-ttu-id="789ab-198">On the Blob storage output settings page, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="789ab-198">On the Blob storage output settings page, do the following actions:</span></span> 
    1. <span data-ttu-id="789ab-199">Specify an **alias** for the output.</span><span class="sxs-lookup"><span data-stu-id="789ab-199">Specify an **alias** for the output.</span></span> 
    2. <span data-ttu-id="789ab-200">Select your Azure **subscription**.</span><span class="sxs-lookup"><span data-stu-id="789ab-200">Select your Azure **subscription**.</span></span> 
    3. <span data-ttu-id="789ab-201">Select your **Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="789ab-201">Select your **Azure Storage account**.</span></span> 
    4. <span data-ttu-id="789ab-202">Enter a **name for the container** that stores the output data from the Stream Analytics query.</span><span class="sxs-lookup"><span data-stu-id="789ab-202">Enter a **name for the container** that stores the output data from the Stream Analytics query.</span></span>
    5. <span data-ttu-id="789ab-203">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="789ab-203">Select **Save**.</span></span>

        ![Blob Storage output configuration](./media/event-hubs-kafka-stream-analytics/output-blob-settings.png)
 

### <a name="define-a-query"></a><span data-ttu-id="789ab-205">Define a query</span><span class="sxs-lookup"><span data-stu-id="789ab-205">Define a query</span></span>
<span data-ttu-id="789ab-206">After you have a Stream Analytics job setup to read an incoming data stream, the next step is to create a transformation that analyzes data in real time.</span><span class="sxs-lookup"><span data-stu-id="789ab-206">After you have a Stream Analytics job setup to read an incoming data stream, the next step is to create a transformation that analyzes data in real time.</span></span> <span data-ttu-id="789ab-207">You define the transformation query by using [Stream Analytics Query Language](https://msdn.microsoft.com/library/dn834998.aspx).</span><span class="sxs-lookup"><span data-stu-id="789ab-207">You define the transformation query by using [Stream Analytics Query Language](https://msdn.microsoft.com/library/dn834998.aspx).</span></span> <span data-ttu-id="789ab-208">In this walkthrough, you define a query that passes through the data without performing any transformation.</span><span class="sxs-lookup"><span data-stu-id="789ab-208">In this walkthrough, you define a query that passes through the data without performing any transformation.</span></span>

1. <span data-ttu-id="789ab-209">Select **Query**.</span><span class="sxs-lookup"><span data-stu-id="789ab-209">Select **Query**.</span></span>
2. <span data-ttu-id="789ab-210">In the query window, replace `[YourOutputAlias]` with the output alias you created earlier.</span><span class="sxs-lookup"><span data-stu-id="789ab-210">In the query window, replace `[YourOutputAlias]` with the output alias you created earlier.</span></span>
3. <span data-ttu-id="789ab-211">Replace `[YourInputAlias]` with the input alias you created earlier.</span><span class="sxs-lookup"><span data-stu-id="789ab-211">Replace `[YourInputAlias]` with the input alias you created earlier.</span></span> 
4. <span data-ttu-id="789ab-212">Select **Save** on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="789ab-212">Select **Save** on the toolbar.</span></span> 

    ![Query](./media/event-hubs-kafka-stream-analytics/query.png)


### <a name="run-the-stream-analytics-job"></a><span data-ttu-id="789ab-214">Run the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="789ab-214">Run the Stream Analytics job</span></span>

1. <span data-ttu-id="789ab-215">Select **Overview** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="789ab-215">Select **Overview** on the left menu.</span></span> 
2. <span data-ttu-id="789ab-216">Select **Start**.</span><span class="sxs-lookup"><span data-stu-id="789ab-216">Select **Start**.</span></span> 

    ![Start menu](./media/event-hubs-kafka-stream-analytics/start-menu.png)
1. <span data-ttu-id="789ab-218">On the **Start job** page, select **Start**.</span><span class="sxs-lookup"><span data-stu-id="789ab-218">On the **Start job** page, select **Start**.</span></span> 

    ![Start job page](./media/event-hubs-kafka-stream-analytics/start-job-page.png)
1. <span data-ttu-id="789ab-220">Wait until the status of the job changes from **Starting** to **running**.</span><span class="sxs-lookup"><span data-stu-id="789ab-220">Wait until the status of the job changes from **Starting** to **running**.</span></span> 

    ![Job status - running](./media/event-hubs-kafka-stream-analytics/running.png)

## <a name="test-the-scenario"></a><span data-ttu-id="789ab-222">Test the scenario</span><span class="sxs-lookup"><span data-stu-id="789ab-222">Test the scenario</span></span>
1. <span data-ttu-id="789ab-223">Run the **Kafka producer** again to send events to the event hub.</span><span class="sxs-lookup"><span data-stu-id="789ab-223">Run the **Kafka producer** again to send events to the event hub.</span></span> 

    ```shell
    mvn exec:java -Dexec.mainClass="TestProducer"                                    
    ```
1. <span data-ttu-id="789ab-224">Confirm that you see **output data** is generated in the **Azure blob storage**.</span><span class="sxs-lookup"><span data-stu-id="789ab-224">Confirm that you see **output data** is generated in the **Azure blob storage**.</span></span> <span data-ttu-id="789ab-225">You see a JSON file in the container with 100 rows that look like the following sample rows:</span><span class="sxs-lookup"><span data-stu-id="789ab-225">You see a JSON file in the container with 100 rows that look like the following sample rows:</span></span> 

    ```
    {"eventData":"Test Data 0","EventProcessedUtcTime":"2018-08-30T03:27:23.1592910Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}
    {"eventData":"Test Data 1","EventProcessedUtcTime":"2018-08-30T03:27:23.3936511Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}
    {"eventData":"Test Data 2","EventProcessedUtcTime":"2018-08-30T03:27:23.3936511Z","PartitionId":0,"EventEnqueuedUtcTime":"2018-08-30T03:27:22.9220000Z"}
    ```

    <span data-ttu-id="789ab-226">The Azure Stream Analytics job received input data from the event hub and stored it in the Azure blob storage in this scenario.</span><span class="sxs-lookup"><span data-stu-id="789ab-226">The Azure Stream Analytics job received input data from the event hub and stored it in the Azure blob storage in this scenario.</span></span> 



## <a name="next-steps"></a><span data-ttu-id="789ab-227">Next steps</span><span class="sxs-lookup"><span data-stu-id="789ab-227">Next steps</span></span>
<span data-ttu-id="789ab-228">In this article, you learned how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span><span class="sxs-lookup"><span data-stu-id="789ab-228">In this article, you learned how to stream into Kafka-enabled Event Hubs without changing your protocol clients or running your own clusters.</span></span> <span data-ttu-id="789ab-229">To learn more, continue with the following tutorial:</span><span class="sxs-lookup"><span data-stu-id="789ab-229">To learn more, continue with the following tutorial:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="789ab-230">Use Kafka MirrorMaker with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="789ab-230">Use Kafka MirrorMaker with Event Hubs</span></span>](event-hubs-kafka-mirror-maker-tutorial.md)
