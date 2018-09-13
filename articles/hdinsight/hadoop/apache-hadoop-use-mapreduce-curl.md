---
title: Use MapReduce and Curl with Hadoop in HDInsight - Azure
description: Learn how to remotely run MapReduce jobs with Hadoop on HDInsight using Curl.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.author: jasonh
ms.openlocfilehash: f497184b05432d6e32883bb3470f7e4da5fe550f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857260"
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a><span data-ttu-id="31d42-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="31d42-103">Run MapReduce jobs with Hadoop on HDInsight using REST</span></span>

<span data-ttu-id="31d42-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="31d42-104">Learn how to use the WebHCat REST API to run MapReduce jobs on a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="31d42-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span><span class="sxs-lookup"><span data-stu-id="31d42-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run MapReduce jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="31d42-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](../hdinsight-hadoop-linux-information.md) document.</span><span class="sxs-lookup"><span data-stu-id="31d42-106">If you are already familiar with using Linux-based Hadoop servers, but you are new to HDInsight, see the [What you need to know about Linux-based Hadoop on HDInsight](../hdinsight-hadoop-linux-information.md) document.</span></span>


## <a id="prereq"></a><span data-ttu-id="31d42-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31d42-107">Prerequisites</span></span>

* <span data-ttu-id="31d42-108">A Hadoop on HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="31d42-108">A Hadoop on HDInsight cluster</span></span>
* <span data-ttu-id="31d42-109">Windows PowerShell or [Curl](http://curl.haxx.se/) and [jq](http://stedolan.github.io/jq/)</span><span class="sxs-lookup"><span data-stu-id="31d42-109">Windows PowerShell or [Curl](http://curl.haxx.se/) and [jq](http://stedolan.github.io/jq/)</span></span>

## <a id="curl"></a><span data-ttu-id="31d42-110">Run a MapReduce job</span><span class="sxs-lookup"><span data-stu-id="31d42-110">Run a MapReduce job</span></span>

> [!NOTE]
> <span data-ttu-id="31d42-111">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span><span class="sxs-lookup"><span data-stu-id="31d42-111">When you use Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the HDInsight cluster administrator user name and password.</span></span> <span data-ttu-id="31d42-112">You must use the cluster name as part of the URI that is used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="31d42-112">You must use the cluster name as part of the URI that is used to send the requests to the server.</span></span>
>
> <span data-ttu-id="31d42-113">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="31d42-113">The REST API is secured by using [basic access authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="31d42-114">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="31d42-114">You should always make requests by using HTTPS to ensure that your credentials are securely sent to the server.</span></span>

1. <span data-ttu-id="31d42-115">To set the cluster login that is used by the scripts in this document, use one of the followig commands:</span><span class="sxs-lookup"><span data-stu-id="31d42-115">To set the cluster login that is used by the scripts in this document, use one of the followig commands:</span></span>

    ```bash
    read -p "Enter your cluster login account name: " LOGIN
    ```

    ```powershell
    $creds = Get-Credential -UserName admin -Message "Enter the cluster login name and password"
    ```

2. <span data-ttu-id="31d42-116">To set the cluster name, use one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="31d42-116">To set the cluster name, use one of the following commands:</span></span>

    ```bash
    read -p "Enter the HDInsight cluster name: " CLUSTERNAME
    ```

    ```powershell
    $clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
    ```

3. <span data-ttu-id="31d42-117">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="31d42-117">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>

    ```bash
    curl -u $LOGIN -G https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clustername.azurehdinsight.net/templeton/v1/status" `
        -Credential $creds `
        -UseBasicParsing
    $resp.Content
    ```

    <span data-ttu-id="31d42-118">You receive a response similar to the following JSON:</span><span class="sxs-lookup"><span data-stu-id="31d42-118">You receive a response similar to the following JSON:</span></span>

        {"status":"ok","version":"v1"}

    <span data-ttu-id="31d42-119">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="31d42-119">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="31d42-120">**-u**: Indicates the user name and password used to authenticate the request</span><span class="sxs-lookup"><span data-stu-id="31d42-120">**-u**: Indicates the user name and password used to authenticate the request</span></span>
   * <span data-ttu-id="31d42-121">**-G**: Indicates that this operation is a GET request</span><span class="sxs-lookup"><span data-stu-id="31d42-121">**-G**: Indicates that this operation is a GET request</span></span>

   <span data-ttu-id="31d42-122">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="31d42-122">The beginning of the URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, is the same for all requests.</span></span>

4. <span data-ttu-id="31d42-123">To submit a MapReduce job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="31d42-123">To submit a MapReduce job, use the following command:</span></span>

    ```bash
    JOBID=`curl -u $LOGIN -d user.name=$LOGIN -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/output https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar | jq .id`
    echo $JOBID
    ```

    ```powershell
    $reqParams = @{}
    $reqParams."user.name" = "admin"
    $reqParams.jar = "/example/jars/hadoop-mapreduce-examples.jar"
    $reqParams.class = "wordcount"
    $reqParams.arg = @()
    $reqParams.arg += "/example/data/gutenberg/davinci.txt"
    $reqparams.arg += "/example/data/output"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/mapreduce/jar" `
       -Credential $creds `
       -Body $reqParams `
       -Method POST `
       -UseBasicParsing
    $jobID = (ConvertFrom-Json $resp.Content).id
    $jobID
    ```

    <span data-ttu-id="31d42-124">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span><span class="sxs-lookup"><span data-stu-id="31d42-124">The end of the URI (/mapreduce/jar) tells WebHCat that this request starts a MapReduce job from a class in a jar file.</span></span> <span data-ttu-id="31d42-125">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="31d42-125">The parameters used in this command are as follows:</span></span>

   * <span data-ttu-id="31d42-126">**-d**: `-G` is not used, so the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="31d42-126">**-d**: `-G` is not used, so the request defaults to the POST method.</span></span> <span data-ttu-id="31d42-127">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="31d42-127">`-d` specifies the data values that are sent with the request.</span></span>
    * <span data-ttu-id="31d42-128">**user.name**: The user who is running the command</span><span class="sxs-lookup"><span data-stu-id="31d42-128">**user.name**: The user who is running the command</span></span>
    * <span data-ttu-id="31d42-129">**jar**: The location of the jar file that contains class to be ran</span><span class="sxs-lookup"><span data-stu-id="31d42-129">**jar**: The location of the jar file that contains class to be ran</span></span>
    * <span data-ttu-id="31d42-130">**class**: The class that contains the MapReduce logic</span><span class="sxs-lookup"><span data-stu-id="31d42-130">**class**: The class that contains the MapReduce logic</span></span>
    * <span data-ttu-id="31d42-131">**arg**: The arguments to be passed to the MapReduce job.</span><span class="sxs-lookup"><span data-stu-id="31d42-131">**arg**: The arguments to be passed to the MapReduce job.</span></span> <span data-ttu-id="31d42-132">In this case, the input text file and the directory that are used for the output</span><span class="sxs-lookup"><span data-stu-id="31d42-132">In this case, the input text file and the directory that are used for the output</span></span>

   <span data-ttu-id="31d42-133">This command should return a job ID that can be used to check the status of the job:</span><span class="sxs-lookup"><span data-stu-id="31d42-133">This command should return a job ID that can be used to check the status of the job:</span></span>

       job_1415651640909_0026

5. <span data-ttu-id="31d42-134">To check the status of the job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="31d42-134">To check the status of the job, use the following command:</span></span>

    ```bash
    curl -G -u $LOGIN -d user.name=$LOGIN https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/$JOBID | jq .status.state
    ```

    ```powershell
    $reqParams=@{"user.name"="admin"}
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/jobs/$jobID" `
       -Credential $creds `
       -Body $reqParams `
       -UseBasicParsing
    # ConvertFrom-JSON can't handle duplicate names with different case
    # So change one to prevent the error
    $fixDup=$resp.Content.Replace("jobID","job_ID")
    (ConvertFrom-Json $fixDup).status.state
    ```

    <span data-ttu-id="31d42-135">If the job is complete, the state returned is `SUCCEEDED`.</span><span class="sxs-lookup"><span data-stu-id="31d42-135">If the job is complete, the state returned is `SUCCEEDED`.</span></span>

   > [!NOTE]
   > <span data-ttu-id="31d42-136">This Curl request returns a JSON document with information about the job.</span><span class="sxs-lookup"><span data-stu-id="31d42-136">This Curl request returns a JSON document with information about the job.</span></span> <span data-ttu-id="31d42-137">Jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="31d42-137">Jq is used to retrieve only the state value.</span></span>

6. <span data-ttu-id="31d42-138">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="31d42-138">When the state of the job has changed to `SUCCEEDED`, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="31d42-139">The `statusdir` parameter that is passed with the query contains the location of the output file.</span><span class="sxs-lookup"><span data-stu-id="31d42-139">The `statusdir` parameter that is passed with the query contains the location of the output file.</span></span> <span data-ttu-id="31d42-140">In this example, the location is `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="31d42-140">In this example, the location is `/example/curl`.</span></span> <span data-ttu-id="31d42-141">This address stores the output of the job in the clusters default storage at `/example/curl`.</span><span class="sxs-lookup"><span data-stu-id="31d42-141">This address stores the output of the job in the clusters default storage at `/example/curl`.</span></span>

<span data-ttu-id="31d42-142">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="31d42-142">You can list and download these files by using the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="31d42-143">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="31d42-143">For more information on working with blobs from the Azure CLI, see the [Using the Azure CLI 2.0 with Azure Storage](../../storage/common/storage-azure-cli.md#create-and-manage-blobs) document.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="31d42-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="31d42-144">Next steps</span></span>

<span data-ttu-id="31d42-145">For general information about MapReduce jobs in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31d42-145">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="31d42-146">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="31d42-146">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="31d42-147">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="31d42-147">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="31d42-148">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="31d42-148">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="31d42-149">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="31d42-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="31d42-150">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span><span class="sxs-lookup"><span data-stu-id="31d42-150">For more information about the REST interface that is used in this article, see the [WebHCat Reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).</span></span>
