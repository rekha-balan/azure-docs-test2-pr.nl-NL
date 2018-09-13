---
title: Container workloads on Azure Batch | Microsoft Docs
description: Learn how to run applications from container images on Azure Batch.
services: batch
author: dlepow
manager: jeconnoc
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.workload: na
ms.date: 06/04/2018
ms.author: danlep
ms.openlocfilehash: a85db0315a2ee8aa9fd34b8c18893f4cb1068528
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967727"
---
# <a name="run-container-applications-on-azure-batch"></a><span data-ttu-id="02918-103">Run container applications on Azure Batch</span><span class="sxs-lookup"><span data-stu-id="02918-103">Run container applications on Azure Batch</span></span>

<span data-ttu-id="02918-104">Azure Batch lets you run and scale large numbers of batch computing jobs on Azure.</span><span class="sxs-lookup"><span data-stu-id="02918-104">Azure Batch lets you run and scale large numbers of batch computing jobs on Azure.</span></span> <span data-ttu-id="02918-105">Batch tasks can run directly on virtual machines (nodes) in a Batch pool, but you can also set up a Batch pool to run tasks in Docker-compatible containers on the nodes.</span><span class="sxs-lookup"><span data-stu-id="02918-105">Batch tasks can run directly on virtual machines (nodes) in a Batch pool, but you can also set up a Batch pool to run tasks in Docker-compatible containers on the nodes.</span></span> <span data-ttu-id="02918-106">This article shows you how to create a pool of compute nodes that support running container tasks, and then run container tasks on the pool.</span><span class="sxs-lookup"><span data-stu-id="02918-106">This article shows you how to create a pool of compute nodes that support running container tasks, and then run container tasks on the pool.</span></span> 

<span data-ttu-id="02918-107">You should be familiar with container concepts and how to create a Batch pool and job.</span><span class="sxs-lookup"><span data-stu-id="02918-107">You should be familiar with container concepts and how to create a Batch pool and job.</span></span> <span data-ttu-id="02918-108">The code examples use the Batch .NET and Python SDKs.</span><span class="sxs-lookup"><span data-stu-id="02918-108">The code examples use the Batch .NET and Python SDKs.</span></span> <span data-ttu-id="02918-109">You can also use other Batch SDKs and tools, including the Azure portal, to create container-enabled Batch pools and to run container tasks.</span><span class="sxs-lookup"><span data-stu-id="02918-109">You can also use other Batch SDKs and tools, including the Azure portal, to create container-enabled Batch pools and to run container tasks.</span></span>

## <a name="why-use-containers"></a><span data-ttu-id="02918-110">Why use containers?</span><span class="sxs-lookup"><span data-stu-id="02918-110">Why use containers?</span></span>

<span data-ttu-id="02918-111">Using containers provides an easy way to run Batch tasks without having to manage an environment and dependencies to run applications.</span><span class="sxs-lookup"><span data-stu-id="02918-111">Using containers provides an easy way to run Batch tasks without having to manage an environment and dependencies to run applications.</span></span> <span data-ttu-id="02918-112">Containers deploy applications as lightweight, portable, self-sufficient units that can run in several different environments.</span><span class="sxs-lookup"><span data-stu-id="02918-112">Containers deploy applications as lightweight, portable, self-sufficient units that can run in several different environments.</span></span> <span data-ttu-id="02918-113">For example, you can build and test a container locally, then upload the container image to a registry in Azure or elsewhere.</span><span class="sxs-lookup"><span data-stu-id="02918-113">For example, you can build and test a container locally, then upload the container image to a registry in Azure or elsewhere.</span></span> <span data-ttu-id="02918-114">The container deployment model ensures that the runtime environment of your application is always correctly installed and configured wherever you host the application.</span><span class="sxs-lookup"><span data-stu-id="02918-114">The container deployment model ensures that the runtime environment of your application is always correctly installed and configured wherever you host the application.</span></span> <span data-ttu-id="02918-115">Container-based tasks in Batch can also take advantage of features of non-container tasks, including application packages and management of resource files and output files.</span><span class="sxs-lookup"><span data-stu-id="02918-115">Container-based tasks in Batch can also take advantage of features of non-container tasks, including application packages and management of resource files and output files.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="02918-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="02918-116">Prerequisites</span></span>

