---
title: Resources for batch and HPC in the Azure cloud | Microsoft Docs
description: Lists technical resources to help you run your large-scale parallel, batch, and high performance computing (HPC) workloads in Azure.
services: batch, cloud-services, virtual-machines
documentationcenter: ''
author: dlepow
manager: timlt
editor: ''
ms.assetid: 6f8be911-c841-41ae-88d3-3bcfc029eb7f
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: big-compute
ms.date: 03/17/2017
ms.author: danlep
ms.openlocfilehash: aff11fe3d7e4cea3580f73d54a53d9624e4f3ac9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555046"
---
# <a name="big-compute-in-azure-technical-resources-for-batch-and-high-performance-computing"></a><span data-ttu-id="04ef5-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span><span class="sxs-lookup"><span data-stu-id="04ef5-103">Big Compute in Azure: Technical resources for batch and high-performance computing</span></span>
<span data-ttu-id="04ef5-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span><span class="sxs-lookup"><span data-stu-id="04ef5-104">This is a guide to technical resources to help you run your large-scale parallel, batch, and high-performance computing (HPC) workloads in Azure.</span></span> <span data-ttu-id="04ef5-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span><span class="sxs-lookup"><span data-stu-id="04ef5-105">Extend your existing batch or HPC workloads to the Azure cloud, or build new Big Compute solutions using a range of Azure services.</span></span>

## <a name="solutions-options"></a><span data-ttu-id="04ef5-106">Solutions options</span><span class="sxs-lookup"><span data-stu-id="04ef5-106">Solutions options</span></span>
<span data-ttu-id="04ef5-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span><span class="sxs-lookup"><span data-stu-id="04ef5-107">Learn about Big Compute options in Azure, and choose the right approach for your workload and business need.</span></span>

