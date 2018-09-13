---
title: Render a scene in the cloud - Azure Batch
description: Tutorial - How to render an Autodesk 3ds Max scene with Arnold using the Batch Rendering Service and Azure Command-Line Interface
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.topic: tutorial
ms.date: 04/19/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: 8dfec4c30a9610d8f30ceea131ebd7d2e1d64aa1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855928"
---
# <a name="tutorial-render-a-scene-with-azure-batch"></a><span data-ttu-id="84216-103">Tutorial: Render a scene with Azure Batch</span><span class="sxs-lookup"><span data-stu-id="84216-103">Tutorial: Render a scene with Azure Batch</span></span> 

<span data-ttu-id="84216-104">Azure Batch provides cloud-scale rendering capabilities on a pay-per-use basis.</span><span class="sxs-lookup"><span data-stu-id="84216-104">Azure Batch provides cloud-scale rendering capabilities on a pay-per-use basis.</span></span> <span data-ttu-id="84216-105">The Batch Rendering service supports rendering apps including Autodesk Maya, 3ds Max, Arnold, and V-Ray.</span><span class="sxs-lookup"><span data-stu-id="84216-105">The Batch Rendering service supports rendering apps including Autodesk Maya, 3ds Max, Arnold, and V-Ray.</span></span> <span data-ttu-id="84216-106">This tutorial shows you the steps to render a small scene with Batch using the Azure Command-Line Interface.</span><span class="sxs-lookup"><span data-stu-id="84216-106">This tutorial shows you the steps to render a small scene with Batch using the Azure Command-Line Interface.</span></span> <span data-ttu-id="84216-107">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="84216-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84216-108">Upload a scene to Azure storage</span><span class="sxs-lookup"><span data-stu-id="84216-108">Upload a scene to Azure storage</span></span>
> * <span data-ttu-id="84216-109">Create a Batch pool for rendering</span><span class="sxs-lookup"><span data-stu-id="84216-109">Create a Batch pool for rendering</span></span>
> * <span data-ttu-id="84216-110">Render a single-frame scene</span><span class="sxs-lookup"><span data-stu-id="84216-110">Render a single-frame scene</span></span>
> * <span data-ttu-id="84216-111">Scale the pool, and render a multi-frame scene</span><span class="sxs-lookup"><span data-stu-id="84216-111">Scale the pool, and render a multi-frame scene</span></span>
> * <span data-ttu-id="84216-112">Download rendered output</span><span class="sxs-lookup"><span data-stu-id="84216-112">Download rendered output</span></span>

