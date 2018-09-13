---
title: Azure Quickstart - Create Batch AI cluster - Azure CLI | Microsoft Docs
description: Quickstart - Create a Batch AI cluster for training machine learning and AI models - Azure CLI
services: batch-ai
documentationcenter: na
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.custom: ''
ms.service: batch-ai
ms.workload: ''
ms.tgt_pltfrm: na
ms.devlang: CLI
ms.topic: quickstart
ms.date: 09/03/2018
ms.author: danlep
ms.openlocfilehash: 0d4ba7edfb22a6710222c854ceb2bf86284d2d77
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868579"
---
# <a name="quickstart-create-a-cluster-for-batch-ai-training-jobs-using-the-azure-cli"></a><span data-ttu-id="b7238-103">Quickstart: Create a cluster for Batch AI training jobs using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b7238-103">Quickstart: Create a cluster for Batch AI training jobs using the Azure CLI</span></span>

<span data-ttu-id="b7238-104">This quickstart shows how to use the Azure CLI to create a Batch AI cluster you can use for training AI and machine learning models.</span><span class="sxs-lookup"><span data-stu-id="b7238-104">This quickstart shows how to use the Azure CLI to create a Batch AI cluster you can use for training AI and machine learning models.</span></span> <span data-ttu-id="b7238-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b7238-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span></span>

