---
title: Upgrade HDInsight cluster to a newer version -Azure
description: Learn how to Upgrade HDInsight cluster to a newer version.
services: hdinsight
ms.service: hdinsight
author: omidm1
ms.author: omidm
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 04/04/2017
ms.openlocfilehash: cab2c7aabf23ba8636f46a92c8d864b1c9b74120
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44804081"
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="16234-103">Upgrade HDInsight cluster to a newer version</span><span class="sxs-lookup"><span data-stu-id="16234-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="16234-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span><span class="sxs-lookup"><span data-stu-id="16234-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="16234-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span><span class="sxs-lookup"><span data-stu-id="16234-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="16234-106">For information on supported versions of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="16234-106">For information on supported versions of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="16234-107">Upgrade tasks</span><span class="sxs-lookup"><span data-stu-id="16234-107">Upgrade tasks</span></span>
<span data-ttu-id="16234-108">The workflow to upgrade HDInsight Cluster is as follows.</span><span class="sxs-lookup"><span data-stu-id="16234-108">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Upgrade workflow diagram](./media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="16234-110">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="16234-110">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="16234-111">Create a cluster as a test/quality assurance environment.</span><span class="sxs-lookup"><span data-stu-id="16234-111">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="16234-112">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="16234-112">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="16234-113">Copy existing jobs, data sources, and sinks to the new environment.</span><span class="sxs-lookup"><span data-stu-id="16234-113">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="16234-114">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span><span class="sxs-lookup"><span data-stu-id="16234-114">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="16234-115">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span><span class="sxs-lookup"><span data-stu-id="16234-115">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="16234-116">Once you have verified that everything works as expected, schedule downtime for the migration.</span><span class="sxs-lookup"><span data-stu-id="16234-116">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="16234-117">During this downtime, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="16234-117">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="16234-118">Back up any transient data stored locally on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="16234-118">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="16234-119">For example, if you have data stored directly on a head node.</span><span class="sxs-lookup"><span data-stu-id="16234-119">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="16234-120">Delete the existing cluster.</span><span class="sxs-lookup"><span data-stu-id="16234-120">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="16234-121">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span><span class="sxs-lookup"><span data-stu-id="16234-121">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="16234-122">This allows the new cluster to continue working against your existing production data.</span><span class="sxs-lookup"><span data-stu-id="16234-122">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="16234-123">Import any transient data you backed up.</span><span class="sxs-lookup"><span data-stu-id="16234-123">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="16234-124">Start jobs/continue processing using the new cluster.</span><span class="sxs-lookup"><span data-stu-id="16234-124">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16234-125">Next Steps</span><span class="sxs-lookup"><span data-stu-id="16234-125">Next Steps</span></span>
* [<span data-ttu-id="16234-126">Learn how to create Linux-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="16234-126">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="16234-127">Connect to HDInsight using SSH</span><span class="sxs-lookup"><span data-stu-id="16234-127">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="16234-128">Manage a Linux-based cluster using Ambari</span><span class="sxs-lookup"><span data-stu-id="16234-128">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

