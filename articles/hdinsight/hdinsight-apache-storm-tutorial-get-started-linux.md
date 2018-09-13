---
title: Get started with Apache Storm on Azure HDInsight | Microsoft Docs
description: Get started with big data analytics using Apache Storm and the Storm Starter samples on Linux-based HDInsight. Learn how to use Storm to process data real-time.
keywords: apache storm,apache storm tutorial,big data analytics,storm starter
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: d710dcac-35d1-4c27-a8d6-acaf8146b485
ms.service: hdinsight
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 5af25b5c31784953f392a6016be5a3a77c15208d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554219"
---
#<a name="get-started-with-the-storm-starter-samples-for-big-data-analytics-on-linux-based-hdinsight"></a><span data-ttu-id="dc06a-105">Get started with the Storm Starter samples for big data analytics on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc06a-105">Get started with the Storm Starter samples for big data analytics on Linux-based HDInsight</span></span>

<span data-ttu-id="dc06a-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span><span class="sxs-lookup"><span data-stu-id="dc06a-106">Apache Storm is a scalable, fault-tolerant, distributed, real-time computation system for processing streams of data.</span></span> <span data-ttu-id="dc06a-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span><span class="sxs-lookup"><span data-stu-id="dc06a-107">With Storm on Azure HDInsight, you can create a cloud-based Storm cluster that performs big data analytics in real time.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc06a-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="dc06a-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dc06a-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="dc06a-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc06a-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="dc06a-110">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="dc06a-111">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="dc06a-111">**An Azure subscription**.</span></span> <span data-ttu-id="dc06a-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="dc06a-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="dc06a-113">**Familiarity with SSH and SCP**.</span><span class="sxs-lookup"><span data-stu-id="dc06a-113">**Familiarity with SSH and SCP**.</span></span> <span data-ttu-id="dc06a-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dc06a-114">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

### <a name="access-control-requirements"></a><span data-ttu-id="dc06a-115">Access control requirements</span><span class="sxs-lookup"><span data-stu-id="dc06a-115">Access control requirements</span></span>

[!INCLUDE [access-control](../../includes/hdinsight-access-control-requirements.md)]

## <a name="create-a-storm-cluster"></a><span data-ttu-id="dc06a-116">Create a Storm cluster</span><span class="sxs-lookup"><span data-stu-id="dc06a-116">Create a Storm cluster</span></span>

<span data-ttu-id="dc06a-117">Use the following steps to create a Storm on HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="dc06a-117">Use the following steps to create a Storm on HDInsight cluster:</span></span>

1. <span data-ttu-id="dc06a-118">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dc06a-118">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>

    ![Create a HDInsight cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/create-hdinsight.png)

2. <span data-ttu-id="dc06a-120">From the **Basics** blade, enter the following information:</span><span class="sxs-lookup"><span data-stu-id="dc06a-120">From the **Basics** blade, enter the following information:</span></span>

    * <span data-ttu-id="dc06a-121">**Cluster Name**: The name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-121">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="dc06a-122">**Subscription**: Select the subscription to use.</span><span class="sxs-lookup"><span data-stu-id="dc06a-122">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="dc06a-123">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dc06a-123">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="dc06a-124">You use these credentials to access services such as the Ambari Web UI or REST API.</span><span class="sxs-lookup"><span data-stu-id="dc06a-124">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="dc06a-125">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span><span class="sxs-lookup"><span data-stu-id="dc06a-125">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="dc06a-126">By default the password is the same as the cluster login password.</span><span class="sxs-lookup"><span data-stu-id="dc06a-126">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="dc06a-127">**Resource Group**: The resource group to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="dc06a-127">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="dc06a-128">**Location**: The Azure region to create the cluster in.</span><span class="sxs-lookup"><span data-stu-id="dc06a-128">**Location**: The Azure region to create the cluster in.</span></span>

    ![Select subscription](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-basic-configuration.png)

