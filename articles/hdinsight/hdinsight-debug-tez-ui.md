---
title: Use Tez UI with Windows-based HDInsight | Microsoft Docs
description: Learn how to use the Tez UI to debug Tez jobs on Windows-based HDInsight HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 49439d4c687d39003789a25bc074f68dc01e558e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669679"
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="31b0b-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="31b0b-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="31b0b-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="31b0b-104">The Tez UI is a web page that can be used to understand and debug jobs that use Tez as the execution engine on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="31b0b-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span><span class="sxs-lookup"><span data-stu-id="31b0b-105">The Tez UI allows you to visualize the job as a graph of connected items, drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="31b0b-106">The steps in this document require an HDInsight cluster that uses Windows.</span><span class="sxs-lookup"><span data-stu-id="31b0b-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="31b0b-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="31b0b-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="31b0b-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="31b0b-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="31b0b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="31b0b-109">Prerequisites</span></span>
* <span data-ttu-id="31b0b-110">A Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="31b0b-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="31b0b-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="31b0b-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="31b0b-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span><span class="sxs-lookup"><span data-stu-id="31b0b-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="31b0b-113">A Windows-based Remote Desktop client.</span><span class="sxs-lookup"><span data-stu-id="31b0b-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="31b0b-114">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="31b0b-114">Understanding Tez</span></span>
<span data-ttu-id="31b0b-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span><span class="sxs-lookup"><span data-stu-id="31b0b-115">Tez is an extensible framework for data processing in Hadoop that provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="31b0b-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span><span class="sxs-lookup"><span data-stu-id="31b0b-116">For Windows-based HDInsight clusters, it is an optional engine that you can enable for Hive by using the following command as part of your Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="31b0b-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span><span class="sxs-lookup"><span data-stu-id="31b0b-117">When work is submitted to Tez, it creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="31b0b-118">Individual actions are called vertices, and execute a piece of the overall job.</span><span class="sxs-lookup"><span data-stu-id="31b0b-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="31b0b-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="31b0b-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="31b0b-120">Understanding the Tez UI</span><span class="sxs-lookup"><span data-stu-id="31b0b-120">Understanding the Tez UI</span></span>
<span data-ttu-id="31b0b-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span><span class="sxs-lookup"><span data-stu-id="31b0b-121">The Tez UI is a web page provides information on processes that are running, or have previously ran using Tez.</span></span> <span data-ttu-id="31b0b-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span><span class="sxs-lookup"><span data-stu-id="31b0b-122">It allows you to view the DAG generated by Tez, how it is distributed across clusters, counters such as memory used by tasks and vertices, and error information.</span></span> <span data-ttu-id="31b0b-123">It may offer useful information in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="31b0b-123">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="31b0b-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span><span class="sxs-lookup"><span data-stu-id="31b0b-124">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="31b0b-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span><span class="sxs-lookup"><span data-stu-id="31b0b-125">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="31b0b-126">Generate a DAG</span><span class="sxs-lookup"><span data-stu-id="31b0b-126">Generate a DAG</span></span>
<span data-ttu-id="31b0b-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span><span class="sxs-lookup"><span data-stu-id="31b0b-127">The Tez UI will only contain data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="31b0b-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span><span class="sxs-lookup"><span data-stu-id="31b0b-128">Simple Hive queries can usually be resolved without using Tez, however more complex queries that do filtering, grouping, ordering, joins, etc. will usually require Tez.</span></span>

<span data-ttu-id="31b0b-129">Use the following steps to run a Hive query that will execute using Tez.</span><span class="sxs-lookup"><span data-stu-id="31b0b-129">Use the following steps to run a Hive query that will execute using Tez.</span></span>

