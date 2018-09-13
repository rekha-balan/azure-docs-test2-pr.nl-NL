---
title: Deploy and manage Apache Storm topologies on Azure HDInsight
description: Learn how to deploy, monitor and manage Apache Storm topologies using the Storm Dashboard on Linux-based HDInsight. Use Hadoop tools for Visual Studio.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/22/2018
ms.openlocfilehash: 486fcdfecf70b13d01c259f36b74676fb8e4d54f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870025"
---
# <a name="deploy-and-manage-apache-storm-topologies-on-azure-hdinsight"></a><span data-ttu-id="c3148-104">Deploy and manage Apache Storm topologies on Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="c3148-104">Deploy and manage Apache Storm topologies on Azure HDInsight</span></span> 

<span data-ttu-id="c3148-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="c3148-105">In this document, learn the basics of managing and monitoring Storm topologies running on Storm on HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3148-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-106">The steps in this article require a Linux-based Storm on HDInsight cluster.</span></span> <span data-ttu-id="c3148-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="c3148-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c3148-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c3148-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 
>
> <span data-ttu-id="c3148-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](apache-storm-deploy-monitor-topology.md)</span><span class="sxs-lookup"><span data-stu-id="c3148-109">For information on deploying and monitoring topologies on Windows-based HDInsight, see [Deploy and manage Apache Storm topologies on Windows-based HDInsight](apache-storm-deploy-monitor-topology.md)</span></span>


## <a name="prerequisites"></a><span data-ttu-id="c3148-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c3148-110">Prerequisites</span></span>

* <span data-ttu-id="c3148-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span><span class="sxs-lookup"><span data-stu-id="c3148-111">**A Linux-based Storm on HDInsight cluster**: see [Get started with Apache Storm on HDInsight](apache-storm-tutorial-get-started-linux.md) for steps on creating a cluster</span></span>

