---
title: Apache Storm topologies with Visual Studio and C# - Azure HDInsight
description: Learn how to create Storm topologies in C#. Create a simple word count topology in Visual Studio by using the Hadoop tools for Visual Studio.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 11/27/2017
ROBOTS: NOINDEX
ms.openlocfilehash: b36e5b27ff0fb2e5231bd2ad8166a8ead64ad5cb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869096"
---
# <a name="develop-c-topologies-for-apache-storm-by-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="17cdf-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17cdf-104">Develop C# topologies for Apache Storm by using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="17cdf-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="17cdf-105">Learn how to create a C# Storm topology by using the Azure Data Lake (Hadoop) tools for Visual Studio.</span></span> <span data-ttu-id="17cdf-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-106">This document walks through the process of creating a Storm project in Visual Studio, testing it locally, and deploying it to an Apache Storm on Azure HDInsight cluster.</span></span>

<span data-ttu-id="17cdf-107">You also learn how to create hybrid topologies that use C# and Java components.</span><span class="sxs-lookup"><span data-stu-id="17cdf-107">You also learn how to create hybrid topologies that use C# and Java components.</span></span>

> [!NOTE]
> <span data-ttu-id="17cdf-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-108">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to either a Linux or Windows-based HDInsight cluster.</span></span> <span data-ttu-id="17cdf-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span><span class="sxs-lookup"><span data-stu-id="17cdf-109">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="17cdf-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span><span class="sxs-lookup"><span data-stu-id="17cdf-110">To use a C# topology with a Linux-based cluster, you must update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or later.</span></span> <span data-ttu-id="17cdf-111">The version of the package must also match the major version of Storm installed on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17cdf-111">The version of the package must also match the major version of Storm installed on HDInsight.</span></span>

| <span data-ttu-id="17cdf-112">HDInsight version</span><span class="sxs-lookup"><span data-stu-id="17cdf-112">HDInsight version</span></span> | <span data-ttu-id="17cdf-113">Storm version</span><span class="sxs-lookup"><span data-stu-id="17cdf-113">Storm version</span></span> | <span data-ttu-id="17cdf-114">SCP.NET version</span><span class="sxs-lookup"><span data-stu-id="17cdf-114">SCP.NET version</span></span> | <span data-ttu-id="17cdf-115">Default Mono version</span><span class="sxs-lookup"><span data-stu-id="17cdf-115">Default Mono version</span></span> |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| <span data-ttu-id="17cdf-116">3.3</span><span class="sxs-lookup"><span data-stu-id="17cdf-116">3.3</span></span> |<span data-ttu-id="17cdf-117">0.10.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-117">0.10.x</span></span> |<span data-ttu-id="17cdf-118">0.10.x.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-118">0.10.x.x</span></span></br><span data-ttu-id="17cdf-119">(only on Windows-based HDInsight)</span><span class="sxs-lookup"><span data-stu-id="17cdf-119">(only on Windows-based HDInsight)</span></span> | <span data-ttu-id="17cdf-120">NA</span><span class="sxs-lookup"><span data-stu-id="17cdf-120">NA</span></span> |
| <span data-ttu-id="17cdf-121">3.4</span><span class="sxs-lookup"><span data-stu-id="17cdf-121">3.4</span></span> | <span data-ttu-id="17cdf-122">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-122">0.10.0.x</span></span> | <span data-ttu-id="17cdf-123">0.10.0.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-123">0.10.0.x</span></span> | <span data-ttu-id="17cdf-124">3.2.8</span><span class="sxs-lookup"><span data-stu-id="17cdf-124">3.2.8</span></span> |
| <span data-ttu-id="17cdf-125">3.5</span><span class="sxs-lookup"><span data-stu-id="17cdf-125">3.5</span></span> | <span data-ttu-id="17cdf-126">1.0.2.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-126">1.0.2.x</span></span> | <span data-ttu-id="17cdf-127">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-127">1.0.0.x</span></span> | <span data-ttu-id="17cdf-128">4.2.1</span><span class="sxs-lookup"><span data-stu-id="17cdf-128">4.2.1</span></span> |
| <span data-ttu-id="17cdf-129">3.6</span><span class="sxs-lookup"><span data-stu-id="17cdf-129">3.6</span></span> | <span data-ttu-id="17cdf-130">1.1.0.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-130">1.1.0.x</span></span> | <span data-ttu-id="17cdf-131">1.0.0.x</span><span class="sxs-lookup"><span data-stu-id="17cdf-131">1.0.0.x</span></span> | <span data-ttu-id="17cdf-132">4.2.8</span><span class="sxs-lookup"><span data-stu-id="17cdf-132">4.2.8</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="17cdf-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-133">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="17cdf-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span><span class="sxs-lookup"><span data-stu-id="17cdf-134">Check [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) for potential incompatibilities.</span></span>

## <a name="install-visual-studio"></a><span data-ttu-id="17cdf-135">Install Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17cdf-135">Install Visual Studio</span></span>

<span data-ttu-id="17cdf-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="17cdf-136">You can develop C# topologies with SCP.NET by using one of the following versions of Visual Studio:</span></span>

* <span data-ttu-id="17cdf-137">Visual Studio 2012 with Update 4</span><span class="sxs-lookup"><span data-stu-id="17cdf-137">Visual Studio 2012 with Update 4</span></span>

* <span data-ttu-id="17cdf-138">Visual Studio 2013 with Update 4 or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span><span class="sxs-lookup"><span data-stu-id="17cdf-138">Visual Studio 2013 with Update 4 or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)</span></span>

* <span data-ttu-id="17cdf-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span><span class="sxs-lookup"><span data-stu-id="17cdf-139">Visual Studio 2015 or [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)</span></span>

* <span data-ttu-id="17cdf-140">Visual Studio 2017 (any edition)</span><span class="sxs-lookup"><span data-stu-id="17cdf-140">Visual Studio 2017 (any edition)</span></span>

## <a name="install-data-lake-tools-for-visual-studio"></a><span data-ttu-id="17cdf-141">Install Data Lake tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="17cdf-141">Install Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="17cdf-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="17cdf-142">To install Data Lake tools for Visual Studio, follow the steps in [Get started using Data Lake tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md).</span></span>

## <a name="install-java"></a><span data-ttu-id="17cdf-143">Install Java</span><span class="sxs-lookup"><span data-stu-id="17cdf-143">Install Java</span></span>

<span data-ttu-id="17cdf-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span><span class="sxs-lookup"><span data-stu-id="17cdf-144">When you submit a Storm topology from Visual Studio, SCP.NET generates a zip file that contains the topology and dependencies.</span></span> <span data-ttu-id="17cdf-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="17cdf-145">Java is used to create these zip files, because it uses a format that is more compatible with Linux-based clusters.</span></span>

