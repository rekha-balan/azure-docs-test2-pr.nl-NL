---
title: Use Apache Phoenix and SQuirreL with Azure HDInsight (HBase) | Microsoft Docs
description: Learn how to use Apache Phoenix in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.
services: hdinsight
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/06/2017
ms.author: jgao
ms.openlocfilehash: 5d76bd813260e953515dab4eae0d146c1ed77fc8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563895"
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="350ea-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="350ea-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="350ea-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span><span class="sxs-lookup"><span data-stu-id="350ea-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="350ea-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="350ea-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="350ea-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="350ea-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="350ea-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="350ea-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="350ea-108">Use SQLLine</span><span class="sxs-lookup"><span data-stu-id="350ea-108">Use SQLLine</span></span>
<span data-ttu-id="350ea-109">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span><span class="sxs-lookup"><span data-stu-id="350ea-109">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="350ea-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="350ea-110">Prerequisites</span></span>
<span data-ttu-id="350ea-111">Before you can use SQLLine, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="350ea-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="350ea-112">**A HBase cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="350ea-112">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="350ea-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="350ea-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="350ea-114">**Connect to the HBase cluster via the remote desktop protocol**.</span><span class="sxs-lookup"><span data-stu-id="350ea-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="350ea-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="350ea-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="350ea-116">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="350ea-116">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="350ea-117">Each HDInsight cluster has 3 Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="350ea-117">Each HDInsight cluster has 3 Zookeepers.</span></span>

<span data-ttu-id="350ea-118">**To find out the Zookeeper host name**</span><span class="sxs-lookup"><span data-stu-id="350ea-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="350ea-119">Open Ambari by browse to **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="350ea-119">Open Ambari by browse to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="350ea-120">Enter the HTTP (cluster) username and password to login.</span><span class="sxs-lookup"><span data-stu-id="350ea-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="350ea-121">Click **ZooKeeper** from the left menu.</span><span class="sxs-lookup"><span data-stu-id="350ea-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="350ea-122">You shall see 3 **ZooKeeper Server** listed.</span><span class="sxs-lookup"><span data-stu-id="350ea-122">You shall see 3 **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="350ea-123">Click one of the **ZooKeeper Server** listed.</span><span class="sxs-lookup"><span data-stu-id="350ea-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="350ea-124">On the Summary pane, find the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="350ea-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="350ea-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="350ea-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="350ea-126">**To use SQLLine**</span><span class="sxs-lookup"><span data-stu-id="350ea-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="350ea-127">Connect to the cluster using SSH.</span><span class="sxs-lookup"><span data-stu-id="350ea-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="350ea-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="350ea-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="350ea-129">From SSH, run the following commands to run SQLLine:</span><span class="sxs-lookup"><span data-stu-id="350ea-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="350ea-130">Run the following commands to create a HBase table, and insert some data:</span><span class="sxs-lookup"><span data-stu-id="350ea-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="350ea-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="350ea-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="350ea-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="350ea-132">Next steps</span></span>
<span data-ttu-id="350ea-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="350ea-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="350ea-134">To learn more, see</span><span class="sxs-lookup"><span data-stu-id="350ea-134">To learn more, see</span></span>

* <span data-ttu-id="350ea-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span><span class="sxs-lookup"><span data-stu-id="350ea-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="350ea-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span><span class="sxs-lookup"><span data-stu-id="350ea-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="350ea-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="350ea-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="350ea-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="350ea-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png







