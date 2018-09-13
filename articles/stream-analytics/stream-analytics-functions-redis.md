---
title: Stream Analytics real-time processing for Azure Functions | Microsoft Docs
description: Learn how to use an Azure Function connected a Service Bus Queue, to populate an Azure Redis Cache from the output of a Stream Analytics job.
keywords: data stream, redis cache, service bus queue
services: stream-analytics
author: ryancrawcour
manager: jhubbard
documentationcenter: ''
ms.assetid: d428bb33-4244-4001-b93d-c77bed816527
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/28/2017
ms.author: ryancraw
ms.openlocfilehash: be98c99b23fa42af87513c06c097a2fea3aa58a6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44672278"
---
# <a name="how-to-store-data-from-azure-stream-analytics-in-an-azure-redis-cache-using-azure-functions"></a><span data-ttu-id="48e59-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span><span class="sxs-lookup"><span data-stu-id="48e59-104">How to store data from Azure Stream Analytics in an Azure Redis Cache using Azure Functions</span></span>
<span data-ttu-id="48e59-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span><span class="sxs-lookup"><span data-stu-id="48e59-105">Azure Stream Analytics lets you rapidly develop and deploy low-cost solutions to gain real-time insights from devices, sensors, infrastructure, and applications, or any stream of data.</span></span> <span data-ttu-id="48e59-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span><span class="sxs-lookup"><span data-stu-id="48e59-106">It enables various use cases such as real-time management and monitoring, command and control, fraud detection, connected cars and many more.</span></span> <span data-ttu-id="48e59-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-107">In many such scenarios, you may want to store data outputted by Azure Stream Analytics into a distributed data store such as an Azure Redis cache.</span></span>

<span data-ttu-id="48e59-108">Suppose you are part of a telecommunications company.</span><span class="sxs-lookup"><span data-stu-id="48e59-108">Suppose you are part of a telecommunications company.</span></span> <span data-ttu-id="48e59-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span><span class="sxs-lookup"><span data-stu-id="48e59-109">You are trying to detect SIM fraud where multiple calls coming from the same identity, at the same time, but in different geographically locations.</span></span> <span data-ttu-id="48e59-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-110">You are tasked with storing all the potential fraudulent phone calls in an Azure Redis cache.</span></span> <span data-ttu-id="48e59-111">In this blog, we provide guidance on how you can easily complete your task.</span><span class="sxs-lookup"><span data-stu-id="48e59-111">In this blog, we provide guidance on how you can easily complete your task.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="48e59-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="48e59-112">Prerequisites</span></span>
<span data-ttu-id="48e59-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span><span class="sxs-lookup"><span data-stu-id="48e59-113">Complete the [Real-time Fraud Detection][fraud-detection] walk-through for ASA</span></span>

## <a name="architecture-overview"></a><span data-ttu-id="48e59-114">Architecture Overview</span><span class="sxs-lookup"><span data-stu-id="48e59-114">Architecture Overview</span></span>
![Screenshot of architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/architecture-overview.png)

<span data-ttu-id="48e59-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span><span class="sxs-lookup"><span data-stu-id="48e59-116">As shown in the preceding figure, Stream Analytics allows streaming input data to be queried and sent to an output.</span></span> <span data-ttu-id="48e59-117">Based on the output, Azure Functions can then trigger some type of event.</span><span class="sxs-lookup"><span data-stu-id="48e59-117">Based on the output, Azure Functions can then trigger some type of event.</span></span> 

<span data-ttu-id="48e59-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-118">In this blog, we focus on the Azure Functions part of this pipeline, or more specifically the triggering of an event that stores fraudulent data into the cache.</span></span>
<span data-ttu-id="48e59-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span><span class="sxs-lookup"><span data-stu-id="48e59-119">After completing the [Real-time Fraud Detection][fraud-detection] tutorial, you have an input (an event hub), a query, and an output (blob storage) already configured and running.</span></span> <span data-ttu-id="48e59-120">In this blog, we change the output to use a Service Bus Queue instead.</span><span class="sxs-lookup"><span data-stu-id="48e59-120">In this blog, we change the output to use a Service Bus Queue instead.</span></span> <span data-ttu-id="48e59-121">After that, we connect an Azure Function to this queue.</span><span class="sxs-lookup"><span data-stu-id="48e59-121">After that, we connect an Azure Function to this queue.</span></span> 

