---
title: Scale cluster sizes - Azure HDInsight
description: Scale an HDInsight cluster to your workload.
services: hdinsight
author: ashishthaps
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/02/2018
ms.author: ashish
ms.openlocfilehash: d554cdf5e89898874811ea113985fac4b332fac6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856836"
---
# <a name="scale-hdinsight-clusters"></a><span data-ttu-id="0a0f3-103">Scale HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="0a0f3-103">Scale HDInsight clusters</span></span>

<span data-ttu-id="0a0f3-104">HDInsight provides elasticity by giving you the option to scale up and scale down the number of worker nodes in your clusters.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-104">HDInsight provides elasticity by giving you the option to scale up and scale down the number of worker nodes in your clusters.</span></span> <span data-ttu-id="0a0f3-105">This allows you to shrink a cluster after hours or on weekends, and expand it during peak business demands.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-105">This allows you to shrink a cluster after hours or on weekends, and expand it during peak business demands.</span></span>

<span data-ttu-id="0a0f3-106">For example, if you have some batch processing that happens once a day or once a month, the HDInsight cluster can be scaled up a few minutes prior to that scheduled event so  there will be adequate  memory and CPU compute power.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-106">For example, if you have some batch processing that happens once a day or once a month, the HDInsight cluster can be scaled up a few minutes prior to that scheduled event so  there will be adequate  memory and CPU compute power.</span></span> <span data-ttu-id="0a0f3-107">You can automate scaling with the PowerShell cmdlet [`Set–AzureRmHDInsightClusterSize`](hdinsight-administer-use-powershell.md#scale-clusters).</span><span class="sxs-lookup"><span data-stu-id="0a0f3-107">You can automate scaling with the PowerShell cmdlet [`Set–AzureRmHDInsightClusterSize`](hdinsight-administer-use-powershell.md#scale-clusters).</span></span>  <span data-ttu-id="0a0f3-108">Later, after the processing is done, and usage goes down again, you can scale down the HDInsight cluster to fewer worker nodes.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-108">Later, after the processing is done, and usage goes down again, you can scale down the HDInsight cluster to fewer worker nodes.</span></span>

* <span data-ttu-id="0a0f3-109">To scale your cluster through [PowerShell](hdinsight-administer-use-powershell.md):</span><span class="sxs-lookup"><span data-stu-id="0a0f3-109">To scale your cluster through [PowerShell](hdinsight-administer-use-powershell.md):</span></span>

    ```powershell
    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>
    ```
    
* <span data-ttu-id="0a0f3-110">To scale your cluster through the [Azure CLI](hdinsight-administer-use-command-line.md):</span><span class="sxs-lookup"><span data-stu-id="0a0f3-110">To scale your cluster through the [Azure CLI](hdinsight-administer-use-command-line.md):</span></span>

    ```
    azure hdinsight cluster resize [options] <clusterName> <Target Instance Count>
    ```
    
