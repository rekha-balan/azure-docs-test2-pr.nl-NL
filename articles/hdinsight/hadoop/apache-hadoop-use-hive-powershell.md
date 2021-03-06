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
# <a name="run-hive-queries-using-powershell"></a>Run Hive queries using PowerShell
[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.

> [!NOTE]
> This document does not provide a detailed description of what the HiveQL statements that are used in the examples do. For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).

## <a name="prerequisites"></a>Prerequisites

* A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.

  > [!IMPORTANT]
  > Linux is the only operating system used on HDInsight version 3.4 or greater. For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).

* A client with Azure PowerShell.

[!INCLUDE [upgrade-powershell](../../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-a-hive-query"></a>Run a Hive query

Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight. Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.

The following cmdlets are used when running Hive queries in a remote HDInsight cluster:

* `Connect-AzureRmAccount`: Authenticates Azure PowerShell to your Azure subscription.
* `New-AzureRmHDInsightHiveJobDefinition`: Creates a *job definition* by using the specified HiveQL statements.
* `Start-AzureRmHDInsightJob`: Sends the job definition to HDInsight and starts the job. A *job* object is returned.
* `Wait-AzureRmHDInsightJob`: Uses the job object to check the status of the job. It waits until the job completes or the wait time is exceeded.
* `Get-AzureRmHDInsightJobOutput`: Used to retrieve the output of the job.
* `Invoke-AzureRmHDInsightHiveJob`: Used to run HiveQL statements. This cmdlet blocks the query completes, then returns the results.
* `Use-AzureRmHDInsightCluster`: Sets the current cluster to use for the `Invoke-AzureRmHDInsightHiveJob` command.

The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:

1. Using an editor, save the following code as `hivejob.ps1`.

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Open a new **Azure PowerShell** command prompt. Change directories to the location of the `hivejob.ps1` file, then use the following command to run the script:

        .\hivejob.ps1

    When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster. You may also be prompted to log in to your Azure subscription.

3. When the job completes, it returns information similar to the following text:

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. As mentioned earlier, `Invoke-Hive` can be used to run a query and wait for the response. Use the following script to see how Invoke-Hive works:

    [!code-powershell[main](../../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    The output looks like the following text:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files. The following snippet shows how to use the `Invoke-Hive` cmdlet to run a HiveQL script file. The HiveQL script file must be uploaded to wasb://.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.

## <a name="troubleshooting"></a>Troubleshooting

If no information is returned when the job completes, view the error logs. To view error information for this job, add the following to the end of the `hivejob.ps1` file, save it, and then run it again.

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

This cmdlet returns the information that is written to STDERR during job processing.

## <a name="summary"></a>Summary

As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.

## <a name="next-steps"></a>Next steps

For general information about Hive in HDInsight:

* [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md)

For information about other ways you can work with Hadoop on HDInsight:

* [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md)
* [Use MapReduce with Hadoop on HDInsight](hdinsight-use-mapreduce.md)
