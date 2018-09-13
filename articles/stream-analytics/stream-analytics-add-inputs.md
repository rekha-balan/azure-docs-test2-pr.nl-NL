---
title: Add a data input to your Stream Analytics jobs | Microsoft Docs
description: Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blog storage.
keywords: data input, streaming data
documentationcenter: ''
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: fcba3f3c1d67dee4a57c9f610bcdeb493e795bea
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44663091"
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="df532-104">Add a streaming data input or reference data to a Stream Analytics job</span><span class="sxs-lookup"><span data-stu-id="df532-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="df532-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span><span class="sxs-lookup"><span data-stu-id="df532-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="df532-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span><span class="sxs-lookup"><span data-stu-id="df532-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="df532-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span><span class="sxs-lookup"><span data-stu-id="df532-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="df532-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span><span class="sxs-lookup"><span data-stu-id="df532-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="df532-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="df532-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="df532-110">Data input: Streaming data and reference data</span><span class="sxs-lookup"><span data-stu-id="df532-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="df532-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span><span class="sxs-lookup"><span data-stu-id="df532-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="df532-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span><span class="sxs-lookup"><span data-stu-id="df532-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="df532-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span><span class="sxs-lookup"><span data-stu-id="df532-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="df532-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span><span class="sxs-lookup"><span data-stu-id="df532-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="df532-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span><span class="sxs-lookup"><span data-stu-id="df532-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="df532-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span><span class="sxs-lookup"><span data-stu-id="df532-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="df532-117">As opposed to data in motion, this data is static or slowing changing.</span><span class="sxs-lookup"><span data-stu-id="df532-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="df532-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span><span class="sxs-lookup"><span data-stu-id="df532-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="df532-119">Azure Blob storage is currently the only supported input source for reference data.</span><span class="sxs-lookup"><span data-stu-id="df532-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="df532-120">To add an input to your Stream Analytics job:</span><span class="sxs-lookup"><span data-stu-id="df532-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="df532-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="df532-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Azure classic portal - add an input.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="df532-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="df532-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Azure portal - Add data input.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="df532-125">Specify the type of the input: either **Data stream** or **Reference data**.</span><span class="sxs-lookup"><span data-stu-id="df532-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Add the correct data input, streamed or reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Add the correct data input, streamed or reference](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="df532-128">If creating a Data Stream input, specify the source type for the input.</span><span class="sxs-lookup"><span data-stu-id="df532-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="df532-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span><span class="sxs-lookup"><span data-stu-id="df532-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Add data stream data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Add data stream data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="df532-132">Provide a friendly name for this input in the Input Alias box.</span><span class="sxs-lookup"><span data-stu-id="df532-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="df532-133">This name will be used in your job's query later on to refer to the input.</span><span class="sxs-lookup"><span data-stu-id="df532-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="df532-134">Fill in the rest of the required connection properties to connect to your data source.</span><span class="sxs-lookup"><span data-stu-id="df532-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="df532-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="df532-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Add event hub data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="df532-137">Specify the serialization settings for the input data:</span><span class="sxs-lookup"><span data-stu-id="df532-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="df532-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span><span class="sxs-lookup"><span data-stu-id="df532-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="df532-139">Supported serialization formats are JSON, CSV, and Avro.</span><span class="sxs-lookup"><span data-stu-id="df532-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="df532-140">Verify the **Encoding** for the data.</span><span class="sxs-lookup"><span data-stu-id="df532-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="df532-141">UTF-8 is the only supported encoding format at this time.</span><span class="sxs-lookup"><span data-stu-id="df532-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Data serialization settings for the data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Data serialization settings for the data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="df532-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span><span class="sxs-lookup"><span data-stu-id="df532-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="df532-145">You can view the status of the Test Connection operation in the Notification hub.</span><span class="sxs-lookup"><span data-stu-id="df532-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Test connection of the streaming data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Test connection of the streaming data input](https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="df532-148">Get help with streaming data inputs</span><span class="sxs-lookup"><span data-stu-id="df532-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="df532-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="df532-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="df532-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="df532-150">Next steps</span></span>
* [<span data-ttu-id="df532-151">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="df532-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="df532-152">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="df532-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="df532-153">Scale Azure Stream Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="df532-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="df532-154">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="df532-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="df532-155">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="df532-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)












