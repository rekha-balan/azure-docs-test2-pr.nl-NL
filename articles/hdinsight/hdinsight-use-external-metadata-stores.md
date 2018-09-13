---
title: Use external metadata stores - Azure HDInsight
description: Use external metadata stores with HDInsight clusters.
services: hdinsight
author: jasonwhowell
ms.reviewer: jasonh
ms.author: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 05/14/2018
ms.openlocfilehash: a2c992a47e40a4f8764f5950c65bb90f1cd9e066
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870333"
---
# <a name="use-external-metadata-stores-in-azure-hdinsight"></a><span data-ttu-id="aed8e-103">Use external metadata stores in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aed8e-103">Use external metadata stores in Azure HDInsight</span></span>

<span data-ttu-id="aed8e-104">The Hive metastore in HDInsight is an essential part of Hadoop architecture.</span><span class="sxs-lookup"><span data-stu-id="aed8e-104">The Hive metastore in HDInsight is an essential part of Hadoop architecture.</span></span> <span data-ttu-id="aed8e-105">A metastore is the central schema repository that can be used by other big data access tools such as Spark, Interactive Query (LLAP), Presto, or Pig.</span><span class="sxs-lookup"><span data-stu-id="aed8e-105">A metastore is the central schema repository that can be used by other big data access tools such as Spark, Interactive Query (LLAP), Presto, or Pig.</span></span> <span data-ttu-id="aed8e-106">HDInsight uses an Azure SQL Database as the Hive metastore.</span><span class="sxs-lookup"><span data-stu-id="aed8e-106">HDInsight uses an Azure SQL Database as the Hive metastore.</span></span>

![HDInsight Hive Metadata Store Architecture](./media/hdinsight-use-external-metadata-stores/metadata-store-architecture.png)

<span data-ttu-id="aed8e-108">There are two ways you can set up a metastore for your HDInsight clusters:</span><span class="sxs-lookup"><span data-stu-id="aed8e-108">There are two ways you can set up a metastore for your HDInsight clusters:</span></span>

