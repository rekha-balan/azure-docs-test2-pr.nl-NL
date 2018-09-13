---
title: Use Hadoop Hive with PowerShell in HDInsight - Azure
description: Use PowerShell to run Hive queries in Hadoop on HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/23/2018
ms.author: jasonh
ms.openlocfilehash: 16caee1b04b8fb3ae2e83b8105b802e121092f60
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868810"
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="edbcd-103">Run Hive queries using PowerShell</span><span class="sxs-lookup"><span data-stu-id="edbcd-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="edbcd-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="edbcd-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="edbcd-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span><span class="sxs-lookup"><span data-stu-id="edbcd-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="edbcd-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="edbcd-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="edbcd-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="edbcd-107">Prerequisites</span></span>

* <span data-ttu-id="edbcd-108">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="edbcd-108">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="edbcd-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="edbcd-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="edbcd-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="edbcd-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="edbcd-111">A client with Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="edbcd-111">A client with Azure PowerShell.</span></span>

[!INCLUDE [upgrade-powershell](../../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-a-hive-query"></a><span data-ttu-id="edbcd-112">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="edbcd-112">Run a Hive query</span></span>

<span data-ttu-id="edbcd-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="edbcd-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="edbcd-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="edbcd-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="edbcd-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="edbcd-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="edbcd-116">`Connect-AzureRmAccount`: Authenticates Azure PowerShell to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="edbcd-116">`Connect-AzureRmAccount`: Authenticates Azure PowerShell to your Azure subscription.</span></span>
* <span data-ttu-id="edbcd-117">`New-AzureRmHDInsightHiveJobDefinition`: Creates a *job definition* by using the specified HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="edbcd-117">`New-AzureRmHDInsightHiveJobDefinition`: Creates a *job definition* by using the specified HiveQL statements.</span></span>
* <span data-ttu-id="edbcd-118">`Start-AzureRmHDInsightJob`: Sends the job definition to HDInsight and starts the job.</span><span class="sxs-lookup"><span data-stu-id="edbcd-118">`Start-AzureRmHDInsightJob`: Sends the job definition to HDInsight and starts the job.</span></span> <span data-ttu-id="edbcd-119">A *job* object is returned.</span><span class="sxs-lookup"><span data-stu-id="edbcd-119">A *job* object is returned.</span></span>
* <span data-ttu-id="edbcd-120">`Wait-AzureRmHDInsightJob`: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="edbcd-120">`Wait-AzureRmHDInsightJob`: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="edbcd-121">It waits until the job completes or the wait time is exceeded.</span><span class="sxs-lookup"><span data-stu-id="edbcd-121">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="edbcd-122">`Get-AzureRmHDInsightJobOutput`: Used to retrieve the output of the job.</span><span class="sxs-lookup"><span data-stu-id="edbcd-122">`Get-AzureRmHDInsightJobOutput`: Used to retrieve the output of the job.</span></span>
* <span data-ttu-id="edbcd-123">`Invoke-AzureRmHDInsightHiveJob`: Used to run HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="edbcd-123">`Invoke-AzureRmHDInsightHiveJob`: Used to run HiveQL statements.</span></span> <span data-ttu-id="edbcd-124">This cmdlet blocks the query completes, then returns the results.</span><span class="sxs-lookup"><span data-stu-id="edbcd-124">This cmdlet blocks the query completes, then returns the results.</span></span>
* <span data-ttu-id="edbcd-125">`Use-AzureRmHDInsightCluster`: Sets the current cluster to use for the `Invoke-AzureRmHDInsightHiveJob` command.</span><span class="sxs-lookup"><span data-stu-id="edbcd-125">`Use-AzureRmHDInsightCluster`: Sets the current cluster to use for the `Invoke-AzureRmHDInsightHiveJob` command.</span></span>

<span data-ttu-id="edbcd-126">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="edbcd-126">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="edbcd-127">Using an editor, save the following code as `hivejob.ps1`.</span><span class="sxs-lookup"><span data-stu-id="edbcd-127">Using an editor, save the following code as `hivejob.ps1`.</span></span>

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="edbcd-128">Open a new **Azure PowerShell** command prompt.</span><span class="sxs-lookup"><span data-stu-id="edbcd-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="edbcd-129">Change directories to the location of the `hivejob.ps1` file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="edbcd-129">Change directories to the location of the `hivejob.ps1` file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="edbcd-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="edbcd-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="edbcd-131">You may also be prompted to log in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="edbcd-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="edbcd-132">When the job completes, it returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="edbcd-132">When the job completes, it returns information similar to the following text:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="edbcd-133">As mentioned earlier, `Invoke-Hive` can be used to run a query and wait for the response.</span><span class="sxs-lookup"><span data-stu-id="edbcd-133">As mentioned earlier, `Invoke-Hive` can be used to run a query and wait for the response.</span></span> <span data-ttu-id="edbcd-134">Use the following script to see how Invoke-Hive works:</span><span class="sxs-lookup"><span data-stu-id="edbcd-134">Use the following script to see how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="edbcd-135">The output looks like the following text:</span><span class="sxs-lookup"><span data-stu-id="edbcd-135">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="edbcd-136">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span><span class="sxs-lookup"><span data-stu-id="edbcd-136">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="edbcd-137">The following snippet shows how to use the `Invoke-Hive` cmdlet to run a HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="edbcd-137">The following snippet shows how to use the `Invoke-Hive` cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="edbcd-138">The HiveQL script file must be uploaded to wasb://.</span><span class="sxs-lookup"><span data-stu-id="edbcd-138">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="edbcd-139">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span><span class="sxs-lookup"><span data-stu-id="edbcd-139">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="edbcd-140">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="edbcd-140">Troubleshooting</span></span>

<span data-ttu-id="edbcd-141">If no information is returned when the job completes, view the error logs.</span><span class="sxs-lookup"><span data-stu-id="edbcd-141">If no information is returned when the job completes, view the error logs.</span></span> <span data-ttu-id="edbcd-142">To view error information for this job, add the following to the end of the `hivejob.ps1` file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="edbcd-142">To view error information for this job, add the following to the end of the `hivejob.ps1` file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="edbcd-143">This cmdlet returns the information that is written to STDERR during job processing.</span><span class="sxs-lookup"><span data-stu-id="edbcd-143">This cmdlet returns the information that is written to STDERR during job processing.</span></span>

## <a name="summary"></a><span data-ttu-id="edbcd-144">Summary</span><span class="sxs-lookup"><span data-stu-id="edbcd-144">Summary</span></span>

<span data-ttu-id="edbcd-145">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="edbcd-145">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="edbcd-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="edbcd-146">Next steps</span></span>

<span data-ttu-id="edbcd-147">For general information about Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="edbcd-147">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="edbcd-148">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="edbcd-148">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="edbcd-149">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="edbcd-149">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="edbcd-150">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="edbcd-150">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="edbcd-151">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="edbcd-151">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
