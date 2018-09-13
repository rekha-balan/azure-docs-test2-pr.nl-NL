---
title: Analyze sensor data using Hive and Hadoop | Microsoft Docs
description: Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel with PowerView.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: a8ac160c-1cef-45d9-bf36-7beb5a439105
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: cbeeeb696a5b3a558346a52f414be54ab38b6155
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549730"
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="af4dc-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="af4dc-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="af4dc-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span><span class="sxs-lookup"><span data-stu-id="af4dc-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="af4dc-105">The steps in this document only work with Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="af4dc-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="af4dc-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="af4dc-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="af4dc-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="af4dc-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="af4dc-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="af4dc-108">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>


<span data-ttu-id="af4dc-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span><span class="sxs-lookup"><span data-stu-id="af4dc-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="af4dc-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span><span class="sxs-lookup"><span data-stu-id="af4dc-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="af4dc-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span><span class="sxs-lookup"><span data-stu-id="af4dc-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="af4dc-112">Create HIVE queries to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="af4dc-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="af4dc-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="af4dc-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="af4dc-114">To visualize the data, use Power View.</span><span class="sxs-lookup"><span data-stu-id="af4dc-114">To visualize the data, use Power View.</span></span>

![A diagram of the solution architecture](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="af4dc-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="af4dc-116">Prerequisites</span></span>

* <span data-ttu-id="af4dc-117">An HDInsight (Hadoop) cluster: See [Provision Hadoop clusters in HDInsight](hdinsight-provision-clusters.md) for information about creating a cluster.</span><span class="sxs-lookup"><span data-stu-id="af4dc-117">An HDInsight (Hadoop) cluster: See [Provision Hadoop clusters in HDInsight](hdinsight-provision-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="af4dc-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="af4dc-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="af4dc-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="af4dc-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="af4dc-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="af4dc-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="af4dc-121">To run the sample</span><span class="sxs-lookup"><span data-stu-id="af4dc-121">To run the sample</span></span>

1. <span data-ttu-id="af4dc-122">From your web browser, navigate to the following URL:</span><span class="sxs-lookup"><span data-stu-id="af4dc-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="af4dc-123">Replace `<clustername>` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="af4dc-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="af4dc-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span><span class="sxs-lookup"><span data-stu-id="af4dc-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="af4dc-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span><span class="sxs-lookup"><span data-stu-id="af4dc-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Getting started gallery image](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="af4dc-127">Follow the instructions provided on the web page to finish the sample.</span><span class="sxs-lookup"><span data-stu-id="af4dc-127">Follow the instructions provided on the web page to finish the sample.</span></span>


