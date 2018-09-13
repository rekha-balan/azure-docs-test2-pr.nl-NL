---
title: Use Hadoop Pig with REST in HDInsight - Azure
description: Learn how to use REST to run Pig Latin jobs on a Hadoop cluster in Azure HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: jasonh
ms.openlocfilehash: e97dcd5a15fa1a58782fb8225e8b3381d7061bb6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967883"
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a><span data-ttu-id="1f1d0-103">Run Pig jobs with Hadoop on HDInsight by using REST</span><span class="sxs-lookup"><span data-stu-id="1f1d0-103">Run Pig jobs with Hadoop on HDInsight by using REST</span></span>

[!INCLUDE [pig-selector](../../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="1f1d0-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-104">Learn how to run Pig Latin jobs by making REST requests to an Azure HDInsight cluster.</span></span> <span data-ttu-id="1f1d0-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-105">Curl is used to demonstrate how you can interact with HDInsight using the WebHCat REST API.</span></span>

> [!NOTE]
> <span data-ttu-id="1f1d0-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](../hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="1f1d0-106">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](../hdinsight-hadoop-linux-information.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="1f1d0-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1f1d0-107">Prerequisites</span></span>

* <span data-ttu-id="1f1d0-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span><span class="sxs-lookup"><span data-stu-id="1f1d0-108">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1f1d0-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1f1d0-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1f1d0-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="1f1d0-111">Curl</span><span class="sxs-lookup"><span data-stu-id="1f1d0-111">Curl</span></span>](http://curl.haxx.se/)

* [<span data-ttu-id="1f1d0-112">jq</span><span class="sxs-lookup"><span data-stu-id="1f1d0-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a id="curl"></a><span data-ttu-id="1f1d0-113">Run Pig jobs by using Curl</span><span class="sxs-lookup"><span data-stu-id="1f1d0-113">Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="1f1d0-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="1f1d0-114">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="1f1d0-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-115">Always make requests by using Secure HTTP (HTTPS) to ensure that your credentials are securely sent to the server.</span></span>
>
> <span data-ttu-id="1f1d0-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-116">When using the commands in this section, replace `USERNAME` with the user to authenticate to the cluster, and replace `PASSWORD` with the password for the user account.</span></span> <span data-ttu-id="1f1d0-117">Replace `CLUSTERNAME` with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-117">Replace `CLUSTERNAME` with the name of your cluster.</span></span>
>


1. <span data-ttu-id="1f1d0-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="1f1d0-119">You should receive the following JSON response:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-119">You should receive the following JSON response:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="1f1d0-120">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-120">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="1f1d0-121">**-u**: The user name and password used to authenticate the request</span><span class="sxs-lookup"><span data-stu-id="1f1d0-121">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="1f1d0-122">**-G**: Indicates that this request is a GET request</span><span class="sxs-lookup"><span data-stu-id="1f1d0-122">**-G**: Indicates that this request is a GET request</span></span>

     <span data-ttu-id="1f1d0-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-123">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span> <span data-ttu-id="1f1d0-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-124">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="1f1d0-125">Use the following code to submit a Pig Latin job to the cluster:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-125">Use the following code to submit a Pig Latin job to the cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    <span data-ttu-id="1f1d0-126">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-126">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="1f1d0-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-127">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="1f1d0-128">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-128">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="1f1d0-129">**user.name**: The user who is running the command</span><span class="sxs-lookup"><span data-stu-id="1f1d0-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="1f1d0-130">**execute**: The Pig Latin statements to execute</span><span class="sxs-lookup"><span data-stu-id="1f1d0-130">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="1f1d0-131">**statusdir**: The directory that the status for this job is written to</span><span class="sxs-lookup"><span data-stu-id="1f1d0-131">**statusdir**: The directory that the status for this job is written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f1d0-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-132">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="1f1d0-133">This command should return a job ID that can be used to check the status of the job, for example:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-133">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="1f1d0-134">To check the status of the job, use the following command</span><span class="sxs-lookup"><span data-stu-id="1f1d0-134">To check the status of the job, use the following command</span></span>

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     <span data-ttu-id="1f1d0-135">Replace `JOBID` with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-135">Replace `JOBID` with the value returned in the previous step.</span></span> <span data-ttu-id="1f1d0-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-136">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then `JOBID` is `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="1f1d0-137">If the job has finished, the state is **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-137">If the job has finished, the state is **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1f1d0-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-138">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <a id="results"></a><span data-ttu-id="1f1d0-139">View results</span><span class="sxs-lookup"><span data-stu-id="1f1d0-139">View results</span></span>

<span data-ttu-id="1f1d0-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-140">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job.</span></span> <span data-ttu-id="1f1d0-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/pigcurl`.</span></span>

<span data-ttu-id="1f1d0-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-142">HDInsight can use either Azure Storage or Azure Data Lake Store as the default data store.</span></span> <span data-ttu-id="1f1d0-143">There are various ways to get at the data depending on which one you use.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-143">There are various ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="1f1d0-144">For more information, see the storage section of the [Linux-based HDInsight information](../hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-144">For more information, see the storage section of the [Linux-based HDInsight information](../hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) document.</span></span>

## <a id="summary"></a><span data-ttu-id="1f1d0-145">Summary</span><span class="sxs-lookup"><span data-stu-id="1f1d0-145">Summary</span></span>

<span data-ttu-id="1f1d0-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1f1d0-146">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="1f1d0-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="1f1d0-147">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <a id="nextsteps"></a><span data-ttu-id="1f1d0-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f1d0-148">Next steps</span></span>

<span data-ttu-id="1f1d0-149">For general information about Pig on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-149">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="1f1d0-150">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f1d0-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="1f1d0-151">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1f1d0-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="1f1d0-152">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f1d0-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="1f1d0-153">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="1f1d0-153">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
