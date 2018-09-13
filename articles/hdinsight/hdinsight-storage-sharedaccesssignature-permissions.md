---
title: Restrict HDInsight access to data using Shared Access Signatures
description: Learn how to use Shared Access Signatures to restrict HDInsight access to data stored in Azure storage blobs.
services: hdinsight
documentationcenter: ''
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 7bcad2dd-edea-467c-9130-44cffc005ff3
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/28/2017
ms.author: larryfr
ms.openlocfilehash: 758a7e3792869d532d1667277d230f5f5b9d38ca
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662982"
---
# <a name="use-azure-storage-shared-access-signatures-to-restrict-access-to-data-with-hdinsight"></a><span data-ttu-id="67e79-103">Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-103">Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight</span></span>
<span data-ttu-id="67e79-104">HDInsight uses Azure storage Blobs for data storage.</span><span class="sxs-lookup"><span data-stu-id="67e79-104">HDInsight uses Azure storage Blobs for data storage.</span></span> <span data-ttu-id="67e79-105">While HDInsight must have full access to the blob used as default storage for the cluster, you can restrict permissions to data stored in other blobs used by the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-105">While HDInsight must have full access to the blob used as default storage for the cluster, you can restrict permissions to data stored in other blobs used by the cluster.</span></span> <span data-ttu-id="67e79-106">For example, you may want to make some data read-only.</span><span class="sxs-lookup"><span data-stu-id="67e79-106">For example, you may want to make some data read-only.</span></span> <span data-ttu-id="67e79-107">You can do this using Shared Access Signatures.</span><span class="sxs-lookup"><span data-stu-id="67e79-107">You can do this using Shared Access Signatures.</span></span>

<span data-ttu-id="67e79-108">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span><span class="sxs-lookup"><span data-stu-id="67e79-108">Shared Access Signatures (SAS) are a feature of Azure storage accounts that allows you to limit access to data.</span></span> <span data-ttu-id="67e79-109">For example, providing read-only access to data.</span><span class="sxs-lookup"><span data-stu-id="67e79-109">For example, providing read-only access to data.</span></span> <span data-ttu-id="67e79-110">In this document, you learn how to use SAS to enable read and list-only access to a blob container from HDInsight.</span><span class="sxs-lookup"><span data-stu-id="67e79-110">In this document, you learn how to use SAS to enable read and list-only access to a blob container from HDInsight.</span></span>

## <a name="requirements"></a><span data-ttu-id="67e79-111">Requirements</span><span class="sxs-lookup"><span data-stu-id="67e79-111">Requirements</span></span>
* <span data-ttu-id="67e79-112">An Azure subscription</span><span class="sxs-lookup"><span data-stu-id="67e79-112">An Azure subscription</span></span>
* <span data-ttu-id="67e79-113">C# or Python.</span><span class="sxs-lookup"><span data-stu-id="67e79-113">C# or Python.</span></span> <span data-ttu-id="67e79-114">C# example code is provided as a Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="67e79-114">C# example code is provided as a Visual Studio solution.</span></span>

  * <span data-ttu-id="67e79-115">Visual Studio must be version 2013, 2015, or 2017</span><span class="sxs-lookup"><span data-stu-id="67e79-115">Visual Studio must be version 2013, 2015, or 2017</span></span>
  * <span data-ttu-id="67e79-116">Python must be version 2.7 or higher</span><span class="sxs-lookup"><span data-stu-id="67e79-116">Python must be version 2.7 or higher</span></span>

