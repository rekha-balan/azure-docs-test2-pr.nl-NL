---
title: Troubleshoot Storm by using Azure HDInsight
description: Get answers to common questions about using Apache Storm with Azure HDInsight.
keywords: Azure HDInsight, Storm, FAQ, troubleshooting guide, common problems
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonwhowell
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 11/2/2017
ms.openlocfilehash: cad9e6ceb22ab66b5a3fe00358eb6b6170a3f29f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871288"
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="a2b52-104">Troubleshoot Storm by using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a2b52-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="a2b52-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="a2b52-105">Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a><span data-ttu-id="a2b52-106">How do I access the Storm UI on a cluster?</span><span class="sxs-lookup"><span data-stu-id="a2b52-106">How do I access the Storm UI on a cluster?</span></span>
<span data-ttu-id="a2b52-107">You have two options for accessing the Storm UI from a browser:</span><span class="sxs-lookup"><span data-stu-id="a2b52-107">You have two options for accessing the Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="a2b52-108">Ambari UI</span><span class="sxs-lookup"><span data-stu-id="a2b52-108">Ambari UI</span></span>
1. <span data-ttu-id="a2b52-109">Go to the Ambari dashboard.</span><span class="sxs-lookup"><span data-stu-id="a2b52-109">Go to the Ambari dashboard.</span></span>
2. <span data-ttu-id="a2b52-110">In the list of services, select **Storm**.</span><span class="sxs-lookup"><span data-stu-id="a2b52-110">In the list of services, select **Storm**.</span></span>
3. <span data-ttu-id="a2b52-111">In the **Quick Links** menu, select **Storm UI**.</span><span class="sxs-lookup"><span data-stu-id="a2b52-111">In the **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="a2b52-112">Direct link</span><span class="sxs-lookup"><span data-stu-id="a2b52-112">Direct link</span></span>
<span data-ttu-id="a2b52-113">You can access the Storm UI at the following URL:</span><span class="sxs-lookup"><span data-stu-id="a2b52-113">You can access the Storm UI at the following URL:</span></span>

<span data-ttu-id="a2b52-114">https://\<cluster DNS name\>/stormui</span><span class="sxs-lookup"><span data-stu-id="a2b52-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="a2b52-115">Example:</span><span class="sxs-lookup"><span data-stu-id="a2b52-115">Example:</span></span>

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a><span data-ttu-id="a2b52-116">How do I transfer Storm event hub spout checkpoint information from one topology to another?</span><span class="sxs-lookup"><span data-stu-id="a2b52-116">How do I transfer Storm event hub spout checkpoint information from one topology to another?</span></span>

<span data-ttu-id="a2b52-117">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b52-117">When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster.</span></span> <span data-ttu-id="a2b52-118">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b52-118">However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="a2b52-119">Where checkpoint data is stored</span><span class="sxs-lookup"><span data-stu-id="a2b52-119">Where checkpoint data is stored</span></span>
<span data-ttu-id="a2b52-120">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span><span class="sxs-lookup"><span data-stu-id="a2b52-120">Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="a2b52-121">Nontransactional spout checkpoints are stored in /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="a2b52-121">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="a2b52-122">Transactional spout checkpoint data is stored in /transactional.</span><span class="sxs-lookup"><span data-stu-id="a2b52-122">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-to-restore"></a><span data-ttu-id="a2b52-123">How to restore</span><span class="sxs-lookup"><span data-stu-id="a2b52-123">How to restore</span></span>
<span data-ttu-id="a2b52-124">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="a2b52-124">To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="a2b52-125">The lib folder has .jar files that contain the implementation for the export/import operation.</span><span class="sxs-lookup"><span data-stu-id="a2b52-125">The lib folder has .jar files that contain the implementation for the export/import operation.</span></span> <span data-ttu-id="a2b52-126">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b52-126">The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.</span></span>

