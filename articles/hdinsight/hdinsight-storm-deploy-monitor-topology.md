---
title: Deploy and manage Apache Storm topologies on HDInsight | Microsoft Docs
description: Learn how to deploy, monitor and manage Apache Storm topologies using the Storm Dashboard on HDInsight. Use Hadoop tools for Visual Studio.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 0f3ae9d8e3b05b413645c202391861fbacad5714
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540711"
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a><span data-ttu-id="5a74e-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="5a74e-104">Deploy and manage Apache Storm topologies on Windows-based HDInsight</span></span>

<span data-ttu-id="5a74e-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span><span class="sxs-lookup"><span data-stu-id="5a74e-105">The Storm Dashboard allows you to easily deploy and run Apache Storm topologies to your HDInsight cluster by using your web browser.</span></span> <span data-ttu-id="5a74e-106">You can also use the dashboard to monitor and manage running topologies.</span><span class="sxs-lookup"><span data-stu-id="5a74e-106">You can also use the dashboard to monitor and manage running topologies.</span></span> <span data-ttu-id="5a74e-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a74e-107">If you use Visual Studio, the HDInsight Tools for Visual Studio provide similar features in Visual Studio.</span></span>

<span data-ttu-id="5a74e-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span><span class="sxs-lookup"><span data-stu-id="5a74e-108">The Storm Dashboard and the Storm features in the HDInsight Tools rely on the Storm REST API, which can be used to create your own monitoring and management solutions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a74e-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span><span class="sxs-lookup"><span data-stu-id="5a74e-109">The steps in this document require a Storm on HDInsight cluster that uses Windows as the operating system.</span></span> <span data-ttu-id="5a74e-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="5a74e-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5a74e-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="5a74e-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>
>
> <span data-ttu-id="5a74e-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="5a74e-112">For information on deploying and managing Storm topologies with an HDInsight cluster that uses Linux, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a74e-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5a74e-113">Prerequisites</span></span>

