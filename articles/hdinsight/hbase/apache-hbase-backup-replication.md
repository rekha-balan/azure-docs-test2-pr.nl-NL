---
title: Set up HBase and Phoenix backup and replication - Azure HDInsight
description: Set up backup and replication for HBase and Phoenix.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/22/2018
ms.author: ashishth
ms.openlocfilehash: 0dfb1cf5ce16e9aa30bb7f9fcc43bd24ccb90d76
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856112"
---
# <a name="set-up-backup-and-replication-for-hbase-and-phoenix-on-hdinsight"></a><span data-ttu-id="bc530-103">Set up backup and replication for HBase and Phoenix on HDInsight</span><span class="sxs-lookup"><span data-stu-id="bc530-103">Set up backup and replication for HBase and Phoenix on HDInsight</span></span>

<span data-ttu-id="bc530-104">HBase supports several approaches for guarding against data loss:</span><span class="sxs-lookup"><span data-stu-id="bc530-104">HBase supports several approaches for guarding against data loss:</span></span>

* <span data-ttu-id="bc530-105">Copy the `hbase` folder</span><span class="sxs-lookup"><span data-stu-id="bc530-105">Copy the `hbase` folder</span></span>
* <span data-ttu-id="bc530-106">Export then Import</span><span class="sxs-lookup"><span data-stu-id="bc530-106">Export then Import</span></span>
* <span data-ttu-id="bc530-107">Copy tables</span><span class="sxs-lookup"><span data-stu-id="bc530-107">Copy tables</span></span>
* <span data-ttu-id="bc530-108">Snapshots</span><span class="sxs-lookup"><span data-stu-id="bc530-108">Snapshots</span></span>
* <span data-ttu-id="bc530-109">Replication</span><span class="sxs-lookup"><span data-stu-id="bc530-109">Replication</span></span>

> [!NOTE]
> <span data-ttu-id="bc530-110">Apache Phoenix stores its metadata in HBase tables, so that metadata is backed up when you back up the HBase system catalog tables.</span><span class="sxs-lookup"><span data-stu-id="bc530-110">Apache Phoenix stores its metadata in HBase tables, so that metadata is backed up when you back up the HBase system catalog tables.</span></span>

<span data-ttu-id="bc530-111">The following sections describe the usage scenario for each of these approaches.</span><span class="sxs-lookup"><span data-stu-id="bc530-111">The following sections describe the usage scenario for each of these approaches.</span></span>

## <a name="copy-the-hbase-folder"></a><span data-ttu-id="bc530-112">Copy the hbase folder</span><span class="sxs-lookup"><span data-stu-id="bc530-112">Copy the hbase folder</span></span>

<span data-ttu-id="bc530-113">With this approach, you copy all HBase data, without being able to select a subset of tables or column families.</span><span class="sxs-lookup"><span data-stu-id="bc530-113">With this approach, you copy all HBase data, without being able to select a subset of tables or column families.</span></span> <span data-ttu-id="bc530-114">Subsequent approaches provide greater control.</span><span class="sxs-lookup"><span data-stu-id="bc530-114">Subsequent approaches provide greater control.</span></span>

<span data-ttu-id="bc530-115">HBase in HDInsight uses the default storage selected when creating the cluster, either Azure Storage blobs or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="bc530-115">HBase in HDInsight uses the default storage selected when creating the cluster, either Azure Storage blobs or Azure Data Lake Store.</span></span> <span data-ttu-id="bc530-116">In either case, HBase stores its data and metadata files under the following path:</span><span class="sxs-lookup"><span data-stu-id="bc530-116">In either case, HBase stores its data and metadata files under the following path:</span></span>

    /hbase

* <span data-ttu-id="bc530-117">In an Azure Storage account the `hbase` folder resides at the root of the blob container:</span><span class="sxs-lookup"><span data-stu-id="bc530-117">In an Azure Storage account the `hbase` folder resides at the root of the blob container:</span></span>

    ```
    wasbs://<containername>@<accountname>.blob.core.windows.net/hbase
    ```

