---
title: Troubleshoot HBase by using Azure HDInsight
description: Get answers to common questions about working with HBase and Azure HDInsight.
services: hdinsight
ms.service: hdinsight
author: nitinver
ms.author: nitinver
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 7/7/2017
ms.openlocfilehash: f79c4e330703eb5711c4081f7377d01977b63e5a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869771"
---
# <a name="troubleshoot-hbase-by-using-azure-hdinsight"></a><span data-ttu-id="bbd55-103">Troubleshoot HBase by using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd55-103">Troubleshoot HBase by using Azure HDInsight</span></span>

<span data-ttu-id="bbd55-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="bbd55-104">Learn about the top issues and their resolutions when working with Apache HBase payloads in Apache Ambari.</span></span>

## <a name="how-do-i-run-hbck-command-reports-with-multiple-unassigned-regions"></a><span data-ttu-id="bbd55-105">How do I run hbck command reports with multiple unassigned regions?</span><span class="sxs-lookup"><span data-stu-id="bbd55-105">How do I run hbck command reports with multiple unassigned regions?</span></span>

<span data-ttu-id="bbd55-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span><span class="sxs-lookup"><span data-stu-id="bbd55-106">A common error message that you might see when you run the `hbase hbck` command is "multiple regions being unassigned or holes in the chain of regions."</span></span>

<span data-ttu-id="bbd55-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span><span class="sxs-lookup"><span data-stu-id="bbd55-107">In the HBase Master UI, you can see the number of regions that are unbalanced across all region servers.</span></span> <span data-ttu-id="bbd55-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span><span class="sxs-lookup"><span data-stu-id="bbd55-108">Then, you can run `hbase hbck` command to see holes in the region chain.</span></span>

<span data-ttu-id="bbd55-109">Holes might be caused by the offline regions, so fix the assignments first.</span><span class="sxs-lookup"><span data-stu-id="bbd55-109">Holes might be caused by the offline regions, so fix the assignments first.</span></span> 

<span data-ttu-id="bbd55-110">To bring the unassigned regions back to a normal state, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="bbd55-110">To bring the unassigned regions back to a normal state, complete the following steps:</span></span>

1. <span data-ttu-id="bbd55-111">Sign in to the HDInsight HBase cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="bbd55-111">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="bbd55-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-112">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="bbd55-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-113">Run the `rmr /hbase/regions-in-transition` command or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="bbd55-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-114">To exit from the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="bbd55-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span><span class="sxs-lookup"><span data-stu-id="bbd55-115">Open the Apache Ambari UI, and then restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="bbd55-116">Run the `hbase hbck` command again (without any options).</span><span class="sxs-lookup"><span data-stu-id="bbd55-116">Run the `hbase hbck` command again (without any options).</span></span> <span data-ttu-id="bbd55-117">Check the output of this command to ensure that all regions are being assigned.</span><span class="sxs-lookup"><span data-stu-id="bbd55-117">Check the output of this command to ensure that all regions are being assigned.</span></span>


## <a name="how-do-i-fix-timeout-issues-with-hbck-commands-for-region-assignments"></a><span data-ttu-id="bbd55-118">How do I fix timeout issues when using hbck commands for region assignments?</span><span class="sxs-lookup"><span data-stu-id="bbd55-118">How do I fix timeout issues when using hbck commands for region assignments?</span></span>

### <a name="issue"></a><span data-ttu-id="bbd55-119">Issue</span><span class="sxs-lookup"><span data-stu-id="bbd55-119">Issue</span></span>

<span data-ttu-id="bbd55-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span><span class="sxs-lookup"><span data-stu-id="bbd55-120">A potential cause for timeout issues when you use the `hbck` command might be that several regions are in the "in transition" state for a long time.</span></span> <span data-ttu-id="bbd55-121">You can see those regions as offline in the HBase Master UI.</span><span class="sxs-lookup"><span data-stu-id="bbd55-121">You can see those regions as offline in the HBase Master UI.</span></span> <span data-ttu-id="bbd55-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span><span class="sxs-lookup"><span data-stu-id="bbd55-122">Because a high number of regions are attempting to transition, HBase Master might timeout and be unable to bring those regions back online.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-123">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-123">Resolution steps</span></span>

1. <span data-ttu-id="bbd55-124">Sign in to the HDInsight HBase cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="bbd55-124">Sign in to the HDInsight HBase cluster by using SSH.</span></span>
2. <span data-ttu-id="bbd55-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-125">To connect with the ZooKeeper shell, run the `hbase zkcli` command.</span></span>
3. <span data-ttu-id="bbd55-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-126">Run the `rmr /hbase/regions-in-transition` or the `rmr /hbase-unsecure/regions-in-transition` command.</span></span>
4. <span data-ttu-id="bbd55-127">To exit the `hbase zkcli` shell, use the `exit` command.</span><span class="sxs-lookup"><span data-stu-id="bbd55-127">To exit the `hbase zkcli` shell, use the `exit` command.</span></span>
5. <span data-ttu-id="bbd55-128">In the Ambari UI, restart the Active HBase Master service.</span><span class="sxs-lookup"><span data-stu-id="bbd55-128">In the Ambari UI, restart the Active HBase Master service.</span></span>
6. <span data-ttu-id="bbd55-129">Run the `hbase hbck -fixAssignments` command again.</span><span class="sxs-lookup"><span data-stu-id="bbd55-129">Run the `hbase hbck -fixAssignments` command again.</span></span>

