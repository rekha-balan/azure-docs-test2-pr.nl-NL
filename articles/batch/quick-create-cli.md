---
title: Azure Quickstart - Run Batch job - CLI
description: Quickly learn to run a Batch job with the Azure CLI.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 07/03/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 142305cf371135e71424ca38885c40595398a74d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869976"
---
# <a name="quickstart-run-your-first-batch-job-with-the-azure-cli"></a><span data-ttu-id="f14fd-103">Quickstart: Run your first Batch job with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f14fd-103">Quickstart: Run your first Batch job with the Azure CLI</span></span>

<span data-ttu-id="f14fd-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="f14fd-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="f14fd-105">This quickstart shows how to use the Azure CLI to create a Batch account, a *pool* of compute nodes (virtual machines), and a *job* that runs *tasks* on the pool.</span><span class="sxs-lookup"><span data-stu-id="f14fd-105">This quickstart shows how to use the Azure CLI to create a Batch account, a *pool* of compute nodes (virtual machines), and a *job* that runs *tasks* on the pool.</span></span> <span data-ttu-id="f14fd-106">Each sample task runs a basic command on one of the pool nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-106">Each sample task runs a basic command on one of the pool nodes.</span></span> <span data-ttu-id="f14fd-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="f14fd-107">After completing this quickstart, you will understand the key concepts of the Batch service and be ready to try Batch with more realistic workloads at larger scale.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f14fd-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="f14fd-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="f14fd-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="f14fd-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="f14fd-110">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f14fd-110">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 

## <a name="create-a-resource-group"></a><span data-ttu-id="f14fd-111">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="f14fd-111">Create a resource group</span></span>

<span data-ttu-id="f14fd-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-112">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="f14fd-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="f14fd-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="f14fd-114">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span><span class="sxs-lookup"><span data-stu-id="f14fd-114">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span></span>

```azurecli-interactive 
az group create \
    --name myResourceGroup \
    --location eastus2
```

## <a name="create-a-storage-account"></a><span data-ttu-id="f14fd-115">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="f14fd-115">Create a storage account</span></span>

<span data-ttu-id="f14fd-116">You can link an Azure Storage account with your Batch account.</span><span class="sxs-lookup"><span data-stu-id="f14fd-116">You can link an Azure Storage account with your Batch account.</span></span> <span data-ttu-id="f14fd-117">Although not required for this quickstart, the storage account is useful to deploy applications and store input and output data for most real-world workloads.</span><span class="sxs-lookup"><span data-stu-id="f14fd-117">Although not required for this quickstart, the storage account is useful to deploy applications and store input and output data for most real-world workloads.</span></span> <span data-ttu-id="f14fd-118">Create a storage account in your resource group with the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-118">Create a storage account in your resource group with the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span></span>

```azurecli-interactive
az storage account create \
    --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus2 \
    --sku Standard_LRS
```

## <a name="create-a-batch-account"></a><span data-ttu-id="f14fd-119">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="f14fd-119">Create a Batch account</span></span>

