---
title: IoT real-time data streams and Azure Stream Analytics | Microsoft Docs
description: IoT sensor tags and data streams with stream analytics and real-time data processing
keywords: iot solution, get started with iot
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 3e829055-75ed-469f-91f5-f0dc95046bdb
ms.service: stream-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8be5db28a0031c1b90bc3d146f45d913d65984ac
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563349"
---
# <a name="get-started-with-azure-stream-analytics-to-process-data-from-iot-devices"></a><span data-ttu-id="e4d55-104">Get started with Azure Stream Analytics to process data from IoT devices</span><span class="sxs-lookup"><span data-stu-id="e4d55-104">Get started with Azure Stream Analytics to process data from IoT devices</span></span>
<span data-ttu-id="e4d55-105">In this tutorial, you will learn how to create stream-processing logic to gather data from Internet of Things (IoT) devices.</span><span class="sxs-lookup"><span data-stu-id="e4d55-105">In this tutorial, you will learn how to create stream-processing logic to gather data from Internet of Things (IoT) devices.</span></span> <span data-ttu-id="e4d55-106">We will use a real-world, Internet of Things (IoT) use case to demonstrate how to build your solution quickly and economically.</span><span class="sxs-lookup"><span data-stu-id="e4d55-106">We will use a real-world, Internet of Things (IoT) use case to demonstrate how to build your solution quickly and economically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4d55-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4d55-107">Prerequisites</span></span>
* [<span data-ttu-id="e4d55-108">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e4d55-108">Azure subscription</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* <span data-ttu-id="e4d55-109">Sample query and data files downloadable from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span><span class="sxs-lookup"><span data-stu-id="e4d55-109">Sample query and data files downloadable from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot)</span></span>

## <a name="scenario"></a><span data-ttu-id="e4d55-110">Scenario</span><span class="sxs-lookup"><span data-stu-id="e4d55-110">Scenario</span></span>
<span data-ttu-id="e4d55-111">Contoso, which is a company in the industrial automation space, has completely automated its manufacturing process.</span><span class="sxs-lookup"><span data-stu-id="e4d55-111">Contoso, which is a company in the industrial automation space, has completely automated its manufacturing process.</span></span> <span data-ttu-id="e4d55-112">The machinery in this plant has sensors that are capable of emitting streams of data in real time.</span><span class="sxs-lookup"><span data-stu-id="e4d55-112">The machinery in this plant has sensors that are capable of emitting streams of data in real time.</span></span> <span data-ttu-id="e4d55-113">In this scenario, a production floor manager wants to have real-time insights from the sensor data to look for patterns and take actions on them.</span><span class="sxs-lookup"><span data-stu-id="e4d55-113">In this scenario, a production floor manager wants to have real-time insights from the sensor data to look for patterns and take actions on them.</span></span> <span data-ttu-id="e4d55-114">We will use the Stream Analytics Query Language (SAQL) over the sensor data to find interesting patterns from the incoming stream of data.</span><span class="sxs-lookup"><span data-stu-id="e4d55-114">We will use the Stream Analytics Query Language (SAQL) over the sensor data to find interesting patterns from the incoming stream of data.</span></span>

<span data-ttu-id="e4d55-115">Here data is being generated from a Texas Instruments sensor tag device.</span><span class="sxs-lookup"><span data-stu-id="e4d55-115">Here data is being generated from a Texas Instruments sensor tag device.</span></span>

![Texas Instruments sensor tag](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-01.jpg)

<span data-ttu-id="e4d55-117">The payload of the data is in JSON format and looks like the following:</span><span class="sxs-lookup"><span data-stu-id="e4d55-117">The payload of the data is in JSON format and looks like the following:</span></span>

    {
        "time": "2016-01-26T20:47:53.0000000",  
        "dspl": "sensorE",  
        "temp": 123,  
        "hmdt": 34  
    }  

<span data-ttu-id="e4d55-118">In a real-world scenario, you could have hundreds of these sensors generating events as a stream.</span><span class="sxs-lookup"><span data-stu-id="e4d55-118">In a real-world scenario, you could have hundreds of these sensors generating events as a stream.</span></span> <span data-ttu-id="e4d55-119">Ideally, a gateway device would run code to push these events to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/).</span><span class="sxs-lookup"><span data-stu-id="e4d55-119">Ideally, a gateway device would run code to push these events to [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) or [Azure IoT Hubs](https://azure.microsoft.com/services/iot-hub/).</span></span> <span data-ttu-id="e4d55-120">Your Stream Analytics job would ingest these events from Event Hubs and run real-time analytics queries against the streams.</span><span class="sxs-lookup"><span data-stu-id="e4d55-120">Your Stream Analytics job would ingest these events from Event Hubs and run real-time analytics queries against the streams.</span></span> <span data-ttu-id="e4d55-121">Then, you could send the results to one of the [supported outputs](stream-analytics-define-outputs.md).</span><span class="sxs-lookup"><span data-stu-id="e4d55-121">Then, you could send the results to one of the [supported outputs](stream-analytics-define-outputs.md).</span></span>

<span data-ttu-id="e4d55-122">For ease of use, this getting started guide provides a sample data file, which was captured from real sensor tag devices.</span><span class="sxs-lookup"><span data-stu-id="e4d55-122">For ease of use, this getting started guide provides a sample data file, which was captured from real sensor tag devices.</span></span> <span data-ttu-id="e4d55-123">You can run queries on the sample data and see results.</span><span class="sxs-lookup"><span data-stu-id="e4d55-123">You can run queries on the sample data and see results.</span></span> <span data-ttu-id="e4d55-124">In subsequent tutorials, you will learn how to connect your job to inputs and outputs and deploy them to the Azure service.</span><span class="sxs-lookup"><span data-stu-id="e4d55-124">In subsequent tutorials, you will learn how to connect your job to inputs and outputs and deploy them to the Azure service.</span></span>

## <a name="create-a-stream-analytics-job"></a><span data-ttu-id="e4d55-125">Create a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="e4d55-125">Create a Stream Analytics job</span></span>
1. <span data-ttu-id="e4d55-126">In the [Azure portal](http://portal.azure.com), click the plus sign and then type **STREAM ANALYTICS** in the text window to the right.</span><span class="sxs-lookup"><span data-stu-id="e4d55-126">In the [Azure portal](http://portal.azure.com), click the plus sign and then type **STREAM ANALYTICS** in the text window to the right.</span></span> <span data-ttu-id="e4d55-127">Then select **Stream Analytics job** in the results list.</span><span class="sxs-lookup"><span data-stu-id="e4d55-127">Then select **Stream Analytics job** in the results list.</span></span>
   
    ![Create a new Stream Analytics job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-02.png)
2. <span data-ttu-id="e4d55-129">Enter a unique job name and verify the subscription is the correct one for your job.</span><span class="sxs-lookup"><span data-stu-id="e4d55-129">Enter a unique job name and verify the subscription is the correct one for your job.</span></span> <span data-ttu-id="e4d55-130">Then either create a new resource group or select an existing one on your subscription.</span><span class="sxs-lookup"><span data-stu-id="e4d55-130">Then either create a new resource group or select an existing one on your subscription.</span></span>
3. <span data-ttu-id="e4d55-131">Then select a location for your job.</span><span class="sxs-lookup"><span data-stu-id="e4d55-131">Then select a location for your job.</span></span> <span data-ttu-id="e4d55-132">For speed of processing and reduction of cost in data transfer selecting the same location as the resource group and intended storage account is recommended.</span><span class="sxs-lookup"><span data-stu-id="e4d55-132">For speed of processing and reduction of cost in data transfer selecting the same location as the resource group and intended storage account is recommended.</span></span>
   
    ![Create a new Stream Analytics job details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03.png)
   
   > [!NOTE]
   > <span data-ttu-id="e4d55-134">You should create this storage account only once per region.</span><span class="sxs-lookup"><span data-stu-id="e4d55-134">You should create this storage account only once per region.</span></span> <span data-ttu-id="e4d55-135">This storage will be shared across all Stream Analytics jobs that are created in that region.</span><span class="sxs-lookup"><span data-stu-id="e4d55-135">This storage will be shared across all Stream Analytics jobs that are created in that region.</span></span>
   > 
   > 
4. <span data-ttu-id="e4d55-136">Check the box to place your job on your dashboard and then click **CREATE**.</span><span class="sxs-lookup"><span data-stu-id="e4d55-136">Check the box to place your job on your dashboard and then click **CREATE**.</span></span>
   
    ![job creation in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03a.png)
5. <span data-ttu-id="e4d55-138">You should see a 'Deployment started...' displayed in the top right of your browser window.</span><span class="sxs-lookup"><span data-stu-id="e4d55-138">You should see a 'Deployment started...' displayed in the top right of your browser window.</span></span> <span data-ttu-id="e4d55-139">Soon it will change to a completed window as shown below.</span><span class="sxs-lookup"><span data-stu-id="e4d55-139">Soon it will change to a completed window as shown below.</span></span>
   
    ![job creation in progress](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-03b.png)

### <a name="create-an-azure-stream-analytics-query"></a><span data-ttu-id="e4d55-141">Create an Azure Stream Analytics query</span><span class="sxs-lookup"><span data-stu-id="e4d55-141">Create an Azure Stream Analytics query</span></span>
<span data-ttu-id="e4d55-142">After your job is created it's time to open it and build a query.</span><span class="sxs-lookup"><span data-stu-id="e4d55-142">After your job is created it's time to open it and build a query.</span></span> <span data-ttu-id="e4d55-143">You can easily access your job by clicking the tile for it.</span><span class="sxs-lookup"><span data-stu-id="e4d55-143">You can easily access your job by clicking the tile for it.</span></span>

![Job tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-04.png)

<span data-ttu-id="e4d55-145">In the **Job Topology** pane click the **QUERY** box to go to the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="e4d55-145">In the **Job Topology** pane click the **QUERY** box to go to the Query Editor.</span></span> <span data-ttu-id="e4d55-146">The **QUERY** editor allows you to enter a T-SQL query that performs the transformation over the incoming event data.</span><span class="sxs-lookup"><span data-stu-id="e4d55-146">The **QUERY** editor allows you to enter a T-SQL query that performs the transformation over the incoming event data.</span></span>

![Query box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-05.png)

### <a name="query-archive-your-raw-data"></a><span data-ttu-id="e4d55-148">Query: Archive your raw data</span><span class="sxs-lookup"><span data-stu-id="e4d55-148">Query: Archive your raw data</span></span>
<span data-ttu-id="e4d55-149">The simplest form of query is a pass-through query that archives all input data to its designated output.</span><span class="sxs-lookup"><span data-stu-id="e4d55-149">The simplest form of query is a pass-through query that archives all input data to its designated output.</span></span> <span data-ttu-id="e4d55-150">Download the sample data file from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) to a location on your computer.</span><span class="sxs-lookup"><span data-stu-id="e4d55-150">Download the sample data file from [GitHub](https://aka.ms/azure-stream-analytics-get-started-iot) to a location on your computer.</span></span> 

1. <span data-ttu-id="e4d55-151">Paste the query from the PassThrough.txt file.</span><span class="sxs-lookup"><span data-stu-id="e4d55-151">Paste the query from the PassThrough.txt file.</span></span> 
   
    ![Test input stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06.png)
2. <span data-ttu-id="e4d55-153">Click the three dots next to your input and select **Upload sample data from file** box.</span><span class="sxs-lookup"><span data-stu-id="e4d55-153">Click the three dots next to your input and select **Upload sample data from file** box.</span></span>
   
    ![Test input stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06a.png)
3. <span data-ttu-id="e4d55-155">A pane opens on the right as a result, in it select the HelloWorldASA-InputStream.json data file from your downloaded location and click **OK** at the bottom of the pane.</span><span class="sxs-lookup"><span data-stu-id="e4d55-155">A pane opens on the right as a result, in it select the HelloWorldASA-InputStream.json data file from your downloaded location and click **OK** at the bottom of the pane.</span></span>
   
    ![Test input stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-06b.png)
4. <span data-ttu-id="e4d55-157">Then click the **Test** gear in the top left area of the window and process your test query against the sample dataset.</span><span class="sxs-lookup"><span data-stu-id="e4d55-157">Then click the **Test** gear in the top left area of the window and process your test query against the sample dataset.</span></span> <span data-ttu-id="e4d55-158">A results window will open below your query as the processing is complete.</span><span class="sxs-lookup"><span data-stu-id="e4d55-158">A results window will open below your query as the processing is complete.</span></span>
   
    ![Test results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-07.png)

### <a name="query-filter-the-data-based-on-a-condition"></a><span data-ttu-id="e4d55-160">Query: Filter the data based on a condition</span><span class="sxs-lookup"><span data-stu-id="e4d55-160">Query: Filter the data based on a condition</span></span>
<span data-ttu-id="e4d55-161">Let’s try to filter the results based on a condition.</span><span class="sxs-lookup"><span data-stu-id="e4d55-161">Let’s try to filter the results based on a condition.</span></span> <span data-ttu-id="e4d55-162">We would like to show results for only those events that come from “sensorA.”</span><span class="sxs-lookup"><span data-stu-id="e4d55-162">We would like to show results for only those events that come from “sensorA.”</span></span> <span data-ttu-id="e4d55-163">The query is in the Filtering.txt file.</span><span class="sxs-lookup"><span data-stu-id="e4d55-163">The query is in the Filtering.txt file.</span></span>

![Filtering a data stream](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-08.png)

<span data-ttu-id="e4d55-165">Note that the case-sensitive query compares a string value.</span><span class="sxs-lookup"><span data-stu-id="e4d55-165">Note that the case-sensitive query compares a string value.</span></span> <span data-ttu-id="e4d55-166">Click the **Test** gear again to execute the query.</span><span class="sxs-lookup"><span data-stu-id="e4d55-166">Click the **Test** gear again to execute the query.</span></span> <span data-ttu-id="e4d55-167">The query should return 389 rows out of 1860 events.</span><span class="sxs-lookup"><span data-stu-id="e4d55-167">The query should return 389 rows out of 1860 events.</span></span>

![Second output results from query test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-09.png)

### <a name="query-alert-to-trigger-a-business-workflow"></a><span data-ttu-id="e4d55-169">Query: Alert to trigger a business workflow</span><span class="sxs-lookup"><span data-stu-id="e4d55-169">Query: Alert to trigger a business workflow</span></span>
<span data-ttu-id="e4d55-170">Let's make our query more detailed.</span><span class="sxs-lookup"><span data-stu-id="e4d55-170">Let's make our query more detailed.</span></span> <span data-ttu-id="e4d55-171">For every type of sensor, we want to monitor average temperature per 30-second window and display results only if the average temperature is above 100 degrees.</span><span class="sxs-lookup"><span data-stu-id="e4d55-171">For every type of sensor, we want to monitor average temperature per 30-second window and display results only if the average temperature is above 100 degrees.</span></span> <span data-ttu-id="e4d55-172">We will write the following query and then click **Test** to see the results.</span><span class="sxs-lookup"><span data-stu-id="e4d55-172">We will write the following query and then click **Test** to see the results.</span></span> <span data-ttu-id="e4d55-173">The query is in the ThresholdAlerting.txt file.</span><span class="sxs-lookup"><span data-stu-id="e4d55-173">The query is in the ThresholdAlerting.txt file.</span></span>

![30-second filter query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-10.png)

<span data-ttu-id="e4d55-175">You should now see results that contain only 245 rows and names of sensors where the average temperate is greater than 100.</span><span class="sxs-lookup"><span data-stu-id="e4d55-175">You should now see results that contain only 245 rows and names of sensors where the average temperate is greater than 100.</span></span> <span data-ttu-id="e4d55-176">This query groups the stream of events by **dspl**, which is the sensor name, over a **Tumbling Window** of 30 seconds.</span><span class="sxs-lookup"><span data-stu-id="e4d55-176">This query groups the stream of events by **dspl**, which is the sensor name, over a **Tumbling Window** of 30 seconds.</span></span> <span data-ttu-id="e4d55-177">Temporal queries must state how we want time to progress.</span><span class="sxs-lookup"><span data-stu-id="e4d55-177">Temporal queries must state how we want time to progress.</span></span> <span data-ttu-id="e4d55-178">By using the **TIMESTAMP BY** clause, we have specified the **OUTPUTTIME** column to associate times with all temporal calculations.</span><span class="sxs-lookup"><span data-stu-id="e4d55-178">By using the **TIMESTAMP BY** clause, we have specified the **OUTPUTTIME** column to associate times with all temporal calculations.</span></span> <span data-ttu-id="e4d55-179">For detailed information, read the MSDN articles about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing functions](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4d55-179">For detailed information, read the MSDN articles about [Time Management](https://msdn.microsoft.com/library/azure/mt582045.aspx) and [Windowing functions](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

### <a name="query-detect-absence-of-events"></a><span data-ttu-id="e4d55-180">Query: Detect absence of events</span><span class="sxs-lookup"><span data-stu-id="e4d55-180">Query: Detect absence of events</span></span>
<span data-ttu-id="e4d55-181">How can we write a query to find a lack of input events?</span><span class="sxs-lookup"><span data-stu-id="e4d55-181">How can we write a query to find a lack of input events?</span></span> <span data-ttu-id="e4d55-182">Let’s find the last time that a sensor sent data and then did not send events for the next minute.</span><span class="sxs-lookup"><span data-stu-id="e4d55-182">Let’s find the last time that a sensor sent data and then did not send events for the next minute.</span></span> <span data-ttu-id="e4d55-183">The query is in the AbsenseOfEvent.txt file.</span><span class="sxs-lookup"><span data-stu-id="e4d55-183">The query is in the AbsenseOfEvent.txt file.</span></span>

![Detect absence of events](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-get-started-with-iot-devices/stream-analytics-get-started-with-iot-devices-11.png)

<span data-ttu-id="e4d55-185">Here we use a **LEFT OUTER** join to the same data stream (self-join).</span><span class="sxs-lookup"><span data-stu-id="e4d55-185">Here we use a **LEFT OUTER** join to the same data stream (self-join).</span></span> <span data-ttu-id="e4d55-186">For an **INNER** join, a result is returned only when a match is found.</span><span class="sxs-lookup"><span data-stu-id="e4d55-186">For an **INNER** join, a result is returned only when a match is found.</span></span>  <span data-ttu-id="e4d55-187">For a **LEFT OUTER** join, if an event from the left side of the join is unmatched, a row that has NULL for all the columns of the right side is returned.</span><span class="sxs-lookup"><span data-stu-id="e4d55-187">For a **LEFT OUTER** join, if an event from the left side of the join is unmatched, a row that has NULL for all the columns of the right side is returned.</span></span> <span data-ttu-id="e4d55-188">This technique is very useful to find an absence of events.</span><span class="sxs-lookup"><span data-stu-id="e4d55-188">This technique is very useful to find an absence of events.</span></span> <span data-ttu-id="e4d55-189">See our MSDN documentation for more information about [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).</span><span class="sxs-lookup"><span data-stu-id="e4d55-189">See our MSDN documentation for more information about [JOIN](https://msdn.microsoft.com/library/azure/dn835026.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="e4d55-190">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e4d55-190">Conclusion</span></span>
<span data-ttu-id="e4d55-191">The purpose of this tutorial is to demonstrate how to write different Stream Analytics Query Language queries and see results in the browser.</span><span class="sxs-lookup"><span data-stu-id="e4d55-191">The purpose of this tutorial is to demonstrate how to write different Stream Analytics Query Language queries and see results in the browser.</span></span> <span data-ttu-id="e4d55-192">However, this is just getting started.</span><span class="sxs-lookup"><span data-stu-id="e4d55-192">However, this is just getting started.</span></span> <span data-ttu-id="e4d55-193">You can do so much more with Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="e4d55-193">You can do so much more with Stream Analytics.</span></span> <span data-ttu-id="e4d55-194">Stream Analytics supports a variety of inputs and outputs and can even use functions in Azure Machine Learning to make it a robust tool for analyzing data streams.</span><span class="sxs-lookup"><span data-stu-id="e4d55-194">Stream Analytics supports a variety of inputs and outputs and can even use functions in Azure Machine Learning to make it a robust tool for analyzing data streams.</span></span> <span data-ttu-id="e4d55-195">You can start to explore more about Stream Analytics by using our [learning map](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="e4d55-195">You can start to explore more about Stream Analytics by using our [learning map](https://azure.microsoft.com/documentation/learning-paths/stream-analytics/).</span></span> <span data-ttu-id="e4d55-196">For more information about how to write queries, read the article about [common query patterns](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="e4d55-196">For more information about how to write queries, read the article about [common query patterns](stream-analytics-stream-analytics-query-patterns.md).</span></span>
















