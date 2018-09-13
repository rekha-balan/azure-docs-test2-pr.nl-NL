---
title: Use Livy to submit jobs remotely to Spark on Azure HDInsight | Microsoft Docs
description: Learn how to use Livy with HDInsight clusters to submit Spark jobs remotely.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: nitinme
ms.openlocfilehash: 6cb0da6d7b3aafeb9a8079b427e31c66811a6281
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550172"
---
# <a name="submit-spark-jobs-remotely-to-an-apache-spark-cluster-on-hdinsight-using-livy"></a><span data-ttu-id="7df57-103">Submit Spark jobs remotely to an Apache Spark cluster on HDInsight using Livy</span><span class="sxs-lookup"><span data-stu-id="7df57-103">Submit Spark jobs remotely to an Apache Spark cluster on HDInsight using Livy</span></span>

<span data-ttu-id="7df57-104">Apache Spark cluster on Azure HDInsight includes Livy, a REST interface for submitting jobs remotely to a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-104">Apache Spark cluster on Azure HDInsight includes Livy, a REST interface for submitting jobs remotely to a Spark cluster.</span></span> <span data-ttu-id="7df57-105">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span><span class="sxs-lookup"><span data-stu-id="7df57-105">For detailed documentation, see [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).</span></span>

<span data-ttu-id="7df57-106">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span><span class="sxs-lookup"><span data-stu-id="7df57-106">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="7df57-107">This article talks about using Livy to submit batch jobs.</span><span class="sxs-lookup"><span data-stu-id="7df57-107">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="7df57-108">The syntax below uses Curl to make REST calls to the Livy endpoint.</span><span class="sxs-lookup"><span data-stu-id="7df57-108">The syntax below uses Curl to make REST calls to the Livy endpoint.</span></span>

<span data-ttu-id="7df57-109">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="7df57-109">**Prerequisites:**</span></span>

<span data-ttu-id="7df57-110">You must have the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-110">You must have the following:</span></span>