<span data-ttu-id="f14fd-120">Create a Batch account with the [az batch account create](/cli/azure/batch/account#az-batch-account-create) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-120">Create a Batch account with the [az batch account create](/cli/azure/batch/account#az-batch-account-create) command.</span></span> <span data-ttu-id="f14fd-121">You need an account to create compute resources (pools of compute nodes) and Batch jobs.</span><span class="sxs-lookup"><span data-stu-id="f14fd-121">You need an account to create compute resources (pools of compute nodes) and Batch jobs.</span></span>

<span data-ttu-id="f14fd-122">The following example creates a Batch account named *mybatchaccount* in *myResourceGroup*, and links the storage account you created.</span><span class="sxs-lookup"><span data-stu-id="f14fd-122">The following example creates a Batch account named *mybatchaccount* in *myResourceGroup*, and links the storage account you created.</span></span>  

```azurecli-interactive 
az batch account create \
    --name mybatchaccount \
    --storage-account mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus2
```

<span data-ttu-id="f14fd-123">To create and manage compute pools and jobs, you need to authenticate with Batch.</span><span class="sxs-lookup"><span data-stu-id="f14fd-123">To create and manage compute pools and jobs, you need to authenticate with Batch.</span></span> <span data-ttu-id="f14fd-124">Log in to the account with the [az batch account login](/cli/azure/batch/account#az-batch-account-login) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-124">Log in to the account with the [az batch account login](/cli/azure/batch/account#az-batch-account-login) command.</span></span> <span data-ttu-id="f14fd-125">After you log in, your `az batch` commands use this account context.</span><span class="sxs-lookup"><span data-stu-id="f14fd-125">After you log in, your `az batch` commands use this account context.</span></span>

```azurecli-interactive 
az batch account login \
    --name mybatchaccount \
    --resource-group myResourceGroup \
    --shared-key-auth
```

## <a name="create-a-pool-of-compute-nodes"></a><span data-ttu-id="f14fd-126">Create a pool of compute nodes</span><span class="sxs-lookup"><span data-stu-id="f14fd-126">Create a pool of compute nodes</span></span>

<span data-ttu-id="f14fd-127">Now that you have a Batch account, create a sample pool of Linux compute nodes using the [az batch pool create](/cli/azure/batch/pool#az-batch-pool-create) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-127">Now that you have a Batch account, create a sample pool of Linux compute nodes using the [az batch pool create](/cli/azure/batch/pool#az-batch-pool-create) command.</span></span> <span data-ttu-id="f14fd-128">The following example creates a pool named *mypool* of 2 size *Standard_A1_v2* nodes running Ubuntu 16.04 LTS.</span><span class="sxs-lookup"><span data-stu-id="f14fd-128">The following example creates a pool named *mypool* of 2 size *Standard_A1_v2* nodes running Ubuntu 16.04 LTS.</span></span> <span data-ttu-id="f14fd-129">The suggested node size offers a good balance of performance versus cost for this quick example.</span><span class="sxs-lookup"><span data-stu-id="f14fd-129">The suggested node size offers a good balance of performance versus cost for this quick example.</span></span>
 
```azurecli-interactive
az batch pool create \
    --id mypool --vm-size Standard_A1_v2 \
    --target-dedicated-nodes 2 \
    --image canonical:ubuntuserver:16.04-LTS \
    --node-agent-sku-id "batch.node.ubuntu 16.04" 
```

<span data-ttu-id="f14fd-130">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-130">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span></span> <span data-ttu-id="f14fd-131">During this time, the pool is in the `resizing` state.</span><span class="sxs-lookup"><span data-stu-id="f14fd-131">During this time, the pool is in the `resizing` state.</span></span> <span data-ttu-id="f14fd-132">To see the status of the pool, run the [az batch pool show](/cli/azure/batch/pool#az-batch-pool-show) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-132">To see the status of the pool, run the [az batch pool show](/cli/azure/batch/pool#az-batch-pool-show) command.</span></span> <span data-ttu-id="f14fd-133">This command shows all the properties of the pool, and you can query for specific properties.</span><span class="sxs-lookup"><span data-stu-id="f14fd-133">This command shows all the properties of the pool, and you can query for specific properties.</span></span> <span data-ttu-id="f14fd-134">The following command gets the allocation state of the pool:</span><span class="sxs-lookup"><span data-stu-id="f14fd-134">The following command gets the allocation state of the pool:</span></span>

```azurecli-interactive
az batch pool show --pool-id mypool \
    --query "allocationState"
```

<span data-ttu-id="f14fd-135">Continue the following steps to create a job and tasks while the pool state is changing.</span><span class="sxs-lookup"><span data-stu-id="f14fd-135">Continue the following steps to create a job and tasks while the pool state is changing.</span></span> <span data-ttu-id="f14fd-136">The pool is ready to run tasks when the allocation state is `steady` and all the nodes are running.</span><span class="sxs-lookup"><span data-stu-id="f14fd-136">The pool is ready to run tasks when the allocation state is `steady` and all the nodes are running.</span></span> 

## <a name="create-a-job"></a><span data-ttu-id="f14fd-137">Create a job</span><span class="sxs-lookup"><span data-stu-id="f14fd-137">Create a job</span></span>

<span data-ttu-id="f14fd-138">Now that you have a pool, create a job to run on it.</span><span class="sxs-lookup"><span data-stu-id="f14fd-138">Now that you have a pool, create a job to run on it.</span></span>  <span data-ttu-id="f14fd-139">A Batch job is a logical group for one or more tasks.</span><span class="sxs-lookup"><span data-stu-id="f14fd-139">A Batch job is a logical group for one or more tasks.</span></span> <span data-ttu-id="f14fd-140">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span><span class="sxs-lookup"><span data-stu-id="f14fd-140">A job includes settings common to the tasks, such as priority and the pool to run tasks on.</span></span> <span data-ttu-id="f14fd-141">Create a Batch job by using the [az batch job create](/cli/azure/batch/job#az-batch-job-create) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-141">Create a Batch job by using the [az batch job create](/cli/azure/batch/job#az-batch-job-create) command.</span></span> <span data-ttu-id="f14fd-142">The following example creates a job *myjob* on the pool *mypool*.</span><span class="sxs-lookup"><span data-stu-id="f14fd-142">The following example creates a job *myjob* on the pool *mypool*.</span></span> <span data-ttu-id="f14fd-143">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="f14fd-143">Initially the job has no tasks.</span></span>

```azurecli-interactive 
az batch job create \
    --id myjob \
    --pool-id mypool
```

## <a name="create-tasks"></a><span data-ttu-id="f14fd-144">Create tasks</span><span class="sxs-lookup"><span data-stu-id="f14fd-144">Create tasks</span></span>

<span data-ttu-id="f14fd-145">Now use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create some tasks to run in the job.</span><span class="sxs-lookup"><span data-stu-id="f14fd-145">Now use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create some tasks to run in the job.</span></span> <span data-ttu-id="f14fd-146">In this example, you create four identical tasks.</span><span class="sxs-lookup"><span data-stu-id="f14fd-146">In this example, you create four identical tasks.</span></span> <span data-ttu-id="f14fd-147">Each task runs a `command-line` to display the Batch environment variables on a compute node, and then waits 90 seconds.</span><span class="sxs-lookup"><span data-stu-id="f14fd-147">Each task runs a `command-line` to display the Batch environment variables on a compute node, and then waits 90 seconds.</span></span> <span data-ttu-id="f14fd-148">When you use Batch, this command line is where you specify your app or script.</span><span class="sxs-lookup"><span data-stu-id="f14fd-148">When you use Batch, this command line is where you specify your app or script.</span></span> <span data-ttu-id="f14fd-149">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-149">Batch provides a number of ways to deploy apps and scripts to compute nodes.</span></span>

<span data-ttu-id="f14fd-150">The following Bash script creates 4 parallel tasks (*mytask1* to *mytask4*).</span><span class="sxs-lookup"><span data-stu-id="f14fd-150">The following Bash script creates 4 parallel tasks (*mytask1* to *mytask4*).</span></span>

```azurecli-interactive 
for i in {1..4}
do
   az batch task create \
    --task-id mytask$i \
    --job-id myjob \
    --command-line "/bin/bash -c 'printenv | grep AZ_BATCH; sleep 90s'"
done
```

<span data-ttu-id="f14fd-151">The command output shows settings for each of the tasks.</span><span class="sxs-lookup"><span data-stu-id="f14fd-151">The command output shows settings for each of the tasks.</span></span> <span data-ttu-id="f14fd-152">Batch distributes the tasks to the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-152">Batch distributes the tasks to the compute nodes.</span></span>

## <a name="view-task-status"></a><span data-ttu-id="f14fd-153">View task status</span><span class="sxs-lookup"><span data-stu-id="f14fd-153">View task status</span></span>

<span data-ttu-id="f14fd-154">After you create a task, Batch queues it to run on the pool.</span><span class="sxs-lookup"><span data-stu-id="f14fd-154">After you create a task, Batch queues it to run on the pool.</span></span> <span data-ttu-id="f14fd-155">Once a node is available to run it, the task runs.</span><span class="sxs-lookup"><span data-stu-id="f14fd-155">Once a node is available to run it, the task runs.</span></span>

<span data-ttu-id="f14fd-156">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view the status of the Batch tasks.</span><span class="sxs-lookup"><span data-stu-id="f14fd-156">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view the status of the Batch tasks.</span></span> <span data-ttu-id="f14fd-157">The following example shows details about *mytask1* running on one of the pool nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-157">The following example shows details about *mytask1* running on one of the pool nodes.</span></span>

```azurecli-interactive 
az batch task show \
    --job-id myjob \
    --task-id mytask1
```

<span data-ttu-id="f14fd-158">The command output includes many details, but take note of the `exitCode` of the task command line and the `nodeId`.</span><span class="sxs-lookup"><span data-stu-id="f14fd-158">The command output includes many details, but take note of the `exitCode` of the task command line and the `nodeId`.</span></span> <span data-ttu-id="f14fd-159">An `exitCode` of 0 indicates that the task command line completed successfully.</span><span class="sxs-lookup"><span data-stu-id="f14fd-159">An `exitCode` of 0 indicates that the task command line completed successfully.</span></span> <span data-ttu-id="f14fd-160">The `nodeId` indicates the ID of the pool node on which the task ran.</span><span class="sxs-lookup"><span data-stu-id="f14fd-160">The `nodeId` indicates the ID of the pool node on which the task ran.</span></span>

## <a name="view-task-output"></a><span data-ttu-id="f14fd-161">View task output</span><span class="sxs-lookup"><span data-stu-id="f14fd-161">View task output</span></span>

<span data-ttu-id="f14fd-162">To list the files created by a task on a compute node, use the [az batch task file list](/cli/azure/batch/task#az-batch-task-file-list) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-162">To list the files created by a task on a compute node, use the [az batch task file list](/cli/azure/batch/task#az-batch-task-file-list) command.</span></span> <span data-ttu-id="f14fd-163">The following command lists the files created by *mytask1*:</span><span class="sxs-lookup"><span data-stu-id="f14fd-163">The following command lists the files created by *mytask1*:</span></span> 

```azurecli-interactive 
az batch task file list \
    --job-id myjob \
    --task-id mytask1 \
    --output table
```

<span data-ttu-id="f14fd-164">Output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f14fd-164">Output is similar to the following:</span></span>

```
Name        URL                                                                                         Is Directory      Content Length
----------  ------------------------------------------------------------------------------------------  --------------  ----------------
stdout.txt  https://mybatchaccount.eastus2.batch.azure.com/jobs/myjob/tasks/mytask1/files/stdout.txt  False                  695
certs       https://mybatchaccount.eastus2.batch.azure.com/jobs/myjob/tasks/mytask1/files/certs       True
wd          https://mybatchaccount.eastus2.batch.azure.com/jobs/myjob/tasks/mytask1/files/wd          True
stderr.txt  https://mybatchaccount.eastus2.batch.azure.com/jobs/myjob/tasks/mytask1/files/stderr.txt  False                     0

```

<span data-ttu-id="f14fd-165">To download one of the output files to a local directory, use the [az batch task file download](/cli/azure/batch/task#az-batch-task-file-download) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-165">To download one of the output files to a local directory, use the [az batch task file download](/cli/azure/batch/task#az-batch-task-file-download) command.</span></span> <span data-ttu-id="f14fd-166">In this example, task output is in `stdout.txt`.</span><span class="sxs-lookup"><span data-stu-id="f14fd-166">In this example, task output is in `stdout.txt`.</span></span> 

```azurecli-interactive
az batch task file download \
    --job-id myjob \
    --task-id mytask1 \
    --file-path stdout.txt \
    --destination ./stdout.txt
```

<span data-ttu-id="f14fd-167">You can view the contents of `stdout.txt` in a text editor.</span><span class="sxs-lookup"><span data-stu-id="f14fd-167">You can view the contents of `stdout.txt` in a text editor.</span></span> <span data-ttu-id="f14fd-168">The contents show the Azure Batch environment variables that are set on the node.</span><span class="sxs-lookup"><span data-stu-id="f14fd-168">The contents show the Azure Batch environment variables that are set on the node.</span></span> <span data-ttu-id="f14fd-169">When you create your own Batch jobs, you can reference these environment variables in task command lines, and in the apps and scripts run by the command lines.</span><span class="sxs-lookup"><span data-stu-id="f14fd-169">When you create your own Batch jobs, you can reference these environment variables in task command lines, and in the apps and scripts run by the command lines.</span></span> <span data-ttu-id="f14fd-170">For example:</span><span class="sxs-lookup"><span data-stu-id="f14fd-170">For example:</span></span>

```
AZ_BATCH_TASK_DIR=/mnt/batch/tasks/workitems/myjob/job-1/mytask1
AZ_BATCH_NODE_STARTUP_DIR=/mnt/batch/tasks/startup
AZ_BATCH_CERTIFICATES_DIR=/mnt/batch/tasks/workitems/myjob/job-1/mytask1/certs
AZ_BATCH_ACCOUNT_URL=https://mybatchaccount.eastus2.batch.azure.com/
AZ_BATCH_TASK_WORKING_DIR=/mnt/batch/tasks/workitems/myjob/job-1/mytask1/wd
AZ_BATCH_NODE_SHARED_DIR=/mnt/batch/tasks/shared
AZ_BATCH_TASK_USER=_azbatch
AZ_BATCH_NODE_ROOT_DIR=/mnt/batch/tasks
AZ_BATCH_JOB_ID=myjobl
AZ_BATCH_NODE_IS_DEDICATED=true
AZ_BATCH_NODE_ID=tvm-257509324_2-20180703t215033z
AZ_BATCH_POOL_ID=mypool
AZ_BATCH_TASK_ID=mytask1
AZ_BATCH_ACCOUNT_NAME=mybatchaccount
AZ_BATCH_TASK_USER_IDENTITY=PoolNonAdmin
```
## <a name="clean-up-resources"></a><span data-ttu-id="f14fd-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f14fd-171">Clean up resources</span></span>
<span data-ttu-id="f14fd-172">If you want to continue with Batch tutorials and samples, use the Batch account and linked storage account created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="f14fd-172">If you want to continue with Batch tutorials and samples, use the Batch account and linked storage account created in this quickstart.</span></span> <span data-ttu-id="f14fd-173">There is no charge for the Batch account itself.</span><span class="sxs-lookup"><span data-stu-id="f14fd-173">There is no charge for the Batch account itself.</span></span>

<span data-ttu-id="f14fd-174">You are charged for pools while the nodes are running, even if no jobs are scheduled.</span><span class="sxs-lookup"><span data-stu-id="f14fd-174">You are charged for pools while the nodes are running, even if no jobs are scheduled.</span></span> <span data-ttu-id="f14fd-175">When you no longer need a pool, delete it with the [az batch pool delete](/cli/azure/batch/pool#az-batch-pool-delete) command.</span><span class="sxs-lookup"><span data-stu-id="f14fd-175">When you no longer need a pool, delete it with the [az batch pool delete](/cli/azure/batch/pool#az-batch-pool-delete) command.</span></span> <span data-ttu-id="f14fd-176">When you delete the pool, all task output on the nodes is deleted.</span><span class="sxs-lookup"><span data-stu-id="f14fd-176">When you delete the pool, all task output on the nodes is deleted.</span></span> 

```azurecli-interactive
az batch pool delete --pool-id mypool
```

<span data-ttu-id="f14fd-177">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, Batch account, pools, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="f14fd-177">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, Batch account, pools, and all related resources.</span></span> <span data-ttu-id="f14fd-178">Delete the resources as follows:</span><span class="sxs-lookup"><span data-stu-id="f14fd-178">Delete the resources as follows:</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="f14fd-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="f14fd-179">Next steps</span></span>

<span data-ttu-id="f14fd-180">In this quickstart, you created a Batch account, a Batch pool, and a Batch job.</span><span class="sxs-lookup"><span data-stu-id="f14fd-180">In this quickstart, you created a Batch account, a Batch pool, and a Batch job.</span></span> <span data-ttu-id="f14fd-181">The job ran sample tasks, and you viewed output created on one of the nodes.</span><span class="sxs-lookup"><span data-stu-id="f14fd-181">The job ran sample tasks, and you viewed output created on one of the nodes.</span></span> <span data-ttu-id="f14fd-182">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span><span class="sxs-lookup"><span data-stu-id="f14fd-182">Now that you understand the key concepts of the Batch service, you are ready to try Batch with more realistic workloads at larger scale.</span></span> <span data-ttu-id="f14fd-183">To learn more about Azure Batch, continue to the Azure Batch tutorials.</span><span class="sxs-lookup"><span data-stu-id="f14fd-183">To learn more about Azure Batch, continue to the Azure Batch tutorials.</span></span> 


> [!div class="nextstepaction"]
> [<span data-ttu-id="f14fd-184">Azure Batch tutorials</span><span class="sxs-lookup"><span data-stu-id="f14fd-184">Azure Batch tutorials</span></span>](./tutorial-parallel-dotnet.md)
