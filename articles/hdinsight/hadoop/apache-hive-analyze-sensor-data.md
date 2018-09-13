---
title: Analyze sensor data using Hive and Hadoop - Azure HDInsight
description: Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel with PowerView.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.topic: conceptual
ms.date: 04/14/2017
ROBOTS: NOINDEX
ms.openlocfilehash: f82bac1b478183cad41e1bb9f7dce3fed8b5417b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856548"
---
# <a name="analyze-sensor-data-using-the-hive-query-console-on-hadoop-in-hdinsight"></a><span data-ttu-id="60e11-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="60e11-103">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>

<span data-ttu-id="60e11-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span><span class="sxs-lookup"><span data-stu-id="60e11-104">Learn how to analyze sensor data by using the Hive Query Console with HDInsight (Hadoop), then visualize the data in Microsoft Excel by using Power View.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="60e11-105">The steps in this document only work with Windows-based HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="60e11-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="60e11-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="60e11-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="60e11-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="60e11-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="60e11-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="60e11-108">For more information, see [HDInsight retirement on Windows](../hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


<span data-ttu-id="60e11-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span><span class="sxs-lookup"><span data-stu-id="60e11-109">In this sample, you use Hive to process historical data and identify problems with heating and air conditioning systems.</span></span> <span data-ttu-id="60e11-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span><span class="sxs-lookup"><span data-stu-id="60e11-110">Specifically, you identify systems are not able to reliably maintain a set temperature by performing the following tasks:</span></span>

* <span data-ttu-id="60e11-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span><span class="sxs-lookup"><span data-stu-id="60e11-111">Create HIVE tables to query data stored in comma-separated value (CSV) files.</span></span>
* <span data-ttu-id="60e11-112">Create HIVE queries to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="60e11-112">Create HIVE queries to analyze the data.</span></span>
* <span data-ttu-id="60e11-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span><span class="sxs-lookup"><span data-stu-id="60e11-113">To retrieve the analyzed data, use Microsoft Excel to connect to HDInsight.</span></span>
* <span data-ttu-id="60e11-114">To visualize the data, use Power View.</span><span class="sxs-lookup"><span data-stu-id="60e11-114">To visualize the data, use Power View.</span></span>

![A diagram of the solution architecture](./media/apache-hive-analyze-sensor-data/hvac-architecture.png)

## <a name="prerequisites"></a><span data-ttu-id="60e11-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="60e11-116">Prerequisites</span></span>

* <span data-ttu-id="60e11-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span><span class="sxs-lookup"><span data-stu-id="60e11-117">An HDInsight (Hadoop) cluster: See [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md) for information about creating a cluster.</span></span>
* <span data-ttu-id="60e11-118">Microsoft Excel 2013</span><span class="sxs-lookup"><span data-stu-id="60e11-118">Microsoft Excel 2013</span></span>

  > [!NOTE]
  > <span data-ttu-id="60e11-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span><span class="sxs-lookup"><span data-stu-id="60e11-119">Microsoft Excel is used for data visualization with [Power View](https://support.office.com/Article/Power-View-Explore-visualize-and-present-your-data-98268d31-97e2-42aa-a52b-a68cf460472e?ui=en-US&rs=en-US&ad=US).</span></span>

* [<span data-ttu-id="60e11-120">Microsoft Hive ODBC Driver</span><span class="sxs-lookup"><span data-stu-id="60e11-120">Microsoft Hive ODBC Driver</span></span>](http://www.microsoft.com/download/details.aspx?id=40886)

## <a name="to-run-the-sample"></a><span data-ttu-id="60e11-121">To run the sample</span><span class="sxs-lookup"><span data-stu-id="60e11-121">To run the sample</span></span>

1. <span data-ttu-id="60e11-122">From your web browser, navigate to the following URL:</span><span class="sxs-lookup"><span data-stu-id="60e11-122">From your web browser, navigate to the following URL:</span></span> 

         https://<clustername>.azurehdinsight.net

    <span data-ttu-id="60e11-123">Replace `<clustername>` with the name of your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="60e11-123">Replace `<clustername>` with the name of your HDInsight cluster.</span></span>

    <span data-ttu-id="60e11-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span><span class="sxs-lookup"><span data-stu-id="60e11-124">When prompted, authenticate by using the administrator user name and password you used when provisioning this cluster.</span></span>

2. <span data-ttu-id="60e11-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span><span class="sxs-lookup"><span data-stu-id="60e11-125">From the web page that opens, click the **Getting Started Gallery** tab, and then under the **Solutions with Sample Data** category, click the **Sensor Data Analysis** sample.</span></span>

    ![Getting started gallery image](./media/apache-hive-analyze-sensor-data/getting-started-gallery.png)

3. <span data-ttu-id="60e11-127">Follow the instructions provided on the web page to finish the sample.</span><span class="sxs-lookup"><span data-stu-id="60e11-127">Follow the instructions provided on the web page to finish the sample.</span></span>