* [<span data-ttu-id="aed8e-109">Default metastore</span><span class="sxs-lookup"><span data-stu-id="aed8e-109">Default metastore</span></span>](#default-metastore)
* [<span data-ttu-id="aed8e-110">Custom metastore</span><span class="sxs-lookup"><span data-stu-id="aed8e-110">Custom metastore</span></span>](#custom-metastore)

## <a name="default-metastore"></a><span data-ttu-id="aed8e-111">Default metastore</span><span class="sxs-lookup"><span data-stu-id="aed8e-111">Default metastore</span></span>

<span data-ttu-id="aed8e-112">By default, HDInsight provisions a metastore with every cluster type.</span><span class="sxs-lookup"><span data-stu-id="aed8e-112">By default, HDInsight provisions a metastore with every cluster type.</span></span> <span data-ttu-id="aed8e-113">You can instead specify a custom metastore.</span><span class="sxs-lookup"><span data-stu-id="aed8e-113">You can instead specify a custom metastore.</span></span> <span data-ttu-id="aed8e-114">The default metastore includes the following considerations:</span><span class="sxs-lookup"><span data-stu-id="aed8e-114">The default metastore includes the following considerations:</span></span>
- <span data-ttu-id="aed8e-115">No additional cost.</span><span class="sxs-lookup"><span data-stu-id="aed8e-115">No additional cost.</span></span> <span data-ttu-id="aed8e-116">HDInsight provisions a metastore with every cluster type without any additional cost to you.</span><span class="sxs-lookup"><span data-stu-id="aed8e-116">HDInsight provisions a metastore with every cluster type without any additional cost to you.</span></span>
- <span data-ttu-id="aed8e-117">Each default metastore is part of the cluster lifecycle.</span><span class="sxs-lookup"><span data-stu-id="aed8e-117">Each default metastore is part of the cluster lifecycle.</span></span> <span data-ttu-id="aed8e-118">When you delete a cluster that metastore and metadata are also deleted.</span><span class="sxs-lookup"><span data-stu-id="aed8e-118">When you delete a cluster that metastore and metadata are also deleted.</span></span>
- <span data-ttu-id="aed8e-119">You cannot share the default metastore with other clusters.</span><span class="sxs-lookup"><span data-stu-id="aed8e-119">You cannot share the default metastore with other clusters.</span></span>
- <span data-ttu-id="aed8e-120">The default metastore uses the basic Azure SQL DB, which has a 5 DTU (database transaction unit) limit.</span><span class="sxs-lookup"><span data-stu-id="aed8e-120">The default metastore uses the basic Azure SQL DB, which has a 5 DTU (database transaction unit) limit.</span></span>
<span data-ttu-id="aed8e-121">This default metastore is typically used for relatively simple workloads that don't require multiple clusters and don’t need metadata preserved beyond the cluster's lifecycle.</span><span class="sxs-lookup"><span data-stu-id="aed8e-121">This default metastore is typically used for relatively simple workloads that don't require multiple clusters and don’t need metadata preserved beyond the cluster's lifecycle.</span></span>


## <a name="custom-metastore"></a><span data-ttu-id="aed8e-122">Custom metastore</span><span class="sxs-lookup"><span data-stu-id="aed8e-122">Custom metastore</span></span>

<span data-ttu-id="aed8e-123">HDInsight also supports custom metastores, which are recommended for production clusters:</span><span class="sxs-lookup"><span data-stu-id="aed8e-123">HDInsight also supports custom metastores, which are recommended for production clusters:</span></span>
- <span data-ttu-id="aed8e-124">You specify your own Azure SQL Database as the metastore.</span><span class="sxs-lookup"><span data-stu-id="aed8e-124">You specify your own Azure SQL Database as the metastore.</span></span>
- <span data-ttu-id="aed8e-125">The lifecycle of the metastore is not tied to a clusters lifecycle, so you can create and delete clusters without losing metadata.</span><span class="sxs-lookup"><span data-stu-id="aed8e-125">The lifecycle of the metastore is not tied to a clusters lifecycle, so you can create and delete clusters without losing metadata.</span></span> <span data-ttu-id="aed8e-126">Metadata such as your Hive schemas will persist even after you delete and re-create the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="aed8e-126">Metadata such as your Hive schemas will persist even after you delete and re-create the HDInsight cluster.</span></span>
- <span data-ttu-id="aed8e-127">A custom metastore lets you attach multiple clusters and cluster types to that metastore.</span><span class="sxs-lookup"><span data-stu-id="aed8e-127">A custom metastore lets you attach multiple clusters and cluster types to that metastore.</span></span> <span data-ttu-id="aed8e-128">For example, a single metastore can be shared across Interactive Query, Hive, and Spark clusters in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aed8e-128">For example, a single metastore can be shared across Interactive Query, Hive, and Spark clusters in HDInsight.</span></span>
- <span data-ttu-id="aed8e-129">You pay for the cost of a metastore (Azure SQL DB) according to the performance level you choose.</span><span class="sxs-lookup"><span data-stu-id="aed8e-129">You pay for the cost of a metastore (Azure SQL DB) according to the performance level you choose.</span></span>
- <span data-ttu-id="aed8e-130">You can scale up the metastore as needed.</span><span class="sxs-lookup"><span data-stu-id="aed8e-130">You can scale up the metastore as needed.</span></span>


![HDInsight Hive Metadata Store Use Case](./media/hdinsight-use-external-metadata-stores/metadata-store-use-case.png)

<!-- Image – Typical shared custom Metastore scenario in HDInsight (?) -->



### <a name="select-a-custom-metastore-during-cluster-creation"></a><span data-ttu-id="aed8e-132">Select a custom metastore during cluster creation</span><span class="sxs-lookup"><span data-stu-id="aed8e-132">Select a custom metastore during cluster creation</span></span>

<span data-ttu-id="aed8e-133">You can point your cluster to a previously created Azure SQL Database during cluster creation, or you can configure the SQL Database after the cluster is created.</span><span class="sxs-lookup"><span data-stu-id="aed8e-133">You can point your cluster to a previously created Azure SQL Database during cluster creation, or you can configure the SQL Database after the cluster is created.</span></span> <span data-ttu-id="aed8e-134">This option is specified with the Storage > Metastore settings while creating a new Hadoop, Spark, or interactive Hive cluster from Azure portal.</span><span class="sxs-lookup"><span data-stu-id="aed8e-134">This option is specified with the Storage > Metastore settings while creating a new Hadoop, Spark, or interactive Hive cluster from Azure portal.</span></span>

![HDInsight Hive Metadata Store Azure portal](./media/hdinsight-use-external-metadata-stores/metadata-store-azure-portal.png)

<span data-ttu-id="aed8e-136">You can also add additional clusters to a custom metastore from Azure portal or from Ambari configurations (Hive > Advanced)</span><span class="sxs-lookup"><span data-stu-id="aed8e-136">You can also add additional clusters to a custom metastore from Azure portal or from Ambari configurations (Hive > Advanced)</span></span>

![HDInsight Hive Metadata Store Ambari](./media/hdinsight-use-external-metadata-stores/metadata-store-ambari.png)

## <a name="hive-metastore-best-practices"></a><span data-ttu-id="aed8e-138">Hive metastore best practices</span><span class="sxs-lookup"><span data-stu-id="aed8e-138">Hive metastore best practices</span></span>

<span data-ttu-id="aed8e-139">Here are some general HDInsight Hive metastore best practices:</span><span class="sxs-lookup"><span data-stu-id="aed8e-139">Here are some general HDInsight Hive metastore best practices:</span></span>

- <span data-ttu-id="aed8e-140">Use a custom metastore whenever possible, as this will help separate compute resources (your running cluster) and metadata (stored in the metastore).</span><span class="sxs-lookup"><span data-stu-id="aed8e-140">Use a custom metastore whenever possible, as this will help separate compute resources (your running cluster) and metadata (stored in the metastore).</span></span>
- <span data-ttu-id="aed8e-141">Start with an S2 tier, which provides  50 DTU and 250 GB of storage.</span><span class="sxs-lookup"><span data-stu-id="aed8e-141">Start with an S2 tier, which provides  50 DTU and 250 GB of storage.</span></span> <span data-ttu-id="aed8e-142">If you see a bottleneck, you can scale the database up.</span><span class="sxs-lookup"><span data-stu-id="aed8e-142">If you see a bottleneck, you can scale the database up.</span></span>
- <span data-ttu-id="aed8e-143">Ensure that the metastore created for one HDInsight cluster version is not shared across different HDInsight cluster versions.</span><span class="sxs-lookup"><span data-stu-id="aed8e-143">Ensure that the metastore created for one HDInsight cluster version is not shared across different HDInsight cluster versions.</span></span> <span data-ttu-id="aed8e-144">Different Hive versions use different schemas.</span><span class="sxs-lookup"><span data-stu-id="aed8e-144">Different Hive versions use different schemas.</span></span> <span data-ttu-id="aed8e-145">For example, you cannot share a metastore with both Hive 1.2 and Hive 2.1 clusters.</span><span class="sxs-lookup"><span data-stu-id="aed8e-145">For example, you cannot share a metastore with both Hive 1.2 and Hive 2.1 clusters.</span></span>
- <span data-ttu-id="aed8e-146">Back up your custom metastore periodically.</span><span class="sxs-lookup"><span data-stu-id="aed8e-146">Back up your custom metastore periodically.</span></span>
- <span data-ttu-id="aed8e-147">Keep your metastore and HDInsight cluster in the same region.</span><span class="sxs-lookup"><span data-stu-id="aed8e-147">Keep your metastore and HDInsight cluster in the same region.</span></span>
- <span data-ttu-id="aed8e-148">Monitor your metastore for performance and availability using Azure SQL Database Monitoring tools, such as the Azure portal or Azure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="aed8e-148">Monitor your metastore for performance and availability using Azure SQL Database Monitoring tools, such as the Azure portal or Azure Log Analytics.</span></span>

## <a name="oozie-metastore"></a><span data-ttu-id="aed8e-149">Oozie Metastore</span><span class="sxs-lookup"><span data-stu-id="aed8e-149">Oozie Metastore</span></span>

<span data-ttu-id="aed8e-150">Apache Oozie is a workflow coordination system that manages Hadoop jobs.</span><span class="sxs-lookup"><span data-stu-id="aed8e-150">Apache Oozie is a workflow coordination system that manages Hadoop jobs.</span></span>  <span data-ttu-id="aed8e-151">Oozie supports Hadoop jobs for Apache MapReduce, Pig, Hive, and others.</span><span class="sxs-lookup"><span data-stu-id="aed8e-151">Oozie supports Hadoop jobs for Apache MapReduce, Pig, Hive, and others.</span></span>  <span data-ttu-id="aed8e-152">Oozie uses a metastore to store details about current and completed workflows.</span><span class="sxs-lookup"><span data-stu-id="aed8e-152">Oozie uses a metastore to store details about current and completed workflows.</span></span> <span data-ttu-id="aed8e-153">To increase performance when using Oozie, you can use Azure SQL Database as a custom metastore.</span><span class="sxs-lookup"><span data-stu-id="aed8e-153">To increase performance when using Oozie, you can use Azure SQL Database as a custom metastore.</span></span> <span data-ttu-id="aed8e-154">The metastore can also provide access to Oozie job data after you delete your cluster.</span><span class="sxs-lookup"><span data-stu-id="aed8e-154">The metastore can also provide access to Oozie job data after you delete your cluster.</span></span>

<span data-ttu-id="aed8e-155">For instructions on creating an Oozie metastore with Azure SQL Database, see [Use Oozie for workflows](hdinsight-use-oozie-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="aed8e-155">For instructions on creating an Oozie metastore with Azure SQL Database, see [Use Oozie for workflows](hdinsight-use-oozie-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aed8e-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="aed8e-156">Next steps</span></span>

- [<span data-ttu-id="aed8e-157">Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more</span><span class="sxs-lookup"><span data-stu-id="aed8e-157">Set up clusters in HDInsight with Hadoop, Spark, Kafka, and more</span></span>](./hdinsight-hadoop-provision-linux-clusters.md)
