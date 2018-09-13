---
title: Receive events from Azure Event Hubs using Apache Storm | Microsoft Docs
description: Get started receiving from Event Hubs using Apache Storm
services: event-hubs
documentationcenter: ''
author: jtaubensee
manager: timlt
editor: ''
ms.assetid: ''
ms.service: event-hubs
ms.workload: na
ms.tgt_pltfrm: java
ms.devlang: multiple
ms.topic: article
ms.date: 01/30/2017
ms.author: jotaub;sethm
ms.openlocfilehash: d7d593a6f6e359034b1a02321bd7cdc7677d4fb9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551665"
---
# <a name="receive-events-from-event-hubs-using-apache-storm"></a><span data-ttu-id="224cf-103">Receive events from Event Hubs using Apache Storm</span><span class="sxs-lookup"><span data-stu-id="224cf-103">Receive events from Event Hubs using Apache Storm</span></span>
<span data-ttu-id="224cf-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span><span class="sxs-lookup"><span data-stu-id="224cf-104">[Apache Storm](https://storm.incubator.apache.org) is a distributed real-time computation system that simplifies reliable processing of unbounded streams of data.</span></span> <span data-ttu-id="224cf-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="224cf-105">This section shows how to use an Azure Event Hubs Storm spout to receive events from Event Hubs.</span></span> <span data-ttu-id="224cf-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span><span class="sxs-lookup"><span data-stu-id="224cf-106">Using Apache Storm, you can split events across multiple processes hosted in different nodes.</span></span> <span data-ttu-id="224cf-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="224cf-107">The Event Hubs integration with Storm simplifies event consumption by transparently checkpointing its progress using Storm's Zookeeper installation, managing persistent checkpoints and parallel receives from Event Hubs.</span></span>

<span data-ttu-id="224cf-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span><span class="sxs-lookup"><span data-stu-id="224cf-108">For more information about Event Hubs receive patterns, see the [Event Hubs overview][Event Hubs overview].</span></span>

<span data-ttu-id="224cf-109">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span><span class="sxs-lookup"><span data-stu-id="224cf-109">This tutorial uses an [HDInsight Storm][HDInsight Storm] installation, which comes with the Event Hubs spout already available.</span></span>

1. <span data-ttu-id="224cf-110">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="224cf-110">Follow the [HDInsight Storm - Get Started](../hdinsight/hdinsight-storm-overview.md) procedure to create a new HDInsight cluster, and connect to it via Remote Desktop.</span></span>
2. <span data-ttu-id="224cf-111">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span><span class="sxs-lookup"><span data-stu-id="224cf-111">Copy the `%STORM_HOME%\examples\eventhubspout\eventhubs-storm-spout-0.9-jar-with-dependencies.jar` file to your local development environment.</span></span> <span data-ttu-id="224cf-112">This contains the events-storm-spout.</span><span class="sxs-lookup"><span data-stu-id="224cf-112">This contains the events-storm-spout.</span></span>
3. <span data-ttu-id="224cf-113">Use the following command to install the package into the local Maven store.</span><span class="sxs-lookup"><span data-stu-id="224cf-113">Use the following command to install the package into the local Maven store.</span></span> <span data-ttu-id="224cf-114">This enables you to add it as a reference in the Storm project in a later step.</span><span class="sxs-lookup"><span data-stu-id="224cf-114">This enables you to add it as a reference in the Storm project in a later step.</span></span>

```shell
        mvn install:install-file -Dfile=target\eventhubs-storm-spout-0.9-jar-with-dependencies.jar -DgroupId=com.microsoft.eventhubs -DartifactId=eventhubs-storm-spout -Dversion=0.9 -Dpackaging=jar
```
4. <span data-ttu-id="224cf-115">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span><span class="sxs-lookup"><span data-stu-id="224cf-115">In Eclipse, create a new Maven project (click **File**, then **New**, then **Project**).</span></span>
   
    ![][12]
