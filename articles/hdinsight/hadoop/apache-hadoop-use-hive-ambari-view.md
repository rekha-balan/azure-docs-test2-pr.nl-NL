---
title: Use Ambari Views to work with Hive on HDInsight (Hadoop) - Azure
description: Learn how to use the Hive View from your web browser to submit Hive queries. The Hive View is part of the Ambari Web UI provided with your Linux-based HDInsight cluster.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: 43b82070ced57c0654d646fbea5a12aeab7c2a31
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867152"
---
# <a name="use-ambari-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="72ad8-104">Use Ambari Hive View with Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-104">Use Ambari Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="72ad8-105">Learn how to run Hive queries by using Ambari Hive View.</span><span class="sxs-lookup"><span data-stu-id="72ad8-105">Learn how to run Hive queries by using Ambari Hive View.</span></span> <span data-ttu-id="72ad8-106">The Hive View allows you to author, optimize, and run Hive queries from your web browser.</span><span class="sxs-lookup"><span data-stu-id="72ad8-106">The Hive View allows you to author, optimize, and run Hive queries from your web browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72ad8-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72ad8-107">Prerequisites</span></span>

* <span data-ttu-id="72ad8-108">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="72ad8-108">A Linux-based Hadoop on HDInsight cluster version 3.4 or greater.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="72ad8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="72ad8-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="72ad8-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="72ad8-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="72ad8-111">A web browser</span><span class="sxs-lookup"><span data-stu-id="72ad8-111">A web browser</span></span>

## <a name="run-a-hive-query"></a><span data-ttu-id="72ad8-112">Run a Hive query</span><span class="sxs-lookup"><span data-stu-id="72ad8-112">Run a Hive query</span></span>

1. <span data-ttu-id="72ad8-113">Open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="72ad8-113">Open the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="72ad8-114">Select your HDInsight cluster, and then select **Ambari Views** from the **Quick Links** section.</span><span class="sxs-lookup"><span data-stu-id="72ad8-114">Select your HDInsight cluster, and then select **Ambari Views** from the **Quick Links** section.</span></span>

    ![Quick links section of the portal](./media/apache-hadoop-use-hive-ambari-view/quicklinks.png)

    <span data-ttu-id="72ad8-116">When prompted to authenticate, use the cluster login (default `admin`) account name and password that you provided when you created the cluster.</span><span class="sxs-lookup"><span data-stu-id="72ad8-116">When prompted to authenticate, use the cluster login (default `admin`) account name and password that you provided when you created the cluster.</span></span>

3. <span data-ttu-id="72ad8-117">From the list of views, select __Hive View__.</span><span class="sxs-lookup"><span data-stu-id="72ad8-117">From the list of views, select __Hive View__.</span></span>

    ![The Hive view selected](./media/apache-hadoop-use-hive-ambari-view/select-hive-view.png)

    <span data-ttu-id="72ad8-119">The Hive view page is similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="72ad8-119">The Hive view page is similar to the following image:</span></span>

    ![Image of the query worksheet for the Hive view](./media/apache-hadoop-use-hive-ambari-view/ambari-hive-view.png)

