---
title: Deploy and manage Apache Storm topologies in Azure HDInsight
description: Learn how to deploy, monitor and manage Apache Storm topologies using the Storm Dashboard on Windows-based HDInsight. Use Hadoop tools for Visual Studio.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 03/01/2017
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: 97dfa2ffc103de377b4c510d2a3a7404b5e96747
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966657"
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="1bfe3-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="1bfe3-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="1bfe3-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="1bfe3-106">You can also use the dashboard to monitor and manage running topologies.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="1bfe3-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="1bfe3-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1bfe3-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="1bfe3-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1bfe3-111">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-111">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="1bfe3-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](apache-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="1bfe3-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](apache-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1bfe3-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1bfe3-113">Prerequisites</span></span>

* <span data-ttu-id="1bfe3-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="1bfe3-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="1bfe3-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="1bfe3-117">See [Get started using HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-117">See [Get started using HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="1bfe3-118">One of the following versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="1bfe3-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="1bfe3-119">Visual Studio 2012 with Update 4</span><span class="sxs-lookup"><span data-stu-id="1bfe3-119">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="1bfe3-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span><span class="sxs-lookup"><span data-stu-id="1bfe3-120">Visual Studio 2013 with Update 4 or Visual Studio 2013 Community</span></span>

  * <span data-ttu-id="1bfe3-121">Visual Studio 2015 (any edition)</span><span class="sxs-lookup"><span data-stu-id="1bfe3-121">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="1bfe3-122">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="1bfe3-122">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="1bfe3-123">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="1bfe3-123">Storm Dashboard</span></span>

<span data-ttu-id="1bfe3-124">The Storm Dashboard is a web page available on your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-124">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="1bfe3-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-125">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="1bfe3-126">From the top of the Storm Dashboard, select **Submit Topology**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-126">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="1bfe3-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-127">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![the submit topology page][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="1bfe3-129">Storm UI</span><span class="sxs-lookup"><span data-stu-id="1bfe3-129">Storm UI</span></span>

<span data-ttu-id="1bfe3-130">From the Storm Dashboard, select the **Storm UI** link.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-130">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="1bfe3-131">This displays information about the cluster, in addition to any running topologies.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-131">This displays information about the cluster, in addition to any running topologies.</span></span>

![the storm ui][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="1bfe3-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-133">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="1bfe3-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-134">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="1bfe3-135">Microsoft is aware of this issue and is working on a solution.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-135">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="1bfe3-136">Main page</span><span class="sxs-lookup"><span data-stu-id="1bfe3-136">Main page</span></span>

<span data-ttu-id="1bfe3-137">The main page of the Storm UI provides the following information:</span><span class="sxs-lookup"><span data-stu-id="1bfe3-137">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="1bfe3-138">**Cluster summary**: Basic information about the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-138">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="1bfe3-139">**Topology summary**: A list of running topologies.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-139">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="1bfe3-140">Use the links in this section to view more information about specific topologies.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-140">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="1bfe3-141">**Supervisor summary**: Information about the Storm supervisor.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-141">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="1bfe3-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-142">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="1bfe3-143">Topology summary</span><span class="sxs-lookup"><span data-stu-id="1bfe3-143">Topology summary</span></span>

<span data-ttu-id="1bfe3-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span><span class="sxs-lookup"><span data-stu-id="1bfe3-144">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="1bfe3-145">**Topology summary**: Basic information about the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-145">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="1bfe3-146">**Topology actions**: Management actions that you can perform for the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-146">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="1bfe3-147">**Activate**: Resumes processing of a deactivated topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-147">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="1bfe3-148">**Deactivate**: Pauses a running topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-148">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="1bfe3-149">**Rebalance**: Adjusts the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-149">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="1bfe3-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-150">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="1bfe3-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-151">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="1bfe3-152">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-152">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="1bfe3-153">**Kill**: Terminates a Storm topology after the specified timeout.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-153">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="1bfe3-154">**Topology stats**: Statistics about the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-154">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="1bfe3-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-155">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="1bfe3-156">**Spouts**: The spouts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-156">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="1bfe3-157">Use the links in this section to view more information about specific spouts.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-157">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="1bfe3-158">**Bolts**: The bolts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-158">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="1bfe3-159">Use the links in this section to view more information about specific bolts.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-159">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="1bfe3-160">**Topology configuration**: The configuration of the selected topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-160">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="1bfe3-161">Spout and Bolt summary</span><span class="sxs-lookup"><span data-stu-id="1bfe3-161">Spout and Bolt summary</span></span>

<span data-ttu-id="1bfe3-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span><span class="sxs-lookup"><span data-stu-id="1bfe3-162">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="1bfe3-163">**Component summary**: Basic information about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-163">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="1bfe3-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-164">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="1bfe3-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-165">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="1bfe3-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-166">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="1bfe3-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-167">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="1bfe3-168">**Executors**: Information about the instances of the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-168">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="1bfe3-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-169">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="1bfe3-170">**Errors**: Any error information for this spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-170">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="1bfe3-171">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1bfe3-171">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="1bfe3-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-172">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="1bfe3-173">The following steps use a sample application.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-173">The following steps use a sample application.</span></span> <span data-ttu-id="1bfe3-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-174">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="1bfe3-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-175">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="1bfe3-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-176">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="1bfe3-177">Open Visual Studio, select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-177">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="1bfe3-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-178">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="1bfe3-179">From the list of templates, select **Storm Sample**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-179">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="1bfe3-180">At the bottom of the dialog box, type a name for the application.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-180">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/apache-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="1bfe3-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-182">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1bfe3-183">If prompted, enter the login credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-183">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="1bfe3-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-184">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="1bfe3-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-185">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="1bfe3-186">You can monitor whether the submission is successful by using the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-186">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="1bfe3-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-187">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="1bfe3-188">Select the topology from the list to view information about the running topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-188">Select the topology from the list to view information about the running topology.</span></span>

    ![visual studio monitor](./media/apache-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="1bfe3-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-190">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="1bfe3-191">Select the shape for the spouts or bolts to view information about these components.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-191">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="1bfe3-192">A new window opens for each item selected.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-192">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1bfe3-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-193">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="1bfe3-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-194">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="1bfe3-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-195">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="1bfe3-196">REST API</span><span class="sxs-lookup"><span data-stu-id="1bfe3-196">REST API</span></span>

<span data-ttu-id="1bfe3-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-197">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="1bfe3-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-198">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="1bfe3-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-199">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="1bfe3-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-200">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="1bfe3-201">Base URI</span><span class="sxs-lookup"><span data-stu-id="1bfe3-201">Base URI</span></span>

<span data-ttu-id="1bfe3-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-202">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="1bfe3-203">Authentication</span><span class="sxs-lookup"><span data-stu-id="1bfe3-203">Authentication</span></span>

<span data-ttu-id="1bfe3-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-204">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="1bfe3-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-205">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="1bfe3-206">Return values</span><span class="sxs-lookup"><span data-stu-id="1bfe3-206">Return values</span></span>

<span data-ttu-id="1bfe3-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-207">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="1bfe3-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span><span class="sxs-lookup"><span data-stu-id="1bfe3-208">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1bfe3-209">Next Steps</span><span class="sxs-lookup"><span data-stu-id="1bfe3-209">Next Steps</span></span>

<span data-ttu-id="1bfe3-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span><span class="sxs-lookup"><span data-stu-id="1bfe3-210">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="1bfe3-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="1bfe3-211">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](apache-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="1bfe3-212">Develop Java-based topologies using Maven</span><span class="sxs-lookup"><span data-stu-id="1bfe3-212">Develop Java-based topologies using Maven</span></span>](apache-storm-develop-java-topology.md)

<span data-ttu-id="1bfe3-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](apache-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="1bfe3-213">For a list of more example topologies, see [Example topologies for Storm on HDInsight](apache-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: ./media/apache-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/apache-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/apache-storm-deploy-monitor-topology/storm-ui-summary.png
