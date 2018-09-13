---
title: Azure file share for Azure Batch pools | Microsoft Docs
description: How to mount an Azure Files share from compute nodes in a Linux or Windows pool in Azure Batch.
services: batch
documentationcenter: ''
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/24/2018
ms.author: danlep
ms.custom: ''
ms.openlocfilehash: 88d7c0d033d7b517a396df27468de8be7ae20be9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856951"
---
# <a name="use-an-azure-file-share-with-a-batch-pool"></a><span data-ttu-id="0f10a-103">Use an Azure file share with a Batch pool</span><span class="sxs-lookup"><span data-stu-id="0f10a-103">Use an Azure file share with a Batch pool</span></span>

<span data-ttu-id="0f10a-104">[Azure Files](../storage/files/storage-files-introduction.md) offers fully managed file shares in the cloud that are accessible via the Server Message Block (SMB) protocol.</span><span class="sxs-lookup"><span data-stu-id="0f10a-104">[Azure Files](../storage/files/storage-files-introduction.md) offers fully managed file shares in the cloud that are accessible via the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="0f10a-105">This article provides information and code examples for mounting and using an Azure file share on pool compute nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-105">This article provides information and code examples for mounting and using an Azure file share on pool compute nodes.</span></span> <span data-ttu-id="0f10a-106">The code examples use the Batch .NET and Python SDKs, but you can perform similar operations using other Batch SDKs and tools.</span><span class="sxs-lookup"><span data-stu-id="0f10a-106">The code examples use the Batch .NET and Python SDKs, but you can perform similar operations using other Batch SDKs and tools.</span></span>

<span data-ttu-id="0f10a-107">Batch provides native API support for using Azure Storage blobs to read and write data.</span><span class="sxs-lookup"><span data-stu-id="0f10a-107">Batch provides native API support for using Azure Storage blobs to read and write data.</span></span> <span data-ttu-id="0f10a-108">However, in some cases you might want to access an Azure file share from your pool compute nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-108">However, in some cases you might want to access an Azure file share from your pool compute nodes.</span></span> <span data-ttu-id="0f10a-109">For example, you have a legacy workload that depends on an SMB file share, or your tasks need to access shared data or produce shared output.</span><span class="sxs-lookup"><span data-stu-id="0f10a-109">For example, you have a legacy workload that depends on an SMB file share, or your tasks need to access shared data or produce shared output.</span></span> 

## <a name="considerations-for-use-with-batch"></a><span data-ttu-id="0f10a-110">Considerations for use with Batch</span><span class="sxs-lookup"><span data-stu-id="0f10a-110">Considerations for use with Batch</span></span>

* <span data-ttu-id="0f10a-111">Consider using an Azure file share when you have pools that run a relatively low number of parallel tasks.</span><span class="sxs-lookup"><span data-stu-id="0f10a-111">Consider using an Azure file share when you have pools that run a relatively low number of parallel tasks.</span></span> <span data-ttu-id="0f10a-112">Review the [performance and scale targets](../storage/files/storage-files-scale-targets.md) to determine if Azure Files (which uses an Azure Storage account) should be used, given your expected pool size and number of asset files.</span><span class="sxs-lookup"><span data-stu-id="0f10a-112">Review the [performance and scale targets](../storage/files/storage-files-scale-targets.md) to determine if Azure Files (which uses an Azure Storage account) should be used, given your expected pool size and number of asset files.</span></span> 

