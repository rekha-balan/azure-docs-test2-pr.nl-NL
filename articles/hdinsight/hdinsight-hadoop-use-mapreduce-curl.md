---
title: Use MapReduce and Curl with Hadoop in HDInsight | Microsoft Docs
description: Learn how to remotely run MapReduce jobs with Hadoop on HDInsight using Curl.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/11/2017
ms.author: larryfr
ms.openlocfilehash: ee7f4536a2d58966f0bcecf19f2a5fec5df68bc2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553997"
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="10a0d-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="10a0d-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="10a0d-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="10a0d-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="10a0d-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="10a0d-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="10a0d-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="10a0d-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](hdinsight-hadoop-linux-information.md) document.</span></span>


## <a id="prereq"></a><span data-ttu-id="10a0d-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="10a0d-107">Prerequisites</span></span>

* <span data-ttu-id="10a0d-108">A Hadoop on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="10a0d-108">A Hadoop on HDInsight cluster</span></span>
* [<span data-ttu-id="10a0d-109">Curl</span><span class="sxs-lookup"><span data-stu-id="10a0d-109">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="10a0d-110">jq</span><span class="sxs-lookup"><span data-stu-id="10a0d-110">jq</span></span>](http://stedolan.github.io/jq/)

## <a id="curl"></a><span data-ttu-id="10a0d-111">Run MapReduce jobs using Curl</span><span class="sxs-lookup"><span data-stu-id="10a0d-111">Run MapReduce jobs using Curl</span></span>

> [!NOTE]
> <span data-ttu-id="10a0d-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span><span class="sxs-lookup"><span data-stu-id="10a0d-112">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="10a0d-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="10a0d-113">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="10a0d-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="10a0d-114">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="10a0d-115">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="10a0d-115">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
>
> <span data-ttu-id="10a0d-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="10a0d-116">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="10a0d-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="10a0d-117">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>


1. <span data-ttu-id="10a0d-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="10a0d-118">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    <span data-ttu-id="10a0d-119">You should receive a response similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="10a0d-119">You should receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="10a0d-120">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="10a0d-120">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="10a0d-121">**-u**: Indicates the user name and password used to authenticate the request</span><span class="sxs-lookup"><span data-stu-id="10a0d-121">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="10a0d-122">**-G**: Indicates that this operation is a GET request</span><span class="sxs-lookup"><span data-stu-id="10a0d-122">**-G**: Indicates that this operation is a GET request</span></span>

     <span data-ttu-id="10a0d-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="10a0d-123">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

2. <span data-ttu-id="10a0d-124">To submit a MapReduce job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="10a0d-124">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    <span data-ttu-id="10a0d-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span><span class="sxs-lookup"><span data-stu-id="10a0d-125">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="10a0d-126">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="10a0d-126">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="10a0d-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="10a0d-127">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="10a0d-128">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="10a0d-128">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="10a0d-129">**user.name**: The user who is running the command</span><span class="sxs-lookup"><span data-stu-id="10a0d-129">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="10a0d-130">**jar**: The location of the jar file that contains class to be ran</span><span class="sxs-lookup"><span data-stu-id="10a0d-130">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="10a0d-131">**class**: The class that contains the MapReduce logic</span><span class="sxs-lookup"><span data-stu-id="10a0d-131">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="10a0d-132">**arg**: The arguments to be passed to the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="10a0d-132">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="10a0d-133">In this case, the input text file and the directory that are used for the output</span><span class="sxs-lookup"><span data-stu-id="10a0d-133">In this case, the input text file and the directory that are used for the output</span></span>

     <span data-ttu-id="10a0d-134">This command should return a job ID that can be used to check the status of the job:</span><span class="sxs-lookup"><span data-stu-id="10a0d-134">This command should return a job ID that can be used to check the status of the job:</span></span>

       <span data-ttu-id="10a0d-135">{"id":"job_1415651640909_0026"}</span><span class="sxs-lookup"><span data-stu-id="10a0d-135">{"id":"job_1415651640909_0026"}</span></span>

3. <span data-ttu-id="10a0d-136">To check the status of the job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="10a0d-136">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    <span data-ttu-id="10a0d-137">Replace the **JOBID** with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="10a0d-137">Replace the **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="10a0d-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="10a0d-138">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then the JOBID would be `job_1415651640909_0026`.</span></span>

    <span data-ttu-id="10a0d-139">If the job is complete, the state returned is `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="10a0d-139">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="10a0d-140">This Curl request returns a JSON document with information about the job.</span><span class="sxs-lookup"><span data-stu-id="10a0d-140">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="10a0d-141">Jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="10a0d-141">Jq is used to retrieve only the state value.</span></span>

4. <span data-ttu-id="10a0d-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="10a0d-142">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="10a0d-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span><span class="sxs-lookup"><span data-stu-id="10a0d-143">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="10a0d-144">In this example, the location is `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="10a0d-144">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="10a0d-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="10a0d-145">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="10a0d-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="10a0d-146">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="10a0d-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/storage-azure-cli.md#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="10a0d-147">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../storage/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="10a0d-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="10a0d-148">Next steps</span></span>

<span data-ttu-id="10a0d-149">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="10a0d-149">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="10a0d-150">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="10a0d-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="10a0d-151">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="10a0d-151">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="10a0d-152">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="10a0d-152">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="10a0d-153">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="10a0d-153">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="10a0d-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="10a0d-154">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>