---
title: Storm-starter examples on Apache Storm on HDInsight - Azure
description: Learn how to do big data analytics and process data in real-time using Apache Storm and the storm-starter examples on HDInsight.
keywords: storm-starter, apache storm example
services: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 02/27/2018
ms.custom: H1Hack27Feb2017,hdinsightactive,hdiseo17may2017
ms.openlocfilehash: a800b3b44d060627bc8f75d8566507a9ad116f86
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864682"
---
# <a name="get-started-with-apache-storm-on-hdinsight-using-the-storm-starter-examples"></a><span data-ttu-id="046af-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span><span class="sxs-lookup"><span data-stu-id="046af-104">Get started with Apache Storm on HDInsight using the storm-starter examples</span></span>

<span data-ttu-id="046af-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span><span class="sxs-lookup"><span data-stu-id="046af-105">Learn how to use Apache Storm in HDInsight using the storm-starter examples.</span></span>

<span data-ttu-id="046af-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span><span class="sxs-lookup"><span data-stu-id="046af-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="046af-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span><span class="sxs-lookup"><span data-stu-id="046af-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="046af-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="046af-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="046af-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="046af-109">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="046af-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="046af-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="046af-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="046af-111">**An Azure subscription**.</span></span> <span data-ttu-id="046af-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="046af-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="046af-113">**Familiarity with SSH and SCP**.</span><span class="sxs-lookup"><span data-stu-id="046af-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="046af-114">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="046af-114">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="create-a-storm-cluster"></a><span data-ttu-id="046af-115">Create a Storm cluster</span><span class="sxs-lookup"><span data-stu-id="046af-115">Create a Storm cluster</span></span>

