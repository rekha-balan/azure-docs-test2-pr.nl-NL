---
title: Run Linux on virtual machine compute nodes - Azure Batch | Microsoft Docs
description: Learn how to process your parallel compute workloads on pools of Linux virtual machines in Azure Batch.
services: batch
documentationcenter: python
author: dlepow
manager: jeconnoc
editor: ''
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: na
ms.date: 06/01/2018
ms.author: danlep
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 713583a6a184a583145c610b4e014f56941efa4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803925"
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="48add-103">Provision Linux compute nodes in Batch pools</span><span class="sxs-lookup"><span data-stu-id="48add-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="48add-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span><span class="sxs-lookup"><span data-stu-id="48add-104">You can use Azure Batch to run parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="48add-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span><span class="sxs-lookup"><span data-stu-id="48add-105">This article details how to create pools of Linux compute nodes in the Batch service by using both the [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="48add-106">Application packages are supported on all Batch pools created after 5 July 2017.</span><span class="sxs-lookup"><span data-stu-id="48add-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="48add-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span><span class="sxs-lookup"><span data-stu-id="48add-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if the pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="48add-108">Batch pools created prior to 10 March 2016 do not support application packages.</span><span class="sxs-lookup"><span data-stu-id="48add-108">Batch pools created prior to 10 March 2016 do not support application packages.</span></span> <span data-ttu-id="48add-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="48add-109">For more information about using application packages to deploy your applications to your Batch nodes, see [Deploy applications to compute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="48add-110">Virtual machine configuration</span><span class="sxs-lookup"><span data-stu-id="48add-110">Virtual machine configuration</span></span>
<span data-ttu-id="48add-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span><span class="sxs-lookup"><span data-stu-id="48add-111">When you create a pool of compute nodes in Batch, you have two options from which to select the node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="48add-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span><span class="sxs-lookup"><span data-stu-id="48add-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="48add-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="48add-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in the [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="48add-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span><span class="sxs-lookup"><span data-stu-id="48add-114">When you create a pool that contains Azure Cloud Services nodes, you specify the node size and the OS family, which are described in the previously mentioned articles.</span></span> <span data-ttu-id="48add-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span><span class="sxs-lookup"><span data-stu-id="48add-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="48add-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span><span class="sxs-lookup"><span data-stu-id="48add-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="48add-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="48add-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="48add-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span><span class="sxs-lookup"><span data-stu-id="48add-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify the size of the nodes, the virtual machine image reference, and the Batch node agent SKU to be installed on the nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="48add-119">Virtual machine image reference</span><span class="sxs-lookup"><span data-stu-id="48add-119">Virtual machine image reference</span></span>
<span data-ttu-id="48add-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide compute nodes in the Virtual Machine Configuration.</span><span class="sxs-lookup"><span data-stu-id="48add-120">The Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) to provide compute nodes in the Virtual Machine Configuration.</span></span> <span data-ttu-id="48add-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span><span class="sxs-lookup"><span data-stu-id="48add-121">You can specify an image from the [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="48add-122">For more details about custom images, see [Create a pool with a custom image](batch-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="48add-122">For more details about custom images, see [Create a pool with a custom image](batch-custom-images.md).</span></span>

<span data-ttu-id="48add-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span><span class="sxs-lookup"><span data-stu-id="48add-123">When you configure a virtual machine image reference, you specify the properties of the virtual machine image.</span></span> <span data-ttu-id="48add-124">The following properties are required when you create a virtual machine image reference:</span><span class="sxs-lookup"><span data-stu-id="48add-124">The following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="48add-125">**Image reference properties**</span><span class="sxs-lookup"><span data-stu-id="48add-125">**Image reference properties**</span></span> | <span data-ttu-id="48add-126">**Example**</span><span class="sxs-lookup"><span data-stu-id="48add-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="48add-127">Publisher</span><span class="sxs-lookup"><span data-stu-id="48add-127">Publisher</span></span> |<span data-ttu-id="48add-128">Canonical</span><span class="sxs-lookup"><span data-stu-id="48add-128">Canonical</span></span> |
| <span data-ttu-id="48add-129">Offer</span><span class="sxs-lookup"><span data-stu-id="48add-129">Offer</span></span> |<span data-ttu-id="48add-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="48add-130">UbuntuServer</span></span> |
| <span data-ttu-id="48add-131">SKU</span><span class="sxs-lookup"><span data-stu-id="48add-131">SKU</span></span> |<span data-ttu-id="48add-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="48add-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="48add-133">Version</span><span class="sxs-lookup"><span data-stu-id="48add-133">Version</span></span> |<span data-ttu-id="48add-134">latest</span><span class="sxs-lookup"><span data-stu-id="48add-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="48add-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="48add-135">You can learn more about these properties and how to list Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="48add-136">Note that not all Marketplace images are currently compatible with Batch.</span><span class="sxs-lookup"><span data-stu-id="48add-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="48add-137">For more information, see [Node agent SKU](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="48add-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="48add-138">Node agent SKU</span><span class="sxs-lookup"><span data-stu-id="48add-138">Node agent SKU</span></span>
<span data-ttu-id="48add-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span><span class="sxs-lookup"><span data-stu-id="48add-139">The Batch node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="48add-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span><span class="sxs-lookup"><span data-stu-id="48add-140">There are different implementations of the node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="48add-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span><span class="sxs-lookup"><span data-stu-id="48add-141">Essentially, when you create a Virtual Machine Configuration, you first specify the virtual machine image reference, and then you specify the node agent to install on the image.</span></span> <span data-ttu-id="48add-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span><span class="sxs-lookup"><span data-stu-id="48add-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="48add-143">Here are a few examples of node agent SKUs:</span><span class="sxs-lookup"><span data-stu-id="48add-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="48add-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="48add-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="48add-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-145">batch.node.centos 7</span></span>
* <span data-ttu-id="48add-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="48add-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span><span class="sxs-lookup"><span data-stu-id="48add-147">Not all virtual machine images that are available in the Marketplace are compatible with the currently available Batch node agents.</span></span> <span data-ttu-id="48add-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span><span class="sxs-lookup"><span data-stu-id="48add-148">Use the Batch SDKs to list the available node agent SKUs and the virtual machine images with which they are compatible.</span></span> <span data-ttu-id="48add-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span><span class="sxs-lookup"><span data-stu-id="48add-149">See the [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how to retrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="48add-150">Create a Linux pool: Batch Python</span><span class="sxs-lookup"><span data-stu-id="48add-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="48add-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span><span class="sxs-lookup"><span data-stu-id="48add-151">The following code snippet shows an example of how to use the [Microsoft Azure Batch Client Library for Python][py_batch_package] to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="48add-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span><span class="sxs-lookup"><span data-stu-id="48add-152">Reference documentation for the Batch Python module can be found at [azure.batch package][py_batch_docs] on Read the Docs.</span></span>

<span data-ttu-id="48add-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span><span class="sxs-lookup"><span data-stu-id="48add-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="48add-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span><span class="sxs-lookup"><span data-stu-id="48add-154">In production code, however, we recommend that you use the [list_node_agent_skus][py_list_skus] method to determine and select from the available image and node agent SKU combinations at runtime.</span></span>

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

<span data-ttu-id="48add-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span><span class="sxs-lookup"><span data-stu-id="48add-155">As mentioned previously, we recommend that instead of creating the [ImageReference][py_imagereference] explicitly, you use the [list_node_agent_skus][py_list_skus] method to dynamically select from the currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="48add-156">The following Python snippet shows how to use this method.</span><span class="sxs-lookup"><span data-stu-id="48add-156">The following Python snippet shows how to use this method.</span></span>

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

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="48add-157">Create a Linux pool: Batch .NET</span><span class="sxs-lookup"><span data-stu-id="48add-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="48add-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span><span class="sxs-lookup"><span data-stu-id="48add-158">The following code snippet shows an example of how to use the [Batch .NET][nuget_batch_net] client library to create a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="48add-159">You can find the [Batch .NET reference documentation][api_net] on docs.microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="48add-159">You can find the [Batch .NET reference documentation][api_net] on docs.microsoft.com.</span></span>

<span data-ttu-id="48add-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span><span class="sxs-lookup"><span data-stu-id="48add-160">The following code snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to select from the list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="48add-161">This technique is desirable because the list of supported combinations may change from time to time.</span><span class="sxs-lookup"><span data-stu-id="48add-161">This technique is desirable because the list of supported combinations may change from time to time.</span></span> <span data-ttu-id="48add-162">Most commonly, supported combinations are added.</span><span class="sxs-lookup"><span data-stu-id="48add-162">Most commonly, supported combinations are added.</span></span>

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
    imageRef.Sku.Contains("14.04");

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
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create the unbound pool object using the VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit the pool to the Batch service
await pool.CommitAsync();
```

<span data-ttu-id="48add-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span><span class="sxs-lookup"><span data-stu-id="48add-163">Although the previous snippet uses the [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method to dynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="48add-164">List of virtual machine images</span><span class="sxs-lookup"><span data-stu-id="48add-164">List of virtual machine images</span></span>
<span data-ttu-id="48add-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span><span class="sxs-lookup"><span data-stu-id="48add-165">The following table lists the Marketplace virtual machine images that are compatible with the available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="48add-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span><span class="sxs-lookup"><span data-stu-id="48add-166">It is important to note that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="48add-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) or [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span><span class="sxs-lookup"><span data-stu-id="48add-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) or [ListNodeAgentSkus][net_list_skus] (Batch .NET) to determine and select from the currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="48add-168">The following list may change at any time.</span><span class="sxs-lookup"><span data-stu-id="48add-168">The following list may change at any time.</span></span> <span data-ttu-id="48add-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span><span class="sxs-lookup"><span data-stu-id="48add-169">Always use the **list node agent SKU** methods available in the Batch APIs to list the compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="48add-170">**Publisher**</span><span class="sxs-lookup"><span data-stu-id="48add-170">**Publisher**</span></span> | <span data-ttu-id="48add-171">**Offer**</span><span class="sxs-lookup"><span data-stu-id="48add-171">**Offer**</span></span> | <span data-ttu-id="48add-172">**Image SKU**</span><span class="sxs-lookup"><span data-stu-id="48add-172">**Image SKU**</span></span> | <span data-ttu-id="48add-173">**Version**</span><span class="sxs-lookup"><span data-stu-id="48add-173">**Version**</span></span> | <span data-ttu-id="48add-174">**Node agent SKU ID**</span><span class="sxs-lookup"><span data-stu-id="48add-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="48add-175">batch</span><span class="sxs-lookup"><span data-stu-id="48add-175">batch</span></span> | <span data-ttu-id="48add-176">rendering-centos73</span><span class="sxs-lookup"><span data-stu-id="48add-176">rendering-centos73</span></span> | <span data-ttu-id="48add-177">rendering</span><span class="sxs-lookup"><span data-stu-id="48add-177">rendering</span></span> | <span data-ttu-id="48add-178">latest</span><span class="sxs-lookup"><span data-stu-id="48add-178">latest</span></span> | <span data-ttu-id="48add-179">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-179">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-180">batch</span><span class="sxs-lookup"><span data-stu-id="48add-180">batch</span></span> | <span data-ttu-id="48add-181">rendering-windows2016</span><span class="sxs-lookup"><span data-stu-id="48add-181">rendering-windows2016</span></span> | <span data-ttu-id="48add-182">rendering</span><span class="sxs-lookup"><span data-stu-id="48add-182">rendering</span></span> | <span data-ttu-id="48add-183">latest</span><span class="sxs-lookup"><span data-stu-id="48add-183">latest</span></span> | <span data-ttu-id="48add-184">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-184">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-185">Canonical</span><span class="sxs-lookup"><span data-stu-id="48add-185">Canonical</span></span> | <span data-ttu-id="48add-186">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="48add-186">UbuntuServer</span></span> | <span data-ttu-id="48add-187">16.04-LTS</span><span class="sxs-lookup"><span data-stu-id="48add-187">16.04-LTS</span></span> | <span data-ttu-id="48add-188">latest</span><span class="sxs-lookup"><span data-stu-id="48add-188">latest</span></span> | <span data-ttu-id="48add-189">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="48add-189">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="48add-190">Canonical</span><span class="sxs-lookup"><span data-stu-id="48add-190">Canonical</span></span> | <span data-ttu-id="48add-191">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="48add-191">UbuntuServer</span></span> | <span data-ttu-id="48add-192">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="48add-192">14.04.5-LTS</span></span> | <span data-ttu-id="48add-193">latest</span><span class="sxs-lookup"><span data-stu-id="48add-193">latest</span></span> | <span data-ttu-id="48add-194">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="48add-194">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="48add-195">Credativ</span><span class="sxs-lookup"><span data-stu-id="48add-195">Credativ</span></span> | <span data-ttu-id="48add-196">Debian</span><span class="sxs-lookup"><span data-stu-id="48add-196">Debian</span></span> | <span data-ttu-id="48add-197">9</span><span class="sxs-lookup"><span data-stu-id="48add-197">9</span></span> | <span data-ttu-id="48add-198">latest</span><span class="sxs-lookup"><span data-stu-id="48add-198">latest</span></span> | <span data-ttu-id="48add-199">batch.node.debian 9</span><span class="sxs-lookup"><span data-stu-id="48add-199">batch.node.debian 9</span></span> |
| <span data-ttu-id="48add-200">Credativ</span><span class="sxs-lookup"><span data-stu-id="48add-200">Credativ</span></span> | <span data-ttu-id="48add-201">Debian</span><span class="sxs-lookup"><span data-stu-id="48add-201">Debian</span></span> | <span data-ttu-id="48add-202">8</span><span class="sxs-lookup"><span data-stu-id="48add-202">8</span></span> | <span data-ttu-id="48add-203">latest</span><span class="sxs-lookup"><span data-stu-id="48add-203">latest</span></span> | <span data-ttu-id="48add-204">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="48add-204">batch.node.debian 8</span></span> |
| <span data-ttu-id="48add-205">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="48add-205">microsoft-ads</span></span> | <span data-ttu-id="48add-206">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="48add-206">linux-data-science-vm</span></span> | <span data-ttu-id="48add-207">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="48add-207">linuxdsvm</span></span> | <span data-ttu-id="48add-208">latest</span><span class="sxs-lookup"><span data-stu-id="48add-208">latest</span></span> | <span data-ttu-id="48add-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-210">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="48add-210">microsoft-ads</span></span> | <span data-ttu-id="48add-211">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="48add-211">standard-data-science-vm</span></span> | <span data-ttu-id="48add-212">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="48add-212">standard-data-science-vm</span></span> | <span data-ttu-id="48add-213">latest</span><span class="sxs-lookup"><span data-stu-id="48add-213">latest</span></span> | <span data-ttu-id="48add-214">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-214">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-215">microsoft-azure-batch</span><span class="sxs-lookup"><span data-stu-id="48add-215">microsoft-azure-batch</span></span> | <span data-ttu-id="48add-216">centos-container</span><span class="sxs-lookup"><span data-stu-id="48add-216">centos-container</span></span> | <span data-ttu-id="48add-217">7-4</span><span class="sxs-lookup"><span data-stu-id="48add-217">7-4</span></span> | <span data-ttu-id="48add-218">latest</span><span class="sxs-lookup"><span data-stu-id="48add-218">latest</span></span> | <span data-ttu-id="48add-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-220">microsoft-azure-batch</span><span class="sxs-lookup"><span data-stu-id="48add-220">microsoft-azure-batch</span></span> | <span data-ttu-id="48add-221">centos-container-rdma</span><span class="sxs-lookup"><span data-stu-id="48add-221">centos-container-rdma</span></span> | <span data-ttu-id="48add-222">7-4</span><span class="sxs-lookup"><span data-stu-id="48add-222">7-4</span></span> | <span data-ttu-id="48add-223">latest</span><span class="sxs-lookup"><span data-stu-id="48add-223">latest</span></span> | <span data-ttu-id="48add-224">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-224">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-225">microsoft-azure-batch</span><span class="sxs-lookup"><span data-stu-id="48add-225">microsoft-azure-batch</span></span> | <span data-ttu-id="48add-226">ubuntu-server-container</span><span class="sxs-lookup"><span data-stu-id="48add-226">ubuntu-server-container</span></span> | <span data-ttu-id="48add-227">16-04-lts</span><span class="sxs-lookup"><span data-stu-id="48add-227">16-04-lts</span></span> | <span data-ttu-id="48add-228">latest</span><span class="sxs-lookup"><span data-stu-id="48add-228">latest</span></span> | <span data-ttu-id="48add-229">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="48add-229">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="48add-230">microsoft-azure-batch</span><span class="sxs-lookup"><span data-stu-id="48add-230">microsoft-azure-batch</span></span> | <span data-ttu-id="48add-231">ubuntu-server-container-rdma</span><span class="sxs-lookup"><span data-stu-id="48add-231">ubuntu-server-container-rdma</span></span> | <span data-ttu-id="48add-232">16-04-lts</span><span class="sxs-lookup"><span data-stu-id="48add-232">16-04-lts</span></span> | <span data-ttu-id="48add-233">latest</span><span class="sxs-lookup"><span data-stu-id="48add-233">latest</span></span> | <span data-ttu-id="48add-234">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="48add-234">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="48add-235">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-235">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-236">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-236">WindowsServer</span></span> | <span data-ttu-id="48add-237">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="48add-237">2016-Datacenter</span></span> | <span data-ttu-id="48add-238">latest</span><span class="sxs-lookup"><span data-stu-id="48add-238">latest</span></span> | <span data-ttu-id="48add-239">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-239">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-240">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-240">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-241">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-241">WindowsServer</span></span> | <span data-ttu-id="48add-242">2016-Datacenter-smalldisk</span><span class="sxs-lookup"><span data-stu-id="48add-242">2016-Datacenter-smalldisk</span></span> | <span data-ttu-id="48add-243">latest</span><span class="sxs-lookup"><span data-stu-id="48add-243">latest</span></span> | <span data-ttu-id="48add-244">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-244">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-245">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-245">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-246">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-246">WindowsServer</span></span> | <span data-ttu-id="48add-247">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="48add-247">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="48add-248">latest</span><span class="sxs-lookup"><span data-stu-id="48add-248">latest</span></span> | <span data-ttu-id="48add-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-251">WindowsServer</span></span> | <span data-ttu-id="48add-252">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="48add-252">2012-R2-Datacenter</span></span> | <span data-ttu-id="48add-253">latest</span><span class="sxs-lookup"><span data-stu-id="48add-253">latest</span></span> | <span data-ttu-id="48add-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-256">WindowsServer</span></span> | <span data-ttu-id="48add-257">2012-R2-Datacenter-smalldisk</span><span class="sxs-lookup"><span data-stu-id="48add-257">2012-R2-Datacenter-smalldisk</span></span> | <span data-ttu-id="48add-258">latest</span><span class="sxs-lookup"><span data-stu-id="48add-258">latest</span></span> | <span data-ttu-id="48add-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-261">WindowsServer</span></span> | <span data-ttu-id="48add-262">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="48add-262">2012-Datacenter</span></span> | <span data-ttu-id="48add-263">latest</span><span class="sxs-lookup"><span data-stu-id="48add-263">latest</span></span> | <span data-ttu-id="48add-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-266">WindowsServer</span></span> | <span data-ttu-id="48add-267">2012-Datacenter-smalldisk</span><span class="sxs-lookup"><span data-stu-id="48add-267">2012-Datacenter-smalldisk</span></span> | <span data-ttu-id="48add-268">latest</span><span class="sxs-lookup"><span data-stu-id="48add-268">latest</span></span> | <span data-ttu-id="48add-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-271">WindowsServer</span></span> | <span data-ttu-id="48add-272">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="48add-272">2008-R2-SP1</span></span> | <span data-ttu-id="48add-273">latest</span><span class="sxs-lookup"><span data-stu-id="48add-273">latest</span></span> | <span data-ttu-id="48add-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-274">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-275">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-275">MicrosoftWindowsServer</span></span> | <span data-ttu-id="48add-276">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="48add-276">WindowsServer</span></span> | <span data-ttu-id="48add-277">2008-R2-SP1-smalldisk</span><span class="sxs-lookup"><span data-stu-id="48add-277">2008-R2-SP1-smalldisk</span></span> | <span data-ttu-id="48add-278">latest</span><span class="sxs-lookup"><span data-stu-id="48add-278">latest</span></span> | <span data-ttu-id="48add-279">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="48add-279">batch.node.windows amd64</span></span> |
| <span data-ttu-id="48add-280">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="48add-280">OpenLogic</span></span> | <span data-ttu-id="48add-281">CentOS</span><span class="sxs-lookup"><span data-stu-id="48add-281">CentOS</span></span> | <span data-ttu-id="48add-282">7.4</span><span class="sxs-lookup"><span data-stu-id="48add-282">7.4</span></span> | <span data-ttu-id="48add-283">latest</span><span class="sxs-lookup"><span data-stu-id="48add-283">latest</span></span> | <span data-ttu-id="48add-284">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-284">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-285">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="48add-285">OpenLogic</span></span> | <span data-ttu-id="48add-286">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="48add-286">CentOS-HPC</span></span> | <span data-ttu-id="48add-287">7.4</span><span class="sxs-lookup"><span data-stu-id="48add-287">7.4</span></span> | <span data-ttu-id="48add-288">latest</span><span class="sxs-lookup"><span data-stu-id="48add-288">latest</span></span> | <span data-ttu-id="48add-289">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-289">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-290">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="48add-290">OpenLogic</span></span> | <span data-ttu-id="48add-291">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="48add-291">CentOS-HPC</span></span> | <span data-ttu-id="48add-292">7.3</span><span class="sxs-lookup"><span data-stu-id="48add-292">7.3</span></span> | <span data-ttu-id="48add-293">latest</span><span class="sxs-lookup"><span data-stu-id="48add-293">latest</span></span> | <span data-ttu-id="48add-294">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-294">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-295">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="48add-295">OpenLogic</span></span> | <span data-ttu-id="48add-296">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="48add-296">CentOS-HPC</span></span> | <span data-ttu-id="48add-297">7.1</span><span class="sxs-lookup"><span data-stu-id="48add-297">7.1</span></span> | <span data-ttu-id="48add-298">latest</span><span class="sxs-lookup"><span data-stu-id="48add-298">latest</span></span> | <span data-ttu-id="48add-299">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-299">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-300">Oracle</span><span class="sxs-lookup"><span data-stu-id="48add-300">Oracle</span></span> | <span data-ttu-id="48add-301">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="48add-301">Oracle-Linux</span></span> | <span data-ttu-id="48add-302">7.4</span><span class="sxs-lookup"><span data-stu-id="48add-302">7.4</span></span> | <span data-ttu-id="48add-303">latest</span><span class="sxs-lookup"><span data-stu-id="48add-303">latest</span></span> | <span data-ttu-id="48add-304">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="48add-304">batch.node.centos 7</span></span> |
| <span data-ttu-id="48add-305">SUSE</span><span class="sxs-lookup"><span data-stu-id="48add-305">SUSE</span></span> | <span data-ttu-id="48add-306">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="48add-306">SLES-HPC</span></span> | <span data-ttu-id="48add-307">12-SP2</span><span class="sxs-lookup"><span data-stu-id="48add-307">12-SP2</span></span> | <span data-ttu-id="48add-308">latest</span><span class="sxs-lookup"><span data-stu-id="48add-308">latest</span></span> | <span data-ttu-id="48add-309">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="48add-309">batch.node.opensuse 42.1</span></span> |

## <a name="connect-to-linux-nodes-using-ssh"></a><span data-ttu-id="48add-310">Connect to Linux nodes using SSH</span><span class="sxs-lookup"><span data-stu-id="48add-310">Connect to Linux nodes using SSH</span></span>
<span data-ttu-id="48add-311">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span><span class="sxs-lookup"><span data-stu-id="48add-311">During development or while troubleshooting, you may find it necessary to sign in to the nodes in your pool.</span></span> <span data-ttu-id="48add-312">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span><span class="sxs-lookup"><span data-stu-id="48add-312">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) to connect to Linux nodes.</span></span> <span data-ttu-id="48add-313">Instead, the Batch service enables SSH access on each node for remote connection.</span><span class="sxs-lookup"><span data-stu-id="48add-313">Instead, the Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="48add-314">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span><span class="sxs-lookup"><span data-stu-id="48add-314">The following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="48add-315">It then prints the secure shell (SSH) connection information for each node.</span><span class="sxs-lookup"><span data-stu-id="48add-315">It then prints the secure shell (SSH) connection information for each node.</span></span>

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

<span data-ttu-id="48add-316">Here is sample output for the previous code for a pool that contains four Linux nodes:</span><span class="sxs-lookup"><span data-stu-id="48add-316">Here is sample output for the previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="48add-317">Instead of a password, you can specify an SSH public key when you create a user on a node.</span><span class="sxs-lookup"><span data-stu-id="48add-317">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="48add-318">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="48add-318">In the Python SDK, use the **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="48add-319">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span><span class="sxs-lookup"><span data-stu-id="48add-319">In .NET, use the [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="48add-320">Pricing</span><span class="sxs-lookup"><span data-stu-id="48add-320">Pricing</span></span>
<span data-ttu-id="48add-321">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span><span class="sxs-lookup"><span data-stu-id="48add-321">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="48add-322">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span><span class="sxs-lookup"><span data-stu-id="48add-322">The Batch service itself is offered at no cost, which means you are charged only for the compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="48add-323">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="48add-323">When you choose **Cloud Services Configuration**, you are charged based on the [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="48add-324">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span><span class="sxs-lookup"><span data-stu-id="48add-324">When you choose **Virtual Machine Configuration**, you are charged based on the [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="48add-325">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span><span class="sxs-lookup"><span data-stu-id="48add-325">If you deploy applications to your Batch nodes using [application packages](batch-application-packages.md), you are also charged for the Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="48add-326">In general, the Azure Storage costs are minimal.</span><span class="sxs-lookup"><span data-stu-id="48add-326">In general, the Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="48add-327">Next steps</span><span class="sxs-lookup"><span data-stu-id="48add-327">Next steps</span></span>

<span data-ttu-id="48add-328">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span><span class="sxs-lookup"><span data-stu-id="48add-328">The [Python code samples][github_samples_py] in the [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how to perform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="48add-329">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span><span class="sxs-lookup"><span data-stu-id="48add-329">The [README][github_py_readme] that accompanies the Python samples has details about how to install the required packages.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
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
[nuget_batch_net]: https://www.nuget.org/packages/Microsoft.Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: https://azure-sdk-for-python.readthedocs.io/batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: https://docs.microsoft.com/python/api/azure.batch.models.computenodeuser
[py_imagereference]: https://docs.microsoft.com/python/api/azure.mgmt.batch.models.imagereference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