<span data-ttu-id="a2b52-127">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span><span class="sxs-lookup"><span data-stu-id="a2b52-127">Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data.</span></span> <span data-ttu-id="a2b52-128">Update the script to the correct Hortonworks Data Platform (HDP) version.</span><span class="sxs-lookup"><span data-stu-id="a2b52-128">Update the script to the correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="a2b52-129">(We are working on making these scripts generic in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a2b52-129">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="a2b52-130">Generic scripts can run from any node on the cluster without modifications by the user.)</span><span class="sxs-lookup"><span data-stu-id="a2b52-130">Generic scripts can run from any node on the cluster without modifications by the user.)</span></span>

<span data-ttu-id="a2b52-131">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span><span class="sxs-lookup"><span data-stu-id="a2b52-131">The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="a2b52-132">Examples</span><span class="sxs-lookup"><span data-stu-id="a2b52-132">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="a2b52-133">Export offset metadata</span><span class="sxs-lookup"><span data-stu-id="a2b52-133">Export offset metadata</span></span>
1. <span data-ttu-id="a2b52-134">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span><span class="sxs-lookup"><span data-stu-id="a2b52-134">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.</span></span>
2. <span data-ttu-id="a2b52-135">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span><span class="sxs-lookup"><span data-stu-id="a2b52-135">Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="a2b52-136">Import offset metadata</span><span class="sxs-lookup"><span data-stu-id="a2b52-136">Import offset metadata</span></span>
1. <span data-ttu-id="a2b52-137">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be imported.</span><span class="sxs-lookup"><span data-stu-id="a2b52-137">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be imported.</span></span>
2. <span data-ttu-id="a2b52-138">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span><span class="sxs-lookup"><span data-stu-id="a2b52-138">Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a><span data-ttu-id="a2b52-139">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span><span class="sxs-lookup"><span data-stu-id="a2b52-139">Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses</span></span>
1. <span data-ttu-id="a2b52-140">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be deleted.</span><span class="sxs-lookup"><span data-stu-id="a2b52-140">Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be deleted.</span></span>
2. <span data-ttu-id="a2b52-141">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span><span class="sxs-lookup"><span data-stu-id="a2b52-141">Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="a2b52-142">How do I locate Storm binaries on a cluster?</span><span class="sxs-lookup"><span data-stu-id="a2b52-142">How do I locate Storm binaries on a cluster?</span></span>
<span data-ttu-id="a2b52-143">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="a2b52-143">Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="a2b52-144">The location is the same both for head nodes and for worker nodes.</span><span class="sxs-lookup"><span data-stu-id="a2b52-144">The location is the same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="a2b52-145">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="a2b52-145">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="a2b52-146">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b52-146">The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.</span></span>

<span data-ttu-id="a2b52-147">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a2b52-147">For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="a2b52-148">How do I determine the deployment topology of a Storm cluster?</span><span class="sxs-lookup"><span data-stu-id="a2b52-148">How do I determine the deployment topology of a Storm cluster?</span></span>
<span data-ttu-id="a2b52-149">First, identify all components that are installed with HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="a2b52-149">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="a2b52-150">A Storm cluster consists of four node categories:</span><span class="sxs-lookup"><span data-stu-id="a2b52-150">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="a2b52-151">Gateway nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-151">Gateway nodes</span></span>
* <span data-ttu-id="a2b52-152">Head nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-152">Head nodes</span></span>
* <span data-ttu-id="a2b52-153">ZooKeeper nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-153">ZooKeeper nodes</span></span>
* <span data-ttu-id="a2b52-154">Worker nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-154">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="a2b52-155">Gateway nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-155">Gateway nodes</span></span>
<span data-ttu-id="a2b52-156">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span><span class="sxs-lookup"><span data-stu-id="a2b52-156">A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service.</span></span> <span data-ttu-id="a2b52-157">It also handles Ambari leader election.</span><span class="sxs-lookup"><span data-stu-id="a2b52-157">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="a2b52-158">Head nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-158">Head nodes</span></span>
<span data-ttu-id="a2b52-159">Storm head nodes run the following services:</span><span class="sxs-lookup"><span data-stu-id="a2b52-159">Storm head nodes run the following services:</span></span>
* <span data-ttu-id="a2b52-160">Nimbus</span><span class="sxs-lookup"><span data-stu-id="a2b52-160">Nimbus</span></span>
* <span data-ttu-id="a2b52-161">Ambari server</span><span class="sxs-lookup"><span data-stu-id="a2b52-161">Ambari server</span></span>
* <span data-ttu-id="a2b52-162">Ambari Metrics server</span><span class="sxs-lookup"><span data-stu-id="a2b52-162">Ambari Metrics server</span></span>
* <span data-ttu-id="a2b52-163">Ambari Metrics Collector</span><span class="sxs-lookup"><span data-stu-id="a2b52-163">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="a2b52-164">ZooKeeper nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-164">ZooKeeper nodes</span></span>
<span data-ttu-id="a2b52-165">HDInsight comes with a three-node ZooKeeper quorum.</span><span class="sxs-lookup"><span data-stu-id="a2b52-165">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="a2b52-166">The quorum size is fixed, and cannot be reconfigured.</span><span class="sxs-lookup"><span data-stu-id="a2b52-166">The quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="a2b52-167">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span><span class="sxs-lookup"><span data-stu-id="a2b52-167">Storm services in the cluster are configured to automatically use the ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="a2b52-168">Worker nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-168">Worker nodes</span></span>
<span data-ttu-id="a2b52-169">Storm worker nodes run the following services:</span><span class="sxs-lookup"><span data-stu-id="a2b52-169">Storm worker nodes run the following services:</span></span>
* <span data-ttu-id="a2b52-170">Supervisor</span><span class="sxs-lookup"><span data-stu-id="a2b52-170">Supervisor</span></span>
* <span data-ttu-id="a2b52-171">Worker Java virtual machines (JVMs), for running topologies</span><span class="sxs-lookup"><span data-stu-id="a2b52-171">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="a2b52-172">Ambari agent</span><span class="sxs-lookup"><span data-stu-id="a2b52-172">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="a2b52-173">How do I locate Storm event hub spout binaries for development?</span><span class="sxs-lookup"><span data-stu-id="a2b52-173">How do I locate Storm event hub spout binaries for development?</span></span>
 
<span data-ttu-id="a2b52-174">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span><span class="sxs-lookup"><span data-stu-id="a2b52-174">For more information about using Storm event hub spout .jar files with your topology, see the following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="a2b52-175">Java-based topology</span><span class="sxs-lookup"><span data-stu-id="a2b52-175">Java-based topology</span></span>
[<span data-ttu-id="a2b52-176">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="a2b52-176">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="a2b52-177">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span><span class="sxs-lookup"><span data-stu-id="a2b52-177">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
[<span data-ttu-id="a2b52-178">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="a2b52-178">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="a2b52-179">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span><span class="sxs-lookup"><span data-stu-id="a2b52-179">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="a2b52-180">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="a2b52-180">To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="a2b52-181">Source code examples</span><span class="sxs-lookup"><span data-stu-id="a2b52-181">Source code examples</span></span>
<span data-ttu-id="a2b52-182">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="a2b52-182">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="a2b52-183">How do I locate Storm Log4J configuration files on clusters?</span><span class="sxs-lookup"><span data-stu-id="a2b52-183">How do I locate Storm Log4J configuration files on clusters?</span></span>
 
<span data-ttu-id="a2b52-184">To identify Apache Log4J configuration files for Storm services.</span><span class="sxs-lookup"><span data-stu-id="a2b52-184">To identify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="a2b52-185">On head nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-185">On head nodes</span></span>
<span data-ttu-id="a2b52-186">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="a2b52-186">The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="a2b52-187">On worker nodes</span><span class="sxs-lookup"><span data-stu-id="a2b52-187">On worker nodes</span></span>
<span data-ttu-id="a2b52-188">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="a2b52-188">The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="a2b52-189">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="a2b52-189">The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="a2b52-190">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="a2b52-190">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

### <a name="see-also"></a><span data-ttu-id="a2b52-191">See Also</span><span class="sxs-lookup"><span data-stu-id="a2b52-191">See Also</span></span>
[<span data-ttu-id="a2b52-192">Troubleshoot by Using Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a2b52-192">Troubleshoot by Using Azure HDInsight</span></span>](../../hdinsight/hdinsight-troubleshoot-guide.md)
