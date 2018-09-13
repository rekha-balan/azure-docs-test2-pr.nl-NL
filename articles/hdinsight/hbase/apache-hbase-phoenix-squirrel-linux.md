---
title: Use Apache Phoenix and SQLLine with HBase in Azure HDInsight
description: Learn how to use Apache Phoenix in HDInsight. Also, learn how to install and set up SQLLine on your computer to connect to an HBase cluster in HDInsight.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/03/2018
ms.author: jasonh
ms.openlocfilehash: e8fec6a327bcf68303af90b55978d105b19d4fd6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870798"
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="72b33-104">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="72b33-104">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="72b33-105">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in Azure HDInsight, and how to use SQLLine.</span><span class="sxs-lookup"><span data-stu-id="72b33-105">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in Azure HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="72b33-106">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="72b33-106">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="72b33-107">For the Phoenix grammar, see [Phoenix grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="72b33-107">For the Phoenix grammar, see [Phoenix grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="72b33-108">For Phoenix version information about HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight](../hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="72b33-108">For Phoenix version information about HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight](../hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="72b33-109">Use SQLLine</span><span class="sxs-lookup"><span data-stu-id="72b33-109">Use SQLLine</span></span>
<span data-ttu-id="72b33-110">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span><span class="sxs-lookup"><span data-stu-id="72b33-110">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="72b33-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="72b33-111">Prerequisites</span></span>
<span data-ttu-id="72b33-112">Before you can use SQLLine, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="72b33-112">Before you can use SQLLine, you must have the following items:</span></span>

* <span data-ttu-id="72b33-113">**An HBase cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="72b33-113">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="72b33-114">To create one, see [Get started with Apache HBase in HDInsight](./apache-hbase-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="72b33-114">To create one, see [Get started with Apache HBase in HDInsight](./apache-hbase-tutorial-get-started-linux.md).</span></span>

<span data-ttu-id="72b33-115">When you connect to an HBase cluster, you need to connect to one of the ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="72b33-115">When you connect to an HBase cluster, you need to connect to one of the ZooKeeper VMs.</span></span> <span data-ttu-id="72b33-116">Each HDInsight cluster has three ZooKeeper VMs.</span><span class="sxs-lookup"><span data-stu-id="72b33-116">Each HDInsight cluster has three ZooKeeper VMs.</span></span>

<span data-ttu-id="72b33-117">**To get the ZooKeeper host name**</span><span class="sxs-lookup"><span data-stu-id="72b33-117">**To get the ZooKeeper host name**</span></span>

1. <span data-ttu-id="72b33-118">Open Ambari by browsing to **https://\<cluster name\>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="72b33-118">Open Ambari by browsing to **https://\<cluster name\>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="72b33-119">To sign in, enter the HTTP (cluster) user name and password.</span><span class="sxs-lookup"><span data-stu-id="72b33-119">To sign in, enter the HTTP (cluster) user name and password.</span></span>
3. <span data-ttu-id="72b33-120">In the left menu, select **ZooKeeper**.</span><span class="sxs-lookup"><span data-stu-id="72b33-120">In the left menu, select **ZooKeeper**.</span></span> <span data-ttu-id="72b33-121">Three **ZooKeeper Server** instances are listed.</span><span class="sxs-lookup"><span data-stu-id="72b33-121">Three **ZooKeeper Server** instances are listed.</span></span>
4. <span data-ttu-id="72b33-122">Select one of the **ZooKeeper Server** instances.</span><span class="sxs-lookup"><span data-stu-id="72b33-122">Select one of the **ZooKeeper Server** instances.</span></span> <span data-ttu-id="72b33-123">On the **Summary** pane, find the **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="72b33-123">On the **Summary** pane, find the **Hostname**.</span></span> <span data-ttu-id="72b33-124">It looks similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="72b33-124">It looks similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="72b33-125">**To use SQLLine**</span><span class="sxs-lookup"><span data-stu-id="72b33-125">**To use SQLLine**</span></span>

1. <span data-ttu-id="72b33-126">Connect to the cluster by using SSH.</span><span class="sxs-lookup"><span data-stu-id="72b33-126">Connect to the cluster by using SSH.</span></span> <span data-ttu-id="72b33-127">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="72b33-127">For more information, see [Use SSH with HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="72b33-128">In SSH, use the following commands to run SQLLine:</span><span class="sxs-lookup"><span data-stu-id="72b33-128">In SSH, use the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ZOOKEEPER SERVER FQDN>:2181:/hbase-unsecure
3. <span data-ttu-id="72b33-129">To create an HBase table, and insert some data, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="72b33-129">To create an HBase table, and insert some data, run the following commands:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="72b33-130">For more information, see the [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix grammar](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="72b33-130">For more information, see the [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="72b33-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="72b33-131">Next steps</span></span>
<span data-ttu-id="72b33-132">In this article, you learned how to use Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="72b33-132">In this article, you learned how to use Apache Phoenix in HDInsight.</span></span> <span data-ttu-id="72b33-133">To learn more, see these articles:</span><span class="sxs-lookup"><span data-stu-id="72b33-133">To learn more, see these articles:</span></span>

* <span data-ttu-id="72b33-134">[HDInsight HBase overview][hdinsight-hbase-overview].</span><span class="sxs-lookup"><span data-stu-id="72b33-134">[HDInsight HBase overview][hdinsight-hbase-overview].</span></span>
  <span data-ttu-id="72b33-135">HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span><span class="sxs-lookup"><span data-stu-id="72b33-135">HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="72b33-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="72b33-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>
  <span data-ttu-id="72b33-137">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications, so applications can communicate directly with HBase.</span><span class="sxs-lookup"><span data-stu-id="72b33-137">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications, so applications can communicate directly with HBase.</span></span>
* <span data-ttu-id="72b33-138">[Configure HBase replication in HDInsight](apache-hbase-replication.md).</span><span class="sxs-lookup"><span data-stu-id="72b33-138">[Configure HBase replication in HDInsight](apache-hbase-replication.md).</span></span> <span data-ttu-id="72b33-139">Learn how to set up HBase replication across two Azure datacenters.</span><span class="sxs-lookup"><span data-stu-id="72b33-139">Learn how to set up HBase replication across two Azure datacenters.</span></span>


[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]:apache-hbase-provision-vnet.md
[hdinsight-hbase-overview]:apache-hbase-overview.md


