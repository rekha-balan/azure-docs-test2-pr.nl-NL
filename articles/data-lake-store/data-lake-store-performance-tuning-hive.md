---
title: Azure Data Lake Store Hive Performance Tuning Guidelines | Microsoft Docs
description: Azure Data Lake Store Hive Performance Tuning Guidelines
services: data-lake-store
documentationcenter: ''
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: e10bf8f7cbae2b81d22823ff74fe652c6bcb2da3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554269"
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="8bbe8-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="8bbe8-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="8bbe8-104">The default settings have been set to provide good performance across many different use cases.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-104">The default settings have been set to provide good performance across many different use cases.</span></span>  <span data-ttu-id="8bbe8-105">For I/O intensive queries, Hive can be tuned to get better performance with ADLS.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-105">For I/O intensive queries, Hive can be tuned to get better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8bbe8-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8bbe8-106">Prerequisites</span></span>

* <span data-ttu-id="8bbe8-107">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-107">**An Azure subscription**.</span></span> <span data-ttu-id="8bbe8-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8bbe8-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8bbe8-109">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="8bbe8-110">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8bbe8-110">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="8bbe8-111">**Azure HDInsight cluster** with access to a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-111">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="8bbe8-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8bbe8-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="8bbe8-113">Make sure you enable Remote Desktop for the cluster.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-113">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="8bbe8-114">**Running Hive on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="8bbe8-115">To learn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="8bbe8-115">To learn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="8bbe8-116">**Performance tuning guidelines on ADLS**.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="8bbe8-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="8bbe8-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="8bbe8-118">Parameters</span><span class="sxs-lookup"><span data-stu-id="8bbe8-118">Parameters</span></span>

<span data-ttu-id="8bbe8-119">Here are the most important settings to tune for improved ADLS performance:</span><span class="sxs-lookup"><span data-stu-id="8bbe8-119">Here are the most important settings to tune for improved ADLS performance:</span></span>

* <span data-ttu-id="8bbe8-120">**hive.tez.container.size** – the amount of memory used by each tasks</span><span class="sxs-lookup"><span data-stu-id="8bbe8-120">**hive.tez.container.size** – the amount of memory used by each tasks</span></span>

* <span data-ttu-id="8bbe8-121">**tez.grouping.min-size** – minimum size of each mapper</span><span class="sxs-lookup"><span data-stu-id="8bbe8-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="8bbe8-122">**tez.grouping.max-size** – maximum size of each mapper</span><span class="sxs-lookup"><span data-stu-id="8bbe8-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="8bbe8-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span><span class="sxs-lookup"><span data-stu-id="8bbe8-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="8bbe8-124">**hive.tez.container.size** - The container size determines how much memory is available for each task.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-124">**hive.tez.container.size** - The container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="8bbe8-125">This is the main input for controlling the concurrency in Hive.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-125">This is the main input for controlling the concurrency in Hive.</span></span>  

<span data-ttu-id="8bbe8-126">**tez.grouping.min-size** – This parameter allows you to set the minimum size of each mapper.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-126">**tez.grouping.min-size** – This parameter allows you to set the minimum size of each mapper.</span></span>  <span data-ttu-id="8bbe8-127">If the number of mappers that Tez chooses is smaller than the value of this parameter, then Tez will use the value set here.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-127">If the number of mappers that Tez chooses is smaller than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="8bbe8-128">**tez.grouping.max-size** – The parameter allows you to set the maximum size of each mapper.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-128">**tez.grouping.max-size** – The parameter allows you to set the maximum size of each mapper.</span></span>  <span data-ttu-id="8bbe8-129">If the number of mappers that Tez chooses is larger than the value of this parameter, then Tez will use the value set here.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-129">If the number of mappers that Tez chooses is larger than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="8bbe8-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets the size of each reducer.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets the size of each reducer.</span></span>  <span data-ttu-id="8bbe8-131">By default, each reducer is 256MB.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="8bbe8-132">Guidance</span><span class="sxs-lookup"><span data-stu-id="8bbe8-132">Guidance</span></span>

<span data-ttu-id="8bbe8-133">**Set hive.exec.reducer.bytes.per.reducer** – The default value works well when the data is uncompressed.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-133">**Set hive.exec.reducer.bytes.per.reducer** – The default value works well when the data is uncompressed.</span></span>  <span data-ttu-id="8bbe8-134">For data that is compressed, you should reduce the size of the reducer.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-134">For data that is compressed, you should reduce the size of the reducer.</span></span>  