## <a name="how-do-i-force-disable-hdfs-safe-mode-in-a-cluster"></a><span data-ttu-id="bbd55-130">How do I force-disable HDFS safe mode in a cluster?</span><span class="sxs-lookup"><span data-stu-id="bbd55-130">How do I force-disable HDFS safe mode in a cluster?</span></span>

### <a name="issue"></a><span data-ttu-id="bbd55-131">Issue</span><span class="sxs-lookup"><span data-stu-id="bbd55-131">Issue</span></span>

<span data-ttu-id="bbd55-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="bbd55-132">The local Hadoop Distributed File System (HDFS) is stuck in safe mode on the HDInsight cluster.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="bbd55-133">Detailed description</span><span class="sxs-lookup"><span data-stu-id="bbd55-133">Detailed description</span></span>

<span data-ttu-id="bbd55-134">This error might be caused by a failure when you run the following HDFS command:</span><span class="sxs-lookup"><span data-stu-id="bbd55-134">This error might be caused by a failure when you run the following HDFS command:</span></span>

```apache
hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
```

<span data-ttu-id="bbd55-135">The error you might see when you try to run the command looks like this:</span><span class="sxs-lookup"><span data-stu-id="bbd55-135">The error you might see when you try to run the command looks like this:</span></span>

```apache
hdiuser@hn0-spark2:~$ hdfs dfs -D "fs.default.name=hdfs://mycluster/" -mkdir /temp
17/04/05 16:20:52 WARN retry.RetryInvocationHandler: Exception while invoking ClientNamenodeProtocolTranslatorPB.mkdirs over hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net/10.0.0.22:8020. Not retrying because try once and fail.
org.apache.hadoop.ipc.RemoteException(org.apache.hadoop.hdfs.server.namenode.SafeModeException): Cannot create directory /temp. Name node is in safe mode.
It was turned on manually. Use "hdfs dfsadmin -safemode leave" to turn safe mode off.
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.checkNameNodeSafeMode(FSNamesystem.java:1359)
        at org.apache.hadoop.hdfs.server.namenode.FSNamesystem.mkdirs(FSNamesystem.java:4010)
        at org.apache.hadoop.hdfs.server.namenode.NameNodeRpcServer.mkdirs(NameNodeRpcServer.java:1102)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolServerSideTranslatorPB.mkdirs(ClientNamenodeProtocolServerSideTranslatorPB.java:630)
        at org.apache.hadoop.hdfs.protocol.proto.ClientNamenodeProtocolProtos$ClientNamenodeProtocol$2.callBlockingMethod(ClientNamenodeProtocolProtos.java)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Server$ProtoBufRpcInvoker.call(ProtobufRpcEngine.java:640)
        at org.apache.hadoop.ipc.RPC$Server.call(RPC.java:982)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2313)
        at org.apache.hadoop.ipc.Server$Handler$1.run(Server.java:2309)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:422)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1724)
        at org.apache.hadoop.ipc.Server$Handler.run(Server.java:2307)
        at org.apache.hadoop.ipc.Client.getRpcResponse(Client.java:1552)
        at org.apache.hadoop.ipc.Client.call(Client.java:1496)
        at org.apache.hadoop.ipc.Client.call(Client.java:1396)
        at org.apache.hadoop.ipc.ProtobufRpcEngine$Invoker.invoke(ProtobufRpcEngine.java:233)
        at com.sun.proxy.$Proxy10.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.protocolPB.ClientNamenodeProtocolTranslatorPB.mkdirs(ClientNamenodeProtocolTranslatorPB.java:603)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invokeMethod(RetryInvocationHandler.java:278)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:194)
        at org.apache.hadoop.io.retry.RetryInvocationHandler.invoke(RetryInvocationHandler.java:176)
        at com.sun.proxy.$Proxy11.mkdirs(Unknown Source)
        at org.apache.hadoop.hdfs.DFSClient.primitiveMkdir(DFSClient.java:3061)
        at org.apache.hadoop.hdfs.DFSClient.mkdirs(DFSClient.java:3031)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1162)
        at org.apache.hadoop.hdfs.DistributedFileSystem$24.doCall(DistributedFileSystem.java:1158)
        at org.apache.hadoop.fs.FileSystemLinkResolver.resolve(FileSystemLinkResolver.java:81)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirsInternal(DistributedFileSystem.java:1158)
        at org.apache.hadoop.hdfs.DistributedFileSystem.mkdirs(DistributedFileSystem.java:1150)
        at org.apache.hadoop.fs.FileSystem.mkdirs(FileSystem.java:1898)
        at org.apache.hadoop.fs.shell.Mkdir.processNonexistentPath(Mkdir.java:76)
        at org.apache.hadoop.fs.shell.Command.processArgument(Command.java:273)
        at org.apache.hadoop.fs.shell.Command.processArguments(Command.java:255)
        at org.apache.hadoop.fs.shell.FsCommand.processRawArguments(FsCommand.java:119)
        at org.apache.hadoop.fs.shell.Command.run(Command.java:165)
        at org.apache.hadoop.fs.FsShell.run(FsShell.java:297)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
        at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:90)
        at org.apache.hadoop.fs.FsShell.main(FsShell.java:350)
mkdir: Cannot create directory /temp. Name node is in safe mode.
```

