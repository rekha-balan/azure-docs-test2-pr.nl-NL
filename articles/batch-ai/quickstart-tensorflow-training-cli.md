---
title: Azure Quickstart - Deep learning training - Azure CLI | Microsoft Docs
description: Quickstart - Quickly learn to train a TensorFlow deep learning neural network on a single GPU with Batch AI using the Azure CLI
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
ms.openlocfilehash: 99d864a5d519ce56a559bea4db7fe89a113e47b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867791"
---
# <a name="quickstart-train-a-deep-learning-model-with-batch-ai"></a><span data-ttu-id="88bf6-103">Quickstart: Train a deep learning model with Batch AI</span><span class="sxs-lookup"><span data-stu-id="88bf6-103">Quickstart: Train a deep learning model with Batch AI</span></span>

<span data-ttu-id="88bf6-104">This quickstart shows how to train a sample deep learning model on a GPU-enabled virtual machine managed by Batch AI.</span><span class="sxs-lookup"><span data-stu-id="88bf6-104">This quickstart shows how to train a sample deep learning model on a GPU-enabled virtual machine managed by Batch AI.</span></span> <span data-ttu-id="88bf6-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="88bf6-105">Batch AI is a managed service for data scientists and AI researchers to train AI and machine learning models at scale on clusters of Azure virtual machines.</span></span> 

