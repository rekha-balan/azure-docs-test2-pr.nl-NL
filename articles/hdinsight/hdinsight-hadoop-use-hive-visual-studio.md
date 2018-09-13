---
title: Hive query with Hadoop tools for Visual Studio | Microsoft Docs
description: Learn how to use Hive with Hadoop in HDInsight using Visual Studio Hadoop tools.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/28/2017
ms.author: larryfr
ms.openlocfilehash: 5c85ebd5b018bcd9cf6227071118c25cb58c17ab
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549804"
---
# <a name="run-hive-queries-using-the-hdinsight-tools-for-visual-studio"></a><span data-ttu-id="2f654-103">Run Hive queries using the HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f654-103">Run Hive queries using the HDInsight tools for Visual Studio</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="2f654-104">Learn how to submit Hive queries to an HDInsight cluster using the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f654-104">Learn how to submit Hive queries to an HDInsight cluster using the HDInsight tools for Visual Studio.</span></span>

## <a id="prereq"></a><span data-ttu-id="2f654-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="2f654-105">Prerequisites</span></span>

<span data-ttu-id="2f654-106">To complete the steps in this article, you need the following.</span><span class="sxs-lookup"><span data-stu-id="2f654-106">To complete the steps in this article, you need the following.</span></span>

* <span data-ttu-id="2f654-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="2f654-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="2f654-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="2f654-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2f654-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="2f654-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="2f654-110">Visual Studio (one of the following versions):</span><span class="sxs-lookup"><span data-stu-id="2f654-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="2f654-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with [Update 4](https://www.microsoft.com/download/details.aspx?id=44921)</span><span class="sxs-lookup"><span data-stu-id="2f654-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with [Update 4](https://www.microsoft.com/download/details.aspx?id=44921)</span></span>

    * <span data-ttu-id="2f654-112">Visual Studio 2015 (any edition)</span><span class="sxs-lookup"><span data-stu-id="2f654-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="2f654-113">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="2f654-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="2f654-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f654-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="2f654-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span><span class="sxs-lookup"><span data-stu-id="2f654-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <a id="run"></a> <span data-ttu-id="2f654-116">Run Hive queries using the Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f654-116">Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="2f654-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span><span class="sxs-lookup"><span data-stu-id="2f654-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="2f654-118">Provide a name for this project.</span><span class="sxs-lookup"><span data-stu-id="2f654-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="2f654-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="2f654-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="2f654-120">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="2f654-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2f654-121">`DROP TABLE`: If the table exists, this statement deletes it.</span><span class="sxs-lookup"><span data-stu-id="2f654-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="2f654-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span><span class="sxs-lookup"><span data-stu-id="2f654-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="2f654-123">External tables only store the table definition in Hive (the data is left in the original location).</span><span class="sxs-lookup"><span data-stu-id="2f654-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="2f654-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span><span class="sxs-lookup"><span data-stu-id="2f654-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="2f654-125">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="2f654-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="2f654-126">`ROW FORMAT`: Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="2f654-126">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="2f654-127">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="2f654-127">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="2f654-128">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="2f654-128">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="2f654-129">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="2f654-129">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="2f654-130">This statement returns a value of `3` because there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="2f654-130">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="2f654-131">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="2f654-131">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="2f654-132">This clause restricts the search to the sample.log file that contains the data.</span><span class="sxs-lookup"><span data-stu-id="2f654-132">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="2f654-133">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span><span class="sxs-lookup"><span data-stu-id="2f654-133">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="2f654-134">Select **Submit** to run the statements as a Hive job.</span><span class="sxs-lookup"><span data-stu-id="2f654-134">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Submit bar](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="2f654-136">The **Hive Job Summary** appears and displays information about the running job.</span><span class="sxs-lookup"><span data-stu-id="2f654-136">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="2f654-137">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="2f654-137">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![job summary displaying a completed job](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="2f654-139">Use the **Job Output** link to view the output of this job.</span><span class="sxs-lookup"><span data-stu-id="2f654-139">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="2f654-140">It displays `[ERROR] 3`, which is the value returned by this query.</span><span class="sxs-lookup"><span data-stu-id="2f654-140">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="2f654-141">You can also run Hive queries without creating a project.</span><span class="sxs-lookup"><span data-stu-id="2f654-141">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="2f654-142">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span><span class="sxs-lookup"><span data-stu-id="2f654-142">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="2f654-143">In the **temp.hql** document that appears, add the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="2f654-143">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="2f654-144">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="2f654-144">These statements perform the following actions:</span></span>

   * <span data-ttu-id="2f654-145">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="2f654-145">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="2f654-146">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="2f654-146">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="2f654-147">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span><span class="sxs-lookup"><span data-stu-id="2f654-147">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="2f654-148">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span><span class="sxs-lookup"><span data-stu-id="2f654-148">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="2f654-149">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="2f654-149">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="2f654-150">ORC is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="2f654-150">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="2f654-151">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span><span class="sxs-lookup"><span data-stu-id="2f654-151">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="2f654-152">From the toolbar, select **Submit** to run the job.</span><span class="sxs-lookup"><span data-stu-id="2f654-152">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="2f654-153">Use the **Job Status** to determine that the job has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="2f654-153">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="2f654-154">To verify that the job created a new table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span><span class="sxs-lookup"><span data-stu-id="2f654-154">To verify that the job created a new table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="2f654-155">The **errorLogs** table and the **log4jLogs** table are listed.</span><span class="sxs-lookup"><span data-stu-id="2f654-155">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="2f654-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f654-156">Next steps</span></span>

<span data-ttu-id="2f654-157">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f654-157">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="2f654-158">For general information about Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2f654-158">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="2f654-159">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f654-159">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="2f654-160">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="2f654-160">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="2f654-161">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f654-161">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="2f654-162">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f654-162">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="2f654-163">For more information about the HDInsight tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2f654-163">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="2f654-164">Getting started with HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2f654-164">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png