* <span data-ttu-id="0a0f3-111">To scale your cluster through the [Azure portal](https://portal.azure.com), open your HDInsight cluster pane, select **Scale cluster** on the left-hand menu, then on the Scale cluster pane, type in the number of worker nodes, and select Save.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-111">To scale your cluster through the [Azure portal](https://portal.azure.com), open your HDInsight cluster pane, select **Scale cluster** on the left-hand menu, then on the Scale cluster pane, type in the number of worker nodes, and select Save.</span></span>

    ![Scale cluster](./media/hdinsight-scaling-best-practices/scale-cluster-blade.png)

<span data-ttu-id="0a0f3-113">Using any of these methods, you can scale your HDInsight cluster up or down within minutes.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-113">Using any of these methods, you can scale your HDInsight cluster up or down within minutes.</span></span>

## <a name="scaling-impacts-on-running-jobs"></a><span data-ttu-id="0a0f3-114">Scaling impacts on running jobs</span><span class="sxs-lookup"><span data-stu-id="0a0f3-114">Scaling impacts on running jobs</span></span>

<span data-ttu-id="0a0f3-115">When you **add** nodes to your running HDInsight cluster, any pending or running jobs will not be impacted.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-115">When you **add** nodes to your running HDInsight cluster, any pending or running jobs will not be impacted.</span></span> <span data-ttu-id="0a0f3-116">In addition, new jobs can be safely submitted while the scaling process is running.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-116">In addition, new jobs can be safely submitted while the scaling process is running.</span></span> <span data-ttu-id="0a0f3-117">If the scaling operations fail for any reason, the failure is gracefully handled, leaving the cluster in a functional state.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-117">If the scaling operations fail for any reason, the failure is gracefully handled, leaving the cluster in a functional state.</span></span>

<span data-ttu-id="0a0f3-118">However, if you are scaling down your cluster by **removing** nodes, any pending or running jobs will fail when the scaling operation completes.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-118">However, if you are scaling down your cluster by **removing** nodes, any pending or running jobs will fail when the scaling operation completes.</span></span> <span data-ttu-id="0a0f3-119">This failure is due to some of the services restarting during the process.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-119">This failure is due to some of the services restarting during the process.</span></span>

<span data-ttu-id="0a0f3-120">To address this issue, you can wait for the jobs to complete before scaling down your cluster, manually terminate the jobs, or  resubmit the jobs after the scaling operation has concluded.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-120">To address this issue, you can wait for the jobs to complete before scaling down your cluster, manually terminate the jobs, or  resubmit the jobs after the scaling operation has concluded.</span></span>

<span data-ttu-id="0a0f3-121">To see a list of pending and running jobs, you can use the YARN ResourceManager UI, following these steps:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-121">To see a list of pending and running jobs, you can use the YARN ResourceManager UI, following these steps:</span></span>

1. <span data-ttu-id="0a0f3-122">Sign in to [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0a0f3-122">Sign in to [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0a0f3-123">On the left menu, select **Browse**, select **HDInsight Clusters**, and then select your cluster.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-123">On the left menu, select **Browse**, select **HDInsight Clusters**, and then select your cluster.</span></span>
3. <span data-ttu-id="0a0f3-124">From your HDInsight cluster pane, select **Dashboard** on the top menu to open the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-124">From your HDInsight cluster pane, select **Dashboard** on the top menu to open the Ambari UI.</span></span> <span data-ttu-id="0a0f3-125">Enter your cluster login credentials.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-125">Enter your cluster login credentials.</span></span>
4. <span data-ttu-id="0a0f3-126">Click **YARN** on the list of services on the left-hand menu.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-126">Click **YARN** on the list of services on the left-hand menu.</span></span> <span data-ttu-id="0a0f3-127">On the YARN page, select **Quick Links** and hover over the active head node, then click **ResourceManager UI**.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-127">On the YARN page, select **Quick Links** and hover over the active head node, then click **ResourceManager UI**.</span></span>

    ![ResourceManager UI](./media/hdinsight-scaling-best-practices/resourcemanager-ui.png)

<span data-ttu-id="0a0f3-129">You may directly access the ResourceManager UI with `https://<HDInsightClusterName>.azurehdinsight.net/yarnui/hn/cluster`.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-129">You may directly access the ResourceManager UI with `https://<HDInsightClusterName>.azurehdinsight.net/yarnui/hn/cluster`.</span></span>

<span data-ttu-id="0a0f3-130">You  see a list of jobs, along with their current state.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-130">You  see a list of jobs, along with their current state.</span></span> <span data-ttu-id="0a0f3-131">In the screenshot, there is  one job currently running:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-131">In the screenshot, there is  one job currently running:</span></span>

![ResourceManager UI applications](./media/hdinsight-scaling-best-practices/resourcemanager-ui-applications.png)

<span data-ttu-id="0a0f3-133">To  manually kill that running application, execute the following command from the SSH shell:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-133">To  manually kill that running application, execute the following command from the SSH shell:</span></span>

```bash
yarn application -kill <application_id>
```

<span data-ttu-id="0a0f3-134">For example:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-134">For example:</span></span>

```bash
yarn application -kill "application_1499348398273_0003"
```

## <a name="rebalancing-an-hbase-cluster"></a><span data-ttu-id="0a0f3-135">Rebalancing an HBase cluster</span><span class="sxs-lookup"><span data-stu-id="0a0f3-135">Rebalancing an HBase cluster</span></span>

<span data-ttu-id="0a0f3-136">Region servers are automatically balanced within a few minutes after completion of the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-136">Region servers are automatically balanced within a few minutes after completion of the scaling operation.</span></span> <span data-ttu-id="0a0f3-137">To manually balance region servers, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-137">To manually balance region servers, use the following steps:</span></span>

1. <span data-ttu-id="0a0f3-138">Connect to the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-138">Connect to the HDInsight cluster using SSH.</span></span> <span data-ttu-id="0a0f3-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0a0f3-139">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0a0f3-140">Start the HBase shell:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-140">Start the HBase shell:</span></span>

        hbase shell

3. <span data-ttu-id="0a0f3-141">Use the following command to manually balance the region servers:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-141">Use the following command to manually balance the region servers:</span></span>

        balancer

## <a name="scale-down-implications"></a><span data-ttu-id="0a0f3-142">Scale down implications</span><span class="sxs-lookup"><span data-stu-id="0a0f3-142">Scale down implications</span></span>

<span data-ttu-id="0a0f3-143">As mentioned previously, any pending or running jobs are terminated at the completion of a scaling down operation.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-143">As mentioned previously, any pending or running jobs are terminated at the completion of a scaling down operation.</span></span> <span data-ttu-id="0a0f3-144">However, there are other potential implications to scaling down that may occur.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-144">However, there are other potential implications to scaling down that may occur.</span></span>

## <a name="hdinsight-name-node-stays-in-safe-mode-after-scaling-down"></a><span data-ttu-id="0a0f3-145">HDInsight name node stays in safe mode after scaling down</span><span class="sxs-lookup"><span data-stu-id="0a0f3-145">HDInsight name node stays in safe mode after scaling down</span></span>

![Scale cluster](./media/hdinsight-scaling-best-practices/scale-cluster.png)

<span data-ttu-id="0a0f3-147">If you shrink your cluster down to the minimum of one worker node, as shown in the previous image,  HDFS may become stuck in safe mode when worker nodes are rebooted due to patching, or immediately after the scaling operation.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-147">If you shrink your cluster down to the minimum of one worker node, as shown in the previous image,  HDFS may become stuck in safe mode when worker nodes are rebooted due to patching, or immediately after the scaling operation.</span></span>

<span data-ttu-id="0a0f3-148">The primary cause of this is that Hive uses a few `scratchdir` files, and by default expects three replicas of each block, but there is only one replica possible if you scale down to the minimum one worker node.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-148">The primary cause of this is that Hive uses a few `scratchdir` files, and by default expects three replicas of each block, but there is only one replica possible if you scale down to the minimum one worker node.</span></span> <span data-ttu-id="0a0f3-149">As a consequence, the files in the `scratchdir` become *under-replicated*.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-149">As a consequence, the files in the `scratchdir` become *under-replicated*.</span></span> <span data-ttu-id="0a0f3-150">This could cause HDFS to stay in safe mode when the services are restarted after the scale operation.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-150">This could cause HDFS to stay in safe mode when the services are restarted after the scale operation.</span></span>

<span data-ttu-id="0a0f3-151">When a scale down attempt happens, HDInsight relies upon the Ambari management interfaces to first decommission the extra unwanted worker nodes, which replicates their HDFS blocks to other online worker nodes, and then safely scale the cluster down.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-151">When a scale down attempt happens, HDInsight relies upon the Ambari management interfaces to first decommission the extra unwanted worker nodes, which replicates their HDFS blocks to other online worker nodes, and then safely scale the cluster down.</span></span> <span data-ttu-id="0a0f3-152">HDFS goes into a safe mode during the maintenance window, and is supposed to come out once the scaling is finished.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-152">HDFS goes into a safe mode during the maintenance window, and is supposed to come out once the scaling is finished.</span></span> <span data-ttu-id="0a0f3-153">It is at this point that HDFS can become stuck in safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-153">It is at this point that HDFS can become stuck in safe mode.</span></span>

<span data-ttu-id="0a0f3-154">HDFS is configured with a `dfs.replication` setting of 3.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-154">HDFS is configured with a `dfs.replication` setting of 3.</span></span> <span data-ttu-id="0a0f3-155">Thus, the blocks of the scratch files are under-replicated whenever there are fewer than three worker nodes online, because there are not the expected three copies of each file block available.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-155">Thus, the blocks of the scratch files are under-replicated whenever there are fewer than three worker nodes online, because there are not the expected three copies of each file block available.</span></span>

<span data-ttu-id="0a0f3-156">You can execute a command  to bring HDFS out of safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-156">You can execute a command  to bring HDFS out of safe mode.</span></span> <span data-ttu-id="0a0f3-157">For example, if you know that the only reason safe mode is on is because the temporary files are under-replicated, then you can safely leave safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-157">For example, if you know that the only reason safe mode is on is because the temporary files are under-replicated, then you can safely leave safe mode.</span></span> <span data-ttu-id="0a0f3-158">This is  because the under-replicated files are Hive temporary scratch files.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-158">This is  because the under-replicated files are Hive temporary scratch files.</span></span>

```bash
hdfs dfsadmin -D 'fs.default.name=hdfs://mycluster/' -safemode leave
```

<span data-ttu-id="0a0f3-159">After leaving safe mode, you can manually remove the  temporary files, or wait for Hive to eventually clean them up automatically.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-159">After leaving safe mode, you can manually remove the  temporary files, or wait for Hive to eventually clean them up automatically.</span></span>

### <a name="example-errors-when-safe-mode-is-turned-on"></a><span data-ttu-id="0a0f3-160">Example errors when safe mode is turned on</span><span class="sxs-lookup"><span data-stu-id="0a0f3-160">Example errors when safe mode is turned on</span></span>

* <span data-ttu-id="0a0f3-161">H070 Unable to open Hive session.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-161">H070 Unable to open Hive session.</span></span> <span data-ttu-id="0a0f3-162">org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.RetriableException): org.apache.hadoop.hdfs.server.namenode.SafeModeException: **Cannot create directory** /tmp/hive/hive/819c215c-6d87-4311-97c8-4f0b9d2adcf0.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-162">org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.RetriableException): org.apache.hadoop.hdfs.server.namenode.SafeModeException: **Cannot create directory** /tmp/hive/hive/819c215c-6d87-4311-97c8-4f0b9d2adcf0.</span></span> <span data-ttu-id="0a0f3-163">**Name node is in safe mode**.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-163">**Name node is in safe mode**.</span></span> <span data-ttu-id="0a0f3-164">The reported blocks 75 needs additional 12 blocks to reach the threshold 0.9900 of total blocks 87.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-164">The reported blocks 75 needs additional 12 blocks to reach the threshold 0.9900 of total blocks 87.</span></span> <span data-ttu-id="0a0f3-165">The number of live datanodes 10 has reached the minimum number 0.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-165">The number of live datanodes 10 has reached the minimum number 0.</span></span> <span data-ttu-id="0a0f3-166">Safe mode will be turned off automatically once the thresholds have been reached.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-166">Safe mode will be turned off automatically once the thresholds have been reached.</span></span>

* <span data-ttu-id="0a0f3-167">H100 Unable to submit statement show databases: org.apache.thrift.transport.TTransportException: org.apache.http.conn.HttpHostConnectException: Connect to hn0-clustername.servername.internal.cloudapp.net:10001 [hn0-clustername.servername.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-167">H100 Unable to submit statement show databases: org.apache.thrift.transport.TTransportException: org.apache.http.conn.HttpHostConnectException: Connect to hn0-clustername.servername.internal.cloudapp.net:10001 [hn0-clustername.servername.</span></span> <span data-ttu-id="0a0f3-168">internal.cloudapp.net/1.1.1.1] failed: **Connection refused**</span><span class="sxs-lookup"><span data-stu-id="0a0f3-168">internal.cloudapp.net/1.1.1.1] failed: **Connection refused**</span></span>

* <span data-ttu-id="0a0f3-169">H020 Could not establish connection to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001: org.apache.thrift.transport.TTransportException: Could not create http connection to http://hn0-hdisrv.servername.bx.internal.cloudapp.net:10001/.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-169">H020 Could not establish connection to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001: org.apache.thrift.transport.TTransportException: Could not create http connection to http://hn0-hdisrv.servername.bx.internal.cloudapp.net:10001/.</span></span> <span data-ttu-id="0a0f3-170">org.apache.http.conn.HttpHostConnectException: Connect to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001 [hn0-hdisrv.servername.bx.internal.cloudapp.net/10.0.0.28] failed: Connection refused: org.apache.thrift.transport.TTransportException: Could not create http connection to http://hn0-hdisrv.servername.bx.internal.cloudapp.net:10001/.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-170">org.apache.http.conn.HttpHostConnectException: Connect to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001 [hn0-hdisrv.servername.bx.internal.cloudapp.net/10.0.0.28] failed: Connection refused: org.apache.thrift.transport.TTransportException: Could not create http connection to http://hn0-hdisrv.servername.bx.internal.cloudapp.net:10001/.</span></span> <span data-ttu-id="0a0f3-171">org.apache.http.conn.HttpHostConnectException: Connect to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001 [hn0-hdisrv.servername.bx.internal.cloudapp.net/10.0.0.28] failed: **Connection refused**</span><span class="sxs-lookup"><span data-stu-id="0a0f3-171">org.apache.http.conn.HttpHostConnectException: Connect to hn0-hdisrv.servername.bx.internal.cloudapp.net:10001 [hn0-hdisrv.servername.bx.internal.cloudapp.net/10.0.0.28] failed: **Connection refused**</span></span>

* <span data-ttu-id="0a0f3-172">From the Hive logs: WARN [main]: server.HiveServer2 (HiveServer2.java:startHiveServer2(442)) – Error starting HiveServer2 on attempt 21, will retry in 60 seconds java.lang.RuntimeException: Error applying authorization policy on hive configuration: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.RetriableException): org.apache.hadoop.hdfs.server.namenode.SafeModeException: **Cannot create directory** /tmp/hive/hive/70a42b8a-9437-466e-acbe-da90b1614374.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-172">From the Hive logs: WARN [main]: server.HiveServer2 (HiveServer2.java:startHiveServer2(442)) – Error starting HiveServer2 on attempt 21, will retry in 60 seconds java.lang.RuntimeException: Error applying authorization policy on hive configuration: org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.ipc.RetriableException): org.apache.hadoop.hdfs.server.namenode.SafeModeException: **Cannot create directory** /tmp/hive/hive/70a42b8a-9437-466e-acbe-da90b1614374.</span></span> <span data-ttu-id="0a0f3-173">**Name node is in safe mode**.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-173">**Name node is in safe mode**.</span></span>
    <span data-ttu-id="0a0f3-174">The reported blocks 0 needs additional 9 blocks to reach the threshold 0.9900 of total blocks 9.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-174">The reported blocks 0 needs additional 9 blocks to reach the threshold 0.9900 of total blocks 9.</span></span>
    <span data-ttu-id="0a0f3-175">The number of live datanodes 10 has reached the minimum number 0.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-175">The number of live datanodes 10 has reached the minimum number 0.</span></span> <span data-ttu-id="0a0f3-176">**Safe mode will be turned off automatically once the thresholds have been reached**.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-176">**Safe mode will be turned off automatically once the thresholds have been reached**.</span></span>
    <span data-ttu-id="0a0f3-177">at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1324)</span><span class="sxs-lookup"><span data-stu-id="0a0f3-177">at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1324)</span></span>

