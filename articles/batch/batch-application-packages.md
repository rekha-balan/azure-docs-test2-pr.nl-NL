---
title: Install application packages on compute nodes - Azure Batch | Microsoft Docs
description: Use the application packages feature of Azure Batch to easily manage multiple applications and versions for installation on Batch compute nodes.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
ms.assetid: 3b6044b7-5f65-4a27-9d43-71e1863d16cf
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 27043b7afab88afc81d24b5fe686ad96e1642105
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669370"
---
# <a name="deploy-applications-to-compute-nodes-with-batch-application-packages"></a><span data-ttu-id="d76fe-103">Deploy applications to compute nodes with Batch application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-103">Deploy applications to compute nodes with Batch application packages</span></span>

<span data-ttu-id="d76fe-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-104">The application packages feature of Azure Batch provides easy management of task applications and their deployment to the compute nodes in your pool.</span></span> <span data-ttu-id="d76fe-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span><span class="sxs-lookup"><span data-stu-id="d76fe-105">With application packages, you can upload and manage multiple versions of the applications your tasks run, including their supporting files.</span></span> <span data-ttu-id="d76fe-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-106">You can then automatically deploy one or more of these applications to the compute nodes in your pool.</span></span>

<span data-ttu-id="d76fe-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d76fe-107">In this article, you will learn how to upload and manage application packages in the Azure portal.</span></span> <span data-ttu-id="d76fe-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span><span class="sxs-lookup"><span data-stu-id="d76fe-108">You will then learn how to install them on a pool's compute nodes with the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="d76fe-109">The application packages feature described here supersedes the "Batch Apps" feature available in previous versions of the service.</span><span class="sxs-lookup"><span data-stu-id="d76fe-109">The application packages feature described here supersedes the "Batch Apps" feature available in previous versions of the service.</span></span>
> 
> 

