---
title: Use Ambari Tez View with HDInsight | Microsoft Docs
description: Learn how to use the Ambari Tez view to debug Tez jobs on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 9c39ea56-670b-4699-aba0-0f64c261e411
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: 60af16de8e3e803ac3abc2fdd22ee8f7c22d1f25
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549989"
---
# <a name="use-ambari-views-to-debug-tez-jobs-on-hdinsight"></a><span data-ttu-id="22f93-103">Use Ambari Views to debug Tez Jobs on HDInsight</span><span class="sxs-lookup"><span data-stu-id="22f93-103">Use Ambari Views to debug Tez Jobs on HDInsight</span></span>

<span data-ttu-id="22f93-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span><span class="sxs-lookup"><span data-stu-id="22f93-104">The Ambari Web UI for HDInsight contains a Tez view that can be used to understand and debug jobs that use Tez.</span></span> <span data-ttu-id="22f93-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span><span class="sxs-lookup"><span data-stu-id="22f93-105">The Tez view allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="22f93-106">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="22f93-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="22f93-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="22f93-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="22f93-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="22f93-108">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f93-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="22f93-109">Prerequisites</span></span>

* <span data-ttu-id="22f93-110">A Linux-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="22f93-110">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="22f93-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="22f93-111">For steps on creating a cluster, see [Get started using Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>
* <span data-ttu-id="22f93-112">A modern web browser that supports HTML5.</span><span class="sxs-lookup"><span data-stu-id="22f93-112">A modern web browser that supports HTML5.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="22f93-113">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="22f93-113">Understanding Tez</span></span>

<span data-ttu-id="22f93-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span><span class="sxs-lookup"><span data-stu-id="22f93-114">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="22f93-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span><span class="sxs-lookup"><span data-stu-id="22f93-115">For Linux-based HDInsight clusters, it is the default engine for Hive.</span></span>

<span data-ttu-id="22f93-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span><span class="sxs-lookup"><span data-stu-id="22f93-116">Tez creates a Directed Acyclic Graph (DAG) that describes the order of actions required by jobs.</span></span> <span data-ttu-id="22f93-117">Individual actions are called vertices, and execute a piece of the overall job.</span><span class="sxs-lookup"><span data-stu-id="22f93-117">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="22f93-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="22f93-118">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-view"></a><span data-ttu-id="22f93-119">Understanding the Tez view</span><span class="sxs-lookup"><span data-stu-id="22f93-119">Understanding the Tez view</span></span>

<span data-ttu-id="22f93-120">The Tez view provides both historical information and information on processes that are running.</span><span class="sxs-lookup"><span data-stu-id="22f93-120">The Tez view provides both historical information and information on processes that are running.</span></span> <span data-ttu-id="22f93-121">This information shows how a job is distributed across clusters.</span><span class="sxs-lookup"><span data-stu-id="22f93-121">This information shows how a job is distributed across clusters.</span></span> <span data-ttu-id="22f93-122">It also displays counters used by tasks and vertices, and error information related to the job.</span><span class="sxs-lookup"><span data-stu-id="22f93-122">It also displays counters used by tasks and vertices, and error information related to the job.</span></span> <span data-ttu-id="22f93-123">It may offer useful information in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="22f93-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="22f93-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span><span class="sxs-lookup"><span data-stu-id="22f93-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="22f93-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span><span class="sxs-lookup"><span data-stu-id="22f93-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="22f93-126">Generate a DAG</span><span class="sxs-lookup"><span data-stu-id="22f93-126">Generate a DAG</span></span>

<span data-ttu-id="22f93-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span><span class="sxs-lookup"><span data-stu-id="22f93-127">The Tez view only contains data if a job that uses the Tez engine is currently running, or has been ran previously.</span></span> <span data-ttu-id="22f93-128">Simple Hive queries can be resolved without using Tez.</span><span class="sxs-lookup"><span data-stu-id="22f93-128">Simple Hive queries can be resolved without using Tez.</span></span> <span data-ttu-id="22f93-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span><span class="sxs-lookup"><span data-stu-id="22f93-129">More complex queries that do filtering, grouping, ordering, joins, etc.</span></span> <span data-ttu-id="22f93-130">use the Tez engine.</span><span class="sxs-lookup"><span data-stu-id="22f93-130">use the Tez engine.</span></span>

