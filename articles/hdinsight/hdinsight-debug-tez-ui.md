---
title: Use Tez UI with Windows-based HDInsight - Azure
description: Learn how to use the Tez UI to debug Tez jobs on Windows-based HDInsight HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 01/17/2017
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: ff47d0a71e97ce4ec9fd04e1d0cb9e5592192d53
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776642"
---
# <a name="use-the-tez-ui-to-debug-tez-jobs-on-windows-based-hdinsight"></a><span data-ttu-id="3dda7-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="3dda7-103">Use the Tez UI to debug Tez Jobs on Windows-based HDInsight</span></span>
<span data-ttu-id="3dda7-104">The Tez UI can be used to debug Hive jobs that use Tez as the execution engine.</span><span class="sxs-lookup"><span data-stu-id="3dda7-104">The Tez UI can be used to debug Hive jobs that use Tez as the execution engine.</span></span> <span data-ttu-id="3dda7-105">The Tez UI visualizes the job as a graph of connected items, can drill into each item, and retrieve statistics and logging information.</span><span class="sxs-lookup"><span data-stu-id="3dda7-105">The Tez UI visualizes the job as a graph of connected items, can drill into each item, and retrieve statistics and logging information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dda7-106">The steps in this document require an HDInsight cluster that uses Windows.</span><span class="sxs-lookup"><span data-stu-id="3dda7-106">The steps in this document require an HDInsight cluster that uses Windows.</span></span> <span data-ttu-id="3dda7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3dda7-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3dda7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3dda7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3dda7-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3dda7-109">Prerequisites</span></span>
* <span data-ttu-id="3dda7-110">A Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3dda7-110">A Windows-based HDInsight cluster.</span></span> <span data-ttu-id="3dda7-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3dda7-111">For steps on creating a new cluster, see [Get started using Windows-based HDInsight](hdinsight-hadoop-tutorial-get-started-windows.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3dda7-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span><span class="sxs-lookup"><span data-stu-id="3dda7-112">The Tez UI is only available on Windows-based HDInsight clusters created after February 8th, 2016.</span></span>
  >
  >
* <span data-ttu-id="3dda7-113">A Windows-based Remote Desktop client.</span><span class="sxs-lookup"><span data-stu-id="3dda7-113">A Windows-based Remote Desktop client.</span></span>

## <a name="understanding-tez"></a><span data-ttu-id="3dda7-114">Understanding Tez</span><span class="sxs-lookup"><span data-stu-id="3dda7-114">Understanding Tez</span></span>
<span data-ttu-id="3dda7-115">Tez is an extensible framework for data processing in Hadoop, and provides greater speeds than traditional MapReduce processing.</span><span class="sxs-lookup"><span data-stu-id="3dda7-115">Tez is an extensible framework for data processing in Hadoop, and provides greater speeds than traditional MapReduce processing.</span></span> <span data-ttu-id="3dda7-116">You can enable Tez by including the following text as part of a Hive query:</span><span class="sxs-lookup"><span data-stu-id="3dda7-116">You can enable Tez by including the following text as part of a Hive query:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="3dda7-117">Tez creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span><span class="sxs-lookup"><span data-stu-id="3dda7-117">Tez creates a Directed Acyclic Graph (DAG) that describes the order of execution of the actions required by the job.</span></span> <span data-ttu-id="3dda7-118">Individual actions are called vertices, and execute a piece of the overall job.</span><span class="sxs-lookup"><span data-stu-id="3dda7-118">Individual actions are called vertices, and execute a piece of the overall job.</span></span> <span data-ttu-id="3dda7-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="3dda7-119">The actual execution of the work described by a vertex is called a task, and may be distributed across multiple nodes in the cluster.</span></span>

### <a name="understanding-the-tez-ui"></a><span data-ttu-id="3dda7-120">Understanding the Tez UI</span><span class="sxs-lookup"><span data-stu-id="3dda7-120">Understanding the Tez UI</span></span>
<span data-ttu-id="3dda7-121">The Tez UI is a web page provides information on processes that use Tez.</span><span class="sxs-lookup"><span data-stu-id="3dda7-121">The Tez UI is a web page provides information on processes that use Tez.</span></span> <span data-ttu-id="3dda7-122">It may offer useful information in the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="3dda7-122">It may offer useful information in the following scenarios:</span></span>