<span data-ttu-id="b7238-106">The cluster initially has a single GPU node.</span><span class="sxs-lookup"><span data-stu-id="b7238-106">The cluster initially has a single GPU node.</span></span> <span data-ttu-id="b7238-107">After completing this quickstart, you'll have a cluster you can scale up and use to train your models.</span><span class="sxs-lookup"><span data-stu-id="b7238-107">After completing this quickstart, you'll have a cluster you can scale up and use to train your models.</span></span> <span data-ttu-id="b7238-108">Submit training jobs to the cluster using Batch AI, [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) tools, or the [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai).</span><span class="sxs-lookup"><span data-stu-id="b7238-108">Submit training jobs to the cluster using Batch AI, [Azure Machine Learning](../machine-learning/service/overview-what-is-azure-ml.md) tools, or the [Visual Studio Tools for AI](https://github.com/Microsoft/vs-tools-for-ai).</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="b7238-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="b7238-109">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="b7238-110">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="b7238-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="b7238-111">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="b7238-111">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="b7238-112">This quickstart assumes you're running commands in a Bash shell, either in Cloud Shell or on your local computer.</span><span class="sxs-lookup"><span data-stu-id="b7238-112">This quickstart assumes you're running commands in a Bash shell, either in Cloud Shell or on your local computer.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="b7238-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="b7238-113">Create a resource group</span></span>

<span data-ttu-id="b7238-114">Create a resource group with the `az group create` command.</span><span class="sxs-lookup"><span data-stu-id="b7238-114">Create a resource group with the `az group create` command.</span></span> <span data-ttu-id="b7238-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="b7238-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="b7238-116">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span><span class="sxs-lookup"><span data-stu-id="b7238-116">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span></span> <span data-ttu-id="b7238-117">Be sure to choose a location such as East US 2 in which the Batch AI service is available.</span><span class="sxs-lookup"><span data-stu-id="b7238-117">Be sure to choose a location such as East US 2 in which the Batch AI service is available.</span></span>

```azurecli-interactive 
az group create \
    --name myResourceGroup \
    --location eastus2
```

## <a name="create-a-batch-ai-cluster"></a><span data-ttu-id="b7238-118">Create a Batch AI cluster</span><span class="sxs-lookup"><span data-stu-id="b7238-118">Create a Batch AI cluster</span></span>

<span data-ttu-id="b7238-119">First, use the `az batchai workspace create` command to create a Batch AI *workspace*.</span><span class="sxs-lookup"><span data-stu-id="b7238-119">First, use the `az batchai workspace create` command to create a Batch AI *workspace*.</span></span> <span data-ttu-id="b7238-120">You need a workspace to organize your Batch AI clusters and other resources.</span><span class="sxs-lookup"><span data-stu-id="b7238-120">You need a workspace to organize your Batch AI clusters and other resources.</span></span>

```azurecli-interactive
az batchai workspace create \
    --workspace myworkspace \
    --resource-group myResourceGroup 
```

<span data-ttu-id="b7238-121">To create a Batch AI cluster, use the `az batchai cluster create` command.</span><span class="sxs-lookup"><span data-stu-id="b7238-121">To create a Batch AI cluster, use the `az batchai cluster create` command.</span></span> <span data-ttu-id="b7238-122">The following example creates a cluster with the following properties:</span><span class="sxs-lookup"><span data-stu-id="b7238-122">The following example creates a cluster with the following properties:</span></span>

* <span data-ttu-id="b7238-123">Contains a single node in the NC6 VM size, which has one NVIDIA Tesla K80 GPU.</span><span class="sxs-lookup"><span data-stu-id="b7238-123">Contains a single node in the NC6 VM size, which has one NVIDIA Tesla K80 GPU.</span></span> 
* <span data-ttu-id="b7238-124">Runs a default Ubuntu Server image designed to host container-based applications, which you can use for most training workloads.</span><span class="sxs-lookup"><span data-stu-id="b7238-124">Runs a default Ubuntu Server image designed to host container-based applications, which you can use for most training workloads.</span></span> 
* <span data-ttu-id="b7238-125">Adds a user account named *myusername*, and generates SSH keys if they don't already exist in the default key location (*~/.ssh*) in your local environment.</span><span class="sxs-lookup"><span data-stu-id="b7238-125">Adds a user account named *myusername*, and generates SSH keys if they don't already exist in the default key location (*~/.ssh*) in your local environment.</span></span> 

```azurecli-interactive
az batchai cluster create \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --vm-size Standard_NC6 \
    --target 1 \
    --user-name myusername \
    --generate-ssh-keys
```

<span data-ttu-id="b7238-126">The command output shows the cluster properties.</span><span class="sxs-lookup"><span data-stu-id="b7238-126">The command output shows the cluster properties.</span></span> <span data-ttu-id="b7238-127">It takes a few minutes to create and start the node.</span><span class="sxs-lookup"><span data-stu-id="b7238-127">It takes a few minutes to create and start the node.</span></span> <span data-ttu-id="b7238-128">To see the status of the cluster, run the `az batchai cluster show` command.</span><span class="sxs-lookup"><span data-stu-id="b7238-128">To see the status of the cluster, run the `az batchai cluster show` command.</span></span> 

```azurecli-interactive
az batchai cluster show \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --output table
```

<span data-ttu-id="b7238-129">Early in cluster creation, output is similar to the following, showing the cluster is in the `resizing` state:</span><span class="sxs-lookup"><span data-stu-id="b7238-129">Early in cluster creation, output is similar to the following, showing the cluster is in the `resizing` state:</span></span>

```bash
Name       Resource Group    Workspace    VM Size       State      Idle    Running    Preparing    Leaving    Unusable
---------  ----------------  -----------  ------------  -------  ------  ---------  -----------  ---------  ----------
mycluster  myResourceGroup   myworkspace  STANDARD_NC6  resizing      0          0            0          0           0

```
<span data-ttu-id="b7238-130">The cluster is ready to use when the state is `steady` and the single node is `Idle`.</span><span class="sxs-lookup"><span data-stu-id="b7238-130">The cluster is ready to use when the state is `steady` and the single node is `Idle`.</span></span>

## <a name="list-cluster-nodes"></a><span data-ttu-id="b7238-131">List cluster nodes</span><span class="sxs-lookup"><span data-stu-id="b7238-131">List cluster nodes</span></span> 

<span data-ttu-id="b7238-132">If you need to connect to the cluster nodes (in this case, a single node) to install applications or perform maintenance, get connection information by running the `az batchai cluster node list` command:</span><span class="sxs-lookup"><span data-stu-id="b7238-132">If you need to connect to the cluster nodes (in this case, a single node) to install applications or perform maintenance, get connection information by running the `az batchai cluster node list` command:</span></span>


```azurecli-interactive
az batchai cluster node list \
    --cluster mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup 
 ```

<span data-ttu-id="b7238-133">JSON output is similar to:</span><span class="sxs-lookup"><span data-stu-id="b7238-133">JSON output is similar to:</span></span>

```JSON
[
  {
    "ipAddress": "40.68.254.143",
    "nodeId": "tvm-1816144089_1-20180626t233430z",
    "port": 50000.0
  }
]
```
<span data-ttu-id="b7238-134">Use this information to make an SSH connection to the node.</span><span class="sxs-lookup"><span data-stu-id="b7238-134">Use this information to make an SSH connection to the node.</span></span> <span data-ttu-id="b7238-135">For example, substitute the correct IP address of your node in the following command:</span><span class="sxs-lookup"><span data-stu-id="b7238-135">For example, substitute the correct IP address of your node in the following command:</span></span>

```bash
ssh myusername@40.68.254.143 -p 50000
``` 
<span data-ttu-id="b7238-136">Exit the SSH session to continue.</span><span class="sxs-lookup"><span data-stu-id="b7238-136">Exit the SSH session to continue.</span></span>

## <a name="resize-the-cluster"></a><span data-ttu-id="b7238-137">Resize the cluster</span><span class="sxs-lookup"><span data-stu-id="b7238-137">Resize the cluster</span></span>

<span data-ttu-id="b7238-138">When you use your cluster to run a training job, you might need more compute resources.</span><span class="sxs-lookup"><span data-stu-id="b7238-138">When you use your cluster to run a training job, you might need more compute resources.</span></span> <span data-ttu-id="b7238-139">For example, to increase the size to 2 nodes for a distributed training job, run the [batch ai cluster resize](/cli/azure/batchai/cluster#az-batchai-cluster-resize) command:</span><span class="sxs-lookup"><span data-stu-id="b7238-139">For example, to increase the size to 2 nodes for a distributed training job, run the [batch ai cluster resize](/cli/azure/batchai/cluster#az-batchai-cluster-resize) command:</span></span>

```azurecli-interactive
az batchai cluster resize \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --target 2
```

<span data-ttu-id="b7238-140">It takes a few minutes for the cluster to resize.</span><span class="sxs-lookup"><span data-stu-id="b7238-140">It takes a few minutes for the cluster to resize.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="b7238-141">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="b7238-141">Clean up resources</span></span>

<span data-ttu-id="b7238-142">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="b7238-142">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace created in this quickstart.</span></span> 

<span data-ttu-id="b7238-143">You're charged for the Batch AI cluster while the nodes are running.</span><span class="sxs-lookup"><span data-stu-id="b7238-143">You're charged for the Batch AI cluster while the nodes are running.</span></span> <span data-ttu-id="b7238-144">If you want to keep the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span><span class="sxs-lookup"><span data-stu-id="b7238-144">If you want to keep the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span></span> 

```azurecli-interactive
az batchai cluster resize \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --target 0
```

<span data-ttu-id="b7238-145">Later, resize it to 1 or more nodes to run your jobs.</span><span class="sxs-lookup"><span data-stu-id="b7238-145">Later, resize it to 1 or more nodes to run your jobs.</span></span> <span data-ttu-id="b7238-146">When you no longer need a cluster, delete it with the `az batchai cluster delete` command:</span><span class="sxs-lookup"><span data-stu-id="b7238-146">When you no longer need a cluster, delete it with the `az batchai cluster delete` command:</span></span>

```azurecli-interactive
az batchai cluster delete \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
```

<span data-ttu-id="b7238-147">When no longer needed, you can use the `az group delete` command to remove the resource group for the Batch AI resources.</span><span class="sxs-lookup"><span data-stu-id="b7238-147">When no longer needed, you can use the `az group delete` command to remove the resource group for the Batch AI resources.</span></span> 

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="b7238-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="b7238-148">Next steps</span></span>

<span data-ttu-id="b7238-149">In this quickstart, you learned how to create a Batch AI cluster, using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b7238-149">In this quickstart, you learned how to create a Batch AI cluster, using the Azure CLI.</span></span> <span data-ttu-id="b7238-150">To learn about how to use a Batch AI cluster to train a model, continue to the quickstart for training a deep learning model.</span><span class="sxs-lookup"><span data-stu-id="b7238-150">To learn about how to use a Batch AI cluster to train a model, continue to the quickstart for training a deep learning model.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b7238-151">Train a deep learning model</span><span class="sxs-lookup"><span data-stu-id="b7238-151">Train a deep learning model</span></span>](./quickstart-tensorflow-training-cli.md)
