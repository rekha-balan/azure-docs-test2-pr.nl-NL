---
title: Hive with Data Lake (Hadoop) tools for Visual Studio - Azure HDInsight
description: Learn how to use the Data Lake tools for Visual Studio to run Apache Hive queries with Apache Hadoop on Azure HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: fd57e713a24fb83e42d46b4a1978530b706bf583
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967372"
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="929b6-103">Run Hive queries using the Data Lake tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="929b6-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="929b6-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="929b6-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="929b6-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="929b6-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <a id="prereq"></a><span data-ttu-id="929b6-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="929b6-106">Prerequisites</span></span>

* <span data-ttu-id="929b6-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span><span class="sxs-lookup"><span data-stu-id="929b6-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="929b6-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="929b6-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="929b6-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="929b6-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="929b6-110">Visual Studio (one of the following versions):</span><span class="sxs-lookup"><span data-stu-id="929b6-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="929b6-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span><span class="sxs-lookup"><span data-stu-id="929b6-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="929b6-112">Visual Studio 2015 (any edition)</span><span class="sxs-lookup"><span data-stu-id="929b6-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="929b6-113">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="929b6-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="929b6-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="929b6-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="929b6-115">See [Get started using Visual Studio Hadoop tools for HDInsight](apache-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span><span class="sxs-lookup"><span data-stu-id="929b6-115">See [Get started using Visual Studio Hadoop tools for HDInsight](apache-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <a id="run"></a> <span data-ttu-id="929b6-116">Run Hive queries using the Visual Studio</span><span class="sxs-lookup"><span data-stu-id="929b6-116">Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="929b6-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span><span class="sxs-lookup"><span data-stu-id="929b6-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="929b6-118">Provide a name for this project.</span><span class="sxs-lookup"><span data-stu-id="929b6-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="929b6-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="929b6-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="929b6-120">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="929b6-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="929b6-121">`DROP TABLE`: If the table exists, this statement deletes it.</span><span class="sxs-lookup"><span data-stu-id="929b6-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="929b6-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span><span class="sxs-lookup"><span data-stu-id="929b6-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="929b6-123">External tables only store the table definition in Hive (the data is left in the original location).</span><span class="sxs-lookup"><span data-stu-id="929b6-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="929b6-124">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="929b6-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="929b6-125">For example, a MapReduce job or Azure service.</span><span class="sxs-lookup"><span data-stu-id="929b6-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="929b6-126">Dropping an external table does **not** delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="929b6-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="929b6-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="929b6-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="929b6-128">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="929b6-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="929b6-129">`STORED AS TEXTFILE LOCATION`: Tells Hive that the data is stored in the example/data directory, and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="929b6-129">`STORED AS TEXTFILE LOCATION`: Tells Hive that the data is stored in the example/data directory, and that it is stored as text.</span></span>

   * <span data-ttu-id="929b6-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="929b6-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="929b6-131">This statement returns a value of `3` because there are three rows that contain this value.</span><span class="sxs-lookup"><span data-stu-id="929b6-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="929b6-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span><span class="sxs-lookup"><span data-stu-id="929b6-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="929b6-133">This clause restricts the search to the sample.log file that contains the data.</span><span class="sxs-lookup"><span data-stu-id="929b6-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="929b6-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span><span class="sxs-lookup"><span data-stu-id="929b6-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="929b6-135">Select **Submit** to run the statements as a Hive job.</span><span class="sxs-lookup"><span data-stu-id="929b6-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![Submit bar](./media/apache-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="929b6-137">The **Hive Job Summary** appears and displays information about the running job.</span><span class="sxs-lookup"><span data-stu-id="929b6-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="929b6-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span><span class="sxs-lookup"><span data-stu-id="929b6-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![job summary displaying a completed job](./media/apache-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="929b6-140">Use the **Job Output** link to view the output of this job.</span><span class="sxs-lookup"><span data-stu-id="929b6-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="929b6-141">It displays `[ERROR] 3`, which is the value returned by this query.</span><span class="sxs-lookup"><span data-stu-id="929b6-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="929b6-142">You can also run Hive queries without creating a project.</span><span class="sxs-lookup"><span data-stu-id="929b6-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="929b6-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span><span class="sxs-lookup"><span data-stu-id="929b6-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="929b6-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="929b6-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="929b6-145">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="929b6-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="929b6-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="929b6-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="929b6-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span><span class="sxs-lookup"><span data-stu-id="929b6-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="929b6-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span><span class="sxs-lookup"><span data-stu-id="929b6-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="929b6-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span><span class="sxs-lookup"><span data-stu-id="929b6-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="929b6-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="929b6-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="929b6-151">ORC is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="929b6-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="929b6-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span><span class="sxs-lookup"><span data-stu-id="929b6-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="929b6-153">From the toolbar, select **Submit** to run the job.</span><span class="sxs-lookup"><span data-stu-id="929b6-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="929b6-154">Use the **Job Status** to determine that the job has completed successfully.</span><span class="sxs-lookup"><span data-stu-id="929b6-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="929b6-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span><span class="sxs-lookup"><span data-stu-id="929b6-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="929b6-156">The **errorLogs** table and the **log4jLogs** table are listed.</span><span class="sxs-lookup"><span data-stu-id="929b6-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="929b6-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="929b6-157">Next steps</span></span>

<span data-ttu-id="929b6-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="929b6-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="929b6-159">For general information about Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="929b6-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="929b6-160">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="929b6-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="929b6-161">For information about other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="929b6-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="929b6-162">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="929b6-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="929b6-163">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="929b6-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="929b6-164">For more information about the HDInsight tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="929b6-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="929b6-165">Getting started with HDInsight tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="929b6-165">Getting started with HDInsight tools for Visual Studio</span></span>](apache-hadoop-visual-studio-tools-get-started.md)

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

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]:submit-apache-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]:apache-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