<span data-ttu-id="22f93-131">Use the following steps to run a Hive query that uses Tez:</span><span class="sxs-lookup"><span data-stu-id="22f93-131">Use the following steps to run a Hive query that uses Tez:</span></span>

1. <span data-ttu-id="22f93-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="22f93-132">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>

2. <span data-ttu-id="22f93-133">From the menu at the top of the page, select the **Views** icon.</span><span class="sxs-lookup"><span data-stu-id="22f93-133">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="22f93-134">This icon looks like a series of squares.</span><span class="sxs-lookup"><span data-stu-id="22f93-134">This icon looks like a series of squares.</span></span> <span data-ttu-id="22f93-135">In the dropdown that appears, select **Hive view**.</span><span class="sxs-lookup"><span data-stu-id="22f93-135">In the dropdown that appears, select **Hive view**.</span></span>

    ![Selecting Hive View](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/selecthive.png)

3. <span data-ttu-id="22f93-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span><span class="sxs-lookup"><span data-stu-id="22f93-137">When the Hive view loads, paste the following query into the Query Editor, and then click **execute**.</span></span>

        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;

    <span data-ttu-id="22f93-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span><span class="sxs-lookup"><span data-stu-id="22f93-138">Once the job has completed, you should see the output displayed in the **Query Process Results** section.</span></span> <span data-ttu-id="22f93-139">The results should be similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="22f93-139">The results should be similar to the following text:</span></span>

        market  state       country
        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica

4. <span data-ttu-id="22f93-140">Select the **Log** tab. You see information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="22f93-140">Select the **Log** tab. You see information similar to the following text:</span></span>

        INFO : Session is already open
        INFO :

        INFO : Status: Running (Executing on YARN cluster with App id application_1454546500517_0063)

    <span data-ttu-id="22f93-141">Save the **App id** value, as this value is used in the next section.</span><span class="sxs-lookup"><span data-stu-id="22f93-141">Save the **App id** value, as this value is used in the next section.</span></span>

## <a name="use-the-tez-view"></a><span data-ttu-id="22f93-142">Use the Tez View</span><span class="sxs-lookup"><span data-stu-id="22f93-142">Use the Tez View</span></span>

1. <span data-ttu-id="22f93-143">From the menu at the top of the page, select the **Views** icon.</span><span class="sxs-lookup"><span data-stu-id="22f93-143">From the menu at the top of the page, select the **Views** icon.</span></span> <span data-ttu-id="22f93-144">In the dropdown that appears, select **Tez view**.</span><span class="sxs-lookup"><span data-stu-id="22f93-144">In the dropdown that appears, select **Tez view**.</span></span>

    ![Selecting Tez view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/selecttez.png)

2. <span data-ttu-id="22f93-146">When the Tez view loads, you see a list of DAGs that are currently running, or have been ran on the cluster.</span><span class="sxs-lookup"><span data-stu-id="22f93-146">When the Tez view loads, you see a list of DAGs that are currently running, or have been ran on the cluster.</span></span>

    ![All DAGS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/alldags.png)

3. <span data-ttu-id="22f93-148">If you have only one entry, it is for the query that you ran in the previous section.</span><span class="sxs-lookup"><span data-stu-id="22f93-148">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="22f93-149">If you have multiple entries, you can search by entering the application ID in the **Application ID** field, and then press enter.</span><span class="sxs-lookup"><span data-stu-id="22f93-149">If you have multiple entries, you can search by entering the application ID in the **Application ID** field, and then press enter.</span></span>

4. <span data-ttu-id="22f93-150">Select the **Dag Name**.</span><span class="sxs-lookup"><span data-stu-id="22f93-150">Select the **Dag Name**.</span></span> <span data-ttu-id="22f93-151">Information about the DAG is displayed.</span><span class="sxs-lookup"><span data-stu-id="22f93-151">Information about the DAG is displayed.</span></span> <span data-ttu-id="22f93-152">You can also download a zip of JSON files containing this information.</span><span class="sxs-lookup"><span data-stu-id="22f93-152">You can also download a zip of JSON files containing this information.</span></span>

    ![DAG Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/dagdetails.png)

