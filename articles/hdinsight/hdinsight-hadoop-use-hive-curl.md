---
title: Use Hadoop Hive with Curl in HDInsight | Microsoft Docs
description: Learn how to remotely submit Pig jobs to HDInsight using Curl.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 5953a4d15af087b30c8bd17245108894791bdf15
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540998"
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="98c5d-103">Run Hive queries with Hadoop in HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="98c5d-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="98c5d-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="98c5d-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

<span data-ttu-id="98c5d-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span><span class="sxs-lookup"><span data-stu-id="98c5d-105">[Curl](http://curl.haxx.se/) is used to demonstrate how you can interact with HDInsight by using raw HTTP requests.</span></span> <span data-ttu-id="98c5d-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span><span class="sxs-lookup"><span data-stu-id="98c5d-106">The [jq](http://stedolan.github.io/jq/) utility is used to process the JSON data returned from REST requests.</span></span>

> [!NOTE]
> <span data-ttu-id="98c5d-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="98c5d-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see the [What you need to know about Hadoop on Linux-based HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>

## <a id="curl"></a><span data-ttu-id="98c5d-108">Run Hive queries</span><span class="sxs-lookup"><span data-stu-id="98c5d-108">Run Hive queries</span></span>

> [!NOTE]
> <span data-ttu-id="98c5d-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="98c5d-109">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="98c5d-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="98c5d-110">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="98c5d-111">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="98c5d-111">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="98c5d-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="98c5d-112">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="98c5d-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="98c5d-113">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="98c5d-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="98c5d-114">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="98c5d-115">You receive a response similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="98c5d-115">You receive a response similar to the following text:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="98c5d-116">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="98c5d-116">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="98c5d-117">**-u** - The user name and password used to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="98c5d-117">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="98c5d-118">**-G** - Indicates that this request is a GET operation.</span><span class="sxs-lookup"><span data-stu-id="98c5d-118">**-G** - Indicates that this request is a GET operation.</span></span>

     <span data-ttu-id="98c5d-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="98c5d-119">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="98c5d-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="98c5d-120">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="98c5d-121">You can also request the version of Hive by using the following command:</span><span class="sxs-lookup"><span data-stu-id="98c5d-121">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     <span data-ttu-id="98c5d-122">This request returns a response similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="98c5d-122">This request returns a response similar to the following text:</span></span>

       <span data-ttu-id="98c5d-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span><span class="sxs-lookup"><span data-stu-id="98c5d-123">{"module":"hive","version":"0.13.0.2.1.6.0-2103"}</span></span>

2. <span data-ttu-id="98c5d-124">Use the following to create a table named **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="98c5d-124">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="98c5d-125">The following parameters used with this request:</span><span class="sxs-lookup"><span data-stu-id="98c5d-125">The following parameters used with this request:</span></span>

   * <span data-ttu-id="98c5d-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="98c5d-126">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="98c5d-127">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="98c5d-127">`-d` specifies the data values that are sent with the request.</span></span>

     * <span data-ttu-id="98c5d-128">**user.name** - The user that is running the command.</span><span class="sxs-lookup"><span data-stu-id="98c5d-128">**user.name** - The user that is running the command.</span></span>
     * <span data-ttu-id="98c5d-129">**execute** - The HiveQL statements to execute.</span><span class="sxs-lookup"><span data-stu-id="98c5d-129">**execute** - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="98c5d-130">**statusdir** - The directory that the status for this job is written to.</span><span class="sxs-lookup"><span data-stu-id="98c5d-130">**statusdir** - The directory that the status for this job is written to.</span></span>

     <span data-ttu-id="98c5d-131">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="98c5d-131">These statements perform the following actions:</span></span>
   * <span data-ttu-id="98c5d-132">**DROP TABLE** - If the table already exists, it is deleted.</span><span class="sxs-lookup"><span data-stu-id="98c5d-132">**DROP TABLE** - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="98c5d-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span><span class="sxs-lookup"><span data-stu-id="98c5d-133">**CREATE EXTERNAL TABLE** - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="98c5d-134">External tables store only the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="98c5d-134">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="98c5d-135">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="98c5d-135">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98c5d-136">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="98c5d-136">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="98c5d-137">For example, an automated data upload process or another MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="98c5d-137">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="98c5d-138">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="98c5d-138">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="98c5d-139">**ROW FORMAT** - How the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="98c5d-139">**ROW FORMAT** - How the data is formatted.</span></span> <span data-ttu-id="98c5d-140">The fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="98c5d-140">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="98c5d-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="98c5d-141">**STORED AS TEXTFILE LOCATION** - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="98c5d-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="98c5d-142">**SELECT** - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="98c5d-143">This statement returns a value of **3** as there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="98c5d-143">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98c5d-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span><span class="sxs-lookup"><span data-stu-id="98c5d-144">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="98c5d-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span><span class="sxs-lookup"><span data-stu-id="98c5d-145">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

   * <span data-ttu-id="98c5d-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="98c5d-146">**INPUT__FILE__NAME LIKE '%25.log'** - This statement limits the search to only use files ending in .log.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98c5d-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span><span class="sxs-lookup"><span data-stu-id="98c5d-147">The `%25` is the URL encoded form of %, so the actual condition is `like '%.log'`.</span></span> <span data-ttu-id="98c5d-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span><span class="sxs-lookup"><span data-stu-id="98c5d-148">The % has to be URL encoded, as it is treated as a special character in URLs.</span></span>

     <span data-ttu-id="98c5d-149">This command should return a job ID that can be used to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="98c5d-149">This command should return a job ID that can be used to check the status of the job.</span></span>

       <span data-ttu-id="98c5d-150">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="98c5d-150">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="98c5d-151">To check the status of the job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="98c5d-151">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="98c5d-152">Replace **JOBID** with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="98c5d-152">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="98c5d-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="98c5d-153">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="98c5d-154">If the job has finished, the state is **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="98c5d-154">If the job has finished, the state is **SUCCEEDED**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="98c5d-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span><span class="sxs-lookup"><span data-stu-id="98c5d-155">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job.</span></span> <span data-ttu-id="98c5d-156">Jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="98c5d-156">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="98c5d-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="98c5d-157">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="98c5d-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span><span class="sxs-lookup"><span data-stu-id="98c5d-158">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/curl**.</span></span> <span data-ttu-id="98c5d-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span><span class="sxs-lookup"><span data-stu-id="98c5d-159">This address stores the output in the **example/curl** directory in the clusters default storage.</span></span>

    <span data-ttu-id="98c5d-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="98c5d-160">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="98c5d-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="98c5d-161">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

5. <span data-ttu-id="98c5d-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="98c5d-162">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    <span data-ttu-id="98c5d-163">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="98c5d-163">These statements perform the following actions:</span></span>

   * <span data-ttu-id="98c5d-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="98c5d-164">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="98c5d-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="98c5d-165">This statement creates an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="98c5d-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span><span class="sxs-lookup"><span data-stu-id="98c5d-166">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="98c5d-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="98c5d-167">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="98c5d-168">ORC is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="98c5d-168">ORC is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="98c5d-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="98c5d-169">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>
   * <span data-ttu-id="98c5d-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="98c5d-170">**SELECT** - Selects all rows from the new **errorLogs** table.</span></span>

6. <span data-ttu-id="98c5d-171">Use the job ID returned to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="98c5d-171">Use the job ID returned to check the status of the job.</span></span> <span data-ttu-id="98c5d-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span><span class="sxs-lookup"><span data-stu-id="98c5d-172">Once it has succeeded, use the Azure CLI as described previously to download and view the results.</span></span> <span data-ttu-id="98c5d-173">The output should contain three lines, all of which contain **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="98c5d-173">The output should contain three lines, all of which contain **[ERROR]**.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="98c5d-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="98c5d-174">Next steps</span></span>

<span data-ttu-id="98c5d-175">For general information on Hive with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="98c5d-175">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="98c5d-176">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="98c5d-176">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="98c5d-177">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="98c5d-177">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="98c5d-178">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="98c5d-178">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="98c5d-179">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="98c5d-179">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="98c5d-180">If you are using Tez with Hive, see the following documents for debugging information:</span><span class="sxs-lookup"><span data-stu-id="98c5d-180">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="98c5d-181">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="98c5d-181">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="98c5d-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span><span class="sxs-lookup"><span data-stu-id="98c5d-182">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md




[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