### <a name="probable-cause"></a><span data-ttu-id="bbd55-136">Probable cause</span><span class="sxs-lookup"><span data-stu-id="bbd55-136">Probable cause</span></span>

<span data-ttu-id="bbd55-137">The HDInsight cluster has been scaled down to a very few nodes.</span><span class="sxs-lookup"><span data-stu-id="bbd55-137">The HDInsight cluster has been scaled down to a very few nodes.</span></span> <span data-ttu-id="bbd55-138">The number of nodes is below or close to the HDFS replication factor.</span><span class="sxs-lookup"><span data-stu-id="bbd55-138">The number of nodes is below or close to the HDFS replication factor.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-139">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-139">Resolution steps</span></span> 

1. <span data-ttu-id="bbd55-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span><span class="sxs-lookup"><span data-stu-id="bbd55-140">Get the status of the HDFS on the HDInsight cluster by running the following commands:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   ```

   ```apache
   hdiuser@hn0-spark2:~$ hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -report
   Safe mode is ON
   Configured Capacity: 3372381241344 (3.07 TB)
   Present Capacity: 3138625077248 (2.85 TB)
   DFS Remaining: 3102710317056 (2.82 TB)
   DFS Used: 35914760192 (33.45 GB)
   DFS Used%: 1.14%
   Under replicated blocks: 0
   Blocks with corrupt replicas: 0
   Missing blocks: 0
   Missing blocks (with replication factor 1): 0

   -------------------------------------------------
   Live datanodes (8):

   Name: 10.0.0.17:30010 (10.0.0.17)
   Hostname: 10.0.0.17
   Decommission Status : Normal
   Configured Capacity: 421547655168 (392.60 GB)
   DFS Used: 5288128512 (4.92 GB)
   Non DFS Used: 29087272960 (27.09 GB)
   DFS Remaining: 387172253696 (360.58 GB)
   DFS Used%: 1.25%
   DFS Remaining%: 91.85%
   Configured Cache Capacity: 0 (0 B)
   Cache Used: 0 (0 B)
   Cache Remaining: 0 (0 B)
   Cache Used%: 100.00%
   Cache Remaining%: 0.00%
   Xceivers: 2
   Last contact: Wed Apr 05 16:22:00 UTC 2017
   ...

   ```
2. <span data-ttu-id="bbd55-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="bbd55-141">You also can check the integrity of the HDFS on the HDInsight cluster by using the following commands:</span></span>

   ```apache
   hdiuser@hn0-spark2:~$ hdfs fsck -D "fs.default.name=hdfs://mycluster/" /
   ```

   ```apache
   Connecting to namenode via http://hn0-spark2.2oyzcdm4sfjuzjmj5dnmvscjpg.dx.internal.cloudapp.net:30070/fsck?ugi=hdiuser&path=%2F
   FSCK started by hdiuser (auth:SIMPLE) from /10.0.0.22 for path / at Wed Apr 05 16:40:28 UTC 2017
   ....................................................................................................

   ....................................................................................................
   ..................Status: HEALTHY
   Total size:    9330539472 B
   Total dirs:    37
   Total files:   2618
   Total symlinks:                0 (Files currently being written: 2)
   Total blocks (validated):      2535 (avg. block size 3680686 B)
   Minimally replicated blocks:   2535 (100.0 %)
   Over-replicated blocks:        0 (0.0 %)
   Under-replicated blocks:       0 (0.0 %)
   Mis-replicated blocks:         0 (0.0 %)
   Default replication factor:    3
   Average block replication:     3.0
   Corrupt blocks:                0
   Missing replicas:              0 (0.0 %)
   Number of data-nodes:          8
   Number of racks:               1
   FSCK ended at Wed Apr 05 16:40:28 UTC 2017 in 187 milliseconds

   The filesystem under path '/' is HEALTHY
   ```

3. <span data-ttu-id="bbd55-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span><span class="sxs-lookup"><span data-stu-id="bbd55-142">If you determine that there are no missing, corrupt, or under-replicated blocks, or that those blocks can be ignored, run the following command to take the name node out of safe mode:</span></span>

   ```apache
   hdfs dfsadmin -D "fs.default.name=hdfs://mycluster/" -safemode leave
   ```


## <a name="how-do-i-fix-jdbc-or-sqlline-connectivity-issues-with-apache-phoenix"></a><span data-ttu-id="bbd55-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix?</span><span class="sxs-lookup"><span data-stu-id="bbd55-143">How do I fix JDBC or SQLLine connectivity issues with Apache Phoenix?</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-144">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-144">Resolution steps</span></span>

