---
title: Process events from Event Hubs with Storm - Azure HDInsight
description: Learn how to process data from Azure Event Hubs with a C# Storm topology created in Visual Studio, by using the HDInsight tools for Visual Studio.
services: hdinsight,notification hubs
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 11/27/2017
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: 7c37abe709559fc0628b94ba50634673c08af375
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870640"
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="d1d3c-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="d1d3c-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="d1d3c-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="d1d3c-105">This document uses a C# Storm topology to read and write data from Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d1d3c-105">This document uses a C# Storm topology to read and write data from Event Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="d1d3c-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](https://azure.microsoft.com/resources/samples/hdinsight-java-storm-eventhub/).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](https://azure.microsoft.com/resources/samples/hdinsight-java-storm-eventhub/).</span></span>

## <a name="scpnet"></a><span data-ttu-id="d1d3c-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="d1d3c-107">SCP.NET</span></span>

<span data-ttu-id="d1d3c-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d3c-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d1d3c-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="d1d3c-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="d1d3c-112">The example used in this document works with HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="d1d3c-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="d1d3c-114">Cluster versioning</span><span class="sxs-lookup"><span data-stu-id="d1d3c-114">Cluster versioning</span></span>

<span data-ttu-id="d1d3c-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="d1d3c-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d3c-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="d1d3c-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d1d3c-119">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-119">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="d1d3c-120">C# topologies must also target .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="d1d3c-121">How to work with Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d1d3c-121">How to work with Event Hubs</span></span>

<span data-ttu-id="d1d3c-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="d1d3c-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d1d3c-124">While the components are written in Java, you can easily use them from a C# topology.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="d1d3c-125">The following components are used in this example:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-125">The following components are used in this example:</span></span>

* <span data-ttu-id="d1d3c-126">__EventHubSpout__: Reads data from Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="d1d3c-127">__EventHubBolt__: Writes data to Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="d1d3c-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="d1d3c-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="d1d3c-130">Example spout usage</span><span class="sxs-lookup"><span data-stu-id="d1d3c-130">Example spout usage</span></span>

<span data-ttu-id="d1d3c-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="d1d3c-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="d1d3c-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="d1d3c-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="d1d3c-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="d1d3c-136">This setting allows Storm to create an instance of the component for each partition.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="d1d3c-137">Example bolt usage</span><span class="sxs-lookup"><span data-stu-id="d1d3c-137">Example bolt usage</span></span>

<span data-ttu-id="d1d3c-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="d1d3c-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="d1d3c-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="d1d3c-141">Either method works.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-141">Either method works.</span></span> <span data-ttu-id="d1d3c-142">Use the method that feels best to you.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="d1d3c-143">Download the completed project</span><span class="sxs-lookup"><span data-stu-id="d1d3c-143">Download the completed project</span></span>

<span data-ttu-id="d1d3c-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="d1d3c-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="d1d3c-146">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1d3c-146">Prerequisites</span></span>