* <span data-ttu-id="bc530-118">In Azure Data Lake Store the `hbase` folder resides under the root path you specified when provisioning a cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-118">In Azure Data Lake Store the `hbase` folder resides under the root path you specified when provisioning a cluster.</span></span> <span data-ttu-id="bc530-119">This root path typically has a `clusters` folder, with a subfolder named after your HDInsight cluster:</span><span class="sxs-lookup"><span data-stu-id="bc530-119">This root path typically has a `clusters` folder, with a subfolder named after your HDInsight cluster:</span></span>

    ```
    /clusters/<clusterName>/hbase
    ```

<span data-ttu-id="bc530-120">In either case, the `hbase` folder contains all the data that HBase has flushed to disk, but it may not contain the in-memory data.</span><span class="sxs-lookup"><span data-stu-id="bc530-120">In either case, the `hbase` folder contains all the data that HBase has flushed to disk, but it may not contain the in-memory data.</span></span> <span data-ttu-id="bc530-121">Before you can rely on this folder as an accurate representation of the HBase data, you must shut down the cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-121">Before you can rely on this folder as an accurate representation of the HBase data, you must shut down the cluster.</span></span>

<span data-ttu-id="bc530-122">After you delete the cluster, you can either leave the data in place, or copy the data to a new location:</span><span class="sxs-lookup"><span data-stu-id="bc530-122">After you delete the cluster, you can either leave the data in place, or copy the data to a new location:</span></span>

* <span data-ttu-id="bc530-123">Create a new HDInsight instance pointing to the current storage location.</span><span class="sxs-lookup"><span data-stu-id="bc530-123">Create a new HDInsight instance pointing to the current storage location.</span></span> <span data-ttu-id="bc530-124">The new instance is created with all the existing data.</span><span class="sxs-lookup"><span data-stu-id="bc530-124">The new instance is created with all the existing data.</span></span>

* <span data-ttu-id="bc530-125">Copy the `hbase` folder to a different Azure Storage blob container or Data Lake Store location, and then start a new cluster with that data.</span><span class="sxs-lookup"><span data-stu-id="bc530-125">Copy the `hbase` folder to a different Azure Storage blob container or Data Lake Store location, and then start a new cluster with that data.</span></span> <span data-ttu-id="bc530-126">For Azure Storage, use [AzCopy](../../storage/common/storage-use-azcopy.md), and for Data Lake Store use [AdlCopy](../../data-lake-store/data-lake-store-copy-data-azure-storage-blob.md).</span><span class="sxs-lookup"><span data-stu-id="bc530-126">For Azure Storage, use [AzCopy](../../storage/common/storage-use-azcopy.md), and for Data Lake Store use [AdlCopy](../../data-lake-store/data-lake-store-copy-data-azure-storage-blob.md).</span></span>

## <a name="export-then-import"></a><span data-ttu-id="bc530-127">Export then Import</span><span class="sxs-lookup"><span data-stu-id="bc530-127">Export then Import</span></span>

<span data-ttu-id="bc530-128">On the source HDInsight cluster, use the Export utility (included with HBase) to export data from a source table to the default attached storage.</span><span class="sxs-lookup"><span data-stu-id="bc530-128">On the source HDInsight cluster, use the Export utility (included with HBase) to export data from a source table to the default attached storage.</span></span> <span data-ttu-id="bc530-129">You can then copy the exported folder to the destination storage location, and run the Import utility on the destination HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-129">You can then copy the exported folder to the destination storage location, and run the Import utility on the destination HDInsight cluster.</span></span>

<span data-ttu-id="bc530-130">To export a table, first SSH into the head node of your source HDInsight cluster and then run the following `hbase` command:</span><span class="sxs-lookup"><span data-stu-id="bc530-130">To export a table, first SSH into the head node of your source HDInsight cluster and then run the following `hbase` command:</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.Export "<tableName>" "/<path>/<to>/<export>"

<span data-ttu-id="bc530-131">To import a table, SSH into the head node of your destination HDInsight cluster and then run the following `hbase` command:</span><span class="sxs-lookup"><span data-stu-id="bc530-131">To import a table, SSH into the head node of your destination HDInsight cluster and then run the following `hbase` command:</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.Import "<tableName>" "/<path>/<to>/<export>"