* <span data-ttu-id="0f10a-113">Azure file shares are [cost-efficient](https://azure.microsoft.com/pricing/details/storage/files/) and can be configured with data replication to another region so are globally redundant.</span><span class="sxs-lookup"><span data-stu-id="0f10a-113">Azure file shares are [cost-efficient](https://azure.microsoft.com/pricing/details/storage/files/) and can be configured with data replication to another region so are globally redundant.</span></span> 

* <span data-ttu-id="0f10a-114">You can mount an Azure file share concurrently from an on-premises computer.</span><span class="sxs-lookup"><span data-stu-id="0f10a-114">You can mount an Azure file share concurrently from an on-premises computer.</span></span>

* <span data-ttu-id="0f10a-115">See also the general [planning considerations](../storage/files/storage-files-planning.md) for Azure file shares.</span><span class="sxs-lookup"><span data-stu-id="0f10a-115">See also the general [planning considerations](../storage/files/storage-files-planning.md) for Azure file shares.</span></span>


## <a name="create-a-file-share"></a><span data-ttu-id="0f10a-116">Create a file share</span><span class="sxs-lookup"><span data-stu-id="0f10a-116">Create a file share</span></span>

<span data-ttu-id="0f10a-117">[Create a file share](../storage/files/storage-how-to-create-file-share.md) in a storage account that is linked to your Batch account, or in a separate storage account.</span><span class="sxs-lookup"><span data-stu-id="0f10a-117">[Create a file share](../storage/files/storage-how-to-create-file-share.md) in a storage account that is linked to your Batch account, or in a separate storage account.</span></span>

## <a name="mount-a-share-on-a-windows-pool"></a><span data-ttu-id="0f10a-118">Mount a share on a Windows pool</span><span class="sxs-lookup"><span data-stu-id="0f10a-118">Mount a share on a Windows pool</span></span>

<span data-ttu-id="0f10a-119">This section provides steps and code examples to mount and use an Azure file share on a pool of Windows nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-119">This section provides steps and code examples to mount and use an Azure file share on a pool of Windows nodes.</span></span> <span data-ttu-id="0f10a-120">For additional background, see the [documentation](../storage/files/storage-how-to-use-files-windows.md) for mounting an Azure file share on Windows.</span><span class="sxs-lookup"><span data-stu-id="0f10a-120">For additional background, see the [documentation](../storage/files/storage-how-to-use-files-windows.md) for mounting an Azure file share on Windows.</span></span> 

<span data-ttu-id="0f10a-121">In Batch, you need to mount the share each time a task is run on a Windows node.</span><span class="sxs-lookup"><span data-stu-id="0f10a-121">In Batch, you need to mount the share each time a task is run on a Windows node.</span></span> <span data-ttu-id="0f10a-122">Currently, it's not possible to persist the network connection between tasks on Windows nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-122">Currently, it's not possible to persist the network connection between tasks on Windows nodes.</span></span>

<span data-ttu-id="0f10a-123">For example, include a `net use` command to mount the file share as part of each task command line.</span><span class="sxs-lookup"><span data-stu-id="0f10a-123">For example, include a `net use` command to mount the file share as part of each task command line.</span></span> <span data-ttu-id="0f10a-124">To mount the file share, the following credentials are needed:</span><span class="sxs-lookup"><span data-stu-id="0f10a-124">To mount the file share, the following credentials are needed:</span></span>

* <span data-ttu-id="0f10a-125">**User name**: AZURE\\\<storageaccountname\>, for example, AZURE\\*mystorageaccountname*</span><span class="sxs-lookup"><span data-stu-id="0f10a-125">**User name**: AZURE\\\<storageaccountname\>, for example, AZURE\\*mystorageaccountname*</span></span>
* <span data-ttu-id="0f10a-126">**Password**: <StorageAccountKeyWhichEnds in==>, for example, *XXXXXXXXXXXXXXXXXXXXX==*</span><span class="sxs-lookup"><span data-stu-id="0f10a-126">**Password**: <StorageAccountKeyWhichEnds in==>, for example, *XXXXXXXXXXXXXXXXXXXXX==*</span></span>

<span data-ttu-id="0f10a-127">The following command mounts a file share *myfileshare* in storage account *mystorageaccountname* as the *S:* drive:</span><span class="sxs-lookup"><span data-stu-id="0f10a-127">The following command mounts a file share *myfileshare* in storage account *mystorageaccountname* as the *S:* drive:</span></span>

```
net use S: \\mystorageaccountname.file.core.windows.net\myfileshare /user:AZURE\mystorageaccountname XXXXXXXXXXXXXXXXXXXXX==
```

<span data-ttu-id="0f10a-128">For simplicity, the examples here pass the credentials directly in text.</span><span class="sxs-lookup"><span data-stu-id="0f10a-128">For simplicity, the examples here pass the credentials directly in text.</span></span> <span data-ttu-id="0f10a-129">In practice, we strongly recommend managing the credentials using environment variables, certificates, or a solution such as Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0f10a-129">In practice, we strongly recommend managing the credentials using environment variables, certificates, or a solution such as Azure Key Vault.</span></span>

<span data-ttu-id="0f10a-130">To simplify the mount operation, optionally persist the credentials on the nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-130">To simplify the mount operation, optionally persist the credentials on the nodes.</span></span> <span data-ttu-id="0f10a-131">Then, you can mount the share without credentials.</span><span class="sxs-lookup"><span data-stu-id="0f10a-131">Then, you can mount the share without credentials.</span></span> <span data-ttu-id="0f10a-132">Perform the following two steps:</span><span class="sxs-lookup"><span data-stu-id="0f10a-132">Perform the following two steps:</span></span>

1. <span data-ttu-id="0f10a-133">Run the `cmdkey` command-line utility using a start task in the pool configuration.</span><span class="sxs-lookup"><span data-stu-id="0f10a-133">Run the `cmdkey` command-line utility using a start task in the pool configuration.</span></span> <span data-ttu-id="0f10a-134">This persists the credentials on each Windows node.</span><span class="sxs-lookup"><span data-stu-id="0f10a-134">This persists the credentials on each Windows node.</span></span> <span data-ttu-id="0f10a-135">The start task command line is similar to:</span><span class="sxs-lookup"><span data-stu-id="0f10a-135">The start task command line is similar to:</span></span>

  ```
  cmd /c "cmdkey /add:mystorageaccountname.file.core.windows.net /user:AZURE\mystorageaccountname /pass:XXXXXXXXXXXXXXXXXXXXX=="

  ```

2. Mount the share on each node as part of each task using `net use`. For example, the following task command line mounts the file share as the *S:* drive. This would be followed by a command or script that references the share. Cached credentials are used in the call to `net use`. <span data-ttu-id="0f10a-140">This step assumes you are using the same user identity for the tasks that you used in the start task on the pool, which isn't appropriate for all scenarios.</span><span class="sxs-lookup"><span data-stu-id="0f10a-140">This step assumes you are using the same user identity for the tasks that you used in the start task on the pool, which isn't appropriate for all scenarios.</span></span>

  ```
  cmd /c "net use S: \\mystorageaccountname.file.core.windows.net\myfileshare" 
  ```

### <a name="c-example"></a><span data-ttu-id="0f10a-141">C# example</span><span class="sxs-lookup"><span data-stu-id="0f10a-141">C# example</span></span>
<span data-ttu-id="0f10a-142">The following C# example shows how to persist the credentials on a Windows pool using a start task.</span><span class="sxs-lookup"><span data-stu-id="0f10a-142">The following C# example shows how to persist the credentials on a Windows pool using a start task.</span></span> <span data-ttu-id="0f10a-143">The storage file service name and storage credentials are passed as defined constants.</span><span class="sxs-lookup"><span data-stu-id="0f10a-143">The storage file service name and storage credentials are passed as defined constants.</span></span> <span data-ttu-id="0f10a-144">Here, the start task runs under a standard (non-administrator) auto-user account with pool scope.</span><span class="sxs-lookup"><span data-stu-id="0f10a-144">Here, the start task runs under a standard (non-administrator) auto-user account with pool scope.</span></span>

```csharp
...
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: PoolId,
    targetDedicatedComputeNodes: PoolNodeCount,
    virtualMachineSize: PoolVMSize,
    virtualMachineConfiguration: virtualMachineConfiguration);

// Start task to store credentials to mount file share
string startTaskCommandLine = String.Format("cmd /c \"cmdkey /add:{0} /user:AZURE\\{1} /pass:{2}\"", StorageFileService, StorageAccountName, StorageAccountKey);

pool.StartTask = new StartTask
{
    CommandLine = startTaskCommandLine,
    UserIdentity = new UserIdentity(new AutoUserSpecification(
        elevationLevel: ElevationLevel.NonAdmin, 
        scope: AutoUserScope.Pool))
};

pool.Commit();
```

<span data-ttu-id="0f10a-145">After storing the credentials, use your task command lines to mount the share and reference the share in read or write operations.</span><span class="sxs-lookup"><span data-stu-id="0f10a-145">After storing the credentials, use your task command lines to mount the share and reference the share in read or write operations.</span></span> <span data-ttu-id="0f10a-146">As a basic example, the task command line in the following snippet uses the `dir` command to list files in the file share.</span><span class="sxs-lookup"><span data-stu-id="0f10a-146">As a basic example, the task command line in the following snippet uses the `dir` command to list files in the file share.</span></span> <span data-ttu-id="0f10a-147">Make sure to run each job task using the same [user identity](batch-user-accounts.md) you used to run the start task in the pool.</span><span class="sxs-lookup"><span data-stu-id="0f10a-147">Make sure to run each job task using the same [user identity](batch-user-accounts.md) you used to run the start task in the pool.</span></span> 

```csharp
...
string taskId = "myTask";
string taskCommandLine = String.Format("cmd /c \"net use {0} {1} & dir {2}\"", ShareMountPoint, StorageFileShare, ShareMountPoint);

CloudTask task = new CloudTask(taskId, taskCommandLine);
task.UserIdentity = new UserIdentity(new AutoUserSpecification(
    elevationLevel: ElevationLevel.NonAdmin,
    scope: AutoUserScope.Pool));
tasks.Add(task);
```

## <a name="mount-a-share-on-a-linux-pool"></a><span data-ttu-id="0f10a-148">Mount a share on a Linux pool</span><span class="sxs-lookup"><span data-stu-id="0f10a-148">Mount a share on a Linux pool</span></span>

<span data-ttu-id="0f10a-149">Azure file shares can be mounted in Linux distributions using the [CIFS kernel client](https://wiki.samba.org/index.php/LinuxCIFS).</span><span class="sxs-lookup"><span data-stu-id="0f10a-149">Azure file shares can be mounted in Linux distributions using the [CIFS kernel client](https://wiki.samba.org/index.php/LinuxCIFS).</span></span> <span data-ttu-id="0f10a-150">The following example shows how to mount a file share on a pool of Ubuntu 16.04 LTS compute nodes.</span><span class="sxs-lookup"><span data-stu-id="0f10a-150">The following example shows how to mount a file share on a pool of Ubuntu 16.04 LTS compute nodes.</span></span> <span data-ttu-id="0f10a-151">If you use a different Linux distribution, the general steps are similar, but use the package manager appropriate for the distribution.</span><span class="sxs-lookup"><span data-stu-id="0f10a-151">If you use a different Linux distribution, the general steps are similar, but use the package manager appropriate for the distribution.</span></span> <span data-ttu-id="0f10a-152">For details and additional examples, see [Use Azure Files with Linux](../storage/files/storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="0f10a-152">For details and additional examples, see [Use Azure Files with Linux](../storage/files/storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="0f10a-153">First, under an administrator user identity, install the `cifs-utils` package, and create the mount point (for example, */mnt/MyAzureFileShare*) in the local filesystem.</span><span class="sxs-lookup"><span data-stu-id="0f10a-153">First, under an administrator user identity, install the `cifs-utils` package, and create the mount point (for example, */mnt/MyAzureFileShare*) in the local filesystem.</span></span> <span data-ttu-id="0f10a-154">A folder for a mount point can be created anywhere on the file system, but it's common convention to create this under the `/mnt` folder.</span><span class="sxs-lookup"><span data-stu-id="0f10a-154">A folder for a mount point can be created anywhere on the file system, but it's common convention to create this under the `/mnt` folder.</span></span> <span data-ttu-id="0f10a-155">Be sure not to create a mount point directly at `/mnt` (on Ubuntu) or `/mnt/resource` (on other distributions).</span><span class="sxs-lookup"><span data-stu-id="0f10a-155">Be sure not to create a mount point directly at `/mnt` (on Ubuntu) or `/mnt/resource` (on other distributions).</span></span>

```
apt-get update && apt-get install cifs-utils && sudo mkdir -p /mnt/MyAzureFileShare
```

<span data-ttu-id="0f10a-156">Then, run the `mount` command to mount the file share, providing these credentials:</span><span class="sxs-lookup"><span data-stu-id="0f10a-156">Then, run the `mount` command to mount the file share, providing these credentials:</span></span>

* <span data-ttu-id="0f10a-157">**User name**: \<storageaccountname\>, for example, *mystorageaccountname*</span><span class="sxs-lookup"><span data-stu-id="0f10a-157">**User name**: \<storageaccountname\>, for example, *mystorageaccountname*</span></span>
* <span data-ttu-id="0f10a-158">**Password**: <StorageAccountKeyWhichEnds in==>, for example, *XXXXXXXXXXXXXXXXXXXXX==*</span><span class="sxs-lookup"><span data-stu-id="0f10a-158">**Password**: <StorageAccountKeyWhichEnds in==>, for example, *XXXXXXXXXXXXXXXXXXXXX==*</span></span>

<span data-ttu-id="0f10a-159">The following command mounts a file share *myfileshare* in storage account *mystorageaccountname* at */mnt/MyAzureFileShare*:</span><span class="sxs-lookup"><span data-stu-id="0f10a-159">The following command mounts a file share *myfileshare* in storage account *mystorageaccountname* at */mnt/MyAzureFileShare*:</span></span> 

```
mount -t cifs //mystorageaccountname.file.core.windows.net/myfileshare /mnt/MyAzureFileShare -o vers=3.0,username=mystorageaccountname,password=XXXXXXXXXXXXXXXXXXXXX==,dir_mode=0777,file_mode=0777,serverino && ls /mnt/MyAzureFileShare
```

<span data-ttu-id="0f10a-160">For simplicity, the examples here pass the credentials directly in text.</span><span class="sxs-lookup"><span data-stu-id="0f10a-160">For simplicity, the examples here pass the credentials directly in text.</span></span> <span data-ttu-id="0f10a-161">In practice, we strongly recommend managing the credentials using environment variables, certificates, or a solution such as Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0f10a-161">In practice, we strongly recommend managing the credentials using environment variables, certificates, or a solution such as Azure Key Vault.</span></span>

<span data-ttu-id="0f10a-162">On a Linux pool, you can combine all of these steps in a single start task, or run them in a script.</span><span class="sxs-lookup"><span data-stu-id="0f10a-162">On a Linux pool, you can combine all of these steps in a single start task, or run them in a script.</span></span> <span data-ttu-id="0f10a-163">Run the start task as an administrator user on the pool.</span><span class="sxs-lookup"><span data-stu-id="0f10a-163">Run the start task as an administrator user on the pool.</span></span> <span data-ttu-id="0f10a-164">Set your start task to wait to complete successfully before running further tasks on the pool that reference the share.</span><span class="sxs-lookup"><span data-stu-id="0f10a-164">Set your start task to wait to complete successfully before running further tasks on the pool that reference the share.</span></span>

### <a name="python-example"></a><span data-ttu-id="0f10a-165">Python example</span><span class="sxs-lookup"><span data-stu-id="0f10a-165">Python example</span></span>

<span data-ttu-id="0f10a-166">The following Python example shows how to configure an Ubuntu pool to mount the share in a start task.</span><span class="sxs-lookup"><span data-stu-id="0f10a-166">The following Python example shows how to configure an Ubuntu pool to mount the share in a start task.</span></span> <span data-ttu-id="0f10a-167">The mount point, file share endpoint, and storage credentials are passed as defined constants.</span><span class="sxs-lookup"><span data-stu-id="0f10a-167">The mount point, file share endpoint, and storage credentials are passed as defined constants.</span></span> <span data-ttu-id="0f10a-168">The start task runs under an administrator auto-user account with pool scope.</span><span class="sxs-lookup"><span data-stu-id="0f10a-168">The start task runs under an administrator auto-user account with pool scope.</span></span>

```python
pool = batch.models.PoolAddParameter(
    id=pool_id,
    virtual_machine_configuration = batchmodels.VirtualMachineConfiguration(
        image_reference = batchmodels.ImageReference(
            publisher="Canonical",
            offer="UbuntuServer",
            sku="16.04.0-LTS",
            version="latest"),
        node_agent_sku_id = "batch.node.ubuntu 16.04"),
    vm_size=_POOL_VM_SIZE,
    target_dedicated_nodes=_POOL_NODE_COUNT,
    start_task=batchmodels.StartTask(
        command_line="/bin/bash -c \"apt-get update && apt-get install cifs-utils && mkdir -p {} && mount -t cifs {} {} -o vers=3.0,username={},password={},dir_mode=0777,file_mode=0777,serverino\"".format(_COMPUTE_NODE_MOUNT_POINT, _STORAGE_ACCOUNT_SHARE_ENDPOINT, _COMPUTE_NODE_MOUNT_POINT, _STORAGE_ACCOUNT_NAME, _STORAGE_ACCOUNT_KEY),
        wait_for_success=True,
        user_identity=batchmodels.UserIdentity(
            auto_user=batchmodels.AutoUserSpecification(
                scope=batchmodels.AutoUserScope.pool,
                elevation_level=batchmodels.ElevationLevel.admin)),
    )
)
batch_service_client.pool.add(pool)
```

<span data-ttu-id="0f10a-169">After mounting the share and defining a job, use the share in your task command lines.</span><span class="sxs-lookup"><span data-stu-id="0f10a-169">After mounting the share and defining a job, use the share in your task command lines.</span></span> <span data-ttu-id="0f10a-170">For example, the following basic command uses `ls` to list files in the file share.</span><span class="sxs-lookup"><span data-stu-id="0f10a-170">For example, the following basic command uses `ls` to list files in the file share.</span></span>

```python
...
task = batch.models.TaskAddParameter(
    id='mytask',
    command_line="/bin/bash -c \"ls {}\"".format(_COMPUTE_NODE_MOUNT_POINT))

batch_service_client.task.add(job_id, task)
```


## <a name="next-steps"></a><span data-ttu-id="0f10a-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="0f10a-171">Next steps</span></span>

* <span data-ttu-id="0f10a-172">For other options to read and write data in Batch, see the [Batch feature overview](batch-api-basics.md) and [Persist job and task output](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="0f10a-172">For other options to read and write data in Batch, see the [Batch feature overview](batch-api-basics.md) and [Persist job and task output](batch-task-output.md).</span></span>

* <span data-ttu-id="0f10a-173">See also the [Batch Shipyard](https://github.com/Azure/batch-shipyard) toolkit, which includes [Shipyard recipes](https://github.com/Azure/batch-shipyard/tree/master/recipes) to deploy file systems for Batch container workloads.</span><span class="sxs-lookup"><span data-stu-id="0f10a-173">See also the [Batch Shipyard](https://github.com/Azure/batch-shipyard) toolkit, which includes [Shipyard recipes](https://github.com/Azure/batch-shipyard/tree/master/recipes) to deploy file systems for Batch container workloads.</span></span>