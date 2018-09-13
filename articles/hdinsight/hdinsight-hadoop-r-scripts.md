---
title: Use R in HDInsight to customize clusters | Microsoft Docs
description: Learn how to install R using Script Action, and use R on HDInsight clusters.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 4e976a318419d327e4e182c5c08610782ec7dc68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563239"
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="4f5d0-103">Install and use R on HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="4f5d0-103">Install and use R on HDInsight Hadoop clusters</span></span>
<span data-ttu-id="4f5d0-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-104">Learn how to customize Windows based HDInsight cluster with R using Script Action, and how to use R on HDInsight clusters.</span></span> <span data-ttu-id="4f5d0-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-105">The [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="4f5d0-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-106">This allows R scripts to use MapReduce and Spark to run distributed computations.</span></span> <span data-ttu-id="4f5d0-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="4f5d0-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="4f5d0-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="4f5d0-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-110">A sample script to install R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="4f5d0-111">**Related articles**</span><span class="sxs-lookup"><span data-stu-id="4f5d0-111">**Related articles**</span></span>

* [<span data-ttu-id="4f5d0-112">Install and use R on HDinsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4f5d0-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="4f5d0-113">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="4f5d0-113">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="4f5d0-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span><span class="sxs-lookup"><span data-stu-id="4f5d0-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="4f5d0-115">Develop Script Action scripts for HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f5d0-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="4f5d0-116">What is R?</span><span class="sxs-lookup"><span data-stu-id="4f5d0-116">What is R?</span></span>
<span data-ttu-id="4f5d0-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-117">The <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="4f5d0-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="4f5d0-119">It also provides extensive graphical capabilities.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="4f5d0-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-120">R is the preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="4f5d0-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="4f5d0-122">Install R</span><span class="sxs-lookup"><span data-stu-id="4f5d0-122">Install R</span></span>
<span data-ttu-id="4f5d0-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) to install R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="4f5d0-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-124">This section provides instructions about how to use the sample script while creating the cluster using the Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="4f5d0-125">The sample script was introduced with HDInsight cluster version 3.1.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-125">The sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="4f5d0-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="4f5d0-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-127">When you create an HDInsight cluster from the Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="4f5d0-128">On the **Script Actions** page, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="4f5d0-128">On the **Script Actions** page, enter the following values:</span></span>

    <span data-ttu-id="4f5d0-129">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span><span class="sxs-lookup"><span data-stu-id="4f5d0-129">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="4f5d0-130">Property</span><span class="sxs-lookup"><span data-stu-id="4f5d0-130">Property</span></span></th><th><span data-ttu-id="4f5d0-131">Value</span><span class="sxs-lookup"><span data-stu-id="4f5d0-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="4f5d0-132">Name</span><span class="sxs-lookup"><span data-stu-id="4f5d0-132">Name</span></span></td>
            <td><span data-ttu-id="4f5d0-133">Specify a name for the script action, for example, <b>Install R</b>.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-133">Specify a name for the script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="4f5d0-134">Script URI</span><span class="sxs-lookup"><span data-stu-id="4f5d0-134">Script URI</span></span></td>
            <td><span data-ttu-id="4f5d0-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="4f5d0-135">Specify the URI to the script that is invoked to customize the cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="4f5d0-136">Node Type</span><span class="sxs-lookup"><span data-stu-id="4f5d0-136">Node Type</span></span></td>
            <td><span data-ttu-id="4f5d0-137">Specify the nodes on which the customization script is run.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="4f5d0-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="4f5d0-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="4f5d0-139">Parameters</span></span></td>
            <td><span data-ttu-id="4f5d0-140">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="4f5d0-141">However, the script to install R does not require any parameters, so you can leave this blank.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-141">However, the script to install R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="4f5d0-142">You can add more than one script action to install multiple components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="4f5d0-143">After you have added the scripts, click the check mark to start crating the cluster.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-143">After you have added the scripts, click the check mark to start crating the cluster.</span></span>

<span data-ttu-id="4f5d0-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-144">You can also use the script to install R on HDInsight by using Azure PowerShell or the HDInsight .NET SDK.</span></span> <span data-ttu-id="4f5d0-145">Instructions for these procedures are provided later in this article.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="4f5d0-146">Run R scripts</span><span class="sxs-lookup"><span data-stu-id="4f5d0-146">Run R scripts</span></span>
<span data-ttu-id="4f5d0-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-147">This section describes how to run an R script on the Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="4f5d0-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-148">**Establish a Remote Desktop connection to the cluster**: From the Portal, enable Remote Desktop for the cluster you created with R installed, and then connect to the cluster.</span></span> <span data-ttu-id="4f5d0-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-149">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="4f5d0-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-150">**Open the R console**: The R installation puts a link to the R console on the desktop of the head node.</span></span> <span data-ttu-id="4f5d0-151">Click on it to open the R console.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-151">Click on it to open the R console.</span></span>
3. <span data-ttu-id="4f5d0-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-152">**Run the R script**: The R script can be run directly from the R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="4f5d0-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-153">Here is a simple example script that generates the numbers 1 to 100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="4f5d0-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-154">The first two lines call the RHadoop libraries that are installed with R. The final line prints the results to the console.</span></span> <span data-ttu-id="4f5d0-155">The output should look like this:</span><span class="sxs-lookup"><span data-stu-id="4f5d0-155">The output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="4f5d0-156">Install R using Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f5d0-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="4f5d0-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="4f5d0-158">The sample demonstrates how to install Spark using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-158">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="4f5d0-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-159">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="4f5d0-160">Install R using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4f5d0-160">Install R using .NET SDK</span></span>
<span data-ttu-id="4f5d0-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="4f5d0-162">The sample demonstrates how to install Spark using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-162">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="4f5d0-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="4f5d0-163">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="4f5d0-164">See also</span><span class="sxs-lookup"><span data-stu-id="4f5d0-164">See also</span></span>
* [<span data-ttu-id="4f5d0-165">Install and use R on HDinsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4f5d0-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="4f5d0-166">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="4f5d0-166">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="4f5d0-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span><span class="sxs-lookup"><span data-stu-id="4f5d0-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="4f5d0-168">Develop Script Action scripts for HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f5d0-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="4f5d0-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span><span class="sxs-lookup"><span data-stu-id="4f5d0-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="4f5d0-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span><span class="sxs-lookup"><span data-stu-id="4f5d0-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="4f5d0-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span><span class="sxs-lookup"><span data-stu-id="4f5d0-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md