<span data-ttu-id="0a0f3-178">You can review the name node logs from the `/var/log/hadoop/hdfs/` folder, near the time when the cluster was scaled, to see when it entered safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-178">You can review the name node logs from the `/var/log/hadoop/hdfs/` folder, near the time when the cluster was scaled, to see when it entered safe mode.</span></span> <span data-ttu-id="0a0f3-179">The log files are named `Hadoop-hdfs-namenode-hn0-clustername.*`.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-179">The log files are named `Hadoop-hdfs-namenode-hn0-clustername.*`.</span></span>

<span data-ttu-id="0a0f3-180">The root cause of the previous errors is that Hive depends on temporary files in HDFS while running queries.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-180">The root cause of the previous errors is that Hive depends on temporary files in HDFS while running queries.</span></span> <span data-ttu-id="0a0f3-181">When HDFS enters safe mode, Hive cannot run queries because it cannot write to HDFS.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-181">When HDFS enters safe mode, Hive cannot run queries because it cannot write to HDFS.</span></span> <span data-ttu-id="0a0f3-182">The temp files in HDFS are located in the local drive mounted to the individual worker node VMs, and replicated amongst other worker nodes at three replicas, minimum.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-182">The temp files in HDFS are located in the local drive mounted to the individual worker node VMs, and replicated amongst other worker nodes at three replicas, minimum.</span></span>

