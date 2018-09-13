---
title: Use Hadoop Hive with PowerShell in HDInsight | Microsoft Docs
description: Use PowerShell to run Hive queries in Hadoop on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: larryfr
ms.openlocfilehash: fc805414427982f3b43010f694618657f3e54a29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553326"
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="b81f2-103">Run Hive queries using PowerShell</span><span class="sxs-lookup"><span data-stu-id="b81f2-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="b81f2-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b81f2-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="b81f2-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span><span class="sxs-lookup"><span data-stu-id="b81f2-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="b81f2-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="b81f2-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="b81f2-107">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="b81f2-107">**Prerequisites**</span></span>

* <span data-ttu-id="b81f2-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span><span class="sxs-lookup"><span data-stu-id="b81f2-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b81f2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="b81f2-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b81f2-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="b81f2-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="b81f2-111">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b81f2-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="b81f2-112">Run Hive queries using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b81f2-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="b81f2-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b81f2-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="b81f2-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b81f2-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="b81f2-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="b81f2-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="b81f2-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="b81f2-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="b81f2-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span><span class="sxs-lookup"><span data-stu-id="b81f2-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="b81f2-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span><span class="sxs-lookup"><span data-stu-id="b81f2-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="b81f2-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span><span class="sxs-lookup"><span data-stu-id="b81f2-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="b81f2-120">It waits until the job completes or the wait time is exceeded.</span><span class="sxs-lookup"><span data-stu-id="b81f2-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="b81f2-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span><span class="sxs-lookup"><span data-stu-id="b81f2-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="b81f2-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span><span class="sxs-lookup"><span data-stu-id="b81f2-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="b81f2-123">This cmdlet blocks the query completes, then returns the results</span><span class="sxs-lookup"><span data-stu-id="b81f2-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="b81f2-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span><span class="sxs-lookup"><span data-stu-id="b81f2-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="b81f2-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="b81f2-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="b81f2-126">Using an editor, save the following code as **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b81f2-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="b81f2-127">Open a new **Azure PowerShell** command prompt.</span><span class="sxs-lookup"><span data-stu-id="b81f2-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="b81f2-128">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span><span class="sxs-lookup"><span data-stu-id="b81f2-128">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="b81f2-129">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b81f2-129">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="b81f2-130">You may also be prompted to log in to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="b81f2-130">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="b81f2-131">When the job completes, it returns information similar to the following thext:</span><span class="sxs-lookup"><span data-stu-id="b81f2-131">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="b81f2-132">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span><span class="sxs-lookup"><span data-stu-id="b81f2-132">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="b81f2-133">Use the following script to see how Invoke-Hive works:</span><span class="sxs-lookup"><span data-stu-id="b81f2-133">Use the following script to see how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="b81f2-134">The output looks like the following text:</span><span class="sxs-lookup"><span data-stu-id="b81f2-134">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="b81f2-135">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span><span class="sxs-lookup"><span data-stu-id="b81f2-135">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="b81f2-136">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="b81f2-136">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="b81f2-137">The HiveQL script file must be uploaded to wasbs://.</span><span class="sxs-lookup"><span data-stu-id="b81f2-137">The HiveQL script file must be uploaded to wasbs://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasbs://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="b81f2-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span><span class="sxs-lookup"><span data-stu-id="b81f2-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b81f2-139">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="b81f2-139">Troubleshooting</span></span>

<span data-ttu-id="b81f2-140">If no information is returned when the job completes, an error may have occurred during processing.</span><span class="sxs-lookup"><span data-stu-id="b81f2-140">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="b81f2-141">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span><span class="sxs-lookup"><span data-stu-id="b81f2-141">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="b81f2-142">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span><span class="sxs-lookup"><span data-stu-id="b81f2-142">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="b81f2-143">Summary</span><span class="sxs-lookup"><span data-stu-id="b81f2-143">Summary</span></span>

<span data-ttu-id="b81f2-144">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span><span class="sxs-lookup"><span data-stu-id="b81f2-144">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b81f2-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="b81f2-145">Next steps</span></span>

<span data-ttu-id="b81f2-146">For general information about Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b81f2-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="b81f2-147">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b81f2-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="b81f2-148">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b81f2-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b81f2-149">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b81f2-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b81f2-150">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="b81f2-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