## <a name="create-and-connect-a-service-bus-queue-output"></a><span data-ttu-id="48e59-122">Create and connect a Service Bus Queue output</span><span class="sxs-lookup"><span data-stu-id="48e59-122">Create and connect a Service Bus Queue output</span></span>
<span data-ttu-id="48e59-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="48e59-123">To create a Service Bus Queue, follow steps 1 and 2 of the .NET section in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span>
<span data-ttu-id="48e59-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span><span class="sxs-lookup"><span data-stu-id="48e59-124">Now let's connect the queue to the Stream Analytics job that was created in the earlier fraud detection walk-through.</span></span>

1. <span data-ttu-id="48e59-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="48e59-125">In the Azure portal, go to the **Outputs** blade of your job and select **Add** at the top of the page.</span></span>
   
    ![Adding outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/adding-outputs.png)
2. <span data-ttu-id="48e59-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span><span class="sxs-lookup"><span data-stu-id="48e59-127">Choose **Service Bus Queue** as the **Sink** and follow the instructions on the screen.</span></span> <span data-ttu-id="48e59-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span><span class="sxs-lookup"><span data-stu-id="48e59-128">Be sure to choose the namespace of the Service Bus Queue you created in [Get Started with Service Bus Queues][servicebus-getstarted].</span></span> <span data-ttu-id="48e59-129">Click the "right" button when you are finished.</span><span class="sxs-lookup"><span data-stu-id="48e59-129">Click the "right" button when you are finished.</span></span>
3. <span data-ttu-id="48e59-130">Specify the following values:</span><span class="sxs-lookup"><span data-stu-id="48e59-130">Specify the following values:</span></span>
   
   * <span data-ttu-id="48e59-131">**Event Serializer Format**: JSON</span><span class="sxs-lookup"><span data-stu-id="48e59-131">**Event Serializer Format**: JSON</span></span>
   * <span data-ttu-id="48e59-132">**Encoding**: UTF8</span><span class="sxs-lookup"><span data-stu-id="48e59-132">**Encoding**: UTF8</span></span>
   * <span data-ttu-id="48e59-133">**FORMAT**: Line separated</span><span class="sxs-lookup"><span data-stu-id="48e59-133">**FORMAT**: Line separated</span></span>
4. <span data-ttu-id="48e59-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span><span class="sxs-lookup"><span data-stu-id="48e59-134">Click the **Create** button to add this source and to verify that Stream Analytics can successfully connect to the storage account.</span></span>
5. <span data-ttu-id="48e59-135">In the **Query** tab, replace the current query with the following.</span><span class="sxs-lookup"><span data-stu-id="48e59-135">In the **Query** tab, replace the current query with the following.</span></span> <span data-ttu-id="48e59-136">Replace \*[YOUR SERVICE BUS NAME] \* with the output name you created in step 3.</span><span class="sxs-lookup"><span data-stu-id="48e59-136">Replace \*[YOUR SERVICE BUS NAME] \* with the output name you created in step 3.</span></span> 
   
    ```    
   
        SELECT 
            System.Timestamp as Time, CS1.CallingIMSI, CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, CS1.SwitchNum as Switch1, CS2.SwitchNum as Switch2
   
        INTO [YOUR SERVICE BUS NAME]
   
        FROM CallStream CS1 TIMESTAMP BY CallRecTime
        JOIN CallStream CS2 TIMESTAMP BY CallRecTime
            ON CS1.CallingIMSI = CS2.CallingIMSI AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5
   
        WHERE CS1.SwitchNum != CS2.SwitchNum
   
    ```

## <a name="create-an-azure-redis-cache"></a><span data-ttu-id="48e59-137">Create an Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="48e59-137">Create an Azure Redis Cache</span></span>
<span data-ttu-id="48e59-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span><span class="sxs-lookup"><span data-stu-id="48e59-138">Create an Azure Redis cache by following the .NET section in [How to Use Azure Redis Cache][use-rediscache] until the section called ***Configure the cache clients***.</span></span>
<span data-ttu-id="48e59-139">Once complete, you have a new Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-139">Once complete, you have a new Redis Cache.</span></span> <span data-ttu-id="48e59-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span><span class="sxs-lookup"><span data-stu-id="48e59-140">Under **All settings**, select **Access keys** and note down the ***Primary connection string***.</span></span>