1. <span data-ttu-id="17cdf-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span><span class="sxs-lookup"><span data-stu-id="17cdf-146">Install the Java Developer Kit (JDK) 7 or later on your development environment.</span></span> <span data-ttu-id="17cdf-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="17cdf-147">You can get the Oracle JDK from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span> <span data-ttu-id="17cdf-148">You can also use [other Java distributions](http://openjdk.java.net/).</span><span class="sxs-lookup"><span data-stu-id="17cdf-148">You can also use [other Java distributions](http://openjdk.java.net/).</span></span>

2. <span data-ttu-id="17cdf-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span><span class="sxs-lookup"><span data-stu-id="17cdf-149">The `JAVA_HOME` environment variable must point to the directory that contains Java.</span></span>

3. <span data-ttu-id="17cdf-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span><span class="sxs-lookup"><span data-stu-id="17cdf-150">The `PATH` environment variable must include the `%JAVA_HOME%\bin` directory.</span></span>

<span data-ttu-id="17cdf-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span><span class="sxs-lookup"><span data-stu-id="17cdf-151">You can use the following C# console application to verify that Java and the JDK are correctly installed:</span></span>

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable("JAVA_HOME");
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @"\bin", "jar.exe");
               if (File.Exists(jarExe))
               {
                   Console.WriteLine("JAVA Is Installed properly");
                    return;
               }
               else
               {
                   Console.WriteLine("A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.");
               }
           }
           else
           {
             Console.WriteLine("A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.");
           }
       }  
   }
}
```

## <a name="storm-templates"></a><span data-ttu-id="17cdf-152">Storm templates</span><span class="sxs-lookup"><span data-stu-id="17cdf-152">Storm templates</span></span>

<span data-ttu-id="17cdf-153">The Data Lake tools for Visual Studio provide the following templates:</span><span class="sxs-lookup"><span data-stu-id="17cdf-153">The Data Lake tools for Visual Studio provide the following templates:</span></span>

| <span data-ttu-id="17cdf-154">Project type</span><span class="sxs-lookup"><span data-stu-id="17cdf-154">Project type</span></span> | <span data-ttu-id="17cdf-155">Demonstrates</span><span class="sxs-lookup"><span data-stu-id="17cdf-155">Demonstrates</span></span> |
| --- | --- |
| <span data-ttu-id="17cdf-156">Storm Application</span><span class="sxs-lookup"><span data-stu-id="17cdf-156">Storm Application</span></span> |<span data-ttu-id="17cdf-157">An empty Storm topology project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-157">An empty Storm topology project.</span></span> |
| <span data-ttu-id="17cdf-158">Storm Azure SQL Writer Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-158">Storm Azure SQL Writer Sample</span></span> |<span data-ttu-id="17cdf-159">How to write to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="17cdf-159">How to write to Azure SQL Database.</span></span> |
| <span data-ttu-id="17cdf-160">Storm Azure Cosmos DB Reader Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-160">Storm Azure Cosmos DB Reader Sample</span></span> |<span data-ttu-id="17cdf-161">How to read from Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17cdf-161">How to read from Azure Cosmos DB.</span></span> |
| <span data-ttu-id="17cdf-162">Storm Azure Cosmos DB Writer Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-162">Storm Azure Cosmos DB Writer Sample</span></span> |<span data-ttu-id="17cdf-163">How to write to Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="17cdf-163">How to write to Azure Cosmos DB.</span></span> |
| <span data-ttu-id="17cdf-164">Storm EventHub Reader Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-164">Storm EventHub Reader Sample</span></span> |<span data-ttu-id="17cdf-165">How to read from Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="17cdf-165">How to read from Azure Event Hubs.</span></span> |
| <span data-ttu-id="17cdf-166">Storm EventHub Writer Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-166">Storm EventHub Writer Sample</span></span> |<span data-ttu-id="17cdf-167">How to write to Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="17cdf-167">How to write to Azure Event Hubs.</span></span> |
| <span data-ttu-id="17cdf-168">Storm HBase Reader Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-168">Storm HBase Reader Sample</span></span> |<span data-ttu-id="17cdf-169">How to read from HBase on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="17cdf-169">How to read from HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="17cdf-170">Storm HBase Writer Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-170">Storm HBase Writer Sample</span></span> |<span data-ttu-id="17cdf-171">How to write to HBase on HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="17cdf-171">How to write to HBase on HDInsight clusters.</span></span> |
| <span data-ttu-id="17cdf-172">Storm Hybrid Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-172">Storm Hybrid Sample</span></span> |<span data-ttu-id="17cdf-173">How to use a Java component.</span><span class="sxs-lookup"><span data-stu-id="17cdf-173">How to use a Java component.</span></span> |
| <span data-ttu-id="17cdf-174">Storm Sample</span><span class="sxs-lookup"><span data-stu-id="17cdf-174">Storm Sample</span></span> |<span data-ttu-id="17cdf-175">A basic word count topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-175">A basic word count topology.</span></span> |

> [!WARNING]
> <span data-ttu-id="17cdf-176">Not all templates work with Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="17cdf-176">Not all templates work with Linux-based HDInsight.</span></span> <span data-ttu-id="17cdf-177">NuGet packages used by the templates may not be compatible with Mono.</span><span class="sxs-lookup"><span data-stu-id="17cdf-177">NuGet packages used by the templates may not be compatible with Mono.</span></span> <span data-ttu-id="17cdf-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](../hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span><span class="sxs-lookup"><span data-stu-id="17cdf-178">Check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document and use the [.NET Portability Analyzer](../hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) to identify potential problems.</span></span>

<span data-ttu-id="17cdf-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-179">In the steps in this document, you use the basic Storm Application project type to create a topology.</span></span>

### <a name="hbase-templates-notes"></a><span data-ttu-id="17cdf-180">HBase templates notes</span><span class="sxs-lookup"><span data-stu-id="17cdf-180">HBase templates notes</span></span>

<span data-ttu-id="17cdf-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-181">The HBase reader and writer templates use the HBase REST API, not the HBase Java API, to communicate with an HBase on HDInsight cluster.</span></span>

### <a name="eventhub-templates-notes"></a><span data-ttu-id="17cdf-182">EventHub templates notes</span><span class="sxs-lookup"><span data-stu-id="17cdf-182">EventHub templates notes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17cdf-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span><span class="sxs-lookup"><span data-stu-id="17cdf-183">The Java-based EventHub spout component included with the EventHub Reader template may not work with Storm on HDInsight version 3.5 or later.</span></span> <span data-ttu-id="17cdf-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span><span class="sxs-lookup"><span data-stu-id="17cdf-184">An updated version of this component is available at [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).</span></span>

<span data-ttu-id="17cdf-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="17cdf-185">For an example topology that uses this component and works with Storm on HDInsight 3.5, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

## <a name="create-a-c-topology"></a><span data-ttu-id="17cdf-186">Create a C# topology</span><span class="sxs-lookup"><span data-stu-id="17cdf-186">Create a C# topology</span></span>

1. <span data-ttu-id="17cdf-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-187">Open Visual Studio, select **File** > **New**, and then select **Project**.</span></span>

2. <span data-ttu-id="17cdf-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-188">From the **New Project** window, expand **Installed** > **Templates**, and select **Azure Data Lake**.</span></span> <span data-ttu-id="17cdf-189">From the list of templates, select **Storm Application**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-189">From the list of templates, select **Storm Application**.</span></span> <span data-ttu-id="17cdf-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span><span class="sxs-lookup"><span data-stu-id="17cdf-190">At the bottom of the screen, enter **WordCount** as the name of the application.</span></span>

    ![Screenshot of New Project window](./media/apache-storm-develop-csharp-visual-studio-topology/new-project.png)

3. <span data-ttu-id="17cdf-192">After you have created the project, you should have the following files:</span><span class="sxs-lookup"><span data-stu-id="17cdf-192">After you have created the project, you should have the following files:</span></span>

   * <span data-ttu-id="17cdf-193">**Program.cs**: This file defines the topology for your project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-193">**Program.cs**: This file defines the topology for your project.</span></span> <span data-ttu-id="17cdf-194">A default topology that consists of one spout and one bolt is created by default.</span><span class="sxs-lookup"><span data-stu-id="17cdf-194">A default topology that consists of one spout and one bolt is created by default.</span></span>

   * <span data-ttu-id="17cdf-195">**Spout.cs**: An example spout that emits random numbers.</span><span class="sxs-lookup"><span data-stu-id="17cdf-195">**Spout.cs**: An example spout that emits random numbers.</span></span>

   * <span data-ttu-id="17cdf-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span><span class="sxs-lookup"><span data-stu-id="17cdf-196">**Bolt.cs**: An example bolt that keeps a count of numbers emitted by the spout.</span></span>

     <span data-ttu-id="17cdf-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span><span class="sxs-lookup"><span data-stu-id="17cdf-197">When you create the project, NuGet downloads the latest [SCP.NET package](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).</span></span>

     [!INCLUDE [scp.net version important](../../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-the-spout"></a><span data-ttu-id="17cdf-198">Implement the spout</span><span class="sxs-lookup"><span data-stu-id="17cdf-198">Implement the spout</span></span>

1. <span data-ttu-id="17cdf-199">Open **Spout.cs**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-199">Open **Spout.cs**.</span></span> <span data-ttu-id="17cdf-200">Spouts are used to read data in a topology from an external source.</span><span class="sxs-lookup"><span data-stu-id="17cdf-200">Spouts are used to read data in a topology from an external source.</span></span> <span data-ttu-id="17cdf-201">The main components for a spout are:</span><span class="sxs-lookup"><span data-stu-id="17cdf-201">The main components for a spout are:</span></span>

   * <span data-ttu-id="17cdf-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span><span class="sxs-lookup"><span data-stu-id="17cdf-202">**NextTuple**: Called by Storm when the spout is allowed to emit new tuples.</span></span>

   * <span data-ttu-id="17cdf-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span><span class="sxs-lookup"><span data-stu-id="17cdf-203">**Ack** (transactional topology only): Handles acknowledgements initiated by other components in the topology for tuples sent from the spout.</span></span> <span data-ttu-id="17cdf-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span><span class="sxs-lookup"><span data-stu-id="17cdf-204">Acknowledging a tuple lets the spout know that it was processed successfully by downstream components.</span></span>

   * <span data-ttu-id="17cdf-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-205">**Fail** (transactional topology only): Handles tuples that are fail-processing other components in the topology.</span></span> <span data-ttu-id="17cdf-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span><span class="sxs-lookup"><span data-stu-id="17cdf-206">Implementing a Fail method allows you to re-emit the tuple so that it can be processed again.</span></span>

2. <span data-ttu-id="17cdf-207">Replace the contents of the **Spout** class with the following text: This spout randomly emits a sentence into the topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-207">Replace the contents of the **Spout** class with the following text: This spout randomly emits a sentence into the topology.</span></span>

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

### <a name="implement-the-bolts"></a><span data-ttu-id="17cdf-208">Implement the bolts</span><span class="sxs-lookup"><span data-stu-id="17cdf-208">Implement the bolts</span></span>

1. <span data-ttu-id="17cdf-209">Delete the existing **Bolt.cs** file from the project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-209">Delete the existing **Bolt.cs** file from the project.</span></span>

2. <span data-ttu-id="17cdf-210">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-210">In **Solution Explorer**, right-click the project, and select **Add** > **New item**.</span></span> <span data-ttu-id="17cdf-211">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span><span class="sxs-lookup"><span data-stu-id="17cdf-211">From the list, select **Storm Bolt**, and enter **Splitter.cs** as the name.</span></span> <span data-ttu-id="17cdf-212">Repeat this process to create a second bolt named **Counter.cs**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-212">Repeat this process to create a second bolt named **Counter.cs**.</span></span>

   * <span data-ttu-id="17cdf-213">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span><span class="sxs-lookup"><span data-stu-id="17cdf-213">**Splitter.cs**: Implements a bolt that splits sentences into individual words, and emits a new stream of words.</span></span>

   * <span data-ttu-id="17cdf-214">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span><span class="sxs-lookup"><span data-stu-id="17cdf-214">**Counter.cs**: Implements a bolt that counts each word, and emits a new stream of words and the count for each word.</span></span>

     > [!NOTE]
     > <span data-ttu-id="17cdf-215">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span><span class="sxs-lookup"><span data-stu-id="17cdf-215">These bolts read and write to streams, but you can also use a bolt to communicate with sources such as a database or service.</span></span>

3. <span data-ttu-id="17cdf-216">Open **Splitter.cs**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-216">Open **Splitter.cs**.</span></span> <span data-ttu-id="17cdf-217">It has only one method by default: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-217">It has only one method by default: **Execute**.</span></span> <span data-ttu-id="17cdf-218">The Execute method is called when the bolt receives a tuple for processing.</span><span class="sxs-lookup"><span data-stu-id="17cdf-218">The Execute method is called when the bolt receives a tuple for processing.</span></span> <span data-ttu-id="17cdf-219">Here, you can read and process incoming tuples, and emit outbound tuples.</span><span class="sxs-lookup"><span data-stu-id="17cdf-219">Here, you can read and process incoming tuples, and emit outbound tuples.</span></span>

4. <span data-ttu-id="17cdf-220">Replace the contents of the **Splitter** class with the following code:</span><span class="sxs-lookup"><span data-stu-id="17cdf-220">Replace the contents of the **Splitter** class with the following code:</span></span>

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

5. <span data-ttu-id="17cdf-221">Open **Counter.cs**, and replace the class contents with the following code:</span><span class="sxs-lookup"><span data-stu-id="17cdf-221">Open **Counter.cs**, and replace the class contents with the following code:</span></span>

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

### <a name="define-the-topology"></a><span data-ttu-id="17cdf-222">Define the topology</span><span class="sxs-lookup"><span data-stu-id="17cdf-222">Define the topology</span></span>

<span data-ttu-id="17cdf-223">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span><span class="sxs-lookup"><span data-stu-id="17cdf-223">Spouts and bolts are arranged in a graph, which defines how the data flows between components.</span></span> <span data-ttu-id="17cdf-224">For this topology, the graph is as follows:</span><span class="sxs-lookup"><span data-stu-id="17cdf-224">For this topology, the graph is as follows:</span></span>

![Diagram of how components are arranged](./media/apache-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

<span data-ttu-id="17cdf-226">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span><span class="sxs-lookup"><span data-stu-id="17cdf-226">Sentences are emitted from the spout, and are distributed to instances of the Splitter bolt.</span></span> <span data-ttu-id="17cdf-227">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span><span class="sxs-lookup"><span data-stu-id="17cdf-227">The Splitter bolt breaks the sentences into words, which are distributed to the Counter bolt.</span></span>

<span data-ttu-id="17cdf-228">Because word count is held locally in the Counter instance, you want to make sure that specific words flow to the same Counter bolt instance.</span><span class="sxs-lookup"><span data-stu-id="17cdf-228">Because word count is held locally in the Counter instance, you want to make sure that specific words flow to the same Counter bolt instance.</span></span> <span data-ttu-id="17cdf-229">Each instance keeps track of specific words.</span><span class="sxs-lookup"><span data-stu-id="17cdf-229">Each instance keeps track of specific words.</span></span> <span data-ttu-id="17cdf-230">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span><span class="sxs-lookup"><span data-stu-id="17cdf-230">Since the Splitter bolt maintains no state, it really doesn't matter which instance of the splitter receives which sentence.</span></span>

<span data-ttu-id="17cdf-231">Open **Program.cs**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-231">Open **Program.cs**.</span></span> <span data-ttu-id="17cdf-232">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span><span class="sxs-lookup"><span data-stu-id="17cdf-232">The important method is **GetTopologyBuilder**, which is used to define the topology that is submitted to Storm.</span></span> <span data-ttu-id="17cdf-233">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span><span class="sxs-lookup"><span data-stu-id="17cdf-233">Replace the contents of **GetTopologyBuilder** with the following code to implement the topology described previously:</span></span>

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

## <a name="submit-the-topology"></a><span data-ttu-id="17cdf-234">Submit the topology</span><span class="sxs-lookup"><span data-stu-id="17cdf-234">Submit the topology</span></span>

1. <span data-ttu-id="17cdf-235">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-235">In **Solution Explorer**, right-click the project, and select **Submit to Storm on HDInsight**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17cdf-236">If prompted, enter the credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="17cdf-236">If prompted, enter the credentials for your Azure subscription.</span></span> <span data-ttu-id="17cdf-237">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-237">If you have more than one subscription, sign in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="17cdf-238">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-238">Select your Storm on HDInsight cluster from the **Storm Cluster** drop-down list, and then select **Submit**.</span></span> <span data-ttu-id="17cdf-239">You can monitor if the submission is successful by using the **Output** window.</span><span class="sxs-lookup"><span data-stu-id="17cdf-239">You can monitor if the submission is successful by using the **Output** window.</span></span>

3. <span data-ttu-id="17cdf-240">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span><span class="sxs-lookup"><span data-stu-id="17cdf-240">When the topology has been successfully submitted, the **Storm Topologies** for the cluster should appear.</span></span> <span data-ttu-id="17cdf-241">Select the **WordCount** topology from the list to view information about the running topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-241">Select the **WordCount** topology from the list to view information about the running topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17cdf-242">You can also view **Storm Topologies** from **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-242">You can also view **Storm Topologies** from **Server Explorer**.</span></span> <span data-ttu-id="17cdf-243">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-243">Expand **Azure** > **HDInsight**, right-click a Storm on HDInsight cluster, and then select **View Storm Topologies**.</span></span>

    <span data-ttu-id="17cdf-244">To view information about the components in the topology, double-click the component in the diagram.</span><span class="sxs-lookup"><span data-stu-id="17cdf-244">To view information about the components in the topology, double-click the component in the diagram.</span></span>

4. <span data-ttu-id="17cdf-245">From the **Topology Summary** view, click **Kill** to stop the topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-245">From the **Topology Summary** view, click **Kill** to stop the topology.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17cdf-246">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="17cdf-246">Storm topologies continue to run until they are deactivated, or the cluster is deleted.</span></span>

## <a name="transactional-topology"></a><span data-ttu-id="17cdf-247">Transactional topology</span><span class="sxs-lookup"><span data-stu-id="17cdf-247">Transactional topology</span></span>

<span data-ttu-id="17cdf-248">The previous topology is non-transactional.</span><span class="sxs-lookup"><span data-stu-id="17cdf-248">The previous topology is non-transactional.</span></span> <span data-ttu-id="17cdf-249">The components in the topology do not implement functionality to replaying messages.</span><span class="sxs-lookup"><span data-stu-id="17cdf-249">The components in the topology do not implement functionality to replaying messages.</span></span> <span data-ttu-id="17cdf-250">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span><span class="sxs-lookup"><span data-stu-id="17cdf-250">For an example of a transactional topology, create a project and select **Storm Sample** as the project type.</span></span>

<span data-ttu-id="17cdf-251">Transactional topologies implement the following to support replay of data:</span><span class="sxs-lookup"><span data-stu-id="17cdf-251">Transactional topologies implement the following to support replay of data:</span></span>

* <span data-ttu-id="17cdf-252">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="17cdf-252">**Metadata caching**: The spout must store metadata about the data emitted, so that the data can be retrieved and emitted again if a failure occurs.</span></span> <span data-ttu-id="17cdf-253">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span><span class="sxs-lookup"><span data-stu-id="17cdf-253">Because the data emitted by the sample is small, the raw data for each tuple is stored in a dictionary for replay.</span></span>

* <span data-ttu-id="17cdf-254">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span><span class="sxs-lookup"><span data-stu-id="17cdf-254">**Ack**: Each bolt in the topology can call `this.ctx.Ack(tuple)` to acknowledge that it has successfully processed a tuple.</span></span> <span data-ttu-id="17cdf-255">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span><span class="sxs-lookup"><span data-stu-id="17cdf-255">When all bolts have acked the tuple, the `Ack` method of the spout is invoked.</span></span> <span data-ttu-id="17cdf-256">The `Ack` method allows the spout to remove data that was cached for replay.</span><span class="sxs-lookup"><span data-stu-id="17cdf-256">The `Ack` method allows the spout to remove data that was cached for replay.</span></span>

* <span data-ttu-id="17cdf-257">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span><span class="sxs-lookup"><span data-stu-id="17cdf-257">**Fail**: Each bolt can call `this.ctx.Fail(tuple)` to indicate that processing has failed for a tuple.</span></span> <span data-ttu-id="17cdf-258">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span><span class="sxs-lookup"><span data-stu-id="17cdf-258">The failure propagates to the `Fail` method of the spout, where the tuple can be replayed by using cached metadata.</span></span>

* <span data-ttu-id="17cdf-259">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span><span class="sxs-lookup"><span data-stu-id="17cdf-259">**Sequence ID**: When emitting a tuple, a unique sequence ID can be specified.</span></span> <span data-ttu-id="17cdf-260">This value identifies the tuple for replay (Ack and Fail) processing.</span><span class="sxs-lookup"><span data-stu-id="17cdf-260">This value identifies the tuple for replay (Ack and Fail) processing.</span></span> <span data-ttu-id="17cdf-261">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span><span class="sxs-lookup"><span data-stu-id="17cdf-261">For example, the spout in the **Storm Sample** project uses the following when emitting data:</span></span>

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    <span data-ttu-id="17cdf-262">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-262">This code emits a tuple that contains a sentence to the default stream, with the sequence ID value contained in **lastSeqId**.</span></span> <span data-ttu-id="17cdf-263">For this example, **lastSeqId** is incremented for every tuple emitted.</span><span class="sxs-lookup"><span data-stu-id="17cdf-263">For this example, **lastSeqId** is incremented for every tuple emitted.</span></span>

<span data-ttu-id="17cdf-264">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span><span class="sxs-lookup"><span data-stu-id="17cdf-264">As demonstrated in the **Storm Sample** project, whether a component is transactional can be set at runtime, based on configuration.</span></span>

## <a name="hybrid-topology-with-c-and-java"></a><span data-ttu-id="17cdf-265">Hybrid topology with C# and Java</span><span class="sxs-lookup"><span data-stu-id="17cdf-265">Hybrid topology with C# and Java</span></span>

<span data-ttu-id="17cdf-266">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span><span class="sxs-lookup"><span data-stu-id="17cdf-266">You can also use Data Lake tools for Visual Studio to create hybrid topologies, where some components are C# and others are Java.</span></span>

<span data-ttu-id="17cdf-267">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-267">For an example of a hybrid topology, create a project and select **Storm Hybrid Sample**.</span></span> <span data-ttu-id="17cdf-268">This sample type demonstrates the following concepts:</span><span class="sxs-lookup"><span data-stu-id="17cdf-268">This sample type demonstrates the following concepts:</span></span>

* <span data-ttu-id="17cdf-269">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-269">**Java spout** and **C# bolt**: Defined in **HybridTopology_javaSpout_csharpBolt**.</span></span>

    * <span data-ttu-id="17cdf-270">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-270">A transactional version is defined in **HybridTopologyTx_javaSpout_csharpBolt**.</span></span>

* <span data-ttu-id="17cdf-271">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-271">**C# spout** and **Java bolt**: Defined in **HybridTopology_csharpSpout_javaBolt**.</span></span>

    * <span data-ttu-id="17cdf-272">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-272">A transactional version is defined in **HybridTopologyTx_csharpSpout_javaBolt**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="17cdf-273">This version also demonstrates how to use Clojure code from a text file as a Java component.</span><span class="sxs-lookup"><span data-stu-id="17cdf-273">This version also demonstrates how to use Clojure code from a text file as a Java component.</span></span>


<span data-ttu-id="17cdf-274">To switch the topology that is used when the project is submitted, move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-274">To switch the topology that is used when the project is submitted, move the `[Active(true)]` statement to the topology you want to use, before submitting it to the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="17cdf-275">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span><span class="sxs-lookup"><span data-stu-id="17cdf-275">All the Java files that are required are provided as part of this project in the **JavaDependency** folder.</span></span>

<span data-ttu-id="17cdf-276">Consider the following when you are creating and submitting a hybrid topology:</span><span class="sxs-lookup"><span data-stu-id="17cdf-276">Consider the following when you are creating and submitting a hybrid topology:</span></span>

* <span data-ttu-id="17cdf-277">Use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span><span class="sxs-lookup"><span data-stu-id="17cdf-277">Use **JavaComponentConstructor** to create an instance of the Java class for a spout or bolt.</span></span>

* <span data-ttu-id="17cdf-278">Use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span><span class="sxs-lookup"><span data-stu-id="17cdf-278">Use **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** to serialize data into or out of Java components from Java objects to JSON.</span></span>

* <span data-ttu-id="17cdf-279">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-279">When submitting the topology to the server, you must use the **Additional configurations** option to specify the **Java File paths**.</span></span> <span data-ttu-id="17cdf-280">The path specified should be the directory that contains the JAR files that contain your Java classes.</span><span class="sxs-lookup"><span data-stu-id="17cdf-280">The path specified should be the directory that contains the JAR files that contain your Java classes.</span></span>

### <a name="azure-event-hubs"></a><span data-ttu-id="17cdf-281">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="17cdf-281">Azure Event Hubs</span></span>

<span data-ttu-id="17cdf-282">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span><span class="sxs-lookup"><span data-stu-id="17cdf-282">SCP.NET version 0.9.4.203 introduces a new class and method specifically for working with the Event Hub spout (a Java spout that reads from Event Hubs).</span></span> <span data-ttu-id="17cdf-283">When you create a topology that uses an Event Hub spout, use the following methods:</span><span class="sxs-lookup"><span data-stu-id="17cdf-283">When you create a topology that uses an Event Hub spout, use the following methods:</span></span>

* <span data-ttu-id="17cdf-284">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span><span class="sxs-lookup"><span data-stu-id="17cdf-284">**EventHubSpoutConfig** class: Creates an object that contains the configuration for the spout component.</span></span>

* <span data-ttu-id="17cdf-285">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span><span class="sxs-lookup"><span data-stu-id="17cdf-285">**TopologyBuilder.SetEventHubSpout** method: Adds the Event Hub spout component to the topology.</span></span>

> [!NOTE]
> <span data-ttu-id="17cdf-286">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span><span class="sxs-lookup"><span data-stu-id="17cdf-286">You must still use the **CustomizedInteropJSONSerializer** to serialize data produced by the spout.</span></span>

## <a id="configurationmanager"></a><span data-ttu-id="17cdf-287">Use ConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="17cdf-287">Use ConfigurationManager</span></span>

<span data-ttu-id="17cdf-288">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span><span class="sxs-lookup"><span data-stu-id="17cdf-288">Don't use **ConfigurationManager** to retrieve configuration values from bolt and spout components.</span></span> <span data-ttu-id="17cdf-289">Doing so can cause a null pointer exception.</span><span class="sxs-lookup"><span data-stu-id="17cdf-289">Doing so can cause a null pointer exception.</span></span> <span data-ttu-id="17cdf-290">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span><span class="sxs-lookup"><span data-stu-id="17cdf-290">Instead, the configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="17cdf-291">Each component that relies on configuration values must retrieve them from the context during initialization.</span><span class="sxs-lookup"><span data-stu-id="17cdf-291">Each component that relies on configuration values must retrieve them from the context during initialization.</span></span>

<span data-ttu-id="17cdf-292">The following code demonstrates how to retrieve these values:</span><span class="sxs-lookup"><span data-stu-id="17cdf-292">The following code demonstrates how to retrieve these values:</span></span>

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

<span data-ttu-id="17cdf-293">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span><span class="sxs-lookup"><span data-stu-id="17cdf-293">If you use a `Get` method to return an instance of your component, you must ensure that it passes both the `Context` and `Dictionary<string, Object>` parameters to the constructor.</span></span> <span data-ttu-id="17cdf-294">The following example is a basic `Get` method that properly passes these values:</span><span class="sxs-lookup"><span data-stu-id="17cdf-294">The following example is a basic `Get` method that properly passes these values:</span></span>

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-to-update-scpnet"></a><span data-ttu-id="17cdf-295">How to update SCP.NET</span><span class="sxs-lookup"><span data-stu-id="17cdf-295">How to update SCP.NET</span></span>

<span data-ttu-id="17cdf-296">Recent releases of SCP.NET support package upgrade through NuGet.</span><span class="sxs-lookup"><span data-stu-id="17cdf-296">Recent releases of SCP.NET support package upgrade through NuGet.</span></span> <span data-ttu-id="17cdf-297">When a new update is available, you receive an upgrade notification.</span><span class="sxs-lookup"><span data-stu-id="17cdf-297">When a new update is available, you receive an upgrade notification.</span></span> <span data-ttu-id="17cdf-298">To manually check for an upgrade, follow these steps:</span><span class="sxs-lookup"><span data-stu-id="17cdf-298">To manually check for an upgrade, follow these steps:</span></span>

1. <span data-ttu-id="17cdf-299">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-299">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>

2. <span data-ttu-id="17cdf-300">From the package manager, select **Updates**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-300">From the package manager, select **Updates**.</span></span> <span data-ttu-id="17cdf-301">If an update is available, it is listed.</span><span class="sxs-lookup"><span data-stu-id="17cdf-301">If an update is available, it is listed.</span></span> <span data-ttu-id="17cdf-302">Click **Update** for the package to install it.</span><span class="sxs-lookup"><span data-stu-id="17cdf-302">Click **Update** for the package to install it.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17cdf-303">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span><span class="sxs-lookup"><span data-stu-id="17cdf-303">If your project was created with an earlier version of SCP.NET that did not use NuGet, you must perform the following steps to update to a newer version:</span></span>
>
> 1. <span data-ttu-id="17cdf-304">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-304">In **Solution Explorer**, right-click the project, and select **Manage NuGet Packages**.</span></span>
> 2. <span data-ttu-id="17cdf-305">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-305">Using the **Search** field, search for, and then add, **Microsoft.SCP.Net.SDK** to the project.</span></span>

## <a name="troubleshoot-common-issues-with-topologies"></a><span data-ttu-id="17cdf-306">Troubleshoot common issues with topologies</span><span class="sxs-lookup"><span data-stu-id="17cdf-306">Troubleshoot common issues with topologies</span></span>

### <a name="null-pointer-exceptions"></a><span data-ttu-id="17cdf-307">Null pointer exceptions</span><span class="sxs-lookup"><span data-stu-id="17cdf-307">Null pointer exceptions</span></span>

<span data-ttu-id="17cdf-308">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span><span class="sxs-lookup"><span data-stu-id="17cdf-308">When you are using a C# topology with a Linux-based HDInsight cluster, bolt and spout components that use **ConfigurationManager** to read configuration settings at runtime may return null pointer exceptions.</span></span>

<span data-ttu-id="17cdf-309">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span><span class="sxs-lookup"><span data-stu-id="17cdf-309">The configuration for your project is passed into the Storm topology as a key and value pair in the topology context.</span></span> <span data-ttu-id="17cdf-310">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span><span class="sxs-lookup"><span data-stu-id="17cdf-310">It can be retrieved from the dictionary object that is passed to your components when they are initialized.</span></span>

<span data-ttu-id="17cdf-311">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span><span class="sxs-lookup"><span data-stu-id="17cdf-311">For more information, see the [ConfigurationManager](#configurationmanager) section of this document.</span></span>

### <a name="systemtypeloadexception"></a><span data-ttu-id="17cdf-312">System.TypeLoadException</span><span class="sxs-lookup"><span data-stu-id="17cdf-312">System.TypeLoadException</span></span>

<span data-ttu-id="17cdf-313">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span><span class="sxs-lookup"><span data-stu-id="17cdf-313">When you are using a C# topology with a Linux-based HDInsight cluster, you may encounter the following error:</span></span>

    System.TypeLoadException: Failure has occurred while loading a type.

<span data-ttu-id="17cdf-314">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span><span class="sxs-lookup"><span data-stu-id="17cdf-314">This error occurs when you use a binary that is not compatible with the version of .NET that Mono supports.</span></span>

<span data-ttu-id="17cdf-315">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span><span class="sxs-lookup"><span data-stu-id="17cdf-315">For Linux-based HDInsight clusters, make sure that your project uses binaries compiled for .NET 4.5.</span></span>

### <a name="test-a-topology-locally"></a><span data-ttu-id="17cdf-316">Test a topology locally</span><span class="sxs-lookup"><span data-stu-id="17cdf-316">Test a topology locally</span></span>

<span data-ttu-id="17cdf-317">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span><span class="sxs-lookup"><span data-stu-id="17cdf-317">Although it is easy to deploy a topology to a cluster, in some cases, you may need to test a topology locally.</span></span> <span data-ttu-id="17cdf-318">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span><span class="sxs-lookup"><span data-stu-id="17cdf-318">Use the following steps to run and test the example topology in this tutorial locally in your development environment.</span></span>

> [!WARNING]
> <span data-ttu-id="17cdf-319">Local testing only works for basic, C#-only topologies.</span><span class="sxs-lookup"><span data-stu-id="17cdf-319">Local testing only works for basic, C#-only topologies.</span></span> <span data-ttu-id="17cdf-320">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span><span class="sxs-lookup"><span data-stu-id="17cdf-320">You cannot use local testing for hybrid topologies or topologies that use multiple streams.</span></span>

1. <span data-ttu-id="17cdf-321">In **Solution Explorer**, right-click the project, and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-321">In **Solution Explorer**, right-click the project, and select **Properties**.</span></span> <span data-ttu-id="17cdf-322">In the project properties, change the **Output type** to **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-322">In the project properties, change the **Output type** to **Console Application**.</span></span>

    ![Screenshot of project properties, with Output type highlighted](./media/apache-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > <span data-ttu-id="17cdf-324">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-324">Remember to change the **Output type** back to **Class Library** before you deploy the topology to a cluster.</span></span>

2. <span data-ttu-id="17cdf-325">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-325">In **Solution Explorer**, right-click the project, and then select **Add** > **New Item**.</span></span> <span data-ttu-id="17cdf-326">Select **Class**, and enter **LocalTest.cs** as the class name.</span><span class="sxs-lookup"><span data-stu-id="17cdf-326">Select **Class**, and enter **LocalTest.cs** as the class name.</span></span> <span data-ttu-id="17cdf-327">Finally, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-327">Finally, click **Add**.</span></span>

3. <span data-ttu-id="17cdf-328">Open **LocalTest.cs**, and add the following **using** statement at the top:</span><span class="sxs-lookup"><span data-stu-id="17cdf-328">Open **LocalTest.cs**, and add the following **using** statement at the top:</span></span>

    ```csharp
    using Microsoft.SCP;
    ```

4. <span data-ttu-id="17cdf-329">Use the following code as the contents of the **LocalTest** class:</span><span class="sxs-lookup"><span data-stu-id="17cdf-329">Use the following code as the contents of the **LocalTest** class:</span></span>

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

    <span data-ttu-id="17cdf-330">Take a moment to read through the code comments.</span><span class="sxs-lookup"><span data-stu-id="17cdf-330">Take a moment to read through the code comments.</span></span> <span data-ttu-id="17cdf-331">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span><span class="sxs-lookup"><span data-stu-id="17cdf-331">This code uses **LocalContext** to run the components in the development environment, and it persists the data stream between components to text files on the local drive.</span></span>

1. <span data-ttu-id="17cdf-332">Open **Program.cs**, and add the following to the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="17cdf-332">Open **Program.cs**, and add the following to the **Main** method:</span></span>

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

2. <span data-ttu-id="17cdf-333">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-333">Save the changes, and then click **F5** or select **Debug** > **Start Debugging** to start the project.</span></span> <span data-ttu-id="17cdf-334">A console window should appear, and log status as the tests progress.</span><span class="sxs-lookup"><span data-stu-id="17cdf-334">A console window should appear, and log status as the tests progress.</span></span> <span data-ttu-id="17cdf-335">When **Tests finished** appears, press any key to close the window.</span><span class="sxs-lookup"><span data-stu-id="17cdf-335">When **Tests finished** appears, press any key to close the window.</span></span>

3. <span data-ttu-id="17cdf-336">Use **Windows Explorer** to locate the directory that contains your project.</span><span class="sxs-lookup"><span data-stu-id="17cdf-336">Use **Windows Explorer** to locate the directory that contains your project.</span></span> <span data-ttu-id="17cdf-337">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-337">For example: **C:\Users\<your_user_name>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**.</span></span> <span data-ttu-id="17cdf-338">In this directory, open **Bin**, and then click **Debug**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-338">In this directory, open **Bin**, and then click **Debug**.</span></span> <span data-ttu-id="17cdf-339">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span><span class="sxs-lookup"><span data-stu-id="17cdf-339">You should see the text files that were produced when the tests ran: sentences.txt, counter.txt, and splitter.txt.</span></span> <span data-ttu-id="17cdf-340">Open each text file and inspect the data.</span><span class="sxs-lookup"><span data-stu-id="17cdf-340">Open each text file and inspect the data.</span></span>

   > [!NOTE]
   > <span data-ttu-id="17cdf-341">String data persists as an array of decimal values in these files.</span><span class="sxs-lookup"><span data-stu-id="17cdf-341">String data persists as an array of decimal values in these files.</span></span> <span data-ttu-id="17cdf-342">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span><span class="sxs-lookup"><span data-stu-id="17cdf-342">For example, \[[97,103,111]] in the **splitter.txt** file is the word *and*.</span></span>

> [!NOTE]
> <span data-ttu-id="17cdf-343">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-343">Be sure to set the **Project type** back to **Class Library** before deploying to a Storm on HDInsight cluster.</span></span>

### <a name="log-information"></a><span data-ttu-id="17cdf-344">Log information</span><span class="sxs-lookup"><span data-stu-id="17cdf-344">Log information</span></span>

<span data-ttu-id="17cdf-345">You can easily log information from your topology components by using `Context.Logger`.</span><span class="sxs-lookup"><span data-stu-id="17cdf-345">You can easily log information from your topology components by using `Context.Logger`.</span></span> <span data-ttu-id="17cdf-346">For example, the following command creates an informational log entry:</span><span class="sxs-lookup"><span data-stu-id="17cdf-346">For example, the following command creates an informational log entry:</span></span>

```csharp
Context.Logger.Info("Component started");
```

<span data-ttu-id="17cdf-347">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-347">Logged information can be viewed from the **Hadoop Service Log**, which is found in **Server Explorer**.</span></span> <span data-ttu-id="17cdf-348">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-348">Expand the entry for your Storm on HDInsight cluster, and then expand **Hadoop Service Log**.</span></span> <span data-ttu-id="17cdf-349">Finally, select the log file to view.</span><span class="sxs-lookup"><span data-stu-id="17cdf-349">Finally, select the log file to view.</span></span>

> [!NOTE]
> <span data-ttu-id="17cdf-350">The logs are stored in the Azure storage account that is used by your cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-350">The logs are stored in the Azure storage account that is used by your cluster.</span></span> <span data-ttu-id="17cdf-351">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span><span class="sxs-lookup"><span data-stu-id="17cdf-351">To view the logs in Visual Studio, you must sign in to the Azure subscription that owns the storage account.</span></span>

### <a name="view-error-information"></a><span data-ttu-id="17cdf-352">View error information</span><span class="sxs-lookup"><span data-stu-id="17cdf-352">View error information</span></span>

<span data-ttu-id="17cdf-353">To view errors that have occurred in a running topology, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="17cdf-353">To view errors that have occurred in a running topology, use the following steps:</span></span>

1. <span data-ttu-id="17cdf-354">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span><span class="sxs-lookup"><span data-stu-id="17cdf-354">From **Server Explorer**, right-click the Storm on HDInsight cluster, and select **View Storm topologies**.</span></span>

2. <span data-ttu-id="17cdf-355">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span><span class="sxs-lookup"><span data-stu-id="17cdf-355">For the **Spout** and **Bolts**, the **Last Error** column contains information on the last error.</span></span>

3. <span data-ttu-id="17cdf-356">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span><span class="sxs-lookup"><span data-stu-id="17cdf-356">Select the **Spout Id** or **Bolt Id** for the component that has an error listed.</span></span> <span data-ttu-id="17cdf-357">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="17cdf-357">On the details page that is displayed, additional error information is listed in the **Errors** section at the bottom of the page.</span></span>

4. <span data-ttu-id="17cdf-358">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span><span class="sxs-lookup"><span data-stu-id="17cdf-358">To obtain more information, select a **Port** from the **Executors** section of the page, to see the Storm worker log for the last few minutes.</span></span>

### <a name="errors-submitting-topologies"></a><span data-ttu-id="17cdf-359">Errors submitting topologies</span><span class="sxs-lookup"><span data-stu-id="17cdf-359">Errors submitting topologies</span></span>

<span data-ttu-id="17cdf-360">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-360">If you encounter errors submitting a topology to HDInsight, you can find logs for the server-side components that handle topology submission on your HDInsight cluster.</span></span> <span data-ttu-id="17cdf-361">To retrieve these logs, use the following command from a command line:</span><span class="sxs-lookup"><span data-stu-id="17cdf-361">To retrieve these logs, use the following command from a command line:</span></span>

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

<span data-ttu-id="17cdf-362">Replace __sshuser__ with the SSH user account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-362">Replace __sshuser__ with the SSH user account for the cluster.</span></span> <span data-ttu-id="17cdf-363">Replace __clustername__ with the name of the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="17cdf-363">Replace __clustername__ with the name of the HDInsight cluster.</span></span> <span data-ttu-id="17cdf-364">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="17cdf-364">For more information on using `scp` and `ssh` with HDInsight, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="17cdf-365">Submissions can fail for multiple reasons:</span><span class="sxs-lookup"><span data-stu-id="17cdf-365">Submissions can fail for multiple reasons:</span></span>

* <span data-ttu-id="17cdf-366">JDK is not installed or is not in the path.</span><span class="sxs-lookup"><span data-stu-id="17cdf-366">JDK is not installed or is not in the path.</span></span>
* <span data-ttu-id="17cdf-367">Required Java dependencies are not included in the submission.</span><span class="sxs-lookup"><span data-stu-id="17cdf-367">Required Java dependencies are not included in the submission.</span></span>
* <span data-ttu-id="17cdf-368">Incompatible dependencies.</span><span class="sxs-lookup"><span data-stu-id="17cdf-368">Incompatible dependencies.</span></span>
* <span data-ttu-id="17cdf-369">Duplicate topology names.</span><span class="sxs-lookup"><span data-stu-id="17cdf-369">Duplicate topology names.</span></span>

<span data-ttu-id="17cdf-370">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span><span class="sxs-lookup"><span data-stu-id="17cdf-370">If the `hdinsight-scpwebapi.out` log contains a `FileNotFoundException`, this might be caused by the following conditions:</span></span>

* <span data-ttu-id="17cdf-371">The JDK is not in the path on the development environment.</span><span class="sxs-lookup"><span data-stu-id="17cdf-371">The JDK is not in the path on the development environment.</span></span> <span data-ttu-id="17cdf-372">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span><span class="sxs-lookup"><span data-stu-id="17cdf-372">Verify that the JDK is installed in the development environment, and that `%JAVA_HOME%/bin` is in the path.</span></span>
* <span data-ttu-id="17cdf-373">You are missing a Java dependency.</span><span class="sxs-lookup"><span data-stu-id="17cdf-373">You are missing a Java dependency.</span></span> <span data-ttu-id="17cdf-374">Make sure you are including any required .jar files as part of the submission.</span><span class="sxs-lookup"><span data-stu-id="17cdf-374">Make sure you are including any required .jar files as part of the submission.</span></span>

## <a name="next-steps"></a><span data-ttu-id="17cdf-375">Next steps</span><span class="sxs-lookup"><span data-stu-id="17cdf-375">Next steps</span></span>

<span data-ttu-id="17cdf-376">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](apache-storm-develop-csharp-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="17cdf-376">For an example of processing data from Event Hubs, see [Process events from Azure Event Hubs with Storm on HDInsight](apache-storm-develop-csharp-event-hub-topology.md).</span></span>

<span data-ttu-id="17cdf-377">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span><span class="sxs-lookup"><span data-stu-id="17cdf-377">For an example of a C# topology that splits stream data into multiple streams, see [C# Storm example](https://github.com/Blackmist/csharp-storm-example).</span></span>

<span data-ttu-id="17cdf-378">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span><span class="sxs-lookup"><span data-stu-id="17cdf-378">To discover more information about creating C# topologies, see [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).</span></span>

<span data-ttu-id="17cdf-379">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="17cdf-379">For more ways to work with HDInsight and more Storm on HDInsight samples, see the following documents:</span></span>

<span data-ttu-id="17cdf-380">**Microsoft SCP.NET**</span><span class="sxs-lookup"><span data-stu-id="17cdf-380">**Microsoft SCP.NET**</span></span>

* [<span data-ttu-id="17cdf-381">SCP programming guide</span><span class="sxs-lookup"><span data-stu-id="17cdf-381">SCP programming guide</span></span>](apache-storm-scp-programming-guide.md)

<span data-ttu-id="17cdf-382">**Apache Storm on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="17cdf-382">**Apache Storm on HDInsight**</span></span>

* [<span data-ttu-id="17cdf-383">Deploy and monitor topologies with Apache Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-383">Deploy and monitor topologies with Apache Storm on HDInsight</span></span>](apache-storm-deploy-monitor-topology.md)
* [<span data-ttu-id="17cdf-384">Example topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-384">Example topologies for Storm on HDInsight</span></span>](apache-storm-example-topology.md)

<span data-ttu-id="17cdf-385">**Apache Hadoop on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="17cdf-385">**Apache Hadoop on HDInsight**</span></span>

* [<span data-ttu-id="17cdf-386">Use Hive with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-386">Use Hive with Hadoop on HDInsight</span></span>](../hadoop/hdinsight-use-hive.md)
* [<span data-ttu-id="17cdf-387">Use Pig with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-387">Use Pig with Hadoop on HDInsight</span></span>](../hadoop/hdinsight-use-pig.md)
* [<span data-ttu-id="17cdf-388">Use MapReduce with Hadoop on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-388">Use MapReduce with Hadoop on HDInsight</span></span>](../hadoop/hdinsight-use-mapreduce.md)

<span data-ttu-id="17cdf-389">**Apache HBase on HDInsight**</span><span class="sxs-lookup"><span data-stu-id="17cdf-389">**Apache HBase on HDInsight**</span></span>

* [<span data-ttu-id="17cdf-390">Getting started with HBase on HDInsight</span><span class="sxs-lookup"><span data-stu-id="17cdf-390">Getting started with HBase on HDInsight</span></span>](../hbase/apache-hbase-tutorial-get-started-linux.md)