4. <span data-ttu-id="72ad8-121">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span><span class="sxs-lookup"><span data-stu-id="72ad8-121">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(
        t1 string,
        t2 string,
        t3 string,
        t4 string,
        t5 string,
        t6 string,
        t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS loglevel, COUNT(*) AS count FROM log4jLogs 
        WHERE t4 = '[ERROR]' 
        GROUP BY t4;
    ```

    <span data-ttu-id="72ad8-122">These statements perform the following actions:</span><span class="sxs-lookup"><span data-stu-id="72ad8-122">These statements perform the following actions:</span></span>

   * <span data-ttu-id="72ad8-123">`DROP TABLE`: Deletes the table and the data file, in case the table already exists.</span><span class="sxs-lookup"><span data-stu-id="72ad8-123">`DROP TABLE`: Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="72ad8-124">`CREATE EXTERNAL TABLE`: Creates a new "external" table in Hive.</span><span class="sxs-lookup"><span data-stu-id="72ad8-124">`CREATE EXTERNAL TABLE`: Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="72ad8-125">External tables store only the table definition in Hive.</span><span class="sxs-lookup"><span data-stu-id="72ad8-125">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="72ad8-126">The data is left in the original location.</span><span class="sxs-lookup"><span data-stu-id="72ad8-126">The data is left in the original location.</span></span>

   * <span data-ttu-id="72ad8-127">`ROW FORMAT`: Shows how the data is formatted.</span><span class="sxs-lookup"><span data-stu-id="72ad8-127">`ROW FORMAT`: Shows how the data is formatted.</span></span> <span data-ttu-id="72ad8-128">In this case, the fields in each log are separated by a space.</span><span class="sxs-lookup"><span data-stu-id="72ad8-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="72ad8-129">`STORED AS TEXTFILE LOCATION`: Shows where the data is stored, and that it's stored as text.</span><span class="sxs-lookup"><span data-stu-id="72ad8-129">`STORED AS TEXTFILE LOCATION`: Shows where the data is stored, and that it's stored as text.</span></span>

   * <span data-ttu-id="72ad8-130">`SELECT`: Selects a count of all rows where column t4 contains the value [ERROR].</span><span class="sxs-lookup"><span data-stu-id="72ad8-130">`SELECT`: Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="72ad8-131">Leave the __Database__ selection at __default__.</span><span class="sxs-lookup"><span data-stu-id="72ad8-131">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="72ad8-132">The examples in this document use the default database included with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72ad8-132">The examples in this document use the default database included with HDInsight.</span></span>

5. <span data-ttu-id="72ad8-133">To start the query, use the **Execute** button below the worksheet.</span><span class="sxs-lookup"><span data-stu-id="72ad8-133">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="72ad8-134">The button turns orange and the text changes to **Stop**.</span><span class="sxs-lookup"><span data-stu-id="72ad8-134">The button turns orange and the text changes to **Stop**.</span></span>

6. <span data-ttu-id="72ad8-135">After the query has finished, the **Results** tab displays the results of the operation.</span><span class="sxs-lookup"><span data-stu-id="72ad8-135">After the query has finished, the **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="72ad8-136">The following text is the result of the query:</span><span class="sxs-lookup"><span data-stu-id="72ad8-136">The following text is the result of the query:</span></span>

        loglevel       count
        [ERROR]        3

    <span data-ttu-id="72ad8-137">You can use the **Logs** tab to view the logging information that the job created.</span><span class="sxs-lookup"><span data-stu-id="72ad8-137">You can use the **Logs** tab to view the logging information that the job created.</span></span>

   > [!TIP]
   > <span data-ttu-id="72ad8-138">Download or save results from the **Save results** drop-down dialog box in the upper left of the **Query Process Results** section.</span><span class="sxs-lookup"><span data-stu-id="72ad8-138">Download or save results from the **Save results** drop-down dialog box in the upper left of the **Query Process Results** section.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="72ad8-139">Visual explain</span><span class="sxs-lookup"><span data-stu-id="72ad8-139">Visual explain</span></span>

<span data-ttu-id="72ad8-140">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span><span class="sxs-lookup"><span data-stu-id="72ad8-140">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="72ad8-141">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span><span class="sxs-lookup"><span data-stu-id="72ad8-141">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="72ad8-142">You can see a textual equivalent of this view by using the **Explain** button in the Query Editor.</span><span class="sxs-lookup"><span data-stu-id="72ad8-142">You can see a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="72ad8-143">Tez UI</span><span class="sxs-lookup"><span data-stu-id="72ad8-143">Tez UI</span></span>

<span data-ttu-id="72ad8-144">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span><span class="sxs-lookup"><span data-stu-id="72ad8-144">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72ad8-145">Tez is not used to resolve all queries.</span><span class="sxs-lookup"><span data-stu-id="72ad8-145">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="72ad8-146">You can resolve many queries without using Tez.</span><span class="sxs-lookup"><span data-stu-id="72ad8-146">You can resolve many queries without using Tez.</span></span> 

<span data-ttu-id="72ad8-147">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span><span class="sxs-lookup"><span data-stu-id="72ad8-147">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="72ad8-148">If you want to view the DAG for queries you've run in the past, or if you want to debug the Tez process, use the [Tez View](../hdinsight-debug-ambari-tez-view.md) instead.</span><span class="sxs-lookup"><span data-stu-id="72ad8-148">If you want to view the DAG for queries you've run in the past, or if you want to debug the Tez process, use the [Tez View](../hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="72ad8-149">View job history</span><span class="sxs-lookup"><span data-stu-id="72ad8-149">View job history</span></span>

<span data-ttu-id="72ad8-150">The __Jobs__ tab displays a history of Hive queries.</span><span class="sxs-lookup"><span data-stu-id="72ad8-150">The __Jobs__ tab displays a history of Hive queries.</span></span>

![Image of the job history](./media/apache-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="72ad8-152">Database tables</span><span class="sxs-lookup"><span data-stu-id="72ad8-152">Database tables</span></span>

<span data-ttu-id="72ad8-153">You can use the __Tables__ tab to work with tables within a Hive database.</span><span class="sxs-lookup"><span data-stu-id="72ad8-153">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Image of the tables tab](./media/apache-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="72ad8-155">Saved queries</span><span class="sxs-lookup"><span data-stu-id="72ad8-155">Saved queries</span></span>

<span data-ttu-id="72ad8-156">From the **Query** tab, you can optionally save queries.</span><span class="sxs-lookup"><span data-stu-id="72ad8-156">From the **Query** tab, you can optionally save queries.</span></span> <span data-ttu-id="72ad8-157">After you save a query, you can reuse it from the __Saved Queries__ tab.</span><span class="sxs-lookup"><span data-stu-id="72ad8-157">After you save a query, you can reuse it from the __Saved Queries__ tab.</span></span>

![Image of saved queries tab](./media/apache-hadoop-use-hive-ambari-view/saved-queries.png)

> [!TIP]
> <span data-ttu-id="72ad8-159">Saved queries are stored in the default cluster storage.</span><span class="sxs-lookup"><span data-stu-id="72ad8-159">Saved queries are stored in the default cluster storage.</span></span> <span data-ttu-id="72ad8-160">You can find the saved queries under the path `/user/<username>/hive/scripts`.</span><span class="sxs-lookup"><span data-stu-id="72ad8-160">You can find the saved queries under the path `/user/<username>/hive/scripts`.</span></span> <span data-ttu-id="72ad8-161">These are stored as plain-text `.hql` files.</span><span class="sxs-lookup"><span data-stu-id="72ad8-161">These are stored as plain-text `.hql` files.</span></span>
>
> <span data-ttu-id="72ad8-162">If you delete the cluster, but keep the storage, you can use a utility like [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) or Data Lake Storage Explorer (from the [Azure Portal](https://portal.azure.com)) to retrieve the queries.</span><span class="sxs-lookup"><span data-stu-id="72ad8-162">If you delete the cluster, but keep the storage, you can use a utility like [Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) or Data Lake Storage Explorer (from the [Azure Portal](https://portal.azure.com)) to retrieve the queries.</span></span>

## <a name="user-defined-functions"></a><span data-ttu-id="72ad8-163">User-defined functions</span><span class="sxs-lookup"><span data-stu-id="72ad8-163">User-defined functions</span></span>

<span data-ttu-id="72ad8-164">You can extend Hive through user-defined functions (UDF).</span><span class="sxs-lookup"><span data-stu-id="72ad8-164">You can extend Hive through user-defined functions (UDF).</span></span> <span data-ttu-id="72ad8-165">Use a UDF to implement functionality or logic that isn't easily modeled in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="72ad8-165">Use a UDF to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="72ad8-166">Declare and save a set of UDFs by using the **UDF** tab at the top of the Hive View.</span><span class="sxs-lookup"><span data-stu-id="72ad8-166">Declare and save a set of UDFs by using the **UDF** tab at the top of the Hive View.</span></span> <span data-ttu-id="72ad8-167">These UDFs can be used with the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="72ad8-167">These UDFs can be used with the **Query Editor**.</span></span>

![Image of UDF tab](./media/apache-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="72ad8-169">After you've added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span><span class="sxs-lookup"><span data-stu-id="72ad8-169">After you've added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="72ad8-170">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span><span class="sxs-lookup"><span data-stu-id="72ad8-170">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="72ad8-171">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span><span class="sxs-lookup"><span data-stu-id="72ad8-171">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="72ad8-172">For example, if you have defined a UDF with the following properties:</span><span class="sxs-lookup"><span data-stu-id="72ad8-172">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="72ad8-173">Resource name: myudfs</span><span class="sxs-lookup"><span data-stu-id="72ad8-173">Resource name: myudfs</span></span>

* <span data-ttu-id="72ad8-174">Resource path: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="72ad8-174">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="72ad8-175">UDF name: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="72ad8-175">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="72ad8-176">UDF class name: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="72ad8-176">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="72ad8-177">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down list for each UDF defined for that resource.</span><span class="sxs-lookup"><span data-stu-id="72ad8-177">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down list for each UDF defined for that resource.</span></span> <span data-ttu-id="72ad8-178">In this case, it is **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="72ad8-178">In this case, it is **myawesomeudf**.</span></span> <span data-ttu-id="72ad8-179">Selecting this entry adds the following to the beginning of the query:</span><span class="sxs-lookup"><span data-stu-id="72ad8-179">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="72ad8-180">You can then use the UDF in your query.</span><span class="sxs-lookup"><span data-stu-id="72ad8-180">You can then use the UDF in your query.</span></span> <span data-ttu-id="72ad8-181">For example, `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="72ad8-181">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="72ad8-182">For more information on using UDFs with Hive on HDInsight, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="72ad8-182">For more information on using UDFs with Hive on HDInsight, see the following articles:</span></span>

* [<span data-ttu-id="72ad8-183">Using Python with Hive and Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-183">Using Python with Hive and Pig in HDInsight</span></span>](python-udf-hdinsight.md)
* [<span data-ttu-id="72ad8-184">How to add a custom Hive UDF to HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-184">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="72ad8-185">Hive settings</span><span class="sxs-lookup"><span data-stu-id="72ad8-185">Hive settings</span></span>

<span data-ttu-id="72ad8-186">You can change various Hive settings, such as changing the execution engine for Hive from Tez (the default) to MapReduce.</span><span class="sxs-lookup"><span data-stu-id="72ad8-186">You can change various Hive settings, such as changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <a id="nextsteps"></a><span data-ttu-id="72ad8-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="72ad8-187">Next steps</span></span>

<span data-ttu-id="72ad8-188">For general information on Hive on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="72ad8-188">For general information on Hive on HDInsight:</span></span>

* [<span data-ttu-id="72ad8-189">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-189">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="72ad8-190">For information on other ways you can work with Hadoop on HDInsight:</span><span class="sxs-lookup"><span data-stu-id="72ad8-190">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="72ad8-191">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-191">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="72ad8-192">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="72ad8-192">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