* <span data-ttu-id="67e79-117">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-117">A Linux-based HDInsight cluster OR [Azure PowerShell][powershell] - If you have an existing Linux-based cluster, you can use Ambari to add a Shared Access Signature to the cluster.</span></span> <span data-ttu-id="67e79-118">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="67e79-118">If not, you can use Azure PowerShell to create a cluster and add a Shared Access Signature during cluster creation.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="67e79-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span><span class="sxs-lookup"><span data-stu-id="67e79-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="67e79-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span><span class="sxs-lookup"><span data-stu-id="67e79-120">For more information, see [HDInsight Deprecation on Windows](hdinsight-component-versioning.md#hdi-version-33-nearing-deprecation-date).</span></span>

* <span data-ttu-id="67e79-121">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="67e79-121">The example files from [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span> <span data-ttu-id="67e79-122">This repository contains the following items:</span><span class="sxs-lookup"><span data-stu-id="67e79-122">This repository contains the following items:</span></span>

  * <span data-ttu-id="67e79-123">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-123">A Visual Studio project that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="67e79-124">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-124">A Python script that can create a storage container, stored policy, and SAS for use with HDInsight</span></span>
  * <span data-ttu-id="67e79-125">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span><span class="sxs-lookup"><span data-stu-id="67e79-125">A PowerShell script that can create a HDInsight cluster and configure it to use the SAS.</span></span>

## <a name="shared-access-signatures"></a><span data-ttu-id="67e79-126">Shared Access Signatures</span><span class="sxs-lookup"><span data-stu-id="67e79-126">Shared Access Signatures</span></span>
<span data-ttu-id="67e79-127">There are two forms of Shared Access Signatures:</span><span class="sxs-lookup"><span data-stu-id="67e79-127">There are two forms of Shared Access Signatures:</span></span>

* <span data-ttu-id="67e79-128">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI (or implied, in the case where start time is omitted).</span><span class="sxs-lookup"><span data-stu-id="67e79-128">Ad hoc: The start time, expiry time, and permissions for the SAS are all specified on the SAS URI (or implied, in the case where start time is omitted).</span></span>
* <span data-ttu-id="67e79-129">Stored access policy: A stored access policy is defined on a resource container, such as a blob container, table, queue, or file share.</span><span class="sxs-lookup"><span data-stu-id="67e79-129">Stored access policy: A stored access policy is defined on a resource container, such as a blob container, table, queue, or file share.</span></span> <span data-ttu-id="67e79-130">A policy can be used to manage constraints for one or more shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="67e79-130">A policy can be used to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="67e79-131">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span><span class="sxs-lookup"><span data-stu-id="67e79-131">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span>

<span data-ttu-id="67e79-132">The difference between the two forms is important for one key scenario: revocation.</span><span class="sxs-lookup"><span data-stu-id="67e79-132">The difference between the two forms is important for one key scenario: revocation.</span></span> <span data-ttu-id="67e79-133">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span><span class="sxs-lookup"><span data-stu-id="67e79-133">A SAS is a URL, so anyone who obtains the SAS can use it, regardless of who requested it to begin with.</span></span> <span data-ttu-id="67e79-134">If a SAS is published publicly, it can be used by anyone in the world.</span><span class="sxs-lookup"><span data-stu-id="67e79-134">If a SAS is published publicly, it can be used by anyone in the world.</span></span> <span data-ttu-id="67e79-135">A SAS that is distributed is valid until one of four things happens:</span><span class="sxs-lookup"><span data-stu-id="67e79-135">A SAS that is distributed is valid until one of four things happens:</span></span>

1. <span data-ttu-id="67e79-136">The expiry time specified on the SAS is reached.</span><span class="sxs-lookup"><span data-stu-id="67e79-136">The expiry time specified on the SAS is reached.</span></span>
2. <span data-ttu-id="67e79-137">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span><span class="sxs-lookup"><span data-stu-id="67e79-137">The expiry time specified on the stored access policy referenced by the SAS is reached (if a stored access policy is referenced, and if it specifies an expiry time).</span></span> <span data-ttu-id="67e79-138">This can either occur because the interval elapses, or because you have modified the stored access policy to have an expiry time in the past, which is one way to revoke the SAS.</span><span class="sxs-lookup"><span data-stu-id="67e79-138">This can either occur because the interval elapses, or because you have modified the stored access policy to have an expiry time in the past, which is one way to revoke the SAS.</span></span>
3. <span data-ttu-id="67e79-139">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span><span class="sxs-lookup"><span data-stu-id="67e79-139">The stored access policy referenced by the SAS is deleted, which is another way to revoke the SAS.</span></span> <span data-ttu-id="67e79-140">If you recreate the stored access policy with exactly the same name, all  SAS tokens for the previous policy will be valid (if the expiry time on the SAS has not passed).</span><span class="sxs-lookup"><span data-stu-id="67e79-140">If you recreate the stored access policy with exactly the same name, all  SAS tokens for the previous policy will be valid (if the expiry time on the SAS has not passed).</span></span> <span data-ttu-id="67e79-141">If you intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span><span class="sxs-lookup"><span data-stu-id="67e79-141">If you intending to revoke the SAS, be sure to use a different name if you recreate the access policy with an expiry time in the future.</span></span>
4. <span data-ttu-id="67e79-142">The account key that was used to create the SAS is regenerated.</span><span class="sxs-lookup"><span data-stu-id="67e79-142">The account key that was used to create the SAS is regenerated.</span></span> <span data-ttu-id="67e79-143">Regenerating the key causes all application components that use the previous key to fail authentication until they are updated the new key.</span><span class="sxs-lookup"><span data-stu-id="67e79-143">Regenerating the key causes all application components that use the previous key to fail authentication until they are updated the new key.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="67e79-144">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span><span class="sxs-lookup"><span data-stu-id="67e79-144">A shared access signature URI is associated with the account key used to create the signature, and the associated stored access policy (if any).</span></span> <span data-ttu-id="67e79-145">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span><span class="sxs-lookup"><span data-stu-id="67e79-145">If no stored access policy is specified, the only way to revoke a shared access signature is to change the account key.</span></span>
>
>

<span data-ttu-id="67e79-146">It is recommended that you always use stored access policies, so that you can either revoke signatures or extend the expiry date as needed.</span><span class="sxs-lookup"><span data-stu-id="67e79-146">It is recommended that you always use stored access policies, so that you can either revoke signatures or extend the expiry date as needed.</span></span> <span data-ttu-id="67e79-147">The steps in this document use stored access policies to generate SAS.</span><span class="sxs-lookup"><span data-stu-id="67e79-147">The steps in this document use stored access policies to generate SAS.</span></span>

<span data-ttu-id="67e79-148">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="67e79-148">For more information on Shared Access Signatures, see [Understanding the SAS model](../storage/storage-dotnet-shared-access-signature-part-1.md).</span></span>

## <a name="create-a-stored-policy-and-generate-a-sas"></a><span data-ttu-id="67e79-149">Create a stored policy and generate a SAS</span><span class="sxs-lookup"><span data-stu-id="67e79-149">Create a stored policy and generate a SAS</span></span>
<span data-ttu-id="67e79-150">Currently you must create a stored policy programmatically.</span><span class="sxs-lookup"><span data-stu-id="67e79-150">Currently you must create a stored policy programmatically.</span></span> <span data-ttu-id="67e79-151">You can find both the C# and Python example of creating a stored policy and SAS at [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span><span class="sxs-lookup"><span data-stu-id="67e79-151">You can find both the C# and Python example of creating a stored policy and SAS at [https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature](https://github.com/Azure-Samples/hdinsight-dotnet-python-azure-storage-shared-access-signature).</span></span>

### <a name="create-a-stored-policy-and-sas-using-c"></a><span data-ttu-id="67e79-152">Create a stored policy and SAS using C\\</span><span class="sxs-lookup"><span data-stu-id="67e79-152">Create a stored policy and SAS using C\\</span></span>
1. <span data-ttu-id="67e79-153">Open the solution in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67e79-153">Open the solution in Visual Studio.</span></span>
2. <span data-ttu-id="67e79-154">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="67e79-154">In Solution Explorer, right-click on the **SASToken** project and select **Properties**.</span></span>
3. <span data-ttu-id="67e79-155">Select **Settings** and add values for the following entries:</span><span class="sxs-lookup"><span data-stu-id="67e79-155">Select **Settings** and add values for the following entries:</span></span>

   * <span data-ttu-id="67e79-156">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span><span class="sxs-lookup"><span data-stu-id="67e79-156">StorageConnectionString: The connection string for the storage account that you want to create a stored policy and SAS for.</span></span> <span data-ttu-id="67e79-157">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span><span class="sxs-lookup"><span data-stu-id="67e79-157">The format should be `DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey` where `myaccount` is the name of your storage account and `mykey` is the key for the storage account.</span></span>
   * <span data-ttu-id="67e79-158">ContainerName: The container in the storage account that you want to restrict access to.</span><span class="sxs-lookup"><span data-stu-id="67e79-158">ContainerName: The container in the storage account that you want to restrict access to.</span></span>
   * <span data-ttu-id="67e79-159">SASPolicyName: The name to use for the stored policy to create.</span><span class="sxs-lookup"><span data-stu-id="67e79-159">SASPolicyName: The name to use for the stored policy to create.</span></span>
   * <span data-ttu-id="67e79-160">FileToUpload: The path to a file that is uploaded to the container.</span><span class="sxs-lookup"><span data-stu-id="67e79-160">FileToUpload: The path to a file that is uploaded to the container.</span></span>
4. <span data-ttu-id="67e79-161">Run the project.</span><span class="sxs-lookup"><span data-stu-id="67e79-161">Run the project.</span></span> <span data-ttu-id="67e79-162">A console window appears, and information similar to the following text is displayed once the SAS has been generated:</span><span class="sxs-lookup"><span data-stu-id="67e79-162">A console window appears, and information similar to the following text is displayed once the SAS has been generated:</span></span>

        Container SAS token using stored access policy: sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="67e79-163">Save the SAS policy token, storage account name, and container name.</span><span class="sxs-lookup"><span data-stu-id="67e79-163">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="67e79-164">These values are used when associating the storage account with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-164">These values are used when associating the storage account with your HDInsight cluster.</span></span>

### <a name="create-a-stored-policy-and-sas-using-python"></a><span data-ttu-id="67e79-165">Create a stored policy and SAS using Python</span><span class="sxs-lookup"><span data-stu-id="67e79-165">Create a stored policy and SAS using Python</span></span>
1. <span data-ttu-id="67e79-166">Open the SASToken.py file and change the following values:</span><span class="sxs-lookup"><span data-stu-id="67e79-166">Open the SASToken.py file and change the following values:</span></span>

   * <span data-ttu-id="67e79-167">policy\_name: The name to use for the stored policy to create.</span><span class="sxs-lookup"><span data-stu-id="67e79-167">policy\_name: The name to use for the stored policy to create.</span></span>
   * <span data-ttu-id="67e79-168">storage\_account\_name: The name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="67e79-168">storage\_account\_name: The name of your storage account.</span></span>
   * <span data-ttu-id="67e79-169">storage\_account\_key: The key for the storage account.</span><span class="sxs-lookup"><span data-stu-id="67e79-169">storage\_account\_key: The key for the storage account.</span></span>
   * <span data-ttu-id="67e79-170">storage\_container\_name: The container in the storage account that you want to restrict access to.</span><span class="sxs-lookup"><span data-stu-id="67e79-170">storage\_container\_name: The container in the storage account that you want to restrict access to.</span></span>
   * <span data-ttu-id="67e79-171">example\_file\_path: The path to a file that is uploaded to the container</span><span class="sxs-lookup"><span data-stu-id="67e79-171">example\_file\_path: The path to a file that is uploaded to the container</span></span>
2. <span data-ttu-id="67e79-172">Run the script.</span><span class="sxs-lookup"><span data-stu-id="67e79-172">Run the script.</span></span> <span data-ttu-id="67e79-173">It displays the SAS token similar to the following text when the script completes:</span><span class="sxs-lookup"><span data-stu-id="67e79-173">It displays the SAS token similar to the following text when the script completes:</span></span>

        sr=c&si=policyname&sig=dOAi8CXuz5Fm15EjRUu5dHlOzYNtcK3Afp1xqxniEps%3D&sv=2014-02-14

    <span data-ttu-id="67e79-174">Save the SAS policy token, storage account name, and container name.</span><span class="sxs-lookup"><span data-stu-id="67e79-174">Save the SAS policy token, storage account name, and container name.</span></span> <span data-ttu-id="67e79-175">These values are used when associating the storage account with your HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-175">These values are used when associating the storage account with your HDInsight cluster.</span></span>

## <a name="use-the-sas-with-hdinsight"></a><span data-ttu-id="67e79-176">Use the SAS with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-176">Use the SAS with HDInsight</span></span>
<span data-ttu-id="67e79-177">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span><span class="sxs-lookup"><span data-stu-id="67e79-177">When creating an HDInsight cluster, you must specify a primary storage account and you can optionally specify additional storage accounts.</span></span> <span data-ttu-id="67e79-178">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span><span class="sxs-lookup"><span data-stu-id="67e79-178">Both of these methods of adding storage require full access to the storage accounts and containers that are used.</span></span>

<span data-ttu-id="67e79-179">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-179">To use a Shared Access Signature to limit access to a container, add a custom entry to the **core-site** configuration for the cluster.</span></span>

* <span data-ttu-id="67e79-180">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="67e79-180">For **Windows-based** or **Linux-based** HDInsight clusters, you can add the entry during cluster creation using PowerShell.</span></span>
* <span data-ttu-id="67e79-181">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span><span class="sxs-lookup"><span data-stu-id="67e79-181">For **Linux-based** HDInsight clusters, change the configuration after cluster creation using Ambari.</span></span>

### <a name="create-a-cluster-that-uses-the-sas"></a><span data-ttu-id="67e79-182">Create a cluster that uses the SAS</span><span class="sxs-lookup"><span data-stu-id="67e79-182">Create a cluster that uses the SAS</span></span>
<span data-ttu-id="67e79-183">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span><span class="sxs-lookup"><span data-stu-id="67e79-183">An example of creating an HDInsight cluster that uses the SAS is included in the `CreateCluster` directory of the repository.</span></span> <span data-ttu-id="67e79-184">To use it, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="67e79-184">To use it, use the following steps:</span></span>

1. <span data-ttu-id="67e79-185">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span><span class="sxs-lookup"><span data-stu-id="67e79-185">Open the `CreateCluster\HDInsightSAS.ps1` file in a text editor and modify the following values at the beginning of the document.</span></span>

        # Replace 'mycluster' with the name of the cluster to be created
        $clusterName = 'mycluster'
        # Valid values are 'Linux' and 'Windows'
        $osType = 'Linux'
        # Replace 'myresourcegroup' with the name of the group to be created
        $resourceGroupName = 'myresourcegroup'
        # Replace with the Azure data center you want to the cluster to live in
        $location = 'North Europe'
        # Replace with the name of the default storage account to be created
        $defaultStorageAccountName = 'mystorageaccount'
        # Replace with the name of the SAS container created earlier
        $SASContainerName = 'sascontainer'
        # Replace with the name of the SAS storage account created earlier
        $SASStorageAccountName = 'sasaccount'
        # Replace with the SAS token generated earlier
        $SASToken = 'sastoken'
        # Set the number of worker nodes in the cluster
        $clusterSizeInNodes = 2

    <span data-ttu-id="67e79-186">For example, change `'mycluster'` to the name of the cluster you want to create.</span><span class="sxs-lookup"><span data-stu-id="67e79-186">For example, change `'mycluster'` to the name of the cluster you want to create.</span></span> <span data-ttu-id="67e79-187">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span><span class="sxs-lookup"><span data-stu-id="67e79-187">The SAS values should match the values from the previous steps when creating a storage account and SAS token.</span></span>

    <span data-ttu-id="67e79-188">Once you have changed the values, save the file.</span><span class="sxs-lookup"><span data-stu-id="67e79-188">Once you have changed the values, save the file.</span></span>
2. <span data-ttu-id="67e79-189">Open a new Azure PowerShell prompt.</span><span class="sxs-lookup"><span data-stu-id="67e79-189">Open a new Azure PowerShell prompt.</span></span> <span data-ttu-id="67e79-190">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span><span class="sxs-lookup"><span data-stu-id="67e79-190">If you are unfamiliar with Azure PowerShell, or have not installed it, see [Install and configure Azure PowerShell][powershell].</span></span>
3. <span data-ttu-id="67e79-191">From the prompt, use the following command to authenticate to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="67e79-191">From the prompt, use the following command to authenticate to your Azure subscription:</span></span>

        Login-AzureRmAccount

    <span data-ttu-id="67e79-192">When prompted, log in with the account for your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="67e79-192">When prompted, log in with the account for your Azure subscription.</span></span>

    <span data-ttu-id="67e79-193">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span><span class="sxs-lookup"><span data-stu-id="67e79-193">If your account is associated with multiple Azure subscriptions, you may need to use `Select-AzureRmSubscription` to select the subscription you wish to use.</span></span>
4. <span data-ttu-id="67e79-194">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span><span class="sxs-lookup"><span data-stu-id="67e79-194">From the prompt, change directories to the `CreateCluster` directory that contains the HDInsightSAS.ps1 file.</span></span> <span data-ttu-id="67e79-195">Then use the following command to run the script</span><span class="sxs-lookup"><span data-stu-id="67e79-195">Then use the following command to run the script</span></span>

        .\HDInsightSAS.ps1

    <span data-ttu-id="67e79-196">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="67e79-196">As the script runs, it logs output to the PowerShell prompt as it creates the resource group and storage accounts.</span></span> <span data-ttu-id="67e79-197">You are prompted to enter the HTTP user for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-197">You are prompted to enter the HTTP user for the HDInsight cluster.</span></span> <span data-ttu-id="67e79-198">This account is used to secure HTTP/s access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-198">This account is used to secure HTTP/s access to the cluster.</span></span>

    <span data-ttu-id="67e79-199">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span><span class="sxs-lookup"><span data-stu-id="67e79-199">If you are creating a Linux-based cluster, you are prompted for an SSH user account name and password.</span></span> <span data-ttu-id="67e79-200">This account is used to remotely log in to the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-200">This account is used to remotely log in to the cluster.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="67e79-201">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="67e79-201">When prompted for the HTTP/s or SSH user name and password, you must provide a password that meets the following criteria:</span></span>
   >
   > * <span data-ttu-id="67e79-202">Must be at least 10 characters in length</span><span class="sxs-lookup"><span data-stu-id="67e79-202">Must be at least 10 characters in length</span></span>
   > * <span data-ttu-id="67e79-203">Must contain at least one digit</span><span class="sxs-lookup"><span data-stu-id="67e79-203">Must contain at least one digit</span></span>
   > * <span data-ttu-id="67e79-204">Must contain at least one non-alphanumeric character</span><span class="sxs-lookup"><span data-stu-id="67e79-204">Must contain at least one non-alphanumeric character</span></span>
   > * <span data-ttu-id="67e79-205">Must contain at least one upper or lower case letter</span><span class="sxs-lookup"><span data-stu-id="67e79-205">Must contain at least one upper or lower case letter</span></span>
   >
   >

<span data-ttu-id="67e79-206">It takes a while for this script to complete, usually around 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="67e79-206">It takes a while for this script to complete, usually around 15 minutes.</span></span> <span data-ttu-id="67e79-207">When the script completes without any errors, the cluster has been created.</span><span class="sxs-lookup"><span data-stu-id="67e79-207">When the script completes without any errors, the cluster has been created.</span></span>

### <a name="use-the-sas-with-an-existing-cluster"></a><span data-ttu-id="67e79-208">Use the SAS with an existing cluster</span><span class="sxs-lookup"><span data-stu-id="67e79-208">Use the SAS with an existing cluster</span></span>

<span data-ttu-id="67e79-209">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span><span class="sxs-lookup"><span data-stu-id="67e79-209">If you have an existing Linux-based cluster, you can add the SAS to the **core-site** configuration by using the following steps:</span></span>

1. <span data-ttu-id="67e79-210">Open the Ambari web UI for your cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-210">Open the Ambari web UI for your cluster.</span></span> <span data-ttu-id="67e79-211">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="67e79-211">The address for this page is https://YOURCLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="67e79-212">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-212">When prompted, authenticate to the cluster using the admin name (admin) and password you used when creating the cluster.</span></span>
2. <span data-ttu-id="67e79-213">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span><span class="sxs-lookup"><span data-stu-id="67e79-213">From the left side of the Ambari web UI, select **HDFS** and then select the **Configs** tab in the middle of the page.</span></span>
3. <span data-ttu-id="67e79-214">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span><span class="sxs-lookup"><span data-stu-id="67e79-214">Select the **Advanced** tab, and then scroll until you find the **Custom core-site** section.</span></span>
4. <span data-ttu-id="67e79-215">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span><span class="sxs-lookup"><span data-stu-id="67e79-215">Expand the **Custom core-site** section, then scroll to the end and select the **Add property...** link.</span></span> <span data-ttu-id="67e79-216">Use the following values for the **Key** and **Value** fields:</span><span class="sxs-lookup"><span data-stu-id="67e79-216">Use the following values for the **Key** and **Value** fields:</span></span>

   * <span data-ttu-id="67e79-217">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="67e79-217">**Key**: fs.azure.sas.CONTAINERNAME.STORAGEACCOUNTNAME.blob.core.windows.net</span></span>
   * <span data-ttu-id="67e79-218">**Value**: The SAS returned by the C# or Python application you ran previously</span><span class="sxs-lookup"><span data-stu-id="67e79-218">**Value**: The SAS returned by the C# or Python application you ran previously</span></span>

     <span data-ttu-id="67e79-219">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span><span class="sxs-lookup"><span data-stu-id="67e79-219">Replace **CONTAINERNAME** with the container name you used with the C# or SAS application.</span></span> <span data-ttu-id="67e79-220">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span><span class="sxs-lookup"><span data-stu-id="67e79-220">Replace **STORAGEACCOUNTNAME** with the storage account name you used.</span></span>
5. <span data-ttu-id="67e79-221">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span><span class="sxs-lookup"><span data-stu-id="67e79-221">Click the **Add** button to save this key and value, then click the **Save** button to save the configuration changes.</span></span> <span data-ttu-id="67e79-222">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="67e79-222">When prompted, add a description of the change ("adding SAS storage access" for example) and then click **Save**.</span></span>

    <span data-ttu-id="67e79-223">Click **OK** when the changes have been completed.</span><span class="sxs-lookup"><span data-stu-id="67e79-223">Click **OK** when the changes have been completed.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="67e79-224">You must restart several services before the change takes effect.</span><span class="sxs-lookup"><span data-stu-id="67e79-224">You must restart several services before the change takes effect.</span></span>
   >
   >
6. <span data-ttu-id="67e79-225">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span><span class="sxs-lookup"><span data-stu-id="67e79-225">In the Ambari web UI, select **HDFS** from the list on the left, and then select **Restart All** from the **Service Actions** drop down list on the right.</span></span> <span data-ttu-id="67e79-226">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span><span class="sxs-lookup"><span data-stu-id="67e79-226">When prompted, select **Turn on maintenance mode** and then select __Conform Restart All".</span></span>

    <span data-ttu-id="67e79-227">Repeat this process for MapReduce2 and YARN.</span><span class="sxs-lookup"><span data-stu-id="67e79-227">Repeat this process for MapReduce2 and YARN.</span></span>

7. <span data-ttu-id="67e79-228">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span><span class="sxs-lookup"><span data-stu-id="67e79-228">Once the services have restarted, select each one and disable maintenance mode from the **Service Actions** drop down.</span></span>

## <a name="test-restricted-access"></a><span data-ttu-id="67e79-229">Test restricted access</span><span class="sxs-lookup"><span data-stu-id="67e79-229">Test restricted access</span></span>
<span data-ttu-id="67e79-230">To verify that you have restricted access, use the following methods:</span><span class="sxs-lookup"><span data-stu-id="67e79-230">To verify that you have restricted access, use the following methods:</span></span>

* <span data-ttu-id="67e79-231">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-231">For **Windows-based** HDInsight clusters, use Remote Desktop to connect to the cluster.</span></span> <span data-ttu-id="67e79-232">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="67e79-232">For more information, see [Connect to HDInsight using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

    <span data-ttu-id="67e79-233">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="67e79-233">Once connected, use the **Hadoop Command-Line** icon on the desktop to open a command prompt.</span></span>
* <span data-ttu-id="67e79-234">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span><span class="sxs-lookup"><span data-stu-id="67e79-234">For **Linux-based** HDInsight clusters, use SSH to connect to the cluster.</span></span> <span data-ttu-id="67e79-235">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="67e79-235">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

<span data-ttu-id="67e79-236">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span><span class="sxs-lookup"><span data-stu-id="67e79-236">Once connected to the cluster, use the following steps to verify that you can only read and list items on the SAS storage account:</span></span>

1. <span data-ttu-id="67e79-237">From the prompt, type the following.</span><span class="sxs-lookup"><span data-stu-id="67e79-237">From the prompt, type the following.</span></span> <span data-ttu-id="67e79-238">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span><span class="sxs-lookup"><span data-stu-id="67e79-238">Replace **SASCONTAINER** with the name of the container created for the SAS storage account.</span></span> <span data-ttu-id="67e79-239">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS:</span><span class="sxs-lookup"><span data-stu-id="67e79-239">Replace **SASACCOUNTNAME** with the name of the storage account used for the SAS:</span></span>

        hdfs dfs -ls wasbs://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/

    <span data-ttu-id="67e79-240">This command lists the contents of the container, which should include the file that was uploaded when the container and SAS was created.</span><span class="sxs-lookup"><span data-stu-id="67e79-240">This command lists the contents of the container, which should include the file that was uploaded when the container and SAS was created.</span></span>
2. <span data-ttu-id="67e79-241">Use the following command to verify that you can read the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="67e79-241">Use the following command to verify that you can read the contents of the file.</span></span> <span data-ttu-id="67e79-242">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span><span class="sxs-lookup"><span data-stu-id="67e79-242">Replace the **SASCONTAINER** and **SASACCOUNTNAME** as in the previous step.</span></span> <span data-ttu-id="67e79-243">Replace **FILENAME** with the name of the file displayed in the previous command:</span><span class="sxs-lookup"><span data-stu-id="67e79-243">Replace **FILENAME** with the name of the file displayed in the previous command:</span></span>

        hdfs dfs -text wasbs://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME

    <span data-ttu-id="67e79-244">This command lists the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="67e79-244">This command lists the contents of the file.</span></span>
3. <span data-ttu-id="67e79-245">Use the following command to download the file to the local file system:</span><span class="sxs-lookup"><span data-stu-id="67e79-245">Use the following command to download the file to the local file system:</span></span>

        hdfs dfs -get wasbs://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/FILENAME testfile.txt

    <span data-ttu-id="67e79-246">This command downloads the file to a local file named **testfile.txt**.</span><span class="sxs-lookup"><span data-stu-id="67e79-246">This command downloads the file to a local file named **testfile.txt**.</span></span>
4. <span data-ttu-id="67e79-247">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span><span class="sxs-lookup"><span data-stu-id="67e79-247">Use the following command to upload the local file to a new file named **testupload.txt** on the SAS storage:</span></span>

        hdfs dfs -put testfile.txt wasbs://SASCONTAINER@SASACCOUNTNAME.blob.core.windows.net/testupload.txt

    <span data-ttu-id="67e79-248">You receive a message similar to the following text:</span><span class="sxs-lookup"><span data-stu-id="67e79-248">You receive a message similar to the following text:</span></span>

        put: java.io.IOException

    <span data-ttu-id="67e79-249">This error occurs because the storage location is read+list only.</span><span class="sxs-lookup"><span data-stu-id="67e79-249">This error occurs because the storage location is read+list only.</span></span> <span data-ttu-id="67e79-250">Use the following command to put the data on the default storage for the cluster, which is writable:</span><span class="sxs-lookup"><span data-stu-id="67e79-250">Use the following command to put the data on the default storage for the cluster, which is writable:</span></span>

        hdfs dfs -put testfile.txt wasbs:///testupload.txt

    <span data-ttu-id="67e79-251">This time, the operation should complete successfully.</span><span class="sxs-lookup"><span data-stu-id="67e79-251">This time, the operation should complete successfully.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="67e79-252">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="67e79-252">Troubleshooting</span></span>
### <a name="a-task-was-canceled"></a><span data-ttu-id="67e79-253">A task was canceled</span><span class="sxs-lookup"><span data-stu-id="67e79-253">A task was canceled</span></span>
<span data-ttu-id="67e79-254">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span><span class="sxs-lookup"><span data-stu-id="67e79-254">**Symptoms**: When creating a cluster using the PowerShell script, you may receive the following error message:</span></span>

    New-AzureRmHDInsightCluster : A task was canceled.
    At C:\Users\larryfr\Documents\GitHub\hdinsight-azure-storage-sas\CreateCluster\HDInsightSAS.ps1:62 char:5
    +     New-AzureRmHDInsightCluster `
    +     ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
        + CategoryInfo          : NotSpecified: (:) [New-AzureRmHDInsightCluster], CloudException
        + FullyQualifiedErrorId : Hyak.Common.CloudException,Microsoft.Azure.Commands.HDInsight.NewAzureHDInsightClusterCommand

<span data-ttu-id="67e79-255">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span><span class="sxs-lookup"><span data-stu-id="67e79-255">**Cause**: This error can occur if you use a password for the admin/HTTP user for the cluster, or (for Linux-based clusters) the SSH user.</span></span>

<span data-ttu-id="67e79-256">**Resolution**: Use a password that meets the following criteria:</span><span class="sxs-lookup"><span data-stu-id="67e79-256">**Resolution**: Use a password that meets the following criteria:</span></span>

* <span data-ttu-id="67e79-257">Must be at least 10 characters in length</span><span class="sxs-lookup"><span data-stu-id="67e79-257">Must be at least 10 characters in length</span></span>
* <span data-ttu-id="67e79-258">Must contain at least one digit</span><span class="sxs-lookup"><span data-stu-id="67e79-258">Must contain at least one digit</span></span>
* <span data-ttu-id="67e79-259">Must contain at least one non-alphanumeric character</span><span class="sxs-lookup"><span data-stu-id="67e79-259">Must contain at least one non-alphanumeric character</span></span>
* <span data-ttu-id="67e79-260">Must contain at least one upper or lower case letter</span><span class="sxs-lookup"><span data-stu-id="67e79-260">Must contain at least one upper or lower case letter</span></span>

## <a name="next-steps"></a><span data-ttu-id="67e79-261">Next steps</span><span class="sxs-lookup"><span data-stu-id="67e79-261">Next steps</span></span>
<span data-ttu-id="67e79-262">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span><span class="sxs-lookup"><span data-stu-id="67e79-262">Now that you have learned how to add limited-access storage to your HDInsight cluster, learn other ways to work with data on your cluster:</span></span>

* [<span data-ttu-id="67e79-263">Use Hive with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-263">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="67e79-264">Use Pig with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-264">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="67e79-265">Use MapReduce with HDInsight</span><span class="sxs-lookup"><span data-stu-id="67e79-265">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[powershell]: /powershell/azureps-cmdlets-docs
