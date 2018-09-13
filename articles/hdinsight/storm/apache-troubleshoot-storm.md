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
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a>Troubleshoot Storm by using Azure HDInsight

Learn about the top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.

## <a name="how-do-i-access-the-storm-ui-on-a-cluster"></a>How do I access the Storm UI on a cluster?
You have two options for accessing the Storm UI from a browser:

### <a name="ambari-ui"></a>Ambari UI
1. Go to the Ambari dashboard.
2. In the list of services, select **Storm**.
3. In the **Quick Links** menu, select **Storm UI**.

### <a name="direct-link"></a>Direct link
You can access the Storm UI at the following URL:

https://\<cluster DNS name\>/stormui

Example:

 https://stormcluster.azurehdinsight.net/stormui

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-to-another"></a>How do I transfer Storm event hub spout checkpoint information from one topology to another?

When you develop topologies that read from Azure Event Hubs by using the HDInsight Storm event hub spout .jar file, you must deploy a topology that has the same name on a new cluster. However, you must retain the checkpoint data that was committed to Apache ZooKeeper on the old cluster.

### <a name="where-checkpoint-data-is-stored"></a>Where checkpoint data is stored
Checkpoint data for offsets is stored by the event hub spout in ZooKeeper in two root paths:
- Nontransactional spout checkpoints are stored in /eventhubspout.
- Transactional spout checkpoint data is stored in /transactional.

### <a name="how-to-restore"></a>How to restore
To get the scripts and libraries that you use to export data out of ZooKeeper and then import the data back to ZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).

The lib folder has .jar files that contain the implementation for the export/import operation. The bash folder has an example script that demonstrates how to export data from the ZooKeeper server on the old cluster, and then import it back to the ZooKeeper server on the new cluster.

Run the [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from the ZooKeeper nodes to export and then import data. Update the script to the correct Hortonworks Data Platform (HDP) version. (We are working on making these scripts generic in HDInsight. Generic scripts can run from any node on the cluster without modifications by the user.)

The export command writes the metadata to an Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.

### <a name="examples"></a>Examples

#### <a name="export-offset-metadata"></a>Export offset metadata
1. Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be exported.
2. Run the following command (after you update the HDP version string) to export ZooKeeper offset data to the /stormmetadta/zkdata HDFS path:

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a>Import offset metadata
1. Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be imported.
2. Run the following command (after you update the HDP version string) to import ZooKeeper offset data from the HDFS path /stormmetadata/zkdata to the ZooKeeper server on the target cluster:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-the-beginning-or-from-a-timestamp-that-the-user-chooses"></a>Delete offset metadata so that topologies can start processing data from the beginning, or from a timestamp that the user chooses
1. Use SSH to go to the ZooKeeper cluster on the cluster from which the checkpoint offset needs to be deleted.
2. Run the following command (after you update the HDP version string) to delete all ZooKeeper offset data in the current cluster:

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a>How do I locate Storm binaries on a cluster?
Storm binaries for the current HDP stack are in /usr/hdp/current/storm-client. The location is the same both for head nodes and for worker nodes.
 
There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm). The /usr/hdp/current/storm-client folder is symlinked to the latest version that is running on the cluster.

For more information, see [Connect to an HDInsight cluster by using SSH](https://docs.microsoft.com/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).
 
## <a name="how-do-i-determine-the-deployment-topology-of-a-storm-cluster"></a>How do I determine the deployment topology of a Storm cluster?
First, identify all components that are installed with HDInsight Storm. A Storm cluster consists of four node categories:

* Gateway nodes
* Head nodes
* ZooKeeper nodes
* Worker nodes
 
### <a name="gateway-nodes"></a>Gateway nodes
A gateway node is a gateway and reverse proxy service that enables public access to an active Ambari management service. It also handles Ambari leader election.
 
### <a name="head-nodes"></a>Head nodes
Storm head nodes run the following services:
* Nimbus
* Ambari server
* Ambari Metrics server
* Ambari Metrics Collector
 
### <a name="zookeeper-nodes"></a>ZooKeeper nodes
HDInsight comes with a three-node ZooKeeper quorum. The quorum size is fixed, and cannot be reconfigured.
 
Storm services in the cluster are configured to automatically use the ZooKeeper quorum.
 
### <a name="worker-nodes"></a>Worker nodes
Storm worker nodes run the following services:
* Supervisor
* Worker Java virtual machines (JVMs), for running topologies
* Ambari agent
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a>How do I locate Storm event hub spout binaries for development?
 
For more information about using Storm event hub spout .jar files with your topology, see the following resources.
 
### <a name="java-based-topology"></a>Java-based topology
[Process events from Azure Event Hubs with Storm on HDInsight (Java)](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a>C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)
[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a>Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters
To learn how to use the latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see the mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).
 
### <a name="source-code-examples"></a>Source code examples
See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how to read and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a>How do I locate Storm Log4J configuration files on clusters?
 
To identify Apache Log4J configuration files for Storm services.
 
### <a name="on-head-nodes"></a>On head nodes
The Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.
 
### <a name="on-worker-nodes"></a>On worker nodes
The supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.
 
The worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.
 
Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml

### <a name="see-also"></a>See Also
[Troubleshoot by Using Azure HDInsight](../../hdinsight/hdinsight-troubleshoot-guide.md)