<span data-ttu-id="bc530-132">Specify the full export path to the default storage or to any of the attached storage options.</span><span class="sxs-lookup"><span data-stu-id="bc530-132">Specify the full export path to the default storage or to any of the attached storage options.</span></span> <span data-ttu-id="bc530-133">For example, in Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="bc530-133">For example, in Azure Storage:</span></span>

    wasbs://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="bc530-134">In Azure Data Lake Store, the syntax is:</span><span class="sxs-lookup"><span data-stu-id="bc530-134">In Azure Data Lake Store, the syntax is:</span></span>

    adl://<accountName>.azuredatalakestore.net:443/<path>

<span data-ttu-id="bc530-135">This approach offers table-level granularity.</span><span class="sxs-lookup"><span data-stu-id="bc530-135">This approach offers table-level granularity.</span></span> <span data-ttu-id="bc530-136">You can also specify a date range for the rows to include, which allows you to perform the process incrementally.</span><span class="sxs-lookup"><span data-stu-id="bc530-136">You can also specify a date range for the rows to include, which allows you to perform the process incrementally.</span></span> <span data-ttu-id="bc530-137">Each date is in milliseconds since the Unix epoch.</span><span class="sxs-lookup"><span data-stu-id="bc530-137">Each date is in milliseconds since the Unix epoch.</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.Export "<tableName>" "/<path>/<to>/<export>" <numberOfVersions> <startTimeInMS> <endTimeInMS>

<span data-ttu-id="bc530-138">Note that you have to specify the number of versions of each row to export.</span><span class="sxs-lookup"><span data-stu-id="bc530-138">Note that you have to specify the number of versions of each row to export.</span></span> <span data-ttu-id="bc530-139">To include all versions in the date range, set `<numberOfVersions>` to a value greater than your maximum possible row versions, such as 100000.</span><span class="sxs-lookup"><span data-stu-id="bc530-139">To include all versions in the date range, set `<numberOfVersions>` to a value greater than your maximum possible row versions, such as 100000.</span></span>

## <a name="copy-tables"></a><span data-ttu-id="bc530-140">Copy tables</span><span class="sxs-lookup"><span data-stu-id="bc530-140">Copy tables</span></span>

<span data-ttu-id="bc530-141">The CopyTable utility copies data from a source table, row by row, to an existing destination table with the same schema as the source.</span><span class="sxs-lookup"><span data-stu-id="bc530-141">The CopyTable utility copies data from a source table, row by row, to an existing destination table with the same schema as the source.</span></span> <span data-ttu-id="bc530-142">The destination table can be on the same cluster or a different HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-142">The destination table can be on the same cluster or a different HBase cluster.</span></span>

<span data-ttu-id="bc530-143">To use CopyTable within a cluster, SSH into the head node of your source HDInsight cluster and then run this `hbase` command:</span><span class="sxs-lookup"><span data-stu-id="bc530-143">To use CopyTable within a cluster, SSH into the head node of your source HDInsight cluster and then run this `hbase` command:</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.CopyTable --new.name=<destTableName> <srcTableName>

<span data-ttu-id="bc530-144">To use CopyTable to copy to a table on a different cluster, add the `peer` switch with the destination cluster's address:</span><span class="sxs-lookup"><span data-stu-id="bc530-144">To use CopyTable to copy to a table on a different cluster, add the `peer` switch with the destination cluster's address:</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.CopyTable --new.name=<destTableName> --peer.adr=<destinationAddress> <srcTableName>

<span data-ttu-id="bc530-145">The destination address is composed of the following three parts:</span><span class="sxs-lookup"><span data-stu-id="bc530-145">The destination address is composed of the following three parts:</span></span>

    <destinationAddress> = <ZooKeeperQuorum>:<Port>:<ZnodeParent>

* <span data-ttu-id="bc530-146">`<ZooKeeperQuorum>` is a comma-separated list of ZooKeeper nodes, for example:</span><span class="sxs-lookup"><span data-stu-id="bc530-146">`<ZooKeeperQuorum>` is a comma-separated list of ZooKeeper nodes, for example:</span></span>

    <span data-ttu-id="bc530-147">zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk4-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk3-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="bc530-147">zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk4-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk3-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net</span></span>

