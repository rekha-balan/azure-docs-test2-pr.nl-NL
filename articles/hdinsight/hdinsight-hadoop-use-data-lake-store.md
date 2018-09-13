---
title: Use Data Lake Store with Hadoop in Azure HDInsight
description: Learn how to query data from Azure Data Lake Store and to store results of your analysis.
services: hdinsight,storage
author: jasonwhowell
ms.author: jasonh
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.topic: conceptual
ms.date: 07/23/2018
ms.openlocfilehash: 1f2863ac13a6b94a226cdc01a57f6554f75625ae
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866598"
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="05a1d-103">Use Data Lake Store with Azure HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="05a1d-103">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="05a1d-104">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span><span class="sxs-lookup"><span data-stu-id="05a1d-104">To analyze data in HDInsight cluster, you can store the data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="05a1d-105">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span><span class="sxs-lookup"><span data-stu-id="05a1d-105">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="05a1d-106">In this article, you learn how Data Lake Store works with HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="05a1d-106">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="05a1d-107">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="05a1d-107">To learn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="05a1d-108">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="05a1d-108">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="05a1d-109">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span><span class="sxs-lookup"><span data-stu-id="05a1d-109">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="05a1d-110">You always use `adl`.</span><span class="sxs-lookup"><span data-stu-id="05a1d-110">You always use `adl`.</span></span>
> 


## <a name="availability-for-hdinsight-clusters"></a><span data-ttu-id="05a1d-111">Availability for HDInsight clusters</span><span class="sxs-lookup"><span data-stu-id="05a1d-111">Availability for HDInsight clusters</span></span>

<span data-ttu-id="05a1d-112">Hadoop supports a notion of the default file system.</span><span class="sxs-lookup"><span data-stu-id="05a1d-112">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="05a1d-113">The default file system implies a default scheme and authority.</span><span class="sxs-lookup"><span data-stu-id="05a1d-113">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="05a1d-114">It can also be used to resolve relative paths.</span><span class="sxs-lookup"><span data-stu-id="05a1d-114">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="05a1d-115">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span><span class="sxs-lookup"><span data-stu-id="05a1d-115">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> 

<span data-ttu-id="05a1d-116">HDInsight clusters can use Data Lake Store in two ways:</span><span class="sxs-lookup"><span data-stu-id="05a1d-116">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="05a1d-117">As the default storage</span><span class="sxs-lookup"><span data-stu-id="05a1d-117">As the default storage</span></span>
* <span data-ttu-id="05a1d-118">As additional storage, with Azure Storage Blob as default storage.</span><span class="sxs-lookup"><span data-stu-id="05a1d-118">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="05a1d-119">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span><span class="sxs-lookup"><span data-stu-id="05a1d-119">As of now, only some of the HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="05a1d-120">HDInsight cluster type</span><span class="sxs-lookup"><span data-stu-id="05a1d-120">HDInsight cluster type</span></span> | <span data-ttu-id="05a1d-121">Data Lake Store as default storage</span><span class="sxs-lookup"><span data-stu-id="05a1d-121">Data Lake Store as default storage</span></span> | <span data-ttu-id="05a1d-122">Data Lake Store as additional storage</span><span class="sxs-lookup"><span data-stu-id="05a1d-122">Data Lake Store as additional storage</span></span>| <span data-ttu-id="05a1d-123">Notes</span><span class="sxs-lookup"><span data-stu-id="05a1d-123">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="05a1d-124">HDInsight version 3.6</span><span class="sxs-lookup"><span data-stu-id="05a1d-124">HDInsight version 3.6</span></span> | <span data-ttu-id="05a1d-125">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-125">Yes</span></span> | <span data-ttu-id="05a1d-126">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-126">Yes</span></span> | |
| <span data-ttu-id="05a1d-127">HDInsight version 3.5</span><span class="sxs-lookup"><span data-stu-id="05a1d-127">HDInsight version 3.5</span></span> | <span data-ttu-id="05a1d-128">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-128">Yes</span></span> | <span data-ttu-id="05a1d-129">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-129">Yes</span></span> | <span data-ttu-id="05a1d-130">With the exception of HBase</span><span class="sxs-lookup"><span data-stu-id="05a1d-130">With the exception of HBase</span></span>|
| <span data-ttu-id="05a1d-131">HDInsight version 3.4</span><span class="sxs-lookup"><span data-stu-id="05a1d-131">HDInsight version 3.4</span></span> | <span data-ttu-id="05a1d-132">No</span><span class="sxs-lookup"><span data-stu-id="05a1d-132">No</span></span> | <span data-ttu-id="05a1d-133">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-133">Yes</span></span> | |
| <span data-ttu-id="05a1d-134">HDInsight version 3.3</span><span class="sxs-lookup"><span data-stu-id="05a1d-134">HDInsight version 3.3</span></span> | <span data-ttu-id="05a1d-135">No</span><span class="sxs-lookup"><span data-stu-id="05a1d-135">No</span></span> | <span data-ttu-id="05a1d-136">No</span><span class="sxs-lookup"><span data-stu-id="05a1d-136">No</span></span> | |
| <span data-ttu-id="05a1d-137">HDInsight version 3.2</span><span class="sxs-lookup"><span data-stu-id="05a1d-137">HDInsight version 3.2</span></span> | <span data-ttu-id="05a1d-138">No</span><span class="sxs-lookup"><span data-stu-id="05a1d-138">No</span></span> | <span data-ttu-id="05a1d-139">Yes</span><span class="sxs-lookup"><span data-stu-id="05a1d-139">Yes</span></span> | |
| <span data-ttu-id="05a1d-140">Storm</span><span class="sxs-lookup"><span data-stu-id="05a1d-140">Storm</span></span> | | |<span data-ttu-id="05a1d-141">You can use Data Lake Store to write data from a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="05a1d-141">You can use Data Lake Store to write data from a Storm topology.</span></span> <span data-ttu-id="05a1d-142">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span><span class="sxs-lookup"><span data-stu-id="05a1d-142">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="05a1d-143">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span><span class="sxs-lookup"><span data-stu-id="05a1d-143">Using Data Lake Store as an additional storage account does not affect performance or the ability to read or write to Azure storage from the cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="05a1d-144">Use Data Lake Store as default storage</span><span class="sxs-lookup"><span data-stu-id="05a1d-144">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="05a1d-145">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span><span class="sxs-lookup"><span data-stu-id="05a1d-145">When HDInsight is deployed with Data Lake Store as default storage, the cluster-related files are stored in Data Lake Store in the following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="05a1d-146">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="05a1d-146">where `<cluster_root_path>` is the name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="05a1d-147">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span><span class="sxs-lookup"><span data-stu-id="05a1d-147">By specifying a root path for each cluster, you can use the same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="05a1d-148">So, you can have a setup where:</span><span class="sxs-lookup"><span data-stu-id="05a1d-148">So, you can have a setup where:</span></span>