5. <span data-ttu-id="224cf-116">Select **Use default Workspace location**, then click **Next**</span><span class="sxs-lookup"><span data-stu-id="224cf-116">Select **Use default Workspace location**, then click **Next**</span></span>
6. <span data-ttu-id="224cf-117">Select the **maven-archetype-quickstart** archetype, then click **Next**</span><span class="sxs-lookup"><span data-stu-id="224cf-117">Select the **maven-archetype-quickstart** archetype, then click **Next**</span></span>
7. <span data-ttu-id="224cf-118">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span><span class="sxs-lookup"><span data-stu-id="224cf-118">Insert a **GroupId** and **ArtifactId**, then click **Finish**</span></span>
8. <span data-ttu-id="224cf-119">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span><span class="sxs-lookup"><span data-stu-id="224cf-119">In **pom.xml**, add the following dependencies in the `<dependency>` node.</span></span>
```xml  
        <dependency>
            <groupId>org.apache.storm</groupId>
            <artifactId>storm-core</artifactId>
            <version>0.9.2-incubating</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>com.microsoft.eventhubs</groupId>
            <artifactId>eventhubs-storm-spout</artifactId>
            <version>0.9</version>
        </dependency>
        <dependency>
            <groupId>com.netflix.curator</groupId>
            <artifactId>curator-framework</artifactId>
            <version>1.3.3</version>
            <exclusions>
                <exclusion>
                    <groupId>log4j</groupId>
                    <artifactId>log4j</artifactId>
                </exclusion>
                <exclusion>
                    <groupId>org.slf4j</groupId>
                    <artifactId>slf4j-log4j12</artifactId>
                </exclusion>
            </exclusions>
            <scope>provided</scope>
        </dependency>
```
9. <span data-ttu-id="224cf-120">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the following values:</span><span class="sxs-lookup"><span data-stu-id="224cf-120">In the **src** folder, create a file called **Config.properties** and copy the following content, substituting the following values:</span></span>

    ```java
    eventhubspout.username = ReceiveRule
    eventhubspout.password = {receive rule key}
    eventhubspout.namespace = ioteventhub-ns
    eventhubspout.entitypath = {event hub name}
    eventhubspout.partitions.count = 16
       
    # if not provided, will use storm's zookeeper settings
    # zookeeper.connectionstring=localhost:2181
       
    eventhubspout.checkpoint.interval = 10
    eventhub.receiver.credits = 10
    ```
    <span data-ttu-id="224cf-121">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span><span class="sxs-lookup"><span data-stu-id="224cf-121">The value for **eventhub.receiver.credits** determines how many events are batched before releasing them to the Storm pipeline.</span></span> <span data-ttu-id="224cf-122">For the sake of simplicity, this example sets this value to 10.</span><span class="sxs-lookup"><span data-stu-id="224cf-122">For the sake of simplicity, this example sets this value to 10.</span></span> <span data-ttu-id="224cf-123">In production, it should usually be set to higher values; for example, 1024.</span><span class="sxs-lookup"><span data-stu-id="224cf-123">In production, it should usually be set to higher values; for example, 1024.</span></span>
10. <span data-ttu-id="224cf-124">Create a new class called **LoggerBolt** with the following code:</span><span class="sxs-lookup"><span data-stu-id="224cf-124">Create a new class called **LoggerBolt** with the following code:</span></span>
    
    ```java
    import java.util.Map;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import backtype.storm.task.OutputCollector;
    import backtype.storm.task.TopologyContext;
    import backtype.storm.topology.OutputFieldsDeclarer;
    import backtype.storm.topology.base.BaseRichBolt;
    import backtype.storm.tuple.Tuple;
    
    public class LoggerBolt extends BaseRichBolt {
        private OutputCollector collector;
        private static final Logger logger = LoggerFactory
                  .getLogger(LoggerBolt.class);
    
        @Override
        public void execute(Tuple tuple) {
            String value = tuple.getString(0);
            logger.info("Tuple value: " + value);
   
            collector.ack(tuple);
        }
   
        @Override
        public void prepare(Map map, TopologyContext context, OutputCollector collector) {
            this.collector = collector;
            this.count = 0;
        }
        
        @Override
        public void declareOutputFields(OutputFieldsDeclarer declarer) {
            // no output fields
        }
    
    }
    ```
    
    <span data-ttu-id="224cf-125">This Storm bolt logs the content of the received events.</span><span class="sxs-lookup"><span data-stu-id="224cf-125">This Storm bolt logs the content of the received events.</span></span> <span data-ttu-id="224cf-126">This can easily be extended to store tuples in a storage service.</span><span class="sxs-lookup"><span data-stu-id="224cf-126">This can easily be extended to store tuples in a storage service.</span></span> <span data-ttu-id="224cf-127">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span><span class="sxs-lookup"><span data-stu-id="224cf-127">The [HDInsight sensor analysis tutorial] uses this same approach to store data into HBase.</span></span>