<span data-ttu-id="0a0f3-183">The `hive.exec.scratchdir` parameter in Hive is configured within `/etc/hive/conf/hive-site.xml`:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-183">The `hive.exec.scratchdir` parameter in Hive is configured within `/etc/hive/conf/hive-site.xml`:</span></span>

```xml
<property>
    <name>hive.exec.scratchdir</name>
    <value>hdfs://mycluster/tmp/hive</value>
</property>
```

### <a name="view-the-health-and-state-of-your-hdfs-file-system"></a><span data-ttu-id="0a0f3-184">View the health and state of your HDFS file system</span><span class="sxs-lookup"><span data-stu-id="0a0f3-184">View the health and state of your HDFS file system</span></span>

<span data-ttu-id="0a0f3-185">You can view a status report from each name node to see whether nodes are in safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-185">You can view a status report from each name node to see whether nodes are in safe mode.</span></span> <span data-ttu-id="0a0f3-186">To view the report, SSH into each head node and run the following command:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-186">To view the report, SSH into each head node and run the following command:</span></span>

```
hdfs dfsadmin -D 'fs.default.name=hdfs://mycluster/' -safemode get
```

![Safe mode off](./media/hdinsight-scaling-best-practices/safe-mode-off.png)

> [!NOTE]
> <span data-ttu-id="0a0f3-188">The `-D` switch is necessary because the default file system in HDInsight is either Azure Storage or Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-188">The `-D` switch is necessary because the default file system in HDInsight is either Azure Storage or Azure Data Lake Store.</span></span> <span data-ttu-id="0a0f3-189">`-D` specifies that the commands execute against the local HDFS file system.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-189">`-D` specifies that the commands execute against the local HDFS file system.</span></span>

