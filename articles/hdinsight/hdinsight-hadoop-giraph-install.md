---
title: Install and use Giraph on Hadoop clusters in HDInsight | Microsoft Docs
description: Learn how to customize HDInsight cluster with Giraph, and how to use Giraph.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f98e129015e257a00c884e9e82a5ced13d93880c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550367"
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="2dd3e-103">Install and use Giraph on Windows-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="2dd3e-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="2dd3e-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-104">Learn how to customize Windows based HDInsight cluster with Giraph using Script Action, and how to use Giraph to process large-scale graphs.</span></span> <span data-ttu-id="2dd3e-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2dd3e-106">The steps in this document only work with Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-106">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="2dd3e-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="2dd3e-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="2dd3e-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-109">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="2dd3e-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-110">For information on how to install Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="2dd3e-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="2dd3e-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-112">A sample script to install Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="2dd3e-113">The sample script works only with HDInsight cluster version 3.1.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-113">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="2dd3e-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="2dd3e-115">**Related articles**</span><span class="sxs-lookup"><span data-stu-id="2dd3e-115">**Related articles**</span></span>

* [<span data-ttu-id="2dd3e-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="2dd3e-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="2dd3e-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="2dd3e-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="2dd3e-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="2dd3e-120">What is Giraph?</span><span class="sxs-lookup"><span data-stu-id="2dd3e-120">What is Giraph?</span></span>
<span data-ttu-id="2dd3e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="2dd3e-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-122">Graphs model relationships between objects, such as the connections between routers on a large network like the Internet, or relationships between people on social networks (sometimes referred to as a social graph).</span></span> <span data-ttu-id="2dd3e-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-123">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="2dd3e-124">Identifying potential friends based on your current relationships.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="2dd3e-125">Identifying the shortest route between two computers in a network.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-125">Identifying the shortest route between two computers in a network.</span></span>
* <span data-ttu-id="2dd3e-126">Calculating the page rank of webpages.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-126">Calculating the page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="2dd3e-127">Install Giraph using portal</span><span class="sxs-lookup"><span data-stu-id="2dd3e-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="2dd3e-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-128">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="2dd3e-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-129">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="2dd3e-130">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span><span class="sxs-lookup"><span data-stu-id="2dd3e-130">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="2dd3e-131">Property</span><span class="sxs-lookup"><span data-stu-id="2dd3e-131">Property</span></span></th><th><span data-ttu-id="2dd3e-132">Value</span><span class="sxs-lookup"><span data-stu-id="2dd3e-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="2dd3e-133">Name</span><span class="sxs-lookup"><span data-stu-id="2dd3e-133">Name</span></span></td>
            <td><span data-ttu-id="2dd3e-134">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-134">Specify a name for the script action.</span></span> <span data-ttu-id="2dd3e-135">For example, <b>Install Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="2dd3e-136">Script URI</span><span class="sxs-lookup"><span data-stu-id="2dd3e-136">Script URI</span></span></td>
            <td><span data-ttu-id="2dd3e-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-137">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="2dd3e-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="2dd3e-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="2dd3e-139">Node Type</span><span class="sxs-lookup"><span data-stu-id="2dd3e-139">Node Type</span></span></td>
            <td><span data-ttu-id="2dd3e-140">Specify the nodes on which the customization script is run.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-140">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="2dd3e-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="2dd3e-142">Parameters</span><span class="sxs-lookup"><span data-stu-id="2dd3e-142">Parameters</span></span></td>
            <td><span data-ttu-id="2dd3e-143">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-143">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="2dd3e-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-144">The script to install Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="2dd3e-145">You can add more than one script action to install multiple components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-145">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="2dd3e-146">After you have added the scripts, click the checkmark to start creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-146">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="2dd3e-147">Use Giraph</span><span class="sxs-lookup"><span data-stu-id="2dd3e-147">Use Giraph</span></span>
<span data-ttu-id="2dd3e-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-148">We use the SimpleShortestPathsComputation example to demonstrate the basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding the shortest path between objects in a graph.</span></span> <span data-ttu-id="2dd3e-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-149">Use the following steps to upload the sample data and the sample jar, run a job by using the SimpleShortestPathsComputation example, and then view the results.</span></span>

1. <span data-ttu-id="2dd3e-150">Upload a sample data file to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-150">Upload a sample data file to Azure Blob storage.</span></span> <span data-ttu-id="2dd3e-151">On your local workstation, create a new file named **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="2dd3e-152">It should contain the following lines:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-152">It should contain the following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="2dd3e-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-153">Upload the tiny_graph.txt file to the primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="2dd3e-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-154">For instructions on how to upload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="2dd3e-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-155">This data describes a relationship between objects in a directed graph, by using the format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="2dd3e-156">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-156">The **edge\_value** (or weight) can be thought of as the strength or distance of the connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="2dd3e-157">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-157">Drawn out, and using the value (or weight) as the distance between objects, the above data might look like this:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="2dd3e-159">Run the SimpleShortestPathsComputation example.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-159">Run the SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="2dd3e-160">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-160">Use the following Azure PowerShell cmdlets to run the example by using the tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="2dd3e-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="2dd3e-162">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-162">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2dd3e-163">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-163">Please follow the steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="2dd3e-164">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-164">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasbs:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasbs:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasbs:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="2dd3e-165">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-165">In the above example, replace **clustername** with the name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="2dd3e-166">View the results.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-166">View the results.</span></span> <span data-ttu-id="2dd3e-167">Once the job has finished, the results will be stored in two output files in the **wasbs:///example/out/shotestpaths** folder.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-167">Once the job has finished, the results will be stored in two output files in the **wasbs:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="2dd3e-168">The files are called **part-m-00001** and **part-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-168">The files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="2dd3e-169">Perform the following steps to download and view the output:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-169">Perform the following steps to download and view the output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="2dd3e-170">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-170">This will create the **example/output/shortestpaths** directory structure in the current directory on your workstation, and download the two output files to that location.</span></span>

    <span data-ttu-id="2dd3e-171">Use the **Cat** cmdlet to display the contents of the files:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-171">Use the **Cat** cmdlet to display the contents of the files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="2dd3e-172">The output should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="2dd3e-172">The output should appear similar to the following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="2dd3e-173">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-173">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="2dd3e-174">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-174">So the output should be read as `destination_id distance`, where distance is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="2dd3e-175">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-175">Visualizing this, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="2dd3e-176">Note that the shortest path between ID 1 and ID 4 is 5.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-176">Note that the shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="2dd3e-177">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-177">This is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="2dd3e-179">Install Giraph using Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2dd3e-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="2dd3e-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="2dd3e-181">The sample demonstrates how to install Spark using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-181">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="2dd3e-182">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-182">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="2dd3e-183">Install Giraph using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2dd3e-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="2dd3e-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="2dd3e-185">The sample demonstrates how to install Spark using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-185">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="2dd3e-186">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-186">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="2dd3e-187">See also</span><span class="sxs-lookup"><span data-stu-id="2dd3e-187">See also</span></span>
* [<span data-ttu-id="2dd3e-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="2dd3e-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="2dd3e-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="2dd3e-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="2dd3e-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="2dd3e-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="2dd3e-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="2dd3e-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="2dd3e-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span><span class="sxs-lookup"><span data-stu-id="2dd3e-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md



