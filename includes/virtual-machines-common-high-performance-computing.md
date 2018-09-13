---
title: include file
description: include file
services: virtual-machines-linux, virtual-machines-windows
author: dlepow
ms.service: multiple
ms.topic: include
ms.date: 07/02/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 5a6c5498b4607719199363b5f6d93d3b42ccec0d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868599"
---
<span data-ttu-id="50c7f-103">Organizations have large-scale computing needs.</span><span class="sxs-lookup"><span data-stu-id="50c7f-103">Organizations have large-scale computing needs.</span></span> <span data-ttu-id="50c7f-104">These Big Compute workloads include engineering design and analysis, financial risk calculations, image rendering, complex modeling, Monte Carlo simulations, and more.</span><span class="sxs-lookup"><span data-stu-id="50c7f-104">These Big Compute workloads include engineering design and analysis, financial risk calculations, image rendering, complex modeling, Monte Carlo simulations, and more.</span></span> 

<span data-ttu-id="50c7f-105">Use the Azure cloud to efficiently run compute-intensive Linux and Windows workloads, from parallel batch jobs to traditional HPC simulations.</span><span class="sxs-lookup"><span data-stu-id="50c7f-105">Use the Azure cloud to efficiently run compute-intensive Linux and Windows workloads, from parallel batch jobs to traditional HPC simulations.</span></span> <span data-ttu-id="50c7f-106">Run your HPC and batch workloads on Azure infrastructure, with your choice of compute services, grid managers, Marketplace solutions, and vendor-hosted (SaaS) applications.</span><span class="sxs-lookup"><span data-stu-id="50c7f-106">Run your HPC and batch workloads on Azure infrastructure, with your choice of compute services, grid managers, Marketplace solutions, and vendor-hosted (SaaS) applications.</span></span> <span data-ttu-id="50c7f-107">Azure provides flexible solutions to distribute work and scale to thousands of VMs or cores and then scale down when you need fewer resources.</span><span class="sxs-lookup"><span data-stu-id="50c7f-107">Azure provides flexible solutions to distribute work and scale to thousands of VMs or cores and then scale down when you need fewer resources.</span></span> 



## <a name="solution-options"></a><span data-ttu-id="50c7f-108">Solution options</span><span class="sxs-lookup"><span data-stu-id="50c7f-108">Solution options</span></span>