* <span data-ttu-id="3dda7-123">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span><span class="sxs-lookup"><span data-stu-id="3dda7-123">Monitoring long-running processes, viewing the progress of map and reduce tasks.</span></span>
* <span data-ttu-id="3dda7-124">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span><span class="sxs-lookup"><span data-stu-id="3dda7-124">Analyzing historical data for successful or failed processes to learn how processing could be improved or why it failed.</span></span>

## <a name="generate-a-dag"></a><span data-ttu-id="3dda7-125">Generate a DAG</span><span class="sxs-lookup"><span data-stu-id="3dda7-125">Generate a DAG</span></span>
<span data-ttu-id="3dda7-126">The Tez UI contains data if a job that uses the Tez engine is currently running, or has been ran in the past.</span><span class="sxs-lookup"><span data-stu-id="3dda7-126">The Tez UI contains data if a job that uses the Tez engine is currently running, or has been ran in the past.</span></span> <span data-ttu-id="3dda7-127">Simple Hive queries can usually be resolved without using Tez.</span><span class="sxs-lookup"><span data-stu-id="3dda7-127">Simple Hive queries can usually be resolved without using Tez.</span></span> <span data-ttu-id="3dda7-128">More complex queries that do filtering, grouping, ordering, joins, etc. require Tez.</span><span class="sxs-lookup"><span data-stu-id="3dda7-128">More complex queries that do filtering, grouping, ordering, joins, etc. require Tez.</span></span>

<span data-ttu-id="3dda7-129">Use the following steps to run a Hive query that uses Tez.</span><span class="sxs-lookup"><span data-stu-id="3dda7-129">Use the following steps to run a Hive query that uses Tez.</span></span>

1. <span data-ttu-id="3dda7-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3dda7-130">In a web browser, navigate to https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span>
2. <span data-ttu-id="3dda7-131">From the menu at the top of the page, select the **Hive Editor**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-131">From the menu at the top of the page, select the **Hive Editor**.</span></span> <span data-ttu-id="3dda7-132">This displays a page with the following example query.</span><span class="sxs-lookup"><span data-stu-id="3dda7-132">This displays a page with the following example query.</span></span>

        Select * from hivesampletable

    <span data-ttu-id="3dda7-133">Erase the example query and replace it with the following.</span><span class="sxs-lookup"><span data-stu-id="3dda7-133">Erase the example query and replace it with the following.</span></span>

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. <span data-ttu-id="3dda7-134">Select the **Submit** button.</span><span class="sxs-lookup"><span data-stu-id="3dda7-134">Select the **Submit** button.</span></span> <span data-ttu-id="3dda7-135">The **Job Session** section at the bottom of the page displays the status of the query.</span><span class="sxs-lookup"><span data-stu-id="3dda7-135">The **Job Session** section at the bottom of the page displays the status of the query.</span></span> <span data-ttu-id="3dda7-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span><span class="sxs-lookup"><span data-stu-id="3dda7-136">Once the status changes to **Completed**, select the **View Details** link to view the results.</span></span> <span data-ttu-id="3dda7-137">The **Job Output** should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="3dda7-137">The **Job Output** should be similar to the following:</span></span>

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-the-tez-ui"></a><span data-ttu-id="3dda7-138">Use the Tez UI</span><span class="sxs-lookup"><span data-stu-id="3dda7-138">Use the Tez UI</span></span>
> [!NOTE]
> <span data-ttu-id="3dda7-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span><span class="sxs-lookup"><span data-stu-id="3dda7-139">The Tez UI is only available from the desktop of the cluster head nodes, so you must use Remote Desktop to connect to the head nodes.</span></span>
>
>

