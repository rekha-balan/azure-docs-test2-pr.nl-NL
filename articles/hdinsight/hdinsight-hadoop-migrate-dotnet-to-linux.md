---
title: Use .NET with Hadoop MapReduce on Linux-based HDInsight - Azure | Microsoft Docs
description: Learn how to use .NET applications for streaming MapReduce on Linux-based HDInsight.
services: hdinsight
documentationCenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ''
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/12/2017
ms.author: larryfr
ms.openlocfilehash: 8a5eee116b9fe7652ba8ed59d78e6340a4c905ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540698"
---
# <a name="migrate-net-solutions-for-windows-based-hdinsight-to-linux-based-hdinsight"></a><span data-ttu-id="bcf0f-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf0f-103">Migrate .NET solutions for Windows-based HDInsight to Linux-based HDInsight</span></span>

<span data-ttu-id="bcf0f-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-104">Linux-based HDInsight clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="bcf0f-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-105">Mono allows you to use .NET components such as MapReduce applications with Linux-based HDInsight.</span></span> <span data-ttu-id="bcf0f-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-106">In this document, learn how to migrate .NET solutions created for Windows-based HDInsight clusters to work with Mono on Linux-based HDInsight.</span></span>

## <a name="mono-compatibility-with-net"></a><span data-ttu-id="bcf0f-107">Mono compatibility with .NET</span><span class="sxs-lookup"><span data-stu-id="bcf0f-107">Mono compatibility with .NET</span></span>

<span data-ttu-id="bcf0f-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-108">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="bcf0f-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0f-109">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="bcf0f-110">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-110">For detailed information on compatibility between Mono and .NET, see the [Mono compatibility (http://www.mono-project.com/docs/about-mono/compatibility/)](http://www.mono-project.com/docs/about-mono/compatibility/) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bcf0f-111">The SCP.NET framework is compatible with Mono.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-111">The SCP.NET framework is compatible with Mono.</span></span> <span data-ttu-id="bcf0f-112">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="bcf0f-112">For more information on using SCP.NET with Mono, see [Use Visual Studio to develop C# topologies for Apache Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

## <a name="automated-portability-analysis"></a><span data-ttu-id="bcf0f-113">Automated portability analysis</span><span class="sxs-lookup"><span data-stu-id="bcf0f-113">Automated portability analysis</span></span>

<span data-ttu-id="bcf0f-114">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-114">The [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer) can be used to generate a report of incompatibilities between your application and Mono.</span></span> <span data-ttu-id="bcf0f-115">Use the following steps to configure the analyzer to check your application for Mono portability:</span><span class="sxs-lookup"><span data-stu-id="bcf0f-115">Use the following steps to configure the analyzer to check your application for Mono portability:</span></span>

