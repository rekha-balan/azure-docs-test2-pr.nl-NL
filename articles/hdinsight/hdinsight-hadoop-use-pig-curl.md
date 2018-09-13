---
title: Use Hadoop Pig with Curl in HDInsight | Microsoft Docs
description: Learn how to use Curl to run Pig Latin jobs on a Hadoop cluster in Azure HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/09/2017
ms.author: larryfr
ms.openlocfilehash: ed5df94ec3455803cb3ea60f3a958132e0312ede
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552103"
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-curl"></a><span data-ttu-id="023ef-103">Run Pig jobs with Hadoop on HDInsight by using Curl</span><span class="sxs-lookup"><span data-stu-id="023ef-103">Run Pig jobs with Hadoop on HDInsight by using Curl</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="023ef-104">In this document, you learn how to use Curl to run Pig Latin jobs on an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-104">In this document, you learn how to use Curl to run Pig Latin jobs on an Azure HDInsight cluster.</span></span> <span data-ttu-id="023ef-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span><span class="sxs-lookup"><span data-stu-id="023ef-105">The Pig Latin programming language allows you to describe transformations that are applied to the input data to produce the desired output.</span></span>

<span data-ttu-id="023ef-106">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Pig jobs.</span><span class="sxs-lookup"><span data-stu-id="023ef-106">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Pig jobs.</span></span> <span data-ttu-id="023ef-107">This works by using the WebHCat REST API (formerly known as Templeton) that is provided by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-107">This works by using the WebHCat REST API (formerly known as Templeton) that is provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="023ef-108">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="023ef-108">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Linux-based HDInsight Tips](hdinsight-hadoop-linux-information.md).</span></span>

## <a id="prereq"></a><span data-ttu-id="023ef-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="023ef-109">Prerequisites</span></span>

<span data-ttu-id="023ef-110">To complete the steps in this article, you need the following:</span><span class="sxs-lookup"><span data-stu-id="023ef-110">To complete the steps in this article, you need the following:</span></span>