1. <span data-ttu-id="31b0b-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="31b0b-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="31b0b-131">From the menu at the top of the page, select the **Hive Editor**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="31b0b-132">This will display a page with the following example query.</span><span class="sxs-lookup"><span data-stu-id="31b0b-132">This will display a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="31b0b-133">Erase the example query and replace it with the following.</span><span class="sxs-lookup"><span data-stu-id="31b0b-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="31b0b-134">Select the **Submit** button.</span><span class="sxs-lookup"><span data-stu-id="31b0b-134">Select the **Submit** button.</span></span> <span data-ttu-id="31b0b-135">The **Job Session** section at the bottom of the page will display the status of the query.</span><span class="sxs-lookup"><span data-stu-id="31b0b-135">The **Job Session** section at the bottom of the page will display the status of the query.</span></span> <span data-ttu-id="31b0b-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span><span class="sxs-lookup"><span data-stu-id="31b0b-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="31b0b-137">The **Job Output** should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="31b0b-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="31b0b-138">Use the Tez UI</span><span class="sxs-lookup"><span data-stu-id="31b0b-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="31b0b-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span><span class="sxs-lookup"><span data-stu-id="31b0b-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="31b0b-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="31b0b-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="31b0b-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span><span class="sxs-lookup"><span data-stu-id="31b0b-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="31b0b-142">This will display the remote desktop blade</span><span class="sxs-lookup"><span data-stu-id="31b0b-142">This will display the remote desktop blade</span></span>

    ![Remote desktop icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="31b0b-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="31b0b-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="31b0b-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span><span class="sxs-lookup"><span data-stu-id="31b0b-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Remote desktop connect icon](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="31b0b-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="31b0b-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="31b0b-148">Once it has been enabled, use the previous steps to connect.</span><span class="sxs-lookup"><span data-stu-id="31b0b-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="31b0b-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="31b0b-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="31b0b-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="31b0b-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="31b0b-152">This will display the Tez UI</span><span class="sxs-lookup"><span data-stu-id="31b0b-152">This will display the Tez UI</span></span>

    ![Tez UI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="31b0b-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span><span class="sxs-lookup"><span data-stu-id="31b0b-154">When the Tez UI loads, you will see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="31b0b-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span><span class="sxs-lookup"><span data-stu-id="31b0b-155">The default view includes the Dag Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="31b0b-156">More columns can be added using the gear icon at the right of the page.</span><span class="sxs-lookup"><span data-stu-id="31b0b-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="31b0b-157">If you have only one entry, it will be for the query that you ran in the previous section.</span><span class="sxs-lookup"><span data-stu-id="31b0b-157">If you have only one entry, it will be for the query that you ran in the previous section.</span></span> <span data-ttu-id="31b0b-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="31b0b-159">Select the **Dag Name** for the most recent DAG entry.</span><span class="sxs-lookup"><span data-stu-id="31b0b-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="31b0b-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-160">This will display information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="31b0b-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="31b0b-163">**DAG Counters** displays counters information for this DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="31b0b-164">**Graphical View** displays a graphical representation of this DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="31b0b-165">**All Vertices** displays a list of the vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="31b0b-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="31b0b-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="31b0b-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span><span class="sxs-lookup"><span data-stu-id="31b0b-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="31b0b-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span><span class="sxs-lookup"><span data-stu-id="31b0b-169">If there was a failure with the job, the DAG Details will display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="31b0b-170">Diagnostics information will be displayed beneath the DAG details.</span><span class="sxs-lookup"><span data-stu-id="31b0b-170">Diagnostics information will be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="31b0b-171">Select **Graphical View**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-171">Select **Graphical View**.</span></span> <span data-ttu-id="31b0b-172">This displays a graphical representation of the DAG.</span><span class="sxs-lookup"><span data-stu-id="31b0b-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="31b0b-173">You can place the mouse over each vertex in the view to display information about it.</span><span class="sxs-lookup"><span data-stu-id="31b0b-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Graphical view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="31b0b-175">Clicking on a vertex will load the **Vertex Details** for that item.</span><span class="sxs-lookup"><span data-stu-id="31b0b-175">Clicking on a vertex will load the **Vertex Details** for that item.</span></span> <span data-ttu-id="31b0b-176">Click on the **Map 1** vertex to display details for this item.</span><span class="sxs-lookup"><span data-stu-id="31b0b-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="31b0b-177">Select **Confirm** to confirm the navigation.</span><span class="sxs-lookup"><span data-stu-id="31b0b-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Vertex details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="31b0b-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span><span class="sxs-lookup"><span data-stu-id="31b0b-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="31b0b-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span><span class="sxs-lookup"><span data-stu-id="31b0b-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="31b0b-181">**Vertex Counters** displays counter information for this vertex.</span><span class="sxs-lookup"><span data-stu-id="31b0b-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="31b0b-182">**Tasks** displays tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="31b0b-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="31b0b-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="31b0b-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="31b0b-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="31b0b-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="31b0b-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span><span class="sxs-lookup"><span data-stu-id="31b0b-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="31b0b-186">Select **Tasks**, and then select the item named **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="31b0b-187">This will display **Task Details** for this task.</span><span class="sxs-lookup"><span data-stu-id="31b0b-187">This will display **Task Details** for this task.</span></span> <span data-ttu-id="31b0b-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span><span class="sxs-lookup"><span data-stu-id="31b0b-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Task details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="31b0b-190">Next Steps</span><span class="sxs-lookup"><span data-stu-id="31b0b-190">Next Steps</span></span>
<span data-ttu-id="31b0b-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="31b0b-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="31b0b-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="31b0b-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>







