---
title: Use Script Action to install Solr on Linux-based HDInsight - Azure
description: Learn how to install Solr on Linux-based HDInsight Hadoop clusters using Script Actions.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: jasonh
ms.openlocfilehash: 205983344be8ae5bbe566a208ceb862b2e93cb8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800129"
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d4d0a-103">Install and use Solr on HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="d4d0a-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d4d0a-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="d4d0a-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="d4d0a-106">The steps in this document require an HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d4d0a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d4d0a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4d0a-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="d4d0a-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <a name="whatis"></a><span data-ttu-id="d4d0a-111">What is Solr</span><span class="sxs-lookup"><span data-stu-id="d4d0a-111">What is Solr</span></span>

<span data-ttu-id="d4d0a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="d4d0a-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="d4d0a-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="d4d0a-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="d4d0a-116">Microsoft support may not be able to resolve problems with custom components.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="d4d0a-117">You may need to engage the open source communities for assistance.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="d4d0a-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="d4d0a-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="d4d0a-120">What the script does</span><span class="sxs-lookup"><span data-stu-id="d4d0a-120">What the script does</span></span>

<span data-ttu-id="d4d0a-121">This script makes the following changes to the HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="d4d0a-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="d4d0a-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="d4d0a-123">Creates a user, **solrusr**, which is used to run the Solr service</span><span class="sxs-lookup"><span data-stu-id="d4d0a-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="d4d0a-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="d4d0a-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="d4d0a-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <a name="install"></a><span data-ttu-id="d4d0a-126">Install Solr using Script Actions</span><span class="sxs-lookup"><span data-stu-id="d4d0a-126">Install Solr using Script Actions</span></span>

<span data-ttu-id="d4d0a-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="d4d0a-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="d4d0a-129">During the creation process, use the following steps to install Solr:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="d4d0a-130">From the __Cluster summary__ section, select__Advanced settings__, then __Script actions__.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-130">From the __Cluster summary__ section, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="d4d0a-131">Use the following information to populate the form:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="d4d0a-132">**NAME**: Enter a friendly name for the script action.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="d4d0a-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="d4d0a-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="d4d0a-134">**HEAD**: Check this option</span><span class="sxs-lookup"><span data-stu-id="d4d0a-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="d4d0a-135">**WORKER**: Check this option</span><span class="sxs-lookup"><span data-stu-id="d4d0a-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="d4d0a-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span><span class="sxs-lookup"><span data-stu-id="d4d0a-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="d4d0a-137">**PARAMETERS**: Leave this field blank</span><span class="sxs-lookup"><span data-stu-id="d4d0a-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="d4d0a-138">At the bottom of the **Script actions** section, use the **Select** button to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-138">At the bottom of the **Script actions** section, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="d4d0a-139">Finally, use the **Next** button to return to the __Cluster summary__</span><span class="sxs-lookup"><span data-stu-id="d4d0a-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="d4d0a-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <a name="usesolr"></a><span data-ttu-id="d4d0a-141">How do I use Solr in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4d0a-141">How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d4d0a-142">The steps in this section demonstrate basic Solr functionality.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="d4d0a-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="d4d0a-144">Index data</span><span class="sxs-lookup"><span data-stu-id="d4d0a-144">Index data</span></span>

<span data-ttu-id="d4d0a-145">Use the following steps to add example data to Solr, and then query it:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="d4d0a-146">Connect to the HDInsight cluster using SSH:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-146">Connect to the HDInsight cluster using SSH:</span></span>

    > [!NOTE]
    > <span data-ttu-id="d4d0a-147">Replace `sshuser` with the SSH user for the cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-147">Replace `sshuser` with the SSH user for the cluster.</span></span> <span data-ttu-id="d4d0a-148">Replace `clustername` with the name of the cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-148">Replace `clustername` with the name of the cluster.</span></span>

    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="d4d0a-149">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-149">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="d4d0a-150">Steps later in this document use an SSH tunnel to connect to the Solr web UI.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-150">Steps later in this document use an SSH tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="d4d0a-151">To use these steps, you must establish an SSH tunnel and then configure your browser to use it.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-151">To use these steps, you must establish an SSH tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="d4d0a-152">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-152">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="d4d0a-153">Use the following commands to have Solr index sample data:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-153">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="d4d0a-154">The following output is returned to the console:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-154">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="d4d0a-155">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-155">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="d4d0a-156">Use the following command to query the Solr REST API:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-156">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="d4d0a-157">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-157">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="d4d0a-158">The following JSON document is an example of the response:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-158">The following JSON document is an example of the response:</span></span>

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

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="d4d0a-159">Using the Solr dashboard</span><span class="sxs-lookup"><span data-stu-id="d4d0a-159">Using the Solr dashboard</span></span>