1. <span data-ttu-id="bcf0f-116">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span><span class="sxs-lookup"><span data-stu-id="bcf0f-116">Install the [.NET Portability Analyzer](https://marketplace.visualstudio.com/items?itemName=ConnieYau.NETPortabilityAnalyzer).</span></span> <span data-ttu-id="bcf0f-117">During installation, select the version of Visual Studio to use.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-117">During installation, select the version of Visual Studio to use.</span></span>

2. <span data-ttu-id="bcf0f-118">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-118">From Visual Studio 2015, select __Analyze__ > __Portability Analyzer Settings__, and make sure that __4.5__ is checked in the __Mono__ section.</span></span>

    ![4.5 checked in Mono section for the analyzer settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-settings.png)

    <span data-ttu-id="bcf0f-120">Select __OK__ to save the configuration.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-120">Select __OK__ to save the configuration.</span></span>

3. <span data-ttu-id="bcf0f-121">Select __Analyze__ > __Analyze Assembly Portability__.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-121">Select __Analyze__ > __Analyze Assembly Portability__.</span></span> <span data-ttu-id="bcf0f-122">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-122">Select the assembly that contains your solution, and then select __Open__ to begin analysis.</span></span>

4. <span data-ttu-id="bcf0f-123">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-123">Once analysis is complete, select __Analyze__ > __View analysis reports__.</span></span> <span data-ttu-id="bcf0f-124">In __Portability Analysis Results__, select __Open report__ to open a report.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-124">In __Portability Analysis Results__, select __Open report__ to open a report.</span></span>

    ![Portability analyzer results dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-migrate-dotnet-to-linux/portability-analyzer-results.png)

> [!IMPORTANT]
> <span data-ttu-id="bcf0f-126">The analyzer cannot catch every problem with your solution.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-126">The analyzer cannot catch every problem with your solution.</span></span> <span data-ttu-id="bcf0f-127">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-127">For example, a file path of `c:\temp\file.txt` is considered OK because Mono runs on Windows and the path is valid in that context.</span></span> <span data-ttu-id="bcf0f-128">However, the path is not valid on a Linux platform.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-128">However, the path is not valid on a Linux platform.</span></span>

## <a name="manual-portability-analysis"></a><span data-ttu-id="bcf0f-129">Manual portability analysis</span><span class="sxs-lookup"><span data-stu-id="bcf0f-129">Manual portability analysis</span></span>

<span data-ttu-id="bcf0f-130">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-130">Perform a manual audit of your code using the information in the [Application Portability (http://www.mono-project.com/docs/getting-started/application-portability/)](http://www.mono-project.com/docs/getting-started/application-portability/) document.</span></span>

## <a name="modify-and-build"></a><span data-ttu-id="bcf0f-131">Modify and build</span><span class="sxs-lookup"><span data-stu-id="bcf0f-131">Modify and build</span></span>

<span data-ttu-id="bcf0f-132">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-132">You can continue to use Visual Studio to build your .NET solutions for HDInsight.</span></span> <span data-ttu-id="bcf0f-133">However, you must ensure that the project is configured to use .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-133">However, you must ensure that the project is configured to use .NET Framework 4.5.</span></span>

## <a name="deploy-and-test"></a><span data-ttu-id="bcf0f-134">Deploy and test</span><span class="sxs-lookup"><span data-stu-id="bcf0f-134">Deploy and test</span></span>

<span data-ttu-id="bcf0f-135">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-135">Once you have modified your solution using the recommendations from the .NET Portability Analyzer or from a manual analysis, you must test it with HDInsight.</span></span> <span data-ttu-id="bcf0f-136">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-136">Testing the solution on a Linux-based HDInsight cluster may reveal subtle problems that need to be corrected.</span></span> <span data-ttu-id="bcf0f-137">We recommend that you enable additional logging in your application while testing it.</span><span class="sxs-lookup"><span data-stu-id="bcf0f-137">We recommend that you enable additional logging in your application while testing it.</span></span>

<span data-ttu-id="bcf0f-138">For more information on accessing logs, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="bcf0f-138">For more information on accessing logs, see the following documents:</span></span>

* [<span data-ttu-id="bcf0f-139">Analyze HDInsight logs</span><span class="sxs-lookup"><span data-stu-id="bcf0f-139">Analyze HDInsight logs</span></span>](hdinsight-debug-jobs.md)
* [<span data-ttu-id="bcf0f-140">Access YARN application logs on Linux-based HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf0f-140">Access YARN application logs on Linux-based HDInsight</span></span>](hdinsight-hadoop-access-yarn-app-logs-linux.md)

## <a name="next-steps"></a><span data-ttu-id="bcf0f-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="bcf0f-141">Next steps</span></span>

* [<span data-ttu-id="bcf0f-142">Use C# with MapReduce on HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf0f-142">Use C# with MapReduce on HDInsight</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="bcf0f-143">Use C# user defined functions with Hive and Pig</span><span class="sxs-lookup"><span data-stu-id="bcf0f-143">Use C# user defined functions with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="bcf0f-144">Develop C# topologies for Storm on HDInsight</span><span class="sxs-lookup"><span data-stu-id="bcf0f-144">Develop C# topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

