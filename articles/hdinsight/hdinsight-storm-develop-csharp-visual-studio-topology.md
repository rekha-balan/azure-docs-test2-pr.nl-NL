---
title: Apache Storm topologies with Visual Studio and C#  | Microsoft Docs
description: Learn how to create Storm topologies in C# by creating a simple word count topology in Visual Studio using the HDInsight Tools for Visual Studio.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ms.openlocfilehash: 78c952d82e28a201dbf01bd3c03f983f2dedb229
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554003"
---
# <a name="develop-c-topologies-for-apache-storm-on-hdinsight-using-hadoop-tools-for-visual-studio"></a><span data-ttu-id="3c1a8-103">Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3c1a8-103">Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio</span></span>

<span data-ttu-id="3c1a8-104">Learn how to create a C# Storm topology by using the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-104">Learn how to create a C# Storm topology by using the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="3c1a8-105">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-105">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on HDInsight cluster.</span></span>

<span data-ttu-id="3c1a8-106">You also learn how to create hybrid topologies that use C# and Java components.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-106">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c1a8-107">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-107">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="3c1a8-108">__Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies__.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-108">__Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies__.</span></span>
>
> <span data-ttu-id="3c1a8-109">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-109">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="3c1a8-110">The version of the package must also match the major version of Storm installed on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="3c1a8-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="3c1a8-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="3c1a8-113">Most things work, however you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-113">Most things work, however you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3c1a8-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3c1a8-114">Prerequisites</span></span>