1. <span data-ttu-id="3dda7-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3dda7-140">From the [Azure portal](https://portal.azure.com), select your HDInsight cluster.</span></span> <span data-ttu-id="3dda7-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span><span class="sxs-lookup"><span data-stu-id="3dda7-141">From the top of the HDInsight blade, select the **Remote Desktop** icon.</span></span> <span data-ttu-id="3dda7-142">This link displays the remote desktop blade</span><span class="sxs-lookup"><span data-stu-id="3dda7-142">This link displays the remote desktop blade</span></span>

    ![Remote desktop icon](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. <span data-ttu-id="3dda7-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="3dda7-144">From the Remote Desktop blade, select **Connect** to connect to the cluster head node.</span></span> <span data-ttu-id="3dda7-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span><span class="sxs-lookup"><span data-stu-id="3dda7-145">When prompted, use the cluster Remote Desktop user name and password to authenticate the connection.</span></span>

    ![Remote desktop connect icon](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > <span data-ttu-id="3dda7-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="3dda7-147">If you have not enabled Remote Desktop connectivity, provide a user name, password, and expiration date, then select **Enable** to enable Remote Desktop.</span></span> <span data-ttu-id="3dda7-148">Once it has been enabled, use the previous steps to connect.</span><span class="sxs-lookup"><span data-stu-id="3dda7-148">Once it has been enabled, use the previous steps to connect.</span></span>
   >
   >
3. <span data-ttu-id="3dda7-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-149">Once connected, open Internet Explorer on the remote desktop, select the gear icon in the upper right of the browser, and then select **Compatibility View Settings**.</span></span>
4. <span data-ttu-id="3dda7-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-150">From the bottom of **Compatibility View Settings**, clear the check box for **Display intranet sites in Compatibility View** and **Use Microsoft compatibility lists**, and then select **Close**.</span></span>
5. <span data-ttu-id="3dda7-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span><span class="sxs-lookup"><span data-stu-id="3dda7-151">In Internet Explorer, browse to http://headnodehost:8188/tezui/#/.</span></span> <span data-ttu-id="3dda7-152">This displays the Tez UI</span><span class="sxs-lookup"><span data-stu-id="3dda7-152">This displays the Tez UI</span></span>

    ![Tez UI](./media/hdinsight-debug-tez-ui/tezui.png)

    <span data-ttu-id="3dda7-154">When the Tez UI loads, you see a list of DAGs that are currently running, or have been ran on the cluster.</span><span class="sxs-lookup"><span data-stu-id="3dda7-154">When the Tez UI loads, you see a list of DAGs that are currently running, or have been ran on the cluster.</span></span> <span data-ttu-id="3dda7-155">The default view includes the DAG Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span><span class="sxs-lookup"><span data-stu-id="3dda7-155">The default view includes the DAG Name, Id, Submitter, Status, Start Time, End Time, Duration, Application ID, and Queue.</span></span> <span data-ttu-id="3dda7-156">More columns can be added using the gear icon at the right of the page.</span><span class="sxs-lookup"><span data-stu-id="3dda7-156">More columns can be added using the gear icon at the right of the page.</span></span>

    <span data-ttu-id="3dda7-157">If you have only one entry, it is for the query that you ran in the previous section.</span><span class="sxs-lookup"><span data-stu-id="3dda7-157">If you have only one entry, it is for the query that you ran in the previous section.</span></span> <span data-ttu-id="3dda7-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-158">If you have multiple entries, you can search by entering search criteria in the fields above the DAGs, then hit **Enter**.</span></span>
6. <span data-ttu-id="3dda7-159">Select the **Dag Name** for the most recent DAG entry.</span><span class="sxs-lookup"><span data-stu-id="3dda7-159">Select the **Dag Name** for the most recent DAG entry.</span></span> <span data-ttu-id="3dda7-160">This link displays information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-160">This link displays information about the DAG, as well as the option to download a zip of JSON files that contain information about the DAG.</span></span>

    ![DAG Details](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. <span data-ttu-id="3dda7-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-162">Above the **DAG Details** are several links that can be used to display information about the DAG.</span></span>

   * <span data-ttu-id="3dda7-163">**DAG Counters** displays counters information for this DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-163">**DAG Counters** displays counters information for this DAG.</span></span>
   * <span data-ttu-id="3dda7-164">**Graphical View** displays a graphical representation of this DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-164">**Graphical View** displays a graphical representation of this DAG.</span></span>
   * <span data-ttu-id="3dda7-165">**All Vertices** displays a list of the vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-165">**All Vertices** displays a list of the vertices in this DAG.</span></span>
   * <span data-ttu-id="3dda7-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-166">**All Tasks** displays a list of the tasks for all vertices in this DAG.</span></span>
   * <span data-ttu-id="3dda7-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-167">**All TaskAttempts** displays information about the attempts to run tasks for this DAG.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3dda7-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span><span class="sxs-lookup"><span data-stu-id="3dda7-168">If you scroll the column display for Vertices, Tasks and TaskAttempts, notice that there are links to view **counters** and **view or download logs** for each row.</span></span>
     >
     >

     <span data-ttu-id="3dda7-169">If there was a failure with the job, the DAG Details display a status of FAILED, along with links to information about the failed task.</span><span class="sxs-lookup"><span data-stu-id="3dda7-169">If there was a failure with the job, the DAG Details display a status of FAILED, along with links to information about the failed task.</span></span> <span data-ttu-id="3dda7-170">Diagnostics information is be displayed beneath the DAG details.</span><span class="sxs-lookup"><span data-stu-id="3dda7-170">Diagnostics information is be displayed beneath the DAG details.</span></span>
8. <span data-ttu-id="3dda7-171">Select **Graphical View**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-171">Select **Graphical View**.</span></span> <span data-ttu-id="3dda7-172">This displays a graphical representation of the DAG.</span><span class="sxs-lookup"><span data-stu-id="3dda7-172">This displays a graphical representation of the DAG.</span></span> <span data-ttu-id="3dda7-173">You can place the mouse over each vertex in the view to display information about it.</span><span class="sxs-lookup"><span data-stu-id="3dda7-173">You can place the mouse over each vertex in the view to display information about it.</span></span>

    ![Graphical view](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. <span data-ttu-id="3dda7-175">Clicking on a vertex loads the **Vertex Details** for that item.</span><span class="sxs-lookup"><span data-stu-id="3dda7-175">Clicking on a vertex loads the **Vertex Details** for that item.</span></span> <span data-ttu-id="3dda7-176">Click on the **Map 1** vertex to display details for this item.</span><span class="sxs-lookup"><span data-stu-id="3dda7-176">Click on the **Map 1** vertex to display details for this item.</span></span> <span data-ttu-id="3dda7-177">Select **Confirm** to confirm the navigation.</span><span class="sxs-lookup"><span data-stu-id="3dda7-177">Select **Confirm** to confirm the navigation.</span></span>

    ![Vertex details](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. <span data-ttu-id="3dda7-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span><span class="sxs-lookup"><span data-stu-id="3dda7-179">Note that you now have links at the top of the page that are related to vertices and tasks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="3dda7-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span><span class="sxs-lookup"><span data-stu-id="3dda7-180">You can also arrive at this page by going back to **DAG Details**, selecting **Vertex Details**, and then selecting the **Map 1** vertex.</span></span>
    >
    >

    * <span data-ttu-id="3dda7-181">**Vertex Counters** displays counter information for this vertex.</span><span class="sxs-lookup"><span data-stu-id="3dda7-181">**Vertex Counters** displays counter information for this vertex.</span></span>
    * <span data-ttu-id="3dda7-182">**Tasks** displays tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="3dda7-182">**Tasks** displays tasks for this vertex.</span></span>
    * <span data-ttu-id="3dda7-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="3dda7-183">**Task Attempts** displays information about attempts to run tasks for this vertex.</span></span>
    * <span data-ttu-id="3dda7-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span><span class="sxs-lookup"><span data-stu-id="3dda7-184">**Sources & Sinks** displays data sources and sinks for this vertex.</span></span>

      > [!NOTE]
      > <span data-ttu-id="3dda7-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span><span class="sxs-lookup"><span data-stu-id="3dda7-185">As with the previous menu, you can scroll the column display for Tasks, Task Attempts, and Sources & Sinks__ to display links to more information for each item.</span></span>
      >
      >
11. <span data-ttu-id="3dda7-186">Select **Tasks**, and then select the item named **00_000000**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-186">Select **Tasks**, and then select the item named **00_000000**.</span></span> <span data-ttu-id="3dda7-187">This link displays **Task Details** for this task.</span><span class="sxs-lookup"><span data-stu-id="3dda7-187">This link displays **Task Details** for this task.</span></span> <span data-ttu-id="3dda7-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span><span class="sxs-lookup"><span data-stu-id="3dda7-188">From this screen, you can view **Task Counters** and **Task Attempts**.</span></span>

    ![Task details](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a><span data-ttu-id="3dda7-190">Next Steps</span><span class="sxs-lookup"><span data-stu-id="3dda7-190">Next Steps</span></span>
<span data-ttu-id="3dda7-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hadoop/hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="3dda7-191">Now that you have learned how to use the Tez view, learn more about [Using Hive on HDInsight](hadoop/hdinsight-use-hive.md).</span></span>

<span data-ttu-id="3dda7-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="3dda7-192">For more detailed technical information on Tez, see the [Tez page at Hortonworks](http://hortonworks.com/hadoop/tez/).</span></span>
