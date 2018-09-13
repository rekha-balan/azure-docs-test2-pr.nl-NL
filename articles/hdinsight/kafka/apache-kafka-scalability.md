---
title: Apache Kafka increase scale - Azure HDInsight
description: Learn how to configure managed disks for Apache Kafka cluster on Azure HDInsight to increase scalability.
services: hdinsight
ms.service: hdinsight
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/30/2018
ms.openlocfilehash: f74bc5732bbcf05423698603113998204b7514a9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967631"
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a><span data-ttu-id="86a0d-103">Configure storage and scalability for Apache Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="86a0d-103">Configure storage and scalability for Apache Kafka on HDInsight</span></span>

<span data-ttu-id="86a0d-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86a0d-104">Learn how to configure the number of managed disks used by Apache Kafka on HDInsight.</span></span>

<span data-ttu-id="86a0d-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="86a0d-105">Kafka on HDInsight uses the local disk of the virtual machines in the HDInsight cluster.</span></span> <span data-ttu-id="86a0d-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span><span class="sxs-lookup"><span data-stu-id="86a0d-106">Since Kafka is very I/O heavy, [Azure Managed Disks](../../virtual-machines/windows/managed-disks-overview.md) is used to provide high throughput and provide more storage per node.</span></span> <span data-ttu-id="86a0d-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span><span class="sxs-lookup"><span data-stu-id="86a0d-107">If traditional virtual hard drives (VHD) were used for Kafka, each node is limited to 1 TB.</span></span> <span data-ttu-id="86a0d-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span><span class="sxs-lookup"><span data-stu-id="86a0d-108">With managed disks, you can use multiple disks to achieve 16 TB for each node in the cluster.</span></span>

<span data-ttu-id="86a0d-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span><span class="sxs-lookup"><span data-stu-id="86a0d-109">The following diagram provides a comparison between Kafka on HDInsight before managed disks, and Kafka on HDInsight with managed disks:</span></span>

![Diagram showing Kafka on HDInsight using a single vhd per vm vs. multiple managed disks per vm](./media/apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a><span data-ttu-id="86a0d-111">Configure managed disks: Azure portal</span><span class="sxs-lookup"><span data-stu-id="86a0d-111">Configure managed disks: Azure portal</span></span>

1. <span data-ttu-id="86a0d-112">Follow the steps in the [Create an HDInsight cluster](../hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span><span class="sxs-lookup"><span data-stu-id="86a0d-112">Follow the steps in the [Create an HDInsight cluster](../hdinsight-hadoop-create-linux-clusters-portal.md) to understand the common steps to create a cluster using the portal.</span></span> <span data-ttu-id="86a0d-113">Do not complete the portal creation process.</span><span class="sxs-lookup"><span data-stu-id="86a0d-113">Do not complete the portal creation process.</span></span>

2. <span data-ttu-id="86a0d-114">From the __Cluster size__ section, use the __Disks per worker node__ field to configure the number of disks.</span><span class="sxs-lookup"><span data-stu-id="86a0d-114">From the __Cluster size__ section, use the __Disks per worker node__ field to configure the number of disks.</span></span>

    > [!NOTE]
    > <span data-ttu-id="86a0d-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span><span class="sxs-lookup"><span data-stu-id="86a0d-115">The type of managed disk can be either __Standard__ (HDD) or __Premium__ (SSD).</span></span> <span data-ttu-id="86a0d-116">Premium disks are used with DS and GS series VMs.</span><span class="sxs-lookup"><span data-stu-id="86a0d-116">Premium disks are used with DS and GS series VMs.</span></span> <span data-ttu-id="86a0d-117">All other VM types use standard.</span><span class="sxs-lookup"><span data-stu-id="86a0d-117">All other VM types use standard.</span></span>

    ![Image of the cluster size section with the disks per worker node highlighted](./media/apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a><span data-ttu-id="86a0d-119">Configure managed disks: Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="86a0d-119">Configure managed disks: Resource Manager template</span></span>

<span data-ttu-id="86a0d-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span><span class="sxs-lookup"><span data-stu-id="86a0d-120">To control the number of disks used by the worker nodes in a Kafka cluster, use the following section of the template:</span></span>

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

<span data-ttu-id="86a0d-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span><span class="sxs-lookup"><span data-stu-id="86a0d-121">You can find a complete template that demonstrates how to configure managed disks at [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).</span></span>

## <a name="next-steps"></a><span data-ttu-id="86a0d-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="86a0d-122">Next steps</span></span>

<span data-ttu-id="86a0d-123">For more information on working with Kafka on HDInsight, see the following documents:</span><span class="sxs-lookup"><span data-stu-id="86a0d-123">For more information on working with Kafka on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="86a0d-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="86a0d-124">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](apache-kafka-mirroring.md)
* [<span data-ttu-id="86a0d-125">Use Apache Storm with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="86a0d-125">Use Apache Storm with Kafka on HDInsight</span></span>](../hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="86a0d-126">Use Apache Spark with Kafka on HDInsight</span><span class="sxs-lookup"><span data-stu-id="86a0d-126">Use Apache Spark with Kafka on HDInsight</span></span>](../hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="86a0d-127">Connect to Kafka through an Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="86a0d-127">Connect to Kafka through an Azure Virtual Network</span></span>](apache-kafka-connect-vpn-gateway.md)

* [<span data-ttu-id="86a0d-128">HDInsight blog on managed disks with Kafka</span><span class="sxs-lookup"><span data-stu-id="86a0d-128">HDInsight blog on managed disks with Kafka</span></span>](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)