<span data-ttu-id="bbd55-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span><span class="sxs-lookup"><span data-stu-id="bbd55-145">To connect with Phoenix, you must provide the IP address of an active ZooKeeper node.</span></span> <span data-ttu-id="bbd55-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span><span class="sxs-lookup"><span data-stu-id="bbd55-146">Ensure that the ZooKeeper service to which sqlline.py is trying to connect is up and running.</span></span>
1. <span data-ttu-id="bbd55-147">Sign in to the HDInsight cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="bbd55-147">Sign in to the HDInsight cluster by using SSH.</span></span>
2. <span data-ttu-id="bbd55-148">Enter the following command:</span><span class="sxs-lookup"><span data-stu-id="bbd55-148">Enter the following command:</span></span>
                
   ```apache
           "/usr/hdp/current/phoenix-client/bin/sqlline.py <IP of machine where Active Zookeeper is running"
   ```

   > [!Note] 
   > <span data-ttu-id="bbd55-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span><span class="sxs-lookup"><span data-stu-id="bbd55-149">You can get the IP address of the active ZooKeeper node from the Ambari UI.</span></span> <span data-ttu-id="bbd55-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span><span class="sxs-lookup"><span data-stu-id="bbd55-150">Go to **HBase** > **Quick Links** > **ZK\* (Active)** > **Zookeeper Info**.</span></span> 

3. <span data-ttu-id="bbd55-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span><span class="sxs-lookup"><span data-stu-id="bbd55-151">If the sqlline.py connects to Phoenix and does not timeout, run the following command to validate the availability and health of Phoenix:</span></span>

   ```apache
           !tables
           !quit
   ```      
4. <span data-ttu-id="bbd55-152">If this command works, there is no issue.</span><span class="sxs-lookup"><span data-stu-id="bbd55-152">If this command works, there is no issue.</span></span> <span data-ttu-id="bbd55-153">The IP address provided by the user might be incorrect.</span><span class="sxs-lookup"><span data-stu-id="bbd55-153">The IP address provided by the user might be incorrect.</span></span> <span data-ttu-id="bbd55-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span><span class="sxs-lookup"><span data-stu-id="bbd55-154">However, if the command pauses for an extended time and then displays the following error, continue to step 5.</span></span>

   ```apache
           Error while connecting to sqlline.py (Hbase - phoenix) Setting property: [isolation, TRANSACTION_READ_COMMITTED] issuing: !connect jdbc:phoenix:10.2.0.7 none none org.apache.phoenix.jdbc.PhoenixDriver Connecting to jdbc:phoenix:10.2.0.7 SLF4J: Class path contains multiple SLF4J bindings. 
   ```

5. <span data-ttu-id="bbd55-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span><span class="sxs-lookup"><span data-stu-id="bbd55-155">Run the following commands from the head node (hn0) to diagnose the condition of the Phoenix SYSTEM.CATALOG table:</span></span>

   ```apache
            hbase shell
                
           count 'SYSTEM.CATALOG'
   ```

   <span data-ttu-id="bbd55-156">The command should return an error similar to the following:</span><span class="sxs-lookup"><span data-stu-id="bbd55-156">The command should return an error similar to the following:</span></span> 

   ```apache
           ERROR: org.apache.hadoop.hbase.NotServingRegionException: Region SYSTEM.CATALOG,,1485464083256.c0568c94033870c517ed36c45da98129. is not online on 10.2.0.5,16020,1489466172189) 
   ```
6. <span data-ttu-id="bbd55-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span><span class="sxs-lookup"><span data-stu-id="bbd55-157">In the Ambari UI, complete the following steps to restart the HMaster service on all ZooKeeper nodes:</span></span>

    1. <span data-ttu-id="bbd55-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span><span class="sxs-lookup"><span data-stu-id="bbd55-158">In the **Summary** section of HBase, go to **HBase** > **Active HBase Master**.</span></span> 
    2. <span data-ttu-id="bbd55-159">In the **Components** section, restart the HBase Master service.</span><span class="sxs-lookup"><span data-stu-id="bbd55-159">In the **Components** section, restart the HBase Master service.</span></span>
    3. <span data-ttu-id="bbd55-160">Repeat these steps for all remaining **Standby HBase Master** services.</span><span class="sxs-lookup"><span data-stu-id="bbd55-160">Repeat these steps for all remaining **Standby HBase Master** services.</span></span> 

<span data-ttu-id="bbd55-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span><span class="sxs-lookup"><span data-stu-id="bbd55-161">It can take up to five minutes for the HBase Master service to stabilize and finish the recovery process.</span></span> <span data-ttu-id="bbd55-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span><span class="sxs-lookup"><span data-stu-id="bbd55-162">After a few minutes, repeat the sqlline.py commands to confirm that the SYSTEM.CATALOG table is up, and that it can be queried.</span></span> 