## <a name="application-package-requirements"></a><span data-ttu-id="d76fe-110">Application package requirements</span><span class="sxs-lookup"><span data-stu-id="d76fe-110">Application package requirements</span></span>
<span data-ttu-id="d76fe-111">You must [link an Azure Storage account](#link-a-storage-account) to your Batch account to use application packages.</span><span class="sxs-lookup"><span data-stu-id="d76fe-111">You must [link an Azure Storage account](#link-a-storage-account) to your Batch account to use application packages.</span></span>

<span data-ttu-id="d76fe-112">The application packages feature discussed in this article is compatible *only* with Batch pools that were created after 10 March 2016.</span><span class="sxs-lookup"><span data-stu-id="d76fe-112">The application packages feature discussed in this article is compatible *only* with Batch pools that were created after 10 March 2016.</span></span> <span data-ttu-id="d76fe-113">Application packages will not be deployed to compute nodes in pools created before this date.</span><span class="sxs-lookup"><span data-stu-id="d76fe-113">Application packages will not be deployed to compute nodes in pools created before this date.</span></span>

<span data-ttu-id="d76fe-114">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span><span class="sxs-lookup"><span data-stu-id="d76fe-114">This feature was introduced in [Batch REST API][api_rest] version 2015-12-01.2.2 and the corresponding [Batch .NET][api_net] library version 3.1.0.</span></span> <span data-ttu-id="d76fe-115">We recommend that you always use the latest API version when working with Batch.</span><span class="sxs-lookup"><span data-stu-id="d76fe-115">We recommend that you always use the latest API version when working with Batch.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d76fe-116">Currently, only *CloudServiceConfiguration* pools support application packages.</span><span class="sxs-lookup"><span data-stu-id="d76fe-116">Currently, only *CloudServiceConfiguration* pools support application packages.</span></span> <span data-ttu-id="d76fe-117">You cannot use Application packages in pools created by using VirtualMachineConfiguration images.</span><span class="sxs-lookup"><span data-stu-id="d76fe-117">You cannot use Application packages in pools created by using VirtualMachineConfiguration images.</span></span> <span data-ttu-id="d76fe-118">See the [Virtual machine configuration](batch-linux-nodes.md#virtual-machine-configuration) section of [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about the two different configurations.</span><span class="sxs-lookup"><span data-stu-id="d76fe-118">See the [Virtual machine configuration](batch-linux-nodes.md#virtual-machine-configuration) section of [Provision Linux compute nodes in Azure Batch pools](batch-linux-nodes.md) for more information about the two different configurations.</span></span>
> 
> 

## <a name="about-applications-and-application-packages"></a><span data-ttu-id="d76fe-119">About applications and application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-119">About applications and application packages</span></span>
<span data-ttu-id="d76fe-120">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-120">Within Azure Batch, an *application* refers to a set of versioned binaries that can be automatically downloaded to the compute nodes in your pool.</span></span> <span data-ttu-id="d76fe-121">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-121">An *application package* refers to a *specific set* of those binaries and represents a given *version* of the application.</span></span>

<span data-ttu-id="d76fe-122">![High-level diagram of applications and application packages][1]</span><span class="sxs-lookup"><span data-stu-id="d76fe-122">![High-level diagram of applications and application packages][1]</span></span>

### <a name="applications"></a><span data-ttu-id="d76fe-123">Applications</span><span class="sxs-lookup"><span data-stu-id="d76fe-123">Applications</span></span>
<span data-ttu-id="d76fe-124">An application in Batch contains one or more application packages and specifies configuration options for the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-124">An application in Batch contains one or more application packages and specifies configuration options for the application.</span></span> <span data-ttu-id="d76fe-125">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span><span class="sxs-lookup"><span data-stu-id="d76fe-125">For example, an application can specify the default application package version to install on compute nodes and whether its packages can be updated or deleted.</span></span>

### <a name="application-packages"></a><span data-ttu-id="d76fe-126">Application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-126">Application packages</span></span>
<span data-ttu-id="d76fe-127">An application package is a .zip file that contains the application binaries and supporting files that are required for execution by your tasks.</span><span class="sxs-lookup"><span data-stu-id="d76fe-127">An application package is a .zip file that contains the application binaries and supporting files that are required for execution by your tasks.</span></span> <span data-ttu-id="d76fe-128">Each application package represents a specific version of the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-128">Each application package represents a specific version of the application.</span></span>

<span data-ttu-id="d76fe-129">You can specify application packages at the pool and task level.</span><span class="sxs-lookup"><span data-stu-id="d76fe-129">You can specify application packages at the pool and task level.</span></span> <span data-ttu-id="d76fe-130">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span><span class="sxs-lookup"><span data-stu-id="d76fe-130">You can specify one or more of these packages and (optionally) a version when you create a pool or task.</span></span>

* <span data-ttu-id="d76fe-131">**Pool application packages** are deployed to *every* node in the pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-131">**Pool application packages** are deployed to *every* node in the pool.</span></span> <span data-ttu-id="d76fe-132">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span><span class="sxs-lookup"><span data-stu-id="d76fe-132">Applications are deployed when a node joins a pool, and when it is rebooted or reimaged.</span></span>
  
    <span data-ttu-id="d76fe-133">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span><span class="sxs-lookup"><span data-stu-id="d76fe-133">Pool application packages are appropriate when all nodes in a pool execute a job's tasks.</span></span> <span data-ttu-id="d76fe-134">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span><span class="sxs-lookup"><span data-stu-id="d76fe-134">You can specify one or more application packages when you create a pool, and you can add or update an existing pool's packages.</span></span> <span data-ttu-id="d76fe-135">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-135">If you update an existing pool's application packages, you must restart its nodes to install the new package.</span></span>
* <span data-ttu-id="d76fe-136">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span><span class="sxs-lookup"><span data-stu-id="d76fe-136">**Task application packages** are deployed only to a compute node scheduled to run a task, just before running the task's command line.</span></span> <span data-ttu-id="d76fe-137">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span><span class="sxs-lookup"><span data-stu-id="d76fe-137">If the specified application package and version is already on the node, it is not redeployed and the existing package is used.</span></span>
  
    <span data-ttu-id="d76fe-138">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span><span class="sxs-lookup"><span data-stu-id="d76fe-138">Task application packages are useful in shared-pool environments, where different jobs are run on one pool, and the pool is not deleted when a job is completed.</span></span> <span data-ttu-id="d76fe-139">If your job has less tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span><span class="sxs-lookup"><span data-stu-id="d76fe-139">If your job has less tasks than nodes in the pool, task application packages can minimize data transfer since your application is deployed only to the nodes that run tasks.</span></span>
  
    <span data-ttu-id="d76fe-140">Other scenarios that can benefit from task application packages are jobs that use a particularly large application, but for only a small number of tasks.</span><span class="sxs-lookup"><span data-stu-id="d76fe-140">Other scenarios that can benefit from task application packages are jobs that use a particularly large application, but for only a small number of tasks.</span></span> <span data-ttu-id="d76fe-141">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight.</span><span class="sxs-lookup"><span data-stu-id="d76fe-141">For example, a pre-processing stage or a merge task, where the pre-processing or merge application is heavyweight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d76fe-142">There are restrictions on the number of applications and application packages within a Batch account, as well as the maximum application package size.</span><span class="sxs-lookup"><span data-stu-id="d76fe-142">There are restrictions on the number of applications and application packages within a Batch account, as well as the maximum application package size.</span></span> <span data-ttu-id="d76fe-143">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span><span class="sxs-lookup"><span data-stu-id="d76fe-143">See [Quotas and limits for the Azure Batch service](batch-quota-limit.md) for details about these limits.</span></span>
> 
> 

### <a name="benefits-of-application-packages"></a><span data-ttu-id="d76fe-144">Benefits of application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-144">Benefits of application packages</span></span>
<span data-ttu-id="d76fe-145">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span><span class="sxs-lookup"><span data-stu-id="d76fe-145">Application packages can simplify the code in your Batch solution and lower the overhead required to manage the applications that your tasks run.</span></span>

<span data-ttu-id="d76fe-146">Your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-146">Your pool's start task doesn't have to specify a long list of individual resource files to install on the nodes.</span></span> <span data-ttu-id="d76fe-147">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-147">You don't have to manually manage multiple versions of your application files in Azure Storage, or on your nodes.</span></span> <span data-ttu-id="d76fe-148">And, you don't need to worry about generating [SAS URLs](../storage/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-148">And, you don't need to worry about generating [SAS URLs](../storage/storage-dotnet-shared-access-signature-part-1.md) to provide access to the files in your Storage account.</span></span> <span data-ttu-id="d76fe-149">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-149">Batch works in the background with Azure Storage to store application packages and deploy them to compute nodes.</span></span>

## <a name="upload-and-manage-applications"></a><span data-ttu-id="d76fe-150">Upload and manage applications</span><span class="sxs-lookup"><span data-stu-id="d76fe-150">Upload and manage applications</span></span>
<span data-ttu-id="d76fe-151">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-151">You can use the [Azure portal][portal] or the [Batch Management .NET](batch-management-dotnet.md) library to manage the application packages in your Batch account.</span></span> <span data-ttu-id="d76fe-152">In the next few sections, we first link a Storage account, then discuss adding applications and packages and managing them with the portal.</span><span class="sxs-lookup"><span data-stu-id="d76fe-152">In the next few sections, we first link a Storage account, then discuss adding applications and packages and managing them with the portal.</span></span>

### <a name="link-a-storage-account"></a><span data-ttu-id="d76fe-153">Link a Storage account</span><span class="sxs-lookup"><span data-stu-id="d76fe-153">Link a Storage account</span></span>
<span data-ttu-id="d76fe-154">To use application packages, you must first link an Azure Storage account to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-154">To use application packages, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="d76fe-155">If you have not yet configured a Storage account for your Batch account, the Azure portal will display a warning the first time you click the **Applications** tile in the **Batch account** blade.</span><span class="sxs-lookup"><span data-stu-id="d76fe-155">If you have not yet configured a Storage account for your Batch account, the Azure portal will display a warning the first time you click the **Applications** tile in the **Batch account** blade.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d76fe-156">Batch currently supports *only* the **General purpose** storage account type as described in step 5, [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d76fe-156">Batch currently supports *only* the **General purpose** storage account type as described in step 5, [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account), in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="d76fe-157">When you link an Azure Storage account to your Batch account, link *only* a **General purpose** storage account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-157">When you link an Azure Storage account to your Batch account, link *only* a **General purpose** storage account.</span></span>
> 
> 

<span data-ttu-id="d76fe-158">![No storage account configured warning in Azure portal][9]</span><span class="sxs-lookup"><span data-stu-id="d76fe-158">![No storage account configured warning in Azure portal][9]</span></span>

<span data-ttu-id="d76fe-159">The Batch service uses the associated Storage account for the storage and retrieval of application packages.</span><span class="sxs-lookup"><span data-stu-id="d76fe-159">The Batch service uses the associated Storage account for the storage and retrieval of application packages.</span></span> <span data-ttu-id="d76fe-160">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-160">After you've linked the two accounts, Batch can automatically deploy the packages stored in the linked Storage account to your compute nodes.</span></span> <span data-ttu-id="d76fe-161">Click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade to link a storage account to your Batch account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-161">Click **Storage account settings** on the **Warning** blade, and then click **Storage Account** on the **Storage Account** blade to link a storage account to your Batch account.</span></span>

<span data-ttu-id="d76fe-162">![Choose storage account blade in Azure portal][10]</span><span class="sxs-lookup"><span data-stu-id="d76fe-162">![Choose storage account blade in Azure portal][10]</span></span>

<span data-ttu-id="d76fe-163">We recommend that you create a storage account *specifically* for use with your Batch account, and select it here.</span><span class="sxs-lookup"><span data-stu-id="d76fe-163">We recommend that you create a storage account *specifically* for use with your Batch account, and select it here.</span></span> <span data-ttu-id="d76fe-164">For details about how to create a storage account, see "Create a storage account" in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="d76fe-164">For details about how to create a storage account, see "Create a storage account" in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span> <span data-ttu-id="d76fe-165">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span><span class="sxs-lookup"><span data-stu-id="d76fe-165">After you've created a Storage account, you can then link it to your Batch account by using the **Storage Account** blade.</span></span>

> [!WARNING]
> <span data-ttu-id="d76fe-166">Because Batch uses Azure Storage to store your application packages, you are [charged as normal][storage_pricing] for the block blob data.</span><span class="sxs-lookup"><span data-stu-id="d76fe-166">Because Batch uses Azure Storage to store your application packages, you are [charged as normal][storage_pricing] for the block blob data.</span></span> <span data-ttu-id="d76fe-167">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize cost.</span><span class="sxs-lookup"><span data-stu-id="d76fe-167">Be sure to consider the size and number of your application packages, and periodically remove deprecated packages to minimize cost.</span></span>
> 
> 

### <a name="view-current-applications"></a><span data-ttu-id="d76fe-168">View current applications</span><span class="sxs-lookup"><span data-stu-id="d76fe-168">View current applications</span></span>
<span data-ttu-id="d76fe-169">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span><span class="sxs-lookup"><span data-stu-id="d76fe-169">To view the applications in your Batch account, click the **Applications** menu item in the left menu while viewing the **Batch account** blade.</span></span>

<span data-ttu-id="d76fe-170">![Applications tile][2]</span><span class="sxs-lookup"><span data-stu-id="d76fe-170">![Applications tile][2]</span></span>

<span data-ttu-id="d76fe-171">This opens the **Applications** blade:</span><span class="sxs-lookup"><span data-stu-id="d76fe-171">This opens the **Applications** blade:</span></span>

<span data-ttu-id="d76fe-172">![List applications][3]</span><span class="sxs-lookup"><span data-stu-id="d76fe-172">![List applications][3]</span></span>

<span data-ttu-id="d76fe-173">The **Applications** blade displays the ID of each application in your account and the following properties:</span><span class="sxs-lookup"><span data-stu-id="d76fe-173">The **Applications** blade displays the ID of each application in your account and the following properties:</span></span>

* <span data-ttu-id="d76fe-174">**Packages**--The number of versions associated with this application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-174">**Packages**--The number of versions associated with this application.</span></span>
* <span data-ttu-id="d76fe-175">**Default version**--The version that will be installed if you do not specify a version when you set the application for a pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-175">**Default version**--The version that will be installed if you do not specify a version when you set the application for a pool.</span></span> <span data-ttu-id="d76fe-176">This setting is optional.</span><span class="sxs-lookup"><span data-stu-id="d76fe-176">This setting is optional.</span></span>
* <span data-ttu-id="d76fe-177">**Allow updates**--The value that specifies whether package updates, deletions, and additions are allowed.</span><span class="sxs-lookup"><span data-stu-id="d76fe-177">**Allow updates**--The value that specifies whether package updates, deletions, and additions are allowed.</span></span> <span data-ttu-id="d76fe-178">If this is set to **No**, package updates and deletions are disabled for the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-178">If this is set to **No**, package updates and deletions are disabled for the application.</span></span> <span data-ttu-id="d76fe-179">Only new application package versions can be added.</span><span class="sxs-lookup"><span data-stu-id="d76fe-179">Only new application package versions can be added.</span></span> <span data-ttu-id="d76fe-180">The default is **Yes**.</span><span class="sxs-lookup"><span data-stu-id="d76fe-180">The default is **Yes**.</span></span>

### <a name="view-application-details"></a><span data-ttu-id="d76fe-181">View application details</span><span class="sxs-lookup"><span data-stu-id="d76fe-181">View application details</span></span>
<span data-ttu-id="d76fe-182">Click an application in the **Applications** blade to open the blade that includes the details for that application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-182">Click an application in the **Applications** blade to open the blade that includes the details for that application.</span></span>

<span data-ttu-id="d76fe-183">![Application details][4]</span><span class="sxs-lookup"><span data-stu-id="d76fe-183">![Application details][4]</span></span>

<span data-ttu-id="d76fe-184">In the application details blade, you can configure the following settings for your application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-184">In the application details blade, you can configure the following settings for your application.</span></span>

* <span data-ttu-id="d76fe-185">**Allow updates**--Specify whether its application packages can be updated or deleted.</span><span class="sxs-lookup"><span data-stu-id="d76fe-185">**Allow updates**--Specify whether its application packages can be updated or deleted.</span></span> <span data-ttu-id="d76fe-186">See "Update or Delete an application package" later in this article.</span><span class="sxs-lookup"><span data-stu-id="d76fe-186">See "Update or Delete an application package" later in this article.</span></span>
* <span data-ttu-id="d76fe-187">**Default version**--Specify a default application package to deploy to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-187">**Default version**--Specify a default application package to deploy to compute nodes.</span></span>
* <span data-ttu-id="d76fe-188">**Display name**--Specify a "friendly" name that your Batch solution can use when it displays information about the application, such as in the UI of a service that you provide your customers through Batch.</span><span class="sxs-lookup"><span data-stu-id="d76fe-188">**Display name**--Specify a "friendly" name that your Batch solution can use when it displays information about the application, such as in the UI of a service that you provide your customers through Batch.</span></span>

### <a name="add-a-new-application"></a><span data-ttu-id="d76fe-189">Add a new application</span><span class="sxs-lookup"><span data-stu-id="d76fe-189">Add a new application</span></span>
<span data-ttu-id="d76fe-190">To create a new application, add an application package and specify a new, unique application ID.</span><span class="sxs-lookup"><span data-stu-id="d76fe-190">To create a new application, add an application package and specify a new, unique application ID.</span></span> <span data-ttu-id="d76fe-191">The first application package that you add with the new application ID will also create the new application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-191">The first application package that you add with the new application ID will also create the new application.</span></span>

<span data-ttu-id="d76fe-192">Click **Add** on the **Applications** blade to open the **New application** blade.</span><span class="sxs-lookup"><span data-stu-id="d76fe-192">Click **Add** on the **Applications** blade to open the **New application** blade.</span></span>

<span data-ttu-id="d76fe-193">![New application blade in Azure portal][5]</span><span class="sxs-lookup"><span data-stu-id="d76fe-193">![New application blade in Azure portal][5]</span></span>

<span data-ttu-id="d76fe-194">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-194">The **New application** blade provides the following fields to specify the settings of your new application and application package.</span></span>

<span data-ttu-id="d76fe-195">**Application id**</span><span class="sxs-lookup"><span data-stu-id="d76fe-195">**Application id**</span></span>

<span data-ttu-id="d76fe-196">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules:</span><span class="sxs-lookup"><span data-stu-id="d76fe-196">This field specifies the ID of your new application, which is subject to the standard Azure Batch ID validation rules:</span></span>

* <span data-ttu-id="d76fe-197">Can contain any combination of alphanumeric characters, including hyphens and underscores.</span><span class="sxs-lookup"><span data-stu-id="d76fe-197">Can contain any combination of alphanumeric characters, including hyphens and underscores.</span></span>
* <span data-ttu-id="d76fe-198">Cannot contain more than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="d76fe-198">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="d76fe-199">Must be unique within the Batch account.</span><span class="sxs-lookup"><span data-stu-id="d76fe-199">Must be unique within the Batch account.</span></span>
* <span data-ttu-id="d76fe-200">Is case preserving and case insensitive.</span><span class="sxs-lookup"><span data-stu-id="d76fe-200">Is case preserving and case insensitive.</span></span>

<span data-ttu-id="d76fe-201">**Version**</span><span class="sxs-lookup"><span data-stu-id="d76fe-201">**Version**</span></span>

<span data-ttu-id="d76fe-202">Specifies the version of the application package you are uploading.</span><span class="sxs-lookup"><span data-stu-id="d76fe-202">Specifies the version of the application package you are uploading.</span></span> <span data-ttu-id="d76fe-203">Version strings are subject to the following validation rules:</span><span class="sxs-lookup"><span data-stu-id="d76fe-203">Version strings are subject to the following validation rules:</span></span>

* <span data-ttu-id="d76fe-204">Can contain any combination of alphanumeric characters, including hyphens, underscores, and periods.</span><span class="sxs-lookup"><span data-stu-id="d76fe-204">Can contain any combination of alphanumeric characters, including hyphens, underscores, and periods.</span></span>
* <span data-ttu-id="d76fe-205">Cannot contain more than 64 characters.</span><span class="sxs-lookup"><span data-stu-id="d76fe-205">Cannot contain more than 64 characters.</span></span>
* <span data-ttu-id="d76fe-206">Must be unique within the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-206">Must be unique within the application.</span></span>
* <span data-ttu-id="d76fe-207">Case preserving, and case insensitive.</span><span class="sxs-lookup"><span data-stu-id="d76fe-207">Case preserving, and case insensitive.</span></span>

<span data-ttu-id="d76fe-208">**Application package**</span><span class="sxs-lookup"><span data-stu-id="d76fe-208">**Application package**</span></span>

<span data-ttu-id="d76fe-209">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-209">This field specifies the .zip file that contains the application binaries and supporting files that are required to execute the application.</span></span> <span data-ttu-id="d76fe-210">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span><span class="sxs-lookup"><span data-stu-id="d76fe-210">Click the **Select a file** box or the folder icon to browse to and select a .zip file that contains your application's files.</span></span>

<span data-ttu-id="d76fe-211">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d76fe-211">After you've selected a file, click **OK** to begin the upload to Azure Storage.</span></span> <span data-ttu-id="d76fe-212">When the upload operation is complete, you will be notified and the blade will close.</span><span class="sxs-lookup"><span data-stu-id="d76fe-212">When the upload operation is complete, you will be notified and the blade will close.</span></span> <span data-ttu-id="d76fe-213">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span><span class="sxs-lookup"><span data-stu-id="d76fe-213">Depending on the size of the file that you are uploading and the speed of your network connection, this operation may take some time.</span></span>

> [!WARNING]
> <span data-ttu-id="d76fe-214">Do not close the **New application** blade before the upload operation is complete.</span><span class="sxs-lookup"><span data-stu-id="d76fe-214">Do not close the **New application** blade before the upload operation is complete.</span></span> <span data-ttu-id="d76fe-215">Doing so will stop the upload process.</span><span class="sxs-lookup"><span data-stu-id="d76fe-215">Doing so will stop the upload process.</span></span>
> 
> 

### <a name="add-a-new-application-package"></a><span data-ttu-id="d76fe-216">Add a new application package</span><span class="sxs-lookup"><span data-stu-id="d76fe-216">Add a new application package</span></span>
<span data-ttu-id="d76fe-217">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span><span class="sxs-lookup"><span data-stu-id="d76fe-217">To add a new application package version for an existing application, select an application in the **Applications** blade, click **Packages**, then click **Add** to open the **Add package** blade.</span></span>

<span data-ttu-id="d76fe-218">![Add application package blade in Azure portal][8]</span><span class="sxs-lookup"><span data-stu-id="d76fe-218">![Add application package blade in Azure portal][8]</span></span>

<span data-ttu-id="d76fe-219">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span><span class="sxs-lookup"><span data-stu-id="d76fe-219">As you can see, the fields match those of the **New application** blade, but the **Application id** box is disabled.</span></span> <span data-ttu-id="d76fe-220">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-220">As you did for the new application, specify the **Version** for your new package, browse to your **Application package** .zip file, then click **OK** to upload the package.</span></span>

### <a name="update-or-delete-an-application-package"></a><span data-ttu-id="d76fe-221">Update or delete an application package</span><span class="sxs-lookup"><span data-stu-id="d76fe-221">Update or delete an application package</span></span>
<span data-ttu-id="d76fe-222">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span><span class="sxs-lookup"><span data-stu-id="d76fe-222">To update or delete an existing application package, open the details blade for the application, click **Packages** to open the **Packages** blade, click the **ellipsis** in the row of the application package that you want to modify, and select the action that you want to perform.</span></span>

<span data-ttu-id="d76fe-223">![Update or delete package in Azure portal][7]</span><span class="sxs-lookup"><span data-stu-id="d76fe-223">![Update or delete package in Azure portal][7]</span></span>

<span data-ttu-id="d76fe-224">**Update**</span><span class="sxs-lookup"><span data-stu-id="d76fe-224">**Update**</span></span>

<span data-ttu-id="d76fe-225">When you click **Update**, the *Update package* blade is displayed.</span><span class="sxs-lookup"><span data-stu-id="d76fe-225">When you click **Update**, the *Update package* blade is displayed.</span></span> <span data-ttu-id="d76fe-226">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span><span class="sxs-lookup"><span data-stu-id="d76fe-226">This blade is similar to the *New application package* blade, however only the package selection field is enabled, allowing you to specify a new ZIP file to upload.</span></span>

<span data-ttu-id="d76fe-227">![Update package blade in Azure portal][11]</span><span class="sxs-lookup"><span data-stu-id="d76fe-227">![Update package blade in Azure portal][11]</span></span>

<span data-ttu-id="d76fe-228">**Delete**</span><span class="sxs-lookup"><span data-stu-id="d76fe-228">**Delete**</span></span>

<span data-ttu-id="d76fe-229">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d76fe-229">When you click **Delete**, you are asked to confirm the deletion of the package version, and Batch deletes the package from Azure Storage.</span></span> <span data-ttu-id="d76fe-230">If you delete the default version of an application, the **Default version** setting is removed for the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-230">If you delete the default version of an application, the **Default version** setting is removed for the application.</span></span>

<span data-ttu-id="d76fe-231">![Delete application ][12]</span><span class="sxs-lookup"><span data-stu-id="d76fe-231">![Delete application ][12]</span></span>

## <a name="install-applications-on-compute-nodes"></a><span data-ttu-id="d76fe-232">Install applications on compute nodes</span><span class="sxs-lookup"><span data-stu-id="d76fe-232">Install applications on compute nodes</span></span>
<span data-ttu-id="d76fe-233">Now that you've seen how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span><span class="sxs-lookup"><span data-stu-id="d76fe-233">Now that you've seen how to manage application packages with the Azure portal, we can discuss how to deploy them to compute nodes and run them with Batch tasks.</span></span>

### <a name="install-pool-application-packages"></a><span data-ttu-id="d76fe-234">Install pool application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-234">Install pool application packages</span></span>
<span data-ttu-id="d76fe-235">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-235">To install an application package on all compute nodes in a pool, specify one or more application package *references* for the pool.</span></span> <span data-ttu-id="d76fe-236">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span><span class="sxs-lookup"><span data-stu-id="d76fe-236">The application packages that you specify for a pool are installed on each compute node when that node joins the pool, and when the node is rebooted or reimaged.</span></span>

<span data-ttu-id="d76fe-237">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-237">In Batch .NET, specify one or more [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref] when you create a new pool, or for an existing pool.</span></span> <span data-ttu-id="d76fe-238">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-238">The [ApplicationPackageReference][net_pkgref] class specifies an application ID and version to install on a pool's compute nodes.</span></span>

```csharp
// Create the unbound CloudPool
CloudPool myCloudPool =
    batchClient.PoolOperations.CreatePool(
        poolId: "myPool",
        targetDedicated: "1",
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Specify the application and version to install on the compute nodes
myCloudPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "litware",
        Version = "1.1001.2b" }
};

// Commit the pool so that it's created in the Batch service. As the nodes join
// the pool, the specified application package will be installed on each.
await myCloudPool.CommitAsync();
```

> [!IMPORTANT]
> <span data-ttu-id="d76fe-239">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks will be scheduled for execution on that node.</span><span class="sxs-lookup"><span data-stu-id="d76fe-239">If an application package deployment fails for any reason, the Batch service marks the node [unusable][net_nodestate], and no tasks will be scheduled for execution on that node.</span></span> <span data-ttu-id="d76fe-240">In this case, you should **restart** the node to reinitiate the package deployment.</span><span class="sxs-lookup"><span data-stu-id="d76fe-240">In this case, you should **restart** the node to reinitiate the package deployment.</span></span> <span data-ttu-id="d76fe-241">Restarting the node will also enable task scheduling again on the node.</span><span class="sxs-lookup"><span data-stu-id="d76fe-241">Restarting the node will also enable task scheduling again on the node.</span></span>
> 
> 

### <a name="install-task-application-packages"></a><span data-ttu-id="d76fe-242">Install task application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-242">Install task application packages</span></span>
<span data-ttu-id="d76fe-243">Similar to a pool, you specify application package *references* for a task.</span><span class="sxs-lookup"><span data-stu-id="d76fe-243">Similar to a pool, you specify application package *references* for a task.</span></span> <span data-ttu-id="d76fe-244">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span><span class="sxs-lookup"><span data-stu-id="d76fe-244">When a task is scheduled to run on a node, the package is downloaded and extracted just before the task's command line is executed.</span></span> <span data-ttu-id="d76fe-245">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span><span class="sxs-lookup"><span data-stu-id="d76fe-245">If a specified package and version is already installed on the node, the package is not downloaded and the existing package is used.</span></span>

<span data-ttu-id="d76fe-246">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span><span class="sxs-lookup"><span data-stu-id="d76fe-246">To install a task application package, configure the task's [CloudTask][net_cloudtask].[ApplicationPackageReferences][net_cloudtask_pkgref] property:</span></span>

```csharp
CloudTask task =
    new CloudTask(
        "litwaretask001",
        "cmd /c %AZ_BATCH_APP_PACKAGE_LITWARE%\\litware.exe -args -here");

task.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference
    {
        ApplicationId = "litware",
        Version = "1.1001.2b"
    }
};
```

## <a name="execute-the-installed-applications"></a><span data-ttu-id="d76fe-247">Execute the installed applications</span><span class="sxs-lookup"><span data-stu-id="d76fe-247">Execute the installed applications</span></span>
<span data-ttu-id="d76fe-248">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span><span class="sxs-lookup"><span data-stu-id="d76fe-248">The packages that you've specified for a pool or task are downloaded and extracted to a named directory within the `AZ_BATCH_ROOT_DIR` of the node.</span></span> <span data-ttu-id="d76fe-249">Batch also creates an environment variable that contains the path to the named directory.</span><span class="sxs-lookup"><span data-stu-id="d76fe-249">Batch also creates an environment variable that contains the path to the named directory.</span></span> <span data-ttu-id="d76fe-250">Your task command lines use this environment variable when referencing the application on the node.</span><span class="sxs-lookup"><span data-stu-id="d76fe-250">Your task command lines use this environment variable when referencing the application on the node.</span></span> <span data-ttu-id="d76fe-251">The variable is in the following format:</span><span class="sxs-lookup"><span data-stu-id="d76fe-251">The variable is in the following format:</span></span>

`AZ_BATCH_APP_PACKAGE_APPLICATIONID#version`

<span data-ttu-id="d76fe-252">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span><span class="sxs-lookup"><span data-stu-id="d76fe-252">`APPLICATIONID` and `version` are values that correspond to the application and package version you've specified for deployment.</span></span> <span data-ttu-id="d76fe-253">For example, if you specifed that version 2.7 of application *blender* should be installed, your task command lines would use this environment variable to access its files:</span><span class="sxs-lookup"><span data-stu-id="d76fe-253">For example, if you specifed that version 2.7 of application *blender* should be installed, your task command lines would use this environment variable to access its files:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER#2.7`

<span data-ttu-id="d76fe-254">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span><span class="sxs-lookup"><span data-stu-id="d76fe-254">When you upload an application package, you can specify a default version to deploy to your compute nodes.</span></span> <span data-ttu-id="d76fe-255">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span><span class="sxs-lookup"><span data-stu-id="d76fe-255">If you have specified a default version for an application, you can omit the version suffix when you reference the application.</span></span> <span data-ttu-id="d76fe-256">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span><span class="sxs-lookup"><span data-stu-id="d76fe-256">You can specify the default application version in the Azure portal, on the Applications blade, as shown in [Upload and manage applications](#upload-and-manage-applications).</span></span>

<span data-ttu-id="d76fe-257">For example, if you set "2.7" as the default version for application *blender*, your tasks can reference the following environment variable and they will execute version 2.7:</span><span class="sxs-lookup"><span data-stu-id="d76fe-257">For example, if you set "2.7" as the default version for application *blender*, your tasks can reference the following environment variable and they will execute version 2.7:</span></span>

`AZ_BATCH_APP_PACKAGE_BLENDER`

<span data-ttu-id="d76fe-258">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span><span class="sxs-lookup"><span data-stu-id="d76fe-258">The following code snippet shows an example task command line that launches the default version of the *blender* application:</span></span>

```csharp
string taskId = "blendertask01";
string commandLine =
    @"cmd /c %AZ_BATCH_APP_PACKAGE_BLENDER%\blender.exe -args -here";
CloudTask blenderTask = new CloudTask(taskId, commandLine);
```

> [!TIP]
> <span data-ttu-id="d76fe-259">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span><span class="sxs-lookup"><span data-stu-id="d76fe-259">See [Environment settings for tasks](batch-api-basics.md#environment-settings-for-tasks) in the [Batch feature overview](batch-api-basics.md) for more information about compute node environment settings.</span></span>
> 
> 

## <a name="update-a-pools-application-packages"></a><span data-ttu-id="d76fe-260">Update a pool's application packages</span><span class="sxs-lookup"><span data-stu-id="d76fe-260">Update a pool's application packages</span></span>
<span data-ttu-id="d76fe-261">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span><span class="sxs-lookup"><span data-stu-id="d76fe-261">If an existing pool has already been configured with an application package, you can specify a new package for the pool.</span></span> <span data-ttu-id="d76fe-262">If you specify a new package reference for a pool, the following apply:</span><span class="sxs-lookup"><span data-stu-id="d76fe-262">If you specify a new package reference for a pool, the following apply:</span></span>

* <span data-ttu-id="d76fe-263">All new nodes that join the pool and any existing node that is rebooted or reimaged will install the newly specified package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-263">All new nodes that join the pool and any existing node that is rebooted or reimaged will install the newly specified package.</span></span>
* <span data-ttu-id="d76fe-264">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-264">Compute nodes that are already in the pool when you update the package references do not automatically install the new application package.</span></span> <span data-ttu-id="d76fe-265">These compute nodes must be rebooted or reimaged to receive the new package.</span><span class="sxs-lookup"><span data-stu-id="d76fe-265">These compute nodes must be rebooted or reimaged to receive the new package.</span></span>
* <span data-ttu-id="d76fe-266">When a new package is deployed, the created environment variables reflect the new application package references.</span><span class="sxs-lookup"><span data-stu-id="d76fe-266">When a new package is deployed, the created environment variables reflect the new application package references.</span></span>

<span data-ttu-id="d76fe-267">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span><span class="sxs-lookup"><span data-stu-id="d76fe-267">In this example, the existing pool has version 2.7 of the *blender* application configured as one of its [CloudPool][net_cloudpool].[ApplicationPackageReferences][net_cloudpool_pkgref].</span></span> <span data-ttu-id="d76fe-268">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span><span class="sxs-lookup"><span data-stu-id="d76fe-268">To update the pool's nodes with version 2.76b, specify a new [ApplicationPackageReference][net_pkgref] with the new version, and commit the change.</span></span>

```csharp
string newVersion = "2.76b";
CloudPool boundPool = await batchClient.PoolOperations.GetPoolAsync("myPool");
boundPool.ApplicationPackageReferences = new List<ApplicationPackageReference>
{
    new ApplicationPackageReference {
        ApplicationId = "blender",
        Version = newVersion }
};
await boundPool.CommitAsync();
```

<span data-ttu-id="d76fe-269">Now that the new version has been configured, any *new* node that joins the pool will have version 2.76b deployed to it.</span><span class="sxs-lookup"><span data-stu-id="d76fe-269">Now that the new version has been configured, any *new* node that joins the pool will have version 2.76b deployed to it.</span></span> <span data-ttu-id="d76fe-270">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span><span class="sxs-lookup"><span data-stu-id="d76fe-270">To install 2.76b on the nodes that are *already* in the pool, reboot or reimage them.</span></span> <span data-ttu-id="d76fe-271">Note that rebooted nodes will retain the files from previous package deployments.</span><span class="sxs-lookup"><span data-stu-id="d76fe-271">Note that rebooted nodes will retain the files from previous package deployments.</span></span>

## <a name="list-the-applications-in-a-batch-account"></a><span data-ttu-id="d76fe-272">List the applications in a Batch account</span><span class="sxs-lookup"><span data-stu-id="d76fe-272">List the applications in a Batch account</span></span>
<span data-ttu-id="d76fe-273">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span><span class="sxs-lookup"><span data-stu-id="d76fe-273">You can list the applications and their packages in a Batch account by using the [ApplicationOperations][net_appops].[ListApplicationSummaries][net_appops_listappsummaries] method.</span></span>

```csharp
// List the applications and their application packages in the Batch account.
List<ApplicationSummary> applications = await batchClient.ApplicationOperations.ListApplicationSummaries().ToListAsync();
foreach (ApplicationSummary app in applications)
{
    Console.WriteLine("ID: {0} | Display Name: {1}", app.Id, app.DisplayName);

    foreach (string version in app.Versions)
    {
        Console.WriteLine("  {0}", version);
    }
}
```

## <a name="wrap-up"></a><span data-ttu-id="d76fe-274">Wrap up</span><span class="sxs-lookup"><span data-stu-id="d76fe-274">Wrap up</span></span>
<span data-ttu-id="d76fe-275">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span><span class="sxs-lookup"><span data-stu-id="d76fe-275">With application packages, you can help your customers select the applications for their jobs and specify the exact version to use when processing jobs with your Batch-enabled service.</span></span> <span data-ttu-id="d76fe-276">You might also provide the ability for your customers to upload and track their own applications in your service.</span><span class="sxs-lookup"><span data-stu-id="d76fe-276">You might also provide the ability for your customers to upload and track their own applications in your service.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d76fe-277">Next steps</span><span class="sxs-lookup"><span data-stu-id="d76fe-277">Next steps</span></span>
* <span data-ttu-id="d76fe-278">The [Batch REST API][api_rest] also provides support to work with application packages.</span><span class="sxs-lookup"><span data-stu-id="d76fe-278">The [Batch REST API][api_rest] also provides support to work with application packages.</span></span> <span data-ttu-id="d76fe-279">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span><span class="sxs-lookup"><span data-stu-id="d76fe-279">For example, see the [applicationPackageReferences][rest_add_pool_with_packages] element in [Add a pool to an account][rest_add_pool] for information about how to specify packages to install by using the REST API.</span></span> <span data-ttu-id="d76fe-280">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span><span class="sxs-lookup"><span data-stu-id="d76fe-280">See [Applications][rest_applications] for details about how to obtain application information by using the Batch REST API.</span></span>
* <span data-ttu-id="d76fe-281">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="d76fe-281">Learn how to programmatically [manage Azure Batch accounts and quotas with Batch Management .NET](batch-management-dotnet.md).</span></span> <span data-ttu-id="d76fe-282">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span><span class="sxs-lookup"><span data-stu-id="d76fe-282">The [Batch Management .NET][api_net_mgmt] library can enable account creation and deletion features for your Batch application or service.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_mgmt_nuget]: https://www.nuget.org/packages/Microsoft.Azure.Management.Batch/
[github_samples]: https://github.com/Azure/azure-batch-samples
[storage_pricing]: https://azure.microsoft.com/pricing/details/storage/
[net_appops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.aspx
[net_appops_listappsummaries]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationoperations.listapplicationsummaries.aspx
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_cloudpool_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.applicationpackagereferences.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.aspx
[net_cloudtask_pkgref]: https://msdn.microsoft.com/library/microsoft.azure.batch.cloudtask.applicationpackagereferences.aspx
[net_nodestate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.state.aspx
[net_pkgref]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.applicationpackagereference.aspx
[portal]: https://portal.azure.com
[rest_applications]: https://msdn.microsoft.com/library/azure/mt643945.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_pool_with_packages]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_apkgreference

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_01.png "Application packages high-level diagram"
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_02.png "Applications tile in Azure portal"
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_03.png "Applications blade in Azure portal"
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_04.png "Application details blade in Azure portal"
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_05.png "New application blade in Azure portal"
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_07.png "Update or delete packages drop-down in Azure portal"
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_08.png "New application package blade in Azure portal"
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_09.png "No linked Storage account alert"
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_10.png "Choose storage account blade in Azure portal"
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_11.png "Update package blade in Azure portal"
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-application-packages/app_pkg_12.png "Delete package confirmation dialog in Azure portal"