* [<span data-ttu-id="04ef5-108">Batch and HPC solutions</span><span class="sxs-lookup"><span data-stu-id="04ef5-108">Batch and HPC solutions</span></span>](batch-hpc-solutions.md)
* [<span data-ttu-id="04ef5-109">Video: Big Compute in the cloud with Azure and HPC</span><span class="sxs-lookup"><span data-stu-id="04ef5-109">Video: Big Compute in the cloud with Azure and HPC</span></span>](https://azure.microsoft.com/documentation/videos/teched-europe-2014-big-compute-in-the-cloud-with-high-performance-computing-on-azure/)

## <a name="azure-batch"></a><span data-ttu-id="04ef5-110">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="04ef5-110">Azure Batch</span></span>
<span data-ttu-id="04ef5-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span><span class="sxs-lookup"><span data-stu-id="04ef5-111">[Batch](https://azure.microsoft.com/services/batch/) is a platform service that makes it easy to cloud-enable your Linux and Windows applications and run jobs without setting up and managing a cluster and job scheduler.</span></span> <span data-ttu-id="04ef5-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span><span class="sxs-lookup"><span data-stu-id="04ef5-112">Use the SDK to integrate client applications with Azure Batch through various languages, stage data to Azure, and build job execution pipelines.</span></span>

* [<span data-ttu-id="04ef5-113">Documentation</span><span class="sxs-lookup"><span data-stu-id="04ef5-113">Documentation</span></span>](https://azure.microsoft.com/documentation/services/batch/)
* <span data-ttu-id="04ef5-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span><span class="sxs-lookup"><span data-stu-id="04ef5-114">[.NET](https://msdn.microsoft.com/library/azure/mt348682.aspx), [Python](http://azure-sdk-for-python.readthedocs.io/latest/), [Node.js](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/), [Java](http://azure.github.io/azure-sdk-for-java/), and [REST](https://msdn.microsoft.com/library/azure/dn820158.aspx) API reference</span></span>
* <span data-ttu-id="04ef5-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span><span class="sxs-lookup"><span data-stu-id="04ef5-115">[Batch management .NET library](https://msdn.microsoft.com/library/mt463120.aspx) reference</span></span>
* <span data-ttu-id="04ef5-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="04ef5-116">Tutorials: Get started with [Azure Batch library for .NET](batch-dotnet-get-started.md) and [Batch Python client](batch-python-tutorial.md)</span></span>
* [<span data-ttu-id="04ef5-117">Batch forum</span><span class="sxs-lookup"><span data-stu-id="04ef5-117">Batch forum</span></span>](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch)
* [<span data-ttu-id="04ef5-118">Batch videos</span><span class="sxs-lookup"><span data-stu-id="04ef5-118">Batch videos</span></span>](https://azure.microsoft.com/documentation/videos/index/?services=batch)

## <a name="hpc-cluster-solutions"></a><span data-ttu-id="04ef5-119">HPC cluster solutions</span><span class="sxs-lookup"><span data-stu-id="04ef5-119">HPC cluster solutions</span></span>
<span data-ttu-id="04ef5-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span><span class="sxs-lookup"><span data-stu-id="04ef5-120">Deploy or extend your existing Windows or Linux HPC cluster to Azure to run your compute intensive workloads.</span></span>  

### <a name="microsoft-hpc-pack"></a><span data-ttu-id="04ef5-121">Microsoft HPC Pack</span><span class="sxs-lookup"><span data-stu-id="04ef5-121">Microsoft HPC Pack</span></span>
<span data-ttu-id="04ef5-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span><span class="sxs-lookup"><span data-stu-id="04ef5-122">HPC Pack is Microsoft's free HPC solution built on Microsoft Azure and Windows Server technologies, capable of running Windows and Linux HPC workloads.</span></span>  

* [<span data-ttu-id="04ef5-123">Download HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="04ef5-123">Download HPC Pack 2016</span></span>](https://www.microsoft.com/download/details.aspx?id=54507)
* [<span data-ttu-id="04ef5-124">Download HPC Pack 2012 R2 Update 3</span><span class="sxs-lookup"><span data-stu-id="04ef5-124">Download HPC Pack 2012 R2 Update 3</span></span>](https://www.microsoft.com/download/details.aspx?id=49922)
* [<span data-ttu-id="04ef5-125">Documentation</span><span class="sxs-lookup"><span data-stu-id="04ef5-125">Documentation</span></span>](https://technet.microsoft.com/library/jj899572.aspx)
* <span data-ttu-id="04ef5-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="04ef5-126">HPC Pack cluster options in Azure: [Linux](../virtual-machines/linux/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) and [Windows](../virtual-machines/windows/hpcpack-cluster-options.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)</span></span> 
* [<span data-ttu-id="04ef5-127">Burst to Azure worker instances with HPC Pack</span><span class="sxs-lookup"><span data-stu-id="04ef5-127">Burst to Azure worker instances with HPC Pack</span></span>](https://technet.microsoft.com/library/gg481749.aspx)
* [<span data-ttu-id="04ef5-128">Burst to Azure  Batch with HPC Pack</span><span class="sxs-lookup"><span data-stu-id="04ef5-128">Burst to Azure  Batch with HPC Pack</span></span>](https://technet.microsoft.com/library/mt612877.aspx)
* [<span data-ttu-id="04ef5-129">Windows HPC forums</span><span class="sxs-lookup"><span data-stu-id="04ef5-129">Windows HPC forums</span></span>](https://social.microsoft.com/Forums/home?category=windowshpc)

### <a name="linux-and-oss-cluster-solutions"></a><span data-ttu-id="04ef5-130">Linux and OSS cluster solutions</span><span class="sxs-lookup"><span data-stu-id="04ef5-130">Linux and OSS cluster solutions</span></span>
<span data-ttu-id="04ef5-131">Use these Azure templates to deploy Linux HPC clusters.</span><span class="sxs-lookup"><span data-stu-id="04ef5-131">Use these Azure templates to deploy Linux HPC clusters.</span></span>

* <span data-ttu-id="04ef5-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span><span class="sxs-lookup"><span data-stu-id="04ef5-132">[Spin up a SLURM cluster](https://azure.microsoft.com/documentation/templates/slurm/) and [blog post](http://blogs.technet.com/b/windowshpc/archive/2015/06/06/deploy-a-slurm-cluster-on-azure.aspx)</span></span>
* [<span data-ttu-id="04ef5-133">Spin up a Torque cluster</span><span class="sxs-lookup"><span data-stu-id="04ef5-133">Spin up a Torque cluster</span></span>](https://azure.microsoft.com/documentation/templates/torque-cluster/)
* [<span data-ttu-id="04ef5-134">Compute grid templates with PBS Professional</span><span class="sxs-lookup"><span data-stu-id="04ef5-134">Compute grid templates with PBS Professional</span></span>](https://github.com/xpillons/azure-hpc/tree/master/Compute-Grid-Infra)

## <a name="hpc-storage"></a><span data-ttu-id="04ef5-135">HPC storage</span><span class="sxs-lookup"><span data-stu-id="04ef5-135">HPC storage</span></span>
* [<span data-ttu-id="04ef5-136">Parallel file systems for HPC storage on Azure</span><span class="sxs-lookup"><span data-stu-id="04ef5-136">Parallel file systems for HPC storage on Azure</span></span>](https://blogs.msdn.microsoft.com/azurecat/2017/03/17/parallel-file-systems-for-hpc-storage-on-azure/)
* [<span data-ttu-id="04ef5-137">Intel Cloud Edition for Lustre Software - Eval</span><span class="sxs-lookup"><span data-stu-id="04ef5-137">Intel Cloud Edition for Lustre Software - Eval</span></span>](https://azure.microsoft.com/marketplace/partners/intel/lustre-cloud-edition-evaleval-lustre-2-7/)
* [<span data-ttu-id="04ef5-138">BeeGFS on CentOS 7.2 template</span><span class="sxs-lookup"><span data-stu-id="04ef5-138">BeeGFS on CentOS 7.2 template</span></span>](https://github.com/smith1511/hpc/tree/master/beegfs-shared-on-centos7.2)




## <a name="microsoft-mpi"></a><span data-ttu-id="04ef5-139">Microsoft MPI</span><span class="sxs-lookup"><span data-stu-id="04ef5-139">Microsoft MPI</span></span>
<span data-ttu-id="04ef5-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span><span class="sxs-lookup"><span data-stu-id="04ef5-140">[Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) (MS-MPI) is a Microsoft implementation of the Message Passing Interface standard for developing and running parallel applications on the Windows platform.</span></span>

* [<span data-ttu-id="04ef5-141">Download MS-MPI</span><span class="sxs-lookup"><span data-stu-id="04ef5-141">Download MS-MPI</span></span>](http://go.microsoft.com/FWLink/p/?LinkID=389556)
* [<span data-ttu-id="04ef5-142">MS-MPI reference</span><span class="sxs-lookup"><span data-stu-id="04ef5-142">MS-MPI reference</span></span>](https://msdn.microsoft.com/library/dn473458.aspx)
* [<span data-ttu-id="04ef5-143">MPI forum</span><span class="sxs-lookup"><span data-stu-id="04ef5-143">MPI forum</span></span>](https://social.microsoft.com/Forums/en-us/home?forum=windowshpcmpi)

## <a name="compute-intensive-instances"></a><span data-ttu-id="04ef5-144">Compute-intensive instances</span><span class="sxs-lookup"><span data-stu-id="04ef5-144">Compute-intensive instances</span></span>
<span data-ttu-id="04ef5-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span><span class="sxs-lookup"><span data-stu-id="04ef5-145">Azure offers a [range of VM sizes](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), including [compute-intensive H-series](../virtual-machines/windows/a8-a9-a10-a11-specs.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) instances capable of connecting to a back-end RDMA network, to run your Linux and Windows HPC workloads.</span></span> 

* [<span data-ttu-id="04ef5-146">Set up a Linux RDMA cluster to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="04ef5-146">Set up a Linux RDMA cluster to run MPI applications</span></span>](../virtual-machines/linux/classic/rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [<span data-ttu-id="04ef5-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span><span class="sxs-lookup"><span data-stu-id="04ef5-147">Set up a Windows RDMA cluster with Microsoft HPC Pack to run MPI applications</span></span>](../virtual-machines/windows/classic/hpcpack-rdma-cluster.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

<span data-ttu-id="04ef5-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span><span class="sxs-lookup"><span data-stu-id="04ef5-148">For GPU-intensive workloads, check out [NC and NV sizes](https://azure.microsoft.com/blog/azure-n-series-general-availability-on-december-1/).</span></span>

## <a name="samples-and-demos"></a><span data-ttu-id="04ef5-149">Samples and demos</span><span class="sxs-lookup"><span data-stu-id="04ef5-149">Samples and demos</span></span>
* [<span data-ttu-id="04ef5-150">Azure Batch C# and Python code samples</span><span class="sxs-lookup"><span data-stu-id="04ef5-150">Azure Batch C# and Python code samples</span></span>](https://github.com/Azure/azure-batch-samples)
* <span data-ttu-id="04ef5-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span><span class="sxs-lookup"><span data-stu-id="04ef5-151">[Batch Shipyard](https://azure.github.io/batch-shipyard/) toolkit for easy deployment of batch-style Dockerized workloads to Azure Batch</span></span>
* <span data-ttu-id="04ef5-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span><span class="sxs-lookup"><span data-stu-id="04ef5-152">[doAzureParallel](http://www.github.com/Azure/doAzureParallel) R package, built on top of Azure Batch</span></span>
* [<span data-ttu-id="04ef5-153">Test drive SUSE Linux Enterprise Server for HPC</span><span class="sxs-lookup"><span data-stu-id="04ef5-153">Test drive SUSE Linux Enterprise Server for HPC</span></span>](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)

## <a name="related-azure-services"></a><span data-ttu-id="04ef5-154">Related Azure services</span><span class="sxs-lookup"><span data-stu-id="04ef5-154">Related Azure services</span></span>
* [<span data-ttu-id="04ef5-155">Data Factory</span><span class="sxs-lookup"><span data-stu-id="04ef5-155">Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)
* [<span data-ttu-id="04ef5-156">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="04ef5-156">Machine Learning</span></span>](https://azure.microsoft.com/documentation/services/machine-learning/)
* [<span data-ttu-id="04ef5-157">HDInsight</span><span class="sxs-lookup"><span data-stu-id="04ef5-157">HDInsight</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="04ef5-158">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="04ef5-158">Virtual Machines</span></span>](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [<span data-ttu-id="04ef5-159">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="04ef5-159">Virtual Machine Scale Sets</span></span>](https://azure.microsoft.com/documentation/services/virtual-machine-scale-sets/)
* [<span data-ttu-id="04ef5-160">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="04ef5-160">Cloud Services</span></span>](https://azure.microsoft.com/documentation/services/cloud-services/)
* [<span data-ttu-id="04ef5-161">App Service</span><span class="sxs-lookup"><span data-stu-id="04ef5-161">App Service</span></span>](https://azure.microsoft.com/documentation/services/app-service/)
* [<span data-ttu-id="04ef5-162">Media Services</span><span class="sxs-lookup"><span data-stu-id="04ef5-162">Media Services</span></span>](https://azure.microsoft.com/documentation/services/media-services/)
* [<span data-ttu-id="04ef5-163">Functions</span><span class="sxs-lookup"><span data-stu-id="04ef5-163">Functions</span></span>](https://azure.microsoft.com/documentation/services/functions/)

## <a name="architecture-blueprints"></a><span data-ttu-id="04ef5-164">Architecture blueprints</span><span class="sxs-lookup"><span data-stu-id="04ef5-164">Architecture blueprints</span></span>
* <span data-ttu-id="04ef5-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span><span class="sxs-lookup"><span data-stu-id="04ef5-165">[HPC and data orchestration using Azure Batch and Azure Data Factory](http://go.microsoft.com/fwlink/?linkid=717686) (PDF) and [article](../data-factory/data-factory-data-processing-using-batch.md)</span></span>

## <a name="industry-solutions"></a><span data-ttu-id="04ef5-166">Industry solutions</span><span class="sxs-lookup"><span data-stu-id="04ef5-166">Industry solutions</span></span>
* [<span data-ttu-id="04ef5-167">Banking and capital markets</span><span class="sxs-lookup"><span data-stu-id="04ef5-167">Banking and capital markets</span></span>](https://finance.azure.com/)
* [<span data-ttu-id="04ef5-168">Engineering simulations</span><span class="sxs-lookup"><span data-stu-id="04ef5-168">Engineering simulations</span></span>](https://simulation.azure.com/) 

## <a name="customer-stories"></a><span data-ttu-id="04ef5-169">Customer stories</span><span class="sxs-lookup"><span data-stu-id="04ef5-169">Customer stories</span></span>
* [<span data-ttu-id="04ef5-170">ANEO</span><span class="sxs-lookup"><span data-stu-id="04ef5-170">ANEO</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=4168) 
* [<span data-ttu-id="04ef5-171">d3View</span><span class="sxs-lookup"><span data-stu-id="04ef5-171">d3View</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=22088)
* [<span data-ttu-id="04ef5-172">Ludwig Institute of Cancer Research</span><span class="sxs-lookup"><span data-stu-id="04ef5-172">Ludwig Institute of Cancer Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=5830)
* [<span data-ttu-id="04ef5-173">Microsoft Research</span><span class="sxs-lookup"><span data-stu-id="04ef5-173">Microsoft Research</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=15634)
* [<span data-ttu-id="04ef5-174">Milliman</span><span class="sxs-lookup"><span data-stu-id="04ef5-174">Milliman</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=14967)
* [<span data-ttu-id="04ef5-175">Mitsubishi UFJ Securities International</span><span class="sxs-lookup"><span data-stu-id="04ef5-175">Mitsubishi UFJ Securities International</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=26266)
* [<span data-ttu-id="04ef5-176">Schlumberger</span><span class="sxs-lookup"><span data-stu-id="04ef5-176">Schlumberger</span></span>](http://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [<span data-ttu-id="04ef5-177">Towers Watson</span><span class="sxs-lookup"><span data-stu-id="04ef5-177">Towers Watson</span></span>](https://customers.microsoft.com/Pages/CustomerStory.aspx?recid=18222)
* [<span data-ttu-id="04ef5-178">UberCloud</span><span class="sxs-lookup"><span data-stu-id="04ef5-178">UberCloud</span></span>](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

## <a name="next-steps"></a><span data-ttu-id="04ef5-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="04ef5-179">Next steps</span></span>
* <span data-ttu-id="04ef5-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span><span class="sxs-lookup"><span data-stu-id="04ef5-180">For the latest announcements, see the [Microsoft HPC and Batch team blog](http://blogs.technet.com/b/windowshpc/) and the [Azure blog](https://azure.microsoft.com/blog/tag/hpc/).</span></span>
* <span data-ttu-id="04ef5-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span><span class="sxs-lookup"><span data-stu-id="04ef5-181">Also see [what's new in Batch](https://azure.microsoft.com/updates/?service=batch) or subscribe to the [RSS feed](https://azure.microsoft.com/updates/feed/?service=batch).</span></span>