<span data-ttu-id="bbd55-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span><span class="sxs-lookup"><span data-stu-id="bbd55-163">When the SYSTEM.CATALOG table is back to normal, the connectivity issue to Phoenix should be automatically resolved.</span></span>


## <a name="what-causes-a-master-server-to-fail-to-start"></a><span data-ttu-id="bbd55-164">What causes a master server to fail to start?</span><span class="sxs-lookup"><span data-stu-id="bbd55-164">What causes a master server to fail to start?</span></span>

### <a name="error"></a><span data-ttu-id="bbd55-165">Error</span><span class="sxs-lookup"><span data-stu-id="bbd55-165">Error</span></span> 

<span data-ttu-id="bbd55-166">An atomic renaming failure occurs.</span><span class="sxs-lookup"><span data-stu-id="bbd55-166">An atomic renaming failure occurs.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="bbd55-167">Detailed description</span><span class="sxs-lookup"><span data-stu-id="bbd55-167">Detailed description</span></span>

<span data-ttu-id="bbd55-168">During the startup process, HMaster completes many initialization steps.</span><span class="sxs-lookup"><span data-stu-id="bbd55-168">During the startup process, HMaster completes many initialization steps.</span></span> <span data-ttu-id="bbd55-169">These include moving data from the scratch (.tmp) folder to the data folder.</span><span class="sxs-lookup"><span data-stu-id="bbd55-169">These include moving data from the scratch (.tmp) folder to the data folder.</span></span> <span data-ttu-id="bbd55-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span><span class="sxs-lookup"><span data-stu-id="bbd55-170">HMaster also looks at the write-ahead logs (WALs) folder to see if there are any unresponsive region servers, and so on.</span></span> 

<span data-ttu-id="bbd55-171">During startup, HMaster does a basic `list` command on these folders.</span><span class="sxs-lookup"><span data-stu-id="bbd55-171">During startup, HMaster does a basic `list` command on these folders.</span></span> <span data-ttu-id="bbd55-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span><span class="sxs-lookup"><span data-stu-id="bbd55-172">If at any time, HMaster sees an unexpected file in any of these folders, it throws an exception and doesn't start.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="bbd55-173">Probable cause</span><span class="sxs-lookup"><span data-stu-id="bbd55-173">Probable cause</span></span>

<span data-ttu-id="bbd55-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span><span class="sxs-lookup"><span data-stu-id="bbd55-174">In the region server logs, try to identify the timeline of the file creation, and then see if there was a process crash around the time the file was created.</span></span> <span data-ttu-id="bbd55-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span><span class="sxs-lookup"><span data-stu-id="bbd55-175">(Contact HBase support to assist you in doing this.) This helps us provide more robust mechanisms, so that you can avoid hitting this bug, and ensure graceful process shutdowns.</span></span>

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-176">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-176">Resolution steps</span></span>

<span data-ttu-id="bbd55-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span><span class="sxs-lookup"><span data-stu-id="bbd55-177">Check the call stack and try to determine which folder might be causing the problem (for instance, it might be the WALs folder or the .tmp folder).</span></span> <span data-ttu-id="bbd55-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span><span class="sxs-lookup"><span data-stu-id="bbd55-178">Then, in Cloud Explorer or by using HDFS commands, try to locate the problem file.</span></span> <span data-ttu-id="bbd55-179">Usually, this is a \*-renamePending.json file.</span><span class="sxs-lookup"><span data-stu-id="bbd55-179">Usually, this is a \*-renamePending.json file.</span></span> <span data-ttu-id="bbd55-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span><span class="sxs-lookup"><span data-stu-id="bbd55-180">(The \*-renamePending.json file is a journal file that's used to implement the atomic rename operation in the WASB driver.</span></span> <span data-ttu-id="bbd55-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span><span class="sxs-lookup"><span data-stu-id="bbd55-181">Due to bugs in this implementation, these files can be left over after process crashes, and so on.) Force-delete this file either in Cloud Explorer or by using HDFS commands.</span></span> 

<span data-ttu-id="bbd55-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span><span class="sxs-lookup"><span data-stu-id="bbd55-182">Sometimes, there might also be a temporary file named something like *$$$.$$$* at this location.</span></span> <span data-ttu-id="bbd55-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="bbd55-183">You have to use HDFS `ls` command to see this file; you cannot see the file in Cloud Explorer.</span></span> <span data-ttu-id="bbd55-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span><span class="sxs-lookup"><span data-stu-id="bbd55-184">To delete this file, use the HDFS command `hdfs dfs -rm /\<path>\/\$\$\$.\$\$\$`.</span></span>  

<span data-ttu-id="bbd55-185">After you've run these commands, HMaster should start immediately.</span><span class="sxs-lookup"><span data-stu-id="bbd55-185">After you've run these commands, HMaster should start immediately.</span></span> 

### <a name="error"></a><span data-ttu-id="bbd55-186">Error</span><span class="sxs-lookup"><span data-stu-id="bbd55-186">Error</span></span>

<span data-ttu-id="bbd55-187">No server address is listed in *hbase: meta* for region xxx.</span><span class="sxs-lookup"><span data-stu-id="bbd55-187">No server address is listed in *hbase: meta* for region xxx.</span></span>

