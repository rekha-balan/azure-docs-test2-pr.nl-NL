---
title: Debug and analyze Hadoop services with heap dumps | Microsoft Docs
description: Automatically collect heap dumps for Hadoop services and place inside the Azure Blob storage account for debugging and analysis.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: e4ec4ebb-fd32-4668-8382-f956581485c4
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 937f4735f2babf6582787ed860e79d8e09ea3b7e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552407"
---
# <a name="collect-heap-dumps-in-blob-storage-to-debug-and-analyze-hadoop-services"></a><span data-ttu-id="08706-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span><span class="sxs-lookup"><span data-stu-id="08706-103">Collect heap dumps in Blob storage to debug and analyze Hadoop services</span></span>
[!INCLUDE [heapdump-selector](../../includes/hdinsight-selector-heap-dump.md)]

<span data-ttu-id="08706-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span><span class="sxs-lookup"><span data-stu-id="08706-104">Heap dumps contain a snapshot of the application's memory, including the values of variables at the time the dump was created.</span></span> <span data-ttu-id="08706-105">So they are very useful for diagnosing problems that occur at run-time.</span><span class="sxs-lookup"><span data-stu-id="08706-105">So they are very useful for diagnosing problems that occur at run-time.</span></span> <span data-ttu-id="08706-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span><span class="sxs-lookup"><span data-stu-id="08706-106">Heap dumps can be automatically collected for Hadoop services and placed inside the Azure Blob storage account of a user under HDInsightHeapDumps/.</span></span>

<span data-ttu-id="08706-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span><span class="sxs-lookup"><span data-stu-id="08706-107">The collection of heap dumps for various services must be enabled for services on individual clusters.</span></span> <span data-ttu-id="08706-108">The default for this feature is to be off for a cluster.</span><span class="sxs-lookup"><span data-stu-id="08706-108">The default for this feature is to be off for a cluster.</span></span> <span data-ttu-id="08706-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span><span class="sxs-lookup"><span data-stu-id="08706-109">These heap dumps can be large, so it is advisable to monitor the Blob storage account where they are being saved once the collection has been enabled.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08706-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="08706-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="08706-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="08706-111">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span> <span data-ttu-id="08706-112">The information in this article only applies to Windows-based HDInsight.</span><span class="sxs-lookup"><span data-stu-id="08706-112">The information in this article only applies to Windows-based HDInsight.</span></span> <span data-ttu-id="08706-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span><span class="sxs-lookup"><span data-stu-id="08706-113">For information on Linux-based HDInsight, see [Enable heap dumps for Hadoop services on Linux-based HDInsight](hdinsight-hadoop-collect-debug-heap-dump-linux.md)</span></span>


## <a name="eligible-services-for-heap-dumps"></a><span data-ttu-id="08706-114">Eligible services for heap dumps</span><span class="sxs-lookup"><span data-stu-id="08706-114">Eligible services for heap dumps</span></span>
<span data-ttu-id="08706-115">You can enable heap dumps for the following services:</span><span class="sxs-lookup"><span data-stu-id="08706-115">You can enable heap dumps for the following services:</span></span>

* <span data-ttu-id="08706-116">**hcatalog** - tempelton</span><span class="sxs-lookup"><span data-stu-id="08706-116">**hcatalog** - tempelton</span></span>
* <span data-ttu-id="08706-117">**hive** - hiveserver2, metastore, derbyserver</span><span class="sxs-lookup"><span data-stu-id="08706-117">**hive** - hiveserver2, metastore, derbyserver</span></span>
* <span data-ttu-id="08706-118">**mapreduce** - jobhistoryserver</span><span class="sxs-lookup"><span data-stu-id="08706-118">**mapreduce** - jobhistoryserver</span></span>
* <span data-ttu-id="08706-119">**yarn** - resourcemanager, nodemanager, timelineserver</span><span class="sxs-lookup"><span data-stu-id="08706-119">**yarn** - resourcemanager, nodemanager, timelineserver</span></span>
* <span data-ttu-id="08706-120">**hdfs** - datanode, secondarynamenode, namenode</span><span class="sxs-lookup"><span data-stu-id="08706-120">**hdfs** - datanode, secondarynamenode, namenode</span></span>

## <a name="configuration-elements-that-enable-heap-dumps"></a><span data-ttu-id="08706-121">Configuration elements that enable heap dumps</span><span class="sxs-lookup"><span data-stu-id="08706-121">Configuration elements that enable heap dumps</span></span>
<span data-ttu-id="08706-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span><span class="sxs-lookup"><span data-stu-id="08706-122">To turn on heap dumps for a service, you need to set the appropriate configuration elements in the section for that service, which is specified by **service_name**.</span></span>

    "javaargs.<service_name>.XX:+HeapDumpOnOutOfMemoryError" = "-XX:+HeapDumpOnOutOfMemoryError",
    "javaargs.<service_name>.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\Dumps\<service_name>_%date:~4,2%%date:~7,2%%date:~10,2%%time:~0,2%%time:~3,2%%time:~6,2%.hprof"

<span data-ttu-id="08706-123">The value of **service_name** can be any of the services listed above: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span><span class="sxs-lookup"><span data-stu-id="08706-123">The value of **service_name** can be any of the services listed above: tempelton, hiveserver2, metastore, derbyserver, jobhistoryserver, resourcemanager, nodemanager, timelineserver, datanode, secondarynamenode, or namenode.</span></span>

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="08706-124">Enable using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="08706-124">Enable using Azure PowerShell</span></span>
<span data-ttu-id="08706-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you would do the following:</span><span class="sxs-lookup"><span data-stu-id="08706-125">For example, to turn on heap dumps by using Azure PowerShell for jobhistoryserver, you would do the following:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $MapRedConfigValues = new-object 'Microsoft.WindowsAzure.Management.HDInsight.Cmdlet.DataObjects.AzureHDInsightMapReduceConfiguration'

    $MapRedConfigValues.Configuration = @{ "javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError"="-XX:+HeapDumpOnOutOfMemoryError" ; "javaargs.jobhistoryserver.XX:HeapDumpPath" = "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof" }

## <a name="enable-using-net-sdk"></a><span data-ttu-id="08706-126">Enable using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="08706-126">Enable using .NET SDK</span></span>
<span data-ttu-id="08706-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you would do the following:</span><span class="sxs-lookup"><span data-stu-id="08706-127">For example, to turn on heap dumps by using the Azure HDInsight .NET SDK for jobhistoryserver, you would do the following:</span></span>

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:+HeapDumpOnOutOfMemoryError", "-XX:+HeapDumpOnOutOfMemoryError"));

    clusterInfo.MapReduceConfiguration.ConfigurationCollection.Add(new KeyValuePair<string, string>("javaargs.jobhistoryserver.XX:HeapDumpPath", "-XX:HeapDumpPath=c:\\Dumps\\jobhistoryserver_%date:~4,2%_%date:~7,2%_%date:~10,2%_%time:~0,2%_%time:~3,2%_%time:~6,2%.hprof"));