* <span data-ttu-id="bc530-148">`<Port>` on HDInsight defaults to 2181, and `<ZnodeParent>` is `/hbase-unsecure`, so the complete `<destinationAddress>` would be:</span><span class="sxs-lookup"><span data-stu-id="bc530-148">`<Port>` on HDInsight defaults to 2181, and `<ZnodeParent>` is `/hbase-unsecure`, so the complete `<destinationAddress>` would be:</span></span>

    <span data-ttu-id="bc530-149">zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk4-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk3-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net:2181:/hbase-unsecure</span><span class="sxs-lookup"><span data-stu-id="bc530-149">zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk4-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk3-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net:2181:/hbase-unsecure</span></span>

<span data-ttu-id="bc530-150">See [Manually Collecting the ZooKeeper Quorum List](#manually-collect-the-zookeeper-quorum-list) in this article for details on how to retrieve these values for your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-150">See [Manually Collecting the ZooKeeper Quorum List](#manually-collect-the-zookeeper-quorum-list) in this article for details on how to retrieve these values for your HDInsight cluster.</span></span>

<span data-ttu-id="bc530-151">The CopyTable utility also supports parameters to specify the time range of rows to copy, and to specify the subset of column families in a table to copy.</span><span class="sxs-lookup"><span data-stu-id="bc530-151">The CopyTable utility also supports parameters to specify the time range of rows to copy, and to specify the subset of column families in a table to copy.</span></span> <span data-ttu-id="bc530-152">To see the complete list of parameters supported by CopyTable, run CopyTable without any parameters:</span><span class="sxs-lookup"><span data-stu-id="bc530-152">To see the complete list of parameters supported by CopyTable, run CopyTable without any parameters:</span></span>

    hbase org.apache.hadoop.hbase.mapreduce.CopyTable

<span data-ttu-id="bc530-153">CopyTable scans the entire source table content that will be copied over to the destination table.</span><span class="sxs-lookup"><span data-stu-id="bc530-153">CopyTable scans the entire source table content that will be copied over to the destination table.</span></span> <span data-ttu-id="bc530-154">This may reduce your HBase cluster's performance while CopyTable executes.</span><span class="sxs-lookup"><span data-stu-id="bc530-154">This may reduce your HBase cluster's performance while CopyTable executes.</span></span>

> [!NOTE]
> <span data-ttu-id="bc530-155">To automate the copying of data between tables, see the `hdi_copy_table.sh` script in the [Azure HBase Utils](https://github.com/Azure/hbase-utils/tree/master/replication) repository on GitHub.</span><span class="sxs-lookup"><span data-stu-id="bc530-155">To automate the copying of data between tables, see the `hdi_copy_table.sh` script in the [Azure HBase Utils](https://github.com/Azure/hbase-utils/tree/master/replication) repository on GitHub.</span></span>

### <a name="manually-collect-the-zookeeper-quorum-list"></a><span data-ttu-id="bc530-156">Manually collect the ZooKeeper quorum List</span><span class="sxs-lookup"><span data-stu-id="bc530-156">Manually collect the ZooKeeper quorum List</span></span>

<span data-ttu-id="bc530-157">When both HDInsight clusters are in the same virtual network, as described previously, internal host name resolution is automatic.</span><span class="sxs-lookup"><span data-stu-id="bc530-157">When both HDInsight clusters are in the same virtual network, as described previously, internal host name resolution is automatic.</span></span> <span data-ttu-id="bc530-158">To use CopyTable for HDInsight clusters in two separate virtual networks connected by a VPN Gateway, you will need to provide the host IP addresses of the Zookeeper nodes in the quorum.</span><span class="sxs-lookup"><span data-stu-id="bc530-158">To use CopyTable for HDInsight clusters in two separate virtual networks connected by a VPN Gateway, you will need to provide the host IP addresses of the Zookeeper nodes in the quorum.</span></span>

<span data-ttu-id="bc530-159">To acquire the quorum host names, run the following curl command:</span><span class="sxs-lookup"><span data-stu-id="bc530-159">To acquire the quorum host names, run the following curl command:</span></span>

    curl -u admin:<password> -X GET -H "X-Requested-By: ambari" "https://<clusterName>.azurehdinsight.net/api/v1/clusters/<clusterName>/configurations?type=hbase-site&tag=TOPOLOGY_RESOLVED" | grep "hbase.zookeeper.quorum"

<span data-ttu-id="bc530-160">The curl command retrieves a JSON document with HBase configuration information, and the grep command returns only the "hbase.zookeeper.quorum" entry, for example:</span><span class="sxs-lookup"><span data-stu-id="bc530-160">The curl command retrieves a JSON document with HBase configuration information, and the grep command returns only the "hbase.zookeeper.quorum" entry, for example:</span></span>

    "hbase.zookeeper.quorum" : "zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk4-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net,zk3-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net"

<span data-ttu-id="bc530-161">The quorum host names value is the entire string to the right of the colon.</span><span class="sxs-lookup"><span data-stu-id="bc530-161">The quorum host names value is the entire string to the right of the colon.</span></span>

<span data-ttu-id="bc530-162">To retrieve the IP addresses for these hosts, use the following curl command for each host in the previous list:</span><span class="sxs-lookup"><span data-stu-id="bc530-162">To retrieve the IP addresses for these hosts, use the following curl command for each host in the previous list:</span></span>

    curl -u admin:<password> -X GET -H "X-Requested-By: ambari" "https://<clusterName>.azurehdinsight.net/api/v1/clusters/<clusterName>/hosts/<zookeeperHostFullName>" | grep "ip"

<span data-ttu-id="bc530-163">In this curl command, `<zookeeperHostFullName>` is the full DNS name of a ZooKeeper host, such as the example `zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net`.</span><span class="sxs-lookup"><span data-stu-id="bc530-163">In this curl command, `<zookeeperHostFullName>` is the full DNS name of a ZooKeeper host, such as the example `zk0-hdizc2.54o2oqawzlwevlfxgay2500xtg.dx.internal.cloudapp.net`.</span></span> <span data-ttu-id="bc530-164">The output of the command contains the IP address for the specified host, for example:</span><span class="sxs-lookup"><span data-stu-id="bc530-164">The output of the command contains the IP address for the specified host, for example:</span></span>

    100    "ip" : "10.0.0.9",

<span data-ttu-id="bc530-165">After you collect the IP addresses for all ZooKeeper nodes in your quorum, rebuild the destination address:</span><span class="sxs-lookup"><span data-stu-id="bc530-165">After you collect the IP addresses for all ZooKeeper nodes in your quorum, rebuild the destination address:</span></span>

    <destinationAddress>  = <Host_1_IP>,<Host_2_IP>,<Host_3_IP>:<Port>:<ZnodeParent>

<span data-ttu-id="bc530-166">In our example:</span><span class="sxs-lookup"><span data-stu-id="bc530-166">In our example:</span></span>

    <destinationAddress> = 10.0.0.9,10.0.0.8,10.0.0.12:2181:/hbase-unsecure

## <a name="snapshots"></a><span data-ttu-id="bc530-167">Snapshots</span><span class="sxs-lookup"><span data-stu-id="bc530-167">Snapshots</span></span>

<span data-ttu-id="bc530-168">Snapshots enable you to take a point-in-time backup of data in your HBase datastore.</span><span class="sxs-lookup"><span data-stu-id="bc530-168">Snapshots enable you to take a point-in-time backup of data in your HBase datastore.</span></span> <span data-ttu-id="bc530-169">Snapshots have minimal overhead and complete within seconds, because a snapshot operation is effectively a metadata operation capturing the names of all files in storage at that instant.</span><span class="sxs-lookup"><span data-stu-id="bc530-169">Snapshots have minimal overhead and complete within seconds, because a snapshot operation is effectively a metadata operation capturing the names of all files in storage at that instant.</span></span> <span data-ttu-id="bc530-170">At the time of a snapshot, no actual data is copied.</span><span class="sxs-lookup"><span data-stu-id="bc530-170">At the time of a snapshot, no actual data is copied.</span></span> <span data-ttu-id="bc530-171">Snapshots rely on the immutable nature of the data stored in HDFS, where updates, deletes, and inserts are all represented as new data.</span><span class="sxs-lookup"><span data-stu-id="bc530-171">Snapshots rely on the immutable nature of the data stored in HDFS, where updates, deletes, and inserts are all represented as new data.</span></span> <span data-ttu-id="bc530-172">You can restore (*clone*) a snapshot on the same cluster, or export a snapshot to another cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-172">You can restore (*clone*) a snapshot on the same cluster, or export a snapshot to another cluster.</span></span>

<span data-ttu-id="bc530-173">To create a snapshot, SSH in to the head node of your HDInsight HBase cluster and start the `hbase` shell:</span><span class="sxs-lookup"><span data-stu-id="bc530-173">To create a snapshot, SSH in to the head node of your HDInsight HBase cluster and start the `hbase` shell:</span></span>

    hbase shell

<span data-ttu-id="bc530-174">Within the hbase shell, use the snapshot command with the names of the table and of this snapshot:</span><span class="sxs-lookup"><span data-stu-id="bc530-174">Within the hbase shell, use the snapshot command with the names of the table and of this snapshot:</span></span>

    snapshot '<tableName>', '<snapshotName>'

<span data-ttu-id="bc530-175">To restore a snapshot by name within the `hbase` shell, first disable the table, then restore the snapshot and re-enable the table:</span><span class="sxs-lookup"><span data-stu-id="bc530-175">To restore a snapshot by name within the `hbase` shell, first disable the table, then restore the snapshot and re-enable the table:</span></span>

    disable '<tableName>'
    restore_snapshot '<snapshotName>'
    enable '<tableName>'

<span data-ttu-id="bc530-176">To restore a snapshot to a new table, use clone_snapshot:</span><span class="sxs-lookup"><span data-stu-id="bc530-176">To restore a snapshot to a new table, use clone_snapshot:</span></span>

    clone_snapshot '<snapshotName>', '<newTableName>'

<span data-ttu-id="bc530-177">To export a snapshot to HDFS for use by another cluster, first create the snapshot as described previously and then use the ExportSnapshot utility.</span><span class="sxs-lookup"><span data-stu-id="bc530-177">To export a snapshot to HDFS for use by another cluster, first create the snapshot as described previously and then use the ExportSnapshot utility.</span></span> <span data-ttu-id="bc530-178">Run this utility from within the SSH session to the head node, not within the `hbase` shell:</span><span class="sxs-lookup"><span data-stu-id="bc530-178">Run this utility from within the SSH session to the head node, not within the `hbase` shell:</span></span>

     hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot <snapshotName> -copy-to <hdfsHBaseLocation>

<span data-ttu-id="bc530-179">The `<hdfsHBaseLocation>` can be any of the storage locations accessible to your source cluster, and should point to the hbase folder used by your destination cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-179">The `<hdfsHBaseLocation>` can be any of the storage locations accessible to your source cluster, and should point to the hbase folder used by your destination cluster.</span></span> <span data-ttu-id="bc530-180">For example, if you have a secondary Azure Storage account attached to your source cluster, and that account provides access to the container used by the default storage of the destination cluster, you could use this command:</span><span class="sxs-lookup"><span data-stu-id="bc530-180">For example, if you have a secondary Azure Storage account attached to your source cluster, and that account provides access to the container used by the default storage of the destination cluster, you could use this command:</span></span>

    hbase org.apache.hadoop.hbase.snapshot.ExportSnapshot -snapshot 'Snapshot1' -copy-to 'wasbs://secondcluster@myaccount.blob.core.windows.net/hbase'

<span data-ttu-id="bc530-181">After the snapshot is exported, SSH into the head node of the destination cluster and restore the snapshot using the restore_snapshot command as previously described.</span><span class="sxs-lookup"><span data-stu-id="bc530-181">After the snapshot is exported, SSH into the head node of the destination cluster and restore the snapshot using the restore_snapshot command as previously described.</span></span>

<span data-ttu-id="bc530-182">Snapshots provide a complete backup of a table at the time of the `snapshot` command.</span><span class="sxs-lookup"><span data-stu-id="bc530-182">Snapshots provide a complete backup of a table at the time of the `snapshot` command.</span></span> <span data-ttu-id="bc530-183">Snapshots do not provide the ability to perform incremental snapshots by windows of time, nor to specify subsets of columns families to include in the snapshot.</span><span class="sxs-lookup"><span data-stu-id="bc530-183">Snapshots do not provide the ability to perform incremental snapshots by windows of time, nor to specify subsets of columns families to include in the snapshot.</span></span>

## <a name="replication"></a><span data-ttu-id="bc530-184">Replication</span><span class="sxs-lookup"><span data-stu-id="bc530-184">Replication</span></span>

<span data-ttu-id="bc530-185">HBase replication automatically pushes transactions from a source cluster to a destination cluster, using an asynchronous mechanism with minimal overhead on the source cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-185">HBase replication automatically pushes transactions from a source cluster to a destination cluster, using an asynchronous mechanism with minimal overhead on the source cluster.</span></span> <span data-ttu-id="bc530-186">In HDInsight, you can set up replication between clusters where:</span><span class="sxs-lookup"><span data-stu-id="bc530-186">In HDInsight, you can set up replication between clusters where:</span></span>

* <span data-ttu-id="bc530-187">The source and destination clusters are in the same virtual network.</span><span class="sxs-lookup"><span data-stu-id="bc530-187">The source and destination clusters are in the same virtual network.</span></span>
* <span data-ttu-id="bc530-188">The source and destinations clusters are in different virtual networks connected by a VPN gateway, but both clusters exist in the same geographic location.</span><span class="sxs-lookup"><span data-stu-id="bc530-188">The source and destinations clusters are in different virtual networks connected by a VPN gateway, but both clusters exist in the same geographic location.</span></span>
* <span data-ttu-id="bc530-189">The source cluster and destinations clusters are in different virtual networks connected by a VPN gateway and each cluster exists in a different geographic location.</span><span class="sxs-lookup"><span data-stu-id="bc530-189">The source cluster and destinations clusters are in different virtual networks connected by a VPN gateway and each cluster exists in a different geographic location.</span></span>

<span data-ttu-id="bc530-190">The general steps to set up replication are:</span><span class="sxs-lookup"><span data-stu-id="bc530-190">The general steps to set up replication are:</span></span>

1. <span data-ttu-id="bc530-191">On the source cluster, create the tables and populate data.</span><span class="sxs-lookup"><span data-stu-id="bc530-191">On the source cluster, create the tables and populate data.</span></span>
2. <span data-ttu-id="bc530-192">On the destination cluster, create empty destination tables with the source table's schema.</span><span class="sxs-lookup"><span data-stu-id="bc530-192">On the destination cluster, create empty destination tables with the source table's schema.</span></span>
3. <span data-ttu-id="bc530-193">Register the destination cluster as a peer to the source cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-193">Register the destination cluster as a peer to the source cluster.</span></span>
4. <span data-ttu-id="bc530-194">Enable replication on the desired source tables.</span><span class="sxs-lookup"><span data-stu-id="bc530-194">Enable replication on the desired source tables.</span></span>
5. <span data-ttu-id="bc530-195">Copy existing data from the source tables to the destination tables.</span><span class="sxs-lookup"><span data-stu-id="bc530-195">Copy existing data from the source tables to the destination tables.</span></span>
6. <span data-ttu-id="bc530-196">Replication automatically copies new data modifications to the source tables into the destination tables.</span><span class="sxs-lookup"><span data-stu-id="bc530-196">Replication automatically copies new data modifications to the source tables into the destination tables.</span></span>

<span data-ttu-id="bc530-197">To enable replication on HDInsight, apply a Script Action to your running source HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bc530-197">To enable replication on HDInsight, apply a Script Action to your running source HDInsight cluster.</span></span> <span data-ttu-id="bc530-198">For a walkthrough of enabling replication in your cluster, or to experiment with replication on sample clusters created in virtual networks using Azure Resource Management templates, see [Configure HBase replication](apache-hbase-replication.md).</span><span class="sxs-lookup"><span data-stu-id="bc530-198">For a walkthrough of enabling replication in your cluster, or to experiment with replication on sample clusters created in virtual networks using Azure Resource Management templates, see [Configure HBase replication](apache-hbase-replication.md).</span></span> <span data-ttu-id="bc530-199">That article also includes instructions for enabling replication of Phoenix metadata.</span><span class="sxs-lookup"><span data-stu-id="bc530-199">That article also includes instructions for enabling replication of Phoenix metadata.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc530-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc530-200">Next steps</span></span>

* [<span data-ttu-id="bc530-201">Configure HBase replication</span><span class="sxs-lookup"><span data-stu-id="bc530-201">Configure HBase replication</span></span>](apache-hbase-replication.md)
