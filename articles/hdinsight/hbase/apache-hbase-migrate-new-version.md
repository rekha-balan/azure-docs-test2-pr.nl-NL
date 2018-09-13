---
title: Migrate an HBase cluster to a new version - Azure HDInsight
description: How to migrate HBase clusters to a new version.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: ashishth
ms.openlocfilehash: 64b3762c40cc2e01944d78c546ebe267503526a7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855887"
---
# <a name="migrate-an-hbase-cluster-to-a-new-version"></a><span data-ttu-id="42d96-103">Migrate an HBase cluster to a new version</span><span class="sxs-lookup"><span data-stu-id="42d96-103">Migrate an HBase cluster to a new version</span></span>

<span data-ttu-id="42d96-104">Job-based clusters, such as Spark and Hadoop, are straightforward to upgrade - see [Upgrade HDInsight cluster to a newer version](../hdinsight-upgrade-cluster.md):</span><span class="sxs-lookup"><span data-stu-id="42d96-104">Job-based clusters, such as Spark and Hadoop, are straightforward to upgrade - see [Upgrade HDInsight cluster to a newer version](../hdinsight-upgrade-cluster.md):</span></span>

1. <span data-ttu-id="42d96-105">Back up transient (locally stored) data.</span><span class="sxs-lookup"><span data-stu-id="42d96-105">Back up transient (locally stored) data.</span></span>
2. <span data-ttu-id="42d96-106">Delete the existing cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-106">Delete the existing cluster.</span></span>
3. <span data-ttu-id="42d96-107">Create a new cluster in the same VNET subnet.</span><span class="sxs-lookup"><span data-stu-id="42d96-107">Create a new cluster in the same VNET subnet.</span></span>
4. <span data-ttu-id="42d96-108">Import transient data.</span><span class="sxs-lookup"><span data-stu-id="42d96-108">Import transient data.</span></span>
5. <span data-ttu-id="42d96-109">Start jobs and continue processing on the new cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-109">Start jobs and continue processing on the new cluster.</span></span>

<span data-ttu-id="42d96-110">To upgrade an HBase cluster some additional steps are needed, as described in this article.</span><span class="sxs-lookup"><span data-stu-id="42d96-110">To upgrade an HBase cluster some additional steps are needed, as described in this article.</span></span>

> [!NOTE]
> <span data-ttu-id="42d96-111">The downtime while upgrading should be minimal, on the order of minutes.</span><span class="sxs-lookup"><span data-stu-id="42d96-111">The downtime while upgrading should be minimal, on the order of minutes.</span></span> <span data-ttu-id="42d96-112">This downtime is caused by the steps to flush all in-memory data, then the time to configure and restart the services on the new cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-112">This downtime is caused by the steps to flush all in-memory data, then the time to configure and restart the services on the new cluster.</span></span> <span data-ttu-id="42d96-113">Your results will vary, depending on the number of nodes, amount of data, and other variables.</span><span class="sxs-lookup"><span data-stu-id="42d96-113">Your results will vary, depending on the number of nodes, amount of data, and other variables.</span></span>

## <a name="review-hbase-compatibility"></a><span data-ttu-id="42d96-114">Review HBase compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-114">Review HBase compatibility</span></span>

