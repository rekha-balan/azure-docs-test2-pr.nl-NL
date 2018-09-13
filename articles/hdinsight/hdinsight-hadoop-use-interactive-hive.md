---
title: Use Interactive Hive in HDInsight | Microsoft Docs
description: Learn how to use Interactive Hive (Hive on LLAP) in HDInsight.
keywords: ''
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: c33b02e1d72f8bae60bb5bfe2bf098b85d7522f3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564517"
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="1410c-103">Use Interactive Hive in HDInsight (Preview)</span><span class="sxs-lookup"><span data-stu-id="1410c-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="1410c-104">Interactive Hive (A.K.A.</span><span class="sxs-lookup"><span data-stu-id="1410c-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="1410c-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="1410c-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="1410c-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span><span class="sxs-lookup"><span data-stu-id="1410c-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="1410c-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solution on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span><span class="sxs-lookup"><span data-stu-id="1410c-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solution on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="1410c-108">The Interactive Hive cluster is different from the Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="1410c-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="1410c-109">It only contains the Hive service.</span><span class="sxs-lookup"><span data-stu-id="1410c-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="1410c-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span><span class="sxs-lookup"><span data-stu-id="1410c-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="1410c-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="1410c-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="1410c-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1410c-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="1410c-113">Create an Interactive Hive cluster</span><span class="sxs-lookup"><span data-stu-id="1410c-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="1410c-114">Interactive Hive cluster is only supported on Linux-based clusters.</span><span class="sxs-lookup"><span data-stu-id="1410c-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="1410c-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="1410c-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="1410c-116">Execute Hive from Interactive Hive</span><span class="sxs-lookup"><span data-stu-id="1410c-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="1410c-117">There are different options how you can execute Hive queries:</span><span class="sxs-lookup"><span data-stu-id="1410c-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="1410c-118">Run Hive using the Ambari Hive view</span><span class="sxs-lookup"><span data-stu-id="1410c-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="1410c-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="1410c-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="1410c-120">Run Hive using Beeline</span><span class="sxs-lookup"><span data-stu-id="1410c-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="1410c-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="1410c-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="1410c-122">You use Beeline from either the headnode or an empty edge node.</span><span class="sxs-lookup"><span data-stu-id="1410c-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="1410c-123">Using Beeline from an empty edge node is recommended.</span><span class="sxs-lookup"><span data-stu-id="1410c-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="1410c-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="1410c-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="1410c-125">Run Hive using Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="1410c-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="1410c-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="1410c-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="1410c-127">**To find the JDBC connection string:**</span><span class="sxs-lookup"><span data-stu-id="1410c-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="1410c-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="1410c-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="1410c-129">Click **Hive** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="1410c-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="1410c-130">Click the highlighted icon to copy the URL:</span><span class="sxs-lookup"><span data-stu-id="1410c-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![HDInsight Hadoop Interactive Hive LLAP JDBC](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="1410c-132">See also</span><span class="sxs-lookup"><span data-stu-id="1410c-132">See also</span></span>
* <span data-ttu-id="1410c-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1410c-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="1410c-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span><span class="sxs-lookup"><span data-stu-id="1410c-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="1410c-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span><span class="sxs-lookup"><span data-stu-id="1410c-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>


