---
title: Use Hive with Hadoop for website log analysis - Azure HDInsight
description: Learn how to use Hive with HDInsight to analyze website logs. You'll use a log file as input into an HDInsight table, and use HiveQL to query the data.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: conceptual
ms.date: 05/17/2016
ms.author: jasonh
ROBOTS: NOINDEX
ms.openlocfilehash: 47175ed4bc01a43d1f21cbfc84b8a788f11b7338
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870429"
---
# <a name="use-hive-with-windows-based-hdinsight-to-analyze-logs-from-websites"></a><span data-ttu-id="527c4-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span><span class="sxs-lookup"><span data-stu-id="527c4-104">Use Hive with Windows-based HDInsight to analyze logs from websites</span></span>
<span data-ttu-id="527c4-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span><span class="sxs-lookup"><span data-stu-id="527c4-105">Learn how to use HiveQL with HDInsight to analyze logs from a website.</span></span> <span data-ttu-id="527c4-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span><span class="sxs-lookup"><span data-stu-id="527c4-106">Website log analysis can be used to segment your audience based on similar activities, categorize site visitors by demographics, and to find out the content they view, the websites they come from, and so on.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="527c4-107">The steps in this document only work with Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="527c4-107">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="527c4-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="527c4-108">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="527c4-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="527c4-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="527c4-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="527c4-110">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="527c4-111">In this sample, you use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span><span class="sxs-lookup"><span data-stu-id="527c4-111">In this sample, you use an HDInsight cluster to analyze website log files to get insight into the frequency of visits to the website from external websites in a day.</span></span> <span data-ttu-id="527c4-112">You also generate a summary of website errors that the users experience.</span><span class="sxs-lookup"><span data-stu-id="527c4-112">You also generate a summary of website errors that the users experience.</span></span> <span data-ttu-id="527c4-113">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="527c4-113">You learn how to:</span></span>

* <span data-ttu-id="527c4-114">Connect to an Azure Blob storage, which contains website log files.</span><span class="sxs-lookup"><span data-stu-id="527c4-114">Connect to an Azure Blob storage, which contains website log files.</span></span>
* <span data-ttu-id="527c4-115">Create HIVE tables to query those logs.</span><span class="sxs-lookup"><span data-stu-id="527c4-115">Create HIVE tables to query those logs.</span></span>
* <span data-ttu-id="527c4-116">Create HIVE queries to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="527c4-116">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="527c4-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span><span class="sxs-lookup"><span data-stu-id="527c4-117">Use Microsoft Excel to connect to HDInsight (by using open database connectivity (ODBC) to retrieve the analyzed data.</span></span>

![HDI.Samples.Website.Log.Analysis](./media/apache-hive-analyze-website-log/hdinsight-weblogs-sample.png)

## <a name="prerequisites"></a><span data-ttu-id="527c4-119">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="527c4-119">Prerequisites</span></span>
* <span data-ttu-id="527c4-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="527c4-120">You must have provisioned a Hadoop cluster on Azure HDInsight.</span></span> <span data-ttu-id="527c4-121">For instructions, see [Provision HDInsight Clusters](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="527c4-121">For instructions, see [Provision HDInsight Clusters](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="527c4-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span><span class="sxs-lookup"><span data-stu-id="527c4-122">You must have Microsoft Excel 2013 or Excel 2010 installed.</span></span>
* <span data-ttu-id="527c4-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span><span class="sxs-lookup"><span data-stu-id="527c4-123">You must have [Microsoft Hive ODBC Driver](http://www.microsoft.com/download/details.aspx?id=40886) to import data from Hive into Excel.</span></span>

## <a name="to-run-the-sample"></a><span data-ttu-id="527c4-124">To run the sample</span><span class="sxs-lookup"><span data-stu-id="527c4-124">To run the sample</span></span>
1. <span data-ttu-id="527c4-125">From the [Azure portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span><span class="sxs-lookup"><span data-stu-id="527c4-125">From the [Azure portal](https://portal.azure.com/), from the Startboard (if you pinned the cluster there), click the cluster tile on which you want to run the sample.</span></span>
2. <span data-ttu-id="527c4-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="527c4-126">From the cluster blade, under **Quick Links**, click **Cluster Dashboard**, and then from the **Cluster Dashboard** blade, click **HDInsight Cluster Dashboard**.</span></span> <span data-ttu-id="527c4-127">Alternatively, you can directly open the dashboard by using the following URL:</span><span class="sxs-lookup"><span data-stu-id="527c4-127">Alternatively, you can directly open the dashboard by using the following URL:</span></span>

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="527c4-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span><span class="sxs-lookup"><span data-stu-id="527c4-128">When prompted, authenticate by using the administrator user name and password you used when provisioning the cluster.</span></span>
3. <span data-ttu-id="527c4-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span><span class="sxs-lookup"><span data-stu-id="527c4-129">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Website Log Analysis** sample.</span></span>
4. <span data-ttu-id="527c4-130">Follow the instructions provided on the web page to finish the sample.</span><span class="sxs-lookup"><span data-stu-id="527c4-130">Follow the instructions provided on the web page to finish the sample.</span></span>

## <a name="next-steps"></a><span data-ttu-id="527c4-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="527c4-131">Next steps</span></span>
<span data-ttu-id="527c4-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](apache-hive-analyze-sensor-data.md).</span><span class="sxs-lookup"><span data-stu-id="527c4-132">Try the following sample: [Analyzing sensor data using Hive with HDInsight](apache-hive-analyze-sensor-data.md).</span></span>

[hdinsight-sensor-data-sample]: ../hdinsight-use-hive-sensor-data-analysis.md
