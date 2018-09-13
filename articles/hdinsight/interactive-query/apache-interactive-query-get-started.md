---
title: Use Interactive Query with Azure HDInsight
description: Learn how to use Interactive Query (Hive LLAP) with HDInsight.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 02/22/2018
ms.openlocfilehash: e83d51a18c7ab5861699114e4622bda167dab41d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867287"
---
# <a name="use-interactive-query-with-hdinsight"></a><span data-ttu-id="7c57a-103">Use Interactive Query with HDInsight</span><span class="sxs-lookup"><span data-stu-id="7c57a-103">Use Interactive Query with HDInsight</span></span>
<span data-ttu-id="7c57a-104">Interactive Query (also called Hive LLAP, or [Low Latency Analytical Processing](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is an Azure HDInsight [cluster type](../hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="7c57a-104">Interactive Query (also called Hive LLAP, or [Low Latency Analytical Processing](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is an Azure HDInsight [cluster type](../hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span> <span data-ttu-id="7c57a-105">Interactive Query supports in-memory caching, which makes Hive queries faster and much more interactive.</span><span class="sxs-lookup"><span data-stu-id="7c57a-105">Interactive Query supports in-memory caching, which makes Hive queries faster and much more interactive.</span></span>

[!INCLUDE [hdinsight-price-change](../../../includes/hdinsight-enhancements.md)] 

<span data-ttu-id="7c57a-106">An Interactive Query cluster is different from a Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="7c57a-106">An Interactive Query cluster is different from a Hadoop cluster.</span></span> <span data-ttu-id="7c57a-107">It contains only the Hive service.</span><span class="sxs-lookup"><span data-stu-id="7c57a-107">It contains only the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="7c57a-108">You can access the Hive service in the Interactive Query cluster only via Ambari Hive View, Beeline, and the Microsoft Hive Open Database Connectivity driver (Hive ODBC).</span><span class="sxs-lookup"><span data-stu-id="7c57a-108">You can access the Hive service in the Interactive Query cluster only via Ambari Hive View, Beeline, and the Microsoft Hive Open Database Connectivity driver (Hive ODBC).</span></span> <span data-ttu-id="7c57a-109">You can’t access it via the Hive console, Templeton, the Azure command-line tool (Azure CLI), or Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7c57a-109">You can’t access it via the Hive console, Templeton, the Azure command-line tool (Azure CLI), or Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-query-cluster"></a><span data-ttu-id="7c57a-110">Create an Interactive Query cluster</span><span class="sxs-lookup"><span data-stu-id="7c57a-110">Create an Interactive Query cluster</span></span>
<span data-ttu-id="7c57a-111">For information about creating a HDInsight cluster, see [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-111">For information about creating a HDInsight cluster, see [Create Hadoop clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="7c57a-112">Choose the Interactive Query cluster type.</span><span class="sxs-lookup"><span data-stu-id="7c57a-112">Choose the Interactive Query cluster type.</span></span>

## <a name="execute-hive-queries-from-interactive-query"></a><span data-ttu-id="7c57a-113">Execute Hive queries from Interactive Query</span><span class="sxs-lookup"><span data-stu-id="7c57a-113">Execute Hive queries from Interactive Query</span></span>
<span data-ttu-id="7c57a-114">To execute Hive queries, you have the following options:</span><span class="sxs-lookup"><span data-stu-id="7c57a-114">To execute Hive queries, you have the following options:</span></span>

* <span data-ttu-id="7c57a-115">Use Power BI</span><span class="sxs-lookup"><span data-stu-id="7c57a-115">Use Power BI</span></span>

    <span data-ttu-id="7c57a-116">See [Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./apache-hadoop-connect-hive-power-bi-directquery.md) See [Visualize big data with Power BI in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-116">See [Visualize Interactive Query Hive data with Power BI in Azure HDInsight](./apache-hadoop-connect-hive-power-bi-directquery.md) See [Visualize big data with Power BI in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span></span>
 
* <span data-ttu-id="7c57a-117">Use Zeppelin</span><span class="sxs-lookup"><span data-stu-id="7c57a-117">Use Zeppelin</span></span>

    <span data-ttu-id="7c57a-118">See [Use Zeppelin to run Hive queries in Azure HDInsight ](../hdinsight-connect-hive-zeppelin.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-118">See [Use Zeppelin to run Hive queries in Azure HDInsight ](../hdinsight-connect-hive-zeppelin.md).</span></span>

* <span data-ttu-id="7c57a-119">Use Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7c57a-119">Use Visual Studio</span></span>

    <span data-ttu-id="7c57a-120">See [Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-hive-queries).</span><span class="sxs-lookup"><span data-stu-id="7c57a-120">See [Connect to Azure HDInsight and run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-hive-queries).</span></span>

* <span data-ttu-id="7c57a-121">Use Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="7c57a-121">Use Visual Studio Code</span></span>

    <span data-ttu-id="7c57a-122">See [Use Visual Studio Code for Hive, LLAP or pySpark](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-122">See [Use Visual Studio Code for Hive, LLAP or pySpark](../hdinsight-for-vscode.md).</span></span>
* <span data-ttu-id="7c57a-123">Run Hive by using Ambari Hive View.</span><span class="sxs-lookup"><span data-stu-id="7c57a-123">Run Hive by using Ambari Hive View.</span></span>
  
    <span data-ttu-id="7c57a-124">See [Use Hive View with Hadoop in Azure HDInsight](../hadoop/apache-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-124">See [Use Hive View with Hadoop in Azure HDInsight](../hadoop/apache-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="7c57a-125">Run Hive by using Beeline.</span><span class="sxs-lookup"><span data-stu-id="7c57a-125">Run Hive by using Beeline.</span></span>
  
    <span data-ttu-id="7c57a-126">See [Use Hive with Hadoop in HDInsight with Beeline](../hadoop/apache-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-126">See [Use Hive with Hadoop in HDInsight with Beeline](../hadoop/apache-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="7c57a-127">You can use Beeline from either the head node or from an empty edge node.</span><span class="sxs-lookup"><span data-stu-id="7c57a-127">You can use Beeline from either the head node or from an empty edge node.</span></span> <span data-ttu-id="7c57a-128">We recommend using Beeline from an empty edge node.</span><span class="sxs-lookup"><span data-stu-id="7c57a-128">We recommend using Beeline from an empty edge node.</span></span> <span data-ttu-id="7c57a-129">For information about creating an HDInsight cluster by using an empty edge node, see [Use empty edge nodes in HDInsight](../hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-129">For information about creating an HDInsight cluster by using an empty edge node, see [Use empty edge nodes in HDInsight](../hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="7c57a-130">Run Hive by using Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="7c57a-130">Run Hive by using Hive ODBC.</span></span>
  
    <span data-ttu-id="7c57a-131">See [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-131">See [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="7c57a-132">To find the Java Database Connectivity (JDBC) connection string:</span><span class="sxs-lookup"><span data-stu-id="7c57a-132">To find the Java Database Connectivity (JDBC) connection string:</span></span>

1. <span data-ttu-id="7c57a-133">Sign in to Ambari by using the following URL: https://\<cluster name\>.AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="7c57a-133">Sign in to Ambari by using the following URL: https://\<cluster name\>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="7c57a-134">In the left menu, select **Hive**.</span><span class="sxs-lookup"><span data-stu-id="7c57a-134">In the left menu, select **Hive**.</span></span>
3. <span data-ttu-id="7c57a-135">To copy the URL, select the clipboard icon:</span><span class="sxs-lookup"><span data-stu-id="7c57a-135">To copy the URL, select the clipboard icon:</span></span>
   
   ![HDInsight Hadoop Interactive Query LLAP JDBC](./media/apache-interactive-query-get-started/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="next-steps"></a><span data-ttu-id="7c57a-137">Next steps</span><span class="sxs-lookup"><span data-stu-id="7c57a-137">Next steps</span></span>

* <span data-ttu-id="7c57a-138">Learn how to [create Interactive Query clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-138">Learn how to [create Interactive Query clusters in HDInsight](../hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="7c57a-139">Learn how to [visualize big data with Power BI in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-139">Learn how to [visualize big data with Power BI in Azure HDInsight](../hadoop/apache-hadoop-connect-hive-power-bi.md).</span></span>
* <span data-ttu-id="7c57a-140">Learn how to [use Zeppelin to run Hive queries in Azure HDInsight ](../hdinsight-connect-hive-zeppelin.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-140">Learn how to [use Zeppelin to run Hive queries in Azure HDInsight ](../hdinsight-connect-hive-zeppelin.md).</span></span>
* <span data-ttu-id="7c57a-141">Learn how to [run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-hive-queries).</span><span class="sxs-lookup"><span data-stu-id="7c57a-141">Learn how to [run Hive queries using Data Lake Tools for Visual Studio](../hadoop/apache-hadoop-visual-studio-tools-get-started.md#run-interactive-hive-queries).</span></span>
* <span data-ttu-id="7c57a-142">Learn how to [use HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-142">Learn how to [use HDInsight Tools for Visual Studio Code](../hdinsight-for-vscode.md).</span></span>
* <span data-ttu-id="7c57a-143">Learn how to [use Hive View with Hadoop in HDInsight](../hadoop/apache-hadoop-use-hive-ambari-view.md)</span><span class="sxs-lookup"><span data-stu-id="7c57a-143">Learn how to [use Hive View with Hadoop in HDInsight](../hadoop/apache-hadoop-use-hive-ambari-view.md)</span></span>
* <span data-ttu-id="7c57a-144">Learn how to [use Beeline to submit Hive queries in HDInsight](../hadoop/apache-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-144">Learn how to [use Beeline to submit Hive queries in HDInsight](../hadoop/apache-hadoop-use-hive-beeline.md).</span></span>
* <span data-ttu-id="7c57a-145">Learn how to [connect Excel to Hadoop with the Microsoft Hive ODBC driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="7c57a-145">Learn how to [connect Excel to Hadoop with the Microsoft Hive ODBC driver](../hadoop/apache-hadoop-connect-excel-hive-odbc-driver.md).</span></span>

