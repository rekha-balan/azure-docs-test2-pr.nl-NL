---
title: Correlate events over time with Storm and HBase on HDInsight
description: Learn how to correlate events that arrive at different times by using Storm and HBase on HDInsight.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 2deb309e4f030ddb7397538cf959cf162ce23d4f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540703"
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="3fa4b-103">Correlate events that arrive at different times using Storm and HBase</span><span class="sxs-lookup"><span data-stu-id="3fa4b-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="3fa4b-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="3fa4b-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="3fa4b-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="3fa4b-107">The topology uses HBase as a persistent data store.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="3fa4b-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="3fa4b-109">For example, how many user sessions were started or ended during a specific time period.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fa4b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="3fa4b-110">Prerequisites</span></span>

* <span data-ttu-id="3fa4b-111">Visual Studio and the HDInsight tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="3fa4b-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="3fa4b-113">Apache Storm on HDInsight cluster (Windows-based).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3fa4b-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux.</span></span>

* <span data-ttu-id="3fa4b-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="3fa4b-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3fa4b-117">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-117">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="3fa4b-118">[Java](https://java.com) 1.7 or greater on your development environment.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="3fa4b-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="3fa4b-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="3fa4b-121">The **%JAVA_HOME%/bin** directory must be in the path</span><span class="sxs-lookup"><span data-stu-id="3fa4b-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="3fa4b-122">Architecture</span><span class="sxs-lookup"><span data-stu-id="3fa4b-122">Architecture</span></span>

![Diagram of the data flow through the topology](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="3fa4b-124">Correlating events requires a common identifier for the event source.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="3fa4b-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="3fa4b-126">This example uses a GUID value to represent a session ID.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="3fa4b-127">This example consists of two HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="3fa4b-128">HBase: persistent data store for historical data</span><span class="sxs-lookup"><span data-stu-id="3fa4b-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="3fa4b-129">Storm: used to ingest incoming data</span><span class="sxs-lookup"><span data-stu-id="3fa4b-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="3fa4b-130">The data is randomly generated by the Storm topology, and consists of the following items:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="3fa4b-131">Session ID: a GUID that uniquely identifies each session</span><span class="sxs-lookup"><span data-stu-id="3fa4b-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="3fa4b-132">Event: a START or END event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-132">Event: a START or END event.</span></span> <span data-ttu-id="3fa4b-133">For this example, START always occurs before END</span><span class="sxs-lookup"><span data-stu-id="3fa4b-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="3fa4b-134">Time: the time of the event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-134">Time: the time of the event.</span></span>

<span data-ttu-id="3fa4b-135">This data is processed and stored in HBase.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="3fa4b-136">Storm topology</span><span class="sxs-lookup"><span data-stu-id="3fa4b-136">Storm topology</span></span>

<span data-ttu-id="3fa4b-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="3fa4b-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="3fa4b-139">This **Duration** value is then stored in HBase along with the **END** event information.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3fa4b-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="3fa4b-141">Events arriving out of order</span><span class="sxs-lookup"><span data-stu-id="3fa4b-141">Events arriving out of order</span></span>
> * <span data-ttu-id="3fa4b-142">Duplicate events</span><span class="sxs-lookup"><span data-stu-id="3fa4b-142">Duplicate events</span></span>
> * <span data-ttu-id="3fa4b-143">Dropped events</span><span class="sxs-lookup"><span data-stu-id="3fa4b-143">Dropped events</span></span>

<span data-ttu-id="3fa4b-144">The sample topology is composed of the following components:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="3fa4b-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="3fa4b-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="3fa4b-147">Then recycles ended sessions to generate new ones.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="3fa4b-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="3fa4b-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="3fa4b-150">HBaseBolt.cs: Stores information into HBase.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="3fa4b-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="3fa4b-152">HBase schema</span><span class="sxs-lookup"><span data-stu-id="3fa4b-152">HBase schema</span></span>

<span data-ttu-id="3fa4b-153">In HBase, the data is stored in a table with the following schema/settings:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="3fa4b-154">Row key: the session ID is used as the key for rows in this table.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="3fa4b-155">Column family: the family name is 'cf'.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="3fa4b-156">Columns stored in this family are:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="3fa4b-157">event: START or END.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-157">event: START or END.</span></span>

  * <span data-ttu-id="3fa4b-158">time: the time in milliseconds that the event occurred.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="3fa4b-159">duration: the length between START and END event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="3fa4b-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3fa4b-161">Versions are a log of previous values stored for a specific row key.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="3fa4b-162">By default, HBase only returns the value for the most recent version of a row.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="3fa4b-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="3fa4b-164">Versions provide a historical view of events logged for a specific ID.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="3fa4b-165">Download the project</span><span class="sxs-lookup"><span data-stu-id="3fa4b-165">Download the project</span></span>

<span data-ttu-id="3fa4b-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="3fa4b-167">This download contains the following C# projects:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="3fa4b-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="3fa4b-169">Each session lasts between 1 and 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="3fa4b-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="3fa4b-171">Create the table</span><span class="sxs-lookup"><span data-stu-id="3fa4b-171">Create the table</span></span>

1. <span data-ttu-id="3fa4b-172">Open the **SessionInfo** project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="3fa4b-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Screenshot of menu with properties selected](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="3fa4b-175">Select **Settings**, then set the following values:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="3fa4b-176">HBaseClusterURL: the URL to your HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="3fa4b-177">For example, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="3fa4b-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span><span class="sxs-lookup"><span data-stu-id="3fa4b-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="3fa4b-179">HBaseClusterPassword: the password for the admin/HTTP user account</span><span class="sxs-lookup"><span data-stu-id="3fa4b-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="3fa4b-180">HBaseTableName: the name of the table to use with this example</span><span class="sxs-lookup"><span data-stu-id="3fa4b-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="3fa4b-181">HBaseTableColumnFamily: The column family name</span><span class="sxs-lookup"><span data-stu-id="3fa4b-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Image of settings dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="3fa4b-183">Run the solution.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-183">Run the solution.</span></span> <span data-ttu-id="3fa4b-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="3fa4b-185">Build and deploy the Storm topology</span><span class="sxs-lookup"><span data-stu-id="3fa4b-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="3fa4b-186">Open the **CorrelationTopology** solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="3fa4b-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="3fa4b-188">In the properties window, select **Settings** and enter the configuration values for this project.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="3fa4b-189">The first 5 are the same values used by the **SessionInfo** project:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="3fa4b-190">HBaseClusterURL: the URL to your HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="3fa4b-191">For example, https://myhbasecluster.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="3fa4b-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="3fa4b-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="3fa4b-194">HBaseTableName: the name of the table to use with this example.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="3fa4b-195">This value is the same table name as used in the SessionInfo project.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="3fa4b-196">HBaseTableColumnFamily: The column family name.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="3fa4b-197">This value is the same column family name as used in the SessionInfo project.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="3fa4b-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="3fa4b-199">Save the properties, then build the project.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="3fa4b-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="3fa4b-201">If prompted, enter the credentials for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Image of the submit to storm menu item](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="3fa4b-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fa4b-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="3fa4b-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="3fa4b-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Image of the topology view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="3fa4b-208">When the topology begins generating data, the value in the **Emitted** column increments.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3fa4b-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="3fa4b-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="3fa4b-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span><span class="sxs-lookup"><span data-stu-id="3fa4b-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="3fa4b-212">Query the data</span><span class="sxs-lookup"><span data-stu-id="3fa4b-212">Query the data</span></span>

<span data-ttu-id="3fa4b-213">Once data has been emitted, use the following steps to query the data.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="3fa4b-214">Return to the **SessionInfo** project.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="3fa4b-215">If not running, start a new instance of it.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="3fa4b-216">When prompted, select **s** to search for START event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="3fa4b-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="3fa4b-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="3fa4b-219">For example, 11:20pm.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="3fa4b-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="3fa4b-221">The return data contains entries similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="3fa4b-222">Searching for END events works the same as START events.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="3fa4b-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="3fa4b-224">You may have to try a few time ranges to find the END events.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="3fa4b-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="3fa4b-226">Here is an example of data for END events:</span><span class="sxs-lookup"><span data-stu-id="3fa4b-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="3fa4b-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="3fa4b-228">Stop the topology</span><span class="sxs-lookup"><span data-stu-id="3fa4b-228">Stop the topology</span></span>

<span data-ttu-id="3fa4b-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="3fa4b-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span><span class="sxs-lookup"><span data-stu-id="3fa4b-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="3fa4b-231">Delete your cluster</span><span class="sxs-lookup"><span data-stu-id="3fa4b-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="3fa4b-232">Next steps</span><span class="sxs-lookup"><span data-stu-id="3fa4b-232">Next steps</span></span>

<span data-ttu-id="3fa4b-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3fa4b-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>