* <span data-ttu-id="023ef-111">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span><span class="sxs-lookup"><span data-stu-id="023ef-111">An Azure HDInsight (Hadoop on HDInsight) cluster (Linux-based or Windows-based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="023ef-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="023ef-112">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="023ef-113">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="023ef-113">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* [<span data-ttu-id="023ef-114">Curl</span><span class="sxs-lookup"><span data-stu-id="023ef-114">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="023ef-115">jq</span><span class="sxs-lookup"><span data-stu-id="023ef-115">jq</span></span>](http://stedolan.github.io/jq/)

## <a id="curl"></a><span data-ttu-id="023ef-116">Run Pig jobs by using Curl</span><span class="sxs-lookup"><span data-stu-id="023ef-116">Run Pig jobs by using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="023ef-117">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the administrator user name and password for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-117">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the administrator user name and password for the HDInsight cluster.</span></span> <span data-ttu-id="023ef-118">You must also use the cluster name as part of the Uniform Resource Identifier (URI) that is used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="023ef-118">You must also use the cluster name as part of the Uniform Resource Identifier (URI) that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="023ef-119">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="023ef-119">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="023ef-120">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-120">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="023ef-121">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="023ef-121">The REST API is secured via [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="023ef-122">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="023ef-122">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>

1. <span data-ttu-id="023ef-123">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="023ef-123">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status

    <span data-ttu-id="023ef-124">You should receive a response similar to the following:</span><span class="sxs-lookup"><span data-stu-id="023ef-124">You should receive a response similar to the following:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="023ef-125">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="023ef-125">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="023ef-126">**-u**: The user name and password used to authenticate the request</span><span class="sxs-lookup"><span data-stu-id="023ef-126">**-u**: The user name and password used to authenticate the request</span></span>
    * <span data-ttu-id="023ef-127">**-G**: Indicates that this is a GET request</span><span class="sxs-lookup"><span data-stu-id="023ef-127">**-G**: Indicates that this is a GET request</span></span>

     <span data-ttu-id="023ef-128">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="023ef-128">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="023ef-129">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="023ef-129">The path, **/status**, indicates that the request is to return the status of WebHCat (also known as Templeton) for the server.</span></span>

2. <span data-ttu-id="023ef-130">Use the following code to submit a Pig Latin job to the cluster:</span><span class="sxs-lookup"><span data-stu-id="023ef-130">Use the following code to submit a Pig Latin job to the cluster:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig

    <span data-ttu-id="023ef-131">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="023ef-131">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="023ef-132">**-d**: Because `-G` is not used, the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="023ef-132">**-d**: Because `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="023ef-133">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="023ef-133">`-d` specifies the data values that are sent with the request.</span></span>

    * <span data-ttu-id="023ef-134">**user.name**: The user who is running the command</span><span class="sxs-lookup"><span data-stu-id="023ef-134">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="023ef-135">**execute**: The Pig Latin statements to execute</span><span class="sxs-lookup"><span data-stu-id="023ef-135">**execute**: The Pig Latin statements to execute</span></span>
    * <span data-ttu-id="023ef-136">**statusdir**: The directory that the status for this job will be written to</span><span class="sxs-lookup"><span data-stu-id="023ef-136">**statusdir**: The directory that the status for this job will be written to</span></span>

    > [!NOTE]
    > <span data-ttu-id="023ef-137">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span><span class="sxs-lookup"><span data-stu-id="023ef-137">Notice that the spaces in Pig Latin statements are replaced by the `+` character when used with Curl.</span></span>

    <span data-ttu-id="023ef-138">This command should return a job ID that can be used to check the status of the job, for example:</span><span class="sxs-lookup"><span data-stu-id="023ef-138">This command should return a job ID that can be used to check the status of the job, for example:</span></span>

        {"id":"job_1415651640909_0026"}

3. <span data-ttu-id="023ef-139">To check the status of the job, use the following command.</span><span class="sxs-lookup"><span data-stu-id="023ef-139">To check the status of the job, use the following command.</span></span> <span data-ttu-id="023ef-140">Replace **JOBID** with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="023ef-140">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="023ef-141">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="023ef-141">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>

        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state

    <span data-ttu-id="023ef-142">If the job has finished, the state will be **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="023ef-142">If the job has finished, the state will be **SUCCEEDED**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="023ef-143">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="023ef-143">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job, and jq is used to retrieve only the state value.</span></span>

## <a id="results"></a><span data-ttu-id="023ef-144">View results</span><span class="sxs-lookup"><span data-stu-id="023ef-144">View results</span></span>

<span data-ttu-id="023ef-145">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from the default storage used by the cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-145">When the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from the default storage used by the cluster.</span></span> <span data-ttu-id="023ef-146">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/pigcurl**.</span><span class="sxs-lookup"><span data-stu-id="023ef-146">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **/example/pigcurl**.</span></span>

<span data-ttu-id="023ef-147">The backing store for HDInsight can be either Azure Storage or Azure Data Lake Store, and there are a variety of ways to get at the data depending on which one you use.</span><span class="sxs-lookup"><span data-stu-id="023ef-147">The backing store for HDInsight can be either Azure Storage or Azure Data Lake Store, and there are a variety of ways to get at the data depending on which one you use.</span></span> <span data-ttu-id="023ef-148">For more information on how to work with Azure Storage and Azure Data Lake Store, see the [HDFS, Blob storage, and Data Lake Store](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) section of the HDInsight on Linux document.</span><span class="sxs-lookup"><span data-stu-id="023ef-148">For more information on how to work with Azure Storage and Azure Data Lake Store, see the [HDFS, Blob storage, and Data Lake Store](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) section of the HDInsight on Linux document.</span></span>

## <a id="summary"></a><span data-ttu-id="023ef-149">Summary</span><span class="sxs-lookup"><span data-stu-id="023ef-149">Summary</span></span>

<span data-ttu-id="023ef-150">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="023ef-150">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Pig jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="023ef-151">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="023ef-151">For more information about the REST interface used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>

## <a id="nextsteps"></a><span data-ttu-id="023ef-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="023ef-152">Next steps</span></span>

<span data-ttu-id="023ef-153">For general information about Pig on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="023ef-153">For general information about Pig on HDInsight:</span></span>

* [<span data-ttu-id="023ef-154">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="023ef-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="023ef-155">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="023ef-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="023ef-156">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="023ef-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="023ef-157">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="023ef-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
