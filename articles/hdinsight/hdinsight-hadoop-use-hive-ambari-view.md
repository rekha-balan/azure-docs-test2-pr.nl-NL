---
title: Use Ambari Views to work with Hive on HDInsight (Hadoop) | Microsoft Docs
description: Learn how to use the Hive View from your web browser to submit Hive queries. The Hive View is part of the Ambari Web UI provided with your Linux-based HDInsight cluster.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: 035d7695e6313f85cefcaed1df4256655d8046bd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552912"
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="88639-104">Use the Hive View with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="88639-105">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="88639-105">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="88639-106">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span><span class="sxs-lookup"><span data-stu-id="88639-106">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span> <span data-ttu-id="88639-107">This is the **Hive View**, part of the Ambari Views provided with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="88639-107">This is the **Hive View**, part of the Ambari Views provided with your HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="88639-108">Ambari has many capabilities that are not discussed in this document.</span><span class="sxs-lookup"><span data-stu-id="88639-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="88639-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="88639-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88639-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88639-110">Prerequisites</span></span>

* <span data-ttu-id="88639-111">A Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="88639-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="88639-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88639-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="88639-113">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="88639-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="88639-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="88639-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="88639-115">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="88639-115">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="88639-116">Open the Hive view</span><span class="sxs-lookup"><span data-stu-id="88639-116">Open the Hive view</span></span>

