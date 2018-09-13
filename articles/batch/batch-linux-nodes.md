---
title: Run Linux on virtual machine compute nodes - Azure Batch | Microsoft Docs
description: Learn how to process your parallel compute workloads on pools of Linux virtual machines in Azure Batch.
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: ''
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a3858428439e4671489bfc17b043daacc4d3f157
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556575"
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="1dd83-103">Provision Linux compute nodes in Batch pools</span><span class="sxs-lookup"><span data-stu-id="1dd83-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="1dd83-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span><span class="sxs-lookup"><span data-stu-id="1dd83-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="1dd83-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span><span class="sxs-lookup"><span data-stu-id="1dd83-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="1dd83-106">[Application packages](batch-application-packages.md) are currently unsupported on Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-106">[Application packages](batch-application-packages.md) are currently unsupported on Linux compute nodes.</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="1dd83-107">Virtual machine configuration</span><span class="sxs-lookup"><span data-stu-id="1dd83-107">Virtual machine configuration</span></span>
<span data-ttu-id="1dd83-108">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span><span class="sxs-lookup"><span data-stu-id="1dd83-108">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="1dd83-109">**Cloud Services Configuration** provides Windows compute nodes *only*.</span><span class="sxs-lookup"><span data-stu-id="1dd83-109">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="1dd83-110">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="1dd83-110">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="1dd83-111">When you create a pool that contains Azure Cloud Services nodes, you need to specify only the node size and its "OS family," which are found in the previously mentioned articles.</span><span class="sxs-lookup"><span data-stu-id="1dd83-111">When you create a pool that contains Azure Cloud Services nodes, you need to specify only the node size and its "OS family," which are found in the previously mentioned articles.</span></span> <span data-ttu-id="1dd83-112">For pools of Windows compute nodes, Cloud Services is most commonly used.</span><span class="sxs-lookup"><span data-stu-id="1dd83-112">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="1dd83-113">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-113">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="1dd83-114">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="1dd83-114">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="1dd83-115">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-115">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="1dd83-116">Virtual machine image reference</span><span class="sxs-lookup"><span data-stu-id="1dd83-116">Virtual machine image reference</span></span>
<span data-ttu-id="1dd83-117">The Batch service uses [Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-117">The Batch service uses [Virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide Linux compute nodes.</span></span> <span data-ttu-id="1dd83-118">The operating system images for these virtual machines are provided by the [Azure Marketplace][vm_marketplace].</span><span class="sxs-lookup"><span data-stu-id="1dd83-118">The operating system images for these virtual machines are provided by the [Azure Marketplace][vm_marketplace].</span></span> <span data-ttu-id="1dd83-119">When you configure a virtual machine image reference, you specify the properties of a Marketplace virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="1dd83-119">When you configure a virtual machine image reference, you specify the properties of a Marketplace virtual machine image.</span></span> <span data-ttu-id="1dd83-120">The following properties are required when you create a virtual machine image reference:</span><span class="sxs-lookup"><span data-stu-id="1dd83-120">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="1dd83-121">**Image reference properties**</span><span class="sxs-lookup"><span data-stu-id="1dd83-121">**Image reference properties**</span></span> | <span data-ttu-id="1dd83-122">**Example**</span><span class="sxs-lookup"><span data-stu-id="1dd83-122">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="1dd83-123">Publisher</span><span class="sxs-lookup"><span data-stu-id="1dd83-123">Publisher</span></span> |<span data-ttu-id="1dd83-124">Canonical</span><span class="sxs-lookup"><span data-stu-id="1dd83-124">Canonical</span></span> |
| <span data-ttu-id="1dd83-125">Offer</span><span class="sxs-lookup"><span data-stu-id="1dd83-125">Offer</span></span> |<span data-ttu-id="1dd83-126">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-126">UbuntuServer</span></span> |
| <span data-ttu-id="1dd83-127">SKU</span><span class="sxs-lookup"><span data-stu-id="1dd83-127">SKU</span></span> |<span data-ttu-id="1dd83-128">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="1dd83-128">14.04.4-LTS</span></span> |
| <span data-ttu-id="1dd83-129">Version</span><span class="sxs-lookup"><span data-stu-id="1dd83-129">Version</span></span> |<span data-ttu-id="1dd83-130">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-130">latest</span></span> |

> [!TIP]
> <span data-ttu-id="1dd83-131">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="1dd83-131">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="1dd83-132">Note that not all Marketplace images are currently compatible with Batch.</span><span class="sxs-lookup"><span data-stu-id="1dd83-132">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="1dd83-133">For more information, see [Node agent SKU](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="1dd83-133">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="1dd83-134">Node agent SKU</span><span class="sxs-lookup"><span data-stu-id="1dd83-134">Node agent SKU</span></span>
<span data-ttu-id="1dd83-135">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span><span class="sxs-lookup"><span data-stu-id="1dd83-135">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="1dd83-136">There are different implementations of the node agent, known as SKUs, for different operating systems.</span><span class="sxs-lookup"><span data-stu-id="1dd83-136">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="1dd83-137">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span><span class="sxs-lookup"><span data-stu-id="1dd83-137">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="1dd83-138">Typically, each node agent SKU is compatible with multiple virtual machine images.</span><span class="sxs-lookup"><span data-stu-id="1dd83-138">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="1dd83-139">Here are a few examples of node agent SKUs:</span><span class="sxs-lookup"><span data-stu-id="1dd83-139">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="1dd83-140">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1dd83-140">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="1dd83-141">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-141">batch.node.centos 7</span></span>
* <span data-ttu-id="1dd83-142">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-142">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1dd83-143">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span><span class="sxs-lookup"><span data-stu-id="1dd83-143">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="1dd83-144">You must use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span><span class="sxs-lookup"><span data-stu-id="1dd83-144">You must use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="1dd83-145">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information.</span><span class="sxs-lookup"><span data-stu-id="1dd83-145">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="1dd83-146">Create a Linux pool: Batch Python</span><span class="sxs-lookup"><span data-stu-id="1dd83-146">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="1dd83-147">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-147">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="1dd83-148">Reference documentation for the Batch Python module can be found at [azure.batch package ][py_batch_docs] on Read the Docs.</span><span class="sxs-lookup"><span data-stu-id="1dd83-148">Reference documentation for the Batch Python module can be found at [azure.batch package ][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="1dd83-149">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span><span class="sxs-lookup"><span data-stu-id="1dd83-149">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="1dd83-150">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span><span class="sxs-lookup"><span data-stu-id="1dd83-150">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

```python
# Import the required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize the Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure the start task for the pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies the Marketplace
# virtual machine image to install on the nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="1dd83-151">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span><span class="sxs-lookup"><span data-stu-id="1dd83-151">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="1dd83-152">The following Python snippet shows usage of this method.</span><span class="sxs-lookup"><span data-stu-id="1dd83-152">The following Python snippet shows usage of this method.</span></span>

```python
# Get the list of node agents from the Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain the desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick the first image reference from the list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create the VirtualMachineConfiguration, specifying the VM image
# reference and the Batch node agent to be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="1dd83-153">Create a Linux pool: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="1dd83-153">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="1dd83-154">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-154">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="1dd83-155">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span><span class="sxs-lookup"><span data-stu-id="1dd83-155">You can find the [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="1dd83-156">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span><span class="sxs-lookup"><span data-stu-id="1dd83-156">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="1dd83-157">This technique is desirable because the list of supported combinations may change from time to time.</span><span class="sxs-lookup"><span data-stu-id="1dd83-157">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="1dd83-158">Most commonly, supported combinations are added.</span><span class="sxs-lookup"><span data-stu-id="1dd83-158">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us to select from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image
// that we wish to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.SkuId.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the VirtualMachineConfiguration for use when actually
// creating the pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(
        imageReference: imageReference,
        nodeAgentSkuId: ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicated: nodeCount);

// Commit the pool to the Batch service
pool.Commit();
```

<span data-ttu-id="1dd83-159">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span><span class="sxs-lookup"><span data-stu-id="1dd83-159">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    skuId: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="1dd83-160">List of virtual machine images</span><span class="sxs-lookup"><span data-stu-id="1dd83-160">List of virtual machine images</span></span>
<span data-ttu-id="1dd83-161">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span><span class="sxs-lookup"><span data-stu-id="1dd83-161">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="1dd83-162">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span><span class="sxs-lookup"><span data-stu-id="1dd83-162">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="1dd83-163">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span><span class="sxs-lookup"><span data-stu-id="1dd83-163">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="1dd83-164">The following list may change at any time.</span><span class="sxs-lookup"><span data-stu-id="1dd83-164">The following list may change at any time.</span></span> <span data-ttu-id="1dd83-165">Always use the **list node agent SKU** methods available in the Batch APIs to list and then select from the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span><span class="sxs-lookup"><span data-stu-id="1dd83-165">Always use the **list node agent SKU** methods available in the Batch APIs to list and then select from the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="1dd83-166">**Publisher**</span><span class="sxs-lookup"><span data-stu-id="1dd83-166">**Publisher**</span></span> | <span data-ttu-id="1dd83-167">**Offer**</span><span class="sxs-lookup"><span data-stu-id="1dd83-167">**Offer**</span></span> | <span data-ttu-id="1dd83-168">**Image SKU**</span><span class="sxs-lookup"><span data-stu-id="1dd83-168">**Image SKU**</span></span> | <span data-ttu-id="1dd83-169">**Version**</span><span class="sxs-lookup"><span data-stu-id="1dd83-169">**Version**</span></span> | <span data-ttu-id="1dd83-170">**Node agent SKU ID**</span><span class="sxs-lookup"><span data-stu-id="1dd83-170">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="1dd83-171">Canonical</span><span class="sxs-lookup"><span data-stu-id="1dd83-171">Canonical</span></span> | <span data-ttu-id="1dd83-172">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-172">UbuntuServer</span></span> | <span data-ttu-id="1dd83-173">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="1dd83-173">14.04.5-LTS</span></span> | <span data-ttu-id="1dd83-174">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-174">latest</span></span> | <span data-ttu-id="1dd83-175">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="1dd83-175">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="1dd83-176">Canonical</span><span class="sxs-lookup"><span data-stu-id="1dd83-176">Canonical</span></span> | <span data-ttu-id="1dd83-177">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-177">UbuntuServer</span></span> | <span data-ttu-id="1dd83-178">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="1dd83-178">16.04.0-LTS</span></span> | <span data-ttu-id="1dd83-179">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-179">latest</span></span> | <span data-ttu-id="1dd83-180">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="1dd83-180">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="1dd83-181">Credativ</span><span class="sxs-lookup"><span data-stu-id="1dd83-181">Credativ</span></span> | <span data-ttu-id="1dd83-182">Debian</span><span class="sxs-lookup"><span data-stu-id="1dd83-182">Debian</span></span> | <span data-ttu-id="1dd83-183">8</span><span class="sxs-lookup"><span data-stu-id="1dd83-183">8</span></span> | <span data-ttu-id="1dd83-184">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-184">latest</span></span> | <span data-ttu-id="1dd83-185">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="1dd83-185">batch.node.debian 8</span></span> |
| <span data-ttu-id="1dd83-186">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1dd83-186">OpenLogic</span></span> | <span data-ttu-id="1dd83-187">CentOS</span><span class="sxs-lookup"><span data-stu-id="1dd83-187">CentOS</span></span> | <span data-ttu-id="1dd83-188">7.0</span><span class="sxs-lookup"><span data-stu-id="1dd83-188">7.0</span></span> | <span data-ttu-id="1dd83-189">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-189">latest</span></span> | <span data-ttu-id="1dd83-190">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-190">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-191">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1dd83-191">OpenLogic</span></span> | <span data-ttu-id="1dd83-192">CentOS</span><span class="sxs-lookup"><span data-stu-id="1dd83-192">CentOS</span></span> | <span data-ttu-id="1dd83-193">7.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-193">7.1</span></span> | <span data-ttu-id="1dd83-194">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-194">latest</span></span> | <span data-ttu-id="1dd83-195">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-195">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-196">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1dd83-196">OpenLogic</span></span> | <span data-ttu-id="1dd83-197">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="1dd83-197">CentOS-HPC</span></span> | <span data-ttu-id="1dd83-198">7.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-198">7.1</span></span> | <span data-ttu-id="1dd83-199">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-199">latest</span></span> | <span data-ttu-id="1dd83-200">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-200">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-201">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="1dd83-201">OpenLogic</span></span> | <span data-ttu-id="1dd83-202">CentOS</span><span class="sxs-lookup"><span data-stu-id="1dd83-202">CentOS</span></span> | <span data-ttu-id="1dd83-203">7.2</span><span class="sxs-lookup"><span data-stu-id="1dd83-203">7.2</span></span> | <span data-ttu-id="1dd83-204">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-204">latest</span></span> | <span data-ttu-id="1dd83-205">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-205">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-206">Oracle</span><span class="sxs-lookup"><span data-stu-id="1dd83-206">Oracle</span></span> | <span data-ttu-id="1dd83-207">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="1dd83-207">Oracle-Linux</span></span> | <span data-ttu-id="1dd83-208">7.0</span><span class="sxs-lookup"><span data-stu-id="1dd83-208">7.0</span></span> | <span data-ttu-id="1dd83-209">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-209">latest</span></span> | <span data-ttu-id="1dd83-210">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-210">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-211">Oracle</span><span class="sxs-lookup"><span data-stu-id="1dd83-211">Oracle</span></span> | <span data-ttu-id="1dd83-212">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="1dd83-212">Oracle-Linux</span></span> | <span data-ttu-id="1dd83-213">7.2</span><span class="sxs-lookup"><span data-stu-id="1dd83-213">7.2</span></span> | <span data-ttu-id="1dd83-214">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-214">latest</span></span> | <span data-ttu-id="1dd83-215">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-215">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-216">SUSE</span><span class="sxs-lookup"><span data-stu-id="1dd83-216">SUSE</span></span> | <span data-ttu-id="1dd83-217">openSUSE</span><span class="sxs-lookup"><span data-stu-id="1dd83-217">openSUSE</span></span> | <span data-ttu-id="1dd83-218">13.2</span><span class="sxs-lookup"><span data-stu-id="1dd83-218">13.2</span></span> | <span data-ttu-id="1dd83-219">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-219">latest</span></span> | <span data-ttu-id="1dd83-220">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="1dd83-220">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="1dd83-221">SUSE</span><span class="sxs-lookup"><span data-stu-id="1dd83-221">SUSE</span></span> | <span data-ttu-id="1dd83-222">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="1dd83-222">openSUSE-Leap</span></span> | <span data-ttu-id="1dd83-223">42.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-223">42.1</span></span> | <span data-ttu-id="1dd83-224">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-224">latest</span></span> | <span data-ttu-id="1dd83-225">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-225">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1dd83-226">SUSE</span><span class="sxs-lookup"><span data-stu-id="1dd83-226">SUSE</span></span> | <span data-ttu-id="1dd83-227">SLES</span><span class="sxs-lookup"><span data-stu-id="1dd83-227">SLES</span></span> | <span data-ttu-id="1dd83-228">12-SP1</span><span class="sxs-lookup"><span data-stu-id="1dd83-228">12-SP1</span></span> | <span data-ttu-id="1dd83-229">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-229">latest</span></span> | <span data-ttu-id="1dd83-230">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-230">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1dd83-231">SUSE</span><span class="sxs-lookup"><span data-stu-id="1dd83-231">SUSE</span></span> | <span data-ttu-id="1dd83-232">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="1dd83-232">SLES-HPC</span></span> | <span data-ttu-id="1dd83-233">12-SP1</span><span class="sxs-lookup"><span data-stu-id="1dd83-233">12-SP1</span></span> | <span data-ttu-id="1dd83-234">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-234">latest</span></span> | <span data-ttu-id="1dd83-235">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="1dd83-235">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="1dd83-236">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="1dd83-236">microsoft-ads</span></span> | <span data-ttu-id="1dd83-237">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1dd83-237">linux-data-science-vm</span></span> | <span data-ttu-id="1dd83-238">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="1dd83-238">linuxdsvm</span></span> | <span data-ttu-id="1dd83-239">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-239">latest</span></span> | <span data-ttu-id="1dd83-240">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="1dd83-240">batch.node.centos 7</span></span> |
| <span data-ttu-id="1dd83-241">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="1dd83-241">microsoft-ads</span></span> | <span data-ttu-id="1dd83-242">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1dd83-242">standard-data-science-vm</span></span> | <span data-ttu-id="1dd83-243">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="1dd83-243">standard-data-science-vm</span></span> | <span data-ttu-id="1dd83-244">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-244">latest</span></span> | <span data-ttu-id="1dd83-245">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-245">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1dd83-246">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-246">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1dd83-247">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-247">WindowsServer</span></span> | <span data-ttu-id="1dd83-248">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="1dd83-248">2008-R2-SP1</span></span> | <span data-ttu-id="1dd83-249">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-249">latest</span></span> | <span data-ttu-id="1dd83-250">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-250">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1dd83-251">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-251">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1dd83-252">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-252">WindowsServer</span></span> | <span data-ttu-id="1dd83-253">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1dd83-253">2012-Datacenter</span></span> | <span data-ttu-id="1dd83-254">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-254">latest</span></span> | <span data-ttu-id="1dd83-255">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-255">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1dd83-256">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-256">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1dd83-257">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-257">WindowsServer</span></span> | <span data-ttu-id="1dd83-258">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1dd83-258">2012-R2-Datacenter</span></span> | <span data-ttu-id="1dd83-259">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-259">latest</span></span> | <span data-ttu-id="1dd83-260">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-260">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1dd83-261">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-261">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1dd83-262">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-262">WindowsServer</span></span> | <span data-ttu-id="1dd83-263">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="1dd83-263">2016-Datacenter</span></span> | <span data-ttu-id="1dd83-264">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-264">latest</span></span> | <span data-ttu-id="1dd83-265">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-265">batch.node.windows amd64</span></span> |
| <span data-ttu-id="1dd83-266">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-266">MicrosoftWindowsServer</span></span> | <span data-ttu-id="1dd83-267">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="1dd83-267">WindowsServer</span></span> | <span data-ttu-id="1dd83-268">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="1dd83-268">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="1dd83-269">latest</span><span class="sxs-lookup"><span data-stu-id="1dd83-269">latest</span></span> | <span data-ttu-id="1dd83-270">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="1dd83-270">batch.node.windows amd64</span></span> |

## <a name="connect-to-linux-nodes"></a><span data-ttu-id="1dd83-271">Connect to Linux nodes</span><span class="sxs-lookup"><span data-stu-id="1dd83-271">Connect to Linux nodes</span></span>
<span data-ttu-id="1dd83-272">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="1dd83-272">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="1dd83-273">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="1dd83-273">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="1dd83-274">Instead, the Batch service enables SSH access on each node for remote connection.</span><span class="sxs-lookup"><span data-stu-id="1dd83-274">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="1dd83-275">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span><span class="sxs-lookup"><span data-stu-id="1dd83-275">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="1dd83-276">It then prints the secure shell (SSH) connection information for each node.</span><span class="sxs-lookup"><span data-stu-id="1dd83-276">It then prints the secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify the ID of an existing pool containing Linux nodes
# currently in the 'idle' state
pool_id = ''

# Specify the username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create the user that will be added to each node in the pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get the list of nodes in the pool
nodes = batch_client.compute_node.list(pool_id)

# Add the user to each node in the pool and print
# the connection information for the node
for node in nodes:
    # Add the user to the node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for the node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print the connection info for the node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="1dd83-277">Here is sample output for the previous code for a pool that contains four Linux nodes:</span><span class="sxs-lookup"><span data-stu-id="1dd83-277">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="1dd83-278">Note that instead of a password, you can specify an SSH public key when you create a user on a node.</span><span class="sxs-lookup"><span data-stu-id="1dd83-278">Note that instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="1dd83-279">In the Python SDK, this is done by using the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="1dd83-279">In the Python SDK, this is done by using the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="1dd83-280">In .NET, this is done by using the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span><span class="sxs-lookup"><span data-stu-id="1dd83-280">In .NET, this is done by using the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="1dd83-281">Pricing</span><span class="sxs-lookup"><span data-stu-id="1dd83-281">Pricing</span></span>
<span data-ttu-id="1dd83-282">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span><span class="sxs-lookup"><span data-stu-id="1dd83-282">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="1dd83-283">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span><span class="sxs-lookup"><span data-stu-id="1dd83-283">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="1dd83-284">When you choose **Cloud Services Configuration**, you will be charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="1dd83-284">When you choose **Cloud Services Configuration**, you will be charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="1dd83-285">When you choose **Virtual Machine Configuration**, you will be charged based on the [Virtual Machines pricing][vm_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="1dd83-285">When you choose **Virtual Machine Configuration**, you will be charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dd83-286">Next steps</span><span class="sxs-lookup"><span data-stu-id="1dd83-286">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="1dd83-287">Batch Python tutorial</span><span class="sxs-lookup"><span data-stu-id="1dd83-287">Batch Python tutorial</span></span>
<span data-ttu-id="1dd83-288">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="1dd83-288">For a more in-depth tutorial about how to work with Batch by using Python, check out [Get started with the Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="1dd83-289">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span><span class="sxs-lookup"><span data-stu-id="1dd83-289">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique to obtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="1dd83-290">Batch Python code samples</span><span class="sxs-lookup"><span data-stu-id="1dd83-290">Batch Python code samples</span></span>
<span data-ttu-id="1dd83-291">Check out the other [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub for several scripts that show you how to perform common Batch operations such as pool, job, and task creation.</span><span class="sxs-lookup"><span data-stu-id="1dd83-291">Check out the other [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub for several scripts that show you how to perform common Batch operations such as pool, job, and task creation.</span></span> <span data-ttu-id="1dd83-292">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span><span class="sxs-lookup"><span data-stu-id="1dd83-292">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="1dd83-293">Batch forum</span><span class="sxs-lookup"><span data-stu-id="1dd83-293">Batch forum</span></span>
<span data-ttu-id="1dd83-294">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span><span class="sxs-lookup"><span data-stu-id="1dd83-294">The [Azure Batch Forum][forum] on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="1dd83-295">Read helpful "stickied" posts, and post your questions as they arise while you build your Batch solutions.</span><span class="sxs-lookup"><span data-stu-id="1dd83-295">Read helpful "stickied" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