* <span data-ttu-id="02918-117">**SDK versions**: The Batch SDKs support container images as of the following versions:</span><span class="sxs-lookup"><span data-stu-id="02918-117">**SDK versions**: The Batch SDKs support container images as of the following versions:</span></span>
    * <span data-ttu-id="02918-118">Batch REST API version 2017-09-01.6.0</span><span class="sxs-lookup"><span data-stu-id="02918-118">Batch REST API version 2017-09-01.6.0</span></span>
    * <span data-ttu-id="02918-119">Batch .NET SDK version 8.0.0</span><span class="sxs-lookup"><span data-stu-id="02918-119">Batch .NET SDK version 8.0.0</span></span>
    * <span data-ttu-id="02918-120">Batch Python SDK version 4.0</span><span class="sxs-lookup"><span data-stu-id="02918-120">Batch Python SDK version 4.0</span></span>
    * <span data-ttu-id="02918-121">Batch Java SDK version 3.0</span><span class="sxs-lookup"><span data-stu-id="02918-121">Batch Java SDK version 3.0</span></span>
    * <span data-ttu-id="02918-122">Batch Node.js SDK version 3.0</span><span class="sxs-lookup"><span data-stu-id="02918-122">Batch Node.js SDK version 3.0</span></span>

* <span data-ttu-id="02918-123">**Accounts**: In your Azure subscription, you need to create a Batch account and optionally an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="02918-123">**Accounts**: In your Azure subscription, you need to create a Batch account and optionally an Azure Storage account.</span></span>