<span data-ttu-id="84216-113">In this tutorial, you render a 3ds Max scene with Batch using the [Arnold](https://www.autodesk.com/products/arnold/overview) ray-tracing renderer.</span><span class="sxs-lookup"><span data-stu-id="84216-113">In this tutorial, you render a 3ds Max scene with Batch using the [Arnold](https://www.autodesk.com/products/arnold/overview) ray-tracing renderer.</span></span> 

[!INCLUDE [quickstarts-free-trial-note.md](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="84216-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="84216-114">Prerequisites</span></span>

<span data-ttu-id="84216-115">The sample 3ds Max scene for this tutorial is on [GitHub](https://github.com/Azure/azure-docs-cli-python-samples/tree/master/batch/render-scene), along with a sample Bash script and JSON configuration files.</span><span class="sxs-lookup"><span data-stu-id="84216-115">The sample 3ds Max scene for this tutorial is on [GitHub](https://github.com/Azure/azure-docs-cli-python-samples/tree/master/batch/render-scene), along with a sample Bash script and JSON configuration files.</span></span> <span data-ttu-id="84216-116">The 3ds Max scene is from the [Autodesk 3ds Max sample files](http://download.autodesk.com/us/support/files/3dsmax_sample_files/2017/Autodesk_3ds_Max_2017_English_Win_Samples_Files.exe).</span><span class="sxs-lookup"><span data-stu-id="84216-116">The 3ds Max scene is from the [Autodesk 3ds Max sample files](http://download.autodesk.com/us/support/files/3dsmax_sample_files/2017/Autodesk_3ds_Max_2017_English_Win_Samples_Files.exe).</span></span> <span data-ttu-id="84216-117">(Autodesk 3ds Max sample files are available under a Creative Commons Attribution-NonCommercial-Share Alike license.</span><span class="sxs-lookup"><span data-stu-id="84216-117">(Autodesk 3ds Max sample files are available under a Creative Commons Attribution-NonCommercial-Share Alike license.</span></span> <span data-ttu-id="84216-118">Copyright © Autodesk, Inc.)</span><span class="sxs-lookup"><span data-stu-id="84216-118">Copyright © Autodesk, Inc.)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="84216-119">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.20 or later.</span><span class="sxs-lookup"><span data-stu-id="84216-119">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.20 or later.</span></span> <span data-ttu-id="84216-120">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="84216-120">Run `az --version` to find the version.</span></span> <span data-ttu-id="84216-121">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="84216-121">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-batch-account"></a><span data-ttu-id="84216-122">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="84216-122">Create a Batch account</span></span>

<span data-ttu-id="84216-123">If you haven't already, create a resource group, a Batch account, and a linked storage account in your subscription.</span><span class="sxs-lookup"><span data-stu-id="84216-123">If you haven't already, create a resource group, a Batch account, and a linked storage account in your subscription.</span></span> 

<span data-ttu-id="84216-124">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span><span class="sxs-lookup"><span data-stu-id="84216-124">Create a resource group with the [az group create](/cli/azure/group#az-group-create) command.</span></span> <span data-ttu-id="84216-125">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span><span class="sxs-lookup"><span data-stu-id="84216-125">The following example creates a resource group named *myResourceGroup* in the *eastus2* location.</span></span>

```azurecli-interactive 
az group create \
    --name myResourceGroup \
    --location eastus2
```

<span data-ttu-id="84216-126">Create an Azure Storage account in your resource group with the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span><span class="sxs-lookup"><span data-stu-id="84216-126">Create an Azure Storage account in your resource group with the [az storage account create](/cli/azure/storage/account#az-storage-account-create) command.</span></span> <span data-ttu-id="84216-127">For this tutorial, you use the storage account to store an input 3ds Max scene and the rendered output.</span><span class="sxs-lookup"><span data-stu-id="84216-127">For this tutorial, you use the storage account to store an input 3ds Max scene and the rendered output.</span></span>

```azurecli-interactive
az storage account create \
    --resource-group myResourceGroup \
    --name mystorageaccount \
    --location eastus2 \
    --sku Standard_LRS
```
<span data-ttu-id="84216-128">Create a Batch account with the [az batch account create](/cli/azure/batch/account#az-batch-account-create) command.</span><span class="sxs-lookup"><span data-stu-id="84216-128">Create a Batch account with the [az batch account create](/cli/azure/batch/account#az-batch-account-create) command.</span></span> <span data-ttu-id="84216-129">The following example creates a Batch account named *mybatchaccount* in *myResourceGroup*, and links the storage account you created.</span><span class="sxs-lookup"><span data-stu-id="84216-129">The following example creates a Batch account named *mybatchaccount* in *myResourceGroup*, and links the storage account you created.</span></span>  

```azurecli-interactive 
az batch account create \
    --name mybatchaccount \
    --storage-account mystorageaccount \
    --resource-group myResourceGroup \
    --location eastus2
```

<span data-ttu-id="84216-130">To create and manage compute pools and jobs, you need to authenticate with Batch.</span><span class="sxs-lookup"><span data-stu-id="84216-130">To create and manage compute pools and jobs, you need to authenticate with Batch.</span></span> <span data-ttu-id="84216-131">Log in to the account with the [az batch account login](/cli/azure/batch/account#az-batch-account-login) command.</span><span class="sxs-lookup"><span data-stu-id="84216-131">Log in to the account with the [az batch account login](/cli/azure/batch/account#az-batch-account-login) command.</span></span> <span data-ttu-id="84216-132">After you log in, your `az batch` commands use this account context.</span><span class="sxs-lookup"><span data-stu-id="84216-132">After you log in, your `az batch` commands use this account context.</span></span> <span data-ttu-id="84216-133">The following example uses shared key authentication, based on the Batch account name and key.</span><span class="sxs-lookup"><span data-stu-id="84216-133">The following example uses shared key authentication, based on the Batch account name and key.</span></span> <span data-ttu-id="84216-134">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span><span class="sxs-lookup"><span data-stu-id="84216-134">Batch also supports authentication through [Azure Active Directory](batch-aad-auth.md), to authenticate individual users or an unattended application.</span></span>

```azurecli-interactive 
az batch account login \
    --name mybatchaccount \
    --resource-group myResourceGroup \
    --shared-key-auth
```
## <a name="upload-a-scene-to-storage"></a><span data-ttu-id="84216-135">Upload a scene to storage</span><span class="sxs-lookup"><span data-stu-id="84216-135">Upload a scene to storage</span></span>

<span data-ttu-id="84216-136">To upload the input scene to storage, you first need to access the storage account and create a destination container for the blobs.</span><span class="sxs-lookup"><span data-stu-id="84216-136">To upload the input scene to storage, you first need to access the storage account and create a destination container for the blobs.</span></span> <span data-ttu-id="84216-137">To access the Azure storage account, export the `AZURE_STORAGE_KEY` and `AZURE_STORAGE_ACCOUNT` environment variables.</span><span class="sxs-lookup"><span data-stu-id="84216-137">To access the Azure storage account, export the `AZURE_STORAGE_KEY` and `AZURE_STORAGE_ACCOUNT` environment variables.</span></span> <span data-ttu-id="84216-138">The first Bash shell command uses the [az storage account keys list](/cli/azure/storage/account/keys#az-storage-account-keys-list) command to get the first account key.</span><span class="sxs-lookup"><span data-stu-id="84216-138">The first Bash shell command uses the [az storage account keys list](/cli/azure/storage/account/keys#az-storage-account-keys-list) command to get the first account key.</span></span> <span data-ttu-id="84216-139">After you set these environment variables, your storage commands use this account context.</span><span class="sxs-lookup"><span data-stu-id="84216-139">After you set these environment variables, your storage commands use this account context.</span></span>

```azurecli-interactive
export AZURE_STORAGE_KEY=$(az storage account keys list --account-name mystorageaccount --resource-group myResourceGroup -o tsv --query [0].value)

export AZURE_STORAGE_ACCOUNT=mystorageaccount
```

<span data-ttu-id="84216-140">Now, create a blob container in the storage account for the scene files.</span><span class="sxs-lookup"><span data-stu-id="84216-140">Now, create a blob container in the storage account for the scene files.</span></span> <span data-ttu-id="84216-141">The following example uses the [az storage container create](/cli/azure/storage/container#az-storage-container-create) command to create a blob container named *scenefiles* that allows public read access.</span><span class="sxs-lookup"><span data-stu-id="84216-141">The following example uses the [az storage container create](/cli/azure/storage/container#az-storage-container-create) command to create a blob container named *scenefiles* that allows public read access.</span></span>

```azurecli-interactive
az storage container create \
    --public-access blob \
    --name scenefiles
```

<span data-ttu-id="84216-142">Download the scene `MotionBlur-Dragon-Flying.max` from [GitHub](https://github.com/Azure/azure-docs-cli-python-samples/raw/master/batch/render-scene/MotionBlur-DragonFlying.max) to a local working directory.</span><span class="sxs-lookup"><span data-stu-id="84216-142">Download the scene `MotionBlur-Dragon-Flying.max` from [GitHub](https://github.com/Azure/azure-docs-cli-python-samples/raw/master/batch/render-scene/MotionBlur-DragonFlying.max) to a local working directory.</span></span> <span data-ttu-id="84216-143">For example:</span><span class="sxs-lookup"><span data-stu-id="84216-143">For example:</span></span>

```azurecli-interactive
wget -O MotionBlur-DragonFlying.max https://github.com/Azure/azure-docs-cli-python-samples/raw/master/batch/render-scene/MotionBlur-DragonFlying.max
```

<span data-ttu-id="84216-144">Upload the scene file from your local working directory to the blob container.</span><span class="sxs-lookup"><span data-stu-id="84216-144">Upload the scene file from your local working directory to the blob container.</span></span> <span data-ttu-id="84216-145">The following example uses the [az storage blob upload-batch](/cli/azure/storage/blob#az-storage-blob-upload-batch) command, which can upload multiple files:</span><span class="sxs-lookup"><span data-stu-id="84216-145">The following example uses the [az storage blob upload-batch](/cli/azure/storage/blob#az-storage-blob-upload-batch) command, which can upload multiple files:</span></span>

```azurecli-interactive
az storage blob upload-batch \
    --destination scenefiles \
    --source ./
```

## <a name="create-a-rendering-pool"></a><span data-ttu-id="84216-146">Create a rendering pool</span><span class="sxs-lookup"><span data-stu-id="84216-146">Create a rendering pool</span></span>

<span data-ttu-id="84216-147">Create a Batch pool for rendering using the [az batch pool create](/cli/azure/batch/pool#az-batch-pool-create) command.</span><span class="sxs-lookup"><span data-stu-id="84216-147">Create a Batch pool for rendering using the [az batch pool create](/cli/azure/batch/pool#az-batch-pool-create) command.</span></span> <span data-ttu-id="84216-148">In this example, you specify the pool settings in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="84216-148">In this example, you specify the pool settings in a JSON file.</span></span> <span data-ttu-id="84216-149">Within your current shell, create a file name *mypool.json*, then copy and paste the following contents.</span><span class="sxs-lookup"><span data-stu-id="84216-149">Within your current shell, create a file name *mypool.json*, then copy and paste the following contents.</span></span> <span data-ttu-id="84216-150">Be sure all the text copies correctly.</span><span class="sxs-lookup"><span data-stu-id="84216-150">Be sure all the text copies correctly.</span></span> <span data-ttu-id="84216-151">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/mypool.json).)</span><span class="sxs-lookup"><span data-stu-id="84216-151">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/mypool.json).)</span></span>


```json
{
  "id": "myrenderpool",
  "vmSize": "standard_d2_v2",
  "virtualMachineConfiguration": {
    "imageReference": {
      "publisher": "batch",
      "offer": "rendering-windows2016",
      "sku": "rendering",
      "version": "1.2.1"
    },
    "nodeAgentSKUId": "batch.node.windows amd64"
  },
  "targetDedicatedNodes": 0,
  "targetLowPriorityNodes": 1,
  "enableAutoScale": false,
  "applicationLicenses":[
         "3dsmax",
         "arnold"
      ],
  "enableInterNodeCommunication": false 
}
```
<span data-ttu-id="84216-152">Batch supports dedicated nodes and [low-priority](batch-low-pri-vms.md) nodes, and you can use either or both in your pools.</span><span class="sxs-lookup"><span data-stu-id="84216-152">Batch supports dedicated nodes and [low-priority](batch-low-pri-vms.md) nodes, and you can use either or both in your pools.</span></span> <span data-ttu-id="84216-153">Dedicated nodes are reserved for your pool.</span><span class="sxs-lookup"><span data-stu-id="84216-153">Dedicated nodes are reserved for your pool.</span></span> <span data-ttu-id="84216-154">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span><span class="sxs-lookup"><span data-stu-id="84216-154">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span></span> <span data-ttu-id="84216-155">Low-priority nodes become unavailable if Azure does not have enough capacity.</span><span class="sxs-lookup"><span data-stu-id="84216-155">Low-priority nodes become unavailable if Azure does not have enough capacity.</span></span> 

<span data-ttu-id="84216-156">The pool specified contains a single low-priority node running a Windows Server image with software for the Batch Rendering service.</span><span class="sxs-lookup"><span data-stu-id="84216-156">The pool specified contains a single low-priority node running a Windows Server image with software for the Batch Rendering service.</span></span> <span data-ttu-id="84216-157">This pool is licensed to render with 3ds Max and Arnold.</span><span class="sxs-lookup"><span data-stu-id="84216-157">This pool is licensed to render with 3ds Max and Arnold.</span></span> <span data-ttu-id="84216-158">In a later step, you scale the pool to a larger number of nodes.</span><span class="sxs-lookup"><span data-stu-id="84216-158">In a later step, you scale the pool to a larger number of nodes.</span></span>

<span data-ttu-id="84216-159">Create the pool by passing the JSON file to the `az batch pool create` command:</span><span class="sxs-lookup"><span data-stu-id="84216-159">Create the pool by passing the JSON file to the `az batch pool create` command:</span></span>

```azurecli-interactive
az batch pool create \
    --json-file mypool.json
``` 
<span data-ttu-id="84216-160">It takes a few minutes to provision the pool.</span><span class="sxs-lookup"><span data-stu-id="84216-160">It takes a few minutes to provision the pool.</span></span> <span data-ttu-id="84216-161">To see the status of the pool, run the [az batch pool show](/cli/azure/batch/pool#az-batch-pool-show) command.</span><span class="sxs-lookup"><span data-stu-id="84216-161">To see the status of the pool, run the [az batch pool show](/cli/azure/batch/pool#az-batch-pool-show) command.</span></span> <span data-ttu-id="84216-162">The following command gets the allocation state of the pool:</span><span class="sxs-lookup"><span data-stu-id="84216-162">The following command gets the allocation state of the pool:</span></span>

```azurecli-interactive
az batch pool show \
    --pool-id myrenderpool \
    --query "allocationState"
```

<span data-ttu-id="84216-163">Continue the following steps to create a job and tasks while the pool state is changing.</span><span class="sxs-lookup"><span data-stu-id="84216-163">Continue the following steps to create a job and tasks while the pool state is changing.</span></span> <span data-ttu-id="84216-164">The pool is completely provisioned when the allocation state is `steady` and the nodes are running.</span><span class="sxs-lookup"><span data-stu-id="84216-164">The pool is completely provisioned when the allocation state is `steady` and the nodes are running.</span></span>  

## <a name="create-a-blob-container-for-output"></a><span data-ttu-id="84216-165">Create a blob container for output</span><span class="sxs-lookup"><span data-stu-id="84216-165">Create a blob container for output</span></span>

<span data-ttu-id="84216-166">In the examples in this tutorial, every task in the rendering job creates an output file.</span><span class="sxs-lookup"><span data-stu-id="84216-166">In the examples in this tutorial, every task in the rendering job creates an output file.</span></span> <span data-ttu-id="84216-167">Before scheduling the job, create a blob container in your storage account as the destination for the output files.</span><span class="sxs-lookup"><span data-stu-id="84216-167">Before scheduling the job, create a blob container in your storage account as the destination for the output files.</span></span> <span data-ttu-id="84216-168">The following example uses the [az storage container create](/cli/azure/storage/container#az-storage-container-create) command to create the *job-myrenderjob* container with public read access.</span><span class="sxs-lookup"><span data-stu-id="84216-168">The following example uses the [az storage container create](/cli/azure/storage/container#az-storage-container-create) command to create the *job-myrenderjob* container with public read access.</span></span> 

```azurecli-interactive
az storage container create \
    --public-access blob \
    --name job-myrenderjob
```

<span data-ttu-id="84216-169">To write output files to the container, Batch needs to use a Shared Access Signature (SAS) token.</span><span class="sxs-lookup"><span data-stu-id="84216-169">To write output files to the container, Batch needs to use a Shared Access Signature (SAS) token.</span></span> <span data-ttu-id="84216-170">Create the token with the [az storage account generate-sas](/cli/azure/storage/account#az-storage-account-generate-sas) command.</span><span class="sxs-lookup"><span data-stu-id="84216-170">Create the token with the [az storage account generate-sas](/cli/azure/storage/account#az-storage-account-generate-sas) command.</span></span> <span data-ttu-id="84216-171">This example creates a token to write to any blob container in the account, and the token expires on November 15, 2018:</span><span class="sxs-lookup"><span data-stu-id="84216-171">This example creates a token to write to any blob container in the account, and the token expires on November 15, 2018:</span></span>

```azurecli-interactive
az storage account generate-sas \
    --permissions w \
    --resource-types co \
    --services b \
    --expiry 2018-11-15
```

<span data-ttu-id="84216-172">Take note of the token returned by the command, which looks similar to the following.</span><span class="sxs-lookup"><span data-stu-id="84216-172">Take note of the token returned by the command, which looks similar to the following.</span></span> <span data-ttu-id="84216-173">You use this token in a later step.</span><span class="sxs-lookup"><span data-stu-id="84216-173">You use this token in a later step.</span></span>

```
se=2018-11-15&sp=rw&sv=2017-04-17&ss=b&srt=co&sig=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```

## <a name="render-a-single-frame-scene"></a><span data-ttu-id="84216-174">Render a single-frame scene</span><span class="sxs-lookup"><span data-stu-id="84216-174">Render a single-frame scene</span></span>

### <a name="create-a-job"></a><span data-ttu-id="84216-175">Create a job</span><span class="sxs-lookup"><span data-stu-id="84216-175">Create a job</span></span>

<span data-ttu-id="84216-176">Create a rendering job to run on the pool by using the [az batch job create](/cli/azure/batch/job#az-batch-job-create) command.</span><span class="sxs-lookup"><span data-stu-id="84216-176">Create a rendering job to run on the pool by using the [az batch job create](/cli/azure/batch/job#az-batch-job-create) command.</span></span> <span data-ttu-id="84216-177">Initially the job has no tasks.</span><span class="sxs-lookup"><span data-stu-id="84216-177">Initially the job has no tasks.</span></span>

```azurecli-interactive
az batch job create \
    --id myrenderjob \
    --pool-id myrenderpool
```

### <a name="create-a-task"></a><span data-ttu-id="84216-178">Create a task</span><span class="sxs-lookup"><span data-stu-id="84216-178">Create a task</span></span>

<span data-ttu-id="84216-179">Use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create a rendering task in the job.</span><span class="sxs-lookup"><span data-stu-id="84216-179">Use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create a rendering task in the job.</span></span> <span data-ttu-id="84216-180">In this example, you specify the task settings in a JSON file.</span><span class="sxs-lookup"><span data-stu-id="84216-180">In this example, you specify the task settings in a JSON file.</span></span> <span data-ttu-id="84216-181">Within your current shell, create a file named *myrendertask.json*, then copy and paste the following contents.</span><span class="sxs-lookup"><span data-stu-id="84216-181">Within your current shell, create a file named *myrendertask.json*, then copy and paste the following contents.</span></span> <span data-ttu-id="84216-182">Be sure all the text copies correctly.</span><span class="sxs-lookup"><span data-stu-id="84216-182">Be sure all the text copies correctly.</span></span> <span data-ttu-id="84216-183">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/myrendertask.json).)</span><span class="sxs-lookup"><span data-stu-id="84216-183">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/myrendertask.json).)</span></span>

<span data-ttu-id="84216-184">The task specifies a 3ds Max command to render a single frame of the scene *MotionBlur-DragonFlying.max*.</span><span class="sxs-lookup"><span data-stu-id="84216-184">The task specifies a 3ds Max command to render a single frame of the scene *MotionBlur-DragonFlying.max*.</span></span>

<span data-ttu-id="84216-185">Modify the `blobSource` and `containerURL` elements in the JSON file so that they include the name of your storage account and your SAS token.</span><span class="sxs-lookup"><span data-stu-id="84216-185">Modify the `blobSource` and `containerURL` elements in the JSON file so that they include the name of your storage account and your SAS token.</span></span> 

> [!TIP]
> <span data-ttu-id="84216-186">Your `containerURL` ends with your SAS token and is similar to:</span><span class="sxs-lookup"><span data-stu-id="84216-186">Your `containerURL` ends with your SAS token and is similar to:</span></span>
> 
> ```
> https://mystorageaccount.blob.core.windows.net/job-myrenderjob/$TaskOutput?se=2018-11-15&sp=rw&sv=2017-04-17&ss=b&srt=co&sig=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
> ```

```json
{
  "id": "myrendertask",
  "commandLine": "cmd /c \"%3DSMAX_2018%3dsmaxcmdio.exe -secure off -v:5 -rfw:0 -start:1 -end:1 -outputName:\"dragon.jpg\" -w 400 -h 300 MotionBlur-DragonFlying.max\"",
  "resourceFiles": [
    {
        "blobSource": "https://mystorageaccount.blob.core.windows.net/scenefiles/MotionBlur-DragonFlying.max",
        "filePath": "MotionBlur-DragonFlying.max"
    }
  ],
    "outputFiles": [
        {
            "filePattern": "dragon*.jpg",
            "destination": {
                "container": {
                    "containerUrl": "https://mystorageaccount.blob.core.windows.net/job-myrenderjob/myrendertask/$TaskOutput?Add_Your_SAS_Token_Here"
                }
            },
            "uploadOptions": {
                "uploadCondition": "TaskSuccess"
            }
        }
    ],
  "userIdentity": {
    "autoUser": {
      "scope": "task",
      "elevationLevel": "nonAdmin"
    }
  }
}
```

<span data-ttu-id="84216-187">Add the task to the job with the following command:</span><span class="sxs-lookup"><span data-stu-id="84216-187">Add the task to the job with the following command:</span></span>

```azurecli-interactive
az batch task create \
    --job-id myrenderjob \
    --json-file myrendertask.json
```

<span data-ttu-id="84216-188">Batch schedules the task, and the task runs as soon as a node in the pool is available.</span><span class="sxs-lookup"><span data-stu-id="84216-188">Batch schedules the task, and the task runs as soon as a node in the pool is available.</span></span>


### <a name="view-task-output"></a><span data-ttu-id="84216-189">View task output</span><span class="sxs-lookup"><span data-stu-id="84216-189">View task output</span></span>

<span data-ttu-id="84216-190">The task takes a few minutes to run.</span><span class="sxs-lookup"><span data-stu-id="84216-190">The task takes a few minutes to run.</span></span> <span data-ttu-id="84216-191">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view details about the task.</span><span class="sxs-lookup"><span data-stu-id="84216-191">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view details about the task.</span></span>

```azurecli-interactive
az batch task show \
    --job-id myrenderjob \
    --task-id myrendertask
```

<span data-ttu-id="84216-192">The task generates *dragon0001.jpg* on the compute node and uploads it to the *job-myrenderjob* container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="84216-192">The task generates *dragon0001.jpg* on the compute node and uploads it to the *job-myrenderjob* container in your storage account.</span></span> <span data-ttu-id="84216-193">To view the output, download the file from storage to your local computer using the [az storage blob download](/cli/azure/storage/blob#az-storage-blob-download) command.</span><span class="sxs-lookup"><span data-stu-id="84216-193">To view the output, download the file from storage to your local computer using the [az storage blob download](/cli/azure/storage/blob#az-storage-blob-download) command.</span></span>

```azurecli-interactive
az storage blob download \
    --container-name job-myrenderjob \
    --file dragon.jpg \
    --name dragon0001.jpg

```

<span data-ttu-id="84216-194">Open *dragon.jpg* on your computer.</span><span class="sxs-lookup"><span data-stu-id="84216-194">Open *dragon.jpg* on your computer.</span></span> <span data-ttu-id="84216-195">The rendered image looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="84216-195">The rendered image looks similar to the following:</span></span>

![Rendered dragon frame 1](./media/tutorial-rendering-cli/dragon-frame.png) 


## <a name="scale-the-pool"></a><span data-ttu-id="84216-197">Scale the pool</span><span class="sxs-lookup"><span data-stu-id="84216-197">Scale the pool</span></span>

<span data-ttu-id="84216-198">Now modify the pool to prepare for a larger rendering job, with multiple frames.</span><span class="sxs-lookup"><span data-stu-id="84216-198">Now modify the pool to prepare for a larger rendering job, with multiple frames.</span></span> <span data-ttu-id="84216-199">Batch provides a number of ways to scale the compute resources, including [autoscaling](batch-automatic-scaling.md) which adds or removes nodes as task demands change.</span><span class="sxs-lookup"><span data-stu-id="84216-199">Batch provides a number of ways to scale the compute resources, including [autoscaling](batch-automatic-scaling.md) which adds or removes nodes as task demands change.</span></span> <span data-ttu-id="84216-200">For this basic example, use the [az batch pool resize](/cli/azure/batch/pool#az-batch-pool-resize) command to increase the number of low-priority nodes in the pool to *6*:</span><span class="sxs-lookup"><span data-stu-id="84216-200">For this basic example, use the [az batch pool resize](/cli/azure/batch/pool#az-batch-pool-resize) command to increase the number of low-priority nodes in the pool to *6*:</span></span>

```azurecli-interactive
az batch pool resize --pool-id myrenderpool --target-dedicated-nodes 0 --target-low-priority-nodes 6
```

<span data-ttu-id="84216-201">The pool takes a few minutes to resize.</span><span class="sxs-lookup"><span data-stu-id="84216-201">The pool takes a few minutes to resize.</span></span> <span data-ttu-id="84216-202">While that process takes place, set up the next tasks to run in the existing rendering job.</span><span class="sxs-lookup"><span data-stu-id="84216-202">While that process takes place, set up the next tasks to run in the existing rendering job.</span></span>

## <a name="render-a-multiframe-scene"></a><span data-ttu-id="84216-203">Render a multiframe scene</span><span class="sxs-lookup"><span data-stu-id="84216-203">Render a multiframe scene</span></span>

<span data-ttu-id="84216-204">As in the single-frame example, use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create rendering tasks in the job named *myrenderjob*.</span><span class="sxs-lookup"><span data-stu-id="84216-204">As in the single-frame example, use the [az batch task create](/cli/azure/batch/task#az-batch-task-create) command to create rendering tasks in the job named *myrenderjob*.</span></span> <span data-ttu-id="84216-205">Here, specify the task settings in a JSON file called *myrendertask_multi.json*.</span><span class="sxs-lookup"><span data-stu-id="84216-205">Here, specify the task settings in a JSON file called *myrendertask_multi.json*.</span></span> <span data-ttu-id="84216-206">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/myrendertask_multi.json).) Each of the six tasks specifies an Arnold command line to render one frame of the 3ds Max scene *MotionBlur-DragonFlying.max*.</span><span class="sxs-lookup"><span data-stu-id="84216-206">(You can download the file from [GitHub](https://raw.githubusercontent.com/Azure/azure-docs-cli-python-samples/master/batch/render-scene/json/myrendertask_multi.json).) Each of the six tasks specifies an Arnold command line to render one frame of the 3ds Max scene *MotionBlur-DragonFlying.max*.</span></span>

<span data-ttu-id="84216-207">Create a file in your current shell named *myrendertask_multi.json*, and copy and paste the contents from the downloaded file.</span><span class="sxs-lookup"><span data-stu-id="84216-207">Create a file in your current shell named *myrendertask_multi.json*, and copy and paste the contents from the downloaded file.</span></span> <span data-ttu-id="84216-208">Modify the `blobSource` and `containerURL` elements in the JSON file to include the name of your storage account and your SAS token.</span><span class="sxs-lookup"><span data-stu-id="84216-208">Modify the `blobSource` and `containerURL` elements in the JSON file to include the name of your storage account and your SAS token.</span></span> <span data-ttu-id="84216-209">Be sure to change the settings for each of the six tasks.</span><span class="sxs-lookup"><span data-stu-id="84216-209">Be sure to change the settings for each of the six tasks.</span></span> <span data-ttu-id="84216-210">Save the file, and run the following command to queue the tasks:</span><span class="sxs-lookup"><span data-stu-id="84216-210">Save the file, and run the following command to queue the tasks:</span></span>

```azurecli-interactive
az batch task create --job-id myrenderjob --json-file myrendertask_multi.json
```

### <a name="view-task-output"></a><span data-ttu-id="84216-211">View task output</span><span class="sxs-lookup"><span data-stu-id="84216-211">View task output</span></span>

<span data-ttu-id="84216-212">The task takes a few minutes to run.</span><span class="sxs-lookup"><span data-stu-id="84216-212">The task takes a few minutes to run.</span></span> <span data-ttu-id="84216-213">Use the [az batch task list](/cli/azure/batch/task#az-batch-task-list) command to view the state of the tasks.</span><span class="sxs-lookup"><span data-stu-id="84216-213">Use the [az batch task list](/cli/azure/batch/task#az-batch-task-list) command to view the state of the tasks.</span></span> <span data-ttu-id="84216-214">For example:</span><span class="sxs-lookup"><span data-stu-id="84216-214">For example:</span></span>

```azurecli-interactive
az batch task list \
    --job-id myrenderjob \
    --output table
```

<span data-ttu-id="84216-215">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view details about individual tasks.</span><span class="sxs-lookup"><span data-stu-id="84216-215">Use the [az batch task show](/cli/azure/batch/task#az-batch-task-show) command to view details about individual tasks.</span></span> <span data-ttu-id="84216-216">For example:</span><span class="sxs-lookup"><span data-stu-id="84216-216">For example:</span></span>

```azurecli-interactive
az batch task show \
    --job-id myrenderjob \
    --task-id mymultitask1
```
 
<span data-ttu-id="84216-217">The tasks generate output files named *dragon0002.jpg* - *dragon0007.jpg* on the compute nodes and upload them to the *job-myrenderjob* container in your storage account.</span><span class="sxs-lookup"><span data-stu-id="84216-217">The tasks generate output files named *dragon0002.jpg* - *dragon0007.jpg* on the compute nodes and upload them to the *job-myrenderjob* container in your storage account.</span></span> <span data-ttu-id="84216-218">To view the output, download the files to a folder on your local computer using the [az storage blob download-batch](/cli/azure/storage/blob#az-storage-blob-download_batch) command.</span><span class="sxs-lookup"><span data-stu-id="84216-218">To view the output, download the files to a folder on your local computer using the [az storage blob download-batch](/cli/azure/storage/blob#az-storage-blob-download_batch) command.</span></span> <span data-ttu-id="84216-219">For example:</span><span class="sxs-lookup"><span data-stu-id="84216-219">For example:</span></span>

```azurecli-interactive
az storage blob download-batch \
    --source job-myrenderjob \
    --destination .
```

<span data-ttu-id="84216-220">Open one of the files on your computer.</span><span class="sxs-lookup"><span data-stu-id="84216-220">Open one of the files on your computer.</span></span> <span data-ttu-id="84216-221">Rendered frame 6 looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="84216-221">Rendered frame 6 looks similar to the following:</span></span>

![Rendered dragon frame 6](./media/tutorial-rendering-cli/dragon-frame6.png) 


## <a name="clean-up-resources"></a><span data-ttu-id="84216-223">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="84216-223">Clean up resources</span></span>

<span data-ttu-id="84216-224">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, Batch account, pools, and all related resources.</span><span class="sxs-lookup"><span data-stu-id="84216-224">When no longer needed, you can use the [az group delete](/cli/azure/group#az-group-delete) command to remove the resource group, Batch account, pools, and all related resources.</span></span> <span data-ttu-id="84216-225">Delete the resources as follows:</span><span class="sxs-lookup"><span data-stu-id="84216-225">Delete the resources as follows:</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="84216-226">Next steps</span><span class="sxs-lookup"><span data-stu-id="84216-226">Next steps</span></span>

<span data-ttu-id="84216-227">In this tutorial, you learned about how to:</span><span class="sxs-lookup"><span data-stu-id="84216-227">In this tutorial, you learned about how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="84216-228">Upload scenes to Azure storage</span><span class="sxs-lookup"><span data-stu-id="84216-228">Upload scenes to Azure storage</span></span>
> * <span data-ttu-id="84216-229">Create a Batch pool for rendering</span><span class="sxs-lookup"><span data-stu-id="84216-229">Create a Batch pool for rendering</span></span>
> * <span data-ttu-id="84216-230">Render a single-frame scene with Arnold</span><span class="sxs-lookup"><span data-stu-id="84216-230">Render a single-frame scene with Arnold</span></span>
> * <span data-ttu-id="84216-231">Scale the pool, and render a multi-frame scene</span><span class="sxs-lookup"><span data-stu-id="84216-231">Scale the pool, and render a multi-frame scene</span></span>
> * <span data-ttu-id="84216-232">Download rendered output</span><span class="sxs-lookup"><span data-stu-id="84216-232">Download rendered output</span></span>

<span data-ttu-id="84216-233">To learn more about cloud-scale rendering, see the options for the Batch Rendering service.</span><span class="sxs-lookup"><span data-stu-id="84216-233">To learn more about cloud-scale rendering, see the options for the Batch Rendering service.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="84216-234">Batch Rendering service</span><span class="sxs-lookup"><span data-stu-id="84216-234">Batch Rendering service</span></span>](batch-rendering-service.md)