<span data-ttu-id="42d96-115">Before upgrading HBase, ensure the HBase versions on the source and destination clusters are compatible.</span><span class="sxs-lookup"><span data-stu-id="42d96-115">Before upgrading HBase, ensure the HBase versions on the source and destination clusters are compatible.</span></span> <span data-ttu-id="42d96-116">For more information, see [Hadoop components and versions available with HDInsight](../hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="42d96-116">For more information, see [Hadoop components and versions available with HDInsight](../hdinsight-component-versioning.md).</span></span>

> [!NOTE]
> <span data-ttu-id="42d96-117">We highly recommend that you review the version compatibility matrix in the [HBase book](https://hbase.apache.org/book.html#upgrading).</span><span class="sxs-lookup"><span data-stu-id="42d96-117">We highly recommend that you review the version compatibility matrix in the [HBase book](https://hbase.apache.org/book.html#upgrading).</span></span>

<span data-ttu-id="42d96-118">Here is an example version compatibility matrix, where Y indicates compatibility and N indicates a potential incompatibility:</span><span class="sxs-lookup"><span data-stu-id="42d96-118">Here is an example version compatibility matrix, where Y indicates compatibility and N indicates a potential incompatibility:</span></span>

| <span data-ttu-id="42d96-119">Compatibility type</span><span class="sxs-lookup"><span data-stu-id="42d96-119">Compatibility type</span></span> | <span data-ttu-id="42d96-120">Major version</span><span class="sxs-lookup"><span data-stu-id="42d96-120">Major version</span></span>| <span data-ttu-id="42d96-121">Minor version</span><span class="sxs-lookup"><span data-stu-id="42d96-121">Minor version</span></span> | <span data-ttu-id="42d96-122">Patch</span><span class="sxs-lookup"><span data-stu-id="42d96-122">Patch</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="42d96-123">Client-Server wire compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-123">Client-Server wire compatibility</span></span> | <span data-ttu-id="42d96-124">N</span><span class="sxs-lookup"><span data-stu-id="42d96-124">N</span></span> | <span data-ttu-id="42d96-125">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-125">Y</span></span> | <span data-ttu-id="42d96-126">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-126">Y</span></span> |
| <span data-ttu-id="42d96-127">Server-Server compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-127">Server-Server compatibility</span></span> | <span data-ttu-id="42d96-128">N</span><span class="sxs-lookup"><span data-stu-id="42d96-128">N</span></span> | <span data-ttu-id="42d96-129">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-129">Y</span></span> | <span data-ttu-id="42d96-130">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-130">Y</span></span> |
| <span data-ttu-id="42d96-131">File format compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-131">File format compatibility</span></span> | <span data-ttu-id="42d96-132">N</span><span class="sxs-lookup"><span data-stu-id="42d96-132">N</span></span> | <span data-ttu-id="42d96-133">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-133">Y</span></span> | <span data-ttu-id="42d96-134">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-134">Y</span></span> |
| <span data-ttu-id="42d96-135">Client API compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-135">Client API compatibility</span></span> | <span data-ttu-id="42d96-136">N</span><span class="sxs-lookup"><span data-stu-id="42d96-136">N</span></span> | <span data-ttu-id="42d96-137">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-137">Y</span></span> | <span data-ttu-id="42d96-138">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-138">Y</span></span> |
| <span data-ttu-id="42d96-139">Client binary compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-139">Client binary compatibility</span></span> | <span data-ttu-id="42d96-140">N</span><span class="sxs-lookup"><span data-stu-id="42d96-140">N</span></span> | <span data-ttu-id="42d96-141">N</span><span class="sxs-lookup"><span data-stu-id="42d96-141">N</span></span> | <span data-ttu-id="42d96-142">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-142">Y</span></span> |
| <span data-ttu-id="42d96-143">**Server-side limited API compatibility**</span><span class="sxs-lookup"><span data-stu-id="42d96-143">**Server-side limited API compatibility**</span></span> |  |  |  |
| <span data-ttu-id="42d96-144">Stable</span><span class="sxs-lookup"><span data-stu-id="42d96-144">Stable</span></span> | <span data-ttu-id="42d96-145">N</span><span class="sxs-lookup"><span data-stu-id="42d96-145">N</span></span> | <span data-ttu-id="42d96-146">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-146">Y</span></span> | <span data-ttu-id="42d96-147">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-147">Y</span></span> |
| <span data-ttu-id="42d96-148">Evolving</span><span class="sxs-lookup"><span data-stu-id="42d96-148">Evolving</span></span> | <span data-ttu-id="42d96-149">N</span><span class="sxs-lookup"><span data-stu-id="42d96-149">N</span></span> | <span data-ttu-id="42d96-150">N</span><span class="sxs-lookup"><span data-stu-id="42d96-150">N</span></span> | <span data-ttu-id="42d96-151">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-151">Y</span></span> |
| <span data-ttu-id="42d96-152">Unstable</span><span class="sxs-lookup"><span data-stu-id="42d96-152">Unstable</span></span> | <span data-ttu-id="42d96-153">N</span><span class="sxs-lookup"><span data-stu-id="42d96-153">N</span></span> | <span data-ttu-id="42d96-154">N</span><span class="sxs-lookup"><span data-stu-id="42d96-154">N</span></span> | <span data-ttu-id="42d96-155">N</span><span class="sxs-lookup"><span data-stu-id="42d96-155">N</span></span> |
| <span data-ttu-id="42d96-156">Dependency compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-156">Dependency compatibility</span></span> | <span data-ttu-id="42d96-157">N</span><span class="sxs-lookup"><span data-stu-id="42d96-157">N</span></span> | <span data-ttu-id="42d96-158">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-158">Y</span></span> | <span data-ttu-id="42d96-159">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-159">Y</span></span> |
| <span data-ttu-id="42d96-160">Operational compatibility</span><span class="sxs-lookup"><span data-stu-id="42d96-160">Operational compatibility</span></span> | <span data-ttu-id="42d96-161">N</span><span class="sxs-lookup"><span data-stu-id="42d96-161">N</span></span> | <span data-ttu-id="42d96-162">N</span><span class="sxs-lookup"><span data-stu-id="42d96-162">N</span></span> | <span data-ttu-id="42d96-163">Y</span><span class="sxs-lookup"><span data-stu-id="42d96-163">Y</span></span> |

> [!NOTE]
> <span data-ttu-id="42d96-164">Any breaking incompatibilities should be described in the HBase version release notes.</span><span class="sxs-lookup"><span data-stu-id="42d96-164">Any breaking incompatibilities should be described in the HBase version release notes.</span></span>

## <a name="upgrade-with-same-hbase-major-version"></a><span data-ttu-id="42d96-165">Upgrade with same HBase major version</span><span class="sxs-lookup"><span data-stu-id="42d96-165">Upgrade with same HBase major version</span></span>

<span data-ttu-id="42d96-166">The following scenario is for upgrading from HDInsight 3.4 to 3.6 (both come with Apache HBase 1.1.2) with the same HBase major version.</span><span class="sxs-lookup"><span data-stu-id="42d96-166">The following scenario is for upgrading from HDInsight 3.4 to 3.6 (both come with Apache HBase 1.1.2) with the same HBase major version.</span></span> <span data-ttu-id="42d96-167">Other version upgrades are similar, as long as there are no compatibility issues between source and destination versions.</span><span class="sxs-lookup"><span data-stu-id="42d96-167">Other version upgrades are similar, as long as there are no compatibility issues between source and destination versions.</span></span>

1. <span data-ttu-id="42d96-168">Make sure that your application is compatible with the new version, as shown in the HBase compatibility matrix and release notes.</span><span class="sxs-lookup"><span data-stu-id="42d96-168">Make sure that your application is compatible with the new version, as shown in the HBase compatibility matrix and release notes.</span></span> <span data-ttu-id="42d96-169">Test your application in a cluster running the target version of HDInsight and HBase.</span><span class="sxs-lookup"><span data-stu-id="42d96-169">Test your application in a cluster running the target version of HDInsight and HBase.</span></span>

2. <span data-ttu-id="42d96-170">[Set up a new destination HDInsight cluster](../hdinsight-hadoop-provision-linux-clusters.md) using the same storage account, but with a different container name:</span><span class="sxs-lookup"><span data-stu-id="42d96-170">[Set up a new destination HDInsight cluster](../hdinsight-hadoop-provision-linux-clusters.md) using the same storage account, but with a different container name:</span></span>

    ![Use the same Storage account, but create a different Container](./media/apache-hbase-migrate-new-version/same-storage-different-container.png)

3. <span data-ttu-id="42d96-172">Flush your source HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-172">Flush your source HBase cluster.</span></span> <span data-ttu-id="42d96-173">This is the cluster from which you are upgrading.</span><span class="sxs-lookup"><span data-stu-id="42d96-173">This is the cluster from which you are upgrading.</span></span> <span data-ttu-id="42d96-174">HBase writes incoming data to an in-memory store, called a _memstore_.</span><span class="sxs-lookup"><span data-stu-id="42d96-174">HBase writes incoming data to an in-memory store, called a _memstore_.</span></span> <span data-ttu-id="42d96-175">After the memstore reaches a certain size, the memstore is flushed to disk for long-term storage in the cluster's storage account.</span><span class="sxs-lookup"><span data-stu-id="42d96-175">After the memstore reaches a certain size, the memstore is flushed to disk for long-term storage in the cluster's storage account.</span></span> <span data-ttu-id="42d96-176">When deleting the old cluster, the memstores are recycled, potentially losing data.</span><span class="sxs-lookup"><span data-stu-id="42d96-176">When deleting the old cluster, the memstores are recycled, potentially losing data.</span></span> <span data-ttu-id="42d96-177">To manually flush the memstore for each table to disk, run the following script.</span><span class="sxs-lookup"><span data-stu-id="42d96-177">To manually flush the memstore for each table to disk, run the following script.</span></span> <span data-ttu-id="42d96-178">The latest version of this script is on Azure's [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/scripts/flush_all_tables.sh).</span><span class="sxs-lookup"><span data-stu-id="42d96-178">The latest version of this script is on Azure's [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/scripts/flush_all_tables.sh).</span></span>

    ```bash
    #!/bin/bash
    
    #-------------------------------------------------------------------------------#
    # SCRIPT TO FLUSH ALL HBASE TABLES.
    #-------------------------------------------------------------------------------#
    
    LIST_OF_TABLES=/tmp/tables.txt
    HBASE_SCRIPT=/tmp/hbase_script.txt
    TARGET_HOST=$1
    
    usage ()
    {
        if [[ "$1" == "-h" ]] || [[ "$1" == "--help" ]]
        then
            cat << ...
    
    Usage: 
    
    $0 [hostname]
    
    Providing hostname is optional and not required when the script is executed within HDInsight cluster with access to 'hbase shell'.
    
    However hostname should be provided when executing the script as a script-action from HDInsight portal.
    
    For Example:
    
        1.  Executing script inside HDInsight cluster (where 'hbase shell' is 
            accessible):
    
            $0 
    
            [No need to provide hostname]
    
        2.  Executing script from HDinsight Azure portal:
    
            Provide Script URL.
    
            Provide hostname as a parameter (i.e. hn0, hn1 or wn2 etc.).
    ...
            exit
        fi
    }
    
    validate_machine ()
    {
        THIS_HOST=`hostname`
    
        if [[ ! -z "$TARGET_HOST" ]] && [[ $THIS_HOST  != $TARGET_HOST* ]]
        then
            echo "[INFO] This machine '$THIS_HOST' is not the right machine ($TARGET_HOST) to execute the script."
            exit 0
        fi
    }
    
    get_tables_list ()
    {
    hbase shell << ... > $LIST_OF_TABLES 2> /dev/null
        list
        exit
    ...
    }
    
    add_table_for_flush ()
    {
        TABLE_NAME=$1
        echo "[INFO] Adding table '$TABLE_NAME' to flush list..."
        cat << ... >> $HBASE_SCRIPT
            flush '$TABLE_NAME'
    ...
    }
    
    clean_up ()
    {
        rm -f $LIST_OF_TABLES
        rm -f $HBASE_SCRIPT
    }
    
    ########
    # MAIN #
    ########
    
    usage $1
    
    validate_machine
    
    clean_up
    
    get_tables_list
    
    START=false
    
    while read LINE 
    do 
        if [[ $LINE == TABLE ]] 
        then
            START=true
            continue
        elif [[ $LINE == *row*in*seconds ]]
        then
            break
        elif [[ $START == true ]]
        then
            add_table_for_flush $LINE
        fi
    
    done < $LIST_OF_TABLES
    
    cat $HBASE_SCRIPT
    
    hbase shell $HBASE_SCRIPT << ... 2> /dev/null
    exit
    ...
    
    ```
    
4. <span data-ttu-id="42d96-179">Stop ingestion to the old HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-179">Stop ingestion to the old HBase cluster.</span></span>
5. <span data-ttu-id="42d96-180">To ensure that any recent data in the memstore is flushed, run the previous script again.</span><span class="sxs-lookup"><span data-stu-id="42d96-180">To ensure that any recent data in the memstore is flushed, run the previous script again.</span></span>
6. <span data-ttu-id="42d96-181">Log in to Ambari on the old cluster (https://OLDCLUSTERNAME.azurehdidnsight.net) and stop the HBase services.</span><span class="sxs-lookup"><span data-stu-id="42d96-181">Log in to Ambari on the old cluster (https://OLDCLUSTERNAME.azurehdidnsight.net) and stop the HBase services.</span></span> <span data-ttu-id="42d96-182">When you are prompted to confirm that you'd like to stop the services, check the box to turn on maintenance mode for HBase.</span><span class="sxs-lookup"><span data-stu-id="42d96-182">When you are prompted to confirm that you'd like to stop the services, check the box to turn on maintenance mode for HBase.</span></span> <span data-ttu-id="42d96-183">For more information on connecting to and using Ambari, see [Manage HDInsight clusters by using the Ambari Web UI](../hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="42d96-183">For more information on connecting to and using Ambari, see [Manage HDInsight clusters by using the Ambari Web UI](../hdinsight-hadoop-manage-ambari.md).</span></span>

    ![In Ambari, click the Services tab, then HBase on the left-hand menu, then Stop under Service Actions](./media/apache-hbase-migrate-new-version/stop-hbase-services.png)

    ![Check the Turn On Maintenance Mode for HBase checkbox, then confirm](./media/apache-hbase-migrate-new-version/turn-on-maintenance-mode.png)

7. <span data-ttu-id="42d96-186">Log in to Ambari on the new HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-186">Log in to Ambari on the new HDInsight cluster.</span></span> <span data-ttu-id="42d96-187">Change the `fs.defaultFS` HDFS setting to point to the container name used by the original cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-187">Change the `fs.defaultFS` HDFS setting to point to the container name used by the original cluster.</span></span> <span data-ttu-id="42d96-188">This setting is under **HDFS > Configs > Advanced > Advanced core-site**.</span><span class="sxs-lookup"><span data-stu-id="42d96-188">This setting is under **HDFS > Configs > Advanced > Advanced core-site**.</span></span>

    ![In Ambari, click the Services tab, then HDFS on the left-hand menu, then the Configs tab, then the Advanced tab underneath](./media/apache-hbase-migrate-new-version/hdfs-advanced-settings.png)

    ![In Ambari, change the container name](./media/apache-hbase-migrate-new-version/change-container-name.png)

8. <span data-ttu-id="42d96-191">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="42d96-191">Save your changes.</span></span>
9. <span data-ttu-id="42d96-192">Restart all required services as indicated by Ambari.</span><span class="sxs-lookup"><span data-stu-id="42d96-192">Restart all required services as indicated by Ambari.</span></span>
10. <span data-ttu-id="42d96-193">Point your application to the new cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-193">Point your application to the new cluster.</span></span>

    > [!NOTE]
    > <span data-ttu-id="42d96-194">The static DNS for your application changes when upgrading.</span><span class="sxs-lookup"><span data-stu-id="42d96-194">The static DNS for your application changes when upgrading.</span></span> <span data-ttu-id="42d96-195">Rather than hard-coding this DNS, you can configure a CNAME in your domain name's DNS settings that points to the cluster's name.</span><span class="sxs-lookup"><span data-stu-id="42d96-195">Rather than hard-coding this DNS, you can configure a CNAME in your domain name's DNS settings that points to the cluster's name.</span></span> <span data-ttu-id="42d96-196">Another option is to use a configuration file for your application that you can update without redeploying.</span><span class="sxs-lookup"><span data-stu-id="42d96-196">Another option is to use a configuration file for your application that you can update without redeploying.</span></span>

11. <span data-ttu-id="42d96-197">Start the ingestion to see if everything is functioning as expected.</span><span class="sxs-lookup"><span data-stu-id="42d96-197">Start the ingestion to see if everything is functioning as expected.</span></span>
12. <span data-ttu-id="42d96-198">If the new cluster is satisfactory, delete the original cluster.</span><span class="sxs-lookup"><span data-stu-id="42d96-198">If the new cluster is satisfactory, delete the original cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="42d96-199">Next steps</span><span class="sxs-lookup"><span data-stu-id="42d96-199">Next steps</span></span>

<span data-ttu-id="42d96-200">To learn more about HBase and upgrading HDInsight clusters, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="42d96-200">To learn more about HBase and upgrading HDInsight clusters, see the following articles:</span></span>

* [<span data-ttu-id="42d96-201">Upgrade an HDInsight cluster to a newer version</span><span class="sxs-lookup"><span data-stu-id="42d96-201">Upgrade an HDInsight cluster to a newer version</span></span>](../hdinsight-upgrade-cluster.md)
* [<span data-ttu-id="42d96-202">Monitor and manage Azure HDInsight using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="42d96-202">Monitor and manage Azure HDInsight using the Ambari Web UI</span></span>](../hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="42d96-203">Hadoop components and versions</span><span class="sxs-lookup"><span data-stu-id="42d96-203">Hadoop components and versions</span></span>](../hdinsight-component-versioning.md)
* [<span data-ttu-id="42d96-204">Optimize configurations using Ambari</span><span class="sxs-lookup"><span data-stu-id="42d96-204">Optimize configurations using Ambari</span></span>](../hdinsight-changing-configs-via-ambari.md#hbase-optimization-with-the-ambari-web-ui)
