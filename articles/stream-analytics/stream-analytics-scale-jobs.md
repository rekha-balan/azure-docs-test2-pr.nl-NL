---
title: Scale Stream Analytics jobs to increase throughput | Microsoft Docs
description: Learn how to scale Stream Analytics jobs by configuring input partitions, tuning the query definition, and setting job streaming units.
keywords: data streaming, streaming data processing, tune analytics
services: stream-analytics
documentationcenter: ''
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 588a45e7e4e42605dfe898bdf2bb8af4ecdbe6cf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551828"
---
# <a name="scale-azure-stream-analytics-jobs-to-increase-stream-data-processing-throughput"></a><span data-ttu-id="2084f-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span><span class="sxs-lookup"><span data-stu-id="2084f-104">Scale Azure Stream Analytics jobs to increase stream data processing throughput</span></span>
<span data-ttu-id="2084f-105">Learn how to tune analytics jobs and calculate *streaming units* for Stream Analytics, how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition and setting job streaming units.</span><span class="sxs-lookup"><span data-stu-id="2084f-105">Learn how to tune analytics jobs and calculate *streaming units* for Stream Analytics, how to scale Stream Analytics jobs by configuring input partitions, tuning the analytics query definition and setting job streaming units.</span></span> 

## <a name="what-are-the-parts-of-a-stream-analytics-job"></a><span data-ttu-id="2084f-106">What are the parts of a Stream Analytics job?</span><span class="sxs-lookup"><span data-stu-id="2084f-106">What are the parts of a Stream Analytics job?</span></span>
<span data-ttu-id="2084f-107">A Stream Analytics job definition includes inputs, a query, and output.</span><span class="sxs-lookup"><span data-stu-id="2084f-107">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="2084f-108">Inputs are from where the job reads the data stream, the query is used to transform the data input stream, and the output is where the job sends the job results to.</span><span class="sxs-lookup"><span data-stu-id="2084f-108">Inputs are from where the job reads the data stream, the query is used to transform the data input stream, and the output is where the job sends the job results to.</span></span>  

<span data-ttu-id="2084f-109">A job requires at least one input source for data streaming.</span><span class="sxs-lookup"><span data-stu-id="2084f-109">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="2084f-110">The data stream input source can be stored in an Azure Service Bus Event Hub or in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="2084f-110">The data stream input source can be stored in an Azure Service Bus Event Hub or in Azure Blob storage.</span></span> <span data-ttu-id="2084f-111">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="2084f-111">For more information, see [Introduction to Azure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-get-started.md).</span></span>

## <a name="configuring-streaming-units"></a><span data-ttu-id="2084f-112">Configuring streaming units</span><span class="sxs-lookup"><span data-stu-id="2084f-112">Configuring streaming units</span></span>
<span data-ttu-id="2084f-113">Streaming units (SUs) represent the resources and computing power required to execute an Azure Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="2084f-113">Streaming units (SUs) represent the resources and computing power required to execute an Azure Stream Analytics job.</span></span> <span data-ttu-id="2084f-114">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span><span class="sxs-lookup"><span data-stu-id="2084f-114">SUs provide a way to describe the relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="2084f-115">Each streaming unit corresponds to roughly 1MB/second of throughput.</span><span class="sxs-lookup"><span data-stu-id="2084f-115">Each streaming unit corresponds to roughly 1MB/second of throughput.</span></span> 

