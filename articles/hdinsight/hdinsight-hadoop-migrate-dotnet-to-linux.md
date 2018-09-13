---
title: Use .NET with Hadoop MapReduce on Linux-based HDInsight - Azure
description: Learn how to use .NET applications for streaming MapReduce on Linux-based HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/27/2018
ms.author: jasonh
ms.openlocfilehash: f8a29c744d0ebfbab4127c421d0dba22e8d7ff52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773909"
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="e7bac-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7bac-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="e7bac-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="e7bac-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="e7bac-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7bac-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="e7bac-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7bac-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="e7bac-107">Mono compatibility with .NET</span><span class="sxs-lookup"><span data-stu-id="e7bac-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="e7bac-108">Mono version 4.2.1 is included with HDInsight version 3.6.</span><span class="sxs-lookup"><span data-stu-id="e7bac-108">Mono version 4.2.1 is included with HDInsight version 3.6.</span></span> <span data-ttu-id="e7bac-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="e7bac-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="e7bac-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="e7bac-110">To install a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="e7bac-111">For more information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span><span class="sxs-lookup"><span data-stu-id="e7bac-111">For more information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e7bac-112">The SCP.NET framework is compatible with Mono.</span><span class="sxs-lookup"><span data-stu-id="e7bac-112">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="e7bac-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](storm/apache-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e7bac-113">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](storm/apache-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="e7bac-114">Automated portability analysis</span><span class="sxs-lookup"><span data-stu-id="e7bac-114">Automated portability analysis</span></span>

<span data-ttu-id="e7bac-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span><span class="sxs-lookup"><span data-stu-id="e7bac-115">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="e7bac-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span><span class="sxs-lookup"><span data-stu-id="e7bac-116">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="e7bac-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="e7bac-117">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="e7bac-118">During installation, select the version of Visual Studio to use.</span><span class="sxs-lookup"><span data-stu-id="e7bac-118">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="e7bac-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span><span class="sxs-lookup"><span data-stu-id="e7bac-119">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 checked in Mono section for the analyzer settings](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="e7bac-121">Select __OK__ to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="e7bac-121">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="e7bac-122">Select __Analyze__ > __Analyze Assembly Portability__.</span><span class="sxs-lookup"><span data-stu-id="e7bac-122">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="e7bac-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span><span class="sxs-lookup"><span data-stu-id="e7bac-123">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="e7bac-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span><span class="sxs-lookup"><span data-stu-id="e7bac-124">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="e7bac-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span><span class="sxs-lookup"><span data-stu-id="e7bac-125">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Portability analyzer results dialog](./media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="e7bac-127">The analyzer cannot catch every problem with your solution.</span><span class="sxs-lookup"><span data-stu-id="e7bac-127">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="e7bac-128">For example, a file path of `c:\temp\file.txt` is considered OK if Mono is running on Windows.</span><span class="sxs-lookup"><span data-stu-id="e7bac-128">For example, a file path of `c:\temp\file.txt` is considered OK if Mono is running on Windows.</span></span> <span data-ttu-id="e7bac-129">The same path is not valid on a Linux platform.</span><span class="sxs-lookup"><span data-stu-id="e7bac-129">The same path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="e7bac-130">Manual portability analysis</span><span class="sxs-lookup"><span data-stu-id="e7bac-130">Manual portability analysis</span></span>

<span data-ttu-id="e7bac-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span><span class="sxs-lookup"><span data-stu-id="e7bac-131">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="e7bac-132">Modify and build</span><span class="sxs-lookup"><span data-stu-id="e7bac-132">Modify and build</span></span>

<span data-ttu-id="e7bac-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7bac-133">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="e7bac-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="e7bac-134">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="e7bac-135">Deploy and test</span><span class="sxs-lookup"><span data-stu-id="e7bac-135">Deploy and test</span></span>

<span data-ttu-id="e7bac-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e7bac-136">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="e7bac-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span><span class="sxs-lookup"><span data-stu-id="e7bac-137">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="e7bac-138">We recommend that you enable additional logging in your application while testing it.</span><span class="sxs-lookup"><span data-stu-id="e7bac-138">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="e7bac-139">For more information on accessing logs, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="e7bac-139">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="e7bac-140">Access YARN application logs on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7bac-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="e7bac-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="e7bac-141">Next steps</span></span>

* [<span data-ttu-id="e7bac-142">Use C# with MapReduce on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7bac-142">Use C# with MapReduce on HDInsight</span></span>](hadoop/apache-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="e7bac-143">Use C# user-defined functions with Hive and Pig</span><span class="sxs-lookup"><span data-stu-id="e7bac-143">Use C# user-defined functions with Hive and Pig</span></span>](hadoop/apache-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="e7bac-144">Develop C# topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="e7bac-144">Develop C# topologies for Storm on HDInsight</span></span>](storm/apache-storm-develop-csharp-visual-studio-topology.md)