* <span data-ttu-id="02918-124">**A supported VM image**: Containers are only supported in pools created with the Virtual Machine Configuration, from images detailed in the following section, "Supported virtual machine images."</span><span class="sxs-lookup"><span data-stu-id="02918-124">**A supported VM image**: Containers are only supported in pools created with the Virtual Machine Configuration, from images detailed in the following section, "Supported virtual machine images."</span></span> <span data-ttu-id="02918-125">If you provide a custom image, see the considerations in the following section and the requirements in [Use a managed custom image to create a pool of virtual machines](batch-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="02918-125">If you provide a custom image, see the considerations in the following section and the requirements in [Use a managed custom image to create a pool of virtual machines](batch-custom-images.md).</span></span> 

### <a name="limitations"></a><span data-ttu-id="02918-126">Limitations</span><span class="sxs-lookup"><span data-stu-id="02918-126">Limitations</span></span>

* <span data-ttu-id="02918-127">Batch provides RDMA support only for containers running on Linux pools</span><span class="sxs-lookup"><span data-stu-id="02918-127">Batch provides RDMA support only for containers running on Linux pools</span></span>

* <span data-ttu-id="02918-128">For Windows container workloads, it's recommended to choose a multicore VM size for your pool</span><span class="sxs-lookup"><span data-stu-id="02918-128">For Windows container workloads, it's recommended to choose a multicore VM size for your pool</span></span>

## <a name="supported-virtual-machine-images"></a><span data-ttu-id="02918-129">Supported virtual machine images</span><span class="sxs-lookup"><span data-stu-id="02918-129">Supported virtual machine images</span></span>

<span data-ttu-id="02918-130">Use one of the following supported Windows or Linux images to create a pool of VM compute nodes for container workloads.</span><span class="sxs-lookup"><span data-stu-id="02918-130">Use one of the following supported Windows or Linux images to create a pool of VM compute nodes for container workloads.</span></span> <span data-ttu-id="02918-131">For more information about Marketplace images that are compatible with Batch, see [list of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="02918-131">For more information about Marketplace images that are compatible with Batch, see [list of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span> 

### <a name="windows-images"></a><span data-ttu-id="02918-132">Windows images</span><span class="sxs-lookup"><span data-stu-id="02918-132">Windows images</span></span>

<span data-ttu-id="02918-133">For Windows container workloads, Batch currently supports the **Windows Server 2016 Datacenter with Containers** image in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02918-133">For Windows container workloads, Batch currently supports the **Windows Server 2016 Datacenter with Containers** image in the Azure Marketplace.</span></span> <span data-ttu-id="02918-134">Only Docker container images are supported on Windows.</span><span class="sxs-lookup"><span data-stu-id="02918-134">Only Docker container images are supported on Windows.</span></span>

<span data-ttu-id="02918-135">You can also create custom images from VMs running Docker on Windows.</span><span class="sxs-lookup"><span data-stu-id="02918-135">You can also create custom images from VMs running Docker on Windows.</span></span>

### <a name="linux-images"></a><span data-ttu-id="02918-136">Linux images</span><span class="sxs-lookup"><span data-stu-id="02918-136">Linux images</span></span>

<span data-ttu-id="02918-137">For Linux container workloads, Batch currently supports the following Linux images published by Microsoft Azure Batch in the Azure Marketplace:</span><span class="sxs-lookup"><span data-stu-id="02918-137">For Linux container workloads, Batch currently supports the following Linux images published by Microsoft Azure Batch in the Azure Marketplace:</span></span>

* <span data-ttu-id="02918-138">**CentOS for Azure Batch container pools**</span><span class="sxs-lookup"><span data-stu-id="02918-138">**CentOS for Azure Batch container pools**</span></span>

* <span data-ttu-id="02918-139">**CentOS (with RDMA drivers) for Azure Batch container pools**</span><span class="sxs-lookup"><span data-stu-id="02918-139">**CentOS (with RDMA drivers) for Azure Batch container pools**</span></span>

* <span data-ttu-id="02918-140">**Ubuntu Server for Azure Batch container pools**</span><span class="sxs-lookup"><span data-stu-id="02918-140">**Ubuntu Server for Azure Batch container pools**</span></span>

* <span data-ttu-id="02918-141">**Ubuntu Server (with RDMA drivers) for Azure Batch container pools**</span><span class="sxs-lookup"><span data-stu-id="02918-141">**Ubuntu Server (with RDMA drivers) for Azure Batch container pools**</span></span>

<span data-ttu-id="02918-142">These images are only supported for use in Azure Batch pools.</span><span class="sxs-lookup"><span data-stu-id="02918-142">These images are only supported for use in Azure Batch pools.</span></span> <span data-ttu-id="02918-143">They feature:</span><span class="sxs-lookup"><span data-stu-id="02918-143">They feature:</span></span>

* <span data-ttu-id="02918-144">A pre-installed [Moby](https://github.com/moby/moby) container runtime</span><span class="sxs-lookup"><span data-stu-id="02918-144">A pre-installed [Moby](https://github.com/moby/moby) container runtime</span></span> 

* <span data-ttu-id="02918-145">Pre-installed NVIDIA GPU drivers, to streamline deployment on Azure N-series VMs</span><span class="sxs-lookup"><span data-stu-id="02918-145">Pre-installed NVIDIA GPU drivers, to streamline deployment on Azure N-series VMs</span></span>

* <span data-ttu-id="02918-146">Images with or without pre-installed RDMA drivers; these drivers allow pool nodes to access the Azure RDMA network when deployed on RDMA-capable VM sizes</span><span class="sxs-lookup"><span data-stu-id="02918-146">Images with or without pre-installed RDMA drivers; these drivers allow pool nodes to access the Azure RDMA network when deployed on RDMA-capable VM sizes</span></span>  

<span data-ttu-id="02918-147">You can also create custom images from VMs running Docker on one of the Linux distributions that is compatible with Batch.</span><span class="sxs-lookup"><span data-stu-id="02918-147">You can also create custom images from VMs running Docker on one of the Linux distributions that is compatible with Batch.</span></span> <span data-ttu-id="02918-148">If you choose to provide your own custom Linux image, see the instructions in [Use a managed custom image to create a pool of virtual machines](batch-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="02918-148">If you choose to provide your own custom Linux image, see the instructions in [Use a managed custom image to create a pool of virtual machines](batch-custom-images.md).</span></span>

<span data-ttu-id="02918-149">For Docker support on a custom image, install [Docker Community Edition (CE)](https://www.docker.com/community-edition) or [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition).</span><span class="sxs-lookup"><span data-stu-id="02918-149">For Docker support on a custom image, install [Docker Community Edition (CE)](https://www.docker.com/community-edition) or [Docker Enterprise Edition (EE)](https://www.docker.com/enterprise-edition).</span></span>

<span data-ttu-id="02918-150">Additional considerations for using a custom Linux image:</span><span class="sxs-lookup"><span data-stu-id="02918-150">Additional considerations for using a custom Linux image:</span></span>

* <span data-ttu-id="02918-151">To take advantage of the GPU performance of Azure N-series sizes when using a custom image, pre-install NVIDIA drivers.</span><span class="sxs-lookup"><span data-stu-id="02918-151">To take advantage of the GPU performance of Azure N-series sizes when using a custom image, pre-install NVIDIA drivers.</span></span> <span data-ttu-id="02918-152">Also, you need to install the Docker Engine Utility for NVIDIA GPUs, [NVIDIA Docker](https://github.com/NVIDIA/nvidia-docker).</span><span class="sxs-lookup"><span data-stu-id="02918-152">Also, you need to install the Docker Engine Utility for NVIDIA GPUs, [NVIDIA Docker](https://github.com/NVIDIA/nvidia-docker).</span></span>

* <span data-ttu-id="02918-153">To access the Azure RDMA network, use an RDMA-capable VM size.</span><span class="sxs-lookup"><span data-stu-id="02918-153">To access the Azure RDMA network, use an RDMA-capable VM size.</span></span> <span data-ttu-id="02918-154">Necessary RDMA drivers are installed in the CentOS HPC and Ubuntu images supported by Batch.</span><span class="sxs-lookup"><span data-stu-id="02918-154">Necessary RDMA drivers are installed in the CentOS HPC and Ubuntu images supported by Batch.</span></span> <span data-ttu-id="02918-155">Additional configuration may be needed to run MPI workloads.</span><span class="sxs-lookup"><span data-stu-id="02918-155">Additional configuration may be needed to run MPI workloads.</span></span> <span data-ttu-id="02918-156">See [Use RDMA-capable or GPU-enabled instances in Batch pool](batch-pool-compute-intensive-sizes.md).</span><span class="sxs-lookup"><span data-stu-id="02918-156">See [Use RDMA-capable or GPU-enabled instances in Batch pool](batch-pool-compute-intensive-sizes.md).</span></span>


## <a name="container-configuration-for-batch-pool"></a><span data-ttu-id="02918-157">Container configuration for Batch pool</span><span class="sxs-lookup"><span data-stu-id="02918-157">Container configuration for Batch pool</span></span>

<span data-ttu-id="02918-158">To enable a Batch pool to run container workloads, you must specify [ContainerConfiguration](/dotnet/api/microsoft.azure.batch.containerconfiguration) settings in the pool's [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object.</span><span class="sxs-lookup"><span data-stu-id="02918-158">To enable a Batch pool to run container workloads, you must specify [ContainerConfiguration](/dotnet/api/microsoft.azure.batch.containerconfiguration) settings in the pool's [VirtualMachineConfiguration](/dotnet/api/microsoft.azure.batch.virtualmachineconfiguration) object.</span></span> <span data-ttu-id="02918-159">(This article provides links to the Batch .NET API reference.</span><span class="sxs-lookup"><span data-stu-id="02918-159">(This article provides links to the Batch .NET API reference.</span></span> <span data-ttu-id="02918-160">Corresponding settings are in the [Batch Python](/python/api/azure.batch) API.)</span><span class="sxs-lookup"><span data-stu-id="02918-160">Corresponding settings are in the [Batch Python](/python/api/azure.batch) API.)</span></span>

<span data-ttu-id="02918-161">You can create a container-enabled pool with or without prefetched container images, as shown in the following examples.</span><span class="sxs-lookup"><span data-stu-id="02918-161">You can create a container-enabled pool with or without prefetched container images, as shown in the following examples.</span></span> <span data-ttu-id="02918-162">The pull (or prefetch) process lets you pre-load container images from either Docker Hub or another container registry on the Internet.</span><span class="sxs-lookup"><span data-stu-id="02918-162">The pull (or prefetch) process lets you pre-load container images from either Docker Hub or another container registry on the Internet.</span></span> <span data-ttu-id="02918-163">For best performance, use an [Azure container registry](../container-registry/container-registry-intro.md) in the same region as the Batch account.</span><span class="sxs-lookup"><span data-stu-id="02918-163">For best performance, use an [Azure container registry](../container-registry/container-registry-intro.md) in the same region as the Batch account.</span></span>

<span data-ttu-id="02918-164">The advantage of prefetching container images is that when tasks first start running they don't have to wait for the container image to download.</span><span class="sxs-lookup"><span data-stu-id="02918-164">The advantage of prefetching container images is that when tasks first start running they don't have to wait for the container image to download.</span></span> <span data-ttu-id="02918-165">The container configuration pulls container images to the VMs when the pool is created.</span><span class="sxs-lookup"><span data-stu-id="02918-165">The container configuration pulls container images to the VMs when the pool is created.</span></span> <span data-ttu-id="02918-166">Tasks that run on the pool can then reference the list of container images and container run options.</span><span class="sxs-lookup"><span data-stu-id="02918-166">Tasks that run on the pool can then reference the list of container images and container run options.</span></span>


### <a name="pool-without-prefetched-container-images"></a><span data-ttu-id="02918-167">Pool without prefetched container images</span><span class="sxs-lookup"><span data-stu-id="02918-167">Pool without prefetched container images</span></span>

<span data-ttu-id="02918-168">To configure a container-enabled pool without prefetched container images, define `ContainerConfiguration` and `VirtualMachineConfiguration` objects as shown in the following Python example.</span><span class="sxs-lookup"><span data-stu-id="02918-168">To configure a container-enabled pool without prefetched container images, define `ContainerConfiguration` and `VirtualMachineConfiguration` objects as shown in the following Python example.</span></span> <span data-ttu-id="02918-169">This example uses the Ubuntu Server for Azure Batch container pools image from the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="02918-169">This example uses the Ubuntu Server for Azure Batch container pools image from the Marketplace.</span></span>


```python
image_ref_to_use = batch.models.ImageReference(
        publisher='microsoft-azure-batch',
        offer='ubuntu-server-container',
        sku='16-04-lts',
        version='latest')

"""
Specify container configuration. This is required even though there are no prefetched images.
"""

container_conf = batch.models.ContainerConfiguration()

new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batch.models.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            container_configuration=container_conf,
            node_agent_sku_id='batch.node.ubuntu 16.04'),
        vm_size='STANDARD_D1_V2',
        target_dedicated_nodes=1)
...
```


### <a name="prefetch-images-for-container-configuration"></a><span data-ttu-id="02918-170">Prefetch images for container configuration</span><span class="sxs-lookup"><span data-stu-id="02918-170">Prefetch images for container configuration</span></span>

<span data-ttu-id="02918-171">To prefetch container images on the pool, add the list of container images (`container_image_names`, in Python) to the `ContainerConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="02918-171">To prefetch container images on the pool, add the list of container images (`container_image_names`, in Python) to the `ContainerConfiguration`.</span></span> 

<span data-ttu-id="02918-172">The following basic Python example shows how to prefetch a standard Ubuntu container image from [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="02918-172">The following basic Python example shows how to prefetch a standard Ubuntu container image from [Docker Hub](https://hub.docker.com).</span></span>

```python
image_ref_to_use = batch.models.ImageReference(
    publisher='microsoft-azure-batch',
    offer='ubuntu-server-container',
    sku='16-04-lts',
    version='latest')

"""
Specify container configuration, fetching the official Ubuntu container image from Docker Hub. 
"""

container_conf = batch.models.ContainerConfiguration(container_image_names=['ubuntu'])

new_pool = batch.models.PoolAddParameter(
    id=pool_id,
    virtual_machine_configuration=batch.models.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        container_configuration=container_conf,
        node_agent_sku_id='batch.node.ubuntu 16.04'),
    vm_size='STANDARD_D1_V2',
    target_dedicated_nodes=1)
...
```


<span data-ttu-id="02918-173">The following example C# example assumes that you want to prefetch a TensorFlow image from [Docker Hub](https://hub.docker.com).</span><span class="sxs-lookup"><span data-stu-id="02918-173">The following example C# example assumes that you want to prefetch a TensorFlow image from [Docker Hub](https://hub.docker.com).</span></span> <span data-ttu-id="02918-174">This example includes a start task that runs in the VM host on the pool nodes.</span><span class="sxs-lookup"><span data-stu-id="02918-174">This example includes a start task that runs in the VM host on the pool nodes.</span></span> <span data-ttu-id="02918-175">You might run a start task in the host, for example, to mount a file server that can be accessed from the containers.</span><span class="sxs-lookup"><span data-stu-id="02918-175">You might run a start task in the host, for example, to mount a file server that can be accessed from the containers.</span></span>

```csharp

ImageReference imageReference = new ImageReference(
    publisher: "microsoft-azure-batch",
    offer: "ubuntu-server-container",
    sku: "16-04-lts",
    version: "latest");

// Specify container configuration, prefetching Docker images
ContainerConfiguration containerConfig = new ContainerConfiguration(
    containerImageNames: new List<string> { "tensorflow/tensorflow:latest-gpu" } );

// VM configuration
VirtualMachineConfiguration virtualMachineConfiguration = new VirtualMachineConfiguration(
    imageReference: imageReference,
    containerConfiguration: containerConfig,
    nodeAgentSkuId: "batch.node.ubuntu 16.04");

// Set a native host command line start task
StartTask startTaskNative = new StartTask( CommandLine: "<native-host-command-line>" );

// Create pool
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 4,
    virtualMachineSize: "Standard_NC6",
    virtualMachineConfiguration: virtualMachineConfiguration, startTaskContainer);
...
```


### <a name="prefetch-images-from-a-private-container-registry"></a><span data-ttu-id="02918-176">Prefetch images from a private container registry</span><span class="sxs-lookup"><span data-stu-id="02918-176">Prefetch images from a private container registry</span></span>

<span data-ttu-id="02918-177">You can also prefetch container images by authenticating to a private container registry server.</span><span class="sxs-lookup"><span data-stu-id="02918-177">You can also prefetch container images by authenticating to a private container registry server.</span></span> <span data-ttu-id="02918-178">In the following example, the `ContainerConfiguration` and `VirtualMachineConfiguration` objects prefetch a private TensorFlow image from a private Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="02918-178">In the following example, the `ContainerConfiguration` and `VirtualMachineConfiguration` objects prefetch a private TensorFlow image from a private Azure container registry.</span></span> <span data-ttu-id="02918-179">The image reference is the same as in the previous example.</span><span class="sxs-lookup"><span data-stu-id="02918-179">The image reference is the same as in the previous example.</span></span>

```csharp
// Specify a container registry
ContainerRegistry containerRegistry = new ContainerRegistry (
    registryServer: "myContainerRegistry.azurecr.io",
    username: "myUserName",
    password: "myPassword");

// Create container configuration, prefetching Docker images from the container registry
ContainerConfiguration containerConfig = new ContainerConfiguration(
    containerImageNames: new List<string> {
        "myContainerRegistry.azurecr.io/tensorflow/tensorflow:latest-gpu" },
    containerRegistries: new List<ContainerRegistry> { containerRegistry } );

// VM configuration
VirtualMachineConfiguration virtualMachineConfiguration = new VirtualMachineConfiguration(
    imageReference: imageReference,
    containerConfiguration: containerConfig,
    nodeAgentSkuId: "batch.node.ubuntu 16.04");

// Create pool
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 4,
    virtualMachineSize: "Standard_NC6",
    virtualMachineConfiguration: virtualMachineConfiguration);
...
```


## <a name="container-settings-for-the-task"></a><span data-ttu-id="02918-180">Container settings for the task</span><span class="sxs-lookup"><span data-stu-id="02918-180">Container settings for the task</span></span>

<span data-ttu-id="02918-181">To run container tasks on the compute nodes, you must specify container-specific settings such as task run options, images to use, and registry.</span><span class="sxs-lookup"><span data-stu-id="02918-181">To run container tasks on the compute nodes, you must specify container-specific settings such as task run options, images to use, and registry.</span></span>

<span data-ttu-id="02918-182">Use the `ContainerSettings` property of the task classes to configure container-specific settings.</span><span class="sxs-lookup"><span data-stu-id="02918-182">Use the `ContainerSettings` property of the task classes to configure container-specific settings.</span></span> <span data-ttu-id="02918-183">These settings are defined by the [TaskContainerSettings](/dotnet/api/microsoft.azure.batch.taskcontainersettings) class.</span><span class="sxs-lookup"><span data-stu-id="02918-183">These settings are defined by the [TaskContainerSettings](/dotnet/api/microsoft.azure.batch.taskcontainersettings) class.</span></span>

<span data-ttu-id="02918-184">If you run tasks on container images, the [cloud task](/dotnet/api/microsoft.azure.batch.cloudtask) and [job manager task](/dotnet/api/microsoft.azure.batch.cloudjob.jobmanagertask) require container settings.</span><span class="sxs-lookup"><span data-stu-id="02918-184">If you run tasks on container images, the [cloud task](/dotnet/api/microsoft.azure.batch.cloudtask) and [job manager task](/dotnet/api/microsoft.azure.batch.cloudjob.jobmanagertask) require container settings.</span></span> <span data-ttu-id="02918-185">However, the [start task](/dotnet/api/microsoft.azure.batch.starttask), [job preparation task](/dotnet/api/microsoft.azure.batch.cloudjob.jobpreparationtask), and [job release task](/dotnet/api/microsoft.azure.batch.cloudjob.jobreleasetask) do not require container settings (that is, they can run within a container context or directly on the node).</span><span class="sxs-lookup"><span data-stu-id="02918-185">However, the [start task](/dotnet/api/microsoft.azure.batch.starttask), [job preparation task](/dotnet/api/microsoft.azure.batch.cloudjob.jobpreparationtask), and [job release task](/dotnet/api/microsoft.azure.batch.cloudjob.jobreleasetask) do not require container settings (that is, they can run within a container context or directly on the node).</span></span>

<span data-ttu-id="02918-186">The command line for an Azure Batch container task executes in a working directory in the container that is very similar to the environment Batch sets up for a regular (non-container) task:</span><span class="sxs-lookup"><span data-stu-id="02918-186">The command line for an Azure Batch container task executes in a working directory in the container that is very similar to the environment Batch sets up for a regular (non-container) task:</span></span>

* <span data-ttu-id="02918-187">All directories recursively below the `AZ_BATCH_NODE_ROOT_DIR` (the root of Azure Batch directories on the node) are mapped into the container</span><span class="sxs-lookup"><span data-stu-id="02918-187">All directories recursively below the `AZ_BATCH_NODE_ROOT_DIR` (the root of Azure Batch directories on the node) are mapped into the container</span></span>
* <span data-ttu-id="02918-188">All task environment variables are mapped into the container</span><span class="sxs-lookup"><span data-stu-id="02918-188">All task environment variables are mapped into the container</span></span>
* <span data-ttu-id="02918-189">The application working directory is set the same as for a regular task, so you can use features such as application packages and resource files</span><span class="sxs-lookup"><span data-stu-id="02918-189">The application working directory is set the same as for a regular task, so you can use features such as application packages and resource files</span></span>

<span data-ttu-id="02918-190">Because Batch changes the default working directory in your container, the task runs in a location different from the typical container entry point (for example, `c:\` by default on a Windows container, or `/` on Linux).</span><span class="sxs-lookup"><span data-stu-id="02918-190">Because Batch changes the default working directory in your container, the task runs in a location different from the typical container entry point (for example, `c:\` by default on a Windows container, or `/` on Linux).</span></span> <span data-ttu-id="02918-191">Make sure that your task command line or container entry point specifies an absolute path, if it isn't already configured that way.</span><span class="sxs-lookup"><span data-stu-id="02918-191">Make sure that your task command line or container entry point specifies an absolute path, if it isn't already configured that way.</span></span>

<span data-ttu-id="02918-192">The following Python snippet shows a basic command line running in an Ubuntu container pulled from Docker Hub.</span><span class="sxs-lookup"><span data-stu-id="02918-192">The following Python snippet shows a basic command line running in an Ubuntu container pulled from Docker Hub.</span></span> <span data-ttu-id="02918-193">The container run options are additional arguments to the `docker create` command that the task runs.</span><span class="sxs-lookup"><span data-stu-id="02918-193">The container run options are additional arguments to the `docker create` command that the task runs.</span></span> <span data-ttu-id="02918-194">Here, the `--rm` option removes the container after the task finishes.</span><span class="sxs-lookup"><span data-stu-id="02918-194">Here, the `--rm` option removes the container after the task finishes.</span></span>

```python
task_id = 'sampletask'
task_container_settings = batch.models.TaskContainerSettings(
    image_name='ubuntu', 
    container_run_options='--rm')
task = batch.models.TaskAddParameter(
    id=task_id,
    command_line='/bin/echo hello',
    container_settings=task_container_settings
)

```

<span data-ttu-id="02918-195">The following C# example shows basic container settings for a cloud task:</span><span class="sxs-lookup"><span data-stu-id="02918-195">The following C# example shows basic container settings for a cloud task:</span></span>

```csharp
// Simple container task command

string cmdLine = "c:\myApp.exe";

TaskContainerSettings cmdContainerSettings = new TaskContainerSettings (
    imageName: "tensorflow/tensorflow:latest-gpu",
    containerRunOptions: "--rm --read-only"
    );

CloudTask containerTask = new CloudTask (
    id: "Task1",
    containerSettings: cmdContainerSettings,
    commandLine: cmdLine); 
```


## <a name="next-steps"></a><span data-ttu-id="02918-196">Next steps</span><span class="sxs-lookup"><span data-stu-id="02918-196">Next steps</span></span>

* <span data-ttu-id="02918-197">Also see the [Batch Shipyard](https://github.com/Azure/batch-shipyard) toolkit for easy deployment of container workloads on Azure Batch through [Shipyard recipes](https://github.com/Azure/batch-shipyard/tree/master/recipes).</span><span class="sxs-lookup"><span data-stu-id="02918-197">Also see the [Batch Shipyard](https://github.com/Azure/batch-shipyard) toolkit for easy deployment of container workloads on Azure Batch through [Shipyard recipes](https://github.com/Azure/batch-shipyard/tree/master/recipes).</span></span>

* <span data-ttu-id="02918-198">For more information on installing and using Docker CE on Linux, see the [Docker](https://docs.docker.com/engine/installation/) documentation.</span><span class="sxs-lookup"><span data-stu-id="02918-198">For more information on installing and using Docker CE on Linux, see the [Docker](https://docs.docker.com/engine/installation/) documentation.</span></span>

* <span data-ttu-id="02918-199">For more information on using custom images, see [Use a managed custom image to create a pool of virtual machines ](batch-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="02918-199">For more information on using custom images, see [Use a managed custom image to create a pool of virtual machines ](batch-custom-images.md).</span></span>

* <span data-ttu-id="02918-200">Learn more about the [Moby project](https://mobyproject.org/), a framework for creating container-based systems.</span><span class="sxs-lookup"><span data-stu-id="02918-200">Learn more about the [Moby project](https://mobyproject.org/), a framework for creating container-based systems.</span></span>