* <span data-ttu-id="d1d3c-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](apache-storm-tutorial-get-started-linux.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="d1d3c-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="d1d3c-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="d1d3c-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="d1d3c-151">An [Azure event hub](../../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-151">An [Azure event hub](../../event-hubs/event-hubs-create.md).</span></span>

* <span data-ttu-id="d1d3c-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="d1d3c-153">The [HDInsight tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-153">The [HDInsight tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="d1d3c-154">Java JDK 1.8 or later on your development environment.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="d1d3c-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="d1d3c-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="d1d3c-157">The **%JAVA_HOME%/bin** directory must be in the path.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="d1d3c-158">Download the Event Hubs components</span><span class="sxs-lookup"><span data-stu-id="d1d3c-158">Download the Event Hubs components</span></span>

<span data-ttu-id="d1d3c-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="d1d3c-160">Create a directory named `eventhubspout`, and save the file into the directory.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="d1d3c-161">Configure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="d1d3c-161">Configure Event Hubs</span></span>

<span data-ttu-id="d1d3c-162">Event Hubs is the data source for this example.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="d1d3c-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../../event-hubs/event-hubs-create.md).</span></span>

1. <span data-ttu-id="d1d3c-164">After the event hub has been created, view the **EventHub** settings in the Azure portal, and select **Shared access policies**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-164">After the event hub has been created, view the **EventHub** settings in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="d1d3c-165">Select **+ Add** to add the following policies:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="d1d3c-166">Name</span><span class="sxs-lookup"><span data-stu-id="d1d3c-166">Name</span></span> | <span data-ttu-id="d1d3c-167">Permissions</span><span class="sxs-lookup"><span data-stu-id="d1d3c-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1d3c-168">writer</span><span class="sxs-lookup"><span data-stu-id="d1d3c-168">writer</span></span> |<span data-ttu-id="d1d3c-169">Send</span><span class="sxs-lookup"><span data-stu-id="d1d3c-169">Send</span></span> |
   | <span data-ttu-id="d1d3c-170">reader</span><span class="sxs-lookup"><span data-stu-id="d1d3c-170">reader</span></span> |<span data-ttu-id="d1d3c-171">Listen</span><span class="sxs-lookup"><span data-stu-id="d1d3c-171">Listen</span></span> |

    ![Screenshot of Share access policies window](./media/apache-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="d1d3c-173">Select the **reader** and **writer** policies.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="d1d3c-174">Copy and save the primary key value for both policies, as these values are used later.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="d1d3c-175">Configure the EventHubWriter</span><span class="sxs-lookup"><span data-stu-id="d1d3c-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="d1d3c-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="d1d3c-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="d1d3c-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="d1d3c-178">In the **EventHubWriter** project, open the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="d1d3c-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="d1d3c-180">Key</span><span class="sxs-lookup"><span data-stu-id="d1d3c-180">Key</span></span> | <span data-ttu-id="d1d3c-181">Value</span><span class="sxs-lookup"><span data-stu-id="d1d3c-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1d3c-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="d1d3c-182">EventHubPolicyName</span></span> |<span data-ttu-id="d1d3c-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span><span class="sxs-lookup"><span data-stu-id="d1d3c-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="d1d3c-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="d1d3c-184">EventHubPolicyKey</span></span> |<span data-ttu-id="d1d3c-185">The key for the writer policy.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="d1d3c-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="d1d3c-186">EventHubNamespace</span></span> |<span data-ttu-id="d1d3c-187">The namespace that contains your event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="d1d3c-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="d1d3c-188">EventHubName</span></span> |<span data-ttu-id="d1d3c-189">Your event hub name.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-189">Your event hub name.</span></span> |
   | <span data-ttu-id="d1d3c-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="d1d3c-190">EventHubPartitionCount</span></span> |<span data-ttu-id="d1d3c-191">The number of partitions in your event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="d1d3c-192">Save and close the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="d1d3c-193">Configure the EventHubReader</span><span class="sxs-lookup"><span data-stu-id="d1d3c-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="d1d3c-194">Open the **EventHubReader** project.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="d1d3c-195">Open the **App.config** file for the **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="d1d3c-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="d1d3c-197">Key</span><span class="sxs-lookup"><span data-stu-id="d1d3c-197">Key</span></span> | <span data-ttu-id="d1d3c-198">Value</span><span class="sxs-lookup"><span data-stu-id="d1d3c-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="d1d3c-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="d1d3c-199">EventHubPolicyName</span></span> |<span data-ttu-id="d1d3c-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span><span class="sxs-lookup"><span data-stu-id="d1d3c-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="d1d3c-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="d1d3c-201">EventHubPolicyKey</span></span> |<span data-ttu-id="d1d3c-202">The key for the reader policy.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="d1d3c-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="d1d3c-203">EventHubNamespace</span></span> |<span data-ttu-id="d1d3c-204">The namespace that contains your event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="d1d3c-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="d1d3c-205">EventHubName</span></span> |<span data-ttu-id="d1d3c-206">Your event hub name.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-206">Your event hub name.</span></span> |
   | <span data-ttu-id="d1d3c-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="d1d3c-207">EventHubPartitionCount</span></span> |<span data-ttu-id="d1d3c-208">The number of partitions in your event hub.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="d1d3c-209">Save and close the **App.config** file.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="d1d3c-210">Deploy the topologies</span><span class="sxs-lookup"><span data-stu-id="d1d3c-210">Deploy the topologies</span></span>

1. <span data-ttu-id="d1d3c-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Screenshot of Solution Explorer, with Submit to Storm on HDInsight highlighted](./media/apache-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="d1d3c-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="d1d3c-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="d1d3c-215">Finally, click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-215">Finally, click **Submit**.</span></span>

    ![Screenshot of Submit Topology dialog box](./media/apache-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="d1d3c-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="d1d3c-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Screenshot of Storm Topologies Viewer](./media/apache-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="d1d3c-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="d1d3c-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="d1d3c-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="d1d3c-223">Finally, click **Submit**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="d1d3c-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="d1d3c-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="d1d3c-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="d1d3c-227">In the **Executors** section, select one of the links in the **Port** column.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="d1d3c-228">This displays information logged by the component.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-228">This displays information logged by the component.</span></span> <span data-ttu-id="d1d3c-229">The logged information is similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="d1d3c-230">Stop the topologies</span><span class="sxs-lookup"><span data-stu-id="d1d3c-230">Stop the topologies</span></span>

<span data-ttu-id="d1d3c-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Screenshot of Storm Topology Viewer, with Kill button highlighted](./media/apache-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="d1d3c-233">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="d1d3c-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="d1d3c-234">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1d3c-234">Next steps</span></span>

<span data-ttu-id="d1d3c-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="d1d3c-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="d1d3c-236">To learn more about creating C# topologies, see the following:</span><span class="sxs-lookup"><span data-stu-id="d1d3c-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="d1d3c-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d1d3c-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](apache-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="d1d3c-238">SCP programming guide</span><span class="sxs-lookup"><span data-stu-id="d1d3c-238">SCP programming guide</span></span>](apache-storm-scp-programming-guide.md)
* [<span data-ttu-id="d1d3c-239">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="d1d3c-239">Example topologies for Storm on HDInsight</span></span>](apache-storm-example-topology.md)
