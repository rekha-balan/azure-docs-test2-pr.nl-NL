---
title: Work with Azure Batch AI clusters | Microsoft Docs
description: How to choose a Batch AI cluster configuration, and create and manage a cluster AI
services: batch-ai
documentationcenter: ''
author: johnwu10
manager: jeconnoc
editor: ''
ms.service: batch-ai
ms.topic: article
ms.date: 08/14/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 61294d8b6b84b03b1e0c8d79b4d2855452c7f0e6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868972"
---
# <a name="work-with-batch-ai-clusters"></a><span data-ttu-id="eac42-103">Work with Batch AI clusters</span><span class="sxs-lookup"><span data-stu-id="eac42-103">Work with Batch AI clusters</span></span> 

<span data-ttu-id="eac42-104">This article explains how to work with clusters in Azure Batch AI.</span><span class="sxs-lookup"><span data-stu-id="eac42-104">This article explains how to work with clusters in Azure Batch AI.</span></span> <span data-ttu-id="eac42-105">It introduces the concept of clusters, the types of configurations that are possible, and examples.</span><span class="sxs-lookup"><span data-stu-id="eac42-105">It introduces the concept of clusters, the types of configurations that are possible, and examples.</span></span> <span data-ttu-id="eac42-106">Most of the examples to create and manage a cluster in this article use the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="eac42-106">Most of the examples to create and manage a cluster in this article use the Azure CLI.</span></span> <span data-ttu-id="eac42-107">However, you can use other tools including the Azure portal and the Azure Batch AI SDKs to work with clusters.</span><span class="sxs-lookup"><span data-stu-id="eac42-107">However, you can use other tools including the Azure portal and the Azure Batch AI SDKs to work with clusters.</span></span>

<span data-ttu-id="eac42-108">A Batch AI cluster is one of several resources in the service.</span><span class="sxs-lookup"><span data-stu-id="eac42-108">A Batch AI cluster is one of several resources in the service.</span></span> <span data-ttu-id="eac42-109">See the [overview of Batch AI resources](resource-concepts.md) to understand the scope of clusters in the service.</span><span class="sxs-lookup"><span data-stu-id="eac42-109">See the [overview of Batch AI resources](resource-concepts.md) to understand the scope of clusters in the service.</span></span>

## <a name="introduction-to-clusters"></a><span data-ttu-id="eac42-110">Introduction to clusters</span><span class="sxs-lookup"><span data-stu-id="eac42-110">Introduction to clusters</span></span>

<span data-ttu-id="eac42-111">A cluster in Batch AI contains the compute resources for running machine learning and AI training jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-111">A cluster in Batch AI contains the compute resources for running machine learning and AI training jobs.</span></span> <span data-ttu-id="eac42-112">All nodes in a cluster have the same VM size and OS image.</span><span class="sxs-lookup"><span data-stu-id="eac42-112">All nodes in a cluster have the same VM size and OS image.</span></span> <span data-ttu-id="eac42-113">Batch AI offers many options for creating clusters that are customized to different needs.</span><span class="sxs-lookup"><span data-stu-id="eac42-113">Batch AI offers many options for creating clusters that are customized to different needs.</span></span> <span data-ttu-id="eac42-114">Typically, you set up a different cluster for each category of processing power needed to complete a project.</span><span class="sxs-lookup"><span data-stu-id="eac42-114">Typically, you set up a different cluster for each category of processing power needed to complete a project.</span></span> <span data-ttu-id="eac42-115">You can scale the number of nodes in a cluster up and down based on demand and budget.</span><span class="sxs-lookup"><span data-stu-id="eac42-115">You can scale the number of nodes in a cluster up and down based on demand and budget.</span></span> <span data-ttu-id="eac42-116">Clusters can be provisioned and shared among a team, or individuals can each provision their own cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-116">Clusters can be provisioned and shared among a team, or individuals can each provision their own cluster.</span></span> 