<span data-ttu-id="0a0f3-190">Next, you can view a report that shows the details of the HDFS state:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-190">Next, you can view a report that shows the details of the HDFS state:</span></span>

```
hdfs dfsadmin -D 'fs.default.name=hdfs://mycluster/' -report
```

<span data-ttu-id="0a0f3-191">This command results in the following on a healthy cluster where all blocks are replicated to the expected degree:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-191">This command results in the following on a healthy cluster where all blocks are replicated to the expected degree:</span></span>

![Safe mode off](./media/hdinsight-scaling-best-practices/report.png)

<span data-ttu-id="0a0f3-193">HDFS supports the `fsck` command to check for  inconsistencies with various files, such as missing blocks for a file or under-replicated blocks.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-193">HDFS supports the `fsck` command to check for  inconsistencies with various files, such as missing blocks for a file or under-replicated blocks.</span></span> <span data-ttu-id="0a0f3-194">To run the `fsck` command against the `scratchdir` (temporary scratch disk) files:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-194">To run the `fsck` command against the `scratchdir` (temporary scratch disk) files:</span></span>

```
hdfs fsck -D 'fs.default.name=hdfs://mycluster/' /tmp/hive/hive
```

<span data-ttu-id="0a0f3-195">When executed on a healthy HDFS file system with no under-replicated blocks, you see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-195">When executed on a healthy HDFS file system with no under-replicated blocks, you see an output similar to the following:</span></span>

