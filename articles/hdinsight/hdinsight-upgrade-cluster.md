---
title: Upgrade HDInsight cluster to a newer version -Azure | Microsoft Docs
description: Learn how to Upgrade HDInsight cluster to a newer version.
services: hdinsight
documentationcenter: ''
author: bhanupr
manager: asadk
editor: bhanupr
ms.assetid: 60eb573c-e639-4815-9fc6-ea8b106d8dbc
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/04/2017
ms.author: bhanupr
ms.openlocfilehash: ce4e5d8b3dc1c06258dda9bffa9b018c90904476
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555683"
---
# <a name="upgrade-hdinsight-cluster-to-a-newer-version"></a><span data-ttu-id="0825a-103">Upgrade HDInsight cluster to a newer version</span><span class="sxs-lookup"><span data-stu-id="0825a-103">Upgrade HDInsight cluster to a newer version</span></span>
<span data-ttu-id="0825a-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span><span class="sxs-lookup"><span data-stu-id="0825a-104">To take advantage of the latest HDInsight features, we recommend that HDInsight clusters be upgraded to latest version.</span></span> <span data-ttu-id="0825a-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span><span class="sxs-lookup"><span data-stu-id="0825a-105">Follow the below guidelines to upgrade your HDInsight cluster versions.</span></span>

> [!NOTE]
> <span data-ttu-id="0825a-106">HDInsight clusters version 3.2 and 3.3 are nearing deprecation date.</span><span class="sxs-lookup"><span data-stu-id="0825a-106">HDInsight clusters version 3.2 and 3.3 are nearing deprecation date.</span></span> <span data-ttu-id="0825a-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span><span class="sxs-lookup"><span data-stu-id="0825a-107">For information on supported version of HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md#supported-hdinsight-versions).</span></span>
>
>

## <a name="upgrade-tasks"></a><span data-ttu-id="0825a-108">Upgrade tasks</span><span class="sxs-lookup"><span data-stu-id="0825a-108">Upgrade tasks</span></span>
<span data-ttu-id="0825a-109">The workflow to upgrade HDInsight Cluster is as follows.</span><span class="sxs-lookup"><span data-stu-id="0825a-109">The workflow to upgrade HDInsight Cluster is as follows.</span></span>

![Upgrade workflow diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-upgrade-cluster/upgrade-workflow.png)

1. <span data-ttu-id="0825a-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="0825a-111">Read each section of this document to understand changes that may be required when upgrading your HDInsight cluster.</span></span>
2. <span data-ttu-id="0825a-112">Create a cluster as a test/quality assurance environment.</span><span class="sxs-lookup"><span data-stu-id="0825a-112">Create a cluster as a test/quality assurance environment.</span></span> <span data-ttu-id="0825a-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span><span class="sxs-lookup"><span data-stu-id="0825a-113">For more information on creating a cluster, see [Learn how to create Linux-based HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md)</span></span>
3. <span data-ttu-id="0825a-114">Copy existing jobs, data sources, and sinks to the new environment.</span><span class="sxs-lookup"><span data-stu-id="0825a-114">Copy existing jobs, data sources, and sinks to the new environment.</span></span> <span data-ttu-id="0825a-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span><span class="sxs-lookup"><span data-stu-id="0825a-115">See [Copy Data To Test Environment](hdinsight-migrate-from-windows-to-linux.md#copy-data-to-the-test-environment) for more details.</span></span>
4. <span data-ttu-id="0825a-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span><span class="sxs-lookup"><span data-stu-id="0825a-116">Perform validation testing to make sure that your jobs work as expected on the new cluster.</span></span>


<span data-ttu-id="0825a-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span><span class="sxs-lookup"><span data-stu-id="0825a-117">Once you have verified that everything works as expected, schedule downtime for the migration.</span></span> <span data-ttu-id="0825a-118">During this downtime, do the following actions:</span><span class="sxs-lookup"><span data-stu-id="0825a-118">During this downtime, do the following actions:</span></span>

1.  <span data-ttu-id="0825a-119">Back up any transient data stored locally on the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="0825a-119">Back up any transient data stored locally on the cluster nodes.</span></span> <span data-ttu-id="0825a-120">For example, if you have data stored directly on a head node.</span><span class="sxs-lookup"><span data-stu-id="0825a-120">For example, if you have data stored directly on a head node.</span></span>
2.  <span data-ttu-id="0825a-121">Delete the existing cluster.</span><span class="sxs-lookup"><span data-stu-id="0825a-121">Delete the existing cluster.</span></span>
3.  <span data-ttu-id="0825a-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span><span class="sxs-lookup"><span data-stu-id="0825a-122">Create a cluster in the same VNET subnet with latest (or supported) HDI version using the same default data store that the previous cluster used.</span></span> <span data-ttu-id="0825a-123">This allows the new cluster to continue working against your existing production data.</span><span class="sxs-lookup"><span data-stu-id="0825a-123">This allows the new cluster to continue working against your existing production data.</span></span>
4.  <span data-ttu-id="0825a-124">Import any transient data you backed up.</span><span class="sxs-lookup"><span data-stu-id="0825a-124">Import any transient data you backed up.</span></span>
5.  <span data-ttu-id="0825a-125">Start jobs/continue processing using the new cluster.</span><span class="sxs-lookup"><span data-stu-id="0825a-125">Start jobs/continue processing using the new cluster.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0825a-126">Next Steps</span><span class="sxs-lookup"><span data-stu-id="0825a-126">Next Steps</span></span>
* [<span data-ttu-id="0825a-127">Learn how to create Linux-based HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="0825a-127">Learn how to create Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="0825a-128">Connect to HDInsight using SSH</span><span class="sxs-lookup"><span data-stu-id="0825a-128">Connect to HDInsight using SSH</span></span>](hdinsight-hadoop-linux-use-ssh-unix.md)
* [<span data-ttu-id="0825a-129">Manage a Linux-based cluster using Ambari</span><span class="sxs-lookup"><span data-stu-id="0825a-129">Manage a Linux-based cluster using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)