3. <span data-ttu-id="dc06a-130">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span><span class="sxs-lookup"><span data-stu-id="dc06a-130">Select **Cluster type**, and then set the following values on the **Cluster configuration** blade:</span></span>

    * <span data-ttu-id="dc06a-131">**Cluster Type**: Storm</span><span class="sxs-lookup"><span data-stu-id="dc06a-131">**Cluster Type**: Storm</span></span>

    * <span data-ttu-id="dc06a-132">**Operating system**: Linux</span><span class="sxs-lookup"><span data-stu-id="dc06a-132">**Operating system**: Linux</span></span>

    * <span data-ttu-id="dc06a-133">**Version**: Storm 1.0.1 (HDI 3.5)</span><span class="sxs-lookup"><span data-stu-id="dc06a-133">**Version**: Storm 1.0.1 (HDI 3.5)</span></span>

    * <span data-ttu-id="dc06a-134">**Cluster Tier**: Standard</span><span class="sxs-lookup"><span data-stu-id="dc06a-134">**Cluster Tier**: Standard</span></span>

    <span data-ttu-id="dc06a-135">Finally, use the **Select** button to save settings.</span><span class="sxs-lookup"><span data-stu-id="dc06a-135">Finally, use the **Select** button to save settings.</span></span>

    ![Select cluster type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="dc06a-137">After selecting the cluster type, use the __Select__ button to set the cluster type.</span><span class="sxs-lookup"><span data-stu-id="dc06a-137">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="dc06a-138">Next, use the __Next__ button to finish basic configuration.</span><span class="sxs-lookup"><span data-stu-id="dc06a-138">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="dc06a-139">From the **Storage** blade, select or create a Storage account.</span><span class="sxs-lookup"><span data-stu-id="dc06a-139">From the **Storage** blade, select or create a Storage account.</span></span> <span data-ttu-id="dc06a-140">For the steps in this document, leave the other fields on this blade at the default values.</span><span class="sxs-lookup"><span data-stu-id="dc06a-140">For the steps in this document, leave the other fields on this blade at the default values.</span></span> <span data-ttu-id="dc06a-141">Use the __Next__ button to save storage configuration.</span><span class="sxs-lookup"><span data-stu-id="dc06a-141">Use the __Next__ button to save storage configuration.</span></span>

    ![Set the storage account settings for HDInsight](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/set-hdinsight-storage-account.png)

6. <span data-ttu-id="dc06a-143">From the **Summary** blade, review the configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-143">From the **Summary** blade, review the configuration for the cluster.</span></span> <span data-ttu-id="dc06a-144">Use the __Edit__ links to change any settings that are incorrect.</span><span class="sxs-lookup"><span data-stu-id="dc06a-144">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="dc06a-145">Finally, use the__Create__ button to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-145">Finally, use the__Create__ button to create the cluster.</span></span>

    ![Cluster configuration summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/hdinsight-configuration-summary.png)

    > [!NOTE]
    > <span data-ttu-id="dc06a-147">It can take up to 20 minutes to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-147">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="run-a-storm-starter-sample-on-hdinsight"></a><span data-ttu-id="dc06a-148">Run a Storm Starter sample on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc06a-148">Run a Storm Starter sample on HDInsight</span></span>

1. <span data-ttu-id="dc06a-149">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="dc06a-149">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="dc06a-150">If you used a password to secure your SSH user account, you are prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="dc06a-150">If you used a password to secure your SSH user account, you are prompted to enter it.</span></span> <span data-ttu-id="dc06a-151">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span><span class="sxs-lookup"><span data-stu-id="dc06a-151">If you used a public key, you may need use the `-i` parameter to specify the matching private key.</span></span> <span data-ttu-id="dc06a-152">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="dc06a-152">For example, `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

    <span data-ttu-id="dc06a-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="dc06a-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="dc06a-154">Use the following command to start an example topology:</span><span class="sxs-lookup"><span data-stu-id="dc06a-154">Use the following command to start an example topology:</span></span>

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology wordcount

    > [!NOTE]
    > <span data-ttu-id="dc06a-155">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span><span class="sxs-lookup"><span data-stu-id="dc06a-155">On previous versions of HDInsight, the class name of the topology is `storm.starter.WordCountTopology` instead of `org.apache.storm.starter.WordCountTopology`.</span></span>

    <span data-ttu-id="dc06a-156">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span><span class="sxs-lookup"><span data-stu-id="dc06a-156">This command starts the example WordCount topology on the cluster, with a friendly name of 'wordcount'.</span></span> <span data-ttu-id="dc06a-157">It randomly generates sentences and count the occurrence of each word in the sentences.</span><span class="sxs-lookup"><span data-stu-id="dc06a-157">It randomly generates sentences and count the occurrence of each word in the sentences.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc06a-158">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span><span class="sxs-lookup"><span data-stu-id="dc06a-158">When submitting your own topologies to the cluster, you must first copy the jar file containing the cluster before using the `storm` command.</span></span> <span data-ttu-id="dc06a-159">Use the `scp` command to copy the file.</span><span class="sxs-lookup"><span data-stu-id="dc06a-159">Use the `scp` command to copy the file.</span></span> <span data-ttu-id="dc06a-160">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span><span class="sxs-lookup"><span data-stu-id="dc06a-160">For example, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`</span></span>
    >
    > <span data-ttu-id="dc06a-161">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span><span class="sxs-lookup"><span data-stu-id="dc06a-161">The WordCount example, and other storm starter examples, are already included on your cluster at `/usr/hdp/current/storm-client/contrib/storm-starter/`.</span></span>

<span data-ttu-id="dc06a-162">If you are interested in viewing the source for the storm starter examples, you can find the code at [https://github.com/apache/storm/tree/1.0.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.0.x-branch/examples/storm-starter).</span><span class="sxs-lookup"><span data-stu-id="dc06a-162">If you are interested in viewing the source for the storm starter examples, you can find the code at [https://github.com/apache/storm/tree/1.0.x-branch/examples/storm-starter](https://github.com/apache/storm/tree/1.0.x-branch/examples/storm-starter).</span></span> <span data-ttu-id="dc06a-163">This link is for Storm 1.0.x, which is provided with HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="dc06a-163">This link is for Storm 1.0.x, which is provided with HDInsight 3.5.</span></span> <span data-ttu-id="dc06a-164">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span><span class="sxs-lookup"><span data-stu-id="dc06a-164">For other versions of Storm, use the __Branch__ button at the top of the page to select a different Storm version.</span></span>

## <a name="monitor-the-topology"></a><span data-ttu-id="dc06a-165">Monitor the topology</span><span class="sxs-lookup"><span data-stu-id="dc06a-165">Monitor the topology</span></span>

<span data-ttu-id="dc06a-166">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-166">The Storm UI provides a web interface for working with running topologies, and is included on your HDInsight cluster.</span></span>

<span data-ttu-id="dc06a-167">Use the following steps to monitor the topology using the Storm UI:</span><span class="sxs-lookup"><span data-stu-id="dc06a-167">Use the following steps to monitor the topology using the Storm UI:</span></span>

1. <span data-ttu-id="dc06a-168">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="dc06a-168">To display the Storm UI, open a web browser to https://CLUSTERNAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="dc06a-169">Replace **CLUSTERNAME** with the name of your cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-169">Replace **CLUSTERNAME** with the name of your cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="dc06a-170">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-170">If asked to provide a user name and password, enter the cluster administrator (admin) and password that you used when creating the cluster.</span></span>

2. <span data-ttu-id="dc06a-171">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span><span class="sxs-lookup"><span data-stu-id="dc06a-171">Under **Topology summary**, select the **wordcount** entry in the **Name** column.</span></span> <span data-ttu-id="dc06a-172">Information about the topology is displayed.</span><span class="sxs-lookup"><span data-stu-id="dc06a-172">Information about the topology is displayed.</span></span>

    ![Storm Dashboard with Storm Starter WordCount topology information.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/topology-summary.png)

    <span data-ttu-id="dc06a-174">This page provides the following information:</span><span class="sxs-lookup"><span data-stu-id="dc06a-174">This page provides the following information:</span></span>

    * <span data-ttu-id="dc06a-175">**Topology stats** - Basic information on the topology performance, organized into time windows.</span><span class="sxs-lookup"><span data-stu-id="dc06a-175">**Topology stats** - Basic information on the topology performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dc06a-176">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span><span class="sxs-lookup"><span data-stu-id="dc06a-176">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="dc06a-177">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span><span class="sxs-lookup"><span data-stu-id="dc06a-177">**Spouts** - Basic information about spouts, including the last error returned by each spout.</span></span>

    * <span data-ttu-id="dc06a-178">**Bolts** - Basic information about bolts.</span><span class="sxs-lookup"><span data-stu-id="dc06a-178">**Bolts** - Basic information about bolts.</span></span>

    * <span data-ttu-id="dc06a-179">**Topology configuration** - Detailed information about the topology configuration.</span><span class="sxs-lookup"><span data-stu-id="dc06a-179">**Topology configuration** - Detailed information about the topology configuration.</span></span>

    <span data-ttu-id="dc06a-180">This page also provides actions that can be taken on the topology:</span><span class="sxs-lookup"><span data-stu-id="dc06a-180">This page also provides actions that can be taken on the topology:</span></span>

    * <span data-ttu-id="dc06a-181">**Activate** - Resumes processing of a deactivated topology.</span><span class="sxs-lookup"><span data-stu-id="dc06a-181">**Activate** - Resumes processing of a deactivated topology.</span></span>

    * <span data-ttu-id="dc06a-182">**Deactivate** - Pauses a running topology.</span><span class="sxs-lookup"><span data-stu-id="dc06a-182">**Deactivate** - Pauses a running topology.</span></span>

    * <span data-ttu-id="dc06a-183">**Rebalance** - Adjusts the parallelism of the topology.</span><span class="sxs-lookup"><span data-stu-id="dc06a-183">**Rebalance** - Adjusts the parallelism of the topology.</span></span> <span data-ttu-id="dc06a-184">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-184">You should rebalance running topologies after you have changed the number of nodes in the cluster.</span></span> <span data-ttu-id="dc06a-185">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="dc06a-185">Rebalancing adjusts parallelism to compensate for the increased/decreased number of nodes in the cluster.</span></span> <span data-ttu-id="dc06a-186">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span><span class="sxs-lookup"><span data-stu-id="dc06a-186">For more information, see [Understanding the parallelism of a Storm topology](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).</span></span>

    * <span data-ttu-id="dc06a-187">**Kill** - Terminates a Storm topology after the specified timeout.</span><span class="sxs-lookup"><span data-stu-id="dc06a-187">**Kill** - Terminates a Storm topology after the specified timeout.</span></span>

3. <span data-ttu-id="dc06a-188">From this page, select an entry from the **Spouts** or **Bolts** section.</span><span class="sxs-lookup"><span data-stu-id="dc06a-188">From this page, select an entry from the **Spouts** or **Bolts** section.</span></span> <span data-ttu-id="dc06a-189">Information about the selected component is displayed.</span><span class="sxs-lookup"><span data-stu-id="dc06a-189">Information about the selected component is displayed.</span></span>

    ![Storm Dashboard with information about selected components.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-apache-storm-tutorial-get-started-linux/component-summary.png)

    <span data-ttu-id="dc06a-191">This page displays the following information:</span><span class="sxs-lookup"><span data-stu-id="dc06a-191">This page displays the following information:</span></span>

    * <span data-ttu-id="dc06a-192">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span><span class="sxs-lookup"><span data-stu-id="dc06a-192">**Spout/Bolt stats** - Basic information on the component performance, organized into time windows.</span></span>

        > [!NOTE]
        > <span data-ttu-id="dc06a-193">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span><span class="sxs-lookup"><span data-stu-id="dc06a-193">Selecting a specific time window changes the time window for information displayed in other sections of the page.</span></span>

    * <span data-ttu-id="dc06a-194">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span><span class="sxs-lookup"><span data-stu-id="dc06a-194">**Input stats** (bolt only) - Information on components that produce data consumed by the bolt.</span></span>

    * <span data-ttu-id="dc06a-195">**Output stats** - Information on data emitted by this bolt.</span><span class="sxs-lookup"><span data-stu-id="dc06a-195">**Output stats** - Information on data emitted by this bolt.</span></span>

    * <span data-ttu-id="dc06a-196">**Executors** - Information on instances of this component.</span><span class="sxs-lookup"><span data-stu-id="dc06a-196">**Executors** - Information on instances of this component.</span></span>

    * <span data-ttu-id="dc06a-197">**Errors** - Errors produced by this component.</span><span class="sxs-lookup"><span data-stu-id="dc06a-197">**Errors** - Errors produced by this component.</span></span>

4. <span data-ttu-id="dc06a-198">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span><span class="sxs-lookup"><span data-stu-id="dc06a-198">When viewing the details of a spout or bolt, select an entry from the **Port** column in the **Executors** section to view details for a specific instance of the component.</span></span>

        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["with"]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: split default ["nature"]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [snow]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [snow, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [white]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [white, 747293]
        2015-01-27 14:18:02 b.s.d.executor [INFO] Processing received message source: split:21, stream: default, id: {}, [seven]
        2015-01-27 14:18:02 b.s.d.task [INFO] Emitting: count default [seven, 1493957]

    <span data-ttu-id="dc06a-199">In this example, the word **seven** has occurred 1493957 times.</span><span class="sxs-lookup"><span data-stu-id="dc06a-199">In this example, the word **seven** has occurred 1493957 times.</span></span> <span data-ttu-id="dc06a-200">This count is how many times the word has been encountered since this topology was started.</span><span class="sxs-lookup"><span data-stu-id="dc06a-200">This count is how many times the word has been encountered since this topology was started.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="dc06a-201">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="dc06a-201">Stop the topology</span></span>

<span data-ttu-id="dc06a-202">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span><span class="sxs-lookup"><span data-stu-id="dc06a-202">Return to the **Topology summary** page for the word-count topology, and then select the **Kill** button from the **Topology actions** section.</span></span> <span data-ttu-id="dc06a-203">When prompted, enter 10 for the seconds to wait before stopping the topology.</span><span class="sxs-lookup"><span data-stu-id="dc06a-203">When prompted, enter 10 for the seconds to wait before stopping the topology.</span></span> <span data-ttu-id="dc06a-204">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="dc06a-204">After the timeout period, the topology no longer appears when you visit the **Storm UI** section of the dashboard.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="dc06a-205">Delete the cluster</span><span class="sxs-lookup"><span data-stu-id="dc06a-205">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a id="next"></a><span data-ttu-id="dc06a-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="dc06a-206">Next steps</span></span>

<span data-ttu-id="dc06a-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc06a-207">In this Apache Storm tutorial, you learned the basics of working with Storm on HDInsight.</span></span> <span data-ttu-id="dc06a-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="dc06a-208">Next, learn how to [Develop Java-based topologies using Maven](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="dc06a-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dc06a-209">If you're already familiar with developing Java-based topologies and want to deploy an existing topology to HDInsight, see [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md).</span></span>

<span data-ttu-id="dc06a-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="dc06a-210">If you are a .NET developer, you can create C# or hybrid C#/Java topologies using Visual Studio.</span></span> <span data-ttu-id="dc06a-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="dc06a-211">For more information, see [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

<span data-ttu-id="dc06a-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span><span class="sxs-lookup"><span data-stu-id="dc06a-212">For example topologies that can be used with Storm on HDInsight, see the following examples:</span></span>

* [<span data-ttu-id="dc06a-213">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc06a-213">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

[apachestorm]: https://storm.incubator.apache.org
[stormdocs]: http://storm.incubator.apache.org/documentation/Documentation.html
[stormstarter]: https://github.com/apache/storm/tree/master/examples/storm-starter
[stormjavadocs]: https://storm.incubator.apache.org/apidocs/
[azureportal]: https://manage.windowsazure.com/
[hdinsight-provision]: hdinsight-provision-clusters.md
[preview-portal]: https://portal.azure.com/