<span data-ttu-id="eac42-117">Each cluster exists under a Batch AI resource called a *workspace*.</span><span class="sxs-lookup"><span data-stu-id="eac42-117">Each cluster exists under a Batch AI resource called a *workspace*.</span></span> <span data-ttu-id="eac42-118">Before provisioning any cluster, you must have a Batch AI workspace set up.</span><span class="sxs-lookup"><span data-stu-id="eac42-118">Before provisioning any cluster, you must have a Batch AI workspace set up.</span></span> <span data-ttu-id="eac42-119">For example, if you use the Azure CLI, use the [az batchai workspace create](/cli/azure/batchai/workspace?view=azure-cli-latest#az-batchai-workspace-create) command to set up a workspace.</span><span class="sxs-lookup"><span data-stu-id="eac42-119">For example, if you use the Azure CLI, use the [az batchai workspace create](/cli/azure/batchai/workspace?view=azure-cli-latest#az-batchai-workspace-create) command to set up a workspace.</span></span> 

<span data-ttu-id="eac42-120">After you create a cluster, you can submit jobs one at a time into a queue.</span><span class="sxs-lookup"><span data-stu-id="eac42-120">After you create a cluster, you can submit jobs one at a time into a queue.</span></span> <span data-ttu-id="eac42-121">Batch AI then handles the resource allocation process for running the jobs on the cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-121">Batch AI then handles the resource allocation process for running the jobs on the cluster.</span></span> 

## <a name="cluster-configuration-options"></a><span data-ttu-id="eac42-122">Cluster configuration options</span><span class="sxs-lookup"><span data-stu-id="eac42-122">Cluster configuration options</span></span>

<span data-ttu-id="eac42-123">When planning a cluster, first determine your compute requirements.</span><span class="sxs-lookup"><span data-stu-id="eac42-123">When planning a cluster, first determine your compute requirements.</span></span> <span data-ttu-id="eac42-124">Batch AI offers flexible configuration options so you can tailor a cluster to your needs.</span><span class="sxs-lookup"><span data-stu-id="eac42-124">Batch AI offers flexible configuration options so you can tailor a cluster to your needs.</span></span> <span data-ttu-id="eac42-125">The following are the majors options to consider when provisioning a cluster:</span><span class="sxs-lookup"><span data-stu-id="eac42-125">The following are the majors options to consider when provisioning a cluster:</span></span>

* <span data-ttu-id="eac42-126">**VM size** - Choose any [VM size](../virtual-machines/linux/sizes.md) that is available in a [supported region](https://azure.microsoft.com/global-infrastructure/services/) for the cluster nodes.</span><span class="sxs-lookup"><span data-stu-id="eac42-126">**VM size** - Choose any [VM size](../virtual-machines/linux/sizes.md) that is available in a [supported region](https://azure.microsoft.com/global-infrastructure/services/) for the cluster nodes.</span></span> <span data-ttu-id="eac42-127">Each cluster can only contain one size of VM, so if your tasks require multiple types of VMs, you need to provision a separate cluster for each type of compute requirement.</span><span class="sxs-lookup"><span data-stu-id="eac42-127">Each cluster can only contain one size of VM, so if your tasks require multiple types of VMs, you need to provision a separate cluster for each type of compute requirement.</span></span> <span data-ttu-id="eac42-128">To train machine learning or AI models developed with frameworks that take advantage of GPUs, see the [GPU optimized VM sizes](../virtual-machines/linux/sizes-gpu.md) in Azure.</span><span class="sxs-lookup"><span data-stu-id="eac42-128">To train machine learning or AI models developed with frameworks that take advantage of GPUs, see the [GPU optimized VM sizes](../virtual-machines/linux/sizes-gpu.md) in Azure.</span></span>
  
* <span data-ttu-id="eac42-129">**VM priority** - Batch AI offers either dedicated or low-priority VMs for a cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-129">**VM priority** - Batch AI offers either dedicated or low-priority VMs for a cluster.</span></span> <span data-ttu-id="eac42-130">Dedicated VMs are reserved for your use in the cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-130">Dedicated VMs are reserved for your use in the cluster.</span></span> <span data-ttu-id="eac42-131">The low-priority option allocates unused Azure VM capacity at significant cost savings in exchange for the possibility of jobs being pre-empted if Azure reclaims the VMs.</span><span class="sxs-lookup"><span data-stu-id="eac42-131">The low-priority option allocates unused Azure VM capacity at significant cost savings in exchange for the possibility of jobs being pre-empted if Azure reclaims the VMs.</span></span> <span data-ttu-id="eac42-132">Jobs that run for longer than 24 hours on a low-priority VM are also automatically pre-empted.</span><span class="sxs-lookup"><span data-stu-id="eac42-132">Jobs that run for longer than 24 hours on a low-priority VM are also automatically pre-empted.</span></span> <span data-ttu-id="eac42-133">If budget is a concern, consider using low-priority VMs for short experimentation jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-133">If budget is a concern, consider using low-priority VMs for short experimentation jobs.</span></span> <span data-ttu-id="eac42-134">Then, switch to dedicated VMs when it's time to run longer jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-134">Then, switch to dedicated VMs when it's time to run longer jobs.</span></span>

* <span data-ttu-id="eac42-135">**Number of nodes** - Batch AI offers manual and autoscaling options for the number of nodes in the cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-135">**Number of nodes** - Batch AI offers manual and autoscaling options for the number of nodes in the cluster.</span></span> <span data-ttu-id="eac42-136">With the manual option, you control when to scale a cluster up and down, so you can manage your own compute costs.</span><span class="sxs-lookup"><span data-stu-id="eac42-136">With the manual option, you control when to scale a cluster up and down, so you can manage your own compute costs.</span></span> <span data-ttu-id="eac42-137">The autoscaling option ensures that the cluster always downscales when you're not using it, so you minimize your compute costs.</span><span class="sxs-lookup"><span data-stu-id="eac42-137">The autoscaling option ensures that the cluster always downscales when you're not using it, so you minimize your compute costs.</span></span> 

  <span data-ttu-id="eac42-138">If you choose to scale the cluster manually, then you define the initial target during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="eac42-138">If you choose to scale the cluster manually, then you define the initial target during cluster creation.</span></span> <span data-ttu-id="eac42-139">The target is the number of nodes that Batch AI allocates initially.</span><span class="sxs-lookup"><span data-stu-id="eac42-139">The target is the number of nodes that Batch AI allocates initially.</span></span> <span data-ttu-id="eac42-140">Later, you can manually resize the number of nodes.</span><span class="sxs-lookup"><span data-stu-id="eac42-140">Later, you can manually resize the number of nodes.</span></span>  

  <span data-ttu-id="eac42-141">If you choose the autoscaling option, you define the maximum and minimum number of target nodes during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="eac42-141">If you choose the autoscaling option, you define the maximum and minimum number of target nodes during cluster creation.</span></span> <span data-ttu-id="eac42-142">The target can range from 0 to the maximum number of nodes supported by your [Batch AI cores quota](quota-limits.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-142">The target can range from 0 to the maximum number of nodes supported by your [Batch AI cores quota](quota-limits.md).</span></span> <span data-ttu-id="eac42-143">A target of 0 allows you to maintain your cluster configuration without being charged for any compute costs.</span><span class="sxs-lookup"><span data-stu-id="eac42-143">A target of 0 allows you to maintain your cluster configuration without being charged for any compute costs.</span></span> <span data-ttu-id="eac42-144">If you request a higher target than your quota limit supports, then the provisioning will fail.</span><span class="sxs-lookup"><span data-stu-id="eac42-144">If you request a higher target than your quota limit supports, then the provisioning will fail.</span></span> 

* <span data-ttu-id="eac42-145">**VM image** - Batch AI by default provisions the cluster VMs with a default Ubuntu Server image that supports container workloads.</span><span class="sxs-lookup"><span data-stu-id="eac42-145">**VM image** - Batch AI by default provisions the cluster VMs with a default Ubuntu Server image that supports container workloads.</span></span> <span data-ttu-id="eac42-146">You can choose another preconfigured Linux image from the Azure Marketplace, such as a [Data Science Virtual Machine](../machine-learning/data-science-virtual-machine/overview.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-146">You can choose another preconfigured Linux image from the Azure Marketplace, such as a [Data Science Virtual Machine](../machine-learning/data-science-virtual-machine/overview.md).</span></span> 

* <span data-ttu-id="eac42-147">**Storage** - Batch AI provides an auto-storage option, which you can choose when you create a cluster using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="eac42-147">**Storage** - Batch AI provides an auto-storage option, which you can choose when you create a cluster using the Azure CLI.</span></span> <span data-ttu-id="eac42-148">This option automatically creates an Azure file Share and Blob container under a new storage account.</span><span class="sxs-lookup"><span data-stu-id="eac42-148">This option automatically creates an Azure file Share and Blob container under a new storage account.</span></span> <span data-ttu-id="eac42-149">These storage resources are mounted to each of the nodes in the cluster during execution time, allowing the files to be accessed from a local path.</span><span class="sxs-lookup"><span data-stu-id="eac42-149">These storage resources are mounted to each of the nodes in the cluster during execution time, allowing the files to be accessed from a local path.</span></span> <span data-ttu-id="eac42-150">The storage account names, file share name, Blob container name, and mount paths all have default values, which can also be customized using additional parameters during cluster creation.</span><span class="sxs-lookup"><span data-stu-id="eac42-150">The storage account names, file share name, Blob container name, and mount paths all have default values, which can also be customized using additional parameters during cluster creation.</span></span> 

  <span data-ttu-id="eac42-151">If no storage options are defined, then you need to create the storage resources separately and define them when submitting jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-151">If no storage options are defined, then you need to create the storage resources separately and define them when submitting jobs.</span></span> <span data-ttu-id="eac42-152">This option is useful if your cluster is managed at the organization level, but your storage is managed at the user level.</span><span class="sxs-lookup"><span data-stu-id="eac42-152">This option is useful if your cluster is managed at the organization level, but your storage is managed at the user level.</span></span> <span data-ttu-id="eac42-153">For more information on how to upload files to Azure Storage and access them during execution time, see [Store Batch AI job input and output with Azure Storage](use-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="eac42-153">For more information on how to upload files to Azure Storage and access them during execution time, see [Store Batch AI job input and output with Azure Storage](use-azure-storage.md).</span></span>

* <span data-ttu-id="eac42-154">**User access** - Batch AI allows you to generate public and private SSH key files when creating a cluster, or supply your own SSH keys so that you can SSH into individual nodes.</span><span class="sxs-lookup"><span data-stu-id="eac42-154">**User access** - Batch AI allows you to generate public and private SSH key files when creating a cluster, or supply your own SSH keys so that you can SSH into individual nodes.</span></span> <span data-ttu-id="eac42-155">You can also define a user name (set as the current user by default) and password.</span><span class="sxs-lookup"><span data-stu-id="eac42-155">You can also define a user name (set as the current user by default) and password.</span></span> <span data-ttu-id="eac42-156">These credentials can be used to access the nodes during execution in order to view various metrics or gain further insight to your jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-156">These credentials can be used to access the nodes during execution in order to view various metrics or gain further insight to your jobs.</span></span>

* <span data-ttu-id="eac42-157">**Setup task** - Batch AI allows you to define command-line arguments to be executed on each node upon allocation.</span><span class="sxs-lookup"><span data-stu-id="eac42-157">**Setup task** - Batch AI allows you to define command-line arguments to be executed on each node upon allocation.</span></span> <span data-ttu-id="eac42-158">You can also define the path where the output file should be logged to.</span><span class="sxs-lookup"><span data-stu-id="eac42-158">You can also define the path where the output file should be logged to.</span></span> <span data-ttu-id="eac42-159">Use this option when you have additional provisioning steps beyond the base image.</span><span class="sxs-lookup"><span data-stu-id="eac42-159">Use this option when you have additional provisioning steps beyond the base image.</span></span>

* <span data-ttu-id="eac42-160">**Additional configuration** - There are several less common scenarios, which might require more specialized configurations.</span><span class="sxs-lookup"><span data-stu-id="eac42-160">**Additional configuration** - There are several less common scenarios, which might require more specialized configurations.</span></span> <span data-ttu-id="eac42-161">In this case, a [cluster configuration file](https://github.com/Azure/BatchAI/blob/master/documentation/using-azure-cli-20.md#using-cluster-configuration-file) can be attached with the Azure CLI command to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-161">In this case, a [cluster configuration file](https://github.com/Azure/BatchAI/blob/master/documentation/using-azure-cli-20.md#using-cluster-configuration-file) can be attached with the Azure CLI command to create a cluster.</span></span> 

## <a name="create-the-cluster"></a><span data-ttu-id="eac42-162">Create the cluster</span><span class="sxs-lookup"><span data-stu-id="eac42-162">Create the cluster</span></span>

<span data-ttu-id="eac42-163">After you have decided on the cluster configuration options, use the Azure CLI, Azure portal, or Batch AI APIs to create the cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-163">After you have decided on the cluster configuration options, use the Azure CLI, Azure portal, or Batch AI APIs to create the cluster.</span></span> <span data-ttu-id="eac42-164">For example, to create a cluster using the Azure CLI, you can follow the [az batchai cluster create](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-create) documentation to create the exact command that gives you the configurations that you need.</span><span class="sxs-lookup"><span data-stu-id="eac42-164">For example, to create a cluster using the Azure CLI, you can follow the [az batchai cluster create](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-create) documentation to create the exact command that gives you the configurations that you need.</span></span> 

<span data-ttu-id="eac42-165">At the most basic configuration, the following command provisions a Standard_NC6 cluster with one node and SSH access.</span><span class="sxs-lookup"><span data-stu-id="eac42-165">At the most basic configuration, the following command provisions a Standard_NC6 cluster with one node and SSH access.</span></span> <span data-ttu-id="eac42-166">By default, this cluster contains dedicated VMs running the latest default Ubuntu Server image.</span><span class="sxs-lookup"><span data-stu-id="eac42-166">By default, this cluster contains dedicated VMs running the latest default Ubuntu Server image.</span></span>

```azurecli-interactive
az batchai cluster create \
    --name mycluster \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> \
    --vm-size Standard_NC6 \
    --target 1 \
    --generate-ssh-keys
```

<span data-ttu-id="eac42-167">The following example provisions a Standard_NC6 cluster that scales automatically from 0 to 4 nodes and uses low-priority nodes and an auto-storage account.</span><span class="sxs-lookup"><span data-stu-id="eac42-167">The following example provisions a Standard_NC6 cluster that scales automatically from 0 to 4 nodes and uses low-priority nodes and an auto-storage account.</span></span> <span data-ttu-id="eac42-168">This setup is a good configuration if you need a cluster that is low cost and easy to manage.</span><span class="sxs-lookup"><span data-stu-id="eac42-168">This setup is a good configuration if you need a cluster that is low cost and easy to manage.</span></span> 

```azurecli-interactive
az batchai cluster create \
    --name mycluster \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> \
    --vm-size Standard_NC6 \
    --vm-priority lowpriority \
    --max 4 \
    --min 0 \
    --use-auto-storage 
```

<span data-ttu-id="eac42-169">The following example provisions a Standard_NC6 cluster that includes a Data Science Virtual Machine image, custom storage and mounting options, custom SSH credentials, a setup task that installs the *unzip* package, and a cluster configuration file for additional setup.</span><span class="sxs-lookup"><span data-stu-id="eac42-169">The following example provisions a Standard_NC6 cluster that includes a Data Science Virtual Machine image, custom storage and mounting options, custom SSH credentials, a setup task that installs the *unzip* package, and a cluster configuration file for additional setup.</span></span> <span data-ttu-id="eac42-170">This configuration is an example of a cluster that is more customized to your own needs.</span><span class="sxs-lookup"><span data-stu-id="eac42-170">This configuration is an example of a cluster that is more customized to your own needs.</span></span>

```azurecli-interactive
az batchai cluster create \
    --name mycluster \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> \
    --vm-size Standard_NC6 \
    --image UbuntuDSVM \ 
    --config-file cluster.json \
    --setup-task 'apt install unzip -y'
    --storage-account-name <STORAGE ACCOUNT NAME> \
    --nfs-name nfsmount \
    --afs-name afsmount \
    --bfs-name bfsmount \
    --user-name adminuser \
    --ssh-key id_rsa.pub \
    --password secretpassword 
```

## <a name="monitor-the-cluster"></a><span data-ttu-id="eac42-171">Monitor the cluster</span><span class="sxs-lookup"><span data-stu-id="eac42-171">Monitor the cluster</span></span>

<span data-ttu-id="eac42-172">The [az batchai cluster list](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-list), [az batchai cluster show](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-show), and [az batchai cluster node list](/cli/azure/batchai/cluster/node?view=azure-cli-latest#az-batchai-cluster-node-list) commands can be used to monitor various information for each of the clusters.</span><span class="sxs-lookup"><span data-stu-id="eac42-172">The [az batchai cluster list](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-list), [az batchai cluster show](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-show), and [az batchai cluster node list](/cli/azure/batchai/cluster/node?view=azure-cli-latest#az-batchai-cluster-node-list) commands can be used to monitor various information for each of the clusters.</span></span>

### <a name="list-all-clusters"></a><span data-ttu-id="eac42-173">List all clusters</span><span class="sxs-lookup"><span data-stu-id="eac42-173">List all clusters</span></span>

<span data-ttu-id="eac42-174">The following command list alls of the clusters in a workspace.</span><span class="sxs-lookup"><span data-stu-id="eac42-174">The following command list alls of the clusters in a workspace.</span></span>

```azurecli-interactive
az batchai cluster list \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> 
```

### <a name="show-information-about-a-cluster"></a><span data-ttu-id="eac42-175">Show information about a cluster</span><span class="sxs-lookup"><span data-stu-id="eac42-175">Show information about a cluster</span></span>

<span data-ttu-id="eac42-176">The following command shows the full information about a specific cluster in a table format.</span><span class="sxs-lookup"><span data-stu-id="eac42-176">The following command shows the full information about a specific cluster in a table format.</span></span>

```azurecli-interactive
az batchai cluster show \
    --name <CLUSTER NAME> \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> \
    --output table
```

<span data-ttu-id="eac42-177">If your cluster was provisioned using the auto storage option, you'll want to retrieve the storage account name to use when uploading scripts and training jobs.</span><span class="sxs-lookup"><span data-stu-id="eac42-177">If your cluster was provisioned using the auto storage option, you'll want to retrieve the storage account name to use when uploading scripts and training jobs.</span></span> <span data-ttu-id="eac42-178">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="eac42-178">Use the following command:</span></span>

```azurecli-interactive
az batchai cluster show \
    --name <CLUSTER NAME> \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> \
    --query "nodeSetup.mountVolumes.azureFileShares[0].{storageAccountName:accountName}"
```

<span data-ttu-id="eac42-179">The output should be similar to the following.</span><span class="sxs-lookup"><span data-stu-id="eac42-179">The output should be similar to the following.</span></span>

```JSON
{
  "storageAccountName": "baixxxxxxxxx"
}
```

### <a name="list-cluster-nodes"></a><span data-ttu-id="eac42-180">List cluster nodes</span><span class="sxs-lookup"><span data-stu-id="eac42-180">List cluster nodes</span></span>

<span data-ttu-id="eac42-181">If you need to connect to the cluster nodes, the following command retrieves the list of nodes and the connection information.</span><span class="sxs-lookup"><span data-stu-id="eac42-181">If you need to connect to the cluster nodes, the following command retrieves the list of nodes and the connection information.</span></span>  

```azurecli-interactive
az batchai cluster node list \
    --name <CLUSTER NAME> \
    --workspace <WORKSPACE> \
    --resource-group <RESOURCE GROUP> 
 ```

<span data-ttu-id="eac42-182">The output for each node will be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="eac42-182">The output for each node will be similar to the following:</span></span>

```JSON
[
  {
    "ipAddress": "40.68.xxx.xxx",
    "nodeId": "tvm-xxxxxxxxxx-xxxxxxxx",
    "port": 50000.0
  }
]
```
<span data-ttu-id="eac42-183">You can use this information to make an SSH connection to a node using a command similar to the following.</span><span class="sxs-lookup"><span data-stu-id="eac42-183">You can use this information to make an SSH connection to a node using a command similar to the following.</span></span>

```bash
ssh myusername@40.68.xxx.xxx -p 50000
``` 

## <a name="submit-jobs-to-the-cluster"></a><span data-ttu-id="eac42-184">Submit jobs to the cluster</span><span class="sxs-lookup"><span data-stu-id="eac42-184">Submit jobs to the cluster</span></span>

<span data-ttu-id="eac42-185">After provisioning the cluster, you can then submit jobs to run on the nodes.</span><span class="sxs-lookup"><span data-stu-id="eac42-185">After provisioning the cluster, you can then submit jobs to run on the nodes.</span></span> <span data-ttu-id="eac42-186">See the [az batchai job](/cli/azure/batchai/job?view=azure-cli-latest) command for different ways to prepare, submit, and monitor jobs using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="eac42-186">See the [az batchai job](/cli/azure/batchai/job?view=azure-cli-latest) command for different ways to prepare, submit, and monitor jobs using the Azure CLI.</span></span> 

## <a name="downscale-cluster-for-later-use"></a><span data-ttu-id="eac42-187">Downscale cluster for later use</span><span class="sxs-lookup"><span data-stu-id="eac42-187">Downscale cluster for later use</span></span>

<span data-ttu-id="eac42-188">Once you are finished running your jobs, you will want to downscale your cluster.</span><span class="sxs-lookup"><span data-stu-id="eac42-188">Once you are finished running your jobs, you will want to downscale your cluster.</span></span> <span data-ttu-id="eac42-189">It is recommended to always downscale clusters when they are not being used in order to save compute costs.</span><span class="sxs-lookup"><span data-stu-id="eac42-189">It is recommended to always downscale clusters when they are not being used in order to save compute costs.</span></span> <span data-ttu-id="eac42-190">Downscaling a cluster to 0 nodes allows you to stop your billing charges while not needing to reprovision the clusters in the future when you need to upscale again.</span><span class="sxs-lookup"><span data-stu-id="eac42-190">Downscaling a cluster to 0 nodes allows you to stop your billing charges while not needing to reprovision the clusters in the future when you need to upscale again.</span></span> <span data-ttu-id="eac42-191">If autoscaling was selected in cluster creation, the cluster should automatically downscale to the minimum target.</span><span class="sxs-lookup"><span data-stu-id="eac42-191">If autoscaling was selected in cluster creation, the cluster should automatically downscale to the minimum target.</span></span> <span data-ttu-id="eac42-192">If manual scaling was selected, downscale the cluster using the following command.</span><span class="sxs-lookup"><span data-stu-id="eac42-192">If manual scaling was selected, downscale the cluster using the following command.</span></span>

```azurecli-interactive
az batchai cluster resize \
    --name <CLUSTER NAME> \
    --resource-group <RESOURCE GROUP> \
    --workspace <WORKSPACE> \
    --target 0
```

## <a name="delete-a-cluster"></a><span data-ttu-id="eac42-193">Delete a cluster</span><span class="sxs-lookup"><span data-stu-id="eac42-193">Delete a cluster</span></span>

<span data-ttu-id="eac42-194">Once you are finished using a cluster, use the [az batchai cluster delete](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-delete) command to delete it.</span><span class="sxs-lookup"><span data-stu-id="eac42-194">Once you are finished using a cluster, use the [az batchai cluster delete](/cli/azure/batchai/cluster?view=azure-cli-latest#az-batchai-cluster-delete) command to delete it.</span></span>

```azurecli-interactive
az batchai cluster delete \
    --name <CLUSTER NAME> \
    --resource-group <RESOURCE GROUP> \
    --workspace <WORKSPACE>
```

<span data-ttu-id="eac42-195">Deleting your resource group also automatically deletes all clusters that were provisioned under that resource group.</span><span class="sxs-lookup"><span data-stu-id="eac42-195">Deleting your resource group also automatically deletes all clusters that were provisioned under that resource group.</span></span>

```azurecli-interactive
az group delete --name <RESOURCE GROUP>
```

## <a name="next-steps"></a><span data-ttu-id="eac42-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="eac42-196">Next steps</span></span>

<span data-ttu-id="eac42-197">For more examples of creating a Batch AI cluster, see the [Portal](quickstart-create-cluster-portal.md) or [Azure CLI](quickstart-create-cluster-cli.md) quickstart, or the [Batch AI recipes](https://github.com/Azure/BatchAI/tree/master/recipes) on GitHub.</span><span class="sxs-lookup"><span data-stu-id="eac42-197">For more examples of creating a Batch AI cluster, see the [Portal](quickstart-create-cluster-portal.md) or [Azure CLI](quickstart-create-cluster-cli.md) quickstart, or the [Batch AI recipes](https://github.com/Azure/BatchAI/tree/master/recipes) on GitHub.</span></span>