<span data-ttu-id="046af-116">Use the following steps to create a Storm on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="046af-116">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="046af-117">From the [Azure portal](https://portal.azure.com), select **+ Create a resource**, **Data + Analytics**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="046af-117">From the [Azure portal](https://portal.azure.com), select **+ Create a resource**, **Data + Analytics**, and then select **HDInsight**.</span></span>

    ![Create a HDInsight cluster](./media/apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="046af-119">From the **Basics** section, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="046af-119">From the **Basics** section, enter the following information:</span></span>

    * <span data-ttu-id="046af-120">**Cluster Name**: The name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-120">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="046af-121">**Subscription**: Select the subscription to use.</span><span class="sxs-lookup"><span data-stu-id="046af-121">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="046af-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="046af-122">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="046af-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span><span class="sxs-lookup"><span data-stu-id="046af-123">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="046af-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="046af-124">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="046af-125">By default the password is the same as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="046af-125">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="046af-126">**Resource Group**: The resource group to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="046af-126">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="046af-127">**Location**: The Azure region to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="046af-127">**Location**: The Azure region to create the cluster in.</span></span>

   ![Select subscription](./media/apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="046af-129">Select **Cluster type**, and then set the following values in the **Cluster configuration** section:</span><span class="sxs-lookup"><span data-stu-id="046af-129">Select **Cluster type**, and then set the following values in the **Cluster configuration** section:</span></span>

    * <span data-ttu-id="046af-130">**Cluster Type**: Storm</span><span class="sxs-lookup"><span data-stu-id="046af-130">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="046af-131">**Operating system**: Linux</span><span class="sxs-lookup"><span data-stu-id="046af-131">**Operating system**: Linux</span></span>

    * <span data-ttu-id="046af-132">**Version**: Storm 1.1.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="046af-132">**Version**: Storm 1.1.0 (HDI 3.6)</span></span>

   <span data-ttu-id="046af-133">Finally, use the **Select** button to save settings.</span><span class="sxs-lookup"><span data-stu-id="046af-133">Finally, use the **Select** button to save settings.</span></span>

    ![Select cluster type](./media/apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="046af-135">After selecting the cluster type, use the __Select__ button to set the cluster type.</span><span class="sxs-lookup"><span data-stu-id="046af-135">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="046af-136">Next, use the __Next__ button to finish basic configuration.</span><span class="sxs-lookup"><span data-stu-id="046af-136">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="046af-137">From the **Storage** section, select or create a Storage account.</span><span class="sxs-lookup"><span data-stu-id="046af-137">From the **Storage** section, select or create a Storage account.</span></span> <span data-ttu-id="046af-138">For the steps in this document, leave the other fields in this section at the default values.</span><span class="sxs-lookup"><span data-stu-id="046af-138">For the steps in this document, leave the other fields in this section at the default values.</span></span> <span data-ttu-id="046af-139">Use the __Next__ button to save storage configuration.</span><span class="sxs-lookup"><span data-stu-id="046af-139">Use the __Next__ button to save storage configuration.</span></span> <span data-ttu-id="046af-140">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="046af-140">For more information on using Data Lake Storage Gen2, see [Quickstart: Set up clusters in HDInsight](../../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md).</span></span>

    ![Set the storage account settings for HDInsight](./media/apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="046af-142">From the **Summary** section, review the configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-142">From the **Summary** section, review the configuration for the cluster.</span></span> <span data-ttu-id="046af-143">Use the __Edit__ links to change any settings that are incorrect.</span><span class="sxs-lookup"><span data-stu-id="046af-143">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="046af-144">Finally, use the __Create__ button to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-144">Finally, use the __Create__ button to create the cluster.</span></span>

    ![Cluster configuration summary](./media/apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="046af-146">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-146">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="046af-147">Run a storm-starter sample on HDInsight</span><span class="sxs-lookup"><span data-stu-id="046af-147">Run a storm-starter sample on HDInsight</span></span>

1. <span data-ttu-id="046af-148">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="046af-148">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!TIP]
    > <span data-ttu-id="046af-149">Your SSH client may say that the authenticity of the host can't be established.</span><span class="sxs-lookup"><span data-stu-id="046af-149">Your SSH client may say that the authenticity of the host can't be established.</span></span> <span data-ttu-id="046af-150">If so, enter `yes` to continue.</span><span class="sxs-lookup"><span data-stu-id="046af-150">If so, enter `yes` to continue.</span></span>

    > [!NOTE]
    > <span data-ttu-id="046af-151">If you used a password to secure your SSH user account, you are prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="046af-151">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="046af-152">If you used a public key, you may need to use the `-i` parameter to specify the matching private key.</span><span class="sxs-lookup"><span data-stu-id="046af-152">If you used a public key, you may need to use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="046af-153">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="046af-153">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="046af-154">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="046af-154">For information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="046af-155">Use the following command to start an example topology:</span><span class="sxs-lookup"><span data-stu-id="046af-155">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    <span data-ttu-id="046af-156">This command starts the example WordCount topology on the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-156">This command starts the example WordCount topology on the cluster.</span></span> <span data-ttu-id="046af-157">This topology generates random sentences and counts how many times words occur.</span><span class="sxs-lookup"><span data-stu-id="046af-157">This topology generates random sentences and counts how many times words occur.</span></span> <span data-ttu-id="046af-158">The friendly name of the topology is `wordcount`.</span><span class="sxs-lookup"><span data-stu-id="046af-158">The friendly name of the topology is `wordcount`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="046af-159">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span><span class="sxs-lookup"><span data-stu-id="046af-159">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="046af-160">Use the `scp` command to copy the file.</span><span class="sxs-lookup"><span data-stu-id="046af-160">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="046af-161">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="046af-161">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="046af-162">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="046af-162">The WordCount example, and other storm-starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="046af-163">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="046af-163">If you are interested in viewing the source for the storm-starter examples, you can find the code at [https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.1.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="046af-164">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="046af-164">This link is for Storm 1.1.x, which is provided with HDInsight 3.6.</span></span> <span data-ttu-id="046af-165">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span><span class="sxs-lookup"><span data-stu-id="046af-165">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="046af-166">Monitor the topology</span><span class="sxs-lookup"><span data-stu-id="046af-166">Monitor the topology</span></span>

<span data-ttu-id="046af-167">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-167">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="046af-168">Use the following steps to monitor the topology using the Storm UI:</span><span class="sxs-lookup"><span data-stu-id="046af-168">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="046af-169">To display the Storm UI, open a web browser to `https://CLUSTERNAME.azurehdinsight.net/stormui`.</span><span class="sxs-lookup"><span data-stu-id="046af-169">To display the Storm UI, open a web browser to `https://CLUSTERNAME.azurehdinsight.net/stormui`.</span></span> <span data-ttu-id="046af-170">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-170">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="046af-171">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-171">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="046af-172">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span><span class="sxs-lookup"><span data-stu-id="046af-172">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="046af-173">Information about the topology is displayed.</span><span class="sxs-lookup"><span data-stu-id="046af-173">Information about the topology is displayed.</span></span>

    ![Storm Dashboard with storm-starter WordCount topology information.](./media/apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="046af-175">This page provides the following information:</span><span class="sxs-lookup"><span data-stu-id="046af-175">This page provides the following information:</span></span>

    * <span data-ttu-id="046af-176">**Topology stats** - Basic information on the topology performance, organized into time windows.</span><span class="sxs-lookup"><span data-stu-id="046af-176">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="046af-177">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span><span class="sxs-lookup"><span data-stu-id="046af-177">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="046af-178">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span><span class="sxs-lookup"><span data-stu-id="046af-178">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="046af-179">**Bolts** - Basic information about bolts.</span><span class="sxs-lookup"><span data-stu-id="046af-179">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="046af-180">**Topology configuration** - Detailed information about the topology configuration.</span><span class="sxs-lookup"><span data-stu-id="046af-180">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="046af-181">This page also provides actions that can be taken on the topology:</span><span class="sxs-lookup"><span data-stu-id="046af-181">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="046af-182">**Activate** - Resumes processing of a deactivated topology.</span><span class="sxs-lookup"><span data-stu-id="046af-182">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="046af-183">**Deactivate** - Pauses a running topology.</span><span class="sxs-lookup"><span data-stu-id="046af-183">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="046af-184">**Rebalance** - Adjusts the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="046af-184">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="046af-185">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-185">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="046af-186">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="046af-186">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="046af-187">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="046af-187">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="046af-188">**Kill** - Terminates a Storm topology after the specified timeout.</span><span class="sxs-lookup"><span data-stu-id="046af-188">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="046af-189">From this page, select an entry from the **Spouts** or **Bolts** section.</span><span class="sxs-lookup"><span data-stu-id="046af-189">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="046af-190">Information about the selected component is displayed.</span><span class="sxs-lookup"><span data-stu-id="046af-190">Information about the selected component is displayed.</span></span>

    ![Storm Dashboard with information about selected components.](./media/apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="046af-192">This page displays the following information:</span><span class="sxs-lookup"><span data-stu-id="046af-192">This page displays the following information:</span></span>

    * <span data-ttu-id="046af-193">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span><span class="sxs-lookup"><span data-stu-id="046af-193">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="046af-194">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span><span class="sxs-lookup"><span data-stu-id="046af-194">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="046af-195">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span><span class="sxs-lookup"><span data-stu-id="046af-195">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="046af-196">**Output stats** - Information on data emitted by this bolt.</span><span class="sxs-lookup"><span data-stu-id="046af-196">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="046af-197">**Executors** - Information on instances of this component.</span><span class="sxs-lookup"><span data-stu-id="046af-197">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="046af-198">**Errors** - Errors produced by this component.</span><span class="sxs-lookup"><span data-stu-id="046af-198">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="046af-199">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span><span class="sxs-lookup"><span data-stu-id="046af-199">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="046af-200">In this example, the word **seven** has occurred 1493957 times.</span><span class="sxs-lookup"><span data-stu-id="046af-200">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="046af-201">This count is how many times the word has been encountered since this topology was started.</span><span class="sxs-lookup"><span data-stu-id="046af-201">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="046af-202">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="046af-202">Stop the topology</span></span>

<span data-ttu-id="046af-203">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span><span class="sxs-lookup"><span data-stu-id="046af-203">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="046af-204">When prompted, enter 10 for the seconds to wait before stopping the topology.</span><span class="sxs-lookup"><span data-stu-id="046af-204">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="046af-205">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="046af-205">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="046af-206">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="046af-206">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="046af-207">If you run into an issue with creating HDInsight cluster, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="046af-207">If you run into an issue with creating HDInsight cluster, see [access control requirements](../hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a id="next"></a><span data-ttu-id="046af-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="046af-208">Next steps</span></span>

<span data-ttu-id="046af-209">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="046af-209">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="046af-210">Next, learn how to [Develop Java-based topologies using Maven](apache-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="046af-210">Next, learn how to [Develop Java-based topologies using Maven](apache-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="046af-211">If you're already familiar with developing Java-based topologies, see the [Deploy and manage Apache Storm topologies on HDInsight](apache-storm-deploy-monitor-topology-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="046af-211">If you're already familiar with developing Java-based topologies, see the [Deploy and manage Apache Storm topologies on HDInsight](apache-storm-deploy-monitor-topology-linux.md) document.</span></span>

<span data-ttu-id="046af-212">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="046af-212">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="046af-213">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="046af-213">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](apache-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="046af-214">For example topologies that can be used with Storm on HDInsight, see the following examples:</span><span class="sxs-lookup"><span data-stu-id="046af-214">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="046af-215">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="046af-215">Example topologies for Storm on HDInsight</span></span>](apache-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[preview-portal]: https://portal.azure.com/