* <span data-ttu-id="05a1d-149">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="05a1d-149">Cluster1 can use the path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="05a1d-150">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="05a1d-150">Cluster2 can use the path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="05a1d-151">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="05a1d-151">Notice that both the clusters use the same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="05a1d-152">Each cluster has access to its own root filesystem in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="05a1d-152">Each cluster has access to its own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="05a1d-153">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span><span class="sxs-lookup"><span data-stu-id="05a1d-153">The Azure portal deployment experience in particular prompts you to use a folder name such as **/clusters/\<clustername>** for the root path.</span></span>

<span data-ttu-id="05a1d-154">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span><span class="sxs-lookup"><span data-stu-id="05a1d-154">To be able to use a Data Lake Store as default storage, you must grant the service principal access to the following paths:</span></span>

- <span data-ttu-id="05a1d-155">The Data Lake Store account root.</span><span class="sxs-lookup"><span data-stu-id="05a1d-155">The Data Lake Store account root.</span></span>  <span data-ttu-id="05a1d-156">For example: adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="05a1d-156">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="05a1d-157">The folder for all cluster folders.</span><span class="sxs-lookup"><span data-stu-id="05a1d-157">The folder for all cluster folders.</span></span>  <span data-ttu-id="05a1d-158">For example: adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="05a1d-158">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="05a1d-159">The folder for the cluster.</span><span class="sxs-lookup"><span data-stu-id="05a1d-159">The folder for the cluster.</span></span>  <span data-ttu-id="05a1d-160">For example: adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="05a1d-160">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="05a1d-161">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="05a1d-161">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="05a1d-162">Use Data Lake Store as additional storage</span><span class="sxs-lookup"><span data-stu-id="05a1d-162">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="05a1d-163">You can use Data Lake Store as additional storage for the cluster as well.</span><span class="sxs-lookup"><span data-stu-id="05a1d-163">You can use Data Lake Store as additional storage for the cluster as well.</span></span> <span data-ttu-id="05a1d-164">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="05a1d-164">In such cases, the cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="05a1d-165">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span><span class="sxs-lookup"><span data-stu-id="05a1d-165">If you are running HDInsight jobs against the data stored in Data Lake Store as additional storage, you must use the fully-qualified path to the files.</span></span> <span data-ttu-id="05a1d-166">For example:</span><span class="sxs-lookup"><span data-stu-id="05a1d-166">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="05a1d-167">Note that there's no **cluster_root_path** in the URL now.</span><span class="sxs-lookup"><span data-stu-id="05a1d-167">Note that there's no **cluster_root_path** in the URL now.</span></span> <span data-ttu-id="05a1d-168">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span><span class="sxs-lookup"><span data-stu-id="05a1d-168">That's because Data Lake Store is not a default storage in this case so all you need to do is provide the path to the files.</span></span>

