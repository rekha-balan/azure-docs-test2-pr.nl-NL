---
title: Use Hadoop Sqoop with Curl in HDInsight - Azure
description: Learn how to remotely submit Sqoop jobs to HDInsight using Curl.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: 44b151cdd66bdcb5bb2ec005298f58186d98e97a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966077"
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="90168-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span><span class="sxs-lookup"><span data-stu-id="90168-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="90168-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="90168-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="90168-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span><span class="sxs-lookup"><span data-stu-id="90168-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="90168-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="90168-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90168-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="90168-107">Prerequisites</span></span>
<span data-ttu-id="90168-108">To complete the steps in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="90168-108">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="90168-109">Complete [Use Sqoop with Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database) to configure an environment with a HDInsight cluster and a Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="90168-109">Complete [Use Sqoop with Hadoop in HDInsight](hdinsight-use-sqoop.md#create-cluster-and-sql-database) to configure an environment with a HDInsight cluster and a Azure SQL database.</span></span>
* <span data-ttu-id="90168-110">[Curl](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="90168-110">[Curl](http://curl.haxx.se/).</span></span> <span data-ttu-id="90168-111">Curl is a tool to transfer data from or to a HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="90168-111">Curl is a tool to transfer data from or to a HDInsight cluster.</span></span>
* <span data-ttu-id="90168-112">[jq](http://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="90168-112">[jq](http://stedolan.github.io/jq/).</span></span> <span data-ttu-id="90168-113">The jq utility is used to process the JSON data returned from REST requests.</span><span class="sxs-lookup"><span data-stu-id="90168-113">The jq utility is used to process the JSON data returned from REST requests.</span></span>

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="90168-114">Submit Sqoop jobs by using Curl</span><span class="sxs-lookup"><span data-stu-id="90168-114">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="90168-115">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="90168-115">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="90168-116">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="90168-116">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="90168-117">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="90168-117">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="90168-118">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="90168-118">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="90168-119">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="90168-119">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="90168-120">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="90168-120">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="90168-121">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="90168-121">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash   
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="90168-122">You should receive a response similar to the following:</span><span class="sxs-lookup"><span data-stu-id="90168-122">You should receive a response similar to the following:</span></span>

    ```json   
    {"status":"ok","version":"v1"}
    ```
   
    <span data-ttu-id="90168-123">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="90168-123">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="90168-124">**-u** - The user name and password used to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="90168-124">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="90168-125">**-G** - Indicates that this is a GET request.</span><span class="sxs-lookup"><span data-stu-id="90168-125">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="90168-126">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="90168-126">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="90168-127">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="90168-127">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="90168-128">Use the following to submit a sqoop job:</span><span class="sxs-lookup"><span data-stu-id="90168-128">Use the following to submit a sqoop job:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /example/data/sample.log --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/data/sqoop/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop
    ```

    <span data-ttu-id="90168-129">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="90168-129">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="90168-130">**-d** - Since `-G` is not used, the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="90168-130">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="90168-131">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="90168-131">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="90168-132">**user.name** - The user that is running the command.</span><span class="sxs-lookup"><span data-stu-id="90168-132">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="90168-133">**command** - The Sqoop command to execute.</span><span class="sxs-lookup"><span data-stu-id="90168-133">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="90168-134">**statusdir** - The directory that the status for this job will be written to.</span><span class="sxs-lookup"><span data-stu-id="90168-134">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="90168-135">This command shall return a job ID that can be used to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="90168-135">This command shall return a job ID that can be used to check the status of the job.</span></span>

        ```json
        {"id":"job_1415651640909_0026"}
        ```

3. <span data-ttu-id="90168-136">To check the status of the job, use the following command.</span><span class="sxs-lookup"><span data-stu-id="90168-136">To check the status of the job, use the following command.</span></span> <span data-ttu-id="90168-137">Replace **JOBID** with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="90168-137">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="90168-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="90168-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="90168-139">If the job has finished, the state will be **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="90168-139">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="90168-140">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="90168-140">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
4. <span data-ttu-id="90168-141">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="90168-141">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="90168-142">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/data/sqoop/curl**.</span><span class="sxs-lookup"><span data-stu-id="90168-142">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasb:///example/data/sqoop/curl**.</span></span> <span data-ttu-id="90168-143">This address stores the output of the job in the **example/data/sqoop/curl** directory on the default storage container used by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="90168-143">This address stores the output of the job in the **example/data/sqoop/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="90168-144">You can use the Azure portal to access stderr and stdout blobs.</span><span class="sxs-lookup"><span data-stu-id="90168-144">You can use the Azure portal to access stderr and stdout blobs.</span></span>  <span data-ttu-id="90168-145">You can also use Microsoft SQL Server Management Studio to check the data that is uploaded to the log4jlogs table.</span><span class="sxs-lookup"><span data-stu-id="90168-145">You can also use Microsoft SQL Server Management Studio to check the data that is uploaded to the log4jlogs table.</span></span>

## <a name="limitations"></a><span data-ttu-id="90168-146">Limitations</span><span class="sxs-lookup"><span data-stu-id="90168-146">Limitations</span></span>
* <span data-ttu-id="90168-147">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="90168-147">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="90168-148">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="90168-148">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="90168-149">Summary</span><span class="sxs-lookup"><span data-stu-id="90168-149">Summary</span></span>
<span data-ttu-id="90168-150">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="90168-150">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="90168-151">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span><span class="sxs-lookup"><span data-stu-id="90168-151">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90168-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="90168-152">Next steps</span></span>
<span data-ttu-id="90168-153">For general information on Hive with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="90168-153">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="90168-154">Use Sqoop with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="90168-154">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="90168-155">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="90168-155">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="90168-156">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="90168-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="90168-157">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="90168-157">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="90168-158">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="90168-158">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="90168-159">For other HDInsight articles involving curl:</span><span class="sxs-lookup"><span data-stu-id="90168-159">For other HDInsight articles involving curl:</span></span>
 
* [<span data-ttu-id="90168-160">Create Hadoop clusters using the Azure REST API</span><span class="sxs-lookup"><span data-stu-id="90168-160">Create Hadoop clusters using the Azure REST API</span></span>](../hdinsight-hadoop-create-linux-clusters-curl-rest.md)
* [<span data-ttu-id="90168-161">Run Hive queries with Hadoop in HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="90168-161">Run Hive queries with Hadoop in HDInsight using REST</span></span>](apache-hadoop-use-hive-curl.md)
* [<span data-ttu-id="90168-162">Run MapReduce jobs with Hadoop on HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="90168-162">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>](apache-hadoop-use-mapreduce-curl.md)
* [<span data-ttu-id="90168-163">Run Pig jobs with Hadoop on HDInsight using cURL</span><span class="sxs-lookup"><span data-stu-id="90168-163">Run Pig jobs with Hadoop on HDInsight using cURL</span></span>](apache-hadoop-use-pig-curl.md)