<span data-ttu-id="88639-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span><span class="sxs-lookup"><span data-stu-id="88639-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![quick links section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="88639-119">You can also navigate directly to Ambari by going to https://CLUSTERNAME.azurehdinsight.net in a web browser.</span><span class="sxs-lookup"><span data-stu-id="88639-119">You can also navigate directly to Ambari by going to https://CLUSTERNAME.azurehdinsight.net in a web browser.</span></span> <span data-ttu-id="88639-120">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="88639-120">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span> <span data-ttu-id="88639-121">Select the set of squares from the page menu next to the **Admin** link to list available views.</span><span class="sxs-lookup"><span data-stu-id="88639-121">Select the set of squares from the page menu next to the **Admin** link to list available views.</span></span> <span data-ttu-id="88639-122">Select the **Hive view**.</span><span class="sxs-lookup"><span data-stu-id="88639-122">Select the **Hive view**.</span></span>

![Selecting Ambari views](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/selecthiveview.png)<span data-ttu-id="88639-124">.</span><span class="sxs-lookup"><span data-stu-id="88639-124">.</span></span>

> [!NOTE]
> <span data-ttu-id="88639-125">When accessing Ambari, you are prompted to authenticate to the site.</span><span class="sxs-lookup"><span data-stu-id="88639-125">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="88639-126">Enter the admin (default `admin`,) account name and password you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="88639-126">Enter the admin (default `admin`,) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="88639-127">You should see a page similar to the following:</span><span class="sxs-lookup"><span data-stu-id="88639-127">You should see a page similar to the following:</span></span>

![Image of the hive view page, containing a query editor section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hiveview.png)

## <a name="view-tables"></a><span data-ttu-id="88639-129">View tables</span><span class="sxs-lookup"><span data-stu-id="88639-129">View tables</span></span>
<span data-ttu-id="88639-130">In the **Database Explorer** section of the page, select the **default** entry on the **Databases** tab. This displays a list of tables in the default database.</span><span class="sxs-lookup"><span data-stu-id="88639-130">In the **Database Explorer** section of the page, select the **default** entry on the **Databases** tab. This displays a list of tables in the default database.</span></span> <span data-ttu-id="88639-131">For a new HDInsight cluster, only one table should exist; **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="88639-131">For a new HDInsight cluster, only one table should exist; **hivesampletable**.</span></span>

![database explorer with the default database expanded](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/databaseexplorer.png)

<span data-ttu-id="88639-133">As tables are added through the steps in this document, you can use the refresh icon in the upper right corner of the Database Explorer to refresh the list.</span><span class="sxs-lookup"><span data-stu-id="88639-133">As tables are added through the steps in this document, you can use the refresh icon in the upper right corner of the Database Explorer to refresh the list.</span></span>

## <a name="hivequery"></a><span data-ttu-id="88639-134">Query editor</span><span class="sxs-lookup"><span data-stu-id="88639-134">Query editor</span></span>

<span data-ttu-id="88639-135">Use the following steps from the Hive view to execute a Hive query.</span><span class="sxs-lookup"><span data-stu-id="88639-135">Use the following steps from the Hive view to execute a Hive query.</span></span>

1. <span data-ttu-id="88639-136">In the **Query Editor** section of the page, paste the following HiveQL statements into the worksheet:</span><span class="sxs-lookup"><span data-stu-id="88639-136">In the **Query Editor** section of the page, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="88639-137">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="88639-137">These statements perform the following actions:</span></span>

   * <span data-ttu-id="88639-138">**DROP TABLE** - Deletes the table and the data file, in case the table already exists.</span><span class="sxs-lookup"><span data-stu-id="88639-138">**DROP TABLE** - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="88639-139">**CREATE EXTERNAL TABLE** - Creates a new "external" table in Hive.</span><span class="sxs-lookup"><span data-stu-id="88639-139">**CREATE EXTERNAL TABLE** - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="88639-140">External tables store only the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="88639-140">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="88639-141">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="88639-141">The data is left in the original location.</span></span>

   * <span data-ttu-id="88639-142">**ROW FORMAT** - Tells Hive how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="88639-142">**ROW FORMAT** - Tells Hive how the data is formatted.</span></span> <span data-ttu-id="88639-143">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="88639-143">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="88639-144">**STORED AS TEXTFILE LOCATION** - Tells Hive where the data is stored (the example/data directory), and that it is stored as text.</span><span class="sxs-lookup"><span data-stu-id="88639-144">**STORED AS TEXTFILE LOCATION** - Tells Hive where the data is stored (the example/data directory), and that it is stored as text.</span></span>

   * <span data-ttu-id="88639-145">**SELECT** - Selects a count of all rows where column t4 contains the value [ERROR].</span><span class="sxs-lookup"><span data-stu-id="88639-145">**SELECT** - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="88639-146">External tables should be used when you expect the underlying data to be updated by an external source.</span><span class="sxs-lookup"><span data-stu-id="88639-146">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="88639-147">For example, an automated data upload process, or by another MapReduce operation.</span><span class="sxs-lookup"><span data-stu-id="88639-147">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="88639-148">Dropping an external table does *not* delete the data, only the table definition.</span><span class="sxs-lookup"><span data-stu-id="88639-148">Dropping an external table does *not* delete the data, only the table definition.</span></span>

2. <span data-ttu-id="88639-149">To start the query, use the **Execute** button at the bottom of the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="88639-149">To start the query, use the **Execute** button at the bottom of the Query Editor.</span></span> <span data-ttu-id="88639-150">It turns orange and the text changes to **Stop execution**.</span><span class="sxs-lookup"><span data-stu-id="88639-150">It turns orange and the text changes to **Stop execution**.</span></span> <span data-ttu-id="88639-151">A **Query Process Results** section should appear beneath the Query Editor and display information about the job.</span><span class="sxs-lookup"><span data-stu-id="88639-151">A **Query Process Results** section should appear beneath the Query Editor and display information about the job.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="88639-152">Some browsers may not correctly refresh the log or results information.</span><span class="sxs-lookup"><span data-stu-id="88639-152">Some browsers may not correctly refresh the log or results information.</span></span> <span data-ttu-id="88639-153">If you run a job and it appears to run forever without updating the log or returning results, try using Mozilla FireFox or Google Chrome instead.</span><span class="sxs-lookup"><span data-stu-id="88639-153">If you run a job and it appears to run forever without updating the log or returning results, try using Mozilla FireFox or Google Chrome instead.</span></span>

3. <span data-ttu-id="88639-154">Once the query has finished, The **Query Process Results** section displays the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="88639-154">Once the query has finished, The **Query Process Results** section displays the results of the operation.</span></span> <span data-ttu-id="88639-155">The **Stop execution** button also changes back to a green **Execute** button when the query completes.</span><span class="sxs-lookup"><span data-stu-id="88639-155">The **Stop execution** button also changes back to a green **Execute** button when the query completes.</span></span> <span data-ttu-id="88639-156">The **Results** tab should contain the following information:</span><span class="sxs-lookup"><span data-stu-id="88639-156">The **Results** tab should contain the following information:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="88639-157">The **Logs** tab can be used to view the logging information created by the job.</span><span class="sxs-lookup"><span data-stu-id="88639-157">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="88639-158">T **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span><span class="sxs-lookup"><span data-stu-id="88639-158">T **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="88639-159">Select the first four lines of this query, then select **Execute**.</span><span class="sxs-lookup"><span data-stu-id="88639-159">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="88639-160">Notice that there are no results when the job completes.</span><span class="sxs-lookup"><span data-stu-id="88639-160">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="88639-161">Using the **Execute** button when part of the query is selected only runs the selected statements.</span><span class="sxs-lookup"><span data-stu-id="88639-161">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="88639-162">In this case, the selection didn't include the final statement that retrieves rows from the table.</span><span class="sxs-lookup"><span data-stu-id="88639-162">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="88639-163">If you select just that line and use **Execute**, you should see the expected results.</span><span class="sxs-lookup"><span data-stu-id="88639-163">If you select just that line and use **Execute**, you should see the expected results.</span></span>

<span data-ttu-id="88639-164">5.To add a new worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="88639-164">5.To add a new worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="88639-165">In the new worksheet, enter the following HiveQL statements:</span><span class="sxs-lookup"><span data-stu-id="88639-165">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="88639-166">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="88639-166">These statements perform the following actions:</span></span>

   * <span data-ttu-id="88639-167">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="88639-167">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="88639-168">Since the **EXTERNAL** keyword is not used, an internal table is created.</span><span class="sxs-lookup"><span data-stu-id="88639-168">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="88639-169">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span><span class="sxs-lookup"><span data-stu-id="88639-169">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="88639-170">Unlike external tables, dropping an internal table deletes the underlying data as well.</span><span class="sxs-lookup"><span data-stu-id="88639-170">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="88639-171">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span><span class="sxs-lookup"><span data-stu-id="88639-171">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="88639-172">This is a highly optimized and efficient format for storing Hive data.</span><span class="sxs-lookup"><span data-stu-id="88639-172">This is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="88639-173">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain [ERROR], and then inserts the data into the **errorLogs** table.</span><span class="sxs-lookup"><span data-stu-id="88639-173">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain [ERROR], and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="88639-174">Use the **Execute** button to run this query.</span><span class="sxs-lookup"><span data-stu-id="88639-174">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="88639-175">The **Results** tab does not contain any information when the query returns zero rows.</span><span class="sxs-lookup"><span data-stu-id="88639-175">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="88639-176">The status should show as **SUCCEEDED** once the query completes.</span><span class="sxs-lookup"><span data-stu-id="88639-176">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="hive-settings"></a><span data-ttu-id="88639-177">Hive settings</span><span class="sxs-lookup"><span data-stu-id="88639-177">Hive settings</span></span>

<span data-ttu-id="88639-178">Select the **Settings** icon to the right of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-178">Select the **Settings** icon to the right of the editor.</span></span>

![Settings icon for hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-settings-icon.png)

<span data-ttu-id="88639-180">Settings can be used to change various Hive settings, such as changing the execution engine for Hive from Tez (the default) to MapReduce.</span><span class="sxs-lookup"><span data-stu-id="88639-180">Settings can be used to change various Hive settings, such as changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

### <a name="visualization"></a><span data-ttu-id="88639-181">Visualization</span><span class="sxs-lookup"><span data-stu-id="88639-181">Visualization</span></span>

<span data-ttu-id="88639-182">Select the __Visualization__ icon to the right of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-182">Select the __Visualization__ icon to the right of the editor.</span></span>

![Visualization icon for hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-visualization-icon.png)

<span data-ttu-id="88639-184">This opens the visualization interface, where you can create visualizations of the data returned from the query.</span><span class="sxs-lookup"><span data-stu-id="88639-184">This opens the visualization interface, where you can create visualizations of the data returned from the query.</span></span> <span data-ttu-id="88639-185">The following is an example visualization using data from the `hivesampletable` included with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="88639-185">The following is an example visualization using data from the `hivesampletable` included with HDInsight.</span></span>

![Example visualization](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-visualization.png)

### <a name="visual-explain"></a><span data-ttu-id="88639-187">Visual explain</span><span class="sxs-lookup"><span data-stu-id="88639-187">Visual explain</span></span>

<span data-ttu-id="88639-188">Select the **Visual Explain** icon to the right of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-188">Select the **Visual Explain** icon to the right of the editor.</span></span>

![Visual explain icon for hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-visual-explain-icon.png)

<span data-ttu-id="88639-190">This is the **Visual Explain** view of the query, which can be helpful in understanding the flow of complex queries.</span><span class="sxs-lookup"><span data-stu-id="88639-190">This is the **Visual Explain** view of the query, which can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="88639-191">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="88639-191">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

![visual explain image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/visualexplain.png)

### <a name="tez"></a><span data-ttu-id="88639-193">Tez</span><span class="sxs-lookup"><span data-stu-id="88639-193">Tez</span></span>

<span data-ttu-id="88639-194">Select the **Tez** icon to the right of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-194">Select the **Tez** icon to the right of the editor.</span></span>

![Tez icon for hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-tez-icon.png)

<span data-ttu-id="88639-196">This displays the Directed Acyclic Graph (DAG) used by Tez for this query, if one is available.</span><span class="sxs-lookup"><span data-stu-id="88639-196">This displays the Directed Acyclic Graph (DAG) used by Tez for this query, if one is available.</span></span> <span data-ttu-id="88639-197">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span><span class="sxs-lookup"><span data-stu-id="88639-197">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

### <a name="notifications"></a><span data-ttu-id="88639-198">Notifications</span><span class="sxs-lookup"><span data-stu-id="88639-198">Notifications</span></span>

<span data-ttu-id="88639-199">Select the **Notifications** icon to the right of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-199">Select the **Notifications** icon to the right of the editor.</span></span>

![Notifications icon for hive view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-hive-ambari-view/hive-view-notifications-icon.png)

<span data-ttu-id="88639-201">Notifications are messages that are generated when running queries.</span><span class="sxs-lookup"><span data-stu-id="88639-201">Notifications are messages that are generated when running queries.</span></span> <span data-ttu-id="88639-202">For example, you receive a notification when a query is submitted, or when an error occurs.</span><span class="sxs-lookup"><span data-stu-id="88639-202">For example, you receive a notification when a query is submitted, or when an error occurs.</span></span>

## <a name="saved-queries"></a><span data-ttu-id="88639-203">Saved queries</span><span class="sxs-lookup"><span data-stu-id="88639-203">Saved queries</span></span>

1. <span data-ttu-id="88639-204">From the Query Editor, create a worksheet and enter the following query:</span><span class="sxs-lookup"><span data-stu-id="88639-204">From the Query Editor, create a worksheet and enter the following query:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="88639-205">Execute the query to verify that it works.</span><span class="sxs-lookup"><span data-stu-id="88639-205">Execute the query to verify that it works.</span></span> <span data-ttu-id="88639-206">The results are similar to the following example:</span><span class="sxs-lookup"><span data-stu-id="88639-206">The results are similar to the following example:</span></span>

        errorlogs.t1     errorlogs.t2     errorlogs.t3     errorlogs.t4     errorlogs.t5     errorlogs.t6     errorlogs.t7
        2012-02-03     18:35:34     SampleClass0     [ERROR]     incorrect     id     
        2012-02-03     18:55:54     SampleClass1     [ERROR]     incorrect     id     
        2012-02-03     19:25:27     SampleClass4     [ERROR]     incorrect     id

2. <span data-ttu-id="88639-207">Use the **Save as** button at the bottom of the editor.</span><span class="sxs-lookup"><span data-stu-id="88639-207">Use the **Save as** button at the bottom of the editor.</span></span> <span data-ttu-id="88639-208">Name this query **Errorlogs** and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="88639-208">Name this query **Errorlogs** and select **OK**.</span></span> <span data-ttu-id="88639-209">The name of the worksheet changes to **Errorlogs**.</span><span class="sxs-lookup"><span data-stu-id="88639-209">The name of the worksheet changes to **Errorlogs**.</span></span>

3. <span data-ttu-id="88639-210">Select the **Saved Queries** tab at the top of the Hive View page.</span><span class="sxs-lookup"><span data-stu-id="88639-210">Select the **Saved Queries** tab at the top of the Hive View page.</span></span> <span data-ttu-id="88639-211">**Errorlogs** is now listed as a saved query.</span><span class="sxs-lookup"><span data-stu-id="88639-211">**Errorlogs** is now listed as a saved query.</span></span> <span data-ttu-id="88639-212">It remains in this list until you remove it.</span><span class="sxs-lookup"><span data-stu-id="88639-212">It remains in this list until you remove it.</span></span> <span data-ttu-id="88639-213">Selecting the name opens the query in the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="88639-213">Selecting the name opens the query in the Query Editor.</span></span>

## <a name="query-history"></a><span data-ttu-id="88639-214">Query history</span><span class="sxs-lookup"><span data-stu-id="88639-214">Query history</span></span>

<span data-ttu-id="88639-215">The **History** button at the top of the Hive View allows you to view queries you have ran previously.</span><span class="sxs-lookup"><span data-stu-id="88639-215">The **History** button at the top of the Hive View allows you to view queries you have ran previously.</span></span> <span data-ttu-id="88639-216">Use it now and select some of the queries you have ran previously.</span><span class="sxs-lookup"><span data-stu-id="88639-216">Use it now and select some of the queries you have ran previously.</span></span> <span data-ttu-id="88639-217">When you select a query, it opens it in the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="88639-217">When you select a query, it opens it in the Query Editor.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="88639-218">User Defined Functions (UDF)</span><span class="sxs-lookup"><span data-stu-id="88639-218">User Defined Functions (UDF)</span></span>

<span data-ttu-id="88639-219">Hive can also be extended through **user-defined functions (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="88639-219">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="88639-220">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="88639-220">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="88639-221">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs that can be used with the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="88639-221">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs that can be used with the **Query Editor**.</span></span>

<span data-ttu-id="88639-222">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="88639-222">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="88639-223">Selecting this displays a drop-down list of the UDFs defined in the Hive View.</span><span class="sxs-lookup"><span data-stu-id="88639-223">Selecting this displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="88639-224">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span><span class="sxs-lookup"><span data-stu-id="88639-224">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="88639-225">For example, if you have defined a UDF with the following properties:</span><span class="sxs-lookup"><span data-stu-id="88639-225">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="88639-226">Resource name: myudfs</span><span class="sxs-lookup"><span data-stu-id="88639-226">Resource name: myudfs</span></span>

* <span data-ttu-id="88639-227">Resource path: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="88639-227">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="88639-228">UDF name: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="88639-228">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="88639-229">UDF class name: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="88639-229">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="88639-230">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span><span class="sxs-lookup"><span data-stu-id="88639-230">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="88639-231">In this case, **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="88639-231">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="88639-232">Selecting this entry adds the following to the beginning of the query:</span><span class="sxs-lookup"><span data-stu-id="88639-232">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="88639-233">You can then use the UDF in your query.</span><span class="sxs-lookup"><span data-stu-id="88639-233">You can then use the UDF in your query.</span></span> <span data-ttu-id="88639-234">For example, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="88639-234">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="88639-235">For more information on using UDFs with Hive on HDInsight, see the following:</span><span class="sxs-lookup"><span data-stu-id="88639-235">For more information on using UDFs with Hive on HDInsight, see the following:</span></span>

* [<span data-ttu-id="88639-236">Using Python with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-236">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="88639-237">How to add a custom Hive UDF to HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-237">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a id="nextsteps"></a><span data-ttu-id="88639-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="88639-238">Next steps</span></span>
<span data-ttu-id="88639-239">For general information on Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="88639-239">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="88639-240">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-240">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="88639-241">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="88639-241">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="88639-242">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-242">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="88639-243">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="88639-243">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)