### <a name="detailed-description"></a><span data-ttu-id="bbd55-188">Detailed description</span><span class="sxs-lookup"><span data-stu-id="bbd55-188">Detailed description</span></span>

<span data-ttu-id="bbd55-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span><span class="sxs-lookup"><span data-stu-id="bbd55-189">You might see a message on your Linux cluster that indicates that the *hbase: meta* table is not online.</span></span> <span data-ttu-id="bbd55-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span><span class="sxs-lookup"><span data-stu-id="bbd55-190">Running `hbck` might report that "hbase: meta table replicaId 0 is not found on any region."</span></span> <span data-ttu-id="bbd55-191">The problem might be that HMaster could not initialize after you restarted HBase.</span><span class="sxs-lookup"><span data-stu-id="bbd55-191">The problem might be that HMaster could not initialize after you restarted HBase.</span></span> <span data-ttu-id="bbd55-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span><span class="sxs-lookup"><span data-stu-id="bbd55-192">In the HMaster logs, you might see the message: "No server address listed in hbase: meta for region hbase: backup \<region name\>".</span></span>  

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-193">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-193">Resolution steps</span></span>

1. <span data-ttu-id="bbd55-194">In the HBase shell, enter the following commands (change actual values as applicable):</span><span class="sxs-lookup"><span data-stu-id="bbd55-194">In the HBase shell, enter the following commands (change actual values as applicable):</span></span>  

   ```apache
   > scan 'hbase:meta'  
   ```

   ```apache
   > delete 'hbase:meta','hbase:backup <region name>','<column name>'  
   ```

2. <span data-ttu-id="bbd55-195">Delete the *hbase: namespace* entry.</span><span class="sxs-lookup"><span data-stu-id="bbd55-195">Delete the *hbase: namespace* entry.</span></span> <span data-ttu-id="bbd55-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span><span class="sxs-lookup"><span data-stu-id="bbd55-196">This entry might be the same error that's being reported when the *hbase: namespace* table is scanned.</span></span>

3. <span data-ttu-id="bbd55-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span><span class="sxs-lookup"><span data-stu-id="bbd55-197">To bring up HBase in a running state, in the Ambari UI, restart the Active HMaster service.</span></span>  

4. <span data-ttu-id="bbd55-198">In the HBase shell, to bring up all offline tables, run the following command:</span><span class="sxs-lookup"><span data-stu-id="bbd55-198">In the HBase shell, to bring up all offline tables, run the following command:</span></span>

   ```apache 
   hbase hbck -ignorePreCheckPermission -fixAssignments 
   ```

### <a name="additional-reading"></a><span data-ttu-id="bbd55-199">Additional reading</span><span class="sxs-lookup"><span data-stu-id="bbd55-199">Additional reading</span></span>

