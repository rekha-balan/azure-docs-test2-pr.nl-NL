---
title: Install and use Giraph on Linux-based HDInsight (Hadoop) | Microsoft Docs
description: Learn how to install Giraph on Linux-based HDInsight clusters using Script Actions. Script Actions allow you to customize the cluster during creation, by changing cluster configuration or installing services and utilities.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/08/2017
ms.author: larryfr
ms.openlocfilehash: 1cd56fe50970dd77a7dcb2586adbcc035bc30291
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552922"
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="f133d-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span><span class="sxs-lookup"><span data-stu-id="f133d-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="f133d-105">You can install Giraph on any type of cluster in Hadoop on Azure HDInsight by using **Script Action** to customize a cluster.</span><span class="sxs-lookup"><span data-stu-id="f133d-105">You can install Giraph on any type of cluster in Hadoop on Azure HDInsight by using **Script Action** to customize a cluster.</span></span>

<span data-ttu-id="f133d-106">In this topic, you learn how to install Giraph by using Script Action.</span><span class="sxs-lookup"><span data-stu-id="f133d-106">In this topic, you learn how to install Giraph by using Script Action.</span></span> <span data-ttu-id="f133d-107">Once you have installed Giraph, you'll also learn how to use Giraph for most typical applications, which is to process large-scale graphs.</span><span class="sxs-lookup"><span data-stu-id="f133d-107">Once you have installed Giraph, you'll also learn how to use Giraph for most typical applications, which is to process large-scale graphs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f133d-108">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="f133d-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="f133d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="f133d-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f133d-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="f133d-110">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="whatis"></a><span data-ttu-id="f133d-111">What is Giraph?</span><span class="sxs-lookup"><span data-stu-id="f133d-111">What is Giraph?</span></span>

<span data-ttu-id="f133d-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f133d-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="f133d-113">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span><span class="sxs-lookup"><span data-stu-id="f133d-113">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="f133d-114">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span><span class="sxs-lookup"><span data-stu-id="f133d-114">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="f133d-115">Identifying potential friends based on your current relationships.</span><span class="sxs-lookup"><span data-stu-id="f133d-115">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="f133d-116">Identifying the shortest route between two computers in a network.</span><span class="sxs-lookup"><span data-stu-id="f133d-116">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="f133d-117">Calculating the page rank of webpages.</span><span class="sxs-lookup"><span data-stu-id="f133d-117">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="f133d-118">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span><span class="sxs-lookup"><span data-stu-id="f133d-118">Components provided with the HDInsight cluster are fully supported and Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="f133d-119">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="f133d-119">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="f133d-120">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span><span class="sxs-lookup"><span data-stu-id="f133d-120">This might result in resolving the issue OR asking you to engage available channels for the open source technologies where deep expertise for that technology is found.</span></span> <span data-ttu-id="f133d-121">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="f133d-121">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="f133d-122">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="f133d-122">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="f133d-123">What the script does</span><span class="sxs-lookup"><span data-stu-id="f133d-123">What the script does</span></span>

<span data-ttu-id="f133d-124">This script performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="f133d-124">This script performs the following actions:</span></span>