* <span data-ttu-id="5a74e-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-114">**Apache Storm on HDInsight** - see [Get started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps on creating a cluster.</span></span>

* <span data-ttu-id="5a74e-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span><span class="sxs-lookup"><span data-stu-id="5a74e-115">For the **Storm Dashboard**: A modern web browser that supports HTML5.</span></span>

* <span data-ttu-id="5a74e-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a74e-116">For **Visual Studio** - Azure SDK 2.5.1 or newer and the HDInsight Tools for Visual Studio.</span></span> <span data-ttu-id="5a74e-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5a74e-117">See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

    <span data-ttu-id="5a74e-118">One of the following versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5a74e-118">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="5a74e-119">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="5a74e-119">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>

  * <span data-ttu-id="5a74e-120">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="5a74e-120">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="5a74e-121">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="5a74e-121">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="5a74e-122">Visual Studio 2015 (any edition)</span><span class="sxs-lookup"><span data-stu-id="5a74e-122">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="5a74e-123">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="5a74e-123">Visual Studio 2017 (any edition)</span></span>

## <a name="storm-dashboard"></a><span data-ttu-id="5a74e-124">Storm Dashboard</span><span class="sxs-lookup"><span data-stu-id="5a74e-124">Storm Dashboard</span></span>

<span data-ttu-id="5a74e-125">The Storm Dashboard is a web page available on your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-125">The Storm Dashboard is a web page available on your Storm cluster.</span></span> <span data-ttu-id="5a74e-126">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-126">The URL is **https://&lt;clustername>.azurehdinsight.net/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

<span data-ttu-id="5a74e-127">From the top of the Storm Dashboard, select **Submit Topology**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-127">From the top of the Storm Dashboard, select **Submit Topology**.</span></span> <span data-ttu-id="5a74e-128">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span><span class="sxs-lookup"><span data-stu-id="5a74e-128">Follow the instructions on the page to run a sample topology or to upload and run a topology that you created.</span></span>

![the submit topology page][storm-dashboard-submit]

### <a name="storm-ui"></a><span data-ttu-id="5a74e-130">Storm UI</span><span class="sxs-lookup"><span data-stu-id="5a74e-130">Storm UI</span></span>

<span data-ttu-id="5a74e-131">From the Storm Dashboard, select the **Storm UI** link.</span><span class="sxs-lookup"><span data-stu-id="5a74e-131">From the Storm Dashboard, select the **Storm UI** link.</span></span> <span data-ttu-id="5a74e-132">This displays information about the cluster, in addition to any running topologies.</span><span class="sxs-lookup"><span data-stu-id="5a74e-132">This displays information about the cluster, in addition to any running topologies.</span></span>

![the storm ui][storm-dashboard-ui]

> [!NOTE]
> <span data-ttu-id="5a74e-134">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span><span class="sxs-lookup"><span data-stu-id="5a74e-134">With some versions of Internet Explorer, you may discover that the Storm UI does not refresh after you have first visited it.</span></span> <span data-ttu-id="5a74e-135">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span><span class="sxs-lookup"><span data-stu-id="5a74e-135">For example, it may not show the new topologies you submitted, or it may show a topology as active when you previously deactivated it.</span></span> <span data-ttu-id="5a74e-136">Microsoft is aware of this issue and is working on a solution.</span><span class="sxs-lookup"><span data-stu-id="5a74e-136">Microsoft is aware of this issue and is working on a solution.</span></span>

#### <a name="main-page"></a><span data-ttu-id="5a74e-137">Main page</span><span class="sxs-lookup"><span data-stu-id="5a74e-137">Main page</span></span>

<span data-ttu-id="5a74e-138">The main page of the Storm UI provides the following information:</span><span class="sxs-lookup"><span data-stu-id="5a74e-138">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="5a74e-139">**Cluster summary**: Basic information about the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-139">**Cluster summary**: Basic information about the Storm cluster.</span></span>

* <span data-ttu-id="5a74e-140">**Topology summary**: A list of running topologies.</span><span class="sxs-lookup"><span data-stu-id="5a74e-140">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="5a74e-141">Use the links in this section to view more information about specific topologies.</span><span class="sxs-lookup"><span data-stu-id="5a74e-141">Use the links in this section to view more information about specific topologies.</span></span>

* <span data-ttu-id="5a74e-142">**Supervisor summary**: Information about the Storm supervisor.</span><span class="sxs-lookup"><span data-stu-id="5a74e-142">**Supervisor summary**: Information about the Storm supervisor.</span></span>

* <span data-ttu-id="5a74e-143">**Nimbus configuration**: Nimbus configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-143">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

#### <a name="topology-summary"></a><span data-ttu-id="5a74e-144">Topology summary</span><span class="sxs-lookup"><span data-stu-id="5a74e-144">Topology summary</span></span>

<span data-ttu-id="5a74e-145">Selecting a link from the **Topology summary** section displays the following information about the topology:</span><span class="sxs-lookup"><span data-stu-id="5a74e-145">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="5a74e-146">**Topology summary**: Basic information about the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-146">**Topology summary**: Basic information about the topology.</span></span>

* <span data-ttu-id="5a74e-147">**Topology actions**: Management actions that you can perform for the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-147">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="5a74e-148">**Activate**: Resumes processing of a deactivated topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-148">**Activate**: Resumes processing of a deactivated topology.</span></span>

  * <span data-ttu-id="5a74e-149">**Deactivate**: Pauses a running topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-149">**Deactivate**: Pauses a running topology.</span></span>

  * <span data-ttu-id="5a74e-150">**Rebalance**: Adjusts the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-150">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="5a74e-151">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-151">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="5a74e-152">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-152">This allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

      <span data-ttu-id="5a74e-153">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="5a74e-153">For more information, see [Understanding the parallelism of a Storm topology (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

  * <span data-ttu-id="5a74e-154">**Kill**: Terminates a Storm topology after the specified timeout.</span><span class="sxs-lookup"><span data-stu-id="5a74e-154">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>

* <span data-ttu-id="5a74e-155">**Topology stats**: Statistics about the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-155">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="5a74e-156">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span><span class="sxs-lookup"><span data-stu-id="5a74e-156">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="5a74e-157">**Spouts**: The spouts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-157">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="5a74e-158">Use the links in this section to view more information about specific spouts.</span><span class="sxs-lookup"><span data-stu-id="5a74e-158">Use the links in this section to view more information about specific spouts.</span></span>

* <span data-ttu-id="5a74e-159">**Bolts**: The bolts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-159">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="5a74e-160">Use the links in this section to view more information about specific bolts.</span><span class="sxs-lookup"><span data-stu-id="5a74e-160">Use the links in this section to view more information about specific bolts.</span></span>

* <span data-ttu-id="5a74e-161">**Topology configuration**: The configuration of the selected topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-161">**Topology configuration**: The configuration of the selected topology.</span></span>

#### <a name="spout-and-bolt-summary"></a><span data-ttu-id="5a74e-162">Spout and Bolt summary</span><span class="sxs-lookup"><span data-stu-id="5a74e-162">Spout and Bolt summary</span></span>

<span data-ttu-id="5a74e-163">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span><span class="sxs-lookup"><span data-stu-id="5a74e-163">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="5a74e-164">**Component summary**: Basic information about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-164">**Component summary**: Basic information about the spout or bolt.</span></span>

* <span data-ttu-id="5a74e-165">**Spout/Bolt stats**: Statistics about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-165">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="5a74e-166">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span><span class="sxs-lookup"><span data-stu-id="5a74e-166">Use the links in the **Window** column to set the timeframe for the remaining entries on the page.</span></span>

* <span data-ttu-id="5a74e-167">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-167">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>

* <span data-ttu-id="5a74e-168">**Output stats**: Information about the streams emitted by this spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-168">**Output stats**: Information about the streams emitted by this spout or bolt.</span></span>

* <span data-ttu-id="5a74e-169">**Executors**: Information about the instances of the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-169">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="5a74e-170">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span><span class="sxs-lookup"><span data-stu-id="5a74e-170">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>

* <span data-ttu-id="5a74e-171">**Errors**: Any error information for this spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="5a74e-171">**Errors**: Any error information for this spout or bolt.</span></span>

## <a name="hdinsight-tools-for-visual-studio"></a><span data-ttu-id="5a74e-172">HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a74e-172">HDInsight Tools for Visual Studio</span></span>

<span data-ttu-id="5a74e-173">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-173">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="5a74e-174">The following steps use a sample application.</span><span class="sxs-lookup"><span data-stu-id="5a74e-174">The following steps use a sample application.</span></span> <span data-ttu-id="5a74e-175">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5a74e-175">For information about creating your own topologies by using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="5a74e-176">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-176">Use the following steps to deploy a sample to your Storm on HDInsight cluster, then view and manage the topology.</span></span>

1. <span data-ttu-id="5a74e-177">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5a74e-177">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="5a74e-178">Open Visual Studio, select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-178">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="5a74e-179">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-179">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="5a74e-180">From the list of templates, select **Storm Sample**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-180">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="5a74e-181">At the bottom of the dialog box, type a name for the application.</span><span class="sxs-lookup"><span data-stu-id="5a74e-181">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. <span data-ttu-id="5a74e-183">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-183">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5a74e-184">If prompted, enter the login credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="5a74e-184">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="5a74e-185">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-185">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="5a74e-186">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-186">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="5a74e-187">You can monitor whether the submission is successful by using the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="5a74e-187">You can monitor whether the submission is successful by using the **Output** window.</span></span>

6. <span data-ttu-id="5a74e-188">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span><span class="sxs-lookup"><span data-stu-id="5a74e-188">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="5a74e-189">Select the topology from the list to view information about the running topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-189">Select the topology from the list to view information about the running topology.</span></span>

    ![visual studio monitor](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > <span data-ttu-id="5a74e-191">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="5a74e-191">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

    <span data-ttu-id="5a74e-192">Select the shape for the spouts or bolts to view information about these components.</span><span class="sxs-lookup"><span data-stu-id="5a74e-192">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="5a74e-193">A new window opens for each item selected.</span><span class="sxs-lookup"><span data-stu-id="5a74e-193">A new window opens for each item selected.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5a74e-194">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span><span class="sxs-lookup"><span data-stu-id="5a74e-194">The name of the topology is the class name of the topology (in this case, `HelloWord`,) with a timestamp appended.</span></span>

7. <span data-ttu-id="5a74e-195">From the **Topology Summary** view, select **Kill** to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="5a74e-195">From the **Topology Summary** view, select **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5a74e-196">Storm topologies continue running until they are stopped or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="5a74e-196">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span>


## <a name="rest-api"></a><span data-ttu-id="5a74e-197">REST API</span><span class="sxs-lookup"><span data-stu-id="5a74e-197">REST API</span></span>

<span data-ttu-id="5a74e-198">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span><span class="sxs-lookup"><span data-stu-id="5a74e-198">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="5a74e-199">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="5a74e-199">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="5a74e-200">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span><span class="sxs-lookup"><span data-stu-id="5a74e-200">For more information, see [Storm UI REST API](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md).</span></span> <span data-ttu-id="5a74e-201">The following information is specific to using the REST API with Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5a74e-201">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

### <a name="base-uri"></a><span data-ttu-id="5a74e-202">Base URI</span><span class="sxs-lookup"><span data-stu-id="5a74e-202">Base URI</span></span>

<span data-ttu-id="5a74e-203">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-203">The base URI for the REST API on HDInsight clusters is **https://&lt;clustername>.azurehdinsight.net/stormui/api/v1/**, where **clustername** is the name of your Storm on HDInsight cluster.</span></span>

### <a name="authentication"></a><span data-ttu-id="5a74e-204">Authentication</span><span class="sxs-lookup"><span data-stu-id="5a74e-204">Authentication</span></span>

<span data-ttu-id="5a74e-205">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span><span class="sxs-lookup"><span data-stu-id="5a74e-205">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="5a74e-206">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-206">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="5a74e-207">Return values</span><span class="sxs-lookup"><span data-stu-id="5a74e-207">Return values</span></span>

<span data-ttu-id="5a74e-208">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span><span class="sxs-lookup"><span data-stu-id="5a74e-208">Information that is returned from the REST API may only be usable from within the cluster or virtual machines on the same Azure Virtual Network as the cluster.</span></span> <span data-ttu-id="5a74e-209">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span><span class="sxs-lookup"><span data-stu-id="5a74e-209">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers are not be accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a74e-210">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5a74e-210">Next Steps</span></span>

<span data-ttu-id="5a74e-211">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span><span class="sxs-lookup"><span data-stu-id="5a74e-211">Now that you've learned how to deploy and monitor topologies by using the Storm Dashboard, learn how to:</span></span>

* [<span data-ttu-id="5a74e-212">Develop C# topologies using the HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5a74e-212">Develop C# topologies using the HDInsight Tools for Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [<span data-ttu-id="5a74e-213">Develop Java-based topologies using Maven</span><span class="sxs-lookup"><span data-stu-id="5a74e-213">Develop Java-based topologies using Maven</span></span>](hdinsight-storm-develop-java-topology.md)

<span data-ttu-id="5a74e-214">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="5a74e-214">For a list of more example topologies, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>

[hdinsight-dashboard]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png