5. <span data-ttu-id="22f93-154">Above the **DAG Details** are several links that can be used to display information about the DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-154">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="22f93-155">**DAG Counters**: Displays counters information for this DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-155">**DAG Counters**: Displays counters information for this DAG.</span></span>
   * <span data-ttu-id="22f93-156">**Graphical View**: Displays a graphical representation of this DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-156">**Graphical View**: Displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="22f93-157">**All Vertices**: Displays a list of the vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-157">**All Vertices**: Displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="22f93-158">**All Tasks**: Displays a list of the tasks for all vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-158">**All Tasks**: Displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="22f93-159">**All TaskAttempts**: Displays information about the attempts to run tasks for this DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-159">**All TaskAttempts**: Displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="22f93-160">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span><span class="sxs-lookup"><span data-stu-id="22f93-160">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>

     <span data-ttu-id="22f93-161">If there was a failure with the job, the DAG Details display a status of FAILED, along with links to information about the failed task.</span><span class="sxs-lookup"><span data-stu-id="22f93-161">If there was a failure with the job, the DAG Details display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="22f93-162">Diagnostics information is displayed beneath the DAG details.</span><span class="sxs-lookup"><span data-stu-id="22f93-162">Diagnostics information is displayed beneath the DAG details.</span></span>

     ![A DAG Details screen detailing a failure](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/faileddag.png)

6. <span data-ttu-id="22f93-164">Select **Graphical View**.</span><span class="sxs-lookup"><span data-stu-id="22f93-164">Select **Graphical View**.</span></span> <span data-ttu-id="22f93-165">This view displays a graphical representation of the DAG.</span><span class="sxs-lookup"><span data-stu-id="22f93-165">This view displays a graphical representation of the DAG.</span></span> <span data-ttu-id="22f93-166">You can place the mouse over each vertex in the view to display information about it.</span><span class="sxs-lookup"><span data-stu-id="22f93-166">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Graphical view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/dagdiagram.png)

7. <span data-ttu-id="22f93-168">Select a vertex to load the **Vertex Details** for that item.</span><span class="sxs-lookup"><span data-stu-id="22f93-168">Select a vertex to load the **Vertex Details** for that item.</span></span> <span data-ttu-id="22f93-169">Select the **Map 1** vertex to display details for this item.</span><span class="sxs-lookup"><span data-stu-id="22f93-169">Select the **Map 1** vertex to display details for this item.</span></span>

    ![Vertex details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/vertexdetails.png)

8. <span data-ttu-id="22f93-171">You now have links at the top of the page that are related to vertices and tasks.</span><span class="sxs-lookup"><span data-stu-id="22f93-171">You now have links at the top of the page that are related to vertices and tasks.</span></span>

   > [!NOTE]
   > <span data-ttu-id="22f93-172">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span><span class="sxs-lookup"><span data-stu-id="22f93-172">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>

   * <span data-ttu-id="22f93-173">**Vertex Counters**: Displays counter information for this vertex.</span><span class="sxs-lookup"><span data-stu-id="22f93-173">**Vertex Counters**: Displays counter information for this vertex.</span></span>
   * <span data-ttu-id="22f93-174">**Tasks**: Displays tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="22f93-174">**Tasks**: Displays tasks for this vertex.</span></span>
   * <span data-ttu-id="22f93-175">**Task Attempts**: Displays information about attempts to run tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="22f93-175">**Task Attempts**: Displays information about attempts to run tasks for this vertex.</span></span>
   * <span data-ttu-id="22f93-176">**Sources & Sinks**: Displays data sources and sinks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="22f93-176">**Sources & Sinks**: Displays data sources and sinks for this vertex.</span></span>

     > [!NOTE]
     > <span data-ttu-id="22f93-177">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span><span class="sxs-lookup"><span data-stu-id="22f93-177">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>

9. <span data-ttu-id="22f93-178">Select **Tasks**, and then select the item named **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="22f93-178">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="22f93-179">The **Task Details** for this task appear.</span><span class="sxs-lookup"><span data-stu-id="22f93-179">The **Task Details** for this task appear.</span></span> <span data-ttu-id="22f93-180">From this screen, you can view **Task Counters** and **Task Attempts**.</span><span class="sxs-lookup"><span data-stu-id="22f93-180">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

   ![Task details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-ambari-tez-view/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="22f93-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="22f93-182">Next Steps</span></span>

<span data-ttu-id="22f93-183">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="22f93-183">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="22f93-184">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="22f93-184">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="22f93-185">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="22f93-185">For more information on using Ambari with HDInsight, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md)</span></span>