[<span data-ttu-id="bbd55-200">Unable to process the HBase table</span><span class="sxs-lookup"><span data-stu-id="bbd55-200">Unable to process the HBase table</span></span>](http://stackoverflow.com/questions/4794092/unable-to-access-hbase-table)


### <a name="error"></a><span data-ttu-id="bbd55-201">Error</span><span class="sxs-lookup"><span data-stu-id="bbd55-201">Error</span></span>

<span data-ttu-id="bbd55-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span><span class="sxs-lookup"><span data-stu-id="bbd55-202">HMaster times out with a fatal exception similar to "java.io.IOException: Timedout 300000ms waiting for namespace table to be assigned."</span></span>

### <a name="detailed-description"></a><span data-ttu-id="bbd55-203">Detailed description</span><span class="sxs-lookup"><span data-stu-id="bbd55-203">Detailed description</span></span>

<span data-ttu-id="bbd55-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span><span class="sxs-lookup"><span data-stu-id="bbd55-204">You might experience this issue if you have many tables and regions that have not been flushed when you restart your HMaster services.</span></span> <span data-ttu-id="bbd55-205">Restart might fail, and you'll see the preceding error message.</span><span class="sxs-lookup"><span data-stu-id="bbd55-205">Restart might fail, and you'll see the preceding error message.</span></span>  

### <a name="probable-cause"></a><span data-ttu-id="bbd55-206">Probable cause</span><span class="sxs-lookup"><span data-stu-id="bbd55-206">Probable cause</span></span>

<span data-ttu-id="bbd55-207">This is a known issue with the HMaster service.</span><span class="sxs-lookup"><span data-stu-id="bbd55-207">This is a known issue with the HMaster service.</span></span> <span data-ttu-id="bbd55-208">General cluster startup tasks can take a long time.</span><span class="sxs-lookup"><span data-stu-id="bbd55-208">General cluster startup tasks can take a long time.</span></span> <span data-ttu-id="bbd55-209">HMaster shuts down because the namespace table isn’t yet assigned.</span><span class="sxs-lookup"><span data-stu-id="bbd55-209">HMaster shuts down because the namespace table isn’t yet assigned.</span></span> <span data-ttu-id="bbd55-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span><span class="sxs-lookup"><span data-stu-id="bbd55-210">This occurs only in scenarios in which large amount of unflushed data exists, and a timeout of five minutes is not sufficient.</span></span>
  
### <a name="resolution-steps"></a><span data-ttu-id="bbd55-211">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-211">Resolution steps</span></span>

1. <span data-ttu-id="bbd55-212">In the Ambari UI, go to **HBase** > **Configs**.</span><span class="sxs-lookup"><span data-stu-id="bbd55-212">In the Ambari UI, go to **HBase** > **Configs**.</span></span> <span data-ttu-id="bbd55-213">In the custom hbase-site.xml file, add the following setting:</span><span class="sxs-lookup"><span data-stu-id="bbd55-213">In the custom hbase-site.xml file, add the following setting:</span></span> 

   ```apache
   Key: hbase.master.namespace.init.timeout Value: 2400000  
   ```

2. <span data-ttu-id="bbd55-214">Restart the required services (HMaster, and possibly other HBase services).</span><span class="sxs-lookup"><span data-stu-id="bbd55-214">Restart the required services (HMaster, and possibly other HBase services).</span></span>  


## <a name="what-causes-a-restart-failure-on-a-region-server"></a><span data-ttu-id="bbd55-215">What causes a restart failure on a region server?</span><span class="sxs-lookup"><span data-stu-id="bbd55-215">What causes a restart failure on a region server?</span></span>

### <a name="issue"></a><span data-ttu-id="bbd55-216">Issue</span><span class="sxs-lookup"><span data-stu-id="bbd55-216">Issue</span></span>

<span data-ttu-id="bbd55-217">A restart failure on a region server might be prevented by following best practices.</span><span class="sxs-lookup"><span data-stu-id="bbd55-217">A restart failure on a region server might be prevented by following best practices.</span></span> <span data-ttu-id="bbd55-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span><span class="sxs-lookup"><span data-stu-id="bbd55-218">We recommend that you pause heavy workload activity when you are planning to restart HBase region servers.</span></span> <span data-ttu-id="bbd55-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span><span class="sxs-lookup"><span data-stu-id="bbd55-219">If an application continues to connect with region servers when shutdown is in progress, the region server restart operation will be slower by several minutes.</span></span> <span data-ttu-id="bbd55-220">Also, it's a good idea to first flush all the tables.</span><span class="sxs-lookup"><span data-stu-id="bbd55-220">Also, it's a good idea to first flush all the tables.</span></span> <span data-ttu-id="bbd55-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span><span class="sxs-lookup"><span data-stu-id="bbd55-221">For a reference on how to flush tables, see [HDInsight HBase: How to improve the HBase cluster restart time by flushing tables](https://blogs.msdn.microsoft.com/azuredatalake/2016/09/19/hdinsight-hbase-how-to-improve-hbase-cluster-restart-time-by-flushing-tables/).</span></span>

<span data-ttu-id="bbd55-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span><span class="sxs-lookup"><span data-stu-id="bbd55-222">If you initiate the restart operation on HBase region servers from the Ambari UI, you immediately see that the region servers went down, but they don't restart right away.</span></span> 

<span data-ttu-id="bbd55-223">Here's what's happening behind the scenes:</span><span class="sxs-lookup"><span data-stu-id="bbd55-223">Here's what's happening behind the scenes:</span></span> 

1. <span data-ttu-id="bbd55-224">The Ambari agent sends a stop request to the region server.</span><span class="sxs-lookup"><span data-stu-id="bbd55-224">The Ambari agent sends a stop request to the region server.</span></span>
2. <span data-ttu-id="bbd55-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span><span class="sxs-lookup"><span data-stu-id="bbd55-225">The Ambari agent waits for 30 seconds for the region server to shut down gracefully.</span></span> 
3. <span data-ttu-id="bbd55-226">If your application continues to connect with the region server, the server won't shut down immediately.</span><span class="sxs-lookup"><span data-stu-id="bbd55-226">If your application continues to connect with the region server, the server won't shut down immediately.</span></span> <span data-ttu-id="bbd55-227">The 30-second timeout expires before shutdown occurs.</span><span class="sxs-lookup"><span data-stu-id="bbd55-227">The 30-second timeout expires before shutdown occurs.</span></span> 
4. <span data-ttu-id="bbd55-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span><span class="sxs-lookup"><span data-stu-id="bbd55-228">After 30 seconds, the Ambari agent sends a force-kill (`kill -9`) command to the region server.</span></span> <span data-ttu-id="bbd55-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span><span class="sxs-lookup"><span data-stu-id="bbd55-229">You can see this in the ambari-agent log (in the /var/log/ directory of the respective worker node):</span></span>

   ```apache
           2017-03-21 13:22:09,171 - Execute['/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/current/hbase-regionserver/conf stop regionserver'] {'only_if': 'ambari-sudo.sh  -H -E t
           est -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1', 'on_timeout': '! ( ambari-sudo.sh  -H -E test -
           f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >/dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H 
           -E cat /var/run/hbase/hbase-hbase-regionserver.pid`', 'timeout': 30, 'user': 'hbase'}
           2017-03-21 13:22:40,268 - Executing '! ( ambari-sudo.sh  -H -E test -f /var/run/hbase/hbase-hbase-regionserver.pid && ps -p `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid` >
           /dev/null 2>&1 ) || ambari-sudo.sh -H -E kill -9 `ambari-sudo.sh  -H -E cat /var/run/hbase/hbase-hbase-regionserver.pid`'. Reason: Execution of 'ambari-sudo.sh su hbase -l -s /bin/bash -c 'export  
           PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/var/lib/ambari-agent ; /usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh --config /usr/hdp/curre
           nt/hbase-regionserver/conf stop regionserver was killed due timeout after 30 seconds
           2017-03-21 13:22:40,285 - File['/var/run/hbase/hbase-hbase-regionserver.pid'] {'action': ['delete']}
           2017-03-21 13:22:40,285 - Deleting File['/var/run/hbase/hbase-hbase-regionserver.pid']
   ```
<span data-ttu-id="bbd55-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span><span class="sxs-lookup"><span data-stu-id="bbd55-230">Because of the abrupt shutdown, the port associated with the process might not be released, even though the region server process is stopped.</span></span> <span data-ttu-id="bbd55-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span><span class="sxs-lookup"><span data-stu-id="bbd55-231">This situation can lead to an AddressBindException when the region server is starting, as shown in the following logs.</span></span> <span data-ttu-id="bbd55-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span><span class="sxs-lookup"><span data-stu-id="bbd55-232">You can verify this in the region-server.log in the /var/log/hbase directory on the worker nodes where the region server fails to start.</span></span> 

   ```apache

   2017-03-21 13:25:47,061 ERROR [main] regionserver.HRegionServerCommandLine: Region server exiting
   java.lang.RuntimeException: Failed construction of Regionserver: class org.apache.hadoop.hbase.regionserver.HRegionServer
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2636)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.start(HRegionServerCommandLine.java:64)
   at org.apache.hadoop.hbase.regionserver.HRegionServerCommandLine.run(HRegionServerCommandLine.java:87)
   at org.apache.hadoop.util.ToolRunner.run(ToolRunner.java:76)
   at org.apache.hadoop.hbase.util.ServerCommandLine.doMain(ServerCommandLine.java:126)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.main(HRegionServer.java:2651)
        
   Caused by: java.lang.reflect.InvocationTargetException
   at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
   at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:57)
   at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
   at java.lang.reflect.Constructor.newInstance(Constructor.java:526)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.constructRegionServer(HRegionServer.java:2634)
   ... 5 more
        
   Caused by: java.net.BindException: Problem binding to /10.2.0.4:16020 : Address already in use
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2497)
   at org.apache.hadoop.hbase.ipc.RpcServer$Listener.<init>(RpcServer.java:580)
   at org.apache.hadoop.hbase.ipc.RpcServer.<init>(RpcServer.java:1982)
   at org.apache.hadoop.hbase.regionserver.RSRpcServices.<init>(RSRpcServices.java:863)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.createRpcServices(HRegionServer.java:632)
   at org.apache.hadoop.hbase.regionserver.HRegionServer.<init>(HRegionServer.java:532)
   ... 10 more
        
   Caused by: java.net.BindException: Address already in use
   at sun.nio.ch.Net.bind0(Native Method)
   at sun.nio.ch.Net.bind(Net.java:463)
   at sun.nio.ch.Net.bind(Net.java:455)
   at sun.nio.ch.ServerSocketChannelImpl.bind(ServerSocketChannelImpl.java:223)
   at sun.nio.ch.ServerSocketAdaptor.bind(ServerSocketAdaptor.java:74)
   at org.apache.hadoop.hbase.ipc.RpcServer.bind(RpcServer.java:2495)
   ... 15 more
   ```

### <a name="resolution-steps"></a><span data-ttu-id="bbd55-233">Resolution steps</span><span class="sxs-lookup"><span data-stu-id="bbd55-233">Resolution steps</span></span>

1. <span data-ttu-id="bbd55-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span><span class="sxs-lookup"><span data-stu-id="bbd55-234">Try to reduce the load on the HBase region servers before you initiate a restart.</span></span> 
2. <span data-ttu-id="bbd55-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span><span class="sxs-lookup"><span data-stu-id="bbd55-235">Alternatively (if step 1 doesn't help), try to manually restart region servers on the worker nodes by using the following commands:</span></span>

   ```apache
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh stop regionserver"
   sudo su - hbase -c "/usr/hdp/current/hbase-regionserver/bin/hbase-daemon.sh start regionserver"   
   ```

### <a name="see-also"></a><span data-ttu-id="bbd55-236">See Also</span><span class="sxs-lookup"><span data-stu-id="bbd55-236">See Also</span></span>
[<span data-ttu-id="bbd55-237">Troubleshoot by Using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="bbd55-237">Troubleshoot by Using Azure HDInsight</span></span>](../../hdinsight/hdinsight-troubleshoot-guide.md)
