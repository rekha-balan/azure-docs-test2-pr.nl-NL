---
title: Process events from Event Hubs with Storm on HDInsight | Microsoft Docs
description: Learn how to process Event Hubs data with a C# Storm topology created in Visual Studio using the HDInsight Tools for Visual Studio.
services: hdinsight,notification hubs
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ms.openlocfilehash: c03c220afadea12e976603ea2d8b79b16d4162a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551354"
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="43993-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="43993-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="43993-104">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span><span class="sxs-lookup"><span data-stu-id="43993-104">Azure Event Hubs allows you to process massive amounts of data from websites, apps, and devices.</span></span> <span data-ttu-id="43993-105">The Event Hubs spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span><span class="sxs-lookup"><span data-stu-id="43993-105">The Event Hubs spout makes it easy to use Apache Storm on HDInsight to analyze this data in real time.</span></span> <span data-ttu-id="43993-106">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span><span class="sxs-lookup"><span data-stu-id="43993-106">You can also write data to Event Hubs from Storm by using the Event Hubs bolt.</span></span>

<span data-ttu-id="43993-107">In this tutorial, you will learn how to use the Visual Studio templates installed with HDInsight Tools for Visual Studio to create two topologies that work with Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="43993-107">In this tutorial, you will learn how to use the Visual Studio templates installed with HDInsight Tools for Visual Studio to create two topologies that work with Azure Event Hubs.</span></span>

* <span data-ttu-id="43993-108">**EventHubWriter**: Randomly generates data and writes it to Event Hubs</span><span class="sxs-lookup"><span data-stu-id="43993-108">**EventHubWriter**: Randomly generates data and writes it to Event Hubs</span></span>
* <span data-ttu-id="43993-109">**EventHubReader**: Reads data from Event Hubs and logs the data to the Storm logs</span><span class="sxs-lookup"><span data-stu-id="43993-109">**EventHubReader**: Reads data from Event Hubs and logs the data to the Storm logs</span></span>

> [!NOTE]
> <span data-ttu-id="43993-110">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="43993-110">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="43993-111">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="43993-111">SCP.NET</span></span>

<span data-ttu-id="43993-112">These projects use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43993-112">These projects use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43993-113">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="43993-113">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="43993-114">__Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.__</span><span class="sxs-lookup"><span data-stu-id="43993-114">__Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.__</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="43993-115">Cluster versioning</span><span class="sxs-lookup"><span data-stu-id="43993-115">Cluster versioning</span></span>

<span data-ttu-id="43993-116">The Microsoft.SCP.Net.SDK NuGet package used by your project must match the major version of Storm installed on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="43993-116">The Microsoft.SCP.Net.SDK NuGet package used by your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="43993-117">Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, so you must use SCP.NET version 0.10.x.x with these clusters.</span><span class="sxs-lookup"><span data-stu-id="43993-117">Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, so you must use SCP.NET version 0.10.x.x with these clusters.</span></span> <span data-ttu-id="43993-118">HDInsight 3.5 uses Storm 1.0.x., so you must use SCP.NET version 1.0.x.x with this cluster version.</span><span class="sxs-lookup"><span data-stu-id="43993-118">HDInsight 3.5 uses Storm 1.0.x., so you must use SCP.NET version 1.0.x.x with this cluster version.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43993-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="43993-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="43993-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="43993-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

<span data-ttu-id="43993-121">HDInsight 3.4 and greater use Mono to run C# topologies.</span><span class="sxs-lookup"><span data-stu-id="43993-121">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="43993-122">Most things work with Mono.</span><span class="sxs-lookup"><span data-stu-id="43993-122">Most things work with Mono.</span></span> <span data-ttu-id="43993-123">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span><span class="sxs-lookup"><span data-stu-id="43993-123">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

<span data-ttu-id="43993-124">C# topologies must also target .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="43993-124">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="43993-125">How to work with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="43993-125">How to work with Event Hubs</span></span>