<span data-ttu-id="05a1d-169">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span><span class="sxs-lookup"><span data-stu-id="05a1d-169">To be able to use a Data Lake Store as additional storage, you only need to grant the service principal access to the paths where your files are stored.</span></span>  <span data-ttu-id="05a1d-170">For example:</span><span class="sxs-lookup"><span data-stu-id="05a1d-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="05a1d-171">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="05a1d-171">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="05a1d-172">Use more than one Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="05a1d-172">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="05a1d-173">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="05a1d-173">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving the HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="05a1d-174">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="05a1d-174">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="05a1d-175">Configure Data Lake store access</span><span class="sxs-lookup"><span data-stu-id="05a1d-175">Configure Data Lake store access</span></span>

<span data-ttu-id="05a1d-176">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span><span class="sxs-lookup"><span data-stu-id="05a1d-176">To configure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="05a1d-177">Only an Azure AD administrator can create a service principal.</span><span class="sxs-lookup"><span data-stu-id="05a1d-177">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="05a1d-178">The service principal must be created with a certificate.</span><span class="sxs-lookup"><span data-stu-id="05a1d-178">The service principal must be created with a certificate.</span></span> <span data-ttu-id="05a1d-179">For more information, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="05a1d-179">For more information, see [Quickstart: Set up clusters in HDInsight](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="05a1d-180">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span><span class="sxs-lookup"><span data-stu-id="05a1d-180">If you are going to use Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create the cluster as described in this article.</span></span> <span data-ttu-id="05a1d-181">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is not a supported scenario.</span><span class="sxs-lookup"><span data-stu-id="05a1d-181">Adding Azure Data Lake Store as additional storage to an existing HDInsight cluster is not a supported scenario.</span></span>
>

## <a name="access-files-from-the-cluster"></a><span data-ttu-id="05a1d-182">Access files from the cluster</span><span class="sxs-lookup"><span data-stu-id="05a1d-182">Access files from the cluster</span></span>

<span data-ttu-id="05a1d-183">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="05a1d-183">There are several ways you can access the files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="05a1d-184">**Using the fully qualified name**.</span><span class="sxs-lookup"><span data-stu-id="05a1d-184">**Using the fully qualified name**.</span></span> <span data-ttu-id="05a1d-185">With this approach, you provide the full path to the file that you want to access.</span><span class="sxs-lookup"><span data-stu-id="05a1d-185">With this approach, you provide the full path to the file that you want to access.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="05a1d-186">**Using the shortened path format**.</span><span class="sxs-lookup"><span data-stu-id="05a1d-186">**Using the shortened path format**.</span></span> <span data-ttu-id="05a1d-187">With this approach, you replace the path up to the cluster root with adl:///.</span><span class="sxs-lookup"><span data-stu-id="05a1d-187">With this approach, you replace the path up to the cluster root with adl:///.</span></span> <span data-ttu-id="05a1d-188">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="05a1d-188">So, in the example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="05a1d-189">**Using the relative path**.</span><span class="sxs-lookup"><span data-stu-id="05a1d-189">**Using the relative path**.</span></span> <span data-ttu-id="05a1d-190">With this approach, you only provide the relative path to the file that you want to access.</span><span class="sxs-lookup"><span data-stu-id="05a1d-190">With this approach, you only provide the relative path to the file that you want to access.</span></span> <span data-ttu-id="05a1d-191">For example, if the complete path to the file is:</span><span class="sxs-lookup"><span data-stu-id="05a1d-191">For example, if the complete path to the file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="05a1d-192">You can access the same sample.log file by using this relative path instead.</span><span class="sxs-lookup"><span data-stu-id="05a1d-192">You can access the same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-to-data-lake-store"></a><span data-ttu-id="05a1d-193">Create HDInsight clusters with access to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="05a1d-193">Create HDInsight clusters with access to Data Lake Store</span></span>

<span data-ttu-id="05a1d-194">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="05a1d-194">Use the following links for detailed instructions on how to create HDInsight clusters with access to Data Lake Store.</span></span>

* [<span data-ttu-id="05a1d-195">Using Portal</span><span class="sxs-lookup"><span data-stu-id="05a1d-195">Using Portal</span></span>](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md)
* [<span data-ttu-id="05a1d-196">Using PowerShell (with Data Lake Store as default storage)</span><span class="sxs-lookup"><span data-stu-id="05a1d-196">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="05a1d-197">Using PowerShell (with Data Lake Store as additional storage)</span><span class="sxs-lookup"><span data-stu-id="05a1d-197">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="05a1d-198">Using Azure templates</span><span class="sxs-lookup"><span data-stu-id="05a1d-198">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)

## <a name="refresh-the-hdinsight-certificate-for-data-lake-store-access"></a><span data-ttu-id="05a1d-199">Refresh the HDInsight certificate for Data Lake Store access</span><span class="sxs-lookup"><span data-stu-id="05a1d-199">Refresh the HDInsight certificate for Data Lake Store access</span></span>

<span data-ttu-id="05a1d-200">The following example PowerShell code reads a local certificate file, and updates your HDInsight cluster with the new certificate to access Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="05a1d-200">The following example PowerShell code reads a local certificate file, and updates your HDInsight cluster with the new certificate to access Azure Data Lake Store.</span></span> <span data-ttu-id="05a1d-201">Provide your own HDInsight cluster name, resource group name, subscription ID, app ID, local path to the certificate.</span><span class="sxs-lookup"><span data-stu-id="05a1d-201">Provide your own HDInsight cluster name, resource group name, subscription ID, app ID, local path to the certificate.</span></span> <span data-ttu-id="05a1d-202">Type in the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="05a1d-202">Type in the password when prompted.</span></span>

```powershell-interactive
$clusterName = '<clustername>'
$resourceGroupName = '<resourcegroupname>'
$subscriptionId = '01234567-8a6c-43bc-83d3-6b318c6c7305'
$appId = '01234567-e100-4118-8ba6-c25834f4e938'
$generateSelfSignedCert = $false
$addNewCertKeyCredential = $true
$certFilePath = 'C:\localfolder\adls.pfx'
$certPassword = Read-Host "Enter Certificate Password"

if($generateSelfSignedCert)
{
    Write-Host "Generating new SelfSigned certificate"
    
    $cert = New-SelfSignedCertificate -CertStoreLocation "cert:\CurrentUser\My" -Subject "CN=hdinsightAdlsCert" -KeySpec KeyExchange
    $certBytes = $cert.Export([System.Security.Cryptography.X509Certificates.X509ContentType]::Pkcs12, $certPassword);
    $certString = [System.Convert]::ToBase64String($certBytes)
}
else
{

    Write-Host "Reading the cert file from path $certFilePath"

    $cert = new-object System.Security.Cryptography.X509Certificates.X509Certificate2($certFilePath, $certPassword)
    $certString = [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes($certFilePath))
}

Login-AzureRmAccount

if($addNewCertKeyCredential)
{
    Write-Host "Creating new KeyCredential for the app"
    $keyValue = [System.Convert]::ToBase64String($cert.GetRawCertData())
    New-AzureRmADAppCredential -ApplicationId $appId -CertValue $keyValue -EndDate $cert.NotAfter -StartDate $cert.NotBefore
    Write-Host "Waiting for 30 seconds for the permissions to get propagated"
    Start-Sleep -s 30
}

Select-AzureRmSubscription -SubscriptionId $subscriptionId
Write-Host "Updating the certificate on HDInsight cluster..."

Invoke-AzureRmResourceAction `
    -ResourceGroupName $resourceGroupName `
    -ResourceType 'Microsoft.HDInsight/clusters' `
    -ResourceName $clusterName `
    -ApiVersion '2015-03-01-preview' `
    -Action 'updateclusteridentitycertificate' `
    -Parameters @{ ApplicationId = $appId; Certificate = $certString; CertificatePassword = $certPassword.ToString() } `
    -Force
```

## <a name="next-steps"></a><span data-ttu-id="05a1d-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="05a1d-203">Next steps</span></span>
<span data-ttu-id="05a1d-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05a1d-204">In this article, you learned how to use HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="05a1d-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span><span class="sxs-lookup"><span data-stu-id="05a1d-205">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="05a1d-206">For more information, see:</span><span class="sxs-lookup"><span data-stu-id="05a1d-206">For more information, see:</span></span>

* <span data-ttu-id="05a1d-207">[Get started with Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="05a1d-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="05a1d-208">Quickstart: Set up clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="05a1d-208">Quickstart: Set up clusters in HDInsight</span></span>](../storage/data-lake-storage/quickstart-create-connect-hdi-cluster.md)
* [<span data-ttu-id="05a1d-209">Create an HDInsight cluster to use Data Lake Store using the Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="05a1d-209">Create an HDInsight cluster to use Data Lake Store using the Azure PowerShell</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* <span data-ttu-id="05a1d-210">[Upload data to HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="05a1d-210">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="05a1d-211">[Use Hive with HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="05a1d-211">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="05a1d-212">[Use Pig with HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="05a1d-212">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="05a1d-213">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="05a1d-213">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]:hadoop/apache-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]:hadoop/hdinsight-use-hive.md
[hdinsight-use-pig]:hadoop/hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