![Screenshot of architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/redis-cache-keys.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="48e59-142">Create an Azure Function</span><span class="sxs-lookup"><span data-stu-id="48e59-142">Create an Azure Function</span></span>
<span data-ttu-id="48e59-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="48e59-143">Follow [Create your first Azure Function][functions-getstarted] tutorial to get started with Azure Functions.</span></span> <span data-ttu-id="48e59-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span><span class="sxs-lookup"><span data-stu-id="48e59-144">If you already have an Azure function you would like to use, then skip ahead to [Writing to Redis Cache](#Writing-to-Redis-Cache)</span></span>

1. <span data-ttu-id="48e59-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span><span class="sxs-lookup"><span data-stu-id="48e59-145">In the portal, select App Services from the left-hand navigation, then click your Azure function app name to get to the Function's app website.</span></span>
    <span data-ttu-id="48e59-146">![Screenshot of app services function list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/app-services-function-list.png)</span><span class="sxs-lookup"><span data-stu-id="48e59-146">![Screenshot of app services function list](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/app-services-function-list.png)</span></span>
2. <span data-ttu-id="48e59-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span><span class="sxs-lookup"><span data-stu-id="48e59-147">Click **New Function > ServiceBusQueueTrigger – C#**.</span></span> <span data-ttu-id="48e59-148">For the following fields, follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="48e59-148">For the following fields, follow these instructions:</span></span>
   
   * <span data-ttu-id="48e59-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span><span class="sxs-lookup"><span data-stu-id="48e59-149">**Queue name**: The same name as the name you entered when you created the queue in [Get Started with Service Bus Queues][servicebus-getstarted] (not the name of the service bus).</span></span> <span data-ttu-id="48e59-150">Make sure you use the queue that is connected to the Stream Analytics output.</span><span class="sxs-lookup"><span data-stu-id="48e59-150">Make sure you use the queue that is connected to the Stream Analytics output.</span></span>
   * <span data-ttu-id="48e59-151">**Service Bus connection**: Select **Add a connection string**.</span><span class="sxs-lookup"><span data-stu-id="48e59-151">**Service Bus connection**: Select **Add a connection string**.</span></span> <span data-ttu-id="48e59-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="48e59-152">To find the connection string, go to the classic portal, select **Service Bus**, the service bus you created, and **CONNECTION INFORMATION** at the bottom of the screen.</span></span> <span data-ttu-id="48e59-153">Make sure you are on the main screen on this page.</span><span class="sxs-lookup"><span data-stu-id="48e59-153">Make sure you are on the main screen on this page.</span></span> <span data-ttu-id="48e59-154">Copy and paste the connection string.</span><span class="sxs-lookup"><span data-stu-id="48e59-154">Copy and paste the connection string.</span></span> <span data-ttu-id="48e59-155">Feel free to enter any connection name.</span><span class="sxs-lookup"><span data-stu-id="48e59-155">Feel free to enter any connection name.</span></span>
     
       ![Screenshot of service bus connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/servicebus-connection.png)
   * <span data-ttu-id="48e59-157">**AccessRights**: Choose **Manage**</span><span class="sxs-lookup"><span data-stu-id="48e59-157">**AccessRights**: Choose **Manage**</span></span>
3. <span data-ttu-id="48e59-158">Click **Create**</span><span class="sxs-lookup"><span data-stu-id="48e59-158">Click **Create**</span></span>

## <a name="writing-to-redis-cache"></a><span data-ttu-id="48e59-159">Writing to Redis Cache</span><span class="sxs-lookup"><span data-stu-id="48e59-159">Writing to Redis Cache</span></span>
<span data-ttu-id="48e59-160">We have now created an Azure Function that reads from a Service Bus Queue.</span><span class="sxs-lookup"><span data-stu-id="48e59-160">We have now created an Azure Function that reads from a Service Bus Queue.</span></span> <span data-ttu-id="48e59-161">All that is left to do is use our Function to write this data to the Redis Cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-161">All that is left to do is use our Function to write this data to the Redis Cache.</span></span> 

1. <span data-ttu-id="48e59-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span><span class="sxs-lookup"><span data-stu-id="48e59-162">Select your newly created **ServiceBusQueueTrigger**, and click **Function app settings** on the top right corner.</span></span> <span data-ttu-id="48e59-163">Select **Go to App Service Settings > Settings > Application settings**</span><span class="sxs-lookup"><span data-stu-id="48e59-163">Select **Go to App Service Settings > Settings > Application settings**</span></span>
2. <span data-ttu-id="48e59-164">In the Connection strings section, create a name in the **Name** section.</span><span class="sxs-lookup"><span data-stu-id="48e59-164">In the Connection strings section, create a name in the **Name** section.</span></span> <span data-ttu-id="48e59-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span><span class="sxs-lookup"><span data-stu-id="48e59-165">Paste the primary connection string you found in the **Create a Redis Cache** step into the **Value** section.</span></span> <span data-ttu-id="48e59-166">Select **Custom** where it says **SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="48e59-166">Select **Custom** where it says **SQL Database**.</span></span>
3. <span data-ttu-id="48e59-167">Click **Save** at the top.</span><span class="sxs-lookup"><span data-stu-id="48e59-167">Click **Save** at the top.</span></span>
   
    ![Screenshot of service bus connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/function-connection-string.png)
4. <span data-ttu-id="48e59-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span><span class="sxs-lookup"><span data-stu-id="48e59-169">Now go back to the App Service Settings and select **Tools > App Service Editor (Preview) > On > Go**.</span></span>
   
    ![Screenshot of service bus connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/app-service-editor.png)
5. <span data-ttu-id="48e59-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span><span class="sxs-lookup"><span data-stu-id="48e59-171">In an editor of your choice, create a JSON file named **project.json** with the following and save it to your local disk.</span></span>
   
        {
            "frameworks": {
                "net46": {
                    "dependencies": {
                        "StackExchange.Redis":"1.1.603",
                        "Newtonsoft.Json": "9.0.1"
                    }
                }
            }
        }
6. <span data-ttu-id="48e59-172">Upload this file into the root directory of your function (not WWWROOT).</span><span class="sxs-lookup"><span data-stu-id="48e59-172">Upload this file into the root directory of your function (not WWWROOT).</span></span> <span data-ttu-id="48e59-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span><span class="sxs-lookup"><span data-stu-id="48e59-173">You should see a file named **project.lock.json** automatically appear, confirming that the Nuget packages “StackExchange.Redis” and “Newtonsoft.Json” have been imported.</span></span>
7. <span data-ttu-id="48e59-174">In the **run.csx** file, replace the pre-generated code with the following code.</span><span class="sxs-lookup"><span data-stu-id="48e59-174">In the **run.csx** file, replace the pre-generated code with the following code.</span></span> <span data-ttu-id="48e59-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span><span class="sxs-lookup"><span data-stu-id="48e59-175">In the lazyConnection function, replace “CONN NAME” with the name you created in step 2 of **Store data into the Redis cache**.</span></span>

````

    using System;
    using System.Threading.Tasks;
    using StackExchange.Redis;
    using Newtonsoft.Json;
    using System.Configuration;

    public static void Run(string myQueueItem, TraceWriter log)
    {
        log.Info($"Function processed message: {myQueueItem}");

        // Connection refers to a property that returns a ConnectionMultiplexer
        IDatabase db = Connection.GetDatabase();
        log.Info($"Created database {db}");

        // Parse JSON and extract the time
        var message = JsonConvert.DeserializeObject<dynamic>(myQueueItem);
        string time = message.time;
        string callingnum1 = message.callingnum1;

        // Perform cache operations using the cache object...
        // Simple put of integral data types into the cache
        string key = time + " - " + callingnum1;
        db.StringSet(key, myQueueItem);
        log.Info($"Object put in database. Key is {key} and value is {myQueueItem}");

        // Simple get of data types from the cache
        string value = db.StringGet(key);
        log.Info($"Database got: {value}"); 
    }

    // Connect to the Service Bus
    private static Lazy<ConnectionMultiplexer> lazyConnection = 
        new Lazy<ConnectionMultiplexer>(() =>
            {
                var cnn = ConfigurationManager.ConnectionStrings["CONN NAME"].ConnectionString
                return ConnectionMultiplexer.Connect();
            });

    public static ConnectionMultiplexer Connection
    {
        get
        {
            return lazyConnection.Value;
        }
    }

````

## <a name="start-the-stream-analytics-job"></a><span data-ttu-id="48e59-176">Start the Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="48e59-176">Start the Stream Analytics job</span></span>
1. <span data-ttu-id="48e59-177">Start the telcodatagen.exe application.</span><span class="sxs-lookup"><span data-stu-id="48e59-177">Start the telcodatagen.exe application.</span></span> <span data-ttu-id="48e59-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span><span class="sxs-lookup"><span data-stu-id="48e59-178">The usage is as follows: ````telcodatagen.exe [#NumCDRsPerHour] [SIM Card Fraud Probability] [#DurationHours]````</span></span>
2. <span data-ttu-id="48e59-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="48e59-179">From the Stream Analytics Job blade in the portal, click **Start** at the top of the page.</span></span>
   
    ![Screenshot of start job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/starting-job.png)
3. <span data-ttu-id="48e59-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="48e59-181">In the **Start job** blade that appears, select **Now** and then click the **Start** button at the bottom of the screen.</span></span> <span data-ttu-id="48e59-182">The job status changes to Starting and after some time changes to Running.</span><span class="sxs-lookup"><span data-stu-id="48e59-182">The job status changes to Starting and after some time changes to Running.</span></span>
   
    ![Screenshot of start job time selection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/start-job-time.png)

## <a name="run-solution-and-check-results"></a><span data-ttu-id="48e59-184">Run solution and check results</span><span class="sxs-lookup"><span data-stu-id="48e59-184">Run solution and check results</span></span>
<span data-ttu-id="48e59-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span><span class="sxs-lookup"><span data-stu-id="48e59-185">Going back to your **ServiceBusQueueTrigger** page, you should now see log statements.</span></span> <span data-ttu-id="48e59-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span><span class="sxs-lookup"><span data-stu-id="48e59-186">These logs show that you got something from the Service Bus Queue, put it into the database, and fetched it out using the time as the key!</span></span>

<span data-ttu-id="48e59-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span><span class="sxs-lookup"><span data-stu-id="48e59-187">To verify that your data is in your Redis cache, go to your Redis cache page in the new portal (as shown in the preceding [Create an Azure Redis Cache](#Create-an-Azure-Redis-Cache) step) and select Console.</span></span>

<span data-ttu-id="48e59-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span><span class="sxs-lookup"><span data-stu-id="48e59-188">Now you can write Redis commands to confirm that data is in fact in the cache.</span></span>

![Screenshot of Redis Console](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-functions-redis/redis-console.png)

## <a name="next-steps"></a><span data-ttu-id="48e59-190">Next steps</span><span class="sxs-lookup"><span data-stu-id="48e59-190">Next steps</span></span>
<span data-ttu-id="48e59-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span><span class="sxs-lookup"><span data-stu-id="48e59-191">We’re excited about the new things Azure Functions and Stream analytics can do together, and we hope this unlocks new possibilities for you.</span></span> <span data-ttu-id="48e59-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span><span class="sxs-lookup"><span data-stu-id="48e59-192">If you have any feedback on what you want next, feel free to use the [Azure UserVoice site](https://feedback.azure.com/forums/270577-stream-analytics).</span></span>

<span data-ttu-id="48e59-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="48e59-193">If you are new Microsoft Azure, we invite you to try it out by signing up for a [free Azure trial account](https://azure.microsoft.com/pricing/free-trial/).</span></span> <span data-ttu-id="48e59-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="48e59-194">If you are new to Stream Analytics, then we invite you to [create your first Stream Analytics job](stream-analytics-create-a-job.md).</span></span>

<span data-ttu-id="48e59-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span><span class="sxs-lookup"><span data-stu-id="48e59-195">If you need any help or have questions, post on [MSDN](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics) or [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-stream-analytics) forums.</span></span> 

<span data-ttu-id="48e59-196">You can also see the following resources:</span><span class="sxs-lookup"><span data-stu-id="48e59-196">You can also see the following resources:</span></span>

* [<span data-ttu-id="48e59-197">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="48e59-197">Azure Functions developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="48e59-198">Azure Functions C# developer reference</span><span class="sxs-lookup"><span data-stu-id="48e59-198">Azure Functions C# developer reference</span></span>](../azure-functions/functions-reference-csharp.md)
* [<span data-ttu-id="48e59-199">Azure Functions F# developer reference</span><span class="sxs-lookup"><span data-stu-id="48e59-199">Azure Functions F# developer reference</span></span>](../azure-functions/functions-reference-fsharp.md)
* [<span data-ttu-id="48e59-200">Azure Functions NodeJS developer reference</span><span class="sxs-lookup"><span data-stu-id="48e59-200">Azure Functions NodeJS developer reference</span></span>](../azure-functions/functions-reference.md)
* [<span data-ttu-id="48e59-201">Azure Functions triggers and bindings</span><span class="sxs-lookup"><span data-stu-id="48e59-201">Azure Functions triggers and bindings</span></span>](../azure-functions/functions-triggers-bindings.md)
* [<span data-ttu-id="48e59-202">How to monitor Azure Redis Cache</span><span class="sxs-lookup"><span data-stu-id="48e59-202">How to monitor Azure Redis Cache</span></span>](../redis-cache/cache-how-to-monitor.md)

<span data-ttu-id="48e59-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span><span class="sxs-lookup"><span data-stu-id="48e59-203">To stay up-to-date on all the latest news and features, follow [@AzureStreaming](https://twitter.com/AzureStreaming) on Twitter.</span></span>

[fraud-detection]: stream-analytics-real-time-fraud-detection.md
[servicebus-getstarted]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[use-rediscache]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md
[functions-getstarted]: ../azure-functions/functions-create-first-azure-function.md










