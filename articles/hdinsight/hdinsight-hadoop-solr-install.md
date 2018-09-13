---
title: Use Script Action to install Solr on Hadoop cluster | Microsoft Docs
description: Learn how to customize HDInsight cluster with Solr using Script Action.
services: hdinsight
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: d2aa2c1e05f49a3b9c2f8054cbf933bb01ebbed3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661906"
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="4841e-103">Install and use Solr on Windows-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="4841e-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="4841e-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span><span class="sxs-lookup"><span data-stu-id="4841e-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4841e-105">The steps in this document only work with Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4841e-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="4841e-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="4841e-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="4841e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="4841e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4841e-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="4841e-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="4841e-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4841e-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="4841e-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span><span class="sxs-lookup"><span data-stu-id="4841e-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="4841e-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4841e-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="4841e-112">The sample script works only with HDInsight cluster version 3.1.</span><span class="sxs-lookup"><span data-stu-id="4841e-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="4841e-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4841e-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="4841e-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span><span class="sxs-lookup"><span data-stu-id="4841e-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="4841e-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span><span class="sxs-lookup"><span data-stu-id="4841e-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="4841e-116">**Related articles**</span><span class="sxs-lookup"><span data-stu-id="4841e-116">**Related articles**</span></span>

* [<span data-ttu-id="4841e-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4841e-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="4841e-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4841e-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="4841e-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span><span class="sxs-lookup"><span data-stu-id="4841e-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="4841e-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="4841e-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="4841e-121">What is Solr?</span><span class="sxs-lookup"><span data-stu-id="4841e-121">What is Solr?</span></span>
<span data-ttu-id="4841e-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span><span class="sxs-lookup"><span data-stu-id="4841e-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="4841e-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="4841e-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="4841e-124">Install Solr using portal</span><span class="sxs-lookup"><span data-stu-id="4841e-124">Install Solr using portal</span></span>
1. <span data-ttu-id="4841e-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="4841e-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="4841e-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span><span class="sxs-lookup"><span data-stu-id="4841e-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="4841e-127">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span><span class="sxs-lookup"><span data-stu-id="4841e-127">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="4841e-128">Property</span><span class="sxs-lookup"><span data-stu-id="4841e-128">Property</span></span></th><th><span data-ttu-id="4841e-129">Value</span><span class="sxs-lookup"><span data-stu-id="4841e-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="4841e-130">Name</span><span class="sxs-lookup"><span data-stu-id="4841e-130">Name</span></span></td>
            <td><span data-ttu-id="4841e-131">Specify a name for the script action.</span><span class="sxs-lookup"><span data-stu-id="4841e-131">Specify a name for the script action.</span></span> <span data-ttu-id="4841e-132">For example, <b>Install Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="4841e-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="4841e-133">Script URI</span><span class="sxs-lookup"><span data-stu-id="4841e-133">Script URI</span></span></td>
            <td><span data-ttu-id="4841e-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span><span class="sxs-lookup"><span data-stu-id="4841e-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="4841e-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="4841e-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="4841e-136">Node Type</span><span class="sxs-lookup"><span data-stu-id="4841e-136">Node Type</span></span></td>
            <td><span data-ttu-id="4841e-137">Specify the nodes on which the customization script is run.</span><span class="sxs-lookup"><span data-stu-id="4841e-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="4841e-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span><span class="sxs-lookup"><span data-stu-id="4841e-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="4841e-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="4841e-139">Parameters</span></span></td>
            <td><span data-ttu-id="4841e-140">Specify the parameters, if required by the script.</span><span class="sxs-lookup"><span data-stu-id="4841e-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="4841e-141">The script to install Solr does not require any parameters, so you can leave this blank.</span><span class="sxs-lookup"><span data-stu-id="4841e-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="4841e-142">You can add more than one script action to install multiple components on the cluster.</span><span class="sxs-lookup"><span data-stu-id="4841e-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="4841e-143">After you have added the scripts, click the checkmark to start creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="4841e-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="4841e-144">Use Solr</span><span class="sxs-lookup"><span data-stu-id="4841e-144">Use Solr</span></span>
<span data-ttu-id="4841e-145">You must start with indexing Solr with some data files.</span><span class="sxs-lookup"><span data-stu-id="4841e-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="4841e-146">You can then use Solr to run search queries on the indexed data.</span><span class="sxs-lookup"><span data-stu-id="4841e-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="4841e-147">Perform the following steps to use Solr in an HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="4841e-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="4841e-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span><span class="sxs-lookup"><span data-stu-id="4841e-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="4841e-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span><span class="sxs-lookup"><span data-stu-id="4841e-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="4841e-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="4841e-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="4841e-151">**Index Solr by uploading data files**.</span><span class="sxs-lookup"><span data-stu-id="4841e-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="4841e-152">When you index Solr, you put documents in it that you may need to search on.</span><span class="sxs-lookup"><span data-stu-id="4841e-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="4841e-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="4841e-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="4841e-154">Run the following command:</span><span class="sxs-lookup"><span data-stu-id="4841e-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="4841e-155">You'll see the following output on the console:</span><span class="sxs-lookup"><span data-stu-id="4841e-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="4841e-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="4841e-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="4841e-157">The post.jar utility and the sample documents are available with Solr installation.</span><span class="sxs-lookup"><span data-stu-id="4841e-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="4841e-158">**Use the Solr dashboard to search within the indexed documents**.</span><span class="sxs-lookup"><span data-stu-id="4841e-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="4841e-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="4841e-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="4841e-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span><span class="sxs-lookup"><span data-stu-id="4841e-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="4841e-161">As an example, to select and return all the docs in Solr, provide the following values:</span><span class="sxs-lookup"><span data-stu-id="4841e-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="4841e-162">In the **q** text box, enter **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="4841e-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="4841e-163">This will return all the documents that are indexed in Solr.</span><span class="sxs-lookup"><span data-stu-id="4841e-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="4841e-164">If you want to search for a specific string within the documents, you can enter that string here.</span><span class="sxs-lookup"><span data-stu-id="4841e-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="4841e-165">In the **wt** text box, select the output format.</span><span class="sxs-lookup"><span data-stu-id="4841e-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="4841e-166">Default is **json**.</span><span class="sxs-lookup"><span data-stu-id="4841e-166">Default is **json**.</span></span> <span data-ttu-id="4841e-167">Click **Execute Query**.</span><span class="sxs-lookup"><span data-stu-id="4841e-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="4841e-168">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span><span class="sxs-lookup"><span data-stu-id="4841e-168">![Use Script Action to customize a cluster](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="4841e-169">The output returns the two docs that we used for indexing Solr.</span><span class="sxs-lookup"><span data-stu-id="4841e-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="4841e-170">The output resembles the following:</span><span class="sxs-lookup"><span data-stu-id="4841e-170">The output resembles the following:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }
4. <span data-ttu-id="4841e-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span><span class="sxs-lookup"><span data-stu-id="4841e-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="4841e-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4841e-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="4841e-173">Perform the following steps to do so:</span><span class="sxs-lookup"><span data-stu-id="4841e-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="4841e-174">From the RDP session, open Internet Explorer, and point to the following URL:</span><span class="sxs-lookup"><span data-stu-id="4841e-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="4841e-175">You should see a response like this:</span><span class="sxs-lookup"><span data-stu-id="4841e-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="4841e-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span><span class="sxs-lookup"><span data-stu-id="4841e-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="4841e-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="4841e-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="4841e-178">At this location, you should see a snapshot folder created with a name similar to \**snapshot.* timestamp\*\*\*.</span><span class="sxs-lookup"><span data-stu-id="4841e-178">At this location, you should see a snapshot folder created with a name similar to \**snapshot.* timestamp\*\*\*.</span></span>
   3. <span data-ttu-id="4841e-179">Zip the snapshot folder and upload it to Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4841e-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="4841e-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span><span class="sxs-lookup"><span data-stu-id="4841e-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="4841e-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span><span class="sxs-lookup"><span data-stu-id="4841e-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="4841e-182">Install Solr using Aure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4841e-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="4841e-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4841e-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="4841e-184">The sample demonstrates how to install Spark using Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4841e-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="4841e-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4841e-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="4841e-186">Install Solr using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="4841e-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="4841e-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="4841e-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="4841e-188">The sample demonstrates how to install Spark using the .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="4841e-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="4841e-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="4841e-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="4841e-190">See also</span><span class="sxs-lookup"><span data-stu-id="4841e-190">See also</span></span>
* [<span data-ttu-id="4841e-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="4841e-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="4841e-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="4841e-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="4841e-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span><span class="sxs-lookup"><span data-stu-id="4841e-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="4841e-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="4841e-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="4841e-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span><span class="sxs-lookup"><span data-stu-id="4841e-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="4841e-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span><span class="sxs-lookup"><span data-stu-id="4841e-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="4841e-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span><span class="sxs-lookup"><span data-stu-id="4841e-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md


