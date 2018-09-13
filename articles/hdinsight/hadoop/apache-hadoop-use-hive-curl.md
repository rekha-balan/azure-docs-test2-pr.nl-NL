---
title: Use Hadoop Hive with Curl in HDInsight - Azure
description: Learn how to remotely submit Pig jobs to HDInsight using Curl.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: jasonh
ms.openlocfilehash: d8816965fb1ab870d7bd93cd1ace45c4e6e57de6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871284"
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a><span data-ttu-id="72177-103">Run Hive queries with Hadoop in HDInsight using REST</span><span class="sxs-lookup"><span data-stu-id="72177-103">Run Hive queries with Hadoop in HDInsight using REST</span></span>

[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="72177-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="72177-104">Learn how to use the WebHCat REST API to run Hive queries with Hadoop on Azure HDInsight cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72177-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72177-105">Prerequisites</span></span>

* <span data-ttu-id="72177-106">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="72177-106">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="72177-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="72177-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="72177-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="72177-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="72177-109">A REST client.</span><span class="sxs-lookup"><span data-stu-id="72177-109">A REST client.</span></span> <span data-ttu-id="72177-110">This document uses Windows PowerShell and [Curl](http://curl.haxx.se/) examples.</span><span class="sxs-lookup"><span data-stu-id="72177-110">This document uses Windows PowerShell and [Curl](http://curl.haxx.se/) examples.</span></span>

    > [!NOTE]
    > <span data-ttu-id="72177-111">Azure PowerShell provides dedicated cmdlets for working with Hive on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72177-111">Azure PowerShell provides dedicated cmdlets for working with Hive on HDInsight.</span></span> <span data-ttu-id="72177-112">For more information, see the [Use Hive with Azure PowerShell](apache-hadoop-use-hive-powershell.md) document.</span><span class="sxs-lookup"><span data-stu-id="72177-112">For more information, see the [Use Hive with Azure PowerShell](apache-hadoop-use-hive-powershell.md) document.</span></span>

<span data-ttu-id="72177-113">This document also uses Windows PowerShell and [Jq](http://stedolan.github.io/jq/) to process the JSON data returned from REST requests.</span><span class="sxs-lookup"><span data-stu-id="72177-113">This document also uses Windows PowerShell and [Jq](http://stedolan.github.io/jq/) to process the JSON data returned from REST requests.</span></span>

## <a id="curl"></a><span data-ttu-id="72177-114">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="72177-114">Run a Hive query</span></span>

> [!NOTE]
> <span data-ttu-id="72177-115">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span><span class="sxs-lookup"><span data-stu-id="72177-115">When using cURL or any other REST communication with WebHCat, you must authenticate the requests by providing the user name and password for the HDInsight cluster administrator.</span></span>
>
> <span data-ttu-id="72177-116">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span><span class="sxs-lookup"><span data-stu-id="72177-116">The REST API is secured via [basic authentication](http://en.wikipedia.org/wiki/Basic_access_authentication).</span></span> <span data-ttu-id="72177-117">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="72177-117">To help ensure that your credentials are securely sent to the server, always make requests by using Secure HTTP (HTTPS).</span></span>

1. <span data-ttu-id="72177-118">To set the cluster login that is used by the scripts in this document, use one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="72177-118">To set the cluster login that is used by the scripts in this document, use one of the following commands:</span></span>

    ```bash
    read -p "Enter your cluster login account name: " LOGIN
    ```

    ```powershell
    $creds = Get-Credential -UserName admin -Message "Enter the cluster login name and password"
    ```

2. <span data-ttu-id="72177-119">To set the cluster name, use one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="72177-119">To set the cluster name, use one of the following commands:</span></span>

    ```bash
    read -p "Enter the HDInsight cluster name: " CLUSTERNAME
    ```

    ```powershell
    $clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
    ```

3. <span data-ttu-id="72177-120">To verify that you can connect to your HDInsight cluster, use one of the following commands:</span><span class="sxs-lookup"><span data-stu-id="72177-120">To verify that you can connect to your HDInsight cluster, use one of the following commands:</span></span>

    ```bash
    curl -u $LOGIN -G https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/status)
    ```
    
    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/status" `
       -Credential $creds `
       -UseBasicParsing
    $resp.Content
    ```

    <span data-ttu-id="72177-121">You receive a response similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="72177-121">You receive a response similar to the following text:</span></span>

    ```json
    {"status":"ok","version":"v1"}
    ```

    <span data-ttu-id="72177-122">The parameters used in this command are as follows:</span><span class="sxs-lookup"><span data-stu-id="72177-122">The parameters used in this command are as follows:</span></span>

    * <span data-ttu-id="72177-123">`-u` - The user name and password used to authenticate the request.</span><span class="sxs-lookup"><span data-stu-id="72177-123">`-u` - The user name and password used to authenticate the request.</span></span>
    * <span data-ttu-id="72177-124">`-G` - Indicates that this request is a GET operation.</span><span class="sxs-lookup"><span data-stu-id="72177-124">`-G` - Indicates that this request is a GET operation.</span></span>

   <span data-ttu-id="72177-125">The beginning of the URL, `https://$CLUSTERNAME.azurehdinsight.net/templeton/v1`, is the same for all requests.</span><span class="sxs-lookup"><span data-stu-id="72177-125">The beginning of the URL, `https://$CLUSTERNAME.azurehdinsight.net/templeton/v1`, is the same for all requests.</span></span> <span data-ttu-id="72177-126">The path, `/status`, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span><span class="sxs-lookup"><span data-stu-id="72177-126">The path, `/status`, indicates that the request is to return a status of WebHCat (also known as Templeton) for the server.</span></span> <span data-ttu-id="72177-127">You can also request the version of Hive by using the following command:</span><span class="sxs-lookup"><span data-stu-id="72177-127">You can also request the version of Hive by using the following command:</span></span>

    ```bash
    curl -u $LOGIN -G https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

    ```powershell
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/version/hive" `
       -Credential $creds `
       -UseBasicParsing
    $resp.Content
    ```

    <span data-ttu-id="72177-128">This request returns a response similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="72177-128">This request returns a response similar to the following text:</span></span>

    ```json
        {"module":"hive","version":"0.13.0.2.1.6.0-2103"}
    ```

4. <span data-ttu-id="72177-129">Use the following to create a table named **log4jLogs**:</span><span class="sxs-lookup"><span data-stu-id="72177-129">Use the following to create a table named **log4jLogs**:</span></span>

    ```bash
    JOBID=`curl -s -u $LOGIN -d user.name=$LOGIN -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/rest" https://$CLUSTERNAME.azurehdinsight.net/templeton/v1/hive | jq .id`
    echo $JOBID
    ```

    ```powershell
    $reqParams = @{"user.name"="admin";"execute"="set hive.execution.engine=tez;DROP TABLE log4jLogs;CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED BY ' ' STORED AS TEXTFILE LOCATION '/example/data/;SELECT t4 AS sev,COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;";"statusdir"="/example/rest"}
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/templeton/v1/hive" `
       -Credential $creds `
       -Body $reqParams `
       -Method POST `
       -UseBasicParsing
    $jobID = (ConvertFrom-Json $resp.Content).id
    $jobID
    ```

    <span data-ttu-id="72177-130">This request uses the POST method, which sends data as part of the request to the REST API.</span><span class="sxs-lookup"><span data-stu-id="72177-130">This request uses the POST method, which sends data as part of the request to the REST API.</span></span> <span data-ttu-id="72177-131">The following data values are sent with the request:</span><span class="sxs-lookup"><span data-stu-id="72177-131">The following data values are sent with the request:</span></span>

     * <span data-ttu-id="72177-132">`user.name` - The user that is running the command.</span><span class="sxs-lookup"><span data-stu-id="72177-132">`user.name` - The user that is running the command.</span></span>
     * <span data-ttu-id="72177-133">`execute` - The HiveQL statements to execute.</span><span class="sxs-lookup"><span data-stu-id="72177-133">`execute` - The HiveQL statements to execute.</span></span>
     * <span data-ttu-id="72177-134">`statusdir` - The directory that the status for this job is written to.</span><span class="sxs-lookup"><span data-stu-id="72177-134">`statusdir` - The directory that the status for this job is written to.</span></span>

   <span data-ttu-id="72177-135">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="72177-135">These statements perform the following actions:</span></span>
   
   * <span data-ttu-id="72177-136">`DROP TABLE` - If the table already exists, it is deleted.</span><span class="sxs-lookup"><span data-stu-id="72177-136">`DROP TABLE` - If the table already exists, it is deleted.</span></span>
   * <span data-ttu-id="72177-137">`CREATE EXTERNAL TABLE` - Creates a new 'external' table in Hive.</span><span class="sxs-lookup"><span data-stu-id="72177-137">`CREATE EXTERNAL TABLE` - Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="72177-138">External tables store only the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="72177-138">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="72177-139">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="72177-139">The data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="72177-140">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="72177-140">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="72177-141">For example, an automated data upload process or another MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="72177-141">For example, an automated data upload process or another MapReduce operation.</span></span>
     >
     > <span data-ttu-id="72177-142">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="72177-142">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="72177-143">`ROW FORMAT` - How the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="72177-143">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="72177-144">The fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="72177-144">The fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="72177-145">`STORED AS TEXTFILE LOCATION` - Where the data is stored (the example/data directory) and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="72177-145">`STORED AS TEXTFILE LOCATION` - Where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="72177-146">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="72177-146">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="72177-147">This statement returns a value of **3** as there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="72177-147">This statement returns a value of **3** as there are three rows that contain this value.</span></span>

     > [!NOTE]
     > <span data-ttu-id="72177-148">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span><span class="sxs-lookup"><span data-stu-id="72177-148">Notice that the spaces between HiveQL statements are replaced by the `+` character when used with Curl.</span></span> <span data-ttu-id="72177-149">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span><span class="sxs-lookup"><span data-stu-id="72177-149">Quoted values that contain a space, such as the delimiter, should not be replaced by `+`.</span></span>

      <span data-ttu-id="72177-150">This command returns a job ID that can be used to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="72177-150">This command returns a job ID that can be used to check the status of the job.</span></span>

5. <span data-ttu-id="72177-151">To check the status of the job, use the following command:</span><span class="sxs-lookup"><span data-stu-id="72177-151">To check the status of the job, use the following command:</span></span>

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

    <span data-ttu-id="72177-152">If the job has finished, the state is **SUCCEEDED**.</span><span class="sxs-lookup"><span data-stu-id="72177-152">If the job has finished, the state is **SUCCEEDED**.</span></span>

6. <span data-ttu-id="72177-153">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="72177-153">Once the state of the job has changed to **SUCCEEDED**, you can retrieve the results of the job from Azure Blob storage.</span></span> <span data-ttu-id="72177-154">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/rest`.</span><span class="sxs-lookup"><span data-stu-id="72177-154">The `statusdir` parameter passed with the query contains the location of the output file; in this case, `/example/rest`.</span></span> <span data-ttu-id="72177-155">This address stores the output in the `example/curl` directory in the clusters default storage.</span><span class="sxs-lookup"><span data-stu-id="72177-155">This address stores the output in the `example/curl` directory in the clusters default storage.</span></span>

    <span data-ttu-id="72177-156">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="72177-156">You can list and download these files by using the [Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="72177-157">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span><span class="sxs-lookup"><span data-stu-id="72177-157">For more information on using the Azure CLI with Azure Storage, see the [Use Azure CLI 2.0 with Azure Storage](https://docs.microsoft.com/azure/storage/storage-azure-cli#create-and-manage-blobs) document.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="72177-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="72177-158">Next steps</span></span>

<span data-ttu-id="72177-159">For general information on Hive with HDInsight:</span><span class="sxs-lookup"><span data-stu-id="72177-159">For general information on Hive with HDInsight:</span></span>

* [<span data-ttu-id="72177-160">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72177-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="72177-161">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="72177-161">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="72177-162">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72177-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="72177-163">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72177-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="72177-164">If you are using Tez with Hive, see the following documents for debugging information:</span><span class="sxs-lookup"><span data-stu-id="72177-164">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="72177-165">Use the Ambari Tez view on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="72177-165">Use the Ambari Tez view on Linux-based HDInsight</span></span>](../hdinsight-debug-ambari-tez-view.md)

<span data-ttu-id="72177-166">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span><span class="sxs-lookup"><span data-stu-id="72177-166">For more information on the REST API used in this document, see the [WebHCat reference](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) document.</span></span>

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