<span data-ttu-id="43993-126">Microsoft provides a set of Java components that can be used to communicate with Azure Event Hubs from a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="43993-126">Microsoft provides a set of Java components that can be used to communicate with Azure Event Hubs from a Storm topology.</span></span> <span data-ttu-id="43993-127">You can find the jar file that contains the latest version of these components at [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="43993-127">You can find the jar file that contains the latest version of these components at [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="43993-128">While the components are written in Java, you can easily use them from a C# topology.</span><span class="sxs-lookup"><span data-stu-id="43993-128">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="43993-129">The components following components are used in this example:</span><span class="sxs-lookup"><span data-stu-id="43993-129">The components following components are used in this example:</span></span>

* <span data-ttu-id="43993-130">__EventHubSpout__: Reads data from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="43993-130">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="43993-131">__EventHubBolt__: Writes data to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="43993-131">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="43993-132">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="43993-132">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="43993-133">__EventHubBoltConfig__: Used to configure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="43993-133">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>
* <span data-ttu-id="43993-134">__UnicodeEventDataScheme__: Used to configure the spout to use UTF-8 encoding when reading from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="43993-134">__UnicodeEventDataScheme__: Used to configure the spout to use UTF-8 encoding when reading from Event Hubs.</span></span> <span data-ttu-id="43993-135">The default encoding is String.</span><span class="sxs-lookup"><span data-stu-id="43993-135">The default encoding is String.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="43993-136">Example Spout usage</span><span class="sxs-lookup"><span data-stu-id="43993-136">Example Spout usage</span></span>

<span data-ttu-id="43993-137">SCP.NET provides methods for adding an EventHubSpout to your topology.</span><span class="sxs-lookup"><span data-stu-id="43993-137">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="43993-138">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span><span class="sxs-lookup"><span data-stu-id="43993-138">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="43993-139">The following example demonstrates how to create a spout using the __SetEventHubSpout__ and EventHubSpoutConfig methods provided by SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="43993-139">The following example demonstrates how to create a spout using the __SetEventHubSpout__ and EventHubSpoutConfig methods provided by SCP.NET:</span></span>

```csharp
topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        // the shared access signature name and key used to read the data
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        // The namespace that contains the Event Hub to read from
        ConfigurationManager.AppSettings["EventHubNamespace"],
        // The Event Hub name to read from
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        // The number of partitions in the Event Hub
        eventHubPartitions),
    // Parallelism hint for this component. Should be set to the partition count.
    eventHubPartitions);
```

<span data-ttu-id="43993-140">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an Event Hub.</span><span class="sxs-lookup"><span data-stu-id="43993-140">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an Event Hub.</span></span> <span data-ttu-id="43993-141">The parallelism hint for the component is set to the number of partitions in the Event Hub.</span><span class="sxs-lookup"><span data-stu-id="43993-141">The parallelism hint for the component is set to the number of partitions in the Event Hub.</span></span> <span data-ttu-id="43993-142">This setting allows Storm to create an instance of the component for each partition.</span><span class="sxs-lookup"><span data-stu-id="43993-142">This setting allows Storm to create an instance of the component for each partition.</span></span>

> [!WARNING]
> <span data-ttu-id="43993-143">As of January 1st, 2017, using the SetEventHubSpout and EventHubSpoutConfig methods create a spout that uses String encoding when reading data from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="43993-143">As of January 1st, 2017, using the SetEventHubSpout and EventHubSpoutConfig methods create a spout that uses String encoding when reading data from Event Hubs.</span></span>

<span data-ttu-id="43993-144">You can also use the generic JavaComponentConstructor method when creating a spout.</span><span class="sxs-lookup"><span data-stu-id="43993-144">You can also use the generic JavaComponentConstructor method when creating a spout.</span></span> <span data-ttu-id="43993-145">The following example demonstrates how to create a spout using the JavaComponentConstructor method.</span><span class="sxs-lookup"><span data-stu-id="43993-145">The following example demonstrates how to create a spout using the JavaComponentConstructor method.</span></span> <span data-ttu-id="43993-146">It also demonstrates how to configure the spout to read data using a UTF-8 encoding instead of String.</span><span class="sxs-lookup"><span data-stu-id="43993-146">It also demonstrates how to configure the spout to read data using a UTF-8 encoding instead of String.</span></span>

```csharp
// Create an instance of UnicodeEventDataScheme
var schemeConstructor = new JavaComponentConstructor("com.microsoft.eventhubs.spout.UnicodeEventDataScheme");
// Create an instance of EventHubSpoutConfig
var eventHubSpoutConfig = new JavaComponentConstructor(
    "com.microsoft.eventhubs.spout.EventHubSpoutConfig",
    new List<Tuple<string, object>>()
    {
        // the shared access signature name and key used to read the data
        Tuple.Create<string, object>(JavaComponentConstructor.JAVA_LANG_STRING, ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"]),
        Tuple.Create<string, object>(JavaComponentConstructor.JAVA_LANG_STRING, ConfigurationManager.AppSettings["EventHubSharedAccessKey"]),
        // The namespace that contains the Event Hub to read from
        Tuple.Create<string, object>(JavaComponentConstructor.JAVA_LANG_STRING, ConfigurationManager.AppSettings["EventHubNamespace"]),
        // The Event Hub name to read from
        Tuple.Create<string, object>(JavaComponentConstructor.JAVA_LANG_STRING, ConfigurationManager.AppSettings["EventHubEntityPath"]),
        // The number of partitions in the Event Hub
        Tuple.Create<string, object>("int", eventHubPartitions),
        // The encoding scheme to use when reading
        Tuple.Create<string, object>("com.microsoft.eventhubs.spout.IEventDataScheme", schemeConstructor)
    }
    );
// Create an instance of the spout
var eventHubSpout = new JavaComponentConstructor(
    "com.microsoft.eventhubs.spout.EventHubSpout",
    new List<Tuple<string, object>>()
    {
        Tuple.Create<string, object>("com.microsoft.eventhubs.spout.EventHubSpoutConfig", eventHubSpoutConfig)
    }
    );
// Set the spout in the topology
topologyBuilder.SetJavaSpout("EventHubSpout", eventHubSpout, eventHubPartitions);
```

> [!IMPORTANT]
> <span data-ttu-id="43993-147">UnicodeEventDataScheme is only available in the 9.5 version of the Event Hub components, which is available from [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="43993-147">UnicodeEventDataScheme is only available in the 9.5 version of the Event Hub components, which is available from [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="43993-148">Example Bolt usage</span><span class="sxs-lookup"><span data-stu-id="43993-148">Example Bolt usage</span></span>

<span data-ttu-id="43993-149">Use the JavaComponmentConstructor method to create an instance of the bolt.</span><span class="sxs-lookup"><span data-stu-id="43993-149">Use the JavaComponmentConstructor method to create an instance of the bolt.</span></span> <span data-ttu-id="43993-150">The following example demonstrates how to create and configure a new instance of the EventHubBolt:</span><span class="sxs-lookup"><span data-stu-id="43993-150">The following example demonstrates how to create and configure a new instance of the EventHubBolt:</span></span>

```csharp
//Create constructor for the Java bolt
JavaComponentConstructor constructor =
    // Use a Clojure expression to create the EventHubBoltCOnfig
    JavaComponentConstructor.CreateFromClojureExpr(
        String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
    // The policy name and key used to read from Event Hubs
    ConfigurationManager.AppSettings["EventHubPolicyName"],
    ConfigurationManager.AppSettings["EventHubPolicyKey"],
    // The namespace that contains the Event Hub
    ConfigurationManager.AppSettings["EventHubNamespace"],
    "servicebus.windows.net", //suffix for the namespace fqdn
    // The Evetn Hub Name)
    ConfigurationManager.AppSettings["EventHubName"],
    "true"));

//Set the bolt
topologyBuilder.SetJavaBolt(
        "EventHubBolt",
        constructor,
        partitionCount). //Parallelism hint uses partition count
    shuffleGrouping("Spout"); //Consume data from spout
```

> [!NOTE]
> <span data-ttu-id="43993-151">This example uses a Clojure expression passed as a string, instead of using JavaComponentConstructor to create an EventHubBoltConfig as the Spout example did.</span><span class="sxs-lookup"><span data-stu-id="43993-151">This example uses a Clojure expression passed as a string, instead of using JavaComponentConstructor to create an EventHubBoltConfig as the Spout example did.</span></span> <span data-ttu-id="43993-152">Either method works.</span><span class="sxs-lookup"><span data-stu-id="43993-152">Either method works.</span></span> <span data-ttu-id="43993-153">Use the method that feels best to you.</span><span class="sxs-lookup"><span data-stu-id="43993-153">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="43993-154">Download the completed project</span><span class="sxs-lookup"><span data-stu-id="43993-154">Download the completed project</span></span>

<span data-ttu-id="43993-155">You can download a complete version of the project created in this tutorial from GitHub: [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="43993-155">You can download a complete version of the project created in this tutorial from GitHub: [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="43993-156">However, you still need to provide configuration settings by following the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="43993-156">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="43993-157">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="43993-157">Prerequisites</span></span>

* <span data-ttu-id="43993-158">An [Apache Storm on HDInsight cluster version 3.5](hdinsight-apache-storm-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="43993-158">An [Apache Storm on HDInsight cluster version 3.5](hdinsight-apache-storm-tutorial-get-started.md)</span></span>

    > [!WARNING]
    > <span data-ttu-id="43993-159">The example used in this document requires Storm on HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="43993-159">The example used in this document requires Storm on HDInsight version 3.5.</span></span> <span data-ttu-id="43993-160">This will not work with older versions of HDInsight due to breaking class name changes.</span><span class="sxs-lookup"><span data-stu-id="43993-160">This will not work with older versions of HDInsight due to breaking class name changes.</span></span> <span data-ttu-id="43993-161">For a version of this example that works with older clusters, see [https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="43993-161">For a version of this example that works with older clusters, see [https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="43993-162">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span><span class="sxs-lookup"><span data-stu-id="43993-162">An [Azure Event Hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)</span></span>

* <span data-ttu-id="43993-163">The [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="43993-163">The [Azure .NET SDK](http://azure.microsoft.com/downloads/)</span></span>

* <span data-ttu-id="43993-164">The [HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="43993-164">The [HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)</span></span>

* <span data-ttu-id="43993-165">Java JDK 1.7 greater on your development environment.</span><span class="sxs-lookup"><span data-stu-id="43993-165">Java JDK 1.7 greater on your development environment.</span></span> <span data-ttu-id="43993-166">JDK downloads are available from [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="43993-166">JDK downloads are available from [http://www.oracle.com/technetwork/java/javase/downloads/index.html](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="43993-167">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span><span class="sxs-lookup"><span data-stu-id="43993-167">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="43993-168">The **%JAVA_HOME%/bin** directory must be in the path</span><span class="sxs-lookup"><span data-stu-id="43993-168">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="download-the-event-hub-components"></a><span data-ttu-id="43993-169">Download the Event Hub components</span><span class="sxs-lookup"><span data-stu-id="43993-169">Download the Event Hub components</span></span>

<span data-ttu-id="43993-170">The spout and bolt are distributed as a single Java archive (.jar) file named **eventhubs-storm-spout-#.#-jar-with-dependencies.jar**, where #.# is the version of the file.</span><span class="sxs-lookup"><span data-stu-id="43993-170">The spout and bolt are distributed as a single Java archive (.jar) file named **eventhubs-storm-spout-#.#-jar-with-dependencies.jar**, where #.# is the version of the file.</span></span>

<span data-ttu-id="43993-171">To use this solution with HDInsight 3.5, use the version 0.9.5 jar file from  [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span><span class="sxs-lookup"><span data-stu-id="43993-171">To use this solution with HDInsight 3.5, use the version 0.9.5 jar file from  [https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/lib/eventhubs/).</span></span>

<span data-ttu-id="43993-172">Create a directory named `eventhubspout` and save the file into the directory.</span><span class="sxs-lookup"><span data-stu-id="43993-172">Create a directory named `eventhubspout` and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="43993-173">Configure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="43993-173">Configure Event Hubs</span></span>

<span data-ttu-id="43993-174">Event Hubs is the data source for this example.</span><span class="sxs-lookup"><span data-stu-id="43993-174">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="43993-175">Use the information in the **Create an Event Hub** section of the [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md) document.</span><span class="sxs-lookup"><span data-stu-id="43993-175">Use the information in the **Create an Event Hub** section of the [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md) document.</span></span>

1. <span data-ttu-id="43993-176">After the event hub has been created, view the EventHub blade in the Azure portal and select **Shared access Policies**.</span><span class="sxs-lookup"><span data-stu-id="43993-176">After the event hub has been created, view the EventHub blade in the Azure portal and select **Shared access Policies**.</span></span> <span data-ttu-id="43993-177">Select **+ Add** to add the following policies:</span><span class="sxs-lookup"><span data-stu-id="43993-177">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="43993-178">Name</span><span class="sxs-lookup"><span data-stu-id="43993-178">Name</span></span> | <span data-ttu-id="43993-179">Permissions</span><span class="sxs-lookup"><span data-stu-id="43993-179">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="43993-180">writer</span><span class="sxs-lookup"><span data-stu-id="43993-180">writer</span></span> |<span data-ttu-id="43993-181">Send</span><span class="sxs-lookup"><span data-stu-id="43993-181">Send</span></span> |
   | <span data-ttu-id="43993-182">reader</span><span class="sxs-lookup"><span data-stu-id="43993-182">reader</span></span> |<span data-ttu-id="43993-183">Listen</span><span class="sxs-lookup"><span data-stu-id="43993-183">Listen</span></span> |

    ![policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="43993-185">Select the **reader** and **writer** policies.</span><span class="sxs-lookup"><span data-stu-id="43993-185">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="43993-186">Copy and save the **PRIMARY KEY** value for both policies, as these values are used later.</span><span class="sxs-lookup"><span data-stu-id="43993-186">Copy and save the **PRIMARY KEY** value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="43993-187">Configure the EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="43993-187">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="43993-188">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="43993-188">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="43993-189">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="43993-189">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="43993-190">In the **EventHubWriter** project, open the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="43993-190">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="43993-191">Use the information from the Event Hub you configured earlier to fill in the value for the following keys:</span><span class="sxs-lookup"><span data-stu-id="43993-191">Use the information from the Event Hub you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="43993-192">Key</span><span class="sxs-lookup"><span data-stu-id="43993-192">Key</span></span> | <span data-ttu-id="43993-193">Value</span><span class="sxs-lookup"><span data-stu-id="43993-193">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="43993-194">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="43993-194">EventHubPolicyName</span></span> |<span data-ttu-id="43993-195">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span><span class="sxs-lookup"><span data-stu-id="43993-195">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="43993-196">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="43993-196">EventHubPolicyKey</span></span> |<span data-ttu-id="43993-197">The key for the writer policy</span><span class="sxs-lookup"><span data-stu-id="43993-197">The key for the writer policy</span></span> |
   | <span data-ttu-id="43993-198">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="43993-198">EventHubNamespace</span></span> |<span data-ttu-id="43993-199">The namespace that contains your Event Hub</span><span class="sxs-lookup"><span data-stu-id="43993-199">The namespace that contains your Event Hub</span></span> |
   | <span data-ttu-id="43993-200">EventHubName</span><span class="sxs-lookup"><span data-stu-id="43993-200">EventHubName</span></span> |<span data-ttu-id="43993-201">Your Event Hub name</span><span class="sxs-lookup"><span data-stu-id="43993-201">Your Event Hub name</span></span> |
   | <span data-ttu-id="43993-202">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="43993-202">EventHubPartitionCount</span></span> |<span data-ttu-id="43993-203">The number of partitions in your Event Hub</span><span class="sxs-lookup"><span data-stu-id="43993-203">The number of partitions in your Event Hub</span></span> |

4. <span data-ttu-id="43993-204">Save and close the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="43993-204">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="43993-205">Configure the EventHubReader</span><span class="sxs-lookup"><span data-stu-id="43993-205">Configure the EventHubReader</span></span>

1. <span data-ttu-id="43993-206">Open the **EventHubReader** project.</span><span class="sxs-lookup"><span data-stu-id="43993-206">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="43993-207">Open the **App.config** for the **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="43993-207">Open the **App.config** for the **EventHubReader**.</span></span> <span data-ttu-id="43993-208">Use the information from the Event Hub you configured earlier to fill in the value for the following keys:</span><span class="sxs-lookup"><span data-stu-id="43993-208">Use the information from the Event Hub you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="43993-209">Key</span><span class="sxs-lookup"><span data-stu-id="43993-209">Key</span></span> | <span data-ttu-id="43993-210">Value</span><span class="sxs-lookup"><span data-stu-id="43993-210">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="43993-211">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="43993-211">EventHubPolicyName</span></span> |<span data-ttu-id="43993-212">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span><span class="sxs-lookup"><span data-stu-id="43993-212">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="43993-213">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="43993-213">EventHubPolicyKey</span></span> |<span data-ttu-id="43993-214">The key for the reader policy</span><span class="sxs-lookup"><span data-stu-id="43993-214">The key for the reader policy</span></span> |
   | <span data-ttu-id="43993-215">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="43993-215">EventHubNamespace</span></span> |<span data-ttu-id="43993-216">The namespace that contains your Event Hub</span><span class="sxs-lookup"><span data-stu-id="43993-216">The namespace that contains your Event Hub</span></span> |
   | <span data-ttu-id="43993-217">EventHubName</span><span class="sxs-lookup"><span data-stu-id="43993-217">EventHubName</span></span> |<span data-ttu-id="43993-218">Your Event Hub name</span><span class="sxs-lookup"><span data-stu-id="43993-218">Your Event Hub name</span></span> |
   | <span data-ttu-id="43993-219">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="43993-219">EventHubPartitionCount</span></span> |<span data-ttu-id="43993-220">The number of partitions in your Event Hub</span><span class="sxs-lookup"><span data-stu-id="43993-220">The number of partitions in your Event Hub</span></span> |

3. <span data-ttu-id="43993-221">Save and close the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="43993-221">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="43993-222">Deploy the topologies</span><span class="sxs-lookup"><span data-stu-id="43993-222">Deploy the topologies</span></span>

1. <span data-ttu-id="43993-223">From **Solution Explorer**, right-click the **EventHubReader** project and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="43993-223">From **Solution Explorer**, right-click the **EventHubReader** project and select **Submit to Storm on HDInsight**.</span></span>

    ![submit to storm](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="43993-225">On the **Submit Topology** screen, select your **Storm Cluster**.</span><span class="sxs-lookup"><span data-stu-id="43993-225">On the **Submit Topology** screen, select your **Storm Cluster**.</span></span> <span data-ttu-id="43993-226">Expand **Additional Configurations**, select **Java File Paths**, select **...** and select the directory that contains the jar file that you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="43993-226">Expand **Additional Configurations**, select **Java File Paths**, select **...** and select the directory that contains the jar file that you downloaded earlier.</span></span> <span data-ttu-id="43993-227">Finally, click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="43993-227">Finally, click **Submit**.</span></span>

    ![Image of submission dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="43993-229">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span><span class="sxs-lookup"><span data-stu-id="43993-229">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="43993-230">To view information about the topology, select the **EventHubReader** topology in the left pane.</span><span class="sxs-lookup"><span data-stu-id="43993-230">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![example storage view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="43993-232">From **Solution Explorer**, right-click the **EventHubWriter** project and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="43993-232">From **Solution Explorer**, right-click the **EventHubWriter** project and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="43993-233">On the **Submit Topology** screen, select your **Storm Cluster**.</span><span class="sxs-lookup"><span data-stu-id="43993-233">On the **Submit Topology** screen, select your **Storm Cluster**.</span></span> <span data-ttu-id="43993-234">Expand **Additional Configurations**, select **Java File Paths**, select **...** and select the directory that contains the jar file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="43993-234">Expand **Additional Configurations**, select **Java File Paths**, select **...** and select the directory that contains the jar file you downloaded earlier.</span></span> <span data-ttu-id="43993-235">Finally, click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="43993-235">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="43993-236">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="43993-236">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="43993-237">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span><span class="sxs-lookup"><span data-stu-id="43993-237">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="43993-238">To open the **Component Summary** for the bolt, double-click the **LogBolt** component in the diagram.</span><span class="sxs-lookup"><span data-stu-id="43993-238">To open the **Component Summary** for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="43993-239">In the **Executors** section, select one of the links in the **Port** column.</span><span class="sxs-lookup"><span data-stu-id="43993-239">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="43993-240">This will display information logged by the component.</span><span class="sxs-lookup"><span data-stu-id="43993-240">This will display information logged by the component.</span></span> <span data-ttu-id="43993-241">The logged information is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="43993-241">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="43993-242">Stop the topologies</span><span class="sxs-lookup"><span data-stu-id="43993-242">Stop the topologies</span></span>

<span data-ttu-id="43993-243">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span><span class="sxs-lookup"><span data-stu-id="43993-243">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![image of killing a topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="43993-245">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="43993-245">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="43993-246">Next Steps</span><span class="sxs-lookup"><span data-stu-id="43993-246">Next Steps</span></span>

<span data-ttu-id="43993-247">In this document, you have learned how to use the Java Event Hubs Spout and Bolt from a C# topology to work with data in Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="43993-247">In this document, you have learned how to use the Java Event Hubs Spout and Bolt from a C# topology to work with data in Azure Event Hub.</span></span> <span data-ttu-id="43993-248">To learn more about creating C# topologies, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="43993-248">To learn more about creating C# topologies, see the following documents:</span></span>

* [<span data-ttu-id="43993-249">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="43993-249">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="43993-250">SCP programming guide</span><span class="sxs-lookup"><span data-stu-id="43993-250">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="43993-251">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="43993-251">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)