<span data-ttu-id="d4d0a-160">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-160">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="d4d0a-161">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-161">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="d4d0a-162">You can use an SSH tunnel to access it.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-162">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="d4d0a-163">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-163">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="d4d0a-164">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-164">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="d4d0a-165">Determine the host name for the primary headnode:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-165">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="d4d0a-166">Use SSH to connect to the cluster head node.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-166">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="d4d0a-167">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-167">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="d4d0a-168">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-168">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="d4d0a-169">Use the following command to get the fully qualified hostname:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-169">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="d4d0a-170">This command returns a value similar to the following host name:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-170">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="d4d0a-171">Save the value returned, as it is used later.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-171">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="d4d0a-172">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-172">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="d4d0a-173">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-173">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="d4d0a-174">The page appears similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-174">The page appears similar to the following image:</span></span>

    ![Image of Solr dashboard](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="d4d0a-176">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-176">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="d4d0a-177">Several entries should them appear below **collection1**.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-177">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="d4d0a-178">From the entries below **collection1**, select **Query**.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-178">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="d4d0a-179">Use the following values to populate the search page:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-179">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="d4d0a-180">In the **q** text box, enter **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-180">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="d4d0a-181">This query returns all the documents that are indexed in Solr.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-181">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="d4d0a-182">If you want to search for a specific string within the documents, you can enter that string here.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-182">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="d4d0a-183">In the **wt** text box, select the output format.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-183">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="d4d0a-184">Default is **json**.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-184">Default is **json**.</span></span>

     <span data-ttu-id="d4d0a-185">Finally, select the **Execute Query** button at the bottom of the search pate.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-185">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="d4d0a-187">The output returns the two documents that you added to the index earlier.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-187">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="d4d0a-188">The output is similar to the following JSON document:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-188">The output is similar to the following JSON document:</span></span>

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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="d4d0a-189">Starting and stopping Solr</span><span class="sxs-lookup"><span data-stu-id="d4d0a-189">Starting and stopping Solr</span></span>

<span data-ttu-id="d4d0a-190">Use the following commands to manually stop and start Solr:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-190">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="d4d0a-191">Backup indexed data</span><span class="sxs-lookup"><span data-stu-id="d4d0a-191">Backup indexed data</span></span>

<span data-ttu-id="d4d0a-192">Use the following steps to back up Solr data to the default storage for your cluster:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-192">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="d4d0a-193">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-193">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="d4d0a-194">Use the following command to create a snapshot of the indexed data.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-194">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="d4d0a-195">Replace **HOSTNAME** with the name returned from the previous command:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-195">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="d4d0a-196">The response is similar to the following XML:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-196">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="d4d0a-197">Change directories to `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-197">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="d4d0a-198">There is a subdirectory here for each collection.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-198">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="d4d0a-199">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-199">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="d4d0a-200">To create a compressed archive of the snapshot folder, use the following command:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-200">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="d4d0a-201">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-201">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="d4d0a-202">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-202">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="d4d0a-203">You can then store the archive to the cluster's primary storage using the following command:</span><span class="sxs-lookup"><span data-stu-id="d4d0a-203">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="d4d0a-204">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-204">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d4d0a-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="d4d0a-205">Next steps</span></span>

* <span data-ttu-id="d4d0a-206">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-206">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="d4d0a-207">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-207">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d4d0a-208">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-208">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="d4d0a-209">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d4d0a-209">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="d4d0a-210">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-210">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="d4d0a-211">Hue is a set of Web applications used to interact with a Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="d4d0a-211">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