```
Connecting to namenode via http://hn0-scalin.name.bx.internal.cloudapp.net:30070/fsck?ugi=sshuser&path=%2Ftmp%2Fhive%2Fhive
FSCK started by sshuser (auth:SIMPLE) from /10.0.0.21 for path /tmp/hive/hive at Thu Jul 06 20:07:01 UTC 2017
..Status: HEALTHY
 Total size:    53 B
 Total dirs:    5
 Total files:   2
 Total symlinks:                0 (Files currently being written: 2)
 Total blocks (validated):      2 (avg. block size 26 B)
 Minimally replicated blocks:   2 (100.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       0 (0.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     3.0
 Corrupt blocks:                0
 Missing replicas:              0 (0.0 %)
 Number of data-nodes:          4
 Number of racks:               1
FSCK ended at Thu Jul 06 20:07:01 UTC 2017 in 3 milliseconds


The filesystem under path '/tmp/hive/hive' is HEALTHY
```

<span data-ttu-id="0a0f3-196">In contrast, when the `fsck` command is executed on an HDFS file system with some under-replicated blocks, the output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-196">In contrast, when the `fsck` command is executed on an HDFS file system with some under-replicated blocks, the output is similar to the following:</span></span>

```
Connecting to namenode via http://hn0-scalin.name.bx.internal.cloudapp.net:30070/fsck?ugi=sshuser&path=%2Ftmp%2Fhive%2Fhive
FSCK started by sshuser (auth:SIMPLE) from /10.0.0.21 for path /tmp/hive/hive at Thu Jul 06 20:13:58 UTC 2017
.
/tmp/hive/hive/4f3f4253-e6d0-42ac-88bc-90f0ea03602c/inuse.info:  Under replicated BP-1867508080-10.0.0.21-1499348422953:blk_1073741826_1002. Target Replicas is 3 but found 1 live replica(s), 0 decommissioned replica(s) and 0 decommissioning replica(s).
.
/tmp/hive/hive/e7c03964-ff3a-4ee1-aa3c-90637a1f4591/inuse.info: CORRUPT blockpool BP-1867508080-10.0.0.21-1499348422953 block blk_1073741825

/tmp/hive/hive/e7c03964-ff3a-4ee1-aa3c-90637a1f4591/inuse.info: MISSING 1 blocks of total size 26 B.Status: CORRUPT
 Total size:    53 B
 Total dirs:    5
 Total files:   2
 Total symlinks:                0 (Files currently being written: 2)
 Total blocks (validated):      2 (avg. block size 26 B)
  ********************************
  UNDER MIN REPL'D BLOCKS:      1 (50.0 %)
  dfs.namenode.replication.min: 1
  CORRUPT FILES:        1
  MISSING BLOCKS:       1
  MISSING SIZE:         26 B
  CORRUPT BLOCKS:       1
  ********************************
 Minimally replicated blocks:   1 (50.0 %)
 Over-replicated blocks:        0 (0.0 %)
 Under-replicated blocks:       1 (50.0 %)
 Mis-replicated blocks:         0 (0.0 %)
 Default replication factor:    3
 Average block replication:     0.5
 Corrupt blocks:                1
 Missing replicas:              2 (33.333332 %)
 Number of data-nodes:          1
 Number of racks:               1
FSCK ended at Thu Jul 06 20:13:58 UTC 2017 in 28 milliseconds


The filesystem under path '/tmp/hive/hive' is CORRUPT
```

<span data-ttu-id="0a0f3-197">You can also view the HDFS status in Ambari UI by selecting the **HDFS** service on the left, or with  `https://<HDInsightClusterName>.azurehdinsight.net/#/main/services/HDFS/summary`.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-197">You can also view the HDFS status in Ambari UI by selecting the **HDFS** service on the left, or with  `https://<HDInsightClusterName>.azurehdinsight.net/#/main/services/HDFS/summary`.</span></span>

![Ambari HDFS status](./media/hdinsight-scaling-best-practices/ambari-hdfs.png)

<span data-ttu-id="0a0f3-199">You may also see one or more critical errors on the active or standby NameNodes.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-199">You may also see one or more critical errors on the active or standby NameNodes.</span></span> <span data-ttu-id="0a0f3-200">To view the NameNode Blocks Health, select the NameNode link next to the alert.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-200">To view the NameNode Blocks Health, select the NameNode link next to the alert.</span></span>

![NameNode Blocks Health](./media/hdinsight-scaling-best-practices/ambari-hdfs-crit.png)