* <span data-ttu-id="3c1a8-115">[Java](https://java.com) 1.7 or greater on your development environment.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-115">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="3c1a8-116">Java is used to package the topology when it is submitted to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-116">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="3c1a8-117">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-117">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="3c1a8-118">The **%JAVA_HOME%/bin** directory must be in the path</span><span class="sxs-lookup"><span data-stu-id="3c1a8-118">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

* <span data-ttu-id="3c1a8-119">One of the following versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-119">One of the following versions of Visual Studio:</span></span>

  * <span data-ttu-id="3c1a8-120">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="3c1a8-120">Visual Studio 2012 with [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="3c1a8-121">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="3c1a8-121">Visual Studio 2013 with [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>
  * <span data-ttu-id="3c1a8-122">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="3c1a8-122">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>
  * <span data-ttu-id="3c1a8-123">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="3c1a8-123">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="3c1a8-124">Azure SDK 2.9.5 or later</span><span class="sxs-lookup"><span data-stu-id="3c1a8-124">Azure SDK 2.9.5 or later</span></span>

* <span data-ttu-id="3c1a8-125">HDInsight Tools for Visual Studio: See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-125">HDInsight Tools for Visual Studio: See [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) to install and configure the HDInsight tools for Visual Studio.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3c1a8-126">HDInsight Tools for Visual Studio are not supported on Visual Studio Express</span><span class="sxs-lookup"><span data-stu-id="3c1a8-126">HDInsight Tools for Visual Studio are not supported on Visual Studio Express</span></span>

* <span data-ttu-id="3c1a8-127">Apache Storm on HDInsight cluster: See [Getting started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-127">Apache Storm on HDInsight cluster: See [Getting started with Apache Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started.md) for steps to create a cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3c1a8-128">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-128">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3c1a8-129">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-129">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

## <a name="templates"></a><span data-ttu-id="3c1a8-130">Templates</span><span class="sxs-lookup"><span data-stu-id="3c1a8-130">Templates</span></span>

<span data-ttu-id="3c1a8-131">The HDInsight Tools for Visual Studio provide the following templates:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-131">The HDInsight Tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="3c1a8-132">Project type</span><span class="sxs-lookup"><span data-stu-id="3c1a8-132">Project type</span></span> | <span data-ttu-id="3c1a8-133">Demonstrates</span><span class="sxs-lookup"><span data-stu-id="3c1a8-133">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="3c1a8-134">Storm Application</span><span class="sxs-lookup"><span data-stu-id="3c1a8-134">Storm Application</span></span> |<span data-ttu-id="3c1a8-135">An empty Storm topology project</span><span class="sxs-lookup"><span data-stu-id="3c1a8-135">An empty Storm topology project</span></span> |
| <span data-ttu-id="3c1a8-136">Storm Azure SQL Writer Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-136">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="3c1a8-137">How to write to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3c1a8-137">How to write to Azure SQL Database</span></span> |
| <span data-ttu-id="3c1a8-138">Storm DocumentDB Reader Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-138">Storm DocumentDB Reader Sample</span></span> |<span data-ttu-id="3c1a8-139">How to read from Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3c1a8-139">How to read from Azure DocumentDB</span></span> |
| <span data-ttu-id="3c1a8-140">Storm DocumentDB Writer Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-140">Storm DocumentDB Writer Sample</span></span> |<span data-ttu-id="3c1a8-141">How to write to Azure DocumentDB</span><span class="sxs-lookup"><span data-stu-id="3c1a8-141">How to write to Azure DocumentDB</span></span> |
| <span data-ttu-id="3c1a8-142">Storm EventHub Reader Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-142">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="3c1a8-143">How to read from Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3c1a8-143">How to read from Azure Event Hubs</span></span> |
| <span data-ttu-id="3c1a8-144">Storm EventHub Writer Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-144">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="3c1a8-145">How to write to Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3c1a8-145">How to write to Azure Event Hubs</span></span> |
| <span data-ttu-id="3c1a8-146">Storm HBase Reader Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-146">Storm HBase Reader Sample</span></span> |<span data-ttu-id="3c1a8-147">How to read from HBase on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="3c1a8-147">How to read from HBase on HDInsight clusters</span></span> |
| <span data-ttu-id="3c1a8-148">Storm HBase Writer Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-148">Storm HBase Writer Sample</span></span> |<span data-ttu-id="3c1a8-149">How to write to HBase on HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="3c1a8-149">How to write to HBase on HDInsight clusters</span></span> |
| <span data-ttu-id="3c1a8-150">Storm Hybrid Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-150">Storm Hybrid Sample</span></span> |<span data-ttu-id="3c1a8-151">How to use a Java component</span><span class="sxs-lookup"><span data-stu-id="3c1a8-151">How to use a Java component</span></span> |
| <span data-ttu-id="3c1a8-152">Storm Sample</span><span class="sxs-lookup"><span data-stu-id="3c1a8-152">Storm Sample</span></span> |<span data-ttu-id="3c1a8-153">A basic word count topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-153">A basic word count topology</span></span> |

<span data-ttu-id="3c1a8-154">In the steps in this document, you use the basic Storm Application project type to create a topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-154">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="3c1a8-155">HBase templates notes</span><span class="sxs-lookup"><span data-stu-id="3c1a8-155">HBase templates notes</span></span>

<span data-ttu-id="3c1a8-156">The HBase reader and writer templates use the HBase REST API to communicate with an HBase on HDInsight cluster, not the HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-156">The HBase reader and writer templates use the HBase REST API to communicate with an HBase on HDInsight cluster, not the HBase Java API.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="3c1a8-157">EventHub templates notes</span><span class="sxs-lookup"><span data-stu-id="3c1a8-157">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c1a8-158">The Java-based EventHub spout component included with the EventHub Reader template does not work with Storm on HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-158">The Java-based EventHub spout component included with the EventHub Reader template does not work with Storm on HDInsight version 3.5.</span></span> <span data-ttu-id="3c1a8-159">Instead, use the EventHub spout component from [https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar](https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-159">Instead, use the EventHub spout component from [https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar](https://000aarperiscus.blob.core.windows.net/certs/storm-eventhubs-1.0.2-jar-with-dependencies.jar).</span></span>

<span data-ttu-id="3c1a8-160">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-160">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="3c1a8-161">Create a C# topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-161">Create a C# topology</span></span>

1. <span data-ttu-id="3c1a8-162">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-162">If you have not already installed the latest version of the HDInsight Tools for Visual Studio, see [Get started using HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="3c1a8-163">Open Visual Studio, select **File** > **New**, and then **Project**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-163">Open Visual Studio, select **File** > **New**, and then **Project**.</span></span>

3. <span data-ttu-id="3c1a8-164">From the **New Project** screen, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-164">From the **New Project** screen, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="3c1a8-165">From the list of templates, select **Storm Application**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-165">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="3c1a8-166">At the bottom of the screen, enter **WordCount** as the name of the application.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-166">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

4. <span data-ttu-id="3c1a8-168">After the project has been created, you should have the following files:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-168">After the project has been created, you should have the following files:</span></span>

   * <span data-ttu-id="3c1a8-169">**Program.cs**: This file defines the topology for your project.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-169">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="3c1a8-170">A default topology that consists of one spout and one bolt is created by default.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-170">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="3c1a8-171">**Spout.cs**: An example spout that emits random numbers.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-171">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="3c1a8-172">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-172">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="3c1a8-173">As part of project creation, the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/) is downloaded from NuGet.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-173">As part of project creation, the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/) is downloaded from NuGet.</span></span>

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

<span data-ttu-id="3c1a8-174">In the next sections, you modify the project into a basic WordCount application.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-174">In the next sections, you modify the project into a basic WordCount application.</span></span>

### <a name="implement-the-spout"></a><span data-ttu-id="3c1a8-175">Implement the spout</span><span class="sxs-lookup"><span data-stu-id="3c1a8-175">Implement the spout</span></span>

1. <span data-ttu-id="3c1a8-176">Open **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-176">Open **Spout.cs**.</span></span> <span data-ttu-id="3c1a8-177">Spouts are used to read data in a topology from an external source.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-177">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="3c1a8-178">The main components for a spout are:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-178">The main components for a spout are:</span></span>

   * <span data-ttu-id="3c1a8-179">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-179">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="3c1a8-180">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-180">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="3c1a8-181">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-181">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="3c1a8-182">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-182">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="3c1a8-183">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-183">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="3c1a8-184">Replace the contents of the **Spout** class with the following text.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-184">Replace the contents of the **Spout** class with the following text.</span></span> <span data-ttu-id="3c1a8-185">This spout randomly emits a sentence into the topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-185">This spout randomly emits a sentence into the topology.</span></span>

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "the cow jumped over the moon",
        "an apple a day keeps the doctor away",
        "four score and seven years ago",
        "snow white and the seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set the instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // The schema for the default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of the spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // The sentence to be emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

    <span data-ttu-id="3c1a8-186">Take a moment to read through the comments to understand what this code does.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-186">Take a moment to read through the comments to understand what this code does.</span></span>

### <a name="implement-the-bolts"></a><span data-ttu-id="3c1a8-187">Implement the bolts</span><span class="sxs-lookup"><span data-stu-id="3c1a8-187">Implement the bolts</span></span>

1. <span data-ttu-id="3c1a8-188">Delete the existing **Bolt.cs** file from the project.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-188">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="3c1a8-189">In **Solution Explorer**, right-click the project and select **Add** > **New item**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-189">In **Solution Explorer**, right-click the project and select **Add** > **New item**.</span></span> <span data-ttu-id="3c1a8-190">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-190">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="3c1a8-191">Repeat this process to create a second bolt named **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-191">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="3c1a8-192">**Splitter.cs**: Implements a bolt that splits sentences into individual words and emits a new stream of words.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-192">**Splitter.cs**: Implements a bolt that splits sentences into individual words and emits a new stream of words.</span></span>

   * <span data-ttu-id="3c1a8-193">**Counter.cs**: Implements a bolt that counts each word and emits a new stream of words and the count for each word.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-193">**Counter.cs**: Implements a bolt that counts each word and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="3c1a8-194">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-194">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="3c1a8-195">Open **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-195">Open **Splitter.cs**.</span></span> <span data-ttu-id="3c1a8-196">It has only one method by default: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-196">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="3c1a8-197">The Execute method is called when the bolt receives a tuple for processing.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-197">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="3c1a8-198">Here, you can read and process incoming tuples, and emit outbound tuples.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-198">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="3c1a8-199">Replace the contents of the **Splitter** class with the following code:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-199">Replace the contents of the **Splitter** class with the following code:</span></span>

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (the sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (the word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of the bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the sentence from the tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

    <span data-ttu-id="3c1a8-200">Take a moment to read through the comments to understand what this code does.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-200">Take a moment to read through the comments to understand what this code does.</span></span>

5. <span data-ttu-id="3c1a8-201">Open **Counter.cs** and replace the class contents with the following:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-201">Open **Counter.cs** and replace the class contents with the following:</span></span>

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - the word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - the word and the word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get the word from the tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for the word in the dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment the count
        count++;
        // Update the count in the dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit the word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

    <span data-ttu-id="3c1a8-202">Take a moment to read through the comments to understand what this code does.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-202">Take a moment to read through the comments to understand what this code does.</span></span>

### <a name="define-the-topology"></a><span data-ttu-id="3c1a8-203">Define the topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-203">Define the topology</span></span>

<span data-ttu-id="3c1a8-204">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-204">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="3c1a8-205">For this topology, the graph is as follows:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-205">For this topology, the graph is as follows:</span></span>

![image of how components are arranged](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="3c1a8-207">Sentences are emitted from the spout, which are distributed to instances of the Splitter bolt.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-207">Sentences are emitted from the spout, which are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="3c1a8-208">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-208">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="3c1a8-209">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-209">Because word count is held locally in the Counter instance, we want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="3c1a8-210">Each instance keeps track of specific words.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-210">Each instance keeps track of specific words.</span></span> <span data-ttu-id="3c1a8-211">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-211">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="3c1a8-212">Open **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-212">Open **Program.cs**.</span></span> <span data-ttu-id="3c1a8-213">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-213">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="3c1a8-214">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-214">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add the spout to the topology.
// Name the component 'sentences'
// Name the field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add the splitter bolt to the topology.
// Name the component 'splitter'
// Name the field that is emitted 'word'
// Use suffleGrouping to distribute incoming tuples
//   from the 'sentences' spout across instances
//   of the splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add the counter bolt to the topology.
// Name the component 'counter'
// Name the fields that are emitted 'word' and 'count'
// Use fieldsGrouping to ensure that tuples are routed
//   to counter instances based on the contents of field
//   position 0 (the word). This could also have been
//   List<string>(){"word"}.
//   This ensures that the word 'jumped', for example, will always
//   go to the same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

<span data-ttu-id="3c1a8-215">Take a moment to read through the comments to understand what this code does.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-215">Take a moment to read through the comments to understand what this code does.</span></span>

## <a name="submit-the-topology"></a><span data-ttu-id="3c1a8-216">Submit the topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-216">Submit the topology</span></span>

1. <span data-ttu-id="3c1a8-217">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-217">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c1a8-218">If prompted, enter the login credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-218">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="3c1a8-219">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-219">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="3c1a8-220">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-220">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="3c1a8-221">You can monitor if the submission is successful by using the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-221">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="3c1a8-222">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-222">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="3c1a8-223">Select the **WordCount** topology from the list to view information about the running topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-223">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c1a8-224">You can also view **Storm Topologies** from **Server Explorer**: Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-224">You can also view **Storm Topologies** from **Server Explorer**: Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="3c1a8-225">To view information about the components in the topology, double-click the component in the diagram.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-225">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="3c1a8-226">From the **Topology Summary** view, click **Kill** to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-226">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c1a8-227">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-227">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="3c1a8-228">Transactional topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-228">Transactional topology</span></span>

<span data-ttu-id="3c1a8-229">The previous topology is non-transactional.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-229">The previous topology is non-transactional.</span></span> <span data-ttu-id="3c1a8-230">The components in the topology do not implement functionality to replaying messages.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-230">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="3c1a8-231">For an example transactional topology, create a project and select **Storm Sample** as the project type.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-231">For an example transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="3c1a8-232">Transactional topologies implement the following to support replay of data:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-232">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="3c1a8-233">**Metadata caching**: The spout must store metadata about the data emitted so that the data can be retrieved and emitted again if a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-233">**Metadata caching**: The spout must store metadata about the data emitted so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="3c1a8-234">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-234">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="3c1a8-235">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to ack that it has successfully processed a tuple.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-235">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to ack that it has successfully processed a tuple.</span></span> <span data-ttu-id="3c1a8-236">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-236">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="3c1a8-237">The `Ack` method allows the spout to remove data that was cached for replay.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-237">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="3c1a8-238">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-238">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="3c1a8-239">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-239">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="3c1a8-240">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-240">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="3c1a8-241">This value identifies the tuple for replay (Ack and Fail) processing.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-241">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="3c1a8-242">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-242">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="3c1a8-243">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-243">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="3c1a8-244">For this example, **lastSeqId** is incremented for every tuple emitted.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-244">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="3c1a8-245">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at run time, based on configuration.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-245">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at run time, based on configuration.</span></span>

## <a name="hybrid-topology"></a><span data-ttu-id="3c1a8-246">Hybrid topology</span><span class="sxs-lookup"><span data-stu-id="3c1a8-246">Hybrid topology</span></span>

<span data-ttu-id="3c1a8-247">HDInsight tools for Visual Studio can also be used to create hybrid topologies, where some components are C# and others are Java.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-247">HDInsight tools for Visual Studio can also be used to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="3c1a8-248">For an example hybrid topology, create a project and select **Storm Hybrid Sample**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-248">For an example hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="3c1a8-249">This sample type demonstrates the following concepts:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-249">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="3c1a8-250">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-250">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**</span></span>

    * <span data-ttu-id="3c1a8-251">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-251">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**</span></span>

* <span data-ttu-id="3c1a8-252">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-252">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**</span></span>

    * <span data-ttu-id="3c1a8-253">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-253">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**</span></span>

  > [!NOTE]
  > <span data-ttu-id="3c1a8-254">This version also demonstrates how to use Clojure code from a text file as a Java component.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-254">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="3c1a8-255">To switch between the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use before submitting it to the cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-255">To switch between the topology that is used when the project is submitted, simply move the `[Active(true)]` statement to the topology you want to use before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1a8-256">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-256">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>


<span data-ttu-id="3c1a8-257">Consider the following when creating and submitting a hybrid topology:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-257">Consider the following when creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="3c1a8-258">**JavaComponentConstructor** must be used to create an instance of the Java class for a spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-258">**JavaComponentConstructor** must be used to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="3c1a8-259">**microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** should be used to serialize data in to or out of Java components from Java objects to JSON.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-259">**microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** should be used to serialize data in to or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="3c1a8-260">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-260">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="3c1a8-261">The path specified should be the directory that contains the JAR files that contain your Java classes.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-261">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="3c1a8-262">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3c1a8-262">Azure Event Hubs</span></span>

<span data-ttu-id="3c1a8-263">SCP.Net version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub Spout (a Java spout that reads from Event Hub.) When creating a topology that uses an Event Hub spout, use the following methods:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-263">SCP.Net version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub Spout (a Java spout that reads from Event Hub.) When creating a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="3c1a8-264">**EventHubSpoutConfig** class: creates an object that contains the configuration for the spout component.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-264">**EventHubSpoutConfig** class: creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="3c1a8-265">**TopologyBuilder.SetEventHubSpout** method: adds the Event Hub Spout component to the topology.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-265">**TopologyBuilder.SetEventHubSpout** method: adds the Event Hub Spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1a8-266">You must still use the CustomizedInteropJSONSerializer to serialize data produced by the spout.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-266">You must still use the CustomizedInteropJSONSerializer to serialize data produced by the spout.</span></span>

## <a id="configurationmanager"></a><span data-ttu-id="3c1a8-267">Using ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="3c1a8-267">Using ConfigurationManager</span></span>

<span data-ttu-id="3c1a8-268">Don't use ConfigurationManager to retrieve configuration values from bolt and spout components.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-268">Don't use ConfigurationManager to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="3c1a8-269">Doing so can cause a null pointer exception.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-269">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="3c1a8-270">Instead, the configuration for your project is passed into the Storm topology as a key/value pair in the topology context.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-270">Instead, the configuration for your project is passed into the Storm topology as a key/value pair in the topology context.</span></span> <span data-ttu-id="3c1a8-271">Each component that relies on configuration values must retrieve them from the context during initialization.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-271">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="3c1a8-272">The following code demonstrates how to retrieve these values:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-272">The following code demonstrates how to retrieve these values:</span></span>

```csharp
public class MyComponent : ISCPBolt
{
    // To hold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of the context for this component instance
        this.ctx = ctx;
        // If it exists, load the configuration for the component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve the value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

<span data-ttu-id="3c1a8-273">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-273">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="3c1a8-274">The following example is a basic `Get` method that properly passes these values:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-274">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="3c1a8-275">How to update SCP.NET</span><span class="sxs-lookup"><span data-stu-id="3c1a8-275">How to update SCP.NET</span></span>

<span data-ttu-id="3c1a8-276">Recent releases of SCP.NET support package upgrade through NuGet.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-276">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="3c1a8-277">When a new update is available, you receive an upgrade notification.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-277">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="3c1a8-278">To manually check for an upgrade, perform these steps:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-278">To manually check for an upgrade, perform these steps:</span></span>

1. <span data-ttu-id="3c1a8-279">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-279">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="3c1a8-280">From the package manager, select **Updates**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-280">From the package manager, select **Updates**.</span></span> <span data-ttu-id="3c1a8-281">If an update is available, it is listed.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-281">If an update is available, it is listed.</span></span> <span data-ttu-id="3c1a8-282">Click the **Update** button for the package to install it.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-282">Click the **Update** button for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3c1a8-283">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-283">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="3c1a8-284">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-284">In **Solution Explorer**, right-click the project and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="3c1a8-285">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-285">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="3c1a8-286">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="3c1a8-286">Troubleshooting</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="3c1a8-287">Null pointer exceptions</span><span class="sxs-lookup"><span data-stu-id="3c1a8-287">Null pointer exceptions</span></span>

<span data-ttu-id="3c1a8-288">When using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use ConfigurationManager to read configuration settings at runtime may return null pointer exceptions.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-288">When using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use ConfigurationManager to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="3c1a8-289">The configuration for your project is passed into the Storm topology as a key/value pair in the topology context.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-289">The configuration for your project is passed into the Storm topology as a key/value pair in the topology context.</span></span> <span data-ttu-id="3c1a8-290">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-290">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="3c1a8-291">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-291">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="3c1a8-292">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="3c1a8-292">System.TypeLoadException</span></span>

<span data-ttu-id="3c1a8-293">When using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-293">When using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="3c1a8-294">This error occurs when you use a binary that is not compatible with the version of .NET that mono supports.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-294">This error occurs when you use a binary that is not compatible with the version of .NET that mono supports.</span></span>

<span data-ttu-id="3c1a8-295">For Linux-based HDInsight clusters, you should make sure that your project uses binaries compiled for .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-295">For Linux-based HDInsight clusters, you should make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="3c1a8-296">Test a topology locally</span><span class="sxs-lookup"><span data-stu-id="3c1a8-296">Test a topology locally</span></span>

<span data-ttu-id="3c1a8-297">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-297">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="3c1a8-298">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-298">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="3c1a8-299">Local testing only works for basic, C# only topologies.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-299">Local testing only works for basic, C# only topologies.</span></span> <span data-ttu-id="3c1a8-300">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-300">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="3c1a8-301">In **Solution Explorer**, right-click the project, and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-301">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="3c1a8-302">In the project properties, change the **Output type** to **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-302">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![output type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="3c1a8-304">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-304">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="3c1a8-305">In **Solution Explorer**, right-click the project, then select **Add** > **New Item**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-305">In **Solution Explorer**, right-click the project, then select **Add** > **New Item**.</span></span> <span data-ttu-id="3c1a8-306">Select **Class** and enter **LocalTest.cs** as the class name.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-306">Select **Class** and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="3c1a8-307">Finally, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-307">Finally, click **Add**.</span></span>

3. <span data-ttu-id="3c1a8-308">Open **LocalTest.cs** and add the following **using** statement at the top:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-308">Open **LocalTest.cs** and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="3c1a8-309">Use the following code as the contents of the **LocalTest** class:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-309">Use the following code as the contents of the **LocalTest** class:</span></span>

    ```csharp
    // Drives the topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test the spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of the spout, using the local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext to persist the data stream to file
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test the splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set the data stream to the data created by the spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test the counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used to initialize
            // components in the development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of the bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set the data stream to the data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from the stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in the batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext to persist the data stream to file
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    <span data-ttu-id="3c1a8-310">Take a moment to read through the code comments.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-310">Take a moment to read through the code comments.</span></span> <span data-ttu-id="3c1a8-311">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-311">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="3c1a8-312">Open **Program.cs** and add the following to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-312">Open **Program.cs** and add the following to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize the runtime
    SCPRuntime.Initialize();

    //If we are not running under the local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. <span data-ttu-id="3c1a8-313">Save the changes, then click **F5** or select **Debug** > **Start Debugging** to start the project.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-313">Save the changes, then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="3c1a8-314">A console window should appear, and log status as the tests progress.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-314">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="3c1a8-315">When **Tests finished** appears, press any key to close the window.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-315">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="3c1a8-316">Use **Windows Explorer** to locate the directory that contains your project, for example, **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-316">Use **Windows Explorer** to locate the directory that contains your project, for example, **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="3c1a8-317">In this directory, open **Bin**, and then click **Debug**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-317">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="3c1a8-318">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-318">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="3c1a8-319">Open each text file and inspect the data.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-319">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3c1a8-320">String data is persisted as an array of decimal values in these files.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-320">String data is persisted as an array of decimal values in these files.</span></span> <span data-ttu-id="3c1a8-321">For example, \[[97,103,111]] in the **splitter.txt** file is the word 'and'.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-321">For example, \[[97,103,111]] in the **splitter.txt** file is the word 'and'.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1a8-322">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-322">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="3c1a8-323">Log information</span><span class="sxs-lookup"><span data-stu-id="3c1a8-323">Log information</span></span>

<span data-ttu-id="3c1a8-324">You can easily log information from your topology components by using `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-324">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="3c1a8-325">For example, the following creates an informational log entry:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-325">For example, the following creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="3c1a8-326">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-326">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="3c1a8-327">Expand the entry for your Storm on HDInsight cluster, then expand **Hadoop Service Log**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-327">Expand the entry for your Storm on HDInsight cluster, then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="3c1a8-328">Finally, select the log file to view.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-328">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="3c1a8-329">The logs are stored in the Azure Storage account that is used by your cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-329">The logs are stored in the Azure Storage account that is used by your cluster.</span></span> <span data-ttu-id="3c1a8-330">To view the logs in Visual Studio, you must log in to the Azure subscription that owns the storage account.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-330">To view the logs in Visual Studio, you must log in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="3c1a8-331">View error information</span><span class="sxs-lookup"><span data-stu-id="3c1a8-331">View error information</span></span>

<span data-ttu-id="3c1a8-332">To view errors that have occurred in a running topology, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-332">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="3c1a8-333">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-333">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="3c1a8-334">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error that has occurred.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-334">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error that has occurred.</span></span>

3. <span data-ttu-id="3c1a8-335">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-335">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="3c1a8-336">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-336">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="3c1a8-337">To obtain more information, select a **Port** from the **Executors** section of the page to see the Storm worker log for the last few minutes.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-337">To obtain more information, select a **Port** from the **Executors** section of the page to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="3c1a8-338">Errors submitting topologies</span><span class="sxs-lookup"><span data-stu-id="3c1a8-338">Errors submitting topologies</span></span>

<span data-ttu-id="3c1a8-339">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-339">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="3c1a8-340">To retrieve these logs, use the following command from a command line:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-340">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="3c1a8-341">Replace __sshuser__ with the SSH user account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-341">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="3c1a8-342">Replace __clustername__ with the name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-342">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="3c1a8-343">If you used a password for the SSH account, you are prompted to enter it.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-343">If you used a password for the SSH account, you are prompted to enter it.</span></span> <span data-ttu-id="3c1a8-344">The command downloads the file to the directory that the command is ran from.</span><span class="sxs-lookup"><span data-stu-id="3c1a8-344">The command downloads the file to the directory that the command is ran from.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c1a8-345">Next steps</span><span class="sxs-lookup"><span data-stu-id="3c1a8-345">Next steps</span></span>

<span data-ttu-id="3c1a8-346">For an example of processing data from Event Hubs, see [Process events from Azure Event Hub with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-346">For an example of processing data from Event Hubs, see [Process events from Azure Event Hub with Storm on HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="3c1a8-347">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-347">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="3c1a8-348">To discover more information about creating C# topologies, visit [SCP.NET GettingStarted.md](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="3c1a8-348">To discover more information about creating C# topologies, visit [SCP.NET GettingStarted.md](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="3c1a8-349">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="3c1a8-349">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="3c1a8-350">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-350">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="3c1a8-351">SCP programming guide</span><span class="sxs-lookup"><span data-stu-id="3c1a8-351">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)

<span data-ttu-id="3c1a8-352">**Apache Storm on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-352">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="3c1a8-353">Deploy and monitor topologies with Apache Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-353">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="3c1a8-354">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-354">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

<span data-ttu-id="3c1a8-355">**Apache Hadoop on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-355">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="3c1a8-356">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-356">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3c1a8-357">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-357">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3c1a8-358">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-358">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="3c1a8-359">**Apache HBase on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="3c1a8-359">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="3c1a8-360">Getting started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="3c1a8-360">Getting started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)