* <span data-ttu-id="f133d-125">Installs Giraph to `/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="f133d-125">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="f133d-126">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="f133d-126">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <a name="install"></a><span data-ttu-id="f133d-127">Install Giraph using Script Actions</span><span class="sxs-lookup"><span data-stu-id="f133d-127">Install Giraph using Script Actions</span></span>

<span data-ttu-id="f133d-128">A sample script to install Giraph on an HDInsight cluster is available at the following location.</span><span class="sxs-lookup"><span data-stu-id="f133d-128">A sample script to install Giraph on an HDInsight cluster is available at the following location.</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="f133d-129">This section provides instructions on how to use the sample script while creating the cluster by using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="f133d-129">This section provides instructions on how to use the sample script while creating the cluster by using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="f133d-130">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span><span class="sxs-lookup"><span data-stu-id="f133d-130">Azure PowerShell, the Azure CLI, the HDInsight .NET SDK, or Azure Resource Manager templates can also be used to apply script actions.</span></span> <span data-ttu-id="f133d-131">You can also apply script actions to already running clusters.</span><span class="sxs-lookup"><span data-stu-id="f133d-131">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="f133d-132">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f133d-132">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="f133d-133">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span><span class="sxs-lookup"><span data-stu-id="f133d-133">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="f133d-134">On the **Optional Configuration** blade, select **Script Actions**, and provide the information below:</span><span class="sxs-lookup"><span data-stu-id="f133d-134">On the **Optional Configuration** blade, select **Script Actions**, and provide the information below:</span></span>

   * <span data-ttu-id="f133d-135">**NAME**: Enter a friendly name for the script action.</span><span class="sxs-lookup"><span data-stu-id="f133d-135">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="f133d-136">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="f133d-136">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="f133d-137">**HEAD**: Check this option</span><span class="sxs-lookup"><span data-stu-id="f133d-137">**HEAD**: Check this option</span></span>

   * <span data-ttu-id="f133d-138">**WORKER**: Leave this unchecked</span><span class="sxs-lookup"><span data-stu-id="f133d-138">**WORKER**: Leave this unchecked</span></span>

   * <span data-ttu-id="f133d-139">**ZOOKEEPER**: Leave this unchecked</span><span class="sxs-lookup"><span data-stu-id="f133d-139">**ZOOKEEPER**: Leave this unchecked</span></span>

   * <span data-ttu-id="f133d-140">**PARAMETERS**: Leave this field blank</span><span class="sxs-lookup"><span data-stu-id="f133d-140">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="f133d-141">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="f133d-141">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="f133d-142">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span><span class="sxs-lookup"><span data-stu-id="f133d-142">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="f133d-143">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f133d-143">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <a name="usegiraph"></a><span data-ttu-id="f133d-144">How do I use Giraph in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="f133d-144">How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="f133d-145">Once the cluster has finished creating, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span><span class="sxs-lookup"><span data-stu-id="f133d-145">Once the cluster has finished creating, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="f133d-146">This uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span><span class="sxs-lookup"><span data-stu-id="f133d-146">This uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="f133d-147">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="f133d-147">Connect to the HDInsight cluster using SSH:</span></span>

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    <span data-ttu-id="f133d-148">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f133d-148">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="f133d-149">Use the following to create a new file named **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="f133d-149">Use the following to create a new file named **tiny_graph.txt**:</span></span>

    ```
    nano tiny_graph.txt
    ```

    <span data-ttu-id="f133d-150">Use the following as the contents of this file:</span><span class="sxs-lookup"><span data-stu-id="f133d-150">Use the following as the contents of this file:</span></span>

    ```
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="f133d-151">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="f133d-151">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="f133d-152">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span><span class="sxs-lookup"><span data-stu-id="f133d-152">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="f133d-153">The `edge_value` (or weight) can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="f133d-153">The `edge_value` (or weight) can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="f133d-154">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span><span class="sxs-lookup"><span data-stu-id="f133d-154">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="f133d-156">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span><span class="sxs-lookup"><span data-stu-id="f133d-156">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="f133d-157">Use the following to store the data into primary storage for your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="f133d-157">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="f133d-158">Run the SimpleShortestPathsComputation example using the following command.</span><span class="sxs-lookup"><span data-stu-id="f133d-158">Run the SimpleShortestPathsComputation example using the following command.</span></span>

    ```
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="f133d-159">The parameters used with this command are described in the following table.</span><span class="sxs-lookup"><span data-stu-id="f133d-159">The parameters used with this command are described in the following table.</span></span>

   | <span data-ttu-id="f133d-160">Parameter</span><span class="sxs-lookup"><span data-stu-id="f133d-160">Parameter</span></span> | <span data-ttu-id="f133d-161">What it does</span><span class="sxs-lookup"><span data-stu-id="f133d-161">What it does</span></span> |
   | --- | --- |
   | `jar /usr/hdp/current/giraph/giraph-examples.jar` |<span data-ttu-id="f133d-162">The jar file containing the examples.</span><span class="sxs-lookup"><span data-stu-id="f133d-162">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="f133d-163">The class used to start the examples.</span><span class="sxs-lookup"><span data-stu-id="f133d-163">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="f133d-164">The example that is used.</span><span class="sxs-lookup"><span data-stu-id="f133d-164">The example that is used.</span></span> <span data-ttu-id="f133d-165">In this case, it computes the shortest path between ID 1 and all other IDs in the graph.</span><span class="sxs-lookup"><span data-stu-id="f133d-165">In this case, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker=headnodehost:9010` |<span data-ttu-id="f133d-166">The headnode for the cluster.</span><span class="sxs-lookup"><span data-stu-id="f133d-166">The headnode for the cluster.</span></span> |
   | `-vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFromat` |<span data-ttu-id="f133d-167">The input format to use for the input data.</span><span class="sxs-lookup"><span data-stu-id="f133d-167">The input format to use for the input data.</span></span> |
   | `-vip /example/data/tiny_graph.txt` |<span data-ttu-id="f133d-168">The input data file.</span><span class="sxs-lookup"><span data-stu-id="f133d-168">The input data file.</span></span> |
   | `-vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat` |<span data-ttu-id="f133d-169">The output format.</span><span class="sxs-lookup"><span data-stu-id="f133d-169">The output format.</span></span> <span data-ttu-id="f133d-170">In this case, ID and value as plain text.</span><span class="sxs-lookup"><span data-stu-id="f133d-170">In this case, ID and value as plain text.</span></span> |
   | `-op /example/output/shortestpaths` |<span data-ttu-id="f133d-171">The output location.</span><span class="sxs-lookup"><span data-stu-id="f133d-171">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="f133d-172">The number of workers to use.</span><span class="sxs-lookup"><span data-stu-id="f133d-172">The number of workers to use.</span></span> <span data-ttu-id="f133d-173">In this case, 2.</span><span class="sxs-lookup"><span data-stu-id="f133d-173">In this case, 2.</span></span> |

    <span data-ttu-id="f133d-174">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="f133d-174">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="f133d-175">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="f133d-175">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="f133d-176">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span><span class="sxs-lookup"><span data-stu-id="f133d-176">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="f133d-177">Use the following to view the output:</span><span class="sxs-lookup"><span data-stu-id="f133d-177">Use the following to view the output:</span></span>

    ```
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="f133d-178">The output should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f133d-178">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="f133d-179">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span><span class="sxs-lookup"><span data-stu-id="f133d-179">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="f133d-180">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span><span class="sxs-lookup"><span data-stu-id="f133d-180">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="f133d-181">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span><span class="sxs-lookup"><span data-stu-id="f133d-181">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="f133d-182">Note that the shortest path between ID 1 and ID 4 is 5.</span><span class="sxs-lookup"><span data-stu-id="f133d-182">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="f133d-183">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span><span class="sxs-lookup"><span data-stu-id="f133d-183">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="f133d-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="f133d-185">Next steps</span></span>

* <span data-ttu-id="f133d-186">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f133d-186">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="f133d-187">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="f133d-187">Hue is a web UI that makes it easy to create, run and save Pig and Hive jobs, as well as browse the default storage for your HDInsight cluster.</span></span>

* <span data-ttu-id="f133d-188">[Install R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md): Instructions on how to use cluster customization to install and use R on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="f133d-188">[Install R on HDInsight clusters](hdinsight-hadoop-r-scripts-linux.md): Instructions on how to use cluster customization to install and use R on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f133d-189">R is an open-source language and environment for statistical computing.</span><span class="sxs-lookup"><span data-stu-id="f133d-189">R is an open-source language and environment for statistical computing.</span></span> <span data-ttu-id="f133d-190">It provides hundreds of built-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span><span class="sxs-lookup"><span data-stu-id="f133d-190">It provides hundreds of built-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="f133d-191">It also provides extensive graphical capabilities.</span><span class="sxs-lookup"><span data-stu-id="f133d-191">It also provides extensive graphical capabilities.</span></span>

* <span data-ttu-id="f133d-192">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="f133d-192">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span> <span data-ttu-id="f133d-193">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="f133d-193">Use cluster customization to install Solr on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="f133d-194">Solr allows you to perform powerful search operations on data stored.</span><span class="sxs-lookup"><span data-stu-id="f133d-194">Solr allows you to perform powerful search operations on data stored.</span></span>