<span data-ttu-id="0a0f3-202">To clean up the scratch files, which removes the block replication errors, SSH into each head node and run the following command:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-202">To clean up the scratch files, which removes the block replication errors, SSH into each head node and run the following command:</span></span>

```
hadoop fs -rm -r -skipTrash hdfs://mycluster/tmp/hive/
```

> [!NOTE]
> <span data-ttu-id="0a0f3-203">This command can break Hive if some jobs are still running.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-203">This command can break Hive if some jobs are still running.</span></span>

### <a name="how-to-prevent-hdinsight-from-getting-stuck-in-safe-mode-due-to-under-replicated-blocks"></a><span data-ttu-id="0a0f3-204">How to prevent HDInsight from getting stuck in safe mode due to under-replicated blocks</span><span class="sxs-lookup"><span data-stu-id="0a0f3-204">How to prevent HDInsight from getting stuck in safe mode due to under-replicated blocks</span></span>

<span data-ttu-id="0a0f3-205">There are several ways to prevent HDInsight from being left in safe mode:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-205">There are several ways to prevent HDInsight from being left in safe mode:</span></span>

* <span data-ttu-id="0a0f3-206">Stop all Hive jobs before scaling down HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-206">Stop all Hive jobs before scaling down HDInsight.</span></span> <span data-ttu-id="0a0f3-207">Alternately, schedule the scale down process to avoid conflicting with running Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-207">Alternately, schedule the scale down process to avoid conflicting with running Hive jobs.</span></span>
* <span data-ttu-id="0a0f3-208">Manually clean up Hive's scratch `tmp` directory files in HDFS before scaling down.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-208">Manually clean up Hive's scratch `tmp` directory files in HDFS before scaling down.</span></span>
* <span data-ttu-id="0a0f3-209">Only scale down HDInsight to three worker nodes, minimum.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-209">Only scale down HDInsight to three worker nodes, minimum.</span></span> <span data-ttu-id="0a0f3-210">Avoid going as low as one worker node.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-210">Avoid going as low as one worker node.</span></span>
* <span data-ttu-id="0a0f3-211">Run the command to leave safe mode, if needed.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-211">Run the command to leave safe mode, if needed.</span></span>

<span data-ttu-id="0a0f3-212">The following sections describe these options.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-212">The following sections describe these options.</span></span>

#### <a name="stop-all-hive-jobs"></a><span data-ttu-id="0a0f3-213">Stop all Hive jobs</span><span class="sxs-lookup"><span data-stu-id="0a0f3-213">Stop all Hive jobs</span></span>

<span data-ttu-id="0a0f3-214">Stop all Hive jobs before scaling down to one worker node.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-214">Stop all Hive jobs before scaling down to one worker node.</span></span> <span data-ttu-id="0a0f3-215">If  your workload is scheduled, then execute your scale-down after Hive work is done.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-215">If  your workload is scheduled, then execute your scale-down after Hive work is done.</span></span>

<span data-ttu-id="0a0f3-216">This helps minimize the number of scratch files in the tmp folder (if any).</span><span class="sxs-lookup"><span data-stu-id="0a0f3-216">This helps minimize the number of scratch files in the tmp folder (if any).</span></span>

#### <a name="manually-clean-up-hives-scratch-files"></a><span data-ttu-id="0a0f3-217">Manually clean up Hive's scratch files</span><span class="sxs-lookup"><span data-stu-id="0a0f3-217">Manually clean up Hive's scratch files</span></span>

<span data-ttu-id="0a0f3-218">If Hive has left behind temporary files, then you can manually clean up those files before scaling down to avoid safe mode.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-218">If Hive has left behind temporary files, then you can manually clean up those files before scaling down to avoid safe mode.</span></span>

1. <span data-ttu-id="0a0f3-219">Stop Hive services and be sure all queries and jobs are completed.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-219">Stop Hive services and be sure all queries and jobs are completed.</span></span>

2. <span data-ttu-id="0a0f3-220">List the contents of the `hdfs://mycluster/tmp/hive/` directory to see if it contains any files:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-220">List the contents of the `hdfs://mycluster/tmp/hive/` directory to see if it contains any files:</span></span>

    ```
    hadoop fs -ls -R hdfs://mycluster/tmp/hive/hive
    ```
    
    <span data-ttu-id="0a0f3-221">Here is a sample output when files exist:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-221">Here is a sample output when files exist:</span></span>

    ```
    sshuser@hn0-scalin:~$ hadoop fs -ls -R hdfs://mycluster/tmp/hive/hive
    drwx------   - hive hdfs          0 2017-07-06 13:40 hdfs://mycluster/tmp/hive/hive/4f3f4253-e6d0-42ac-88bc-90f0ea03602c
    drwx------   - hive hdfs          0 2017-07-06 13:40 hdfs://mycluster/tmp/hive/hive/4f3f4253-e6d0-42ac-88bc-90f0ea03602c/_tmp_space.db
    -rw-r--r--   3 hive hdfs         27 2017-07-06 13:40 hdfs://mycluster/tmp/hive/hive/4f3f4253-e6d0-42ac-88bc-90f0ea03602c/inuse.info
    -rw-r--r--   3 hive hdfs          0 2017-07-06 13:40 hdfs://mycluster/tmp/hive/hive/4f3f4253-e6d0-42ac-88bc-90f0ea03602c/inuse.lck
    drwx------   - hive hdfs          0 2017-07-06 20:30 hdfs://mycluster/tmp/hive/hive/c108f1c2-453e-400f-ac3e-e3a9b0d22699
    -rw-r--r--   3 hive hdfs         26 2017-07-06 20:30 hdfs://mycluster/tmp/hive/hive/c108f1c2-453e-400f-ac3e-e3a9b0d22699/inuse.info
    ```