* <span data-ttu-id="c3148-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-112">(Optional) **Familiarity with SSH and SCP**: For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="c3148-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3148-113">(Optional) **Visual Studio**: Azure SDK 2.5.1 or newer and the Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="c3148-114">For more information, see [Get started using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-114">For more information, see [Get started using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

    <span data-ttu-id="c3148-115">One of the following versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="c3148-115">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="c3148-116">Visual Studio 2012 with Update 4</span><span class="sxs-lookup"><span data-stu-id="c3148-116">Visual Studio 2012 with Update 4</span></span>

  * <span data-ttu-id="c3148-117">Visual Studio 2013 with Update 4 or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="c3148-117">Visual Studio 2013 with Update 4 or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * [<span data-ttu-id="c3148-118">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="c3148-118">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/)

  * <span data-ttu-id="c3148-119">Visual Studio 2015 (any edition)</span><span class="sxs-lookup"><span data-stu-id="c3148-119">Visual Studio 2015 (any edition)</span></span>

  * <span data-ttu-id="c3148-120">Visual Studio 2017 (any edition).</span><span class="sxs-lookup"><span data-stu-id="c3148-120">Visual Studio 2017 (any edition).</span></span> <span data-ttu-id="c3148-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span><span class="sxs-lookup"><span data-stu-id="c3148-121">Data Lake Tools for Visual Studio 2017 are installed as part of the Azure Workload.</span></span>

## <a name="submit-a-topology-visual-studio"></a><span data-ttu-id="c3148-122">Submit a topology: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3148-122">Submit a topology: Visual Studio</span></span>

<span data-ttu-id="c3148-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-123">The HDInsight Tools can be used to submit C# or hybrid topologies to your Storm cluster.</span></span> <span data-ttu-id="c3148-124">The following steps use a sample application.</span><span class="sxs-lookup"><span data-stu-id="c3148-124">The following steps use a sample application.</span></span> <span data-ttu-id="c3148-125">For information about creating on using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-125">For information about creating on using the HDInsight Tools, see [Develop C# topologies using the HDInsight Tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span></span>

1. <span data-ttu-id="c3148-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-126">If you have not already installed the latest version of the Data Lake tools for Visual Studio, see [Get started using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="c3148-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c3148-127">The Data Lake Tools for Visual Studio were formerly called the HDInsight Tools for Visual Studio.</span></span>
    >
    > <span data-ttu-id="c3148-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="c3148-128">Data Lake Tools for Visual Studio are included in the __Azure Workload__ for Visual Studio 2017.</span></span>

2. <span data-ttu-id="c3148-129">Open Visual Studio, select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="c3148-129">Open Visual Studio, select **File** > **New** > **Project**.</span></span>

3. <span data-ttu-id="c3148-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c3148-130">In the **New Project** dialog box, expand **Installed** > **Templates**, and then select **HDInsight**.</span></span> <span data-ttu-id="c3148-131">From the list of templates, select **Storm Sample**.</span><span class="sxs-lookup"><span data-stu-id="c3148-131">From the list of templates, select **Storm Sample**.</span></span> <span data-ttu-id="c3148-132">At the bottom of the dialog box, type a name for the application.</span><span class="sxs-lookup"><span data-stu-id="c3148-132">At the bottom of the dialog box, type a name for the application.</span></span>

    ![image](./media/apache-storm-deploy-monitor-topology-linux/sample.png)

4. <span data-ttu-id="c3148-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="c3148-134">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3148-135">If prompted, enter the login credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c3148-135">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="c3148-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-136">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

5. <span data-ttu-id="c3148-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="c3148-137">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="c3148-138">You can monitor whether the submission is successful by using the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="c3148-138">You can monitor whether the submission is successful by using the **Output** window.</span></span>

## <a name="submit-a-topology-ssh-and-the-storm-command"></a><span data-ttu-id="c3148-139">Submit a topology: SSH and the Storm command</span><span class="sxs-lookup"><span data-stu-id="c3148-139">Submit a topology: SSH and the Storm command</span></span>

1. <span data-ttu-id="c3148-140">Use SSH to connect to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-140">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="c3148-141">Replace **USERNAME** the name of your SSH login.</span><span class="sxs-lookup"><span data-stu-id="c3148-141">Replace **USERNAME** the name of your SSH login.</span></span> <span data-ttu-id="c3148-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span><span class="sxs-lookup"><span data-stu-id="c3148-142">Replace **CLUSTERNAME** with your HDInsight cluster name:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="c3148-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-143">For more information on using SSH to connect to your HDInsight cluster, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c3148-144">Use the following command to start an example topology:</span><span class="sxs-lookup"><span data-stu-id="c3148-144">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    <span data-ttu-id="c3148-145">This command starts the example WordCount topology on the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-145">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="c3148-146">This topology randomly generates sentences, and then counts the occurrence of each word in the sentences.</span><span class="sxs-lookup"><span data-stu-id="c3148-146">This topology randomly generates sentences, and then counts the occurrence of each word in the sentences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="c3148-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span><span class="sxs-lookup"><span data-stu-id="c3148-147">When submitting topology to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="c3148-148">To copy the file to the cluster, you can use the `scp` command.</span><span class="sxs-lookup"><span data-stu-id="c3148-148">To copy the file to the cluster, you can use the `scp` command.</span></span> <span data-ttu-id="c3148-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="c3148-149">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
   >
   > <span data-ttu-id="c3148-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="c3148-150">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

## <a name="submit-a-topology-programmatically"></a><span data-ttu-id="c3148-151">Submit a topology: programmatically</span><span class="sxs-lookup"><span data-stu-id="c3148-151">Submit a topology: programmatically</span></span>

<span data-ttu-id="c3148-152">You can programmatically deploy a topology using the Nimbus service.</span><span class="sxs-lookup"><span data-stu-id="c3148-152">You can programmatically deploy a topology using the Nimbus service.</span></span> <span data-ttu-id="c3148-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span><span class="sxs-lookup"><span data-stu-id="c3148-153">[https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) provides an example Java application that demonstrates how to deploy and start a topology through the Nimbus service.</span></span>

## <a name="monitor-and-manage-visual-studio"></a><span data-ttu-id="c3148-154">Monitor and manage: Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3148-154">Monitor and manage: Visual Studio</span></span>

<span data-ttu-id="c3148-155">When a topology is submitted using Visual Studio, the **Storm Topologies** view appears.</span><span class="sxs-lookup"><span data-stu-id="c3148-155">When a topology is submitted using Visual Studio, the **Storm Topologies** view appears.</span></span> <span data-ttu-id="c3148-156">Select the topology from the list to view information about the running topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-156">Select the topology from the list to view information about the running topology.</span></span>

![visual studio monitor](./media/apache-storm-deploy-monitor-topology-linux/vsmonitor.png)

> [!NOTE]
> <span data-ttu-id="c3148-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="c3148-158">You can also view **Storm Topologies** from **Server Explorer** by expanding **Azure** > **HDInsight**, and then right-clicking a Storm on HDInsight cluster, and selecting **View Storm Topologies**.</span></span>

<span data-ttu-id="c3148-159">Select the shape for the spouts or bolts to view information about these components.</span><span class="sxs-lookup"><span data-stu-id="c3148-159">Select the shape for the spouts or bolts to view information about these components.</span></span> <span data-ttu-id="c3148-160">A new window opens for each item selected.</span><span class="sxs-lookup"><span data-stu-id="c3148-160">A new window opens for each item selected.</span></span>

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="c3148-161">Deactivate and reactivate</span><span class="sxs-lookup"><span data-stu-id="c3148-161">Deactivate and reactivate</span></span>

<span data-ttu-id="c3148-162">Deactivating a topology pauses it until it is killed or reactivated.</span><span class="sxs-lookup"><span data-stu-id="c3148-162">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="c3148-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="c3148-163">To perform these operations, use the __Deactivate__ and __Reactivate__ buttons at the top of the __Topology Summary__.</span></span>

### <a name="rebalance"></a><span data-ttu-id="c3148-164">Rebalance</span><span class="sxs-lookup"><span data-stu-id="c3148-164">Rebalance</span></span>

<span data-ttu-id="c3148-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-165">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="c3148-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span><span class="sxs-lookup"><span data-stu-id="c3148-166">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

<span data-ttu-id="c3148-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="c3148-167">To rebalance a topology, use the __Rebalance__ button at the top of the __Topology Summary__.</span></span>

> [!WARNING]
> <span data-ttu-id="c3148-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span><span class="sxs-lookup"><span data-stu-id="c3148-168">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="c3148-169">So if the topology was active, it becomes active again.</span><span class="sxs-lookup"><span data-stu-id="c3148-169">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="c3148-170">If it was deactivated, it remains deactivated.</span><span class="sxs-lookup"><span data-stu-id="c3148-170">If it was deactivated, it remains deactivated.</span></span>

### <a name="kill-a-topology"></a><span data-ttu-id="c3148-171">Kill a topology</span><span class="sxs-lookup"><span data-stu-id="c3148-171">Kill a topology</span></span>

<span data-ttu-id="c3148-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="c3148-172">Storm topologies continue running until they are stopped or the cluster is deleted.</span></span> <span data-ttu-id="c3148-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span><span class="sxs-lookup"><span data-stu-id="c3148-173">To stop a topology, use the __Kill__ button at the top of the __Topology Summary__.</span></span>

## <a name="monitor-and-manage-ssh-and-the-storm-command"></a><span data-ttu-id="c3148-174">Monitor and manage: SSH and the Storm command</span><span class="sxs-lookup"><span data-stu-id="c3148-174">Monitor and manage: SSH and the Storm command</span></span>

<span data-ttu-id="c3148-175">The `storm` utility allows you to work with running topologies from the command line.</span><span class="sxs-lookup"><span data-stu-id="c3148-175">The `storm` utility allows you to work with running topologies from the command line.</span></span> <span data-ttu-id="c3148-176">Use `storm -h` for a full list of commands.</span><span class="sxs-lookup"><span data-stu-id="c3148-176">Use `storm -h` for a full list of commands.</span></span>

### <a name="list-topologies"></a><span data-ttu-id="c3148-177">List topologies</span><span class="sxs-lookup"><span data-stu-id="c3148-177">List topologies</span></span>

<span data-ttu-id="c3148-178">Use the following command to list all running topologies:</span><span class="sxs-lookup"><span data-stu-id="c3148-178">Use the following command to list all running topologies:</span></span>

    storm list

<span data-ttu-id="c3148-179">This command returns information similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="c3148-179">This command returns information similar to the following text:</span></span>

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a><span data-ttu-id="c3148-180">Deactivate and reactivate</span><span class="sxs-lookup"><span data-stu-id="c3148-180">Deactivate and reactivate</span></span>

<span data-ttu-id="c3148-181">Deactivating a topology pauses it until it is killed or reactivated.</span><span class="sxs-lookup"><span data-stu-id="c3148-181">Deactivating a topology pauses it until it is killed or reactivated.</span></span> <span data-ttu-id="c3148-182">Use the following command to deactivate and reactivate:</span><span class="sxs-lookup"><span data-stu-id="c3148-182">Use the following command to deactivate and reactivate:</span></span>

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a><span data-ttu-id="c3148-183">Kill a running topology</span><span class="sxs-lookup"><span data-stu-id="c3148-183">Kill a running topology</span></span>

<span data-ttu-id="c3148-184">Storm topologies, once started, continue running until stopped.</span><span class="sxs-lookup"><span data-stu-id="c3148-184">Storm topologies, once started, continue running until stopped.</span></span> <span data-ttu-id="c3148-185">To stop a topology, use the following command:</span><span class="sxs-lookup"><span data-stu-id="c3148-185">To stop a topology, use the following command:</span></span>

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a><span data-ttu-id="c3148-186">Rebalance</span><span class="sxs-lookup"><span data-stu-id="c3148-186">Rebalance</span></span>

<span data-ttu-id="c3148-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-187">Rebalancing a topology allows the system to revise the parallelism of the topology.</span></span> <span data-ttu-id="c3148-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span><span class="sxs-lookup"><span data-stu-id="c3148-188">For example, if you have resized the cluster to add more notes, rebalancing allows a topology to see the new nodes.</span></span>

> [!WARNING]
> <span data-ttu-id="c3148-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span><span class="sxs-lookup"><span data-stu-id="c3148-189">Rebalancing a topology first deactivates the topology, then redistributes workers evenly across the cluster, then finally returns the topology to the state it was in before rebalancing occurred.</span></span> <span data-ttu-id="c3148-190">So if the topology was active, it becomes active again.</span><span class="sxs-lookup"><span data-stu-id="c3148-190">So if the topology was active, it becomes active again.</span></span> <span data-ttu-id="c3148-191">If it was deactivated, it remains deactivated.</span><span class="sxs-lookup"><span data-stu-id="c3148-191">If it was deactivated, it remains deactivated.</span></span>

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a><span data-ttu-id="c3148-192">Monitor and manage: Storm UI</span><span class="sxs-lookup"><span data-stu-id="c3148-192">Monitor and manage: Storm UI</span></span>

<span data-ttu-id="c3148-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-193">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span> <span data-ttu-id="c3148-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-194">To view the Storm UI, use a web browser to open **https://CLUSTERNAME.azurehdinsight.net/stormui**, where **CLUSTERNAME** is the name of your cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c3148-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-195">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

### <a name="main-page"></a><span data-ttu-id="c3148-196">Main page</span><span class="sxs-lookup"><span data-stu-id="c3148-196">Main page</span></span>

<span data-ttu-id="c3148-197">The main page of the Storm UI provides the following information:</span><span class="sxs-lookup"><span data-stu-id="c3148-197">The main page of the Storm UI provides the following information:</span></span>

* <span data-ttu-id="c3148-198">**Cluster summary**: Basic information about the Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-198">**Cluster summary**: Basic information about the Storm cluster.</span></span>
* <span data-ttu-id="c3148-199">**Topology summary**: A list of running topologies.</span><span class="sxs-lookup"><span data-stu-id="c3148-199">**Topology summary**: A list of running topologies.</span></span> <span data-ttu-id="c3148-200">Use the links in this section to view more information about specific topologies.</span><span class="sxs-lookup"><span data-stu-id="c3148-200">Use the links in this section to view more information about specific topologies.</span></span>
* <span data-ttu-id="c3148-201">**Supervisor summary**: Information about the Storm supervisor.</span><span class="sxs-lookup"><span data-stu-id="c3148-201">**Supervisor summary**: Information about the Storm supervisor.</span></span>
* <span data-ttu-id="c3148-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-202">**Nimbus configuration**: Nimbus configuration for the cluster.</span></span>

### <a name="topology-summary"></a><span data-ttu-id="c3148-203">Topology summary</span><span class="sxs-lookup"><span data-stu-id="c3148-203">Topology summary</span></span>

<span data-ttu-id="c3148-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span><span class="sxs-lookup"><span data-stu-id="c3148-204">Selecting a link from the **Topology summary** section displays the following information about the topology:</span></span>

* <span data-ttu-id="c3148-205">**Topology summary**: Basic information about the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-205">**Topology summary**: Basic information about the topology.</span></span>
* <span data-ttu-id="c3148-206">**Topology actions**: Management actions that you can perform for the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-206">**Topology actions**: Management actions that you can perform for the topology.</span></span>

  * <span data-ttu-id="c3148-207">**Activate**: Resumes processing of a deactivated topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-207">**Activate**: Resumes processing of a deactivated topology.</span></span>
  * <span data-ttu-id="c3148-208">**Deactivate**: Pauses a running topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-208">**Deactivate**: Pauses a running topology.</span></span>
  * <span data-ttu-id="c3148-209">**Rebalance**: Adjusts the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-209">**Rebalance**: Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="c3148-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-210">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="c3148-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-211">This operation allows the topology to adjust parallelism to compensate for the increased or decreased number of nodes in the cluster.</span></span>

    <span data-ttu-id="c3148-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span><span class="sxs-lookup"><span data-stu-id="c3148-212">For more information, see <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Understanding the parallelism of a Storm topology</a>.</span></span>
  * <span data-ttu-id="c3148-213">**Kill**: Terminates a Storm topology after the specified timeout.</span><span class="sxs-lookup"><span data-stu-id="c3148-213">**Kill**: Terminates a Storm topology after the specified timeout.</span></span>
* <span data-ttu-id="c3148-214">**Topology stats**: Statistics about the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-214">**Topology stats**: Statistics about the topology.</span></span> <span data-ttu-id="c3148-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span><span class="sxs-lookup"><span data-stu-id="c3148-215">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="c3148-216">**Spouts**: The spouts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-216">**Spouts**: The spouts used by the topology.</span></span> <span data-ttu-id="c3148-217">Use the links in this section to view more information about specific spouts.</span><span class="sxs-lookup"><span data-stu-id="c3148-217">Use the links in this section to view more information about specific spouts.</span></span>
* <span data-ttu-id="c3148-218">**Bolts**: The bolts used by the topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-218">**Bolts**: The bolts used by the topology.</span></span> <span data-ttu-id="c3148-219">Use the links in this section to view more information about specific bolts.</span><span class="sxs-lookup"><span data-stu-id="c3148-219">Use the links in this section to view more information about specific bolts.</span></span>
* <span data-ttu-id="c3148-220">**Topology configuration**: The configuration of the selected topology.</span><span class="sxs-lookup"><span data-stu-id="c3148-220">**Topology configuration**: The configuration of the selected topology.</span></span>

### <a name="spout-and-bolt-summary"></a><span data-ttu-id="c3148-221">Spout and Bolt summary</span><span class="sxs-lookup"><span data-stu-id="c3148-221">Spout and Bolt summary</span></span>

<span data-ttu-id="c3148-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span><span class="sxs-lookup"><span data-stu-id="c3148-222">Selecting a spout from the **Spouts** or **Bolts** sections displays the following information about the selected item:</span></span>

* <span data-ttu-id="c3148-223">**Component summary**: Basic information about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-223">**Component summary**: Basic information about the spout or bolt.</span></span>
* <span data-ttu-id="c3148-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-224">**Spout/Bolt stats**: Statistics about the spout or bolt.</span></span> <span data-ttu-id="c3148-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span><span class="sxs-lookup"><span data-stu-id="c3148-225">To set the timeframe for the remaining entries on the page, use the links in the **Window** column.</span></span>
* <span data-ttu-id="c3148-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-226">**Input stats** (bolt only): Information about the input streams consumed by the bolt.</span></span>
* <span data-ttu-id="c3148-227">**Output stats**: Information about the streams emitted by the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-227">**Output stats**: Information about the streams emitted by the spout or bolt.</span></span>
* <span data-ttu-id="c3148-228">**Executors**: Information about the instances of the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-228">**Executors**: Information about the instances of the spout or bolt.</span></span> <span data-ttu-id="c3148-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span><span class="sxs-lookup"><span data-stu-id="c3148-229">Select the **Port** entry for a specific executor to view a log of diagnostic information produced for this instance.</span></span>
* <span data-ttu-id="c3148-230">**Errors**: Any error information for the spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="c3148-230">**Errors**: Any error information for the spout or bolt.</span></span>

## <a name="monitor-and-manage-rest-api"></a><span data-ttu-id="c3148-231">Monitor and manage: REST API</span><span class="sxs-lookup"><span data-stu-id="c3148-231">Monitor and manage: REST API</span></span>

<span data-ttu-id="c3148-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span><span class="sxs-lookup"><span data-stu-id="c3148-232">The Storm UI is built on top of the REST API, so you can perform similar management and monitoring functionality by using the REST API.</span></span> <span data-ttu-id="c3148-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span><span class="sxs-lookup"><span data-stu-id="c3148-233">You can use the REST API to create custom tools for managing and monitoring Storm topologies.</span></span>

<span data-ttu-id="c3148-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/current/STORM-UI-REST-API.html).</span><span class="sxs-lookup"><span data-stu-id="c3148-234">For more information, see [Storm UI REST API](http://storm.apache.org/releases/current/STORM-UI-REST-API.html).</span></span> <span data-ttu-id="c3148-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c3148-235">The following information is specific to using the REST API with Apache Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3148-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span><span class="sxs-lookup"><span data-stu-id="c3148-236">The Storm REST API is not publicly available over the internet, and must be accessed using an SSH tunnel to the HDInsight cluster head node.</span></span> <span data-ttu-id="c3148-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](../hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-237">For information on creating and using an SSH tunnel, see [Use SSH Tunneling to access Ambari web UI, ResourceManager, JobHistory, NameNode, Oozie, and other web UIs](../hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

### <a name="base-uri"></a><span data-ttu-id="c3148-238">Base URI</span><span class="sxs-lookup"><span data-stu-id="c3148-238">Base URI</span></span>

<span data-ttu-id="c3148-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span><span class="sxs-lookup"><span data-stu-id="c3148-239">The base URI for the REST API on Linux-based HDInsight clusters is available on the head node at **https://HEADNODEFQDN:8744/api/v1/**.</span></span> <span data-ttu-id="c3148-240">The domain name of the head node is generated during cluster creation and is not static.</span><span class="sxs-lookup"><span data-stu-id="c3148-240">The domain name of the head node is generated during cluster creation and is not static.</span></span>

<span data-ttu-id="c3148-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span><span class="sxs-lookup"><span data-stu-id="c3148-241">You can find the fully qualified domain name (FQDN) for the cluster head node in several different ways:</span></span>

* <span data-ttu-id="c3148-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-242">**From an SSH session**: Use the command `headnode -f` from an SSH session to the cluster.</span></span>
* <span data-ttu-id="c3148-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span><span class="sxs-lookup"><span data-stu-id="c3148-243">**From Ambari Web**: Select **Services** from the top of the page, then select **Storm**.</span></span> <span data-ttu-id="c3148-244">From the **Summary** tab, select **Storm UI Server**.</span><span class="sxs-lookup"><span data-stu-id="c3148-244">From the **Summary** tab, select **Storm UI Server**.</span></span> <span data-ttu-id="c3148-245">The FQDN of the node that hosts the Storm UI and REST API is displayed at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="c3148-245">The FQDN of the node that hosts the Storm UI and REST API is displayed at the top of the page.</span></span>
* <span data-ttu-id="c3148-246">**From Ambari REST API**: Use the command `curl -u admin -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span><span class="sxs-lookup"><span data-stu-id="c3148-246">**From Ambari REST API**: Use the command `curl -u admin -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` to retrieve information about the node that the Storm UI and REST API are running on.</span></span> <span data-ttu-id="c3148-247">Replace **CLUSTERNAME** with the cluster name.</span><span class="sxs-lookup"><span data-stu-id="c3148-247">Replace **CLUSTERNAME** with the cluster name.</span></span> <span data-ttu-id="c3148-248">When prompted, enter the password for the login (admin) account.</span><span class="sxs-lookup"><span data-stu-id="c3148-248">When prompted, enter the password for the login (admin) account.</span></span> <span data-ttu-id="c3148-249">In the response, the "host_name" entry contains the FQDN of the node.</span><span class="sxs-lookup"><span data-stu-id="c3148-249">In the response, the "host_name" entry contains the FQDN of the node.</span></span>

### <a name="authentication"></a><span data-ttu-id="c3148-250">Authentication</span><span class="sxs-lookup"><span data-stu-id="c3148-250">Authentication</span></span>

<span data-ttu-id="c3148-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span><span class="sxs-lookup"><span data-stu-id="c3148-251">Requests to the REST API must use **basic authentication**, so you use the HDInsight cluster administrator name and password.</span></span>

> [!NOTE]
> <span data-ttu-id="c3148-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-252">Because basic authentication is sent by using clear text, you should **always** use HTTPS to secure communications with the cluster.</span></span>

### <a name="return-values"></a><span data-ttu-id="c3148-253">Return values</span><span class="sxs-lookup"><span data-stu-id="c3148-253">Return values</span></span>

<span data-ttu-id="c3148-254">Information that is returned from the REST API may only be usable from within the cluster.</span><span class="sxs-lookup"><span data-stu-id="c3148-254">Information that is returned from the REST API may only be usable from within the cluster.</span></span> <span data-ttu-id="c3148-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not accessible from the Internet.</span><span class="sxs-lookup"><span data-stu-id="c3148-255">For example, the fully qualified domain name (FQDN) returned for Zookeeper servers is not accessible from the Internet.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3148-256">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c3148-256">Next Steps</span></span>

<span data-ttu-id="c3148-257">Learn how to [Develop Java-based topologies using Maven](apache-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-257">Learn how to [Develop Java-based topologies using Maven](apache-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="c3148-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](apache-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="c3148-258">For a list of more example topologies, see [Example topologies for Storm on HDInsight](apache-storm-example-topology.md).</span></span>