<span data-ttu-id="8bbe8-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="8bbe8-136">For additional information on setting the appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span><span class="sxs-lookup"><span data-stu-id="8bbe8-136">For additional information on setting the appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="8bbe8-137">I/O intensive workloads can benefit from more parallelism by decreasing the Tez container size.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-137">I/O intensive workloads can benefit from more parallelism by decreasing the Tez container size.</span></span> <span data-ttu-id="8bbe8-138">This gives the user more containers which increases concurrency.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-138">This gives the user more containers which increases concurrency.</span></span>  <span data-ttu-id="8bbe8-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span><span class="sxs-lookup"><span data-stu-id="8bbe8-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="8bbe8-140">If the task does not have enough memory, you will get an out of memory exception during runtime.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-140">If the task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="8bbe8-141">If you receive out of memory exceptions, then you should increase the memory.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-141">If you receive out of memory exceptions, then you should increase the memory.</span></span>   

<span data-ttu-id="8bbe8-142">The concurrent number of tasks running or parallelism will be bounded by the total YARN memory.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-142">The concurrent number of tasks running or parallelism will be bounded by the total YARN memory.</span></span>  <span data-ttu-id="8bbe8-143">The number of YARN containers will dictate how many concurrent tasks can run.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-143">The number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="8bbe8-144">To find the YARN memory per node, you can go to Ambari.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-144">To find the YARN memory per node, you can go to Ambari.</span></span>  <span data-ttu-id="8bbe8-145">Navigate to YARN and view the Configs tab.  The YARN memory is displayed in this window.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-145">Navigate to YARN and view the Configs tab.  The YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="8bbe8-146">The key to improving performance using ADLS is to increase the concurrency as much as possible.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-146">The key to improving performance using ADLS is to increase the concurrency as much as possible.</span></span>  <span data-ttu-id="8bbe8-147">Tez automatically calculates the number of tasks that should be created so you do not need to set it.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-147">Tez automatically calculates the number of tasks that should be created so you do not need to set it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="8bbe8-148">Example Calculation</span><span class="sxs-lookup"><span data-stu-id="8bbe8-148">Example Calculation</span></span>

<span data-ttu-id="8bbe8-149">Let’s say you have an 8 node D14 cluster.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-149">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="8bbe8-150">Limitations</span><span class="sxs-lookup"><span data-stu-id="8bbe8-150">Limitations</span></span>
<span data-ttu-id="8bbe8-151">**ADLS throttling**</span><span class="sxs-lookup"><span data-stu-id="8bbe8-151">**ADLS throttling**</span></span> 

<span data-ttu-id="8bbe8-152">UIf you hit the limits of bandwidth provided by ADLS, you would start to see task failures.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-152">UIf you hit the limits of bandwidth provided by ADLS, you would start to see task failures.</span></span> <span data-ttu-id="8bbe8-153">This could be identified by observing throttling errors in task logs.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-153">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="8bbe8-154">You can decrease the parallelism by increasing Tez container size.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-154">You can decrease the parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="8bbe8-155">If you need more concurrency for your job, please contact us.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-155">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="8bbe8-156">To check if you are getting throttled, you need to enable the debug logging on the client side.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-156">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="8bbe8-157">Here’s how you can do that:</span><span class="sxs-lookup"><span data-stu-id="8bbe8-157">Here’s how you can do that:</span></span>

1. <span data-ttu-id="8bbe8-158">Put the following property in the log4j properties in Hive config. This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all the nodes/service for the config to take effect.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-158">Put the following property in the log4j properties in Hive config. This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all the nodes/service for the config to take effect.</span></span>

2. <span data-ttu-id="8bbe8-159">If you are getting throttled, you’ll see the HTTP 429 error code in the hive log file.</span><span class="sxs-lookup"><span data-stu-id="8bbe8-159">If you are getting throttled, you’ll see the HTTP 429 error code in the hive log file.</span></span> <span data-ttu-id="8bbe8-160">The hive log file is in /tmp/&lt;user&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="8bbe8-160">The hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="8bbe8-161">Further information on Hive tuning</span><span class="sxs-lookup"><span data-stu-id="8bbe8-161">Further information on Hive tuning</span></span>

<span data-ttu-id="8bbe8-162">Here are a few blogs that will help tune your Hive queries:</span><span class="sxs-lookup"><span data-stu-id="8bbe8-162">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="8bbe8-163">Optimize Hive queries for Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8bbe8-163">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="8bbe8-164">Troubleshooting Hive query performance</span><span class="sxs-lookup"><span data-stu-id="8bbe8-164">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="8bbe8-165">Ignite talk on optimize Hive on HDInsight</span><span class="sxs-lookup"><span data-stu-id="8bbe8-165">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