3. <span data-ttu-id="0a0f3-222">If you know Hive is done with these files, you can remove them.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-222">If you know Hive is done with these files, you can remove them.</span></span> <span data-ttu-id="0a0f3-223">Be sure that Hive does not have any queries running by looking in the Yarn ResourceManager UI page.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-223">Be sure that Hive does not have any queries running by looking in the Yarn ResourceManager UI page.</span></span>

    <span data-ttu-id="0a0f3-224">Example command line to remove files from HDFS:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-224">Example command line to remove files from HDFS:</span></span>

    ```
    hadoop fs -rm -r -skipTrash hdfs://mycluster/tmp/hive/
    ```
    
#### <a name="scale--hdinsight-to-three-worker-nodes"></a><span data-ttu-id="0a0f3-225">Scale  HDInsight to three worker nodes</span><span class="sxs-lookup"><span data-stu-id="0a0f3-225">Scale  HDInsight to three worker nodes</span></span>

<span data-ttu-id="0a0f3-226">If getting stuck in safe mode is a persistent problem, and the previous steps are not options, then you may want to avoid the problem by only scaling down to three worker nodes.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-226">If getting stuck in safe mode is a persistent problem, and the previous steps are not options, then you may want to avoid the problem by only scaling down to three worker nodes.</span></span> <span data-ttu-id="0a0f3-227">This may not be optimal, due to cost constraints, compared to scaling down to one node.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-227">This may not be optimal, due to cost constraints, compared to scaling down to one node.</span></span> <span data-ttu-id="0a0f3-228">However, with only one worker node, HDFS cannot guarantee three replicas of the data are available to the cluster.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-228">However, with only one worker node, HDFS cannot guarantee three replicas of the data are available to the cluster.</span></span>

#### <a name="run-the-command-to-leave-safe-mode"></a><span data-ttu-id="0a0f3-229">Run the command to leave safe mode</span><span class="sxs-lookup"><span data-stu-id="0a0f3-229">Run the command to leave safe mode</span></span>

<span data-ttu-id="0a0f3-230">The final option is to watch for the rare occasion in which HDFS enters safe mode, then execute the leave safe mode command.</span><span class="sxs-lookup"><span data-stu-id="0a0f3-230">The final option is to watch for the rare occasion in which HDFS enters safe mode, then execute the leave safe mode command.</span></span> <span data-ttu-id="0a0f3-231">Once you have determined that the reason HDFS has entered safe mode is due to the Hive files being under-replicated, execute the following command to leave safe mode:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-231">Once you have determined that the reason HDFS has entered safe mode is due to the Hive files being under-replicated, execute the following command to leave safe mode:</span></span>

* <span data-ttu-id="0a0f3-232">HDInsight on Linux:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-232">HDInsight on Linux:</span></span>

    ```bash
    hdfs dfsadmin -D 'fs.default.name=hdfs://mycluster/' -safemode leave
    ```
    
* <span data-ttu-id="0a0f3-233">HDInsight on Windows:</span><span class="sxs-lookup"><span data-stu-id="0a0f3-233">HDInsight on Windows:</span></span>

    ```bash
    hdfs dfsadmin -fs hdfs://headnodehost:9000 -safemode leave
    ```
    
## <a name="next-steps"></a><span data-ttu-id="0a0f3-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="0a0f3-234">Next steps</span></span>

* [<span data-ttu-id="0a0f3-235">Introduction to Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="0a0f3-235">Introduction to Azure HDInsight</span></span>](hadoop/apache-hadoop-introduction.md)
* [<span data-ttu-id="0a0f3-236">Scale clusters</span><span class="sxs-lookup"><span data-stu-id="0a0f3-236">Scale clusters</span></span>](hdinsight-administer-use-portal-linux.md#scale-clusters)
* [<span data-ttu-id="0a0f3-237">Manage HDInsight clusters by using the Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="0a0f3-237">Manage HDInsight clusters by using the Ambari Web UI</span></span>](hdinsight-hadoop-manage-ambari.md)