* <span data-ttu-id="7df57-111">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="7df57-111">An Azure subscription.</span></span> <span data-ttu-id="7df57-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="7df57-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="7df57-113">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7df57-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="7df57-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="7df57-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="submit-a-batch-job"></a><span data-ttu-id="7df57-115">Submit a batch job</span><span class="sxs-lookup"><span data-stu-id="7df57-115">Submit a batch job</span></span>
<span data-ttu-id="7df57-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-116">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="7df57-117">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span><span class="sxs-lookup"><span data-stu-id="7df57-117">You can use [**AzCopy**](../storage/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="7df57-118">There are a lot of other clients you can use to upload data.</span><span class="sxs-lookup"><span data-stu-id="7df57-118">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="7df57-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="7df57-119">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

<span data-ttu-id="7df57-120">**Examples**:</span><span class="sxs-lookup"><span data-stu-id="7df57-120">**Examples**:</span></span>

* <span data-ttu-id="7df57-121">If the jar file is on the cluster storage (WASB)</span><span class="sxs-lookup"><span data-stu-id="7df57-121">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasbs://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="7df57-122">If the you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span><span class="sxs-lookup"><span data-stu-id="7df57-122">If the you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-batches-running-on-the-cluster"></a><span data-ttu-id="7df57-123">Get information on batches running on the cluster</span><span class="sxs-lookup"><span data-stu-id="7df57-123">Get information on batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="7df57-124">**Examples**:</span><span class="sxs-lookup"><span data-stu-id="7df57-124">**Examples**:</span></span>

* <span data-ttu-id="7df57-125">If you want to retrieve all the batches running on the cluster:</span><span class="sxs-lookup"><span data-stu-id="7df57-125">If you want to retrieve all the batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* <span data-ttu-id="7df57-126">If you want to retrieve a specific batch with a given batchId</span><span class="sxs-lookup"><span data-stu-id="7df57-126">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-batch-job"></a><span data-ttu-id="7df57-127">Delete a batch job</span><span class="sxs-lookup"><span data-stu-id="7df57-127">Delete a batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="7df57-128">**Example**:</span><span class="sxs-lookup"><span data-stu-id="7df57-128">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-and-high-availability"></a><span data-ttu-id="7df57-129">Livy and high-availability</span><span class="sxs-lookup"><span data-stu-id="7df57-129">Livy and high-availability</span></span>
<span data-ttu-id="7df57-130">Livy provides high-availability for Spark jobs running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-130">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="7df57-131">Here are a couple of examples.</span><span class="sxs-lookup"><span data-stu-id="7df57-131">Here are a couple of examples.</span></span>

* <span data-ttu-id="7df57-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="7df57-132">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="7df57-133">When Livy is back up, it restores the status of the job and reports it back.</span><span class="sxs-lookup"><span data-stu-id="7df57-133">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="7df57-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span><span class="sxs-lookup"><span data-stu-id="7df57-134">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="7df57-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook will continue to run the code cells.</span><span class="sxs-lookup"><span data-stu-id="7df57-135">If a notebook is running a Spark job and the Livy service gets restarted, the notebook will continue to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="7df57-136">Show me an example</span><span class="sxs-lookup"><span data-stu-id="7df57-136">Show me an example</span></span>
<span data-ttu-id="7df57-137">In this section, we look at examples on how to use Livy to submit a Spark application, monitor the progress of the application, and then delete the job.</span><span class="sxs-lookup"><span data-stu-id="7df57-137">In this section, we look at examples on how to use Livy to submit a Spark application, monitor the progress of the application, and then delete the job.</span></span> <span data-ttu-id="7df57-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="7df57-138">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](hdinsight-apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="7df57-139">The steps below assume the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-139">The steps below assume the following:</span></span>

* <span data-ttu-id="7df57-140">You have already copied over the application jar to the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-140">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="7df57-141">You have CuRL installed on the computer where you are trying these steps.</span><span class="sxs-lookup"><span data-stu-id="7df57-141">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="7df57-142">Perform the following steps.</span><span class="sxs-lookup"><span data-stu-id="7df57-142">Perform the following steps.</span></span>

1. <span data-ttu-id="7df57-143">Let us first verify that Livy is running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-143">Let us first verify that Livy is running on the cluster.</span></span> <span data-ttu-id="7df57-144">We can do so by getting a list of running batches.</span><span class="sxs-lookup"><span data-stu-id="7df57-144">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="7df57-145">If this is the first time you are running a job using Livy, this should return zero.</span><span class="sxs-lookup"><span data-stu-id="7df57-145">If this is the first time you are running a job using Livy, this should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="7df57-146">You should get an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-146">You should get an output similar to the following:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="7df57-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span><span class="sxs-lookup"><span data-stu-id="7df57-147">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>
2. <span data-ttu-id="7df57-148">Let us now submit a batch job.</span><span class="sxs-lookup"><span data-stu-id="7df57-148">Let us now submit a batch job.</span></span> <span data-ttu-id="7df57-149">The snippet below uses an input file (input.txt) to pass the jar name and the class name as parameters.</span><span class="sxs-lookup"><span data-stu-id="7df57-149">The snippet below uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="7df57-150">This is the recommended approach if you are running these steps from a Windows computer.</span><span class="sxs-lookup"><span data-stu-id="7df57-150">This is the recommended approach if you are running these steps from a Windows computer.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="7df57-151">The parameters in the file **input.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="7df57-151">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasbs:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="7df57-152">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-152">You should see an output similar to the following:</span></span>
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="7df57-153">Notice how the last line of the output says **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="7df57-153">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="7df57-154">It also says, **id:0**.</span><span class="sxs-lookup"><span data-stu-id="7df57-154">It also says, **id:0**.</span></span> <span data-ttu-id="7df57-155">This is the batch ID.</span><span class="sxs-lookup"><span data-stu-id="7df57-155">This is the batch ID.</span></span>
3. <span data-ttu-id="7df57-156">You can now retrieve the the status of this specific batch using the batch ID.</span><span class="sxs-lookup"><span data-stu-id="7df57-156">You can now retrieve the the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="7df57-157">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-157">You should see an output similar to the following:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="7df57-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span><span class="sxs-lookup"><span data-stu-id="7df57-158">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>
4. <span data-ttu-id="7df57-159">If you want, you can now delete the batch.</span><span class="sxs-lookup"><span data-stu-id="7df57-159">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="7df57-160">You should see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="7df57-160">You should see an output similar to the following:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="7df57-161">The last line of the output shows that the batch was successfully deleted.</span><span class="sxs-lookup"><span data-stu-id="7df57-161">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="7df57-162">If you delete a job while it is running, it will essentially kill the job.</span><span class="sxs-lookup"><span data-stu-id="7df57-162">If you delete a job while it is running, it will essentially kill the job.</span></span> <span data-ttu-id="7df57-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span><span class="sxs-lookup"><span data-stu-id="7df57-163">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-on-hdinsight-35-spark-clusters"></a><span data-ttu-id="7df57-164">Using Livy on HDInsight 3.5 Spark clusters</span><span class="sxs-lookup"><span data-stu-id="7df57-164">Using Livy on HDInsight 3.5 Spark clusters</span></span>

<span data-ttu-id="7df57-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span><span class="sxs-lookup"><span data-stu-id="7df57-165">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="7df57-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-166">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="7df57-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span><span class="sxs-lookup"><span data-stu-id="7df57-167">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="7df57-168">To do so:</span><span class="sxs-lookup"><span data-stu-id="7df57-168">To do so:</span></span>

1. <span data-ttu-id="7df57-169">Go to the Ambari portal for the cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-169">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="7df57-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-170">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="7df57-171">From the left navigation, click **Livy**, and then click **Configs**.</span><span class="sxs-lookup"><span data-stu-id="7df57-171">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="7df57-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span><span class="sxs-lookup"><span data-stu-id="7df57-172">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="7df57-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span><span class="sxs-lookup"><span data-stu-id="7df57-173">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7df57-174">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="7df57-174">Troubleshooting</span></span>

<span data-ttu-id="7df57-175">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="7df57-175">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="7df57-176">Using an external jar from the additional storage is not supported</span><span class="sxs-lookup"><span data-stu-id="7df57-176">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="7df57-177">**Problem:** If you are running a Spark job using Livy referencing an external jar from the additional storage associated with the cluster, the job will fail.</span><span class="sxs-lookup"><span data-stu-id="7df57-177">**Problem:** If you are running a Spark job using Livy referencing an external jar from the additional storage associated with the cluster, the job will fail.</span></span>

<span data-ttu-id="7df57-178">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="7df57-178">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>


## <a name="seealso"></a><span data-ttu-id="7df57-179">See also</span><span class="sxs-lookup"><span data-stu-id="7df57-179">See also</span></span>
* [<span data-ttu-id="7df57-180">Overview: Apache Spark on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-180">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="7df57-181">Scenarios</span><span class="sxs-lookup"><span data-stu-id="7df57-181">Scenarios</span></span>
* [<span data-ttu-id="7df57-182">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span><span class="sxs-lookup"><span data-stu-id="7df57-182">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="7df57-183">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span><span class="sxs-lookup"><span data-stu-id="7df57-183">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="7df57-184">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span><span class="sxs-lookup"><span data-stu-id="7df57-184">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="7df57-185">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span><span class="sxs-lookup"><span data-stu-id="7df57-185">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="7df57-186">Website log analysis using Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-186">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="7df57-187">Create and run applications</span><span class="sxs-lookup"><span data-stu-id="7df57-187">Create and run applications</span></span>
* [<span data-ttu-id="7df57-188">Create a standalone application using Scala</span><span class="sxs-lookup"><span data-stu-id="7df57-188">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="7df57-189">Tools and extensions</span><span class="sxs-lookup"><span data-stu-id="7df57-189">Tools and extensions</span></span>
* [<span data-ttu-id="7df57-190">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span><span class="sxs-lookup"><span data-stu-id="7df57-190">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="7df57-191">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span><span class="sxs-lookup"><span data-stu-id="7df57-191">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="7df57-192">Use Zeppelin notebooks with a Spark cluster on HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-192">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-use-zeppelin-notebook.md)
* [<span data-ttu-id="7df57-193">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-193">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="7df57-194">Use external packages with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="7df57-194">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="7df57-195">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="7df57-195">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="7df57-196">Manage resources</span><span class="sxs-lookup"><span data-stu-id="7df57-196">Manage resources</span></span>
* [<span data-ttu-id="7df57-197">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-197">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="7df57-198">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7df57-198">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