<span data-ttu-id="2084f-116">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and the query defined for the job.</span><span class="sxs-lookup"><span data-stu-id="2084f-116">Choosing how many SUs are required for a particular job depends on the partition configuration for the inputs and the query defined for the job.</span></span> <span data-ttu-id="2084f-117">You can select up to your quota in streaming units for a job by using the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="2084f-117">You can select up to your quota in streaming units for a job by using the Azure Classic Portal.</span></span> <span data-ttu-id="2084f-118">Each Azure subscription by default has a quota of up to 50 streaming units for all the analytics jobs in a specific region.</span><span class="sxs-lookup"><span data-stu-id="2084f-118">Each Azure subscription by default has a quota of up to 50 streaming units for all the analytics jobs in a specific region.</span></span> <span data-ttu-id="2084f-119">To increase streaming units for your subscriptions, contact [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="2084f-119">To increase streaming units for your subscriptions, contact [Microsoft Support](http://support.microsoft.com).</span></span>

<span data-ttu-id="2084f-120">The number of streaming units that a job can utilize depends on the partition configuration for the inputs and the query defined for the job.</span><span class="sxs-lookup"><span data-stu-id="2084f-120">The number of streaming units that a job can utilize depends on the partition configuration for the inputs and the query defined for the job.</span></span> <span data-ttu-id="2084f-121">Note also that a valid value for the stream units must be used.</span><span class="sxs-lookup"><span data-stu-id="2084f-121">Note also that a valid value for the stream units must be used.</span></span> <span data-ttu-id="2084f-122">The valid values start at 1, 3, 6 and then upwards in increments of 6, as shown below.</span><span class="sxs-lookup"><span data-stu-id="2084f-122">The valid values start at 1, 3, 6 and then upwards in increments of 6, as shown below.</span></span>

![Azure Stream Analytics Stream Units Scale][img.stream.analytics.streaming.units.scale]

<span data-ttu-id="2084f-124">This article will show you how to calculate and tune the query to increase throughput for analytics jobs.</span><span class="sxs-lookup"><span data-stu-id="2084f-124">This article will show you how to calculate and tune the query to increase throughput for analytics jobs.</span></span>

## <a name="embarrassingly-parallel-job"></a><span data-ttu-id="2084f-125">Embarrassingly parallel job</span><span class="sxs-lookup"><span data-stu-id="2084f-125">Embarrassingly parallel job</span></span>
<span data-ttu-id="2084f-126">The embarrassingly parallel job is the most scalable scenario we have in Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="2084f-126">The embarrassingly parallel job is the most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="2084f-127">It connects one partition of the input to one instance of the query to one partition of the output.</span><span class="sxs-lookup"><span data-stu-id="2084f-127">It connects one partition of the input to one instance of the query to one partition of the output.</span></span> <span data-ttu-id="2084f-128">Achieving this parallelism requires a few things:</span><span class="sxs-lookup"><span data-stu-id="2084f-128">Achieving this parallelism requires a few things:</span></span>

1. <span data-ttu-id="2084f-129">If your query logic is dependent on the same key being processed by the same query instance, then you must ensure that the events go to the same partition of your input.</span><span class="sxs-lookup"><span data-stu-id="2084f-129">If your query logic is dependent on the same key being processed by the same query instance, then you must ensure that the events go to the same partition of your input.</span></span> <span data-ttu-id="2084f-130">In the case of Event Hubs, this means that the Event Data needs to have **PartitionKey** set or you can use partitioned senders.</span><span class="sxs-lookup"><span data-stu-id="2084f-130">In the case of Event Hubs, this means that the Event Data needs to have **PartitionKey** set or you can use partitioned senders.</span></span> <span data-ttu-id="2084f-131">For Blob, this means that the events are sent to the same partition folder.</span><span class="sxs-lookup"><span data-stu-id="2084f-131">For Blob, this means that the events are sent to the same partition folder.</span></span> <span data-ttu-id="2084f-132">If your query logic does not require the same key be processed by the same query instance, then you can ignore this requirement.</span><span class="sxs-lookup"><span data-stu-id="2084f-132">If your query logic does not require the same key be processed by the same query instance, then you can ignore this requirement.</span></span> <span data-ttu-id="2084f-133">An example of this would be a simple select/project/filter query.</span><span class="sxs-lookup"><span data-stu-id="2084f-133">An example of this would be a simple select/project/filter query.</span></span>  
2. <span data-ttu-id="2084f-134">Once the data is laid out like it needs to be on the input side, we need to ensure that your query is partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-134">Once the data is laid out like it needs to be on the input side, we need to ensure that your query is partitioned.</span></span> <span data-ttu-id="2084f-135">This requires you to use **Partition By** in all of the steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-135">This requires you to use **Partition By** in all of the steps.</span></span> <span data-ttu-id="2084f-136">Multiple steps are allowed but they all must be partitioned by the same key.</span><span class="sxs-lookup"><span data-stu-id="2084f-136">Multiple steps are allowed but they all must be partitioned by the same key.</span></span> <span data-ttu-id="2084f-137">Another thing to note is that, currently, the partitioning key needs to be set to **PartitionId** to have a fully parallel job.</span><span class="sxs-lookup"><span data-stu-id="2084f-137">Another thing to note is that, currently, the partitioning key needs to be set to **PartitionId** to have a fully parallel job.</span></span>  
3. <span data-ttu-id="2084f-138">Currently only Event Hubs and Blob support partitioned output.</span><span class="sxs-lookup"><span data-stu-id="2084f-138">Currently only Event Hubs and Blob support partitioned output.</span></span> <span data-ttu-id="2084f-139">For Event Hubs output, you need to configure the **PartitionKey** field to be **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="2084f-139">For Event Hubs output, you need to configure the **PartitionKey** field to be **PartitionId**.</span></span> <span data-ttu-id="2084f-140">For Blob, you don’t have to do anything.</span><span class="sxs-lookup"><span data-stu-id="2084f-140">For Blob, you don’t have to do anything.</span></span>  
4. <span data-ttu-id="2084f-141">Another thing to note, the number of input partitions must equal the number of output partitions.</span><span class="sxs-lookup"><span data-stu-id="2084f-141">Another thing to note, the number of input partitions must equal the number of output partitions.</span></span> <span data-ttu-id="2084f-142">Blob output doesn’t currently support partitions, but this is okay because it will inherit the partitioning scheme of the upstream query.</span><span class="sxs-lookup"><span data-stu-id="2084f-142">Blob output doesn’t currently support partitions, but this is okay because it will inherit the partitioning scheme of the upstream query.</span></span>    <span data-ttu-id="2084f-143">Examples of partition values that would allow a fully parallel job:</span><span class="sxs-lookup"><span data-stu-id="2084f-143">Examples of partition values that would allow a fully parallel job:</span></span>  
   1. <span data-ttu-id="2084f-144">8 Event Hubs input partitions and 8 Event Hubs output partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-144">8 Event Hubs input partitions and 8 Event Hubs output partitions</span></span>
   2. <span data-ttu-id="2084f-145">8 Event Hubs input partitions and Blob Output</span><span class="sxs-lookup"><span data-stu-id="2084f-145">8 Event Hubs input partitions and Blob Output</span></span>  
   3. <span data-ttu-id="2084f-146">8 Blob input partitions and Blob Output</span><span class="sxs-lookup"><span data-stu-id="2084f-146">8 Blob input partitions and Blob Output</span></span>  
   4. <span data-ttu-id="2084f-147">8 Blob input partitions and 8 Event Hubs output partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-147">8 Blob input partitions and 8 Event Hubs output partitions</span></span>  

<span data-ttu-id="2084f-148">Here are some example scenarios that are embarrassingly parallel.</span><span class="sxs-lookup"><span data-stu-id="2084f-148">Here are some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="2084f-149">Simple query</span><span class="sxs-lookup"><span data-stu-id="2084f-149">Simple query</span></span>
<span data-ttu-id="2084f-150">Input – Event Hubs with 8 partitions Output – Event Hub with 8 partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-150">Input – Event Hubs with 8 partitions Output – Event Hub with 8 partitions</span></span>

<span data-ttu-id="2084f-151">**Query:**</span><span class="sxs-lookup"><span data-stu-id="2084f-151">**Query:**</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="2084f-152">This query is a simple filter and as such, we do not need to worry about partitioning the input we send to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2084f-152">This query is a simple filter and as such, we do not need to worry about partitioning the input we send to Event Hubs.</span></span> <span data-ttu-id="2084f-153">You will notice that the query has **Partition By** of **PartitionId**, so we fulfill requirement #2 from above.</span><span class="sxs-lookup"><span data-stu-id="2084f-153">You will notice that the query has **Partition By** of **PartitionId**, so we fulfill requirement #2 from above.</span></span> <span data-ttu-id="2084f-154">For the output, we need to configure the Event Hubs output in the job to have the **PartitionKey** field set to **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="2084f-154">For the output, we need to configure the Event Hubs output in the job to have the **PartitionKey** field set to **PartitionId**.</span></span> <span data-ttu-id="2084f-155">One last check, input partitions == output partitions.</span><span class="sxs-lookup"><span data-stu-id="2084f-155">One last check, input partitions == output partitions.</span></span> <span data-ttu-id="2084f-156">This topology is embarrassingly parallel.</span><span class="sxs-lookup"><span data-stu-id="2084f-156">This topology is embarrassingly parallel.</span></span>

### <a name="query-with-grouping-key"></a><span data-ttu-id="2084f-157">Query with grouping key</span><span class="sxs-lookup"><span data-stu-id="2084f-157">Query with grouping key</span></span>
<span data-ttu-id="2084f-158">Input – Event Hubs with 8 partitions Output – Blob</span><span class="sxs-lookup"><span data-stu-id="2084f-158">Input – Event Hubs with 8 partitions Output – Blob</span></span>

<span data-ttu-id="2084f-159">**Query:**</span><span class="sxs-lookup"><span data-stu-id="2084f-159">**Query:**</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="2084f-160">This query has a grouping key and as such, the same key needs to be processed by the same query instance.</span><span class="sxs-lookup"><span data-stu-id="2084f-160">This query has a grouping key and as such, the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="2084f-161">This means we need to send our events to Events Hubs in a partitioned manner.</span><span class="sxs-lookup"><span data-stu-id="2084f-161">This means we need to send our events to Events Hubs in a partitioned manner.</span></span> <span data-ttu-id="2084f-162">Which key do we care about?</span><span class="sxs-lookup"><span data-stu-id="2084f-162">Which key do we care about?</span></span> <span data-ttu-id="2084f-163">**PartitionId** is a job logic concept, the real key we care about is **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="2084f-163">**PartitionId** is a job logic concept, the real key we care about is **TollBoothId**.</span></span> <span data-ttu-id="2084f-164">This means we should set the **PartitionKey** of the event data we send to Event Hubs to be the **TollBoothId** of the event.</span><span class="sxs-lookup"><span data-stu-id="2084f-164">This means we should set the **PartitionKey** of the event data we send to Event Hubs to be the **TollBoothId** of the event.</span></span> <span data-ttu-id="2084f-165">The query has **Partition By** of **PartitionId**, so we are good there.</span><span class="sxs-lookup"><span data-stu-id="2084f-165">The query has **Partition By** of **PartitionId**, so we are good there.</span></span> <span data-ttu-id="2084f-166">For the output, since it is Blob, we do not need to worry about configuring **PartitionKey**.</span><span class="sxs-lookup"><span data-stu-id="2084f-166">For the output, since it is Blob, we do not need to worry about configuring **PartitionKey**.</span></span> <span data-ttu-id="2084f-167">For requirement #4, again, this is Blob, so we don’t need to worry about it.</span><span class="sxs-lookup"><span data-stu-id="2084f-167">For requirement #4, again, this is Blob, so we don’t need to worry about it.</span></span> <span data-ttu-id="2084f-168">This topology is embarrassingly parallel.</span><span class="sxs-lookup"><span data-stu-id="2084f-168">This topology is embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-grouping-key"></a><span data-ttu-id="2084f-169">Multi Step Query with Grouping Key</span><span class="sxs-lookup"><span data-stu-id="2084f-169">Multi Step Query with Grouping Key</span></span>
<span data-ttu-id="2084f-170">Input – Event Hub with 8 partitions Output – Event Hub with 8 partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-170">Input – Event Hub with 8 partitions Output – Event Hub with 8 partitions</span></span>

<span data-ttu-id="2084f-171">**Query:**</span><span class="sxs-lookup"><span data-stu-id="2084f-171">**Query:**</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="2084f-172">This query has a grouping key and as such, the same key needs to be processed by the same query instance.</span><span class="sxs-lookup"><span data-stu-id="2084f-172">This query has a grouping key and as such, the same key needs to be processed by the same query instance.</span></span> <span data-ttu-id="2084f-173">We can use the same strategy as the previous query.</span><span class="sxs-lookup"><span data-stu-id="2084f-173">We can use the same strategy as the previous query.</span></span> <span data-ttu-id="2084f-174">The query has multiple steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-174">The query has multiple steps.</span></span> <span data-ttu-id="2084f-175">Does each step have **Partition By** of \*\* PartitionId\*\*?</span><span class="sxs-lookup"><span data-stu-id="2084f-175">Does each step have **Partition By** of \*\* PartitionId\*\*?</span></span> <span data-ttu-id="2084f-176">Yes, so we are good.</span><span class="sxs-lookup"><span data-stu-id="2084f-176">Yes, so we are good.</span></span> <span data-ttu-id="2084f-177">For the output, we need to set the **PartitionKey** to **PartitionId** like discussed above and we can also see it has the same number of partitions as the input.</span><span class="sxs-lookup"><span data-stu-id="2084f-177">For the output, we need to set the **PartitionKey** to **PartitionId** like discussed above and we can also see it has the same number of partitions as the input.</span></span> <span data-ttu-id="2084f-178">This topology is embarrassingly parallel.</span><span class="sxs-lookup"><span data-stu-id="2084f-178">This topology is embarrassingly parallel.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="2084f-179">Example scenarios that are NOT embarrassingly parallel</span><span class="sxs-lookup"><span data-stu-id="2084f-179">Example scenarios that are NOT embarrassingly parallel</span></span>
### <a name="mismatched-partition-count"></a><span data-ttu-id="2084f-180">Mismatched Partition Count</span><span class="sxs-lookup"><span data-stu-id="2084f-180">Mismatched Partition Count</span></span>
<span data-ttu-id="2084f-181">Input – Event Hubs with 8 partitions Output – Event Hub with 32 partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-181">Input – Event Hubs with 8 partitions Output – Event Hub with 32 partitions</span></span>

<span data-ttu-id="2084f-182">It doesn’t matter what the query is in this case because the input partition count != output partition count.</span><span class="sxs-lookup"><span data-stu-id="2084f-182">It doesn’t matter what the query is in this case because the input partition count != output partition count.</span></span>

### <a name="not-using-event-hubs-or-blobs-as-output"></a><span data-ttu-id="2084f-183">Not using Event Hubs or Blobs as output</span><span class="sxs-lookup"><span data-stu-id="2084f-183">Not using Event Hubs or Blobs as output</span></span>
<span data-ttu-id="2084f-184">Input – Event Hubs with 8 partitions Output – PowerBI</span><span class="sxs-lookup"><span data-stu-id="2084f-184">Input – Event Hubs with 8 partitions Output – PowerBI</span></span>

<span data-ttu-id="2084f-185">PowerBI output doesn’t currently support partitioning.</span><span class="sxs-lookup"><span data-stu-id="2084f-185">PowerBI output doesn’t currently support partitioning.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="2084f-186">Multi Step Query with different Partition By values</span><span class="sxs-lookup"><span data-stu-id="2084f-186">Multi Step Query with different Partition By values</span></span>
<span data-ttu-id="2084f-187">Input – Event Hub with 8 partitions Output – Event Hub with 8 partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-187">Input – Event Hub with 8 partitions Output – Event Hub with 8 partitions</span></span>

<span data-ttu-id="2084f-188">**Query:**</span><span class="sxs-lookup"><span data-stu-id="2084f-188">**Query:**</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="2084f-189">As you can see, the second step uses **TollBoothId** as the partitioning key.</span><span class="sxs-lookup"><span data-stu-id="2084f-189">As you can see, the second step uses **TollBoothId** as the partitioning key.</span></span> <span data-ttu-id="2084f-190">This is not the same as the first step and will therefore require us to do a shuffle.</span><span class="sxs-lookup"><span data-stu-id="2084f-190">This is not the same as the first step and will therefore require us to do a shuffle.</span></span> 

<span data-ttu-id="2084f-191">These are some examples and counterexamples of Stream Analytics jobs that will be able to achieve an embarrassingly parallel topology and with it the potential for maximum scale.</span><span class="sxs-lookup"><span data-stu-id="2084f-191">These are some examples and counterexamples of Stream Analytics jobs that will be able to achieve an embarrassingly parallel topology and with it the potential for maximum scale.</span></span> <span data-ttu-id="2084f-192">For jobs that do not fit one of these profiles, future updates detailing how to maximally scale some of the other canonical Stream Analytics scenarios will be made.</span><span class="sxs-lookup"><span data-stu-id="2084f-192">For jobs that do not fit one of these profiles, future updates detailing how to maximally scale some of the other canonical Stream Analytics scenarios will be made.</span></span>

<span data-ttu-id="2084f-193">For now make use of the general guidance below:</span><span class="sxs-lookup"><span data-stu-id="2084f-193">For now make use of the general guidance below:</span></span>

## <a name="calculate-the-maximum-streaming-units-of-a-job"></a><span data-ttu-id="2084f-194">Calculate the maximum streaming units of a job</span><span class="sxs-lookup"><span data-stu-id="2084f-194">Calculate the maximum streaming units of a job</span></span>
<span data-ttu-id="2084f-195">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span><span class="sxs-lookup"><span data-stu-id="2084f-195">The total number of streaming units that can be used by a Stream Analytics job depends on the number of steps in the query defined for the job and the number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="2084f-196">Steps in a query</span><span class="sxs-lookup"><span data-stu-id="2084f-196">Steps in a query</span></span>
<span data-ttu-id="2084f-197">A query can have one or many steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-197">A query can have one or many steps.</span></span> <span data-ttu-id="2084f-198">Each step is a sub-query defined by using the **WITH** keyword.</span><span class="sxs-lookup"><span data-stu-id="2084f-198">Each step is a sub-query defined by using the **WITH** keyword.</span></span> <span data-ttu-id="2084f-199">The only query that is outside of the **WITH** keyword is also counted as a step, for example, the **SELECT** statement in the following query:</span><span class="sxs-lookup"><span data-stu-id="2084f-199">The only query that is outside of the **WITH** keyword is also counted as a step, for example, the **SELECT** statement in the following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="2084f-200">The previous query has two steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-200">The previous query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="2084f-201">This sample query will be explained later in the article.</span><span class="sxs-lookup"><span data-stu-id="2084f-201">This sample query will be explained later in the article.</span></span>
> 
> 

### <a name="partition-a-step"></a><span data-ttu-id="2084f-202">Partition a step</span><span class="sxs-lookup"><span data-stu-id="2084f-202">Partition a step</span></span>
<span data-ttu-id="2084f-203">Partitioning a step requires the following conditions:</span><span class="sxs-lookup"><span data-stu-id="2084f-203">Partitioning a step requires the following conditions:</span></span>

* <span data-ttu-id="2084f-204">The input source must be partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-204">The input source must be partitioned.</span></span> <span data-ttu-id="2084f-205">For more information see the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span><span class="sxs-lookup"><span data-stu-id="2084f-205">For more information see the [Event Hubs Programming Guide](../event-hubs/event-hubs-programming-guide.md).</span></span>
* <span data-ttu-id="2084f-206">The **SELECT** statement of the query must read from a partitioned input source.</span><span class="sxs-lookup"><span data-stu-id="2084f-206">The **SELECT** statement of the query must read from a partitioned input source.</span></span>
* <span data-ttu-id="2084f-207">The query within the step must have the **Partition By** keyword</span><span class="sxs-lookup"><span data-stu-id="2084f-207">The query within the step must have the **Partition By** keyword</span></span>

<span data-ttu-id="2084f-208">When a query is partitioned, the input events will be processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span><span class="sxs-lookup"><span data-stu-id="2084f-208">When a query is partitioned, the input events will be processed and aggregated in separate partition groups, and outputs events are generated for each of the groups.</span></span> <span data-ttu-id="2084f-209">If a combined aggregate is desirable, you must create a second non-partitioned step to aggregate.</span><span class="sxs-lookup"><span data-stu-id="2084f-209">If a combined aggregate is desirable, you must create a second non-partitioned step to aggregate.</span></span>

### <a name="calculate-the-max-streaming-units-for-a-job"></a><span data-ttu-id="2084f-210">Calculate the max streaming units for a job</span><span class="sxs-lookup"><span data-stu-id="2084f-210">Calculate the max streaming units for a job</span></span>
<span data-ttu-id="2084f-211">All non-partitioned steps together can scale up to six streaming units for a Stream Analytics job.</span><span class="sxs-lookup"><span data-stu-id="2084f-211">All non-partitioned steps together can scale up to six streaming units for a Stream Analytics job.</span></span> <span data-ttu-id="2084f-212">To add additional streaming units, a step must be partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-212">To add additional streaming units, a step must be partitioned.</span></span> <span data-ttu-id="2084f-213">Each partition can have six streaming units.</span><span class="sxs-lookup"><span data-stu-id="2084f-213">Each partition can have six streaming units.</span></span>

<table border="1">
<tr><th><span data-ttu-id="2084f-214">Query of a job</span><span class="sxs-lookup"><span data-stu-id="2084f-214">Query of a job</span></span></th><th><span data-ttu-id="2084f-215">Max streaming units for the job</span><span class="sxs-lookup"><span data-stu-id="2084f-215">Max streaming units for the job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="2084f-216">The query contains one step.</span><span class="sxs-lookup"><span data-stu-id="2084f-216">The query contains one step.</span></span></li>
<li><span data-ttu-id="2084f-217">The step is not partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-217">The step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="2084f-218">6</span><span class="sxs-lookup"><span data-stu-id="2084f-218">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="2084f-219">The input data stream is partitioned by 3.</span><span class="sxs-lookup"><span data-stu-id="2084f-219">The input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="2084f-220">The query contains one step.</span><span class="sxs-lookup"><span data-stu-id="2084f-220">The query contains one step.</span></span></li>
<li><span data-ttu-id="2084f-221">The step is partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-221">The step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="2084f-222">18</span><span class="sxs-lookup"><span data-stu-id="2084f-222">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="2084f-223">The query contains two steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-223">The query contains two steps.</span></span></li>
<li><span data-ttu-id="2084f-224">Neither of the steps is partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-224">Neither of the steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="2084f-225">6</span><span class="sxs-lookup"><span data-stu-id="2084f-225">6</span></span></td></tr>



<tr><td>
<ul>
<li><span data-ttu-id="2084f-226">The data stream input is partitioned by 3.</span><span class="sxs-lookup"><span data-stu-id="2084f-226">The data stream input is partitioned by 3.</span></span></li>
<li><span data-ttu-id="2084f-227">The query contains two steps.</span><span class="sxs-lookup"><span data-stu-id="2084f-227">The query contains two steps.</span></span> <span data-ttu-id="2084f-228">The input step is partitioned and the second step is not.</span><span class="sxs-lookup"><span data-stu-id="2084f-228">The input step is partitioned and the second step is not.</span></span></li>
<li><span data-ttu-id="2084f-229">The SELECT statement reads from the partitioned input.</span><span class="sxs-lookup"><span data-stu-id="2084f-229">The SELECT statement reads from the partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="2084f-230">24 (18 for partitioned steps + 6 for non-partitioned steps)</span><span class="sxs-lookup"><span data-stu-id="2084f-230">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scale"></a><span data-ttu-id="2084f-231">Examples of scale</span><span class="sxs-lookup"><span data-stu-id="2084f-231">Examples of scale</span></span>
<span data-ttu-id="2084f-232">The following query calculates the number of cars going through a toll station with three tollbooths within a three-minute window.</span><span class="sxs-lookup"><span data-stu-id="2084f-232">The following query calculates the number of cars going through a toll station with three tollbooths within a three-minute window.</span></span> <span data-ttu-id="2084f-233">This query can be scaled up to six streaming units.</span><span class="sxs-lookup"><span data-stu-id="2084f-233">This query can be scaled up to six streaming units.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="2084f-234">To use more streaming units for the query, both the data stream input and the query must be partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-234">To use more streaming units for the query, both the data stream input and the query must be partitioned.</span></span> <span data-ttu-id="2084f-235">Given that the data stream partition is set to 3, the following modified query can be scaled up to 18 streaming units:</span><span class="sxs-lookup"><span data-stu-id="2084f-235">Given that the data stream partition is set to 3, the following modified query can be scaled up to 18 streaming units:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="2084f-236">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span><span class="sxs-lookup"><span data-stu-id="2084f-236">When a query is partitioned, the input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="2084f-237">Output events are also generated for each of the groups.</span><span class="sxs-lookup"><span data-stu-id="2084f-237">Output events are also generated for each of the groups.</span></span> <span data-ttu-id="2084f-238">Partitioning can cause some unexpected results when the **Group-by** field is not the Partition Key in the data stream input.</span><span class="sxs-lookup"><span data-stu-id="2084f-238">Partitioning can cause some unexpected results when the **Group-by** field is not the Partition Key in the data stream input.</span></span> <span data-ttu-id="2084f-239">For example, the **TollBoothId** field in the previous sample query is not the Partition Key of Input1.</span><span class="sxs-lookup"><span data-stu-id="2084f-239">For example, the **TollBoothId** field in the previous sample query is not the Partition Key of Input1.</span></span> <span data-ttu-id="2084f-240">The data from the TollBooth #1 can be spread in multiple partitions.</span><span class="sxs-lookup"><span data-stu-id="2084f-240">The data from the TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="2084f-241">Each of the Input1 partitions will be processed separately by Stream Analytics, and multiple records of the car-pass-through count for the same tollbooth in the same tumbling window will be created.</span><span class="sxs-lookup"><span data-stu-id="2084f-241">Each of the Input1 partitions will be processed separately by Stream Analytics, and multiple records of the car-pass-through count for the same tollbooth in the same tumbling window will be created.</span></span> <span data-ttu-id="2084f-242">If the input partition key can't be changed, this problem can be fixed by adding an additional non-partition step, for example:</span><span class="sxs-lookup"><span data-stu-id="2084f-242">If the input partition key can't be changed, this problem can be fixed by adding an additional non-partition step, for example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="2084f-243">This query can be scaled to 24 streaming units.</span><span class="sxs-lookup"><span data-stu-id="2084f-243">This query can be scaled to 24 streaming units.</span></span>

> [!NOTE]
> <span data-ttu-id="2084f-244">If you are joining two streams, ensure that the streams are partitioned by the partition key of the column that you do the joins, and you have the same number of partitions in both streams.</span><span class="sxs-lookup"><span data-stu-id="2084f-244">If you are joining two streams, ensure that the streams are partitioned by the partition key of the column that you do the joins, and you have the same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-job-partition"></a><span data-ttu-id="2084f-245">Configure Stream Analytics job partition</span><span class="sxs-lookup"><span data-stu-id="2084f-245">Configure Stream Analytics job partition</span></span>
<span data-ttu-id="2084f-246">**To adjust a streaming unit for a job**</span><span class="sxs-lookup"><span data-stu-id="2084f-246">**To adjust a streaming unit for a job**</span></span>

1. <span data-ttu-id="2084f-247">Sign in to the [Management portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="2084f-247">Sign in to the [Management portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="2084f-248">Click **Stream Analytics** in the left pane.</span><span class="sxs-lookup"><span data-stu-id="2084f-248">Click **Stream Analytics** in the left pane.</span></span>
3. <span data-ttu-id="2084f-249">Click the Stream Analytics job that you want to scale.</span><span class="sxs-lookup"><span data-stu-id="2084f-249">Click the Stream Analytics job that you want to scale.</span></span>
4. <span data-ttu-id="2084f-250">Click **SCALE** at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="2084f-250">Click **SCALE** at the top of the page.</span></span>

![Azure Stream Analytics Stream Units Scale][img.stream.analytics.streaming.units.scale]

<span data-ttu-id="2084f-252">In the Azure Portal, Scale settings can be accessed under Settings:</span><span class="sxs-lookup"><span data-stu-id="2084f-252">In the Azure Portal, Scale settings can be accessed under Settings:</span></span>

![Azure Portal Stream Analytics job configuration][img.stream.analytics.preview.portal.settings.scale]

## <a name="monitor-job-performance"></a><span data-ttu-id="2084f-254">Monitor job performance</span><span class="sxs-lookup"><span data-stu-id="2084f-254">Monitor job performance</span></span>
<span data-ttu-id="2084f-255">Using the management portal, you can track the throughput of a job in Events/second:</span><span class="sxs-lookup"><span data-stu-id="2084f-255">Using the management portal, you can track the throughput of a job in Events/second:</span></span>

![Azure Stream Analytics monitor jobs][img.stream.analytics.monitor.job]

<span data-ttu-id="2084f-257">Calculate the expected throughput of the workload in Events/second.</span><span class="sxs-lookup"><span data-stu-id="2084f-257">Calculate the expected throughput of the workload in Events/second.</span></span> <span data-ttu-id="2084f-258">If the throughput is less than expected, tune the input partition, tune the query, and add additional streaming units to your job.</span><span class="sxs-lookup"><span data-stu-id="2084f-258">If the throughput is less than expected, tune the input partition, tune the query, and add additional streaming units to your job.</span></span>

## <a name="stream-analytics-throughput-at-scale---raspberry-pi-scenario"></a><span data-ttu-id="2084f-259">Stream Analytics Throughput at scale - Raspberry Pi scenario</span><span class="sxs-lookup"><span data-stu-id="2084f-259">Stream Analytics Throughput at scale - Raspberry Pi scenario</span></span>
<span data-ttu-id="2084f-260">To understand how stream analytics jobs scale in a typical scenario in terms of processing throughput across multiple Streaming Units, here is an experiment that sends sensor data (clients) into Event Hub, processes it and sends alert or statistics as an output to another Event Hub.</span><span class="sxs-lookup"><span data-stu-id="2084f-260">To understand how stream analytics jobs scale in a typical scenario in terms of processing throughput across multiple Streaming Units, here is an experiment that sends sensor data (clients) into Event Hub, processes it and sends alert or statistics as an output to another Event Hub.</span></span>

<span data-ttu-id="2084f-261">The client is sending synthesized sensor data to Event Hubs in JSON format to Stream Analytics and the data output is also in JSON format.</span><span class="sxs-lookup"><span data-stu-id="2084f-261">The client is sending synthesized sensor data to Event Hubs in JSON format to Stream Analytics and the data output is also in JSON format.</span></span>  <span data-ttu-id="2084f-262">Here is how the sample data would look like–</span><span class="sxs-lookup"><span data-stu-id="2084f-262">Here is how the sample data would look like–</span></span>  

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="2084f-263">Query: “Send an alert when the light is switched off”</span><span class="sxs-lookup"><span data-stu-id="2084f-263">Query: “Send an alert when the light is switched off”</span></span>  

    SELECT AVG(lght),
     “LightOff” as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

<span data-ttu-id="2084f-264">Measuring Throughput: Throughput in this context is the amount of input data processed by Stream Analytics in a fixed amount of time (10 minutes).</span><span class="sxs-lookup"><span data-stu-id="2084f-264">Measuring Throughput: Throughput in this context is the amount of input data processed by Stream Analytics in a fixed amount of time (10 minutes).</span></span> <span data-ttu-id="2084f-265">To achieve best processing throughput for the input data, both the data stream input and the query must be partitioned.</span><span class="sxs-lookup"><span data-stu-id="2084f-265">To achieve best processing throughput for the input data, both the data stream input and the query must be partitioned.</span></span> <span data-ttu-id="2084f-266">Also **COUNT()** is included in the query to measure how many input events were processed.</span><span class="sxs-lookup"><span data-stu-id="2084f-266">Also **COUNT()** is included in the query to measure how many input events were processed.</span></span> <span data-ttu-id="2084f-267">To ensure the job is not simply waiting for input events to come, each partition of the Input Event Hub was preloaded with sufficient input data (about 300MB).</span><span class="sxs-lookup"><span data-stu-id="2084f-267">To ensure the job is not simply waiting for input events to come, each partition of the Input Event Hub was preloaded with sufficient input data (about 300MB).</span></span>  

<span data-ttu-id="2084f-268">Below are the results with increasing number of Streaming units and corresponding Partition counts in Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="2084f-268">Below are the results with increasing number of Streaming units and corresponding Partition counts in Event Hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="2084f-269">Input Partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-269">Input Partitions</span></span></th><th><span data-ttu-id="2084f-270">Output Partitions</span><span class="sxs-lookup"><span data-stu-id="2084f-270">Output Partitions</span></span></th><th><span data-ttu-id="2084f-271">Streaming Units</span><span class="sxs-lookup"><span data-stu-id="2084f-271">Streaming Units</span></span></th><th><span data-ttu-id="2084f-272">Sustained Throughput</span><span class="sxs-lookup"><span data-stu-id="2084f-272">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="2084f-273">12</span><span class="sxs-lookup"><span data-stu-id="2084f-273">12</span></span></td>
<td><span data-ttu-id="2084f-274">12</span><span class="sxs-lookup"><span data-stu-id="2084f-274">12</span></span></td>
<td><span data-ttu-id="2084f-275">6</span><span class="sxs-lookup"><span data-stu-id="2084f-275">6</span></span></td>
<td><span data-ttu-id="2084f-276">4.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-276">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="2084f-277">12</span><span class="sxs-lookup"><span data-stu-id="2084f-277">12</span></span></td>
<td><span data-ttu-id="2084f-278">12</span><span class="sxs-lookup"><span data-stu-id="2084f-278">12</span></span></td>
<td><span data-ttu-id="2084f-279">12</span><span class="sxs-lookup"><span data-stu-id="2084f-279">12</span></span></td>
<td><span data-ttu-id="2084f-280">8.06 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-280">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="2084f-281">48</span><span class="sxs-lookup"><span data-stu-id="2084f-281">48</span></span></td>
<td><span data-ttu-id="2084f-282">48</span><span class="sxs-lookup"><span data-stu-id="2084f-282">48</span></span></td>
<td><span data-ttu-id="2084f-283">48</span><span class="sxs-lookup"><span data-stu-id="2084f-283">48</span></span></td>
<td><span data-ttu-id="2084f-284">38.32 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-284">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="2084f-285">192</span><span class="sxs-lookup"><span data-stu-id="2084f-285">192</span></span></td>
<td><span data-ttu-id="2084f-286">192</span><span class="sxs-lookup"><span data-stu-id="2084f-286">192</span></span></td>
<td><span data-ttu-id="2084f-287">192</span><span class="sxs-lookup"><span data-stu-id="2084f-287">192</span></span></td>
<td><span data-ttu-id="2084f-288">172.67 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-288">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="2084f-289">480</span><span class="sxs-lookup"><span data-stu-id="2084f-289">480</span></span></td>
<td><span data-ttu-id="2084f-290">480</span><span class="sxs-lookup"><span data-stu-id="2084f-290">480</span></span></td>
<td><span data-ttu-id="2084f-291">480</span><span class="sxs-lookup"><span data-stu-id="2084f-291">480</span></span></td>
<td><span data-ttu-id="2084f-292">454.27 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-292">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="2084f-293">720</span><span class="sxs-lookup"><span data-stu-id="2084f-293">720</span></span></td>
<td><span data-ttu-id="2084f-294">720</span><span class="sxs-lookup"><span data-stu-id="2084f-294">720</span></span></td>
<td><span data-ttu-id="2084f-295">720</span><span class="sxs-lookup"><span data-stu-id="2084f-295">720</span></span></td>
<td><span data-ttu-id="2084f-296">609.69 MB/s</span><span class="sxs-lookup"><span data-stu-id="2084f-296">609.69 MB/s</span></span></td>
</tr>
</table>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="2084f-298">Get help</span><span class="sxs-lookup"><span data-stu-id="2084f-298">Get help</span></span>
<span data-ttu-id="2084f-299">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2084f-299">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2084f-300">Next steps</span><span class="sxs-lookup"><span data-stu-id="2084f-300">Next steps</span></span>
* [<span data-ttu-id="2084f-301">Introduction to Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2084f-301">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2084f-302">Get started using Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2084f-302">Get started using Azure Stream Analytics</span></span>](stream-analytics-get-started.md)
* [<span data-ttu-id="2084f-303">Azure Stream Analytics Query Language Reference</span><span class="sxs-lookup"><span data-stu-id="2084f-303">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2084f-304">Azure Stream Analytics Management REST API Reference</span><span class="sxs-lookup"><span data-stu-id="2084f-304">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor.png
[img.stream.analytics.configure.scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/stream-analytics/media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings.png

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-get-started.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301






