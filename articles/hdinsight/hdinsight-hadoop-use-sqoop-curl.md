---
title: Use Hadoop Sqoop with Curl in HDInsight | Microsoft Docs
description: Learn how to remotely submit Sqoop jobs to HDInsight using Curl.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: b402968ad5404db9fefc09327c8bc3c1bd26953d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551289"
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a><span data-ttu-id="4be19-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span><span class="sxs-lookup"><span data-stu-id="4be19-103">Run Sqoop jobs with Hadoop in HDInsight with Curl</span></span>
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="4be19-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4be19-104">Learn how to use Curl to run Sqoop jobs on a Hadoop cluster in HDInsight.</span></span>

<span data-ttu-id="4be19-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span><span class="sxs-lookup"><span data-stu-id="4be19-105">Curl is used to demonstrate how you can interact with HDInsight by using raw HTTP requests to run, monitor, and retrieve the results of Sqoop jobs.</span></span> <span data-ttu-id="4be19-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4be19-106">This works by using the WebHCat REST API (formerly known as Templeton) provided by your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4be19-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="4be19-107">If you are already familiar with using Linux-based Hadoop servers, but are new to HDInsight, see [Information about using HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="4be19-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4be19-108">Prerequisites</span></span>
<span data-ttu-id="4be19-109">To complete the steps in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="4be19-109">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="4be19-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span><span class="sxs-lookup"><span data-stu-id="4be19-110">A Hadoop on HDInsight cluster (Linux or Windows-based)</span></span>
* [<span data-ttu-id="4be19-111">Curl</span><span class="sxs-lookup"><span data-stu-id="4be19-111">Curl</span></span>](http://curl.haxx.se/)
* [<span data-ttu-id="4be19-112">jq</span><span class="sxs-lookup"><span data-stu-id="4be19-112">jq</span></span>](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a><span data-ttu-id="4be19-113">Submit Sqoop jobs by using Curl</span><span class="sxs-lookup"><span data-stu-id="4be19-113">Submit Sqoop jobs by using Curl</span></span>
> [!NOTE]
> <span data-ttu-id="4be19-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="4be19-114">When using Curl or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span> <span data-ttu-id="4be19-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span><span class="sxs-lookup"><span data-stu-id="4be19-115">You must also use the cluster name as part of the Uniform Resource Identifier (URI) used to send the requests to the server.</span></span>
> 
> <span data-ttu-id="4be19-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span><span class="sxs-lookup"><span data-stu-id="4be19-116">For the commands in this section, replace **USERNAME** with the user to authenticate to the cluster, and replace **PASSWORD** with the password for the user account.</span></span> <span data-ttu-id="4be19-117">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="4be19-117">Replace **CLUSTERNAME** with the name of your cluster.</span></span>
> 
> <span data-ttu-id="4be19-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="4be19-118">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="4be19-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span><span class="sxs-lookup"><span data-stu-id="4be19-119">You should always make requests by using Secure HTTP (HTTPS) to help ensure that your credentials are securely sent to the server.</span></span>
> 
> 

1. <span data-ttu-id="4be19-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="4be19-120">From a command line, use the following command to verify that you can connect to your HDInsight cluster:</span></span>
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    <span data-ttu-id="4be19-121">You should receive a response similar to the following:</span><span class="sxs-lookup"><span data-stu-id="4be19-121">You should receive a response similar to the following:</span></span>
   
        {"status":"ok","version":"v1"}
   
    <span data-ttu-id="4be19-122">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="4be19-122">The parameters used in this command are as follows:</span></span>
   
   * <span data-ttu-id="4be19-123">**-u** - The user name and password used to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="4be19-123">**-u** - The user name and password used to authenticate the request.</span></span>
   * <span data-ttu-id="4be19-124">**-G** - Indicates that this is a GET request.</span><span class="sxs-lookup"><span data-stu-id="4be19-124">**-G** - Indicates that this is a GET request.</span></span>
     
     <span data-ttu-id="4be19-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="4be19-125">The beginning of the URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, will be the same for all requests.</span></span> <span data-ttu-id="4be19-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="4be19-126">The path, **/status**, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> 
2. <span data-ttu-id="4be19-127">Use the following to submit a sqoop job:</span><span class="sxs-lookup"><span data-stu-id="4be19-127">Use the following to submit a sqoop job:</span></span>

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasbs:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    <span data-ttu-id="4be19-128">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="4be19-128">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="4be19-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span><span class="sxs-lookup"><span data-stu-id="4be19-129">**-d** - Since `-G` is not used, the request defaults to the POST method.</span></span> <span data-ttu-id="4be19-130">`-d` specifies the data values that are sent with the request.</span><span class="sxs-lookup"><span data-stu-id="4be19-130">`-d` specifies the data values that are sent with the request.</span></span>

        * <span data-ttu-id="4be19-131">**user.name** - The user that is running the command.</span><span class="sxs-lookup"><span data-stu-id="4be19-131">**user.name** - The user that is running the command.</span></span>

        * <span data-ttu-id="4be19-132">**command** - The Sqoop command to execute.</span><span class="sxs-lookup"><span data-stu-id="4be19-132">**command** - The Sqoop command to execute.</span></span>

        * <span data-ttu-id="4be19-133">**statusdir** - The directory that the status for this job will be written to.</span><span class="sxs-lookup"><span data-stu-id="4be19-133">**statusdir** - The directory that the status for this job will be written to.</span></span>

    <span data-ttu-id="4be19-134">This command should return a job ID that can be used to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="4be19-134">This command should return a job ID that can be used to check the status of the job.</span></span>

        {"id":"job_1415651640909_0026"}

1. <span data-ttu-id="4be19-135">To check the status of the job, use the following command.</span><span class="sxs-lookup"><span data-stu-id="4be19-135">To check the status of the job, use the following command.</span></span> <span data-ttu-id="4be19-136">Replace **JOBID** with the value returned in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4be19-136">Replace **JOBID** with the value returned in the previous step.</span></span> <span data-ttu-id="4be19-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span><span class="sxs-lookup"><span data-stu-id="4be19-137">For example, if the return value was `{"id":"job_1415651640909_0026"}`, then **JOBID** would be `job_1415651640909_0026`.</span></span>
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    <span data-ttu-id="4be19-138">If the job has finished, the state will be **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="4be19-138">If the job has finished, the state will be **SUCCEEDED**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4be19-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span><span class="sxs-lookup"><span data-stu-id="4be19-139">This Curl request returns a JavaScript Object Notation (JSON) document with information about the job; jq is used to retrieve only the state value.</span></span>
   > 
   > 
2. <span data-ttu-id="4be19-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4be19-140">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="4be19-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasbs:///example/curl**.</span><span class="sxs-lookup"><span data-stu-id="4be19-141">The `statusdir` parameter passed with the query contains the location of the output file; in this case, **wasbs:///example/curl**.</span></span> <span data-ttu-id="4be19-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4be19-142">This address stores the output of the job in the **example/curl** directory on the default storage container used by your HDInsight cluster.</span></span>
   
    <span data-ttu-id="4be19-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="4be19-143">You can list and download these files by using the [Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="4be19-144">For example, to list files in **example/curl**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4be19-144">For example, to list files in **example/curl**, use the following command:</span></span>
   
        azure storage blob list <container-name> example/curl
   
    <span data-ttu-id="4be19-145">To download a file, use the following:</span><span class="sxs-lookup"><span data-stu-id="4be19-145">To download a file, use the following:</span></span>
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > <span data-ttu-id="4be19-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span><span class="sxs-lookup"><span data-stu-id="4be19-146">You must either specify the storage account name that contains the blob by using the `-a` and `-k` parameters, or set the **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** environment variables.</span></span> <span data-ttu-id="4be19-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span><span class="sxs-lookup"><span data-stu-id="4be19-147">See <a href="hdinsight-upload-data.md" target="_blank" for more information.</span></span>
   > 
   > 

## <a name="limitations"></a><span data-ttu-id="4be19-148">Limitations</span><span class="sxs-lookup"><span data-stu-id="4be19-148">Limitations</span></span>
* <span data-ttu-id="4be19-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span><span class="sxs-lookup"><span data-stu-id="4be19-149">Bulk export - With Linux-based HDInsight, the Sqoop connector used to export data to Microsoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>
* <span data-ttu-id="4be19-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span><span class="sxs-lookup"><span data-stu-id="4be19-150">Batching - With Linux-based HDInsight, When using the `-batch` switch when performing inserts, Sqoop will perform multiple inserts instead of batching the insert operations.</span></span>

## <a name="summary"></a><span data-ttu-id="4be19-151">Summary</span><span class="sxs-lookup"><span data-stu-id="4be19-151">Summary</span></span>
<span data-ttu-id="4be19-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4be19-152">As demonstrated in this document, you can use a raw HTTP request to run, monitor, and view the results of Sqoop jobs on your HDInsight cluster.</span></span>

<span data-ttu-id="4be19-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span><span class="sxs-lookup"><span data-stu-id="4be19-153">For more information on the REST interface used in this article, see the <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Sqoop REST API guide</a>.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be19-154">Next steps</span><span class="sxs-lookup"><span data-stu-id="4be19-154">Next steps</span></span>
<span data-ttu-id="4be19-155">For general information on Hive with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4be19-155">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="4be19-156">Use Sqoop with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4be19-156">Use Sqoop with Hadoop on HDInsight</span></span>](hdinsight-use-sqoop.md)

<span data-ttu-id="4be19-157">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4be19-157">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4be19-158">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4be19-158">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4be19-159">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4be19-159">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4be19-160">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="4be19-160">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

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