* <span data-ttu-id="50c7f-109">**Do-it-yourself solutions**</span><span class="sxs-lookup"><span data-stu-id="50c7f-109">**Do-it-yourself solutions**</span></span>
    * <span data-ttu-id="50c7f-110">Set up your own cluster environment in Azure virtual machines or [virtual machine scale sets](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="50c7f-110">Set up your own cluster environment in Azure virtual machines or [virtual machine scale sets](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md).</span></span> 
    * <span data-ttu-id="50c7f-111">Lift and shift an on-premises cluster, or deploy a new cluster in Azure for additional capacity.</span><span class="sxs-lookup"><span data-stu-id="50c7f-111">Lift and shift an on-premises cluster, or deploy a new cluster in Azure for additional capacity.</span></span> 
    * <span data-ttu-id="50c7f-112">Use Azure Resource Manager templates to deploy leading [workload managers](#workload-managers), infrastructure, and [applications](#hpc-applications).</span><span class="sxs-lookup"><span data-stu-id="50c7f-112">Use Azure Resource Manager templates to deploy leading [workload managers](#workload-managers), infrastructure, and [applications](#hpc-applications).</span></span> 
    * <span data-ttu-id="50c7f-113">Choose [HPC and GPU VM sizes](#hpc-and-gpu-sizes) that include specialized hardware and network connections for MPI or GPU workloads.</span><span class="sxs-lookup"><span data-stu-id="50c7f-113">Choose [HPC and GPU VM sizes](#hpc-and-gpu-sizes) that include specialized hardware and network connections for MPI or GPU workloads.</span></span> 
    * <span data-ttu-id="50c7f-114">Add [high performance storage](#hpc-storage) for I/O-intensive workloads.</span><span class="sxs-lookup"><span data-stu-id="50c7f-114">Add [high performance storage](#hpc-storage) for I/O-intensive workloads.</span></span>
* <span data-ttu-id="50c7f-115">**Hybrid solutions**</span><span class="sxs-lookup"><span data-stu-id="50c7f-115">**Hybrid solutions**</span></span>
    * <span data-ttu-id="50c7f-116">Extend your on-premises solution to offload ("burst") peak workloads to Azure infrastructure</span><span class="sxs-lookup"><span data-stu-id="50c7f-116">Extend your on-premises solution to offload ("burst") peak workloads to Azure infrastructure</span></span>
    * <span data-ttu-id="50c7f-117">Use cloud compute on-demand with your existing [workload manager](#workload-manager).</span><span class="sxs-lookup"><span data-stu-id="50c7f-117">Use cloud compute on-demand with your existing [workload manager](#workload-manager).</span></span>
    * <span data-ttu-id="50c7f-118">Take advantage of [HPC and GPU VM sizes](#hpc-and-gpu-sizes) for MPI or GPU workloads.</span><span class="sxs-lookup"><span data-stu-id="50c7f-118">Take advantage of [HPC and GPU VM sizes](#hpc-and-gpu-sizes) for MPI or GPU workloads.</span></span>
* <span data-ttu-id="50c7f-119">**Big Compute solutions as a service**</span><span class="sxs-lookup"><span data-stu-id="50c7f-119">**Big Compute solutions as a service**</span></span>
    * <span data-ttu-id="50c7f-120">Develop custom Big Compute solutions and workflows using [Azure Batch](#azure-batch) and related [Azure services](#related-azure-services).</span><span class="sxs-lookup"><span data-stu-id="50c7f-120">Develop custom Big Compute solutions and workflows using [Azure Batch](#azure-batch) and related [Azure services](#related-azure-services).</span></span>
    * <span data-ttu-id="50c7f-121">Run Azure-enabled engineering and simulation solutions from vendors including [Altair](http://www.altair.com/), [Rescale](https://www.rescale.com/azure/), and [Cycle Computing](https://cyclecomputing.com/) (now [joined with Microsoft](https://blogs.microsoft.com/blog/2017/08/15/microsoft-acquires-cycle-computing-accelerate-big-computing-cloud/)).</span><span class="sxs-lookup"><span data-stu-id="50c7f-121">Run Azure-enabled engineering and simulation solutions from vendors including [Altair](http://www.altair.com/), [Rescale](https://www.rescale.com/azure/), and [Cycle Computing](https://cyclecomputing.com/) (now [joined with Microsoft](https://blogs.microsoft.com/blog/2017/08/15/microsoft-acquires-cycle-computing-accelerate-big-computing-cloud/)).</span></span>
    * <span data-ttu-id="50c7f-122">Use a [Cray supercomputer](https://www.cray.com/solutions/supercomputing-as-a-service/cray-in-azure) as a service hosted in Azure.</span><span class="sxs-lookup"><span data-stu-id="50c7f-122">Use a [Cray supercomputer](https://www.cray.com/solutions/supercomputing-as-a-service/cray-in-azure) as a service hosted in Azure.</span></span>
* <span data-ttu-id="50c7f-123">**Marketplace solutions**</span><span class="sxs-lookup"><span data-stu-id="50c7f-123">**Marketplace solutions**</span></span>
    * <span data-ttu-id="50c7f-124">Use the scale of [HPC applications](#hpc-applications) and [solutions](#marketplace-solutions) offered in the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/).</span><span class="sxs-lookup"><span data-stu-id="50c7f-124">Use the scale of [HPC applications](#hpc-applications) and [solutions](#marketplace-solutions) offered in the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/).</span></span> 
    


<span data-ttu-id="50c7f-125">The following sections provide more information about the supporting technologies and links to guidance.</span><span class="sxs-lookup"><span data-stu-id="50c7f-125">The following sections provide more information about the supporting technologies and links to guidance.</span></span>



## <a name="marketplace-solutions"></a><span data-ttu-id="50c7f-126">Marketplace solutions</span><span class="sxs-lookup"><span data-stu-id="50c7f-126">Marketplace solutions</span></span>

<span data-ttu-id="50c7f-127">Visit the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) for Linux and Windows VM images and solutions designed for HPC.</span><span class="sxs-lookup"><span data-stu-id="50c7f-127">Visit the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) for Linux and Windows VM images and solutions designed for HPC.</span></span> <span data-ttu-id="50c7f-128">Examples include:</span><span class="sxs-lookup"><span data-stu-id="50c7f-128">Examples include:</span></span>

* [<span data-ttu-id="50c7f-129">RogueWave CentOS-based HPC</span><span class="sxs-lookup"><span data-stu-id="50c7f-129">RogueWave CentOS-based HPC</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/RogueWave.CentOSbased73HPC?tab=Overview)
* [<span data-ttu-id="50c7f-130">SUSE Linux Enterprise Server for HPC</span><span class="sxs-lookup"><span data-stu-id="50c7f-130">SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)
*  [<span data-ttu-id="50c7f-131">TIBCO Grid Server Engine</span><span class="sxs-lookup"><span data-stu-id="50c7f-131">TIBCO Grid Server Engine</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/tibco-software.gridserverlinuxengine?tab=Overview)
* [<span data-ttu-id="50c7f-132">Azure Data Science VM for Windows and Linux</span><span class="sxs-lookup"><span data-stu-id="50c7f-132">Azure Data Science VM for Windows and Linux</span></span>](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md)
* [<span data-ttu-id="50c7f-133">D3View</span><span class="sxs-lookup"><span data-stu-id="50c7f-133">D3View</span></span>](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/xfinityinc.d3view-v5?tab=Overview)
* [<span data-ttu-id="50c7f-134">UberCloud</span><span class="sxs-lookup"><span data-stu-id="50c7f-134">UberCloud</span></span>](https://azure.microsoft.com/search/marketplace/?q=ubercloud)
* [<span data-ttu-id="50c7f-135">Intel Cloud Edition for Lustre</span><span class="sxs-lookup"><span data-stu-id="50c7f-135">Intel Cloud Edition for Lustre</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/intel.intel-cloud-edition-gs)


 
## <a name="hpc-applications"></a><span data-ttu-id="50c7f-136">HPC applications</span><span class="sxs-lookup"><span data-stu-id="50c7f-136">HPC applications</span></span>

<span data-ttu-id="50c7f-137">Run custom or commercial HPC applications in Azure.</span><span class="sxs-lookup"><span data-stu-id="50c7f-137">Run custom or commercial HPC applications in Azure.</span></span> <span data-ttu-id="50c7f-138">Several examples in this section are benchmarked to scale efficiently with additional VMs or compute cores.</span><span class="sxs-lookup"><span data-stu-id="50c7f-138">Several examples in this section are benchmarked to scale efficiently with additional VMs or compute cores.</span></span> <span data-ttu-id="50c7f-139">Visit the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace) for ready-to-deploy solutions.</span><span class="sxs-lookup"><span data-stu-id="50c7f-139">Visit the [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace) for ready-to-deploy solutions.</span></span>

> [!NOTE]
> <span data-ttu-id="50c7f-140">Check with the vendor of any commercial application for licensing or other restrictions for running in the cloud.</span><span class="sxs-lookup"><span data-stu-id="50c7f-140">Check with the vendor of any commercial application for licensing or other restrictions for running in the cloud.</span></span> <span data-ttu-id="50c7f-141">Not all vendors offer pay-as-you-go licensing.</span><span class="sxs-lookup"><span data-stu-id="50c7f-141">Not all vendors offer pay-as-you-go licensing.</span></span> <span data-ttu-id="50c7f-142">You might need a licensing server in the cloud for your solution, or connect to an on-premises license server.</span><span class="sxs-lookup"><span data-stu-id="50c7f-142">You might need a licensing server in the cloud for your solution, or connect to an on-premises license server.</span></span>

### <a name="engineering-applications"></a><span data-ttu-id="50c7f-143">Engineering applications</span><span class="sxs-lookup"><span data-stu-id="50c7f-143">Engineering applications</span></span>


* [<span data-ttu-id="50c7f-144">Altair RADIOSS</span><span class="sxs-lookup"><span data-stu-id="50c7f-144">Altair RADIOSS</span></span>](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/)
* [<span data-ttu-id="50c7f-145">ANSYS CFD</span><span class="sxs-lookup"><span data-stu-id="50c7f-145">ANSYS CFD</span></span>](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/)
* [<span data-ttu-id="50c7f-146">MATLAB Distributed Computing Server</span><span class="sxs-lookup"><span data-stu-id="50c7f-146">MATLAB Distributed Computing Server</span></span>](../articles/virtual-machines/windows/matlab-mdcs-cluster.md)
* [<span data-ttu-id="50c7f-147">StarCCM+</span><span class="sxs-lookup"><span data-stu-id="50c7f-147">StarCCM+</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/07/07/run-star-ccm-in-an-azure-hpc-cluster/)
* [<span data-ttu-id="50c7f-148">OpenFOAM</span><span class="sxs-lookup"><span data-stu-id="50c7f-148">OpenFOAM</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)



### <a name="graphics-and-rendering"></a><span data-ttu-id="50c7f-149">Graphics and rendering</span><span class="sxs-lookup"><span data-stu-id="50c7f-149">Graphics and rendering</span></span>

* <span data-ttu-id="50c7f-150">[Autodesk Maya, 3ds Max, and Arnold](../articles/batch/batch-rendering-service.md) on Azure Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-150">[Autodesk Maya, 3ds Max, and Arnold](../articles/batch/batch-rendering-service.md) on Azure Batch</span></span> 

### <a name="ai-and-deep-learning"></a><span data-ttu-id="50c7f-151">AI and deep learning</span><span class="sxs-lookup"><span data-stu-id="50c7f-151">AI and deep learning</span></span>

* <span data-ttu-id="50c7f-152">[Batch AI](../articles/batch-ai/overview.md) training for deep learning models</span><span class="sxs-lookup"><span data-stu-id="50c7f-152">[Batch AI](../articles/batch-ai/overview.md) training for deep learning models</span></span>
* [<span data-ttu-id="50c7f-153">Microsoft Cognitive Toolkit</span><span class="sxs-lookup"><span data-stu-id="50c7f-153">Microsoft Cognitive Toolkit</span></span>](https://docs.microsoft.com/cognitive-toolkit/cntk-on-azure)
* [<span data-ttu-id="50c7f-154">Deep Learning VM</span><span class="sxs-lookup"><span data-stu-id="50c7f-154">Deep Learning VM</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning)
* [<span data-ttu-id="50c7f-155">Batch Shipyard recipes for deep learning</span><span class="sxs-lookup"><span data-stu-id="50c7f-155">Batch Shipyard recipes for deep learning</span></span>](https://github.com/Azure/batch-shipyard/tree/master/recipes#deeplearning)






## <a name="hpc-and-gpu-vm-sizes"></a><span data-ttu-id="50c7f-156">HPC and GPU VM sizes</span><span class="sxs-lookup"><span data-stu-id="50c7f-156">HPC and GPU VM sizes</span></span>
<span data-ttu-id="50c7f-157">Azure offers a range of sizes for [Linux](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../articles/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VMs, including sizes designed for compute-intensive workloads.</span><span class="sxs-lookup"><span data-stu-id="50c7f-157">Azure offers a range of sizes for [Linux](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../articles/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) VMs, including sizes designed for compute-intensive workloads.</span></span> <span data-ttu-id="50c7f-158">For example, H16r and H16mr VMs can connect to a high throughput back-end RDMA network.</span><span class="sxs-lookup"><span data-stu-id="50c7f-158">For example, H16r and H16mr VMs can connect to a high throughput back-end RDMA network.</span></span> <span data-ttu-id="50c7f-159">This cloud network can improve the performance of tightly coupled parallel applications running under [Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) or Intel MPI.</span><span class="sxs-lookup"><span data-stu-id="50c7f-159">This cloud network can improve the performance of tightly coupled parallel applications running under [Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) or Intel MPI.</span></span> 

<span data-ttu-id="50c7f-160">N-series VMs feature NVIDIA GPUs designed for compute-intensive or graphics-intensive applications including artificial intelligence (AI) learning and visualization.</span><span class="sxs-lookup"><span data-stu-id="50c7f-160">N-series VMs feature NVIDIA GPUs designed for compute-intensive or graphics-intensive applications including artificial intelligence (AI) learning and visualization.</span></span> 

<span data-ttu-id="50c7f-161">Learn more:</span><span class="sxs-lookup"><span data-stu-id="50c7f-161">Learn more:</span></span>

* <span data-ttu-id="50c7f-162">High performance compute sizes for [Linux](../articles/virtual-machines/linux/sizes-hpc.md) and [Windows](../articles/virtual-machines/windows/sizes-hpc.md) VMs</span><span class="sxs-lookup"><span data-stu-id="50c7f-162">High performance compute sizes for [Linux](../articles/virtual-machines/linux/sizes-hpc.md) and [Windows](../articles/virtual-machines/windows/sizes-hpc.md) VMs</span></span> 
* <span data-ttu-id="50c7f-163">GPU-enabled sizes for [Linux](../articles/virtual-machines/linux/sizes-gpu.md) and [Windows](../articles/virtual-machines/windows/sizes-gpu.md) VMs</span><span class="sxs-lookup"><span data-stu-id="50c7f-163">GPU-enabled sizes for [Linux](../articles/virtual-machines/linux/sizes-gpu.md) and [Windows](../articles/virtual-machines/windows/sizes-gpu.md) VMs</span></span> 

<span data-ttu-id="50c7f-164">Learn how to:</span><span class="sxs-lookup"><span data-stu-id="50c7f-164">Learn how to:</span></span>

* [<span data-ttu-id="50c7f-165">Set up a Linux RDMA cluster to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="50c7f-165">Set up a Linux RDMA cluster to run MPI applications</span></span>](../articles/virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="50c7f-166">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="50c7f-166">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../articles/virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [<span data-ttu-id="50c7f-167">Use compute-intensive VMs in Batch pools</span><span class="sxs-lookup"><span data-stu-id="50c7f-167">Use compute-intensive VMs in Batch pools</span></span>](../articles/batch/batch-pool-compute-intensive-sizes.md)



## <a name="azure-batch"></a><span data-ttu-id="50c7f-168">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-168">Azure Batch</span></span>
<span data-ttu-id="50c7f-169">[Batch](../articles/batch/batch-technical-overview.md) is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span><span class="sxs-lookup"><span data-stu-id="50c7f-169">[Batch](../articles/batch/batch-technical-overview.md) is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="50c7f-170">Azure Batch schedules compute-intensive work to run on a managed pool of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span><span class="sxs-lookup"><span data-stu-id="50c7f-170">Azure Batch schedules compute-intensive work to run on a managed pool of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span> 

<span data-ttu-id="50c7f-171">SaaS providers or developers can use the Batch SDKs and tools to integrate HPC applications or container workloads with Azure, stage data to Azure, and build job execution pipelines.</span><span class="sxs-lookup"><span data-stu-id="50c7f-171">SaaS providers or developers can use the Batch SDKs and tools to integrate HPC applications or container workloads with Azure, stage data to Azure, and build job execution pipelines.</span></span> 

<span data-ttu-id="50c7f-172">Learn how to:</span><span class="sxs-lookup"><span data-stu-id="50c7f-172">Learn how to:</span></span>

* [<span data-ttu-id="50c7f-173">Get started developing with Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-173">Get started developing with Batch</span></span>](../articles/batch/quick-run-dotnet.md)
* [<span data-ttu-id="50c7f-174">Use Azure Batch code samples</span><span class="sxs-lookup"><span data-stu-id="50c7f-174">Use Azure Batch code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* [<span data-ttu-id="50c7f-175">Use low-priority VMs with Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-175">Use low-priority VMs with Batch</span></span>](../articles/batch/batch-low-pri-vms.md)
* [<span data-ttu-id="50c7f-176">Run containerized HPC workloads with Batch Shipyard</span><span class="sxs-lookup"><span data-stu-id="50c7f-176">Run containerized HPC workloads with Batch Shipyard</span></span>](https://github.com/Azure/batch-shipyard)
* [<span data-ttu-id="50c7f-177">Run parallel R workloads on Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-177">Run parallel R workloads on Batch</span></span>](https://github.com/Azure/doAzureParallel)
* [<span data-ttu-id="50c7f-178">Run on-demand Spark jobs on Batch</span><span class="sxs-lookup"><span data-stu-id="50c7f-178">Run on-demand Spark jobs on Batch</span></span>](https://github.com/Azure/aztk)

## <a name="workload-managers"></a><span data-ttu-id="50c7f-179">Workload managers</span><span class="sxs-lookup"><span data-stu-id="50c7f-179">Workload managers</span></span>

<span data-ttu-id="50c7f-180">The following are examples of cluster and workload managers that can run in Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="50c7f-180">The following are examples of cluster and workload managers that can run in Azure infrastructure.</span></span> <span data-ttu-id="50c7f-181">Create stand-alone clusters in Azure VMs or burst to Azure VMs from an on-premises cluster.</span><span class="sxs-lookup"><span data-stu-id="50c7f-181">Create stand-alone clusters in Azure VMs or burst to Azure VMs from an on-premises cluster.</span></span> 
* [<span data-ttu-id="50c7f-182">Alces Flight Compute</span><span class="sxs-lookup"><span data-stu-id="50c7f-182">Alces Flight Compute</span></span>](https://azuremarketplace.microsoft.com/marketplace/apps/alces-flight-limited.alces-flight-compute-solo?tab=Overview)
* [<span data-ttu-id="50c7f-183">TIBCO DataSynapse GridServer</span><span class="sxs-lookup"><span data-stu-id="50c7f-183">TIBCO DataSynapse GridServer</span></span>](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/) 
* [<span data-ttu-id="50c7f-184">Bright Cluster Manager</span><span class="sxs-lookup"><span data-stu-id="50c7f-184">Bright Cluster Manager</span></span>](http://www.brightcomputing.com/technology-partners/microsoft)
* [<span data-ttu-id="50c7f-185">IBM Spectrum Symphony and Symphony LSF</span><span class="sxs-lookup"><span data-stu-id="50c7f-185">IBM Spectrum Symphony and Symphony LSF</span></span>](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/)
* [<span data-ttu-id="50c7f-186">PBS Pro</span><span class="sxs-lookup"><span data-stu-id="50c7f-186">PBS Pro</span></span>](http://pbspro.org)
* <span data-ttu-id="50c7f-187">[Microsoft HPC Pack](https://technet.microsoft.com/library/mt744885.aspx) - see options to run in [Windows](../articles/virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)  and [Linux](../articles/virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VMs</span><span class="sxs-lookup"><span data-stu-id="50c7f-187">[Microsoft HPC Pack](https://technet.microsoft.com/library/mt744885.aspx) - see options to run in [Windows](../articles/virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)  and [Linux](../articles/virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) VMs</span></span> 



## <a name="hpc-storage"></a><span data-ttu-id="50c7f-188">HPC storage</span><span class="sxs-lookup"><span data-stu-id="50c7f-188">HPC storage</span></span>

<span data-ttu-id="50c7f-189">Large-scale Batch and HPC workloads have demands for data storage and access that exceed the capabilities of traditional cloud file systems.</span><span class="sxs-lookup"><span data-stu-id="50c7f-189">Large-scale Batch and HPC workloads have demands for data storage and access that exceed the capabilities of traditional cloud file systems.</span></span> <span data-ttu-id="50c7f-190">Implement parallel file system solutions in Azure such as [Lustre](http://lustre.org/) and [BeeGFS](http://www.beegfs.com/content/).</span><span class="sxs-lookup"><span data-stu-id="50c7f-190">Implement parallel file system solutions in Azure such as [Lustre](http://lustre.org/) and [BeeGFS](http://www.beegfs.com/content/).</span></span>

<span data-ttu-id="50c7f-191">Learn more:</span><span class="sxs-lookup"><span data-stu-id="50c7f-191">Learn more:</span></span>

* [<span data-ttu-id="50c7f-192">Parallel virtual file systems on Azure</span><span class="sxs-lookup"><span data-stu-id="50c7f-192">Parallel virtual file systems on Azure</span></span>](https://azure.microsoft.com/resources/parallel-virtual-file-systems-on-microsoft-azure/)
* <span data-ttu-id="50c7f-193">High performance cloud storage solutions from [Avere](http://www.averesystems.com/about-us/about-avere) (now [joined with Microsoft](https://blogs.microsoft.com/blog/2018/01/03/microsoft-to-acquire-avere-systems-accelerating-high-performance-computing-innovation-for-media-and-entertainment-industry-and-beyond/))</span><span class="sxs-lookup"><span data-stu-id="50c7f-193">High performance cloud storage solutions from [Avere](http://www.averesystems.com/about-us/about-avere) (now [joined with Microsoft](https://blogs.microsoft.com/blog/2018/01/03/microsoft-to-acquire-avere-systems-accelerating-high-performance-computing-innovation-for-media-and-entertainment-industry-and-beyond/))</span></span>


## <a name="related-azure-services"></a><span data-ttu-id="50c7f-194">Related Azure services</span><span class="sxs-lookup"><span data-stu-id="50c7f-194">Related Azure services</span></span>

<span data-ttu-id="50c7f-195">Azure virtual machines, virtual machine scale sets, Batch, and related compute services are the foundation of most Azure HPC solutions.</span><span class="sxs-lookup"><span data-stu-id="50c7f-195">Azure virtual machines, virtual machine scale sets, Batch, and related compute services are the foundation of most Azure HPC solutions.</span></span> <span data-ttu-id="50c7f-196">However, your solution can take advantage of many related Azure services.</span><span class="sxs-lookup"><span data-stu-id="50c7f-196">However, your solution can take advantage of many related Azure services.</span></span> <span data-ttu-id="50c7f-197">Here is a partial list:</span><span class="sxs-lookup"><span data-stu-id="50c7f-197">Here is a partial list:</span></span>

### <a name="storage"></a><span data-ttu-id="50c7f-198">Storage</span><span class="sxs-lookup"><span data-stu-id="50c7f-198">Storage</span></span>

* [<span data-ttu-id="50c7f-199">Blob, table, and queue storage</span><span class="sxs-lookup"><span data-stu-id="50c7f-199">Blob, table, and queue storage</span></span>](../articles/storage/storage-introduction.md)
* [<span data-ttu-id="50c7f-200">File storage</span><span class="sxs-lookup"><span data-stu-id="50c7f-200">File storage</span></span>](../articles/storage/storage-files-introduction.md)

### <a name="data-and-analytics"></a><span data-ttu-id="50c7f-201">Data and analytics</span><span class="sxs-lookup"><span data-stu-id="50c7f-201">Data and analytics</span></span>
* [<span data-ttu-id="50c7f-202">HDInsight</span><span class="sxs-lookup"><span data-stu-id="50c7f-202">HDInsight</span></span>](../articles/hdinsight/hadoop/apache-hadoop-introduction.md)
* [<span data-ttu-id="50c7f-203">Data Factory</span><span class="sxs-lookup"><span data-stu-id="50c7f-203">Data Factory</span></span>](../articles/data-factory/introduction.md)
* [<span data-ttu-id="50c7f-204">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="50c7f-204">Data Lake Store</span></span>](../articles/data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="50c7f-205">Databricks</span><span class="sxs-lookup"><span data-stu-id="50c7f-205">Databricks</span></span>](../articles/azure-databricks/what-is-azure-databricks.md)
* [<span data-ttu-id="50c7f-206">SQL Database</span><span class="sxs-lookup"><span data-stu-id="50c7f-206">SQL Database</span></span>](../articles/sql-database/sql-database-technical-overview.md)

### <a name="ai-and-machine-learning"></a><span data-ttu-id="50c7f-207">AI and machine learning</span><span class="sxs-lookup"><span data-stu-id="50c7f-207">AI and machine learning</span></span>
* [<span data-ttu-id="50c7f-208">Machine Learning Services</span><span class="sxs-lookup"><span data-stu-id="50c7f-208">Machine Learning Services</span></span>](../articles/machine-learning/service/overview-what-is-azure-ml.md)
* [<span data-ttu-id="50c7f-209">Batch AI</span><span class="sxs-lookup"><span data-stu-id="50c7f-209">Batch AI</span></span>](../articles/batch-ai/overview.md)
* [<span data-ttu-id="50c7f-210">Genomics</span><span class="sxs-lookup"><span data-stu-id="50c7f-210">Genomics</span></span>](../articles/genomics/overview-what-is-genomics.md)

### <a name="networking"></a><span data-ttu-id="50c7f-211">Networking</span><span class="sxs-lookup"><span data-stu-id="50c7f-211">Networking</span></span>
* [<span data-ttu-id="50c7f-212">Virtual Network</span><span class="sxs-lookup"><span data-stu-id="50c7f-212">Virtual Network</span></span>](../articles/virtual-network/virtual-networks-overview.md)
* [<span data-ttu-id="50c7f-213">ExpressRoute</span><span class="sxs-lookup"><span data-stu-id="50c7f-213">ExpressRoute</span></span>](../articles/expressroute/expressroute-introduction.md)

### <a name="containers"></a><span data-ttu-id="50c7f-214">Containers</span><span class="sxs-lookup"><span data-stu-id="50c7f-214">Containers</span></span>
* [<span data-ttu-id="50c7f-215">Container Service</span><span class="sxs-lookup"><span data-stu-id="50c7f-215">Container Service</span></span>](../articles/container-service/dcos-swarm/container-service-intro.md)
* [<span data-ttu-id="50c7f-216">Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="50c7f-216">Azure Kubernetes Service (AKS)</span></span>](../articles/aks/intro-kubernetes.md)
* [<span data-ttu-id="50c7f-217">Container Registry</span><span class="sxs-lookup"><span data-stu-id="50c7f-217">Container Registry</span></span>](../articles/container-registry/container-registry-intro.md)



## <a name="customer-stories"></a><span data-ttu-id="50c7f-218">Customer stories</span><span class="sxs-lookup"><span data-stu-id="50c7f-218">Customer stories</span></span>

<span data-ttu-id="50c7f-219">Examples of customers that have solved business problems with Azure HPC solutions:</span><span class="sxs-lookup"><span data-stu-id="50c7f-219">Examples of customers that have solved business problems with Azure HPC solutions:</span></span>

* [<span data-ttu-id="50c7f-220">ANEO</span><span class="sxs-lookup"><span data-stu-id="50c7f-220">ANEO</span></span>](https://customers.microsoft.com/story/it-provider-finds-highly-scalable-cloud-based-hpc-redu) 
* [<span data-ttu-id="50c7f-221">AXA Global P&C</span><span class="sxs-lookup"><span data-stu-id="50c7f-221">AXA Global P&C</span></span>](https://customers.microsoft.com/story/axa-global-p-and-c)
* [<span data-ttu-id="50c7f-222">Axioma</span><span class="sxs-lookup"><span data-stu-id="50c7f-222">Axioma</span></span>](https://customers.microsoft.com/story/axioma-delivers-fintechs-first-born-in-the-cloud-multi-asset-class-enterprise-risk-solution)
* [<span data-ttu-id="50c7f-223">d3View</span><span class="sxs-lookup"><span data-stu-id="50c7f-223">d3View</span></span>](https://customers.microsoft.com/story/big-data-solution-provider-adopts-new-cloud-gains-thou)
* [<span data-ttu-id="50c7f-224">EFS</span><span class="sxs-lookup"><span data-stu-id="50c7f-224">EFS</span></span>](https://customers.microsoft.com/story/efs-professionalservices-azure)
* [<span data-ttu-id="50c7f-225">Hymans Robertson</span><span class="sxs-lookup"><span data-stu-id="50c7f-225">Hymans Robertson</span></span>](https://customers.microsoft.com/story/hymans-robertson)
* [<span data-ttu-id="50c7f-226">MetLife</span><span class="sxs-lookup"><span data-stu-id="50c7f-226">MetLife</span></span>](https://enterprise.microsoft.com/en-us/customer-story/industries/insurance/metlife/)
* [<span data-ttu-id="50c7f-227">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="50c7f-227">Microsoft Research</span></span>](https://customers.microsoft.com/doclink/fast-lmm-and-windows-azure-put-genetics-research-on-fa)
* [<span data-ttu-id="50c7f-228">Milliman</span><span class="sxs-lookup"><span data-stu-id="50c7f-228">Milliman</span></span>](https://customers.microsoft.com/story/actuarial-firm-works-to-transform-insurance-industry-w)
* [<span data-ttu-id="50c7f-229">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="50c7f-229">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/story/powering-risk-compute-grids-in-the-cloud)
* [<span data-ttu-id="50c7f-230">NeuroInitiative</span><span class="sxs-lookup"><span data-stu-id="50c7f-230">NeuroInitiative</span></span>](https://customers.microsoft.com/en-us/story/neuroinitiative-health-provider-azure)
* [<span data-ttu-id="50c7f-231">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="50c7f-231">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="50c7f-232">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="50c7f-232">Towers Watson</span></span>](https://customers.microsoft.com/story/insurance-tech-provider-delivers-disruptive-solutions)


## <a name="next-steps"></a><span data-ttu-id="50c7f-233">Next steps</span><span class="sxs-lookup"><span data-stu-id="50c7f-233">Next steps</span></span>
* <span data-ttu-id="50c7f-234">Learn more about Big Compute solutions for [engineering simulation](https://simulation.azure.com/), [rendering](https://azure.microsoft.com/solutions/big-compute/rendering/), [banking and capital markets](https://finance.azure.com/), and [genomics](https://enterprise.microsoft.com/en-us/industries/health/genomics/).</span><span class="sxs-lookup"><span data-stu-id="50c7f-234">Learn more about Big Compute solutions for [engineering simulation](https://simulation.azure.com/), [rendering](https://azure.microsoft.com/solutions/big-compute/rendering/), [banking and capital markets](https://finance.azure.com/), and [genomics](https://enterprise.microsoft.com/en-us/industries/health/genomics/).</span></span>
* <span data-ttu-id="50c7f-235">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="50c7f-235">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>

* <span data-ttu-id="50c7f-236">Use the managed and scalable Azure [Batch](https://azure.microsoft.com/services/batch/) service to run compute-intensive workloads, without managing underlying infrastructure [Learn more](https://azure.microsoft.com/solutions/architecture/hpc-big-compute-saas/)</span><span class="sxs-lookup"><span data-stu-id="50c7f-236">Use the managed and scalable Azure [Batch](https://azure.microsoft.com/services/batch/) service to run compute-intensive workloads, without managing underlying infrastructure [Learn more](https://azure.microsoft.com/solutions/architecture/hpc-big-compute-saas/)</span></span>



