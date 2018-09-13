---
title: Analyze sensor data with Apache Storm and HBase | Microsoft Docs
description: Learn how to connect to Apache Storm with a virtual network. Use Storm with HBase to process sensor data from an event hub and visualize it with D3.js.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: larryfr
ms.openlocfilehash: a065c6d6aecbb2e30a9e2ef65236097a87292d4d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554579"
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="ccd93-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="ccd93-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="ccd93-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="ccd93-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span><span class="sxs-lookup"><span data-stu-id="ccd93-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="ccd93-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span><span class="sxs-lookup"><span data-stu-id="ccd93-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="ccd93-108">The template creates a Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span><span class="sxs-lookup"><span data-stu-id="ccd93-108">The template creates a Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="ccd93-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span><span class="sxs-lookup"><span data-stu-id="ccd93-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd93-110">The information in this document and example in this document require HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="ccd93-110">The information in this document and example in this document require HDInsight version 3.5.</span></span>
>
> <span data-ttu-id="ccd93-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="ccd93-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ccd93-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="ccd93-112">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ccd93-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ccd93-113">Prerequisites</span></span>

* <span data-ttu-id="ccd93-114">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="ccd93-114">An Azure subscription.</span></span> <span data-ttu-id="ccd93-115">See [Get Azure free trial](http://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ccd93-115">See [Get Azure free trial](http://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
  
  > [!IMPORTANT]
  > <span data-ttu-id="ccd93-116">You do not need an existing HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-116">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="ccd93-117">The steps in this document create the following resources:</span><span class="sxs-lookup"><span data-stu-id="ccd93-117">The steps in this document create the following resources:</span></span>
  > 
  > * <span data-ttu-id="ccd93-118">A Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="ccd93-118">A Azure Virtual Network</span></span>
  > * <span data-ttu-id="ccd93-119">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span><span class="sxs-lookup"><span data-stu-id="ccd93-119">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
  > * <span data-ttu-id="ccd93-120">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span><span class="sxs-lookup"><span data-stu-id="ccd93-120">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
  > * <span data-ttu-id="ccd93-121">An Azure Web App that hosts the web dashboard</span><span class="sxs-lookup"><span data-stu-id="ccd93-121">An Azure Web App that hosts the web dashboard</span></span>

* <span data-ttu-id="ccd93-122">[Node.js](http://nodejs.org/):Used to preview the web dashboard locally on your development environment.</span><span class="sxs-lookup"><span data-stu-id="ccd93-122">[Node.js](http://nodejs.org/):Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="ccd93-123">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span><span class="sxs-lookup"><span data-stu-id="ccd93-123">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="ccd93-124">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span><span class="sxs-lookup"><span data-stu-id="ccd93-124">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="ccd93-125">[Git](http://git-scm.com/): Used to download the project from GitHub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-125">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="ccd93-126">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-126">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="ccd93-127">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-127">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ccd93-128">You must also have access to the `scp` command, which is used to copy files between your local development environment and the HDInsight cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="ccd93-128">You must also have access to the `scp` command, which is used to copy files between your local development environment and the HDInsight cluster using SSH.</span></span>


## <a name="architecture"></a><span data-ttu-id="ccd93-129">Architecture</span><span class="sxs-lookup"><span data-stu-id="ccd93-129">Architecture</span></span>

![architecture diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="ccd93-131">This example consists of the following components:</span><span class="sxs-lookup"><span data-stu-id="ccd93-131">This example consists of the following components:</span></span>

* <span data-ttu-id="ccd93-132">**Azure Event Hubs**: Contains data that is collected from sensors.</span><span class="sxs-lookup"><span data-stu-id="ccd93-132">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="ccd93-133">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-133">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="ccd93-134">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span><span class="sxs-lookup"><span data-stu-id="ccd93-134">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="ccd93-135">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-135">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ccd93-136">A virtual network is required when using the Java HBase client API.</span><span class="sxs-lookup"><span data-stu-id="ccd93-136">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="ccd93-137">It is not exposed over the public gateway for HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-137">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="ccd93-138">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span><span class="sxs-lookup"><span data-stu-id="ccd93-138">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="ccd93-139">**Dashboard website**: An example dashboard that charts data in real time.</span><span class="sxs-lookup"><span data-stu-id="ccd93-139">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="ccd93-140">The website is implemented in Node.js, so it can run on any client operating system for testing, or it can be deployed to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="ccd93-140">The website is implemented in Node.js, so it can run on any client operating system for testing, or it can be deployed to Azure Websites.</span></span>
  * <span data-ttu-id="ccd93-141">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span><span class="sxs-lookup"><span data-stu-id="ccd93-141">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ccd93-142">Using Socket.io for communication is an implementation detail.</span><span class="sxs-lookup"><span data-stu-id="ccd93-142">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="ccd93-143">You can use any communications framework, such as raw WebSockets or SignalR.</span><span class="sxs-lookup"><span data-stu-id="ccd93-143">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="ccd93-144">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span><span class="sxs-lookup"><span data-stu-id="ccd93-144">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccd93-145">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span><span class="sxs-lookup"><span data-stu-id="ccd93-145">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="ccd93-146">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/javadoc/apidocs/org/apache/storm/hbase/bolt/class-use/HBaseBolt.html) class.</span><span class="sxs-lookup"><span data-stu-id="ccd93-146">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/javadoc/apidocs/org/apache/storm/hbase/bolt/class-use/HBaseBolt.html) class.</span></span> <span data-ttu-id="ccd93-147">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="ccd93-147">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="ccd93-148">The following diagram explains the layout of the topology:</span><span class="sxs-lookup"><span data-stu-id="ccd93-148">The following diagram explains the layout of the topology:</span></span>

![topology diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="ccd93-150">This is a simplified view of the topology.</span><span class="sxs-lookup"><span data-stu-id="ccd93-150">This is a simplified view of the topology.</span></span> <span data-ttu-id="ccd93-151">At run time, an instance of each component is created for each partition for the Event Hub that is being read.</span><span class="sxs-lookup"><span data-stu-id="ccd93-151">At run time, an instance of each component is created for each partition for the Event Hub that is being read.</span></span> <span data-ttu-id="ccd93-152">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span><span class="sxs-lookup"><span data-stu-id="ccd93-152">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="ccd93-153">Data from the spout to the parser is load balanced.</span><span class="sxs-lookup"><span data-stu-id="ccd93-153">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="ccd93-154">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span><span class="sxs-lookup"><span data-stu-id="ccd93-154">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="ccd93-155">Topology components</span><span class="sxs-lookup"><span data-stu-id="ccd93-155">Topology components</span></span>

* <span data-ttu-id="ccd93-156">**EventHub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span><span class="sxs-lookup"><span data-stu-id="ccd93-156">**EventHub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ccd93-157">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.3 or 3.4.</span><span class="sxs-lookup"><span data-stu-id="ccd93-157">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.3 or 3.4.</span></span> <span data-ttu-id="ccd93-158">For information on how to use Event Hubs with an older version of Storm on HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-158">For information on how to use Event Hubs with an older version of Storm on HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

* <span data-ttu-id="ccd93-159">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span><span class="sxs-lookup"><span data-stu-id="ccd93-159">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="ccd93-160">This bolt demonstrates how to read the data emitted by the spout, and emit it to a new stream as a tuple that contains multiple fields.</span><span class="sxs-lookup"><span data-stu-id="ccd93-160">This bolt demonstrates how to read the data emitted by the spout, and emit it to a new stream as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="ccd93-161">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span><span class="sxs-lookup"><span data-stu-id="ccd93-161">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="ccd93-162">**Temperature.java**: This defines the topology and loads configuration data from the **Config.properties** file.</span><span class="sxs-lookup"><span data-stu-id="ccd93-162">**Temperature.java**: This defines the topology and loads configuration data from the **Config.properties** file.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="ccd93-163">Prepare your environment</span><span class="sxs-lookup"><span data-stu-id="ccd93-163">Prepare your environment</span></span>

<span data-ttu-id="ccd93-164">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span><span class="sxs-lookup"><span data-stu-id="ccd93-164">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="ccd93-165">Configure Event Hub</span><span class="sxs-lookup"><span data-stu-id="ccd93-165">Configure Event Hub</span></span>

<span data-ttu-id="ccd93-166">Event Hub is the data source for this example.</span><span class="sxs-lookup"><span data-stu-id="ccd93-166">Event Hub is the data source for this example.</span></span> <span data-ttu-id="ccd93-167">Use the following steps to create an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-167">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="ccd93-168">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-168">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="ccd93-169">On the **Create Namespace** blade, perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="ccd93-169">On the **Create Namespace** blade, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="ccd93-170">Enter a **Name** for the namespace.</span><span class="sxs-lookup"><span data-stu-id="ccd93-170">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="ccd93-171">Select a pricing tier.</span><span class="sxs-lookup"><span data-stu-id="ccd93-171">Select a pricing tier.</span></span> <span data-ttu-id="ccd93-172">**Basic** is sufficient for this example.</span><span class="sxs-lookup"><span data-stu-id="ccd93-172">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="ccd93-173">Select the Azure **Subscription** to use.</span><span class="sxs-lookup"><span data-stu-id="ccd93-173">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="ccd93-174">Either select an existing resource group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="ccd93-174">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="ccd93-175">Select the **Location** for the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-175">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="ccd93-176">Select **Pin to dashboard**, and then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-176">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="ccd93-177">When the creation process completes, the Event Hubs blade for your namespace is displayed.</span><span class="sxs-lookup"><span data-stu-id="ccd93-177">When the creation process completes, the Event Hubs blade for your namespace is displayed.</span></span> <span data-ttu-id="ccd93-178">From here, select **+ Add Event Hub**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-178">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="ccd93-179">On the **Create Event Hub** blade, enter a name of **sensordata**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-179">On the **Create Event Hub** blade, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="ccd93-180">Leave the other fields at the default values.</span><span class="sxs-lookup"><span data-stu-id="ccd93-180">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="ccd93-181">From the Event Hubs blade for your namespace, select **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-181">From the Event Hubs blade for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="ccd93-182">Select the **sensordata** entry.</span><span class="sxs-lookup"><span data-stu-id="ccd93-182">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="ccd93-183">From the blade for the sensordata Event Hub, select **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-183">From the blade for the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="ccd93-184">Use the **+ Add** link to add the following policies:</span><span class="sxs-lookup"><span data-stu-id="ccd93-184">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="ccd93-185">Policy name</span><span class="sxs-lookup"><span data-stu-id="ccd93-185">Policy name</span></span> | <span data-ttu-id="ccd93-186">Claims</span><span class="sxs-lookup"><span data-stu-id="ccd93-186">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="ccd93-187">devices</span><span class="sxs-lookup"><span data-stu-id="ccd93-187">devices</span></span> | <span data-ttu-id="ccd93-188">Send</span><span class="sxs-lookup"><span data-stu-id="ccd93-188">Send</span></span> |
    | <span data-ttu-id="ccd93-189">storm</span><span class="sxs-lookup"><span data-stu-id="ccd93-189">storm</span></span> | <span data-ttu-id="ccd93-190">Listen</span><span class="sxs-lookup"><span data-stu-id="ccd93-190">Listen</span></span> |

1. <span data-ttu-id="ccd93-191">Select both policies and make a note of the **PRIMARY KEY** value.</span><span class="sxs-lookup"><span data-stu-id="ccd93-191">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="ccd93-192">You need the value for both policies in future steps.</span><span class="sxs-lookup"><span data-stu-id="ccd93-192">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="ccd93-193">Download and configure the project</span><span class="sxs-lookup"><span data-stu-id="ccd93-193">Download and configure the project</span></span>

<span data-ttu-id="ccd93-194">Use the following to download the project from GitHub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-194">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="ccd93-195">After the command completes, you have the following directory structure:</span><span class="sxs-lookup"><span data-stu-id="ccd93-195">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                hbase-site.xml - connection information for the HBase cluster.
                Config.properties - configuration information for the topology. How to read from Event Hub and the URI to the dashboard.
            src/ - the Java bolts and topology definition.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="ccd93-196">This document does not go in to full details of the code included in this sample.</span><span class="sxs-lookup"><span data-stu-id="ccd93-196">This document does not go in to full details of the code included in this sample.</span></span> <span data-ttu-id="ccd93-197">However, the code is fully commented.</span><span class="sxs-lookup"><span data-stu-id="ccd93-197">However, the code is fully commented.</span></span>

<span data-ttu-id="ccd93-198">Open the **hdinsight-eventhub-example/TemperatureMonitor/resources/Config.properties** file and add your Event Hub information to the following lines:</span><span class="sxs-lookup"><span data-stu-id="ccd93-198">Open the **hdinsight-eventhub-example/TemperatureMonitor/resources/Config.properties** file and add your Event Hub information to the following lines:</span></span>

    eventhubspout.username = <shared access policy name that can read from Event Hub>
    eventhubspout.password = <shared access policy key>
    eventhubspout.namespace = <namespace of your Event Hub
    eventhubspout.entitypath = <name of your event hub>
    eventhubspout.partitions.count = 2

<span data-ttu-id="ccd93-199">Save the file after you add this information.</span><span class="sxs-lookup"><span data-stu-id="ccd93-199">Save the file after you add this information.</span></span>

## <a name="compile-and-test-locally"></a><span data-ttu-id="ccd93-200">Compile and test locally</span><span class="sxs-lookup"><span data-stu-id="ccd93-200">Compile and test locally</span></span>

<span data-ttu-id="ccd93-201">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-201">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ccd93-202">The HBase component of this topology is not active when testing locally.</span><span class="sxs-lookup"><span data-stu-id="ccd93-202">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="ccd93-203">This is because the Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-203">This is because the Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="ccd93-204">Start the web application</span><span class="sxs-lookup"><span data-stu-id="ccd93-204">Start the web application</span></span>

1. <span data-ttu-id="ccd93-205">Open a new command prompt or terminal, and change directories to the **hdinsight-eventhub-example/dashboard**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-205">Open a new command prompt or terminal, and change directories to the **hdinsight-eventhub-example/dashboard**.</span></span> <span data-ttu-id="ccd93-206">Use the following command to install the dependencies needed by the web application:</span><span class="sxs-lookup"><span data-stu-id="ccd93-206">Use the following command to install the dependencies needed by the web application:</span></span>
   
        npm install

2. <span data-ttu-id="ccd93-207">Use the following command to start the web application:</span><span class="sxs-lookup"><span data-stu-id="ccd93-207">Use the following command to start the web application:</span></span>
   
        node server.js
   
    <span data-ttu-id="ccd93-208">You see a message similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="ccd93-208">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="ccd93-209">Open a web browser and enter **http://localhost:3000/** as the address.</span><span class="sxs-lookup"><span data-stu-id="ccd93-209">Open a web browser and enter **http://localhost:3000/** as the address.</span></span> <span data-ttu-id="ccd93-210">You should see a page similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="ccd93-210">You should see a page similar to the following image:</span></span>
   
    ![web dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="ccd93-212">Leave this command prompt or terminal open.</span><span class="sxs-lookup"><span data-stu-id="ccd93-212">Leave this command prompt or terminal open.</span></span> <span data-ttu-id="ccd93-213">After testing, use Ctrl-C to stop the web server.</span><span class="sxs-lookup"><span data-stu-id="ccd93-213">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="start-generating-data"></a><span data-ttu-id="ccd93-214">Start generating data</span><span class="sxs-lookup"><span data-stu-id="ccd93-214">Start generating data</span></span>

> [!NOTE]
> <span data-ttu-id="ccd93-215">The steps in this section use Node.js so that they can be used on any platform.</span><span class="sxs-lookup"><span data-stu-id="ccd93-215">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="ccd93-216">For other language examples, see the **SendEvents** directory.</span><span class="sxs-lookup"><span data-stu-id="ccd93-216">For other language examples, see the **SendEvents** directory.</span></span>

1. <span data-ttu-id="ccd93-217">Open a new prompt, shell, or terminal, and change directories to **hdinsight-eventhub-example/SendEvents/nodejs**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-217">Open a new prompt, shell, or terminal, and change directories to **hdinsight-eventhub-example/SendEvents/nodejs**.</span></span> <span data-ttu-id="ccd93-218">To install the dependencies needed by the application, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ccd93-218">To install the dependencies needed by the application, use the following command:</span></span>
   
        npm install

2. <span data-ttu-id="ccd93-219">Open the **app.js** file in a text editor and add the Event Hub information you obtained earlier:</span><span class="sxs-lookup"><span data-stu-id="ccd93-219">Open the **app.js** file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
        // ServiceBus Namespace
        var namespace = 'YourNamespace';
        // Event Hub Name
        var hubname ='sensordata';
        // Shared access Policy name and key (from Event Hub configuration)
        var my_key_name = 'devices';
        var my_key = 'YourKey';
   
   > [!NOTE]
   > <span data-ttu-id="ccd93-220">This example assumes that you have used **sensordata** as the name of your Event Hub, and **devices** as the name of the policy that has a **Send** claim.</span><span class="sxs-lookup"><span data-stu-id="ccd93-220">This example assumes that you have used **sensordata** as the name of your Event Hub, and **devices** as the name of the policy that has a **Send** claim.</span></span>

3. <span data-ttu-id="ccd93-221">Use the following command to insert new entries in Event Hub:</span><span class="sxs-lookup"><span data-stu-id="ccd93-221">Use the following command to insert new entries in Event Hub:</span></span>
   
        node app.js
   
    <span data-ttu-id="ccd93-222">You see several lines of output that contain the data sent to Event Hub:</span><span class="sxs-lookup"><span data-stu-id="ccd93-222">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="start-the-topology"></a><span data-ttu-id="ccd93-223">Start the topology</span><span class="sxs-lookup"><span data-stu-id="ccd93-223">Start the topology</span></span>

1. <span data-ttu-id="ccd93-224">Open a new command prompt, shell, or terminal and change directories to **hdinsight-eventhub-example/TemperatureMonitor**, and then use the following command to start the topology:</span><span class="sxs-lookup"><span data-stu-id="ccd93-224">Open a new command prompt, shell, or terminal and change directories to **hdinsight-eventhub-example/TemperatureMonitor**, and then use the following command to start the topology:</span></span>
   
        mvn compile exec:java
   
    <span data-ttu-id="ccd93-225">This command starts the topology in local mode.</span><span class="sxs-lookup"><span data-stu-id="ccd93-225">This command starts the topology in local mode.</span></span> <span data-ttu-id="ccd93-226">The values contained in the **Config.properties** file provide the connection information for Event Hubs and the local dashboard web site.</span><span class="sxs-lookup"><span data-stu-id="ccd93-226">The values contained in the **Config.properties** file provide the connection information for Event Hubs and the local dashboard web site.</span></span> <span data-ttu-id="ccd93-227">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span><span class="sxs-lookup"><span data-stu-id="ccd93-227">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="ccd93-228">You should see lines appear in the web dashboard, similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="ccd93-228">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![dashboard with data](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="ccd93-230">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="ccd93-230">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="ccd93-231">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span><span class="sxs-lookup"><span data-stu-id="ccd93-231">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ccd93-232">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span><span class="sxs-lookup"><span data-stu-id="ccd93-232">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="ccd93-233">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span><span class="sxs-lookup"><span data-stu-id="ccd93-233">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="ccd93-234">You can use Ctrl+C to stop the local web server also.</span><span class="sxs-lookup"><span data-stu-id="ccd93-234">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="ccd93-235">Create a Storm and HBase cluster</span><span class="sxs-lookup"><span data-stu-id="ccd93-235">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="ccd93-236">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create a Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="ccd93-236">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create a Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="ccd93-237">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span><span class="sxs-lookup"><span data-stu-id="ccd93-237">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="ccd93-238">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="ccd93-238">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="ccd93-239">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet.json**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-239">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet.json**.</span></span>

1. <span data-ttu-id="ccd93-240">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ccd93-240">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.5.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="ccd93-241">From the **Custom deployment** blade, enter the following values:</span><span class="sxs-lookup"><span data-stu-id="ccd93-241">From the **Custom deployment** blade, enter the following values:</span></span>
   
    ![HDInsight parameters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="ccd93-243">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-243">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="ccd93-244">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-244">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="ccd93-245">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-245">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="ccd93-246">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-246">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="ccd93-247">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-247">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="ccd93-248">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-248">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="ccd93-249">**Location**: The region that the clusters are created in.</span><span class="sxs-lookup"><span data-stu-id="ccd93-249">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="ccd93-250">Click **OK** to save the parameters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-250">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="ccd93-251">Use the **Basics** section to create a resource group or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="ccd93-251">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="ccd93-252">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span><span class="sxs-lookup"><span data-stu-id="ccd93-252">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="ccd93-253">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-253">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="ccd93-254">Finally, check **Pin to dashboard** and then select **Purchase**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-254">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="ccd93-255">It takes about 20 minutes to create the clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-255">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="ccd93-256">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span><span class="sxs-lookup"><span data-stu-id="ccd93-256">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Resource group blade for the vnet and clusters](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="ccd93-258">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span><span class="sxs-lookup"><span data-stu-id="ccd93-258">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="ccd93-259">You use these names in a later step when connecting to the clusters.</span><span class="sxs-lookup"><span data-stu-id="ccd93-259">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="ccd93-260">Also note that the name of the dashboard site is **basename-dashboard**.</span><span class="sxs-lookup"><span data-stu-id="ccd93-260">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="ccd93-261">This value is used later in this document.</span><span class="sxs-lookup"><span data-stu-id="ccd93-261">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="ccd93-262">Configure the Dashboard bolt</span><span class="sxs-lookup"><span data-stu-id="ccd93-262">Configure the Dashboard bolt</span></span>

<span data-ttu-id="ccd93-263">To send data to the dashboard deployed as a web app, you must modify the following line in the **Config.properties** file:</span><span class="sxs-lookup"><span data-stu-id="ccd93-263">To send data to the dashboard deployed as a web app, you must modify the following line in the **Config.properties** file:</span></span>

    dashboard.uri: http://localhost:3000

<span data-ttu-id="ccd93-264">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span><span class="sxs-lookup"><span data-stu-id="ccd93-264">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="ccd93-265">Replace **BASENAME** with the base name you provided in the previous step.</span><span class="sxs-lookup"><span data-stu-id="ccd93-265">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="ccd93-266">You can also use the resource group created previously to select the dashboard and view the URL.</span><span class="sxs-lookup"><span data-stu-id="ccd93-266">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="ccd93-267">Create the HBase table</span><span class="sxs-lookup"><span data-stu-id="ccd93-267">Create the HBase table</span></span>

<span data-ttu-id="ccd93-268">To store data in HBase, we must first create a table.</span><span class="sxs-lookup"><span data-stu-id="ccd93-268">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="ccd93-269">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span><span class="sxs-lookup"><span data-stu-id="ccd93-269">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="ccd93-270">Create the resources outside the topology and use Storm for reading/writing and analytics.</span><span class="sxs-lookup"><span data-stu-id="ccd93-270">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="ccd93-271">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="ccd93-271">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="ccd93-272">For example, if connecting using the `ssh` command, you would use the following syntax:</span><span class="sxs-lookup"><span data-stu-id="ccd93-272">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
        ssh USERNAME@hbase-BASENAME-ssh.azurehdinsight.net
   
    <span data-ttu-id="ccd93-273">In this command, replace **USERNAME** with the SSH user name you provided when creating the cluster, and **BASENAME** with the base name you provided.</span><span class="sxs-lookup"><span data-stu-id="ccd93-273">In this command, replace **USERNAME** with the SSH user name you provided when creating the cluster, and **BASENAME** with the base name you provided.</span></span> <span data-ttu-id="ccd93-274">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="ccd93-274">When prompted, enter the password for the SSH user.</span></span>

2. <span data-ttu-id="ccd93-275">From the SSH session, start the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="ccd93-275">From the SSH session, start the HBase shell.</span></span>
   
        hbase shell
   
    <span data-ttu-id="ccd93-276">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="ccd93-276">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="ccd93-277">From the HBase shell, enter the following command to create a table to store the sensor data:</span><span class="sxs-lookup"><span data-stu-id="ccd93-277">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
        create 'SensorData', 'cf'

4. <span data-ttu-id="ccd93-278">Verify that the table has been created by using the following command:</span><span class="sxs-lookup"><span data-stu-id="ccd93-278">Verify that the table has been created by using the following command:</span></span>
   
        scan 'SensorData'
   
    <span data-ttu-id="ccd93-279">This returns information similar to the following example, indicating that there are 0 rows in the table.</span><span class="sxs-lookup"><span data-stu-id="ccd93-279">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="ccd93-280">Enter `exit` to exit the HBase shell:</span><span class="sxs-lookup"><span data-stu-id="ccd93-280">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="ccd93-281">Configure the HBase bolt</span><span class="sxs-lookup"><span data-stu-id="ccd93-281">Configure the HBase bolt</span></span>

<span data-ttu-id="ccd93-282">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-282">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span> <span data-ttu-id="ccd93-283">This example uses the **hbase-site.xml** file from the HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-283">This example uses the **hbase-site.xml** file from the HBase cluster.</span></span>

### <a name="download-the-hbase-sitexml"></a><span data-ttu-id="ccd93-284">Download the hbase-site.xml</span><span class="sxs-lookup"><span data-stu-id="ccd93-284">Download the hbase-site.xml</span></span>

<span data-ttu-id="ccd93-285">From a command prompt, use SCP to download the **hbase-site.xml** file from the cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-285">From a command prompt, use SCP to download the **hbase-site.xml** file from the cluster.</span></span> <span data-ttu-id="ccd93-286">In the following example, replace **USERNAME** with the SSH user you provided when creating the cluster, and **BASENAME** with the base name you provided earlier.</span><span class="sxs-lookup"><span data-stu-id="ccd93-286">In the following example, replace **USERNAME** with the SSH user you provided when creating the cluster, and **BASENAME** with the base name you provided earlier.</span></span> <span data-ttu-id="ccd93-287">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="ccd93-287">When prompted, enter the password for the SSH user.</span></span> <span data-ttu-id="ccd93-288">Replace the `/path/to/TemperatureMonitor/resources/hbase-site.xml` with the path to this file in the TemperatureMonitor project.</span><span class="sxs-lookup"><span data-stu-id="ccd93-288">Replace the `/path/to/TemperatureMonitor/resources/hbase-site.xml` with the path to this file in the TemperatureMonitor project.</span></span>

    scp USERNAME@hbase-BASENAME-ssh.azurehdinsight.net:/etc/hbase/conf/hbase-site.xml /path/to/TemperatureMonitor/resources/hbase-site.xml

<span data-ttu-id="ccd93-289">This command downloads the **hbase-site.xml** to the path specified.</span><span class="sxs-lookup"><span data-stu-id="ccd93-289">This command downloads the **hbase-site.xml** to the path specified.</span></span>

### <a name="enable-the-hbase-bolt"></a><span data-ttu-id="ccd93-290">Enable the HBase bolt</span><span class="sxs-lookup"><span data-stu-id="ccd93-290">Enable the HBase bolt</span></span>

<span data-ttu-id="ccd93-291">To enable the HBase bolt component, open the **TemperatureMonitor/src/main/java/com/microsoft/examples/Temperature.java** file and uncomment the following lines:</span><span class="sxs-lookup"><span data-stu-id="ccd93-291">To enable the HBase bolt component, open the **TemperatureMonitor/src/main/java/com/microsoft/examples/Temperature.java** file and uncomment the following lines:</span></span>

    // topologyBuilder.setBolt("HBase", new HBaseBolt("SensorData", mapper).withConfigKey("hbase.conf"), spoutConfig.getPartitionCount())
    //  .fieldsGrouping("Parser", "hbasestream", new Fields("deviceid")).setNumTasks(spoutConfig.getPartitionCount());

<span data-ttu-id="ccd93-292">After uncommenting the lines, save the file.</span><span class="sxs-lookup"><span data-stu-id="ccd93-292">After uncommenting the lines, save the file.</span></span>

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="ccd93-293">Build, package, and deploy the solution to HDInsight</span><span class="sxs-lookup"><span data-stu-id="ccd93-293">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="ccd93-294">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-294">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="ccd93-295">From the **TemperatureMonitor** directory, use the following command to perform a new build and create a JAR package from your project:</span><span class="sxs-lookup"><span data-stu-id="ccd93-295">From the **TemperatureMonitor** directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean compile package
   
    <span data-ttu-id="ccd93-296">This command creates a file named **TemperatureMonitor-1.0-SNAPSHOT.jar** in the **target** directory of your project.</span><span class="sxs-lookup"><span data-stu-id="ccd93-296">This command creates a file named **TemperatureMonitor-1.0-SNAPSHOT.jar** in the **target** directory of your project.</span></span>

2. <span data-ttu-id="ccd93-297">Use scp to upload the **TemperatureMonitor-1.0-SNAPSHOT.jar** file to your Storm cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-297">Use scp to upload the **TemperatureMonitor-1.0-SNAPSHOT.jar** file to your Storm cluster.</span></span> <span data-ttu-id="ccd93-298">In the following example, replace **USERNAME** with the SSH user you provided when creating the cluster, and **BASENAME** with the base name you provided earlier.</span><span class="sxs-lookup"><span data-stu-id="ccd93-298">In the following example, replace **USERNAME** with the SSH user you provided when creating the cluster, and **BASENAME** with the base name you provided earlier.</span></span> <span data-ttu-id="ccd93-299">When prompted, enter the password for the SSH user.</span><span class="sxs-lookup"><span data-stu-id="ccd93-299">When prompted, enter the password for the SSH user.</span></span>
   
        scp target/TemperatureMonitor-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:TemperatureMonitor-1.0-SNAPSHOT.jar

   > [!NOTE]
   > <span data-ttu-id="ccd93-300">It may take several minutes to upload the file.</span><span class="sxs-lookup"><span data-stu-id="ccd93-300">It may take several minutes to upload the file.</span></span>

3. <span data-ttu-id="ccd93-301">Once the file has been uploaded, connect to the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="ccd93-301">Once the file has been uploaded, connect to the cluster using SSH.</span></span>
   
        ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net

4. <span data-ttu-id="ccd93-302">To start the topology, use the following command from the SSH session:</span><span class="sxs-lookup"><span data-stu-id="ccd93-302">To start the topology, use the following command from the SSH session:</span></span>
   
        storm jar TemperatureMonitor-1.0-SNAPSHOT.jar com.microsoft.examples.Temperature temperature

5. <span data-ttu-id="ccd93-303">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ccd93-303">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="ccd93-304">You should see the web dashboard update to display the information.</span><span class="sxs-lookup"><span data-stu-id="ccd93-304">You should see the web dashboard update to display the information.</span></span>
   
    ![dashboard](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="ccd93-306">View HBase data</span><span class="sxs-lookup"><span data-stu-id="ccd93-306">View HBase data</span></span>

<span data-ttu-id="ccd93-307">Use the following steps to connect to HBase and verify that the data has been written to the table:</span><span class="sxs-lookup"><span data-stu-id="ccd93-307">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="ccd93-308">Use SSH to connect to the HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="ccd93-308">Use SSH to connect to the HBase cluster.</span></span>
   
        ssh USERNAME@hbase-BASENAME-ssh.azurehdinsight.net

2. <span data-ttu-id="ccd93-309">From the SSH session, start the HBase shell.</span><span class="sxs-lookup"><span data-stu-id="ccd93-309">From the SSH session, start the HBase shell.</span></span>
   
        hbase shell
   
    <span data-ttu-id="ccd93-310">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="ccd93-310">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="ccd93-311">View rows from the table:</span><span class="sxs-lookup"><span data-stu-id="ccd93-311">View rows from the table:</span></span>
   
        scan 'SensorData'
   
    <span data-ttu-id="ccd93-312">This command returns information similar to the following text, indicating that there is data in the table.</span><span class="sxs-lookup"><span data-stu-id="ccd93-312">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="ccd93-313">This scan operation returns a maximum of 10 rows from the table.</span><span class="sxs-lookup"><span data-stu-id="ccd93-313">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="ccd93-314">Delete your clusters</span><span class="sxs-lookup"><span data-stu-id="ccd93-314">Delete your clusters</span></span>
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ccd93-315">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span><span class="sxs-lookup"><span data-stu-id="ccd93-315">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccd93-316">Next steps</span><span class="sxs-lookup"><span data-stu-id="ccd93-316">Next steps</span></span>

<span data-ttu-id="ccd93-317">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="ccd93-317">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="ccd93-318">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="ccd93-318">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="ccd93-319">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-319">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="ccd93-320">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="ccd93-320">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="ccd93-321">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="ccd93-321">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="ccd93-322">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-322">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="ccd93-323">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ccd93-323">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com