11. <span data-ttu-id="224cf-128">Create a class called **LogTopology** with the following code:</span><span class="sxs-lookup"><span data-stu-id="224cf-128">Create a class called **LogTopology** with the following code:</span></span>
    
    ```java
    import java.io.FileReader;
    import java.util.Properties;
    import backtype.storm.Config;
    import backtype.storm.LocalCluster;
    import backtype.storm.StormSubmitter;
    import backtype.storm.generated.StormTopology;
    import backtype.storm.topology.TopologyBuilder;
    import com.microsoft.eventhubs.samples.EventCount;
    import com.microsoft.eventhubs.spout.EventHubSpout;
    import com.microsoft.eventhubs.spout.EventHubSpoutConfig;
        
    public class LogTopology {
        protected EventHubSpoutConfig spoutConfig;
        protected int numWorkers;
        
        protected void readEHConfig(String[] args) throws Exception {
            Properties properties = new Properties();
            if (args.length > 1) {
                properties.load(new FileReader(args[1]));
            } else {
                properties.load(EventCount.class.getClassLoader()
                        .getResourceAsStream("Config.properties"));
            }
        
            String username = properties.getProperty("eventhubspout.username");
            String password = properties.getProperty("eventhubspout.password");
            String namespaceName = properties
                    .getProperty("eventhubspout.namespace");
            String entityPath = properties.getProperty("eventhubspout.entitypath");
            String zkEndpointAddress = properties
                    .getProperty("zookeeper.connectionstring"); // opt
            int partitionCount = Integer.parseInt(properties
                    .getProperty("eventhubspout.partitions.count"));
            int checkpointIntervalInSeconds = Integer.parseInt(properties
                    .getProperty("eventhubspout.checkpoint.interval"));
            int receiverCredits = Integer.parseInt(properties
                    .getProperty("eventhub.receiver.credits")); // prefetch count
                                                                // (opt)
            System.out.println("Eventhub spout config: ");
            System.out.println("  partition count: " + partitionCount);
            System.out.println("  checkpoint interval: "
                    + checkpointIntervalInSeconds);
            System.out.println("  receiver credits: " + receiverCredits);
     
            spoutConfig = new EventHubSpoutConfig(username, password,
                    namespaceName, entityPath, partitionCount, zkEndpointAddress,
                    checkpointIntervalInSeconds, receiverCredits);
        
            // set the number of workers to be the same as partition number.
            // the idea is to have a spout and a logger bolt co-exist in one
            // worker to avoid shuffling messages across workers in storm cluster.
            numWorkers = spoutConfig.getPartitionCount();
        
            if (args.length > 0) {
                // set topology name so that sample Trident topology can use it as
                // stream name.
                spoutConfig.setTopologyName(args[0]);
            }
        }
        
        protected StormTopology buildTopology() {
            TopologyBuilder topologyBuilder = new TopologyBuilder();
       
            EventHubSpout eventHubSpout = new EventHubSpout(spoutConfig);
            topologyBuilder.setSpout("EventHubsSpout", eventHubSpout,
                    spoutConfig.getPartitionCount()).setNumTasks(
                    spoutConfig.getPartitionCount());
            topologyBuilder
                    .setBolt("LoggerBolt", new LoggerBolt(),
                            spoutConfig.getPartitionCount())
                    .localOrShuffleGrouping("EventHubsSpout")
                    .setNumTasks(spoutConfig.getPartitionCount());
            return topologyBuilder.createTopology();
        }
        
        protected void runScenario(String[] args) throws Exception {
            boolean runLocal = true;
            readEHConfig(args);
            StormTopology topology = buildTopology();
            Config config = new Config();
            config.setDebug(false);
        
            if (runLocal) {
                config.setMaxTaskParallelism(2);
                LocalCluster localCluster = new LocalCluster();
                localCluster.submitTopology("test", config, topology);
                Thread.sleep(5000000);
                localCluster.shutdown();
            } else {
                config.setNumWorkers(numWorkers);
                StormSubmitter.submitTopology(args[0], config, topology);
            }
        }
        
        public static void main(String[] args) throws Exception {
            LogTopology topology = new LogTopology();
            topology.runScenario(args);
        }
    }
    ```

    <span data-ttu-id="224cf-129">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span><span class="sxs-lookup"><span data-stu-id="224cf-129">This class creates a new Event Hubs spout, using the properties in the configuration file to instantiate it.</span></span> <span data-ttu-id="224cf-130">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span><span class="sxs-lookup"><span data-stu-id="224cf-130">It is important to note that this example creates as many spouts tasks as the number of partitions in the event hub, in order to use the maximum parallelism allowed by that event hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="224cf-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="224cf-131">Next steps</span></span>
<span data-ttu-id="224cf-132">You can learn more about Event Hubs by visiting the following links:</span><span class="sxs-lookup"><span data-stu-id="224cf-132">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="224cf-133">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="224cf-133">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="224cf-134">Create an event hub</span><span class="sxs-lookup"><span data-stu-id="224cf-134">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="224cf-135">Event Hubs FAQ</span><span class="sxs-lookup"><span data-stu-id="224cf-135">Event Hubs FAQ</span></span>](event-hubs-faq.md)

<!-- Links -->
[Event Hubs overview]: event-hubs-overview.md
[HDInsight Storm]: ../hdinsight/hdinsight-storm-overview.md
[HDInsight sensor analysis tutorial]: ../hdinsight/hdinsight-storm-sensor-data-analysis.md

<!-- Images -->

[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/event-hubs/media/event-hubs-get-started-receive-storm/create-storm1.png