<span data-ttu-id="88bf6-106">In this example, you use the Azure CLI to set up Batch AI to train an example [TensorFlow](https://www.tensorflow.org/) neural network on the [MNIST database](http://yann.lecun.com/exdb/mnist/) of handwritten digits.</span><span class="sxs-lookup"><span data-stu-id="88bf6-106">In this example, you use the Azure CLI to set up Batch AI to train an example [TensorFlow](https://www.tensorflow.org/) neural network on the [MNIST database](http://yann.lecun.com/exdb/mnist/) of handwritten digits.</span></span> <span data-ttu-id="88bf6-107">After completing this quickstart, you'll understand key concepts of using Batch AI to train an AI or machine learning model, and be ready to try training different models at larger scale.</span><span class="sxs-lookup"><span data-stu-id="88bf6-107">After completing this quickstart, you'll understand key concepts of using Batch AI to train an AI or machine learning model, and be ready to try training different models at larger scale.</span></span>

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="88bf6-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span><span class="sxs-lookup"><span data-stu-id="88bf6-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.38 or later.</span></span> <span data-ttu-id="88bf6-109">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="88bf6-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="88bf6-110">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="88bf6-110">If you need to install or upgrade, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="88bf6-111">This quickstart assumes you're running commands in a Bash shell, either in Cloud Shell or on your local computer.</span><span class="sxs-lookup"><span data-stu-id="88bf6-111">This quickstart assumes you're running commands in a Bash shell, either in Cloud Shell or on your local computer.</span></span> <span data-ttu-id="88bf6-112">If you already completed the quickstart to [create a Batch AI cluster with the Azure CLI](quickstart-create-cluster-cli.md), skip the first two steps to create a resource group and a Batch AI cluster.</span><span class="sxs-lookup"><span data-stu-id="88bf6-112">If you already completed the quickstart to [create a Batch AI cluster with the Azure CLI](quickstart-create-cluster-cli.md), skip the first two steps to create a resource group and a Batch AI cluster.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="88bf6-113">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="88bf6-113">Create a resource group</span></span>

<span data-ttu-id="88bf6-114">Create a resource group with the `az group create` command.</span><span class="sxs-lookup"><span data-stu-id="88bf6-114">Create a resource group with the `az group create` command.</span></span> <span data-ttu-id="88bf6-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="88bf6-115">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="88bf6-116">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span><span class="sxs-lookup"><span data-stu-id="88bf6-116">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span></span> <span data-ttu-id="88bf6-117">Be sure to choose the East US 2 location, or another location where the Batch AI service is available.</span><span class="sxs-lookup"><span data-stu-id="88bf6-117">Be sure to choose the East US 2 location, or another location where the Batch AI service is available.</span></span> 

```azurecli-interactive 
az group create \
    --name myResourceGroup \
    --location eastus2
```

## <a name="create-a-batch-ai-cluster"></a><span data-ttu-id="88bf6-118">Create a Batch AI cluster</span><span class="sxs-lookup"><span data-stu-id="88bf6-118">Create a Batch AI cluster</span></span>

<span data-ttu-id="88bf6-119">First, use the `az batchai workspace create` command to create a Batch AI *workspace*.</span><span class="sxs-lookup"><span data-stu-id="88bf6-119">First, use the `az batchai workspace create` command to create a Batch AI *workspace*.</span></span> <span data-ttu-id="88bf6-120">You need a workspace to organize your Batch AI clusters and other resources.</span><span class="sxs-lookup"><span data-stu-id="88bf6-120">You need a workspace to organize your Batch AI clusters and other resources.</span></span>

```azurecli-interactive
az batchai workspace create \
    --workspace myworkspace \
    --resource-group myResourceGroup
```

<span data-ttu-id="88bf6-121">To create a Batch AI cluster, use the `az batchai cluster create` command.</span><span class="sxs-lookup"><span data-stu-id="88bf6-121">To create a Batch AI cluster, use the `az batchai cluster create` command.</span></span> <span data-ttu-id="88bf6-122">The following example creates a one-node cluster with the following properties:</span><span class="sxs-lookup"><span data-stu-id="88bf6-122">The following example creates a one-node cluster with the following properties:</span></span>

* <span data-ttu-id="88bf6-123">Uses the NC6 VM size, which has one NVIDIA Tesla K80 GPU.</span><span class="sxs-lookup"><span data-stu-id="88bf6-123">Uses the NC6 VM size, which has one NVIDIA Tesla K80 GPU.</span></span> <span data-ttu-id="88bf6-124">Azure offers several VM sizes with different NVIDIA GPUs.</span><span class="sxs-lookup"><span data-stu-id="88bf6-124">Azure offers several VM sizes with different NVIDIA GPUs.</span></span>
* <span data-ttu-id="88bf6-125">Runs a default Ubuntu Server image designed to host container-based applications.</span><span class="sxs-lookup"><span data-stu-id="88bf6-125">Runs a default Ubuntu Server image designed to host container-based applications.</span></span> <span data-ttu-id="88bf6-126">You can run most training workloads on this distribution.</span><span class="sxs-lookup"><span data-stu-id="88bf6-126">You can run most training workloads on this distribution.</span></span> 
* <span data-ttu-id="88bf6-127">Adds a user account named *myusername*, and generates SSH keys if they don't already exist in the default key location (*~/.ssh*) in your local environment.</span><span class="sxs-lookup"><span data-stu-id="88bf6-127">Adds a user account named *myusername*, and generates SSH keys if they don't already exist in the default key location (*~/.ssh*) in your local environment.</span></span>

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

<span data-ttu-id="88bf6-128">The command output shows the cluster properties.</span><span class="sxs-lookup"><span data-stu-id="88bf6-128">The command output shows the cluster properties.</span></span> <span data-ttu-id="88bf6-129">It takes a few minutes to create and start the node.</span><span class="sxs-lookup"><span data-stu-id="88bf6-129">It takes a few minutes to create and start the node.</span></span> <span data-ttu-id="88bf6-130">To see the cluster status, run the `az batchai cluster show` command.</span><span class="sxs-lookup"><span data-stu-id="88bf6-130">To see the cluster status, run the `az batchai cluster show` command.</span></span>

```azurecli-interactive
az batchai cluster show \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --output table
```

<span data-ttu-id="88bf6-131">Early in cluster creation, output is similar to the following, showing the cluster is `resizing`:</span><span class="sxs-lookup"><span data-stu-id="88bf6-131">Early in cluster creation, output is similar to the following, showing the cluster is `resizing`:</span></span>

```bash
Name       Resource Group    Workspace    VM Size       State      Idle    Running    Preparing    Leaving    Unusable
---------  ----------------  -----------  ------------  -------  ------  ---------  -----------  ---------  ----------
mycluster  myResourceGroup   myworkspace  STANDARD_NC6  resizing      0          0            0          0           0

```

<span data-ttu-id="88bf6-132">Continue the following steps to upload the training script and create the training job while the cluster state changes.</span><span class="sxs-lookup"><span data-stu-id="88bf6-132">Continue the following steps to upload the training script and create the training job while the cluster state changes.</span></span> <span data-ttu-id="88bf6-133">The cluster is ready to run the training job when the state is `steady` and the single node is `Idle`.</span><span class="sxs-lookup"><span data-stu-id="88bf6-133">The cluster is ready to run the training job when the state is `steady` and the single node is `Idle`.</span></span>

## <a name="upload-training-script"></a><span data-ttu-id="88bf6-134">Upload training script</span><span class="sxs-lookup"><span data-stu-id="88bf6-134">Upload training script</span></span>

<span data-ttu-id="88bf6-135">Use the `az storage account create` command to create a storage account to store your training script and training output.</span><span class="sxs-lookup"><span data-stu-id="88bf6-135">Use the `az storage account create` command to create a storage account to store your training script and training output.</span></span>

```azurecli-interactive
az storage account create \
    --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus2 \
    --sku Standard_LRS
```

<span data-ttu-id="88bf6-136">Create an Azure file share called `myshare` in the account, using the `az storage share create` command:</span><span class="sxs-lookup"><span data-stu-id="88bf6-136">Create an Azure file share called `myshare` in the account, using the `az storage share create` command:</span></span>

```azurecli-interactive
az storage share create \
    --name myshare \
    --account-name mystorageaccount
```

<span data-ttu-id="88bf6-137">Use the `az storage directory create` command to create directories in the Azure file share.</span><span class="sxs-lookup"><span data-stu-id="88bf6-137">Use the `az storage directory create` command to create directories in the Azure file share.</span></span> <span data-ttu-id="88bf6-138">Create the `scripts` directory for the training script, and `logs` for training output:</span><span class="sxs-lookup"><span data-stu-id="88bf6-138">Create the `scripts` directory for the training script, and `logs` for training output:</span></span>

```azurecli-interactive
# Create /scripts directory in file share
az storage directory create \
    --name scripts \
    --share-name myshare \
    --account-name mystorageaccount

# Create /logs directory in file share 
az storage directory create \
    --name logs \
    --share-name myshare \
    --account-name mystorageaccount
```

<span data-ttu-id="88bf6-139">In your Bash shell, create a local working directory, and download the TensorFlow [convolutional.py](https://raw.githubusercontent.com/tensorflow/models/master/tutorials/image/mnist/convolutional.py) sample.</span><span class="sxs-lookup"><span data-stu-id="88bf6-139">In your Bash shell, create a local working directory, and download the TensorFlow [convolutional.py](https://raw.githubusercontent.com/tensorflow/models/master/tutorials/image/mnist/convolutional.py) sample.</span></span> <span data-ttu-id="88bf6-140">The Python script trains a convolutional neural network on the MNIST image set of 60,000 handwritten digits from 0 through 9.</span><span class="sxs-lookup"><span data-stu-id="88bf6-140">The Python script trains a convolutional neural network on the MNIST image set of 60,000 handwritten digits from 0 through 9.</span></span> <span data-ttu-id="88bf6-141">Then it tests the model on a set of test examples.</span><span class="sxs-lookup"><span data-stu-id="88bf6-141">Then it tests the model on a set of test examples.</span></span>

```bash
wget https://raw.githubusercontent.com/tensorflow/models/master/tutorials/image/mnist/convolutional.py
```

<span data-ttu-id="88bf6-142">Upload the script to the `scripts` directory in the share using the `az storage file upload` command.</span><span class="sxs-lookup"><span data-stu-id="88bf6-142">Upload the script to the `scripts` directory in the share using the `az storage file upload` command.</span></span>

```azurecli-interactive
az storage file upload \
    --share-name myshare \
    --path scripts \
    --source convolutional.py \
    --account-name mystorageaccount
```

## <a name="submit-training-job"></a><span data-ttu-id="88bf6-143">Submit training job</span><span class="sxs-lookup"><span data-stu-id="88bf6-143">Submit training job</span></span>

<span data-ttu-id="88bf6-144">First, create a Batch AI *experiment* in your workspace by using the `az batchai experiment create` command.</span><span class="sxs-lookup"><span data-stu-id="88bf6-144">First, create a Batch AI *experiment* in your workspace by using the `az batchai experiment create` command.</span></span> <span data-ttu-id="88bf6-145">An experiment is a logical container for related Batch AI jobs.</span><span class="sxs-lookup"><span data-stu-id="88bf6-145">An experiment is a logical container for related Batch AI jobs.</span></span>

```azurecli-interactive
az batchai experiment create \
    --name myexperiment \
    --workspace myworkspace \
    --resource-group myResourceGroup
```

<span data-ttu-id="88bf6-146">In your working directory, create a training job configuration file `job.json` with the following content.</span><span class="sxs-lookup"><span data-stu-id="88bf6-146">In your working directory, create a training job configuration file `job.json` with the following content.</span></span> <span data-ttu-id="88bf6-147">You pass this configuration file when you submit the training job.</span><span class="sxs-lookup"><span data-stu-id="88bf6-147">You pass this configuration file when you submit the training job.</span></span>

<span data-ttu-id="88bf6-148">This `job.json` file includes settings to locate the Python script file and run it in a TensorFlow container on the GPU node.</span><span class="sxs-lookup"><span data-stu-id="88bf6-148">This `job.json` file includes settings to locate the Python script file and run it in a TensorFlow container on the GPU node.</span></span> <span data-ttu-id="88bf6-149">It also specifies where to save the job's output files in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="88bf6-149">It also specifies where to save the job's output files in Azure storage.</span></span> <span data-ttu-id="88bf6-150">`<AZURE_BATCHAI_STORAGE_ACCOUNT>` indicates that the storage account name will be specified during the job submission.</span><span class="sxs-lookup"><span data-stu-id="88bf6-150">`<AZURE_BATCHAI_STORAGE_ACCOUNT>` indicates that the storage account name will be specified during the job submission.</span></span>

```json
{
    "$schema": "https://raw.githubusercontent.com/Azure/BatchAI/master/schemas/2018-05-01/job.json",
    "properties": {
        "nodeCount": 1,
        "tensorFlowSettings": {
            "pythonScriptFilePath": "$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare/scripts/convolutional.py"
        },
        "stdOutErrPathPrefix": "$AZ_BATCHAI_JOB_MOUNT_ROOT/myshare/logs",
        "mountVolumes": {
            "azureFileShares": [
                {
                    "azureFileUrl": "https://<AZURE_BATCHAI_STORAGE_ACCOUNT>.file.core.windows.net/myshare",
                    "relativeMountPath": "myshare"
                }
            ]
        },
        "containerSettings": {
            "imageSourceRegistry": {
                "image": "tensorflow/tensorflow:1.8.0-gpu"
            }
        }
    }
}
```

<span data-ttu-id="88bf6-151">Use the `az batchai job create` command to submit the job on the node, passing the `job.json` configuration file and the name of your storage account:</span><span class="sxs-lookup"><span data-stu-id="88bf6-151">Use the `az batchai job create` command to submit the job on the node, passing the `job.json` configuration file and the name of your storage account:</span></span>

```azurecli-interactive
az batchai job create \
    --name myjob \
    --cluster mycluster \
    --experiment myexperiment \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --config-file job.json \
    --storage-account-name mystorageaccount
```

<span data-ttu-id="88bf6-152">The command returns with the job properties, and then takes a couple of minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="88bf6-152">The command returns with the job properties, and then takes a couple of minutes to complete.</span></span> <span data-ttu-id="88bf6-153">To monitor this job's progress, use the `az batchai job file stream` command to stream the `stdout-wk-0.txt` file from the standard output directory on the node.</span><span class="sxs-lookup"><span data-stu-id="88bf6-153">To monitor this job's progress, use the `az batchai job file stream` command to stream the `stdout-wk-0.txt` file from the standard output directory on the node.</span></span> <span data-ttu-id="88bf6-154">The training script generates this file after the job starts running.</span><span class="sxs-lookup"><span data-stu-id="88bf6-154">The training script generates this file after the job starts running.</span></span>  

```azurecli-interactive
az batchai job file stream \
    --job myjob \
    --experiment myexperiment \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --file-name stdout-wk-0.txt
```

<span data-ttu-id="88bf6-155">Example output:</span><span class="sxs-lookup"><span data-stu-id="88bf6-155">Example output:</span></span>

```
File found with URL "https://mystorageaccount.file.core.windows.net/logs/00000000-0000-0000-0000-000000000000/myResourceGroup/workspaces/myworkspace/experiments/myexperiment/jobs/myjob/<JOB_ID>/stdouterr/stdout-wk-0.txt?sv=2016-05-31&sr=f&sig=Kih9baozMao8Ugos%2FVG%2BcsVsSeY1O%2FTocCNvLQhwtx4%3D&se=2018-06-20T22%3A07%3A30Z&sp=rl". Start streaming
Successfully downloaded train-images-idx3-ubyte.gz 9912422 bytes.
Successfully downloaded train-labels-idx1-ubyte.gz 28881 bytes.
Successfully downloaded t10k-images-idx3-ubyte.gz 1648877 bytes.
Successfully downloaded t10k-labels-idx1-ubyte.gz 4542 bytes.
Extracting data/train-images-idx3-ubyte.gz
Extracting data/train-labels-idx1-ubyte.gz
Extracting data/t10k-images-idx3-ubyte.gz
Extracting data/t10k-labels-idx1-ubyte.gz
Initialized!
Step 0 (epoch 0.00), 14.9 ms
Minibatch loss: 8.334, learning rate: 0.010000
Minibatch error: 85.9%
Validation error: 84.6%
Step 100 (epoch 0.12), 9.7 ms
Minibatch loss: 3.240, learning rate: 0.010000
Minibatch error: 6.2%
Validation error: 7.7%
Step 200 (epoch 0.23), 8.3 ms
Minibatch loss: 3.335, learning rate: 0.010000
Minibatch error: 7.8%
Validation error: 4.5%
Step 300 (epoch 0.35), 8.3 ms
Minibatch loss: 3.157, learning rate: 0.010000
Minibatch error: 3.1%
...
Step 8500 (epoch 9.89), 8.3 ms
Minibatch loss: 1.605, learning rate: 0.006302
Minibatch error: 0.0%
Validation error: 0.9%
Test error: 0.8%
```

<span data-ttu-id="88bf6-156">The streaming stops when the job completes.</span><span class="sxs-lookup"><span data-stu-id="88bf6-156">The streaming stops when the job completes.</span></span> <span data-ttu-id="88bf6-157">The sample script trains over 10 *epochs*, or passes through the training data set.</span><span class="sxs-lookup"><span data-stu-id="88bf6-157">The sample script trains over 10 *epochs*, or passes through the training data set.</span></span> <span data-ttu-id="88bf6-158">In this example, after 10 epochs, the trained model performs with a test error of only 0.8%.</span><span class="sxs-lookup"><span data-stu-id="88bf6-158">In this example, after 10 epochs, the trained model performs with a test error of only 0.8%.</span></span>

## <a name="get-job-output"></a><span data-ttu-id="88bf6-159">Get job output</span><span class="sxs-lookup"><span data-stu-id="88bf6-159">Get job output</span></span>

<span data-ttu-id="88bf6-160">Batch AI creates a unique folder structure in the storage account for each job's output.</span><span class="sxs-lookup"><span data-stu-id="88bf6-160">Batch AI creates a unique folder structure in the storage account for each job's output.</span></span> <span data-ttu-id="88bf6-161">Set the JOB_OUTPUT_PATH environment variable with this path.</span><span class="sxs-lookup"><span data-stu-id="88bf6-161">Set the JOB_OUTPUT_PATH environment variable with this path.</span></span> <span data-ttu-id="88bf6-162">Then, list the output files in storage using the `az storage file list` command:</span><span class="sxs-lookup"><span data-stu-id="88bf6-162">Then, list the output files in storage using the `az storage file list` command:</span></span>

```azurecli-interactive
export JOB_OUTPUT_PATH=$(az batchai job show --name myjob --experiment myexperiment --workspace myworkspace --resource-group myResourceGroup --query jobOutputDirectoryPathSegment --output tsv)

az storage file list \
    --share-name myshare/logs \
    --account-name mystorageaccount \
    --path $JOB_OUTPUT_PATH/stdouterr \
    --output table
```

<span data-ttu-id="88bf6-163">Output is similar to:</span><span class="sxs-lookup"><span data-stu-id="88bf6-163">Output is similar to:</span></span>

```
Name               Content Length  Type    Last Modified
---------------  ----------------  ------  ---------------
execution.log               14866  file
stderr-wk-0.txt              1527  file
stdout-wk-0.txt             11027  file
```

<span data-ttu-id="88bf6-164">Use the `az storage file download` command to download one or more files to your local working directory.</span><span class="sxs-lookup"><span data-stu-id="88bf6-164">Use the `az storage file download` command to download one or more files to your local working directory.</span></span> <span data-ttu-id="88bf6-165">For example:</span><span class="sxs-lookup"><span data-stu-id="88bf6-165">For example:</span></span>

```azurecli-interactive
az storage file download \
    --share-name myshare/logs \
    --account-name mystorageaccount \
    --path $JOB_OUTPUT_PATH/stdouterr/stdout-wk-0.txt
```

## <a name="clean-up-resources"></a><span data-ttu-id="88bf6-166">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="88bf6-166">Clean up resources</span></span>

<span data-ttu-id="88bf6-167">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace, cluster, and storage account created in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="88bf6-167">If you want to continue with Batch AI tutorials and samples, use the Batch AI workspace, cluster, and storage account created in this quickstart.</span></span> 

<span data-ttu-id="88bf6-168">You're charged for the Batch AI cluster while the nodes are running.</span><span class="sxs-lookup"><span data-stu-id="88bf6-168">You're charged for the Batch AI cluster while the nodes are running.</span></span> <span data-ttu-id="88bf6-169">If you want to keep the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span><span class="sxs-lookup"><span data-stu-id="88bf6-169">If you want to keep the cluster configuration when you have no jobs to run, resize the cluster to 0 nodes.</span></span> 

```azurecli-interactive
az batchai cluster resize \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup \
    --target 0
```

<span data-ttu-id="88bf6-170">Later, resize it to 1 or more nodes to run your jobs.</span><span class="sxs-lookup"><span data-stu-id="88bf6-170">Later, resize it to 1 or more nodes to run your jobs.</span></span> <span data-ttu-id="88bf6-171">When you no longer need a cluster, delete it with the `az batchai cluster delete` command:</span><span class="sxs-lookup"><span data-stu-id="88bf6-171">When you no longer need a cluster, delete it with the `az batchai cluster delete` command:</span></span>

```azurecli-interactive
az batchai cluster delete \
    --name mycluster \
    --workspace myworkspace \
    --resource-group myResourceGroup
```

<span data-ttu-id="88bf6-172">When no longer needed, you can use the `az group delete` command to remove the resource group for the Batch AI and storage resources.</span><span class="sxs-lookup"><span data-stu-id="88bf6-172">When no longer needed, you can use the `az group delete` command to remove the resource group for the Batch AI and storage resources.</span></span> 

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="88bf6-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="88bf6-173">Next steps</span></span>
<span data-ttu-id="88bf6-174">In this quickstart, you learned how to use Batch AI to train an example TensorFlow deep learning model on a single GPU VM, using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="88bf6-174">In this quickstart, you learned how to use Batch AI to train an example TensorFlow deep learning model on a single GPU VM, using the Azure CLI.</span></span> <span data-ttu-id="88bf6-175">To learn about how to distribute model training on a larger GPU cluster, continue to the Batch AI tutorial.</span><span class="sxs-lookup"><span data-stu-id="88bf6-175">To learn about how to distribute model training on a larger GPU cluster, continue to the Batch AI tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="88bf6-176">Distributed training tutorial</span><span class="sxs-lookup"><span data-stu-id="88bf6-176">Distributed training tutorial</span></span>](./tutorial-horovod-tensorflow.md)