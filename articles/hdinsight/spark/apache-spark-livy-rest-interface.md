---
title: Use Livy Spark to submit jobs to Spark cluster on Azure HDInsight
description: Learn how to use Apache Spark REST API to submit Spark jobs remotely to an Azure HDInsight cluster.
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 07/18/2018
ms.openlocfilehash: 677c7d27d34725b75c5dfed70cc377735f5d7d61
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870191"
---
# <a name="use-apache-spark-rest-api-to-submit-remote-jobs-to-an-hdinsight-spark-cluster"></a><span data-ttu-id="8f6a4-103">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span><span class="sxs-lookup"><span data-stu-id="8f6a4-103">Use Apache Spark REST API to submit remote jobs to an HDInsight Spark cluster</span></span>

<span data-ttu-id="8f6a4-104">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-104">Learn how to use Livy, the Apache Spark REST API, which is used to submit remote jobs to an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="8f6a4-105">For detailed documentation, see [http://livy.incubator.apache.org/](http://livy.incubator.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-105">For detailed documentation, see [http://livy.incubator.apache.org/](http://livy.incubator.apache.org/).</span></span>

<span data-ttu-id="8f6a4-106">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-106">You can use Livy to run interactive Spark shells or submit batch jobs to be run on Spark.</span></span> <span data-ttu-id="8f6a4-107">This article talks about using Livy to submit batch jobs.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-107">This article talks about using Livy to submit batch jobs.</span></span> <span data-ttu-id="8f6a4-108">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-108">The snippets in this article use cURL to make REST API calls to the Livy Spark endpoint.</span></span>

<span data-ttu-id="8f6a4-109">**Prerequisites:**</span><span class="sxs-lookup"><span data-stu-id="8f6a4-109">**Prerequisites:**</span></span>

* <span data-ttu-id="8f6a4-110">An Apache Spark cluster on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-110">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="8f6a4-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-111">For instructions, see [Create Apache Spark clusters in Azure HDInsight](apache-spark-jupyter-spark-sql.md).</span></span>

* <span data-ttu-id="8f6a4-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="8f6a4-113">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-113">This article uses cURL to demonstrate how to make REST API calls against an HDInsight Spark cluster.</span></span>

## <a name="submit-a-livy-spark-batch-job"></a><span data-ttu-id="8f6a4-114">Submit a Livy Spark batch job</span><span class="sxs-lookup"><span data-stu-id="8f6a4-114">Submit a Livy Spark batch job</span></span>
<span data-ttu-id="8f6a4-115">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-115">Before you submit a batch job, you must upload the application jar on the cluster storage associated with the cluster.</span></span> <span data-ttu-id="8f6a4-116">You can use [**AzCopy**](../../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-116">You can use [**AzCopy**](../../storage/common/storage-use-azcopy.md), a command-line utility, to do so.</span></span> <span data-ttu-id="8f6a4-117">There are various other clients you can use to upload data.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-117">There are various other clients you can use to upload data.</span></span> <span data-ttu-id="8f6a4-118">You can find more about them at [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-118">You can find more about them at [Upload data for Hadoop jobs in HDInsight](../hdinsight-upload-data.md).</span></span>

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path to application jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches' -H "X-Requested-By: admin"

<span data-ttu-id="8f6a4-119">**Examples**:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-119">**Examples**:</span></span>

* <span data-ttu-id="8f6a4-120">If the jar file is on the cluster storage (WASB)</span><span class="sxs-lookup"><span data-stu-id="8f6a4-120">If the jar file is on the cluster storage (WASB)</span></span>
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"
* <span data-ttu-id="8f6a4-121">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span><span class="sxs-lookup"><span data-stu-id="8f6a4-121">If you want to pass the jar filename and the classname as part of an input file (in this example, input.txt)</span></span>
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"

## <a name="get-information-on-livy-spark-batches-running-on-the-cluster"></a><span data-ttu-id="8f6a4-122">Get information on Livy Spark batches running on the cluster</span><span class="sxs-lookup"><span data-stu-id="8f6a4-122">Get information on Livy Spark batches running on the cluster</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

<span data-ttu-id="8f6a4-123">**Examples**:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-123">**Examples**:</span></span>

* <span data-ttu-id="8f6a4-124">If you want to retrieve all the Livy Spark batches running on the cluster:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-124">If you want to retrieve all the Livy Spark batches running on the cluster:</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches" 
* <span data-ttu-id="8f6a4-125">If you want to retrieve a specific batch with a given batchId</span><span class="sxs-lookup"><span data-stu-id="8f6a4-125">If you want to retrieve a specific batch with a given batchId</span></span>
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a><span data-ttu-id="8f6a4-126">Delete a Livy Spark batch job</span><span class="sxs-lookup"><span data-stu-id="8f6a4-126">Delete a Livy Spark batch job</span></span>
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

<span data-ttu-id="8f6a4-127">**Example**:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-127">**Example**:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a><span data-ttu-id="8f6a4-128">Livy Spark and high-availability</span><span class="sxs-lookup"><span data-stu-id="8f6a4-128">Livy Spark and high-availability</span></span>
<span data-ttu-id="8f6a4-129">Livy provides high-availability for Spark jobs running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-129">Livy provides high-availability for Spark jobs running on the cluster.</span></span> <span data-ttu-id="8f6a4-130">Here is a couple of examples.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-130">Here is a couple of examples.</span></span>

* <span data-ttu-id="8f6a4-131">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-131">If the Livy service goes down after you have submitted a job remotely to a Spark cluster, the job continues to run in the background.</span></span> <span data-ttu-id="8f6a4-132">When Livy is back up, it restores the status of the job and reports it back.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-132">When Livy is back up, it restores the status of the job and reports it back.</span></span>
* <span data-ttu-id="8f6a4-133">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-133">Jupyter notebooks for HDInsight are powered by Livy in the backend.</span></span> <span data-ttu-id="8f6a4-134">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-134">If a notebook is running a Spark job and the Livy service gets restarted, the notebook continues to run the code cells.</span></span> 

## <a name="show-me-an-example"></a><span data-ttu-id="8f6a4-135">Show me an example</span><span class="sxs-lookup"><span data-stu-id="8f6a4-135">Show me an example</span></span>
<span data-ttu-id="8f6a4-136">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-136">In this section, we look at examples to use Livy Spark to submit batch job, monitor the progress of the job, and then delete it.</span></span> <span data-ttu-id="8f6a4-137">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](apache-spark-create-standalone-application.md).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-137">The application we use in this example is the one developed in the article [Create a standalone Scala application and to run on HDInsight Spark cluster](apache-spark-create-standalone-application.md).</span></span> <span data-ttu-id="8f6a4-138">The steps here assume that:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-138">The steps here assume that:</span></span>

* <span data-ttu-id="8f6a4-139">You have already copied over the application jar to the storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-139">You have already copied over the application jar to the storage account associated with the cluster.</span></span>
* <span data-ttu-id="8f6a4-140">You have CuRL installed on the computer where you are trying these steps.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-140">You have CuRL installed on the computer where you are trying these steps.</span></span>

<span data-ttu-id="8f6a4-141">Perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-141">Perform the following steps:</span></span>

1. <span data-ttu-id="8f6a4-142">Let us first verify that Livy Spark is running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-142">Let us first verify that Livy Spark is running on the cluster.</span></span> <span data-ttu-id="8f6a4-143">We can do so by getting a list of running batches.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-143">We can do so by getting a list of running batches.</span></span> <span data-ttu-id="8f6a4-144">If you are running a job using Livy for the first time, the output should return zero.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-144">If you are running a job using Livy for the first time, the output should return zero.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    <span data-ttu-id="8f6a4-145">You should get an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-145">You should get an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="8f6a4-146">Notice how the last line in the output says **total:0**, which suggests no running batches.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-146">Notice how the last line in the output says **total:0**, which suggests no running batches.</span></span>

2. <span data-ttu-id="8f6a4-147">Let us now submit a batch job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-147">Let us now submit a batch job.</span></span> <span data-ttu-id="8f6a4-148">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-148">The following snippet uses an input file (input.txt) to pass the jar name and the class name as parameters.</span></span> <span data-ttu-id="8f6a4-149">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-149">If you are running these steps from a Windows computer, using an input file is the recommended approach.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches" -H "X-Requested-By: admin"
   
    <span data-ttu-id="8f6a4-150">The parameters in the file **input.txt** are defined as follows:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-150">The parameters in the file **input.txt** are defined as follows:</span></span>
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    <span data-ttu-id="8f6a4-151">You should see an output similar to the  following snippet:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-151">You should see an output similar to the  following snippet:</span></span>
   
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
   
    <span data-ttu-id="8f6a4-152">Notice how the last line of the output says **state:starting**.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-152">Notice how the last line of the output says **state:starting**.</span></span> <span data-ttu-id="8f6a4-153">It also says, **id:0**.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-153">It also says, **id:0**.</span></span> <span data-ttu-id="8f6a4-154">Here, **0** is the batch ID.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-154">Here, **0** is the batch ID.</span></span>

3. <span data-ttu-id="8f6a4-155">You can now retrieve the status of this specific batch using the batch ID.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-155">You can now retrieve the status of this specific batch using the batch ID.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="8f6a4-156">You should see an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-156">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="8f6a4-157">The output now shows **state:success**, which suggests that the job was successfully completed.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-157">The output now shows **state:success**, which suggests that the job was successfully completed.</span></span>

4. <span data-ttu-id="8f6a4-158">If you want, you can now delete the batch.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-158">If you want, you can now delete the batch.</span></span>
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    <span data-ttu-id="8f6a4-159">You should see an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-159">You should see an output similar to the following snippet:</span></span>
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact
   
    <span data-ttu-id="8f6a4-160">The last line of the output shows that the batch was successfully deleted.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-160">The last line of the output shows that the batch was successfully deleted.</span></span> <span data-ttu-id="8f6a4-161">Deleting a job, while it is running, also kills the job.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-161">Deleting a job, while it is running, also kills the job.</span></span> <span data-ttu-id="8f6a4-162">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-162">If you delete a job that has completed, successfully or otherwise, it deletes the job information completely.</span></span>

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a><span data-ttu-id="8f6a4-163">Using Livy Spark on HDInsight 3.5 clusters</span><span class="sxs-lookup"><span data-stu-id="8f6a4-163">Using Livy Spark on HDInsight 3.5 clusters</span></span>

<span data-ttu-id="8f6a4-164">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-164">HDInsight 3.5 cluster, by default, disables use of local file paths to access sample data files or jars.</span></span> <span data-ttu-id="8f6a4-165">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-165">We encourage you to use the `wasb://` path instead to access jars or sample data files from the cluster.</span></span> <span data-ttu-id="8f6a4-166">If you do want to use local path, you must update the Ambari configuration accordingly.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-166">If you do want to use local path, you must update the Ambari configuration accordingly.</span></span> <span data-ttu-id="8f6a4-167">To do so:</span><span class="sxs-lookup"><span data-stu-id="8f6a4-167">To do so:</span></span>

1. <span data-ttu-id="8f6a4-168">Go to the Ambari portal for the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-168">Go to the Ambari portal for the cluster.</span></span> <span data-ttu-id="8f6a4-169">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-169">The Ambari Web UI is available on your HDInsight cluster at https://**CLUSTERNAME**.azurehdidnsight.net, where CLUSTERNAME is the name of your cluster.</span></span>

2. <span data-ttu-id="8f6a4-170">From the left navigation, click **Livy**, and then click **Configs**.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-170">From the left navigation, click **Livy**, and then click **Configs**.</span></span>

3. <span data-ttu-id="8f6a4-171">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-171">Under **livy-default** add the property name `livy.file.local-dir-whitelist` and set it's value to **"/"** if you want to allow full access to file system.</span></span> <span data-ttu-id="8f6a4-172">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-172">If you want to allow access only to a specific directory, provide the path to that directory as the value.</span></span>

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a><span data-ttu-id="8f6a4-173">Submitting Livy jobs for a cluster within an Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="8f6a4-173">Submitting Livy jobs for a cluster within an Azure virtual network</span></span>

<span data-ttu-id="8f6a4-174">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-174">If you connect to an HDInsight Spark cluster from within an Azure Virtual Network, you can directly connect to Livy on the cluster.</span></span> <span data-ttu-id="8f6a4-175">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-175">In such a case, the URL for Livy endpoint is `http://<IP address of the headnode>:8998/batches`.</span></span> <span data-ttu-id="8f6a4-176">Here, **8998** is the port on which Livy runs on the cluster headnode.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-176">Here, **8998** is the port on which Livy runs on the cluster headnode.</span></span> <span data-ttu-id="8f6a4-177">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](../hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="8f6a4-177">For more information on accessing services on non-public ports, see [Ports used by Hadoop services on HDInsight](../hdinsight-hadoop-port-settings-for-services.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="8f6a4-178">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="8f6a4-178">Troubleshooting</span></span>

<span data-ttu-id="8f6a4-179">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-179">Here are some issues that you might run into while using Livy for remote job submission to Spark clusters.</span></span>

### <a name="using-an-external-jar-from-the-additional-storage-is-not-supported"></a><span data-ttu-id="8f6a4-180">Using an external jar from the additional storage is not supported</span><span class="sxs-lookup"><span data-stu-id="8f6a4-180">Using an external jar from the additional storage is not supported</span></span>

<span data-ttu-id="8f6a4-181">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-181">**Problem:** If your Livy Spark job references an external jar from the additional storage account associated with the cluster, the job fails.</span></span>

<span data-ttu-id="8f6a4-182">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8f6a4-182">**Resolution:** Make sure that the jar you want to use is available in the default storage associated with the HDInsight cluster.</span></span>





## <a name="next-step"></a><span data-ttu-id="8f6a4-183">Next step</span><span class="sxs-lookup"><span data-stu-id="8f6a4-183">Next step</span></span>

* [<span data-ttu-id="8f6a4-184">Livy REST API documentation</span><span class="sxs-lookup"><span data-stu-id="8f6a4-184">Livy REST API documentation</span></span>](http://livy.incubator.apache.org/docs/latest/rest-api.html)
* [<span data-ttu-id="8f6a4-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f6a4-185">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](apache-spark-resource-manager.md)
* [<span data-ttu-id="8f6a4-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8f6a4-186">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](apache-spark-job-debugging.md)

