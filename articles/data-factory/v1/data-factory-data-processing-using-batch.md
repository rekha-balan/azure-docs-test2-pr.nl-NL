---
title: Process large-scale datasets by using Data Factory and Batch | Microsoft Docs
description: Describes how to process huge amounts of data in an Azure Data Factory pipeline by using the parallel processing capability of Azure Batch.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: 6ad3b4c1f59f5c46fd31aa24d6d2ceb4d7411abd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864915"
---
# <a name="process-large-scale-datasets-by-using-data-factory-and-batch"></a><span data-ttu-id="711c0-103">Process large-scale datasets by using Data Factory and Batch</span><span class="sxs-lookup"><span data-stu-id="711c0-103">Process large-scale datasets by using Data Factory and Batch</span></span>
> [!NOTE]
> <span data-ttu-id="711c0-104">This article applies to version 1 of Azure Data Factory, which is generally available.</span><span class="sxs-lookup"><span data-stu-id="711c0-104">This article applies to version 1 of Azure Data Factory, which is generally available.</span></span> <span data-ttu-id="711c0-105">If you use the current version of the Data Factory service, see [Custom activities in Data Factory](../transform-data-using-dotnet-custom-activity.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-105">If you use the current version of the Data Factory service, see [Custom activities in Data Factory](../transform-data-using-dotnet-custom-activity.md).</span></span>

<span data-ttu-id="711c0-106">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span><span class="sxs-lookup"><span data-stu-id="711c0-106">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="711c0-107">It also provides an end-to-end walkthrough to implement the solution by using Data Factory and Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-107">It also provides an end-to-end walkthrough to implement the solution by using Data Factory and Azure Batch.</span></span>

<span data-ttu-id="711c0-108">This article is longer than a typical article because it contains a walkthrough of an entire sample solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-108">This article is longer than a typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="711c0-109">If you're new to Batch and Data Factory, you can learn about these services and how they work together.</span><span class="sxs-lookup"><span data-stu-id="711c0-109">If you're new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="711c0-110">If you know something about the services and are designing/architecting a solution, you can focus on the [architecture section](#architecture-of-sample-solution) of the article.</span><span class="sxs-lookup"><span data-stu-id="711c0-110">If you know something about the services and are designing/architecting a solution, you can focus on the [architecture section](#architecture-of-sample-solution) of the article.</span></span> <span data-ttu-id="711c0-111">If you're developing a prototype or a solution, you might want to try out the step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="711c0-111">If you're developing a prototype or a solution, you might want to try out the step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="711c0-112">We invite your comments about this content and how you use it.</span><span class="sxs-lookup"><span data-stu-id="711c0-112">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="711c0-113">First, let's look at how Data Factory and Batch services can help you process large datasets in the cloud.</span><span class="sxs-lookup"><span data-stu-id="711c0-113">First, let's look at how Data Factory and Batch services can help you process large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="711c0-114">Why Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="711c0-114">Why Azure Batch?</span></span>
 <span data-ttu-id="711c0-115">You can use Batch to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span><span class="sxs-lookup"><span data-stu-id="711c0-115">You can use Batch to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="711c0-116">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines (VMs).</span><span class="sxs-lookup"><span data-stu-id="711c0-116">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines (VMs).</span></span> <span data-ttu-id="711c0-117">It can automatically scale compute resources to meet the needs of your jobs.</span><span class="sxs-lookup"><span data-stu-id="711c0-117">It can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="711c0-118">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span><span class="sxs-lookup"><span data-stu-id="711c0-118">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="711c0-119">You can run on-demand or scheduled jobs.</span><span class="sxs-lookup"><span data-stu-id="711c0-119">You can run on-demand or scheduled jobs.</span></span> <span data-ttu-id="711c0-120">You don't need to manually create, configure, and manage an HPC cluster, individual VMs, virtual networks, or a complex job and task-scheduling infrastructure.</span><span class="sxs-lookup"><span data-stu-id="711c0-120">You don't need to manually create, configure, and manage an HPC cluster, individual VMs, virtual networks, or a complex job and task-scheduling infrastructure.</span></span>

 <span data-ttu-id="711c0-121">If you aren't familiar with Batch, the following articles help you understand the architecture/implementation of the solution described in this article:</span><span class="sxs-lookup"><span data-stu-id="711c0-121">If you aren't familiar with Batch, the following articles help you understand the architecture/implementation of the solution described in this article:</span></span>   

* [<span data-ttu-id="711c0-122">Basics of Batch</span><span class="sxs-lookup"><span data-stu-id="711c0-122">Basics of Batch</span></span>](../../batch/batch-technical-overview.md)
* [<span data-ttu-id="711c0-123">Batch feature overview</span><span class="sxs-lookup"><span data-stu-id="711c0-123">Batch feature overview</span></span>](../../batch/batch-api-basics.md)

<span data-ttu-id="711c0-124">Optionally, to learn more about Batch, see [Learning path for Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="711c0-124">Optionally, to learn more about Batch, see [Learning path for Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="711c0-125">Why Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="711c0-125">Why Azure Data Factory?</span></span>
<span data-ttu-id="711c0-126">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span><span class="sxs-lookup"><span data-stu-id="711c0-126">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="711c0-127">You can use Data Factory to create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store.</span><span class="sxs-lookup"><span data-stu-id="711c0-127">You can use Data Factory to create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store.</span></span> <span data-ttu-id="711c0-128">An example is Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-128">An example is Azure Blob storage.</span></span> <span data-ttu-id="711c0-129">You can use Data Factory to process/transform data by using services such as Azure HDInsight and Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="711c0-129">You can use Data Factory to process/transform data by using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="711c0-130">You also can schedule data pipelines to run in a scheduled manner (for example, hourly, daily, and weekly).</span><span class="sxs-lookup"><span data-stu-id="711c0-130">You also can schedule data pipelines to run in a scheduled manner (for example, hourly, daily, and weekly).</span></span> <span data-ttu-id="711c0-131">You can monitor and manage the pipelines at a glance to identify issues and take action.</span><span class="sxs-lookup"><span data-stu-id="711c0-131">You can monitor and manage the pipelines at a glance to identify issues and take action.</span></span>

  <span data-ttu-id="711c0-132">If you aren't familiar with Data Factory, the following articles help you understand the architecture/implementation of the solution described in this article:</span><span class="sxs-lookup"><span data-stu-id="711c0-132">If you aren't familiar with Data Factory, the following articles help you understand the architecture/implementation of the solution described in this article:</span></span>  

* [<span data-ttu-id="711c0-133">Introduction to Data Factory</span><span class="sxs-lookup"><span data-stu-id="711c0-133">Introduction to Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="711c0-134">Build your first data pipeline</span><span class="sxs-lookup"><span data-stu-id="711c0-134">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="711c0-135">Optionally, to learn more about Data Factory, see [Learning path for Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="711c0-135">Optionally, to learn more about Data Factory, see [Learning path for Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="711c0-136">Data Factory and Batch together</span><span class="sxs-lookup"><span data-stu-id="711c0-136">Data Factory and Batch together</span></span>
<span data-ttu-id="711c0-137">Data Factory includes built-in activities.</span><span class="sxs-lookup"><span data-stu-id="711c0-137">Data Factory includes built-in activities.</span></span> <span data-ttu-id="711c0-138">For example, the Copy activity is used to copy/move data from a source data store to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="711c0-138">For example, the Copy activity is used to copy/move data from a source data store to a destination data store.</span></span> <span data-ttu-id="711c0-139">The Hive activity is used to process data by using Hadoop clusters (HDInsight) on Azure.</span><span class="sxs-lookup"><span data-stu-id="711c0-139">The Hive activity is used to process data by using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="711c0-140">For a list of supported transformation activities, see [Data transformation activities](data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-140">For a list of supported transformation activities, see [Data transformation activities](data-factory-data-transformation-activities.md).</span></span>

<span data-ttu-id="711c0-141">You also can create custom .NET activities to move or process data with your own logic.</span><span class="sxs-lookup"><span data-stu-id="711c0-141">You also can create custom .NET activities to move or process data with your own logic.</span></span> <span data-ttu-id="711c0-142">You can run these activities on an HDInsight cluster or on a Batch pool of VMs.</span><span class="sxs-lookup"><span data-stu-id="711c0-142">You can run these activities on an HDInsight cluster or on a Batch pool of VMs.</span></span> <span data-ttu-id="711c0-143">When you use Batch, you can configure the pool to autoscale (add or remove VMs based on the workload) based on a formula you provide.</span><span class="sxs-lookup"><span data-stu-id="711c0-143">When you use Batch, you can configure the pool to autoscale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-a-sample-solution"></a><span data-ttu-id="711c0-144">Architecture of a sample solution</span><span class="sxs-lookup"><span data-stu-id="711c0-144">Architecture of a sample solution</span></span>
  <span data-ttu-id="711c0-145">The architecture described in this article is for a simple solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-145">The architecture described in this article is for a simple solution.</span></span> <span data-ttu-id="711c0-146">It's also relevant to complex scenarios, such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span><span class="sxs-lookup"><span data-stu-id="711c0-146">It's also relevant to complex scenarios, such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="711c0-147">The diagram illustrates how Data Factory orchestrates data movement and processing.</span><span class="sxs-lookup"><span data-stu-id="711c0-147">The diagram illustrates how Data Factory orchestrates data movement and processing.</span></span> <span data-ttu-id="711c0-148">It also shows how Batch processes the data in a parallel manner.</span><span class="sxs-lookup"><span data-stu-id="711c0-148">It also shows how Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="711c0-149">Download and print the diagram for easy reference (11 x 17 inches or A3 size).</span><span class="sxs-lookup"><span data-stu-id="711c0-149">Download and print the diagram for easy reference (11 x 17 inches or A3 size).</span></span> <span data-ttu-id="711c0-150">To access the diagram so that you can print it, see [HPC and data orchestration by using Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="711c0-150">To access the diagram so that you can print it, see [HPC and data orchestration by using Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="711c0-151">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="711c0-151">[![Large-scale data processing diagram](./media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="711c0-152">The following list provides the basic steps of the process.</span><span class="sxs-lookup"><span data-stu-id="711c0-152">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="711c0-153">The solution includes code and explanations to build the end-to-end solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-153">The solution includes code and explanations to build the end-to-end solution.</span></span>

* <span data-ttu-id="711c0-154">**Configure Batch with a pool of compute nodes (VMs).**</span><span class="sxs-lookup"><span data-stu-id="711c0-154">**Configure Batch with a pool of compute nodes (VMs).**</span></span> <span data-ttu-id="711c0-155">You can specify the number of nodes and the size of each node.</span><span class="sxs-lookup"><span data-stu-id="711c0-155">You can specify the number of nodes and the size of each node.</span></span>

* <span data-ttu-id="711c0-156">**Create a Data Factory instance** that is configured with entities that represent blob storage, the Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span><span class="sxs-lookup"><span data-stu-id="711c0-156">**Create a Data Factory instance** that is configured with entities that represent blob storage, the Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>

* <span data-ttu-id="711c0-157">**Create a custom .NET activity in the Data Factory pipeline.**</span><span class="sxs-lookup"><span data-stu-id="711c0-157">**Create a custom .NET activity in the Data Factory pipeline.**</span></span> <span data-ttu-id="711c0-158">The activity is your user code that runs on the Batch pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-158">The activity is your user code that runs on the Batch pool.</span></span>

* <span data-ttu-id="711c0-159">**Store large amounts of input data as blobs in Azure Storage.**</span><span class="sxs-lookup"><span data-stu-id="711c0-159">**Store large amounts of input data as blobs in Azure Storage.**</span></span> <span data-ttu-id="711c0-160">Data is divided into logical slices (usually by time).</span><span class="sxs-lookup"><span data-stu-id="711c0-160">Data is divided into logical slices (usually by time).</span></span>

* <span data-ttu-id="711c0-161">**Data Factory copies data that is processed in parallel** to the secondary location.</span><span class="sxs-lookup"><span data-stu-id="711c0-161">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>

* <span data-ttu-id="711c0-162">**Data Factory runs the custom activity by using the pool allocated by Batch.**</span><span class="sxs-lookup"><span data-stu-id="711c0-162">**Data Factory runs the custom activity by using the pool allocated by Batch.**</span></span> <span data-ttu-id="711c0-163">Data Factory can run activities concurrently.</span><span class="sxs-lookup"><span data-stu-id="711c0-163">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="711c0-164">Each activity processes a slice of data.</span><span class="sxs-lookup"><span data-stu-id="711c0-164">Each activity processes a slice of data.</span></span> <span data-ttu-id="711c0-165">The results are stored in storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-165">The results are stored in storage.</span></span>

* <span data-ttu-id="711c0-166">**Data Factory moves the final results to a third location,** either for distribution via an app or for further processing by other tools.</span><span class="sxs-lookup"><span data-stu-id="711c0-166">**Data Factory moves the final results to a third location,** either for distribution via an app or for further processing by other tools.</span></span>

## <a name="implementation-of-the-sample-solution"></a><span data-ttu-id="711c0-167">Implementation of the sample solution</span><span class="sxs-lookup"><span data-stu-id="711c0-167">Implementation of the sample solution</span></span>
<span data-ttu-id="711c0-168">The sample solution is intentionally simple.</span><span class="sxs-lookup"><span data-stu-id="711c0-168">The sample solution is intentionally simple.</span></span> <span data-ttu-id="711c0-169">It's designed to show you how to use Data Factory and Batch together to process datasets.</span><span class="sxs-lookup"><span data-stu-id="711c0-169">It's designed to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="711c0-170">The solution counts the number of occurrences of the search term "Microsoft" in input files that are organized in a time series.</span><span class="sxs-lookup"><span data-stu-id="711c0-170">The solution counts the number of occurrences of the search term "Microsoft" in input files that are organized in a time series.</span></span> <span data-ttu-id="711c0-171">It then outputs the count to output files.</span><span class="sxs-lookup"><span data-stu-id="711c0-171">It then outputs the count to output files.</span></span>

<span data-ttu-id="711c0-172">**Time:** If you're familiar with the basics of Azure, Data Factory, and Batch and have completed the following prerequisites, this solution takes one to two hours to complete.</span><span class="sxs-lookup"><span data-stu-id="711c0-172">**Time:** If you're familiar with the basics of Azure, Data Factory, and Batch and have completed the following prerequisites, this solution takes one to two hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="711c0-173">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="711c0-173">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="711c0-174">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="711c0-174">Azure subscription</span></span>
<span data-ttu-id="711c0-175">If you don't have an Azure subscription, you can create a free trial account quickly.</span><span class="sxs-lookup"><span data-stu-id="711c0-175">If you don't have an Azure subscription, you can create a free trial account quickly.</span></span> <span data-ttu-id="711c0-176">For more information, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="711c0-176">For more information, see [Free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="711c0-177">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="711c0-177">Azure storage account</span></span>
<span data-ttu-id="711c0-178">You use a storage account to store the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="711c0-178">You use a storage account to store the data in this tutorial.</span></span> <span data-ttu-id="711c0-179">If you don't have a storage account, see [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-179">If you don't have a storage account, see [Create a storage account](../../storage/common/storage-quickstart-create-account.md).</span></span> <span data-ttu-id="711c0-180">The sample solution uses blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-180">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="711c0-181">Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="711c0-181">Azure Batch account</span></span>
<span data-ttu-id="711c0-182">Create a Batch account by using the [Azure portal](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="711c0-182">Create a Batch account by using the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="711c0-183">For more information, see [Create and manage a Batch account](../../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-183">For more information, see [Create and manage a Batch account](../../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="711c0-184">Note the Batch account name and account key.</span><span class="sxs-lookup"><span data-stu-id="711c0-184">Note the Batch account name and account key.</span></span> <span data-ttu-id="711c0-185">You also can use the [New-AzureRmBatchAccount](https://docs.microsoft.com/powershell/module/azurerm.batch/new-azurermbatchaccount) cmdlet to create a Batch account.</span><span class="sxs-lookup"><span data-stu-id="711c0-185">You also can use the [New-AzureRmBatchAccount](https://docs.microsoft.com/powershell/module/azurerm.batch/new-azurermbatchaccount) cmdlet to create a Batch account.</span></span> <span data-ttu-id="711c0-186">For instructions on how to use this cmdlet, see [Get started with Batch PowerShell cmdlets](../../batch/batch-powershell-cmdlets-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-186">For instructions on how to use this cmdlet, see [Get started with Batch PowerShell cmdlets](../../batch/batch-powershell-cmdlets-get-started.md).</span></span>

<span data-ttu-id="711c0-187">The sample solution uses Batch (indirectly via a data factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of VMs).</span><span class="sxs-lookup"><span data-stu-id="711c0-187">The sample solution uses Batch (indirectly via a data factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of VMs).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines"></a><span data-ttu-id="711c0-188">Azure Batch pool of virtual machines</span><span class="sxs-lookup"><span data-stu-id="711c0-188">Azure Batch pool of virtual machines</span></span>
<span data-ttu-id="711c0-189">Create a Batch pool with at least two compute nodes.</span><span class="sxs-lookup"><span data-stu-id="711c0-189">Create a Batch pool with at least two compute nodes.</span></span>

1. <span data-ttu-id="711c0-190">In the [Azure portal](https://portal.azure.com), select **Browse** in the left menu, and select **Batch Accounts**.</span><span class="sxs-lookup"><span data-stu-id="711c0-190">In the [Azure portal](https://portal.azure.com), select **Browse** in the left menu, and select **Batch Accounts**.</span></span>

1. <span data-ttu-id="711c0-191">Select your Batch account to open the **Batch Account** blade.</span><span class="sxs-lookup"><span data-stu-id="711c0-191">Select your Batch account to open the **Batch Account** blade.</span></span>

1. <span data-ttu-id="711c0-192">Select the **Pools** tile.</span><span class="sxs-lookup"><span data-stu-id="711c0-192">Select the **Pools** tile.</span></span>

1. <span data-ttu-id="711c0-193">On the **Pools** blade, select the **Add** button on the toolbar to add a pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-193">On the **Pools** blade, select the **Add** button on the toolbar to add a pool.</span></span>

   <span data-ttu-id="711c0-194">a.</span><span class="sxs-lookup"><span data-stu-id="711c0-194">a.</span></span> <span data-ttu-id="711c0-195">Enter an ID for the pool (**Pool ID**).</span><span class="sxs-lookup"><span data-stu-id="711c0-195">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="711c0-196">Note the ID of the pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-196">Note the ID of the pool.</span></span> <span data-ttu-id="711c0-197">You need it when you create the data factory solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-197">You need it when you create the data factory solution.</span></span>

   <span data-ttu-id="711c0-198">b.</span><span class="sxs-lookup"><span data-stu-id="711c0-198">b.</span></span> <span data-ttu-id="711c0-199">Specify **Windows Server 2012 R2** for the **Operating System Family** setting.</span><span class="sxs-lookup"><span data-stu-id="711c0-199">Specify **Windows Server 2012 R2** for the **Operating System Family** setting.</span></span>

   <span data-ttu-id="711c0-200">c.</span><span class="sxs-lookup"><span data-stu-id="711c0-200">c.</span></span> <span data-ttu-id="711c0-201">Select a **node pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="711c0-201">Select a **node pricing tier**.</span></span>

   <span data-ttu-id="711c0-202">d.</span><span class="sxs-lookup"><span data-stu-id="711c0-202">d.</span></span> <span data-ttu-id="711c0-203">Enter **2** as the value for the **Target Dedicated** setting.</span><span class="sxs-lookup"><span data-stu-id="711c0-203">Enter **2** as the value for the **Target Dedicated** setting.</span></span>

   <span data-ttu-id="711c0-204">e.</span><span class="sxs-lookup"><span data-stu-id="711c0-204">e.</span></span> <span data-ttu-id="711c0-205">Enter **2** as the value for the **Max tasks per node** setting.</span><span class="sxs-lookup"><span data-stu-id="711c0-205">Enter **2** as the value for the **Max tasks per node** setting.</span></span>

   <span data-ttu-id="711c0-206">f.</span><span class="sxs-lookup"><span data-stu-id="711c0-206">f.</span></span> <span data-ttu-id="711c0-207">Select **OK** to create the pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-207">Select **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="711c0-208">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="711c0-208">Azure Storage Explorer</span></span>
<span data-ttu-id="711c0-209">You use [Azure Storage Explorer 6](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software) to inspect and alter the data in your Storage projects.</span><span class="sxs-lookup"><span data-stu-id="711c0-209">You use [Azure Storage Explorer 6](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software) to inspect and alter the data in your Storage projects.</span></span> <span data-ttu-id="711c0-210">You also can inspect and alter the data in the logs of your cloud-hosted applications.</span><span class="sxs-lookup"><span data-stu-id="711c0-210">You also can inspect and alter the data in the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="711c0-211">Create a container named **mycontainer** with private access (no anonymous access).</span><span class="sxs-lookup"><span data-stu-id="711c0-211">Create a container named **mycontainer** with private access (no anonymous access).</span></span>

1. <span data-ttu-id="711c0-212">If you use CloudXplorer, create folders and subfolders with the following structure:</span><span class="sxs-lookup"><span data-stu-id="711c0-212">If you use CloudXplorer, create folders and subfolders with the following structure:</span></span>

   ![Folder and subfolder structure](./media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="711c0-214">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span><span class="sxs-lookup"><span data-stu-id="711c0-214">`Inputfolder` and `outputfolder` are top-level folders in `mycontainer`.</span></span> <span data-ttu-id="711c0-215">The `inputfolder` folder has subfolders with date-time stamps (YYYY-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="711c0-215">The `inputfolder` folder has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="711c0-216">If you use Storage Explorer, in the next step, you upload files with the following names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt`, and so on.</span><span class="sxs-lookup"><span data-stu-id="711c0-216">If you use Storage Explorer, in the next step, you upload files with the following names: `inputfolder/2015-11-16-00/file.txt`, `inputfolder/2015-11-16-01/file.txt`, and so on.</span></span> <span data-ttu-id="711c0-217">This step automatically creates the folders.</span><span class="sxs-lookup"><span data-stu-id="711c0-217">This step automatically creates the folders.</span></span>

1. <span data-ttu-id="711c0-218">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="711c0-218">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="711c0-219">An example is "test custom activity Microsoft test custom activity Microsoft."</span><span class="sxs-lookup"><span data-stu-id="711c0-219">An example is "test custom activity Microsoft test custom activity Microsoft."</span></span>

1. <span data-ttu-id="711c0-220">Upload the file to the following input folders in blob storage:</span><span class="sxs-lookup"><span data-stu-id="711c0-220">Upload the file to the following input folders in blob storage:</span></span>

   ![Input folders](./media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="711c0-222">If you use Storage Explorer, upload the **file.txt** file to **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="711c0-222">If you use Storage Explorer, upload the **file.txt** file to **mycontainer**.</span></span> <span data-ttu-id="711c0-223">Select **Copy** on the toolbar to create a copy of the blob.</span><span class="sxs-lookup"><span data-stu-id="711c0-223">Select **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="711c0-224">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span><span class="sxs-lookup"><span data-stu-id="711c0-224">In the **Copy Blob** dialog box, change the **destination blob name** to `inputfolder/2015-11-16-00/file.txt`.</span></span> <span data-ttu-id="711c0-225">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt`, and so on.</span><span class="sxs-lookup"><span data-stu-id="711c0-225">Repeat this step to create `inputfolder/2015-11-16-01/file.txt`, `inputfolder/2015-11-16-02/file.txt`, `inputfolder/2015-11-16-03/file.txt`, `inputfolder/2015-11-16-04/file.txt`, and so on.</span></span> <span data-ttu-id="711c0-226">This action automatically creates the folders.</span><span class="sxs-lookup"><span data-stu-id="711c0-226">This action automatically creates the folders.</span></span>

1. <span data-ttu-id="711c0-227">Create another container named `customactivitycontainer`.</span><span class="sxs-lookup"><span data-stu-id="711c0-227">Create another container named `customactivitycontainer`.</span></span> <span data-ttu-id="711c0-228">Upload the custom activity zip file to this container.</span><span class="sxs-lookup"><span data-stu-id="711c0-228">Upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="711c0-229">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="711c0-229">Visual Studio</span></span>
<span data-ttu-id="711c0-230">Install Visual Studio 2012 or later to create the custom Batch activity to be used in the data factory solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-230">Install Visual Studio 2012 or later to create the custom Batch activity to be used in the data factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="711c0-231">High-level steps to create the solution</span><span class="sxs-lookup"><span data-stu-id="711c0-231">High-level steps to create the solution</span></span>
1. <span data-ttu-id="711c0-232">Create a custom activity that contains the data processing logic.</span><span class="sxs-lookup"><span data-stu-id="711c0-232">Create a custom activity that contains the data processing logic.</span></span>

1. <span data-ttu-id="711c0-233">Create a data factory that uses the custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-233">Create a data factory that uses the custom activity.</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="711c0-234">Create the custom activity</span><span class="sxs-lookup"><span data-stu-id="711c0-234">Create the custom activity</span></span>
<span data-ttu-id="711c0-235">The data factory custom activity is the heart of this sample solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-235">The data factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="711c0-236">The sample solution uses Batch to run the custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-236">The sample solution uses Batch to run the custom activity.</span></span> <span data-ttu-id="711c0-237">For information about how to develop custom activities and use them in data factory pipelines, see [Use custom activities in a data factory pipeline](data-factory-use-custom-activities.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-237">For information about how to develop custom activities and use them in data factory pipelines, see [Use custom activities in a data factory pipeline](data-factory-use-custom-activities.md).</span></span>

<span data-ttu-id="711c0-238">To create a .NET custom activity that you can use in a data factory pipeline, you create a .NET class library project with a class that implements the IDotNetActivity interface.</span><span class="sxs-lookup"><span data-stu-id="711c0-238">To create a .NET custom activity that you can use in a data factory pipeline, you create a .NET class library project with a class that implements the IDotNetActivity interface.</span></span> <span data-ttu-id="711c0-239">This interface has only one method: Execute.</span><span class="sxs-lookup"><span data-stu-id="711c0-239">This interface has only one method: Execute.</span></span> <span data-ttu-id="711c0-240">Here is the signature of the method:</span><span class="sxs-lookup"><span data-stu-id="711c0-240">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="711c0-241">The method has a few key components that you need to understand:</span><span class="sxs-lookup"><span data-stu-id="711c0-241">The method has a few key components that you need to understand:</span></span>

* <span data-ttu-id="711c0-242">The method takes four parameters:</span><span class="sxs-lookup"><span data-stu-id="711c0-242">The method takes four parameters:</span></span>

  * <span data-ttu-id="711c0-243">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="711c0-243">**linkedServices**.</span></span> <span data-ttu-id="711c0-244">This parameter is an enumerable list of linked services that link input/output data sources (for example, blob storage) to the data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-244">This parameter is an enumerable list of linked services that link input/output data sources (for example, blob storage) to the data factory.</span></span> <span data-ttu-id="711c0-245">In this sample, there is only one linked service of the type Azure Storage used for both input and output.</span><span class="sxs-lookup"><span data-stu-id="711c0-245">In this sample, there is only one linked service of the type Azure Storage used for both input and output.</span></span>
  * <span data-ttu-id="711c0-246">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="711c0-246">**datasets**.</span></span> <span data-ttu-id="711c0-247">This parameter is an enumerable list of datasets.</span><span class="sxs-lookup"><span data-stu-id="711c0-247">This parameter is an enumerable list of datasets.</span></span> <span data-ttu-id="711c0-248">You can use this parameter to get the locations and schemas defined by input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="711c0-248">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  * <span data-ttu-id="711c0-249">**activity**.</span><span class="sxs-lookup"><span data-stu-id="711c0-249">**activity**.</span></span> <span data-ttu-id="711c0-250">This parameter represents the current compute entity.</span><span class="sxs-lookup"><span data-stu-id="711c0-250">This parameter represents the current compute entity.</span></span> <span data-ttu-id="711c0-251">In this case, it's a Batch service.</span><span class="sxs-lookup"><span data-stu-id="711c0-251">In this case, it's a Batch service.</span></span>
  * <span data-ttu-id="711c0-252">**logger**.</span><span class="sxs-lookup"><span data-stu-id="711c0-252">**logger**.</span></span> <span data-ttu-id="711c0-253">You can use the logger to write debug comments that surface as the "User" log for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="711c0-253">You can use the logger to write debug comments that surface as the "User" log for the pipeline.</span></span>
* <span data-ttu-id="711c0-254">The method returns a dictionary that can be used to chain custom activities together in the future.</span><span class="sxs-lookup"><span data-stu-id="711c0-254">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="711c0-255">This feature isn't implemented yet, so just return an empty dictionary from the method.</span><span class="sxs-lookup"><span data-stu-id="711c0-255">This feature isn't implemented yet, so just return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="711c0-256">Procedure: Create the custom activity</span><span class="sxs-lookup"><span data-stu-id="711c0-256">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="711c0-257">Create a .NET class library project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="711c0-257">Create a .NET class library project in Visual Studio.</span></span>

   <span data-ttu-id="711c0-258">a.</span><span class="sxs-lookup"><span data-stu-id="711c0-258">a.</span></span> <span data-ttu-id="711c0-259">Start Visual Studio 2012/2013/2015.</span><span class="sxs-lookup"><span data-stu-id="711c0-259">Start Visual Studio 2012/2013/2015.</span></span>

   <span data-ttu-id="711c0-260">b.</span><span class="sxs-lookup"><span data-stu-id="711c0-260">b.</span></span> <span data-ttu-id="711c0-261">Select **File** > **New** > **Project**.</span><span class="sxs-lookup"><span data-stu-id="711c0-261">Select **File** > **New** > **Project**.</span></span>

   <span data-ttu-id="711c0-262">c.</span><span class="sxs-lookup"><span data-stu-id="711c0-262">c.</span></span> <span data-ttu-id="711c0-263">Expand **Templates**, and select **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="711c0-263">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="711c0-264">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-264">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>

   <span data-ttu-id="711c0-265">d.</span><span class="sxs-lookup"><span data-stu-id="711c0-265">d.</span></span> <span data-ttu-id="711c0-266">Select **Class Library** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="711c0-266">Select **Class Library** from the list of project types on the right.</span></span>

   <span data-ttu-id="711c0-267">e.</span><span class="sxs-lookup"><span data-stu-id="711c0-267">e.</span></span> <span data-ttu-id="711c0-268">Enter **MyDotNetActivity** for the **Name**.</span><span class="sxs-lookup"><span data-stu-id="711c0-268">Enter **MyDotNetActivity** for the **Name**.</span></span>

   <span data-ttu-id="711c0-269">f.</span><span class="sxs-lookup"><span data-stu-id="711c0-269">f.</span></span> <span data-ttu-id="711c0-270">Select **C:\\ADF** for the **Location**.</span><span class="sxs-lookup"><span data-stu-id="711c0-270">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="711c0-271">Create the folder **ADF** if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="711c0-271">Create the folder **ADF** if it doesn't exist.</span></span>

   <span data-ttu-id="711c0-272">g.</span><span class="sxs-lookup"><span data-stu-id="711c0-272">g.</span></span> <span data-ttu-id="711c0-273">Select **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="711c0-273">Select **OK** to create the project.</span></span>

1. <span data-ttu-id="711c0-274">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="711c0-274">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

1. <span data-ttu-id="711c0-275">In the Package Manager Console, execute the following command to import Microsoft.Azure.Management.DataFactories:</span><span class="sxs-lookup"><span data-stu-id="711c0-275">In the Package Manager Console, execute the following command to import Microsoft.Azure.Management.DataFactories:</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
1. <span data-ttu-id="711c0-276">Import the **Azure Storage** NuGet package into the project.</span><span class="sxs-lookup"><span data-stu-id="711c0-276">Import the **Azure Storage** NuGet package into the project.</span></span> <span data-ttu-id="711c0-277">You need this package because you use the Blob Storage API in this sample:</span><span class="sxs-lookup"><span data-stu-id="711c0-277">You need this package because you use the Blob Storage API in this sample:</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
1. <span data-ttu-id="711c0-278">Add the following using directives to the source file in the project:</span><span class="sxs-lookup"><span data-stu-id="711c0-278">Add the following using directives to the source file in the project:</span></span>

    ```csharp
    using System.IO;
    using System.Globalization;
    using System.Diagnostics;
    using System.Linq;
    
    using Microsoft.Azure.Management.DataFactories.Models;
    using Microsoft.Azure.Management.DataFactories.Runtime;
    
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Blob;
    ```
1. <span data-ttu-id="711c0-279">Change the name of the namespace to **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="711c0-279">Change the name of the namespace to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
1. <span data-ttu-id="711c0-280">Change the name of the class to **MyDotNetActivity**, and derive it from the **IDotNetActivity** interface as shown:</span><span class="sxs-lookup"><span data-stu-id="711c0-280">Change the name of the class to **MyDotNetActivity**, and derive it from the **IDotNetActivity** interface as shown:</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
1. <span data-ttu-id="711c0-281">Implement (add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class.</span><span class="sxs-lookup"><span data-stu-id="711c0-281">Implement (add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class.</span></span> <span data-ttu-id="711c0-282">Copy the following sample code to the method.</span><span class="sxs-lookup"><span data-stu-id="711c0-282">Copy the following sample code to the method.</span></span> <span data-ttu-id="711c0-283">For an explanation of the logic used in this method, see the [Execute method](#execute-method) section.</span><span class="sxs-lookup"><span data-stu-id="711c0-283">For an explanation of the logic used in this method, see the [Execute method](#execute-method) section.</span></span>

    ```csharp
    /// <summary>
    /// The Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // Declare types for the input and output data stores.
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // Use the First method instead of Single because we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // Create the storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // Initialize the continuation token before using it in the do-while loop.
       BlobContinuationToken continuationToken = null;
       do
       {   // get the list of input blobs from the input storage client object.
           BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
                                    true,
                                    BlobListingDetails.Metadata,
                                    null,
                                    continuationToken,
                                    null,
                                    null);
    
           // The Calculate method returns the number of occurrences of
           // the search term "Microsoft" in each blob associated
           // with the data slice.
           //
           // The definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // Get the output dataset by using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // Create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // Write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // Create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
1. <span data-ttu-id="711c0-284">Add the following helper methods to the class.</span><span class="sxs-lookup"><span data-stu-id="711c0-284">Add the following helper methods to the class.</span></span> <span data-ttu-id="711c0-285">These methods are invoked by the **Execute** method.</span><span class="sxs-lookup"><span data-stu-id="711c0-285">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="711c0-286">Most important, the **Calculate** method isolates the code that iterates through each blob.</span><span class="sxs-lookup"><span data-stu-id="711c0-286">Most important, the **Calculate** method isolates the code that iterates through each blob.</span></span>

    ```csharp
    /// <summary>
    /// Gets the folderPath value from the input/output dataset.
    /// </summary>
    private static string GetFolderPath(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FolderPath;
    }
    
    /// <summary>
    /// Gets the fileName value from the input/output dataset.
    /// </summary>
    
    private static string GetFileName(Dataset dataArtifact)
    {
       if (dataArtifact == null || dataArtifact.Properties == null)
       {
           return null;
       }
    
       AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
       if (blobDataset == null)
       {
           return null;
       }
    
       return blobDataset.FileName;
    }
    
    /// <summary>
    /// Iterates through each blob (file) in the folder, counts the number of instances of the search term in the file,
    /// and prepares the output text that is written to the output blob.
    /// </summary>
    
    public static string Calculate(BlobResultSegment Bresult, IActivityLogger logger, string folderPath, ref BlobContinuationToken token, string searchTerm)
    {
       string output = string.Empty;
       logger.Write("number of blobs found: {0}", Bresult.Results.Count<IListBlobItem>());
       foreach (IListBlobItem listBlobItem in Bresult.Results)
       {
           CloudBlockBlob inputBlob = listBlobItem as CloudBlockBlob;
           if ((inputBlob != null) && (inputBlob.Name.IndexOf("$$$.$$$") == -1))
           {
               string blobText = inputBlob.DownloadText(Encoding.ASCII, null, null, null);
               logger.Write("input blob text: {0}", blobText);
               string[] source = blobText.Split(new char[] { '.', '?', '!', ' ', ';', ':', ',' }, StringSplitOptions.RemoveEmptyEntries);
               var matchQuery = from word in source
                                where word.ToLowerInvariant() == searchTerm.ToLowerInvariant()
                                select word;
               int wordCount = matchQuery.Count();
               output += string.Format("{0} occurrences(s) of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
           }
       }
       return output;
    }
    ```
    <span data-ttu-id="711c0-287">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span><span class="sxs-lookup"><span data-stu-id="711c0-287">The GetFolderPath method returns the path to the folder that the dataset points to and the GetFileName method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="711c0-288">The Calculate method calculates the number of instances of the keyword "Microsoft" in the input files (blobs in the folder).</span><span class="sxs-lookup"><span data-stu-id="711c0-288">The Calculate method calculates the number of instances of the keyword "Microsoft" in the input files (blobs in the folder).</span></span> <span data-ttu-id="711c0-289">The search term "Microsoft" is hard-coded in the code.</span><span class="sxs-lookup"><span data-stu-id="711c0-289">The search term "Microsoft" is hard-coded in the code.</span></span>

1. <span data-ttu-id="711c0-290">Compile the project.</span><span class="sxs-lookup"><span data-stu-id="711c0-290">Compile the project.</span></span> <span data-ttu-id="711c0-291">Select **Build** from the menu, and then select **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="711c0-291">Select **Build** from the menu, and then select **Build Solution**.</span></span>

1. <span data-ttu-id="711c0-292">Start Windows Explorer, and go to the **bin\\debug** or **bin\\release** folder.</span><span class="sxs-lookup"><span data-stu-id="711c0-292">Start Windows Explorer, and go to the **bin\\debug** or **bin\\release** folder.</span></span> <span data-ttu-id="711c0-293">The folder choice depends on the type of build.</span><span class="sxs-lookup"><span data-stu-id="711c0-293">The folder choice depends on the type of build.</span></span>

1. <span data-ttu-id="711c0-294">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="711c0-294">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="711c0-295">You might want to include the MyDotNetActivity.**pdb** file so that you get additional details such as the line number in the source code that caused the issue when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="711c0-295">You might want to include the MyDotNetActivity.**pdb** file so that you get additional details such as the line number in the source code that caused the issue when a failure occurs.</span></span>

   ![The bin\Debug folder list](./media/data-factory-data-processing-using-batch/image5.png)

1. <span data-ttu-id="711c0-297">Upload **MyDotNetActivity.zip** as a blob to the blob container `customactivitycontainer` in the blob storage that the StorageLinkedService linked service in ADFTutorialDataFactory uses.</span><span class="sxs-lookup"><span data-stu-id="711c0-297">Upload **MyDotNetActivity.zip** as a blob to the blob container `customactivitycontainer` in the blob storage that the StorageLinkedService linked service in ADFTutorialDataFactory uses.</span></span> <span data-ttu-id="711c0-298">Create the blob container `customactivitycontainer` if it doesn't already exist.</span><span class="sxs-lookup"><span data-stu-id="711c0-298">Create the blob container `customactivitycontainer` if it doesn't already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="711c0-299">Execute method</span><span class="sxs-lookup"><span data-stu-id="711c0-299">Execute method</span></span>
<span data-ttu-id="711c0-300">This section provides more details about the code in the Execute method.</span><span class="sxs-lookup"><span data-stu-id="711c0-300">This section provides more details about the code in the Execute method.</span></span>

1. <span data-ttu-id="711c0-301">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span><span class="sxs-lookup"><span data-stu-id="711c0-301">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="711c0-302">To iterate through the blob collection, you're required to use the **BlobContinuationToken** class.</span><span class="sxs-lookup"><span data-stu-id="711c0-302">To iterate through the blob collection, you're required to use the **BlobContinuationToken** class.</span></span> <span data-ttu-id="711c0-303">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span><span class="sxs-lookup"><span data-stu-id="711c0-303">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="711c0-304">For more information, see [Use Blob storage from .NET](../../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-304">For more information, see [Use Blob storage from .NET](../../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="711c0-305">A basic loop is shown here:</span><span class="sxs-lookup"><span data-stu-id="711c0-305">A basic loop is shown here:</span></span>

    ```csharp
    // Initialize the continuation token.
    BlobContinuationToken continuationToken = null;
    do
    {
    // Get the list of input blobs from the input storage client object.
    BlobResultSegment blobList = inputClient.ListBlobsSegmented(folderPath,
    
                         true,
                                   BlobListingDetails.Metadata,
                                   null,
                                   continuationToken,
                                   null,
                                   null);
    // Return a string derived from parsing each blob.
    
     output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
    } while (continuationToken != null);

    ```
   <span data-ttu-id="711c0-306">For more information, see the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method.</span><span class="sxs-lookup"><span data-stu-id="711c0-306">For more information, see the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method.</span></span>

1. <span data-ttu-id="711c0-307">The code for working through the set of blobs logically goes within the do-while loop.</span><span class="sxs-lookup"><span data-stu-id="711c0-307">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="711c0-308">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="711c0-308">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="711c0-309">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span><span class="sxs-lookup"><span data-stu-id="711c0-309">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="711c0-310">It returns the number of occurrences of the search term "Microsoft" in the blob passed to the **Calculate** method.</span><span class="sxs-lookup"><span data-stu-id="711c0-310">It returns the number of occurrences of the search term "Microsoft" in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
1. <span data-ttu-id="711c0-311">After the **Calculate** method is finished, it must be written to a new blob.</span><span class="sxs-lookup"><span data-stu-id="711c0-311">After the **Calculate** method is finished, it must be written to a new blob.</span></span> <span data-ttu-id="711c0-312">For every set of blobs processed, a new blob can be written with the results.</span><span class="sxs-lookup"><span data-stu-id="711c0-312">For every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="711c0-313">To write to a new blob, first find the output dataset.</span><span class="sxs-lookup"><span data-stu-id="711c0-313">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset by using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
1. <span data-ttu-id="711c0-314">The code also calls the helper method **GetFolderPath** to retrieve the folder path (the storage container name).</span><span class="sxs-lookup"><span data-stu-id="711c0-314">The code also calls the helper method **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="711c0-315">The GetFolderPath method casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span><span class="sxs-lookup"><span data-stu-id="711c0-315">The GetFolderPath method casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
1. <span data-ttu-id="711c0-316">The code calls the **GetFileName** method to retrieve the file name (blob name).</span><span class="sxs-lookup"><span data-stu-id="711c0-316">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="711c0-317">The code is similar to the previous code that was used to get the folder path.</span><span class="sxs-lookup"><span data-stu-id="711c0-317">The code is similar to the previous code that was used to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
1. <span data-ttu-id="711c0-318">The name of the file is written by creating a URI object.</span><span class="sxs-lookup"><span data-stu-id="711c0-318">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="711c0-319">The URI constructor uses the **BlobEndpoint** property to return the container name.</span><span class="sxs-lookup"><span data-stu-id="711c0-319">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="711c0-320">The folder path and file name are added to construct the output blob URI.</span><span class="sxs-lookup"><span data-stu-id="711c0-320">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
1. <span data-ttu-id="711c0-321">After the name of the file is written, you can write the output string from the **Calculate** method to a new blob:</span><span class="sxs-lookup"><span data-stu-id="711c0-321">After the name of the file is written, you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="711c0-322">Create the data factory</span><span class="sxs-lookup"><span data-stu-id="711c0-322">Create the data factory</span></span>
<span data-ttu-id="711c0-323">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to a blob container.</span><span class="sxs-lookup"><span data-stu-id="711c0-323">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to a blob container.</span></span> <span data-ttu-id="711c0-324">In this section, you create a data factory with a pipeline that uses the custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-324">In this section, you create a data factory with a pipeline that uses the custom activity.</span></span>

<span data-ttu-id="711c0-325">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-325">The input dataset for the custom activity represents the blobs (files) in the input folder (`mycontainer\\inputfolder`) in blob storage.</span></span> <span data-ttu-id="711c0-326">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-326">The output dataset for the activity represents the output blobs in the output folder (`mycontainer\\outputfolder`) in blob storage.</span></span>

<span data-ttu-id="711c0-327">Drop one or more files into the input folders:</span><span class="sxs-lookup"><span data-stu-id="711c0-327">Drop one or more files into the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="711c0-328">For example, drop one file (file.txt) with the following content into each of the folders:</span><span class="sxs-lookup"><span data-stu-id="711c0-328">For example, drop one file (file.txt) with the following content into each of the folders:</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="711c0-329">Each input folder corresponds to a slice in the data factory even if the folder has two or more files.</span><span class="sxs-lookup"><span data-stu-id="711c0-329">Each input folder corresponds to a slice in the data factory even if the folder has two or more files.</span></span> <span data-ttu-id="711c0-330">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-330">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="711c0-331">You see five output files with the same content.</span><span class="sxs-lookup"><span data-stu-id="711c0-331">You see five output files with the same content.</span></span> <span data-ttu-id="711c0-332">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span><span class="sxs-lookup"><span data-stu-id="711c0-332">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="711c0-333">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content into the input folder, you see the following content in the output file.</span><span class="sxs-lookup"><span data-stu-id="711c0-333">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content into the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="711c0-334">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span><span class="sxs-lookup"><span data-stu-id="711c0-334">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="711c0-335">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="711c0-335">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="711c0-336">A task is created for each activity run.</span><span class="sxs-lookup"><span data-stu-id="711c0-336">A task is created for each activity run.</span></span> <span data-ttu-id="711c0-337">In this sample, there is only one activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="711c0-337">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="711c0-338">When a slice is processed by the pipeline, the custom activity runs on Batch to process the slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-338">When a slice is processed by the pipeline, the custom activity runs on Batch to process the slice.</span></span> <span data-ttu-id="711c0-339">Because there are five slices (each slice can have multiple blobs or file), five tasks are created in Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-339">Because there are five slices (each slice can have multiple blobs or file), five tasks are created in Batch.</span></span> <span data-ttu-id="711c0-340">When a task runs on Batch, it's the custom activity that is running.</span><span class="sxs-lookup"><span data-stu-id="711c0-340">When a task runs on Batch, it's the custom activity that is running.</span></span>

<span data-ttu-id="711c0-341">The following walkthrough provides additional details.</span><span class="sxs-lookup"><span data-stu-id="711c0-341">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="711c0-342">Step 1: Create the data factory</span><span class="sxs-lookup"><span data-stu-id="711c0-342">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="711c0-343">After you sign in to the [Azure portal](https://portal.azure.com/), take the following steps:</span><span class="sxs-lookup"><span data-stu-id="711c0-343">After you sign in to the [Azure portal](https://portal.azure.com/), take the following steps:</span></span>

   <span data-ttu-id="711c0-344">a.</span><span class="sxs-lookup"><span data-stu-id="711c0-344">a.</span></span> <span data-ttu-id="711c0-345">Select **NEW** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="711c0-345">Select **NEW** on the left menu.</span></span>

   <span data-ttu-id="711c0-346">b.</span><span class="sxs-lookup"><span data-stu-id="711c0-346">b.</span></span> <span data-ttu-id="711c0-347">Select **Data + Analytics** on the **New** blade.</span><span class="sxs-lookup"><span data-stu-id="711c0-347">Select **Data + Analytics** on the **New** blade.</span></span>

   <span data-ttu-id="711c0-348">c.</span><span class="sxs-lookup"><span data-stu-id="711c0-348">c.</span></span> <span data-ttu-id="711c0-349">Select **Data Factory** on the **Data analytics** blade.</span><span class="sxs-lookup"><span data-stu-id="711c0-349">Select **Data Factory** on the **Data analytics** blade.</span></span>

1. <span data-ttu-id="711c0-350">On the **New data factory** blade, enter **CustomActivityFactory** for the name.</span><span class="sxs-lookup"><span data-stu-id="711c0-350">On the **New data factory** blade, enter **CustomActivityFactory** for the name.</span></span> <span data-ttu-id="711c0-351">The name of the data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="711c0-351">The name of the data factory must be globally unique.</span></span> <span data-ttu-id="711c0-352">If you receive the error "Data factory name CustomActivityFactory is not available," change the name of the data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-352">If you receive the error "Data factory name CustomActivityFactory is not available," change the name of the data factory.</span></span> <span data-ttu-id="711c0-353">For example, use yournameCustomActivityFactory, and create the data factory again.</span><span class="sxs-lookup"><span data-stu-id="711c0-353">For example, use yournameCustomActivityFactory, and create the data factory again.</span></span>

1. <span data-ttu-id="711c0-354">Select **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="711c0-354">Select **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>

1. <span data-ttu-id="711c0-355">Verify that the subscription and region where you want the data factory to be created are correct.</span><span class="sxs-lookup"><span data-stu-id="711c0-355">Verify that the subscription and region where you want the data factory to be created are correct.</span></span>

1. <span data-ttu-id="711c0-356">Select **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="711c0-356">Select **Create** on the **New data factory** blade.</span></span>

1. <span data-ttu-id="711c0-357">The data factory is created in the dashboard of the portal.</span><span class="sxs-lookup"><span data-stu-id="711c0-357">The data factory is created in the dashboard of the portal.</span></span>

1. <span data-ttu-id="711c0-358">After the data factory is created successfully, you see the **Data factory** page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-358">After the data factory is created successfully, you see the **Data factory** page, which shows you the contents of the data factory.</span></span>

   ![Data factory page](./media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="711c0-360">Step 2: Create linked services</span><span class="sxs-lookup"><span data-stu-id="711c0-360">Step 2: Create linked services</span></span>
<span data-ttu-id="711c0-361">Linked services link data stores or compute services to a data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-361">Linked services link data stores or compute services to a data factory.</span></span> <span data-ttu-id="711c0-362">In this step, you link your storage account and Batch account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-362">In this step, you link your storage account and Batch account to your data factory.</span></span>

#### <a name="create-an-azure-storage-linked-service"></a><span data-ttu-id="711c0-363">Create an Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="711c0-363">Create an Azure Storage linked service</span></span>
1. <span data-ttu-id="711c0-364">Select the **Author and deploy** tile on the **Data factory** blade for **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="711c0-364">Select the **Author and deploy** tile on the **Data factory** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="711c0-365">The Data Factory Editor appears.</span><span class="sxs-lookup"><span data-stu-id="711c0-365">The Data Factory Editor appears.</span></span>

1. <span data-ttu-id="711c0-366">Select **New data store** on the command bar, and choose **Azure storage.**</span><span class="sxs-lookup"><span data-stu-id="711c0-366">Select **New data store** on the command bar, and choose **Azure storage.**</span></span> <span data-ttu-id="711c0-367">The JSON script you use to create a Storage linked service in the editor appears.</span><span class="sxs-lookup"><span data-stu-id="711c0-367">The JSON script you use to create a Storage linked service in the editor appears.</span></span>

   ![New data store](./media/data-factory-data-processing-using-batch/image7.png)

1. <span data-ttu-id="711c0-369">Replace **account name** with the name of your storage account.</span><span class="sxs-lookup"><span data-stu-id="711c0-369">Replace **account name** with the name of your storage account.</span></span> <span data-ttu-id="711c0-370">Replace **account key** with the access key of the storage account.</span><span class="sxs-lookup"><span data-stu-id="711c0-370">Replace **account key** with the access key of the storage account.</span></span> <span data-ttu-id="711c0-371">To learn how to get your storage access key, see [View, copy, and regenerate storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="711c0-371">To learn how to get your storage access key, see [View, copy, and regenerate storage access keys](../../storage/common/storage-create-storage-account.md#manage-your-storage-account).</span></span>

1. <span data-ttu-id="711c0-372">Select **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="711c0-372">Select **Deploy** on the command bar to deploy the linked service.</span></span>

   ![Deploy](./media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-an-azure-batch-linked-service"></a><span data-ttu-id="711c0-374">Create an Azure Batch linked service</span><span class="sxs-lookup"><span data-stu-id="711c0-374">Create an Azure Batch linked service</span></span>
<span data-ttu-id="711c0-375">In this step, you create a linked service for your Batch account that is used to run the data factory custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-375">In this step, you create a linked service for your Batch account that is used to run the data factory custom activity.</span></span>

1. <span data-ttu-id="711c0-376">Select **New compute** on the command bar, and choose **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="711c0-376">Select **New compute** on the command bar, and choose **Azure Batch.**</span></span> <span data-ttu-id="711c0-377">The JSON script you use to create a Batch linked service in the editor appears.</span><span class="sxs-lookup"><span data-stu-id="711c0-377">The JSON script you use to create a Batch linked service in the editor appears.</span></span>

1. <span data-ttu-id="711c0-378">In the JSON script:</span><span class="sxs-lookup"><span data-stu-id="711c0-378">In the JSON script:</span></span>

   <span data-ttu-id="711c0-379">a.</span><span class="sxs-lookup"><span data-stu-id="711c0-379">a.</span></span> <span data-ttu-id="711c0-380">Replace **account name** with the name of your Batch account.</span><span class="sxs-lookup"><span data-stu-id="711c0-380">Replace **account name** with the name of your Batch account.</span></span>

   <span data-ttu-id="711c0-381">b.</span><span class="sxs-lookup"><span data-stu-id="711c0-381">b.</span></span> <span data-ttu-id="711c0-382">Replace **access key** with the access key of the Batch account.</span><span class="sxs-lookup"><span data-stu-id="711c0-382">Replace **access key** with the access key of the Batch account.</span></span>

   <span data-ttu-id="711c0-383">c.</span><span class="sxs-lookup"><span data-stu-id="711c0-383">c.</span></span> <span data-ttu-id="711c0-384">Enter the ID of the pool for the **poolName** property.</span><span class="sxs-lookup"><span data-stu-id="711c0-384">Enter the ID of the pool for the **poolName** property.</span></span> <span data-ttu-id="711c0-385">For this property, you can specify either the pool name or the pool ID.</span><span class="sxs-lookup"><span data-stu-id="711c0-385">For this property, you can specify either the pool name or the pool ID.</span></span>

   <span data-ttu-id="711c0-386">d.</span><span class="sxs-lookup"><span data-stu-id="711c0-386">d.</span></span> <span data-ttu-id="711c0-387">Enter the batch URI for the **batchUri** JSON property.</span><span class="sxs-lookup"><span data-stu-id="711c0-387">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="711c0-388">The URL from the **Batch Account** blade is in the following format: \<accountname\>.\<region\>.batch.azure.com.</span><span class="sxs-lookup"><span data-stu-id="711c0-388">The URL from the **Batch Account** blade is in the following format: \<accountname\>.\<region\>.batch.azure.com.</span></span> <span data-ttu-id="711c0-389">For the **batchUri** property in the JSON script, you need to remove a88"accountname."\*\* from the URL.</span><span class="sxs-lookup"><span data-stu-id="711c0-389">For the **batchUri** property in the JSON script, you need to remove a88"accountname."\*\* from the URL.</span></span> <span data-ttu-id="711c0-390">An example is `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="711c0-390">An example is `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![Batch Account blade](./media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="711c0-392">For the **poolName** property, you also can specify the ID of the pool instead of the name of the pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-392">For the **poolName** property, you also can specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="711c0-393">The Data Factory service doesn't support an on-demand option for Batch as it does for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="711c0-393">The Data Factory service doesn't support an on-demand option for Batch as it does for HDInsight.</span></span> <span data-ttu-id="711c0-394">You can use only your own Batch pool in a data factory.</span><span class="sxs-lookup"><span data-stu-id="711c0-394">You can use only your own Batch pool in a data factory.</span></span>
      >
      >
   
   <span data-ttu-id="711c0-395">e.</span><span class="sxs-lookup"><span data-stu-id="711c0-395">e.</span></span> <span data-ttu-id="711c0-396">Specify **StorageLinkedService** for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="711c0-396">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="711c0-397">You created this linked service in the previous step.</span><span class="sxs-lookup"><span data-stu-id="711c0-397">You created this linked service in the previous step.</span></span> <span data-ttu-id="711c0-398">This storage is used as a staging area for files and logs.</span><span class="sxs-lookup"><span data-stu-id="711c0-398">This storage is used as a staging area for files and logs.</span></span>

1. <span data-ttu-id="711c0-399">Select **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="711c0-399">Select **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="711c0-400">Step 3: Create datasets</span><span class="sxs-lookup"><span data-stu-id="711c0-400">Step 3: Create datasets</span></span>
<span data-ttu-id="711c0-401">In this step, you create datasets to represent input and output data.</span><span class="sxs-lookup"><span data-stu-id="711c0-401">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-the-input-dataset"></a><span data-ttu-id="711c0-402">Create the input dataset</span><span class="sxs-lookup"><span data-stu-id="711c0-402">Create the input dataset</span></span>
1. <span data-ttu-id="711c0-403">In the Data Factory Editor, select the **New dataset** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="711c0-403">In the Data Factory Editor, select the **New dataset** button on the toolbar.</span></span> <span data-ttu-id="711c0-404">Select **Azure Blob storage** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="711c0-404">Select **Azure Blob storage** from the drop-down list.</span></span>

1. <span data-ttu-id="711c0-405">Replace the JSON script in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="711c0-405">Replace the JSON script in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "InputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
               "format": {
                   "type": "TextFormat"
               },
               "partitionedBy": [
                   {
                       "name": "Year",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy"
                       }
                   },
                   {
                       "name": "Month",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "MM"
                       }
                   },
                   {
                       "name": "Day",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "dd"
                       }
                   },
                   {
                       "name": "Hour",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           },
           "external": true,
           "policy": {}
       }
    }
    ```

    <span data-ttu-id="711c0-406">You create a pipeline later in this walkthrough with the start time 2015-11-16T00:00:00Z and the end time 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="711c0-406">You create a pipeline later in this walkthrough with the start time 2015-11-16T00:00:00Z and the end time 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="711c0-407">It's scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -\> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="711c0-407">It's scheduled to produce data hourly, so there are five input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="711c0-408">The **frequency** and **interval** for the input dataset are set to **Hour** and **1**, which means that the input slice is available hourly.</span><span class="sxs-lookup"><span data-stu-id="711c0-408">The **frequency** and **interval** for the input dataset are set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="711c0-409">The start time for each slice is represented by the **SliceStart** system variable in the previous JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="711c0-409">The start time for each slice is represented by the **SliceStart** system variable in the previous JSON snippet.</span></span> <span data-ttu-id="711c0-410">Here are the start times for each slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-410">Here are the start times for each slice.</span></span>

    | <span data-ttu-id="711c0-411">**Slice**</span><span class="sxs-lookup"><span data-stu-id="711c0-411">**Slice**</span></span> | <span data-ttu-id="711c0-412">**Start time**</span><span class="sxs-lookup"><span data-stu-id="711c0-412">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="711c0-413">1</span><span class="sxs-lookup"><span data-stu-id="711c0-413">1</span></span>         | <span data-ttu-id="711c0-414">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-414">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="711c0-415">2</span><span class="sxs-lookup"><span data-stu-id="711c0-415">2</span></span>         | <span data-ttu-id="711c0-416">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-416">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="711c0-417">3</span><span class="sxs-lookup"><span data-stu-id="711c0-417">3</span></span>         | <span data-ttu-id="711c0-418">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-418">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="711c0-419">4</span><span class="sxs-lookup"><span data-stu-id="711c0-419">4</span></span>         | <span data-ttu-id="711c0-420">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-420">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="711c0-421">5</span><span class="sxs-lookup"><span data-stu-id="711c0-421">5</span></span>         | <span data-ttu-id="711c0-422">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-422">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="711c0-423">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="711c0-423">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="711c0-424">Here is how an input folder is mapped to a slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-424">Here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="711c0-425">**Slice**</span><span class="sxs-lookup"><span data-stu-id="711c0-425">**Slice**</span></span> | <span data-ttu-id="711c0-426">**Start time**</span><span class="sxs-lookup"><span data-stu-id="711c0-426">**Start time**</span></span>          | <span data-ttu-id="711c0-427">**Input folder**</span><span class="sxs-lookup"><span data-stu-id="711c0-427">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="711c0-428">1</span><span class="sxs-lookup"><span data-stu-id="711c0-428">1</span></span>         | <span data-ttu-id="711c0-429">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-429">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="711c0-430">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="711c0-430">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="711c0-431">2</span><span class="sxs-lookup"><span data-stu-id="711c0-431">2</span></span>         | <span data-ttu-id="711c0-432">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-432">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="711c0-433">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="711c0-433">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="711c0-434">3</span><span class="sxs-lookup"><span data-stu-id="711c0-434">3</span></span>         | <span data-ttu-id="711c0-435">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-435">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="711c0-436">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="711c0-436">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="711c0-437">4</span><span class="sxs-lookup"><span data-stu-id="711c0-437">4</span></span>         | <span data-ttu-id="711c0-438">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-438">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="711c0-439">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="711c0-439">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="711c0-440">5</span><span class="sxs-lookup"><span data-stu-id="711c0-440">5</span></span>         | <span data-ttu-id="711c0-441">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-441">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="711c0-442">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="711c0-442">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="711c0-443">Select **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span><span class="sxs-lookup"><span data-stu-id="711c0-443">Select **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-the-output-dataset"></a><span data-ttu-id="711c0-444">Create the output dataset</span><span class="sxs-lookup"><span data-stu-id="711c0-444">Create the output dataset</span></span>
<span data-ttu-id="711c0-445">In this step, you create another dataset of the type AzureBlob to represent the output data.</span><span class="sxs-lookup"><span data-stu-id="711c0-445">In this step, you create another dataset of the type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="711c0-446">In the Data Factory Editor, select the **New dataset** button on the toolbar.</span><span class="sxs-lookup"><span data-stu-id="711c0-446">In the Data Factory Editor, select the **New dataset** button on the toolbar.</span></span> <span data-ttu-id="711c0-447">Select **Azure Blob storage** from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="711c0-447">Select **Azure Blob storage** from the drop-down list.</span></span>

1. <span data-ttu-id="711c0-448">Replace the JSON script in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="711c0-448">Replace the JSON script in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "OutputDataset",
       "properties": {
           "type": "AzureBlob",
           "linkedServiceName": "AzureStorageLinkedService",
           "typeProperties": {
               "fileName": "{slice}.txt",
               "folderPath": "mycontainer/outputfolder",
               "partitionedBy": [
                   {
                       "name": "slice",
                       "value": {
                           "type": "DateTime",
                           "date": "SliceStart",
                           "format": "yyyy-MM-dd-HH"
                       }
                   }
               ]
           },
           "availability": {
               "frequency": "Hour",
               "interval": 1
           }
       }
    }
    ```

    <span data-ttu-id="711c0-449">An output blob/file is generated for each input slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-449">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="711c0-450">Here is how an output file is named for each slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-450">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="711c0-451">All the output files are generated in one output folder, `mycontainer\\outputfolder`.</span><span class="sxs-lookup"><span data-stu-id="711c0-451">All the output files are generated in one output folder, `mycontainer\\outputfolder`.</span></span>

    | <span data-ttu-id="711c0-452">**Slice**</span><span class="sxs-lookup"><span data-stu-id="711c0-452">**Slice**</span></span> | <span data-ttu-id="711c0-453">**Start time**</span><span class="sxs-lookup"><span data-stu-id="711c0-453">**Start time**</span></span>          | <span data-ttu-id="711c0-454">**Output file**</span><span class="sxs-lookup"><span data-stu-id="711c0-454">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="711c0-455">1</span><span class="sxs-lookup"><span data-stu-id="711c0-455">1</span></span>         | <span data-ttu-id="711c0-456">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-456">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="711c0-457">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="711c0-457">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="711c0-458">2</span><span class="sxs-lookup"><span data-stu-id="711c0-458">2</span></span>         | <span data-ttu-id="711c0-459">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-459">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="711c0-460">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="711c0-460">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="711c0-461">3</span><span class="sxs-lookup"><span data-stu-id="711c0-461">3</span></span>         | <span data-ttu-id="711c0-462">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-462">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="711c0-463">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="711c0-463">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="711c0-464">4</span><span class="sxs-lookup"><span data-stu-id="711c0-464">4</span></span>         | <span data-ttu-id="711c0-465">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-465">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="711c0-466">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="711c0-466">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="711c0-467">5</span><span class="sxs-lookup"><span data-stu-id="711c0-467">5</span></span>         | <span data-ttu-id="711c0-468">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="711c0-468">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="711c0-469">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="711c0-469">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="711c0-470">Remember that all the files in an input folder (for example, 2015-11-16-00) are part of a slice with the start time 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="711c0-470">Remember that all the files in an input folder (for example, 2015-11-16-00) are part of a slice with the start time 2015-11-16-00.</span></span> <span data-ttu-id="711c0-471">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of the search term "Microsoft."</span><span class="sxs-lookup"><span data-stu-id="711c0-471">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of the search term "Microsoft."</span></span> <span data-ttu-id="711c0-472">If there are three files in the folder 2015-11-16-00, there are three lines in the output file  2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="711c0-472">If there are three files in the folder 2015-11-16-00, there are three lines in the output file  2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="711c0-473">Select **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="711c0-473">Select **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-a-custom-activity"></a><span data-ttu-id="711c0-474">Step 4: Create and run the pipeline with a custom activity</span><span class="sxs-lookup"><span data-stu-id="711c0-474">Step 4: Create and run the pipeline with a custom activity</span></span>
<span data-ttu-id="711c0-475">In this step, you create a pipeline with one activity, the custom activity you created previously.</span><span class="sxs-lookup"><span data-stu-id="711c0-475">In this step, you create a pipeline with one activity, the custom activity you created previously.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="711c0-476">If you haven't uploaded **file.txt** to input folders in the blob container, do so before you create the pipeline.</span><span class="sxs-lookup"><span data-stu-id="711c0-476">If you haven't uploaded **file.txt** to input folders in the blob container, do so before you create the pipeline.</span></span> <span data-ttu-id="711c0-477">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately because the **start** date is in the past.</span><span class="sxs-lookup"><span data-stu-id="711c0-477">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately because the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="711c0-478">In the Data Factory Editor, select **New pipeline** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="711c0-478">In the Data Factory Editor, select **New pipeline** on the command bar.</span></span> <span data-ttu-id="711c0-479">If you don't see the command, select the ellipsis symbol to display it.</span><span class="sxs-lookup"><span data-stu-id="711c0-479">If you don't see the command, select the ellipsis symbol to display it.</span></span>

1. <span data-ttu-id="711c0-480">Replace the JSON script in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="711c0-480">Replace the JSON script in the right pane with the following JSON snippet:</span></span>

    ```json
    {
       "name": "PipelineCustom",
       "properties": {
           "description": "Use custom activity",
           "activities": [
               {
                   "type": "DotNetActivity",
                   "typeProperties": {
                       "assemblyName": "MyDotNetActivity.dll",
                       "entryPoint": "MyDotNetActivityNS.MyDotNetActivity",
                       "packageLinkedService": "AzureStorageLinkedService",
                       "packageFile": "customactivitycontainer/MyDotNetActivity.zip"
                   },
                   "inputs": [
                       {
                           "name": "InputDataset"
                       }
                   ],
                   "outputs": [
                       {
                           "name": "OutputDataset"
                       }
                   ],
                   "policy": {
                       "timeout": "00:30:00",
                       "concurrency": 5,
                       "retry": 3
                   },
                   "scheduler": {
                       "frequency": "Hour",
                       "interval": 1
                   },
                   "name": "MyDotNetActivity",
                   "linkedServiceName": "AzureBatchLinkedService"
               }
           ],
           "start": "2015-11-16T00:00:00Z",
           "end": "2015-11-16T05:00:00Z",
           "isPaused": false
      }
    }
    ```
   <span data-ttu-id="711c0-481">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="711c0-481">Note the following points:</span></span>

   * <span data-ttu-id="711c0-482">Only one activity is in the pipeline, and it's of the type **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="711c0-482">Only one activity is in the pipeline, and it's of the type **DotNetActivity**.</span></span>
   * <span data-ttu-id="711c0-483">**AssemblyName** is set to the name of the DLL **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="711c0-483">**AssemblyName** is set to the name of the DLL **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="711c0-484">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="711c0-484">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="711c0-485">It's basically \<namespace\>.\<classname\> in your code.</span><span class="sxs-lookup"><span data-stu-id="711c0-485">It's basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="711c0-486">**PackageLinkedService** is set to **StorageLinkedService**, which points to the blob storage that contains the custom activity zip file.</span><span class="sxs-lookup"><span data-stu-id="711c0-486">**PackageLinkedService** is set to **StorageLinkedService**, which points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="711c0-487">If you use different storage accounts for input/output files and the custom activity zip file, you have to create another Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="711c0-487">If you use different storage accounts for input/output files and the custom activity zip file, you have to create another Storage linked service.</span></span> <span data-ttu-id="711c0-488">This article assumes that you use the same storage account.</span><span class="sxs-lookup"><span data-stu-id="711c0-488">This article assumes that you use the same storage account.</span></span>
   * <span data-ttu-id="711c0-489">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="711c0-489">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="711c0-490">It's in the format \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="711c0-490">It's in the format \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="711c0-491">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span><span class="sxs-lookup"><span data-stu-id="711c0-491">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="711c0-492">The **linkedServiceName** property of the custom activity points to **AzureBatchLinkedService**, which tells Data Factory that the custom activity needs to run on Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-492">The **linkedServiceName** property of the custom activity points to **AzureBatchLinkedService**, which tells Data Factory that the custom activity needs to run on Batch.</span></span>
   * <span data-ttu-id="711c0-493">The **concurrency** setting is important.</span><span class="sxs-lookup"><span data-stu-id="711c0-493">The **concurrency** setting is important.</span></span> <span data-ttu-id="711c0-494">If you use the default value, which is 1, even if you have two or more compute nodes in the Batch pool, the slices are processed one after another.</span><span class="sxs-lookup"><span data-stu-id="711c0-494">If you use the default value, which is 1, even if you have two or more compute nodes in the Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="711c0-495">Therefore, you aren't taking advantage of the parallel processing capability of Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-495">Therefore, you aren't taking advantage of the parallel processing capability of Batch.</span></span> <span data-ttu-id="711c0-496">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Batch) can be processed at the same time.</span><span class="sxs-lookup"><span data-stu-id="711c0-496">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Batch) can be processed at the same time.</span></span> <span data-ttu-id="711c0-497">In this case, both the VMs in the Batch pool are utilized.</span><span class="sxs-lookup"><span data-stu-id="711c0-497">In this case, both the VMs in the Batch pool are utilized.</span></span> <span data-ttu-id="711c0-498">Set the concurrency property appropriately.</span><span class="sxs-lookup"><span data-stu-id="711c0-498">Set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="711c0-499">Only one task (slice) is executed on a VM at any point by default.</span><span class="sxs-lookup"><span data-stu-id="711c0-499">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="711c0-500">By default, **Maximum tasks per VM** is set to 1 for a Batch pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-500">By default, **Maximum tasks per VM** is set to 1 for a Batch pool.</span></span> <span data-ttu-id="711c0-501">As part of the prerequisites, you created a pool with this property set to 2.</span><span class="sxs-lookup"><span data-stu-id="711c0-501">As part of the prerequisites, you created a pool with this property set to 2.</span></span> <span data-ttu-id="711c0-502">Therefore, two data factory slices can run on a VM at the same time.</span><span class="sxs-lookup"><span data-stu-id="711c0-502">Therefore, two data factory slices can run on a VM at the same time.</span></span>
    - <span data-ttu-id="711c0-503">The **isPaused** property is set to false by default.</span><span class="sxs-lookup"><span data-stu-id="711c0-503">The **isPaused** property is set to false by default.</span></span> <span data-ttu-id="711c0-504">The pipeline runs immediately in this example because the slices start in the past.</span><span class="sxs-lookup"><span data-stu-id="711c0-504">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="711c0-505">You can set this property to **true** to pause the pipeline and set it back to **false** to restart.</span><span class="sxs-lookup"><span data-stu-id="711c0-505">You can set this property to **true** to pause the pipeline and set it back to **false** to restart.</span></span>
    -   <span data-ttu-id="711c0-506">The **start** and **end** times are five hours apart.</span><span class="sxs-lookup"><span data-stu-id="711c0-506">The **start** and **end** times are five hours apart.</span></span> <span data-ttu-id="711c0-507">Slices are produced hourly, so five slices are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="711c0-507">Slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="711c0-508">Select **Deploy** on the command bar to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="711c0-508">Select **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="711c0-509">Step 5: Test the pipeline</span><span class="sxs-lookup"><span data-stu-id="711c0-509">Step 5: Test the pipeline</span></span>
<span data-ttu-id="711c0-510">In this step, you test the pipeline by dropping files into the input folders.</span><span class="sxs-lookup"><span data-stu-id="711c0-510">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="711c0-511">Start by testing the pipeline with one file for each input folder.</span><span class="sxs-lookup"><span data-stu-id="711c0-511">Start by testing the pipeline with one file for each input folder.</span></span>

1. <span data-ttu-id="711c0-512">On the **Data factory** blade in the Azure portal, select **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="711c0-512">On the **Data factory** blade in the Azure portal, select **Diagram**.</span></span>

   ![Diagram](./media/data-factory-data-processing-using-batch/image10.png)

1. <span data-ttu-id="711c0-514">In the **Diagram** view, double-click the input dataset **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="711c0-514">In the **Diagram** view, double-click the input dataset **InputDataset**.</span></span>

   ![InputDataset](./media/data-factory-data-processing-using-batch/image11.png)

1. <span data-ttu-id="711c0-516">The **InputDataset** blade appears with all five slices ready.</span><span class="sxs-lookup"><span data-stu-id="711c0-516">The **InputDataset** blade appears with all five slices ready.</span></span> <span data-ttu-id="711c0-517">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-517">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![Input slice start and end times](./media/data-factory-data-processing-using-batch/image12.png)

1. <span data-ttu-id="711c0-519">In the **Diagram** view, select **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="711c0-519">In the **Diagram** view, select **OutputDataset**.</span></span>

1. <span data-ttu-id="711c0-520">The five output slices appear in the **Ready** state if they were produced.</span><span class="sxs-lookup"><span data-stu-id="711c0-520">The five output slices appear in the **Ready** state if they were produced.</span></span>

   ![Output slice start and end times](./media/data-factory-data-processing-using-batch/image13.png)

1. <span data-ttu-id="711c0-522">Use the portal to view the tasks associated with the slices and see what VM each slice ran on.</span><span class="sxs-lookup"><span data-stu-id="711c0-522">Use the portal to view the tasks associated with the slices and see what VM each slice ran on.</span></span> <span data-ttu-id="711c0-523">For more information, see the [Data Factory and Batch integration](#data-factory-and-batch-integration) section.</span><span class="sxs-lookup"><span data-stu-id="711c0-523">For more information, see the [Data Factory and Batch integration](#data-factory-and-batch-integration) section.</span></span>

1. <span data-ttu-id="711c0-524">The output files appear under `mycontainer` in `outputfolder` in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-524">The output files appear under `mycontainer` in `outputfolder` in your blob storage.</span></span>

   ![Output files in storage](./media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="711c0-526">Five output files are listed, one for each input slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-526">Five output files are listed, one for each input slice.</span></span> <span data-ttu-id="711c0-527">Each of the output files has content similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="711c0-527">Each of the output files has content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="711c0-528">The following diagram illustrates how the data factory slices map to tasks in Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-528">The following diagram illustrates how the data factory slices map to tasks in Batch.</span></span> <span data-ttu-id="711c0-529">In this example, a slice has only one run.</span><span class="sxs-lookup"><span data-stu-id="711c0-529">In this example, a slice has only one run.</span></span>

   ![Slice mapping diagram](./media/data-factory-data-processing-using-batch/image16.png)

1. <span data-ttu-id="711c0-531">Now try with multiple files in a folder.</span><span class="sxs-lookup"><span data-stu-id="711c0-531">Now try with multiple files in a folder.</span></span> <span data-ttu-id="711c0-532">Create the files **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="711c0-532">Create the files **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder **2015-11-06-01**.</span></span>

1. <span data-ttu-id="711c0-533">In the output folder, delete the output file **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="711c0-533">In the output folder, delete the output file **2015-11-16-01.txt**.</span></span>

1. <span data-ttu-id="711c0-534">On the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**.</span><span class="sxs-lookup"><span data-stu-id="711c0-534">On the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**.</span></span> <span data-ttu-id="711c0-535">Select **Run** to rerun/reprocess the slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-535">Select **Run** to rerun/reprocess the slice.</span></span> <span data-ttu-id="711c0-536">The slice now has five files instead of one file.</span><span class="sxs-lookup"><span data-stu-id="711c0-536">The slice now has five files instead of one file.</span></span>

    ![Run](./media/data-factory-data-processing-using-batch/image17.png)

1. <span data-ttu-id="711c0-538">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**).</span><span class="sxs-lookup"><span data-stu-id="711c0-538">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**).</span></span> <span data-ttu-id="711c0-539">The output file appears under `mycontainer` in `outputfolder` in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="711c0-539">The output file appears under `mycontainer` in `outputfolder` in your blob storage.</span></span> <span data-ttu-id="711c0-540">There should be a line for each file of the slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-540">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="711c0-541">If you didn't delete the output file 2015-11-16-01.txt before you tried with five input files, you see one line from the previous slice run and five lines from the current slice run.</span><span class="sxs-lookup"><span data-stu-id="711c0-541">If you didn't delete the output file 2015-11-16-01.txt before you tried with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="711c0-542">By default, the content is appended to the output file if it already exists.</span><span class="sxs-lookup"><span data-stu-id="711c0-542">By default, the content is appended to the output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="711c0-543">Data Factory and Batch integration</span><span class="sxs-lookup"><span data-stu-id="711c0-543">Data Factory and Batch integration</span></span>
<span data-ttu-id="711c0-544">The Data Factory service creates a job in Batch with the name `adf-poolname:job-xxx`.</span><span class="sxs-lookup"><span data-stu-id="711c0-544">The Data Factory service creates a job in Batch with the name `adf-poolname:job-xxx`.</span></span>

![Batch jobs](media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="711c0-546">A task in the job is created for each activity run of a slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-546">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="711c0-547">If 10 slices are ready to be processed, 10 tasks are created in the job.</span><span class="sxs-lookup"><span data-stu-id="711c0-547">If 10 slices are ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="711c0-548">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-548">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="711c0-549">If the maximum number of tasks per compute node is set to greater than one, more than one slice can run on the same compute.</span><span class="sxs-lookup"><span data-stu-id="711c0-549">If the maximum number of tasks per compute node is set to greater than one, more than one slice can run on the same compute.</span></span>

<span data-ttu-id="711c0-550">In this example, there are five slices, so there are five tasks in Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-550">In this example, there are five slices, so there are five tasks in Batch.</span></span> <span data-ttu-id="711c0-551">With **concurrency** set to **5** in the pipeline JSON in the data factory and **Maximum tasks per VM** set to **2** in the Batch pool with **2** VMs, the tasks run fast.</span><span class="sxs-lookup"><span data-stu-id="711c0-551">With **concurrency** set to **5** in the pipeline JSON in the data factory and **Maximum tasks per VM** set to **2** in the Batch pool with **2** VMs, the tasks run fast.</span></span> <span data-ttu-id="711c0-552">(Check the start and end times for tasks.)</span><span class="sxs-lookup"><span data-stu-id="711c0-552">(Check the start and end times for tasks.)</span></span>

<span data-ttu-id="711c0-553">Use the portal to view the Batch job and its tasks that are associated with the slices and see what VM each slice ran on.</span><span class="sxs-lookup"><span data-stu-id="711c0-553">Use the portal to view the Batch job and its tasks that are associated with the slices and see what VM each slice ran on.</span></span>

![Batch job tasks](media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="711c0-555">Debug the pipeline</span><span class="sxs-lookup"><span data-stu-id="711c0-555">Debug the pipeline</span></span>
<span data-ttu-id="711c0-556">Debugging consists of a few basic techniques.</span><span class="sxs-lookup"><span data-stu-id="711c0-556">Debugging consists of a few basic techniques.</span></span>

1. <span data-ttu-id="711c0-557">If the input slice isn't set to **Ready**, confirm that the input folder structure is correct and that file.txt exists in the input folders.</span><span class="sxs-lookup"><span data-stu-id="711c0-557">If the input slice isn't set to **Ready**, confirm that the input folder structure is correct and that file.txt exists in the input folders.</span></span>

   ![Input folder structure](./media/data-factory-data-processing-using-batch/image3.png)

1. <span data-ttu-id="711c0-559">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="711c0-559">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="711c0-560">The logged messages show up in the user\_0.log file.</span><span class="sxs-lookup"><span data-stu-id="711c0-560">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="711c0-561">On the **OutputDataset** blade, select the slice to see the **Data slice** blade for that slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-561">On the **OutputDataset** blade, select the slice to see the **Data slice** blade for that slice.</span></span> <span data-ttu-id="711c0-562">Under **Activity runs**, you see one activity run for the slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-562">Under **Activity runs**, you see one activity run for the slice.</span></span> <span data-ttu-id="711c0-563">If you select **Run** in the command bar, you can start another activity run for the same slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-563">If you select **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="711c0-564">When you select the activity run, you see the **Activity run details** blade with a list of log files.</span><span class="sxs-lookup"><span data-stu-id="711c0-564">When you select the activity run, you see the **Activity run details** blade with a list of log files.</span></span> <span data-ttu-id="711c0-565">You see logged messages in the user\_0.log file.</span><span class="sxs-lookup"><span data-stu-id="711c0-565">You see logged messages in the user\_0.log file.</span></span> <span data-ttu-id="711c0-566">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span><span class="sxs-lookup"><span data-stu-id="711c0-566">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="711c0-567">When you select the activity run, you see the log files that you can review to troubleshoot the error.</span><span class="sxs-lookup"><span data-stu-id="711c0-567">When you select the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![OutputDataset and Data slice blades](./media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="711c0-569">In the list of log files, select **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="711c0-569">In the list of log files, select **user-0.log**.</span></span> <span data-ttu-id="711c0-570">In the right panel, the results of using the **IActivityLogger.Write** method appear.</span><span class="sxs-lookup"><span data-stu-id="711c0-570">In the right panel, the results of using the **IActivityLogger.Write** method appear.</span></span>

   ![Activity run details blade](./media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="711c0-572">Check the system-0.log for any system error messages and exceptions.</span><span class="sxs-lookup"><span data-stu-id="711c0-572">Check the system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
1. <span data-ttu-id="711c0-573">Include the **PDB** file in the zip file so that the error details have information such as call stack when an error occurs.</span><span class="sxs-lookup"><span data-stu-id="711c0-573">Include the **PDB** file in the zip file so that the error details have information such as call stack when an error occurs.</span></span>

1. <span data-ttu-id="711c0-574">All the files in the zip file for the custom activity must be at the top level with no subfolders.</span><span class="sxs-lookup"><span data-stu-id="711c0-574">All the files in the zip file for the custom activity must be at the top level with no subfolders.</span></span>

   ![Custom activity zip file list](./media/data-factory-data-processing-using-batch/image20.png)

1. <span data-ttu-id="711c0-576">Ensure that **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the blob storage that contains the zip file) are set to the correct values.</span><span class="sxs-lookup"><span data-stu-id="711c0-576">Ensure that **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the blob storage that contains the zip file) are set to the correct values.</span></span>

1. <span data-ttu-id="711c0-577">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and select **Run**.</span><span class="sxs-lookup"><span data-stu-id="711c0-577">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and select **Run**.</span></span>

   ![OutputDataset blade Run option](./media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="711c0-579">A container is in your blob storage named `adfjobs`.</span><span class="sxs-lookup"><span data-stu-id="711c0-579">A container is in your blob storage named `adfjobs`.</span></span> <span data-ttu-id="711c0-580">This container isn't automatically deleted, but you can safely delete it after you finish testing the solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-580">This container isn't automatically deleted, but you can safely delete it after you finish testing the solution.</span></span> <span data-ttu-id="711c0-581">Similarly, the data factory solution creates a Batch job named `adf-\<pool ID/name\>:job-0000000001`.</span><span class="sxs-lookup"><span data-stu-id="711c0-581">Similarly, the data factory solution creates a Batch job named `adf-\<pool ID/name\>:job-0000000001`.</span></span> <span data-ttu-id="711c0-582">You can delete this job after you test the solution if you like.</span><span class="sxs-lookup"><span data-stu-id="711c0-582">You can delete this job after you test the solution if you like.</span></span>
   >
   >
1. <span data-ttu-id="711c0-583">The custom activity doesn't use the **app.config** file from your package.</span><span class="sxs-lookup"><span data-stu-id="711c0-583">The custom activity doesn't use the **app.config** file from your package.</span></span> <span data-ttu-id="711c0-584">Therefore, if your code reads any connection strings from the configuration file, it doesn't work at runtime.</span><span class="sxs-lookup"><span data-stu-id="711c0-584">Therefore, if your code reads any connection strings from the configuration file, it doesn't work at runtime.</span></span> <span data-ttu-id="711c0-585">The best practice when you use Batch is to hold any secrets in Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="711c0-585">The best practice when you use Batch is to hold any secrets in Azure Key Vault.</span></span> <span data-ttu-id="711c0-586">Then use a certificate-based service principal to protect the key vault and distribute the certificate to the Batch pool.</span><span class="sxs-lookup"><span data-stu-id="711c0-586">Then use a certificate-based service principal to protect the key vault and distribute the certificate to the Batch pool.</span></span> <span data-ttu-id="711c0-587">The .NET custom activity can access secrets from the key vault at runtime.</span><span class="sxs-lookup"><span data-stu-id="711c0-587">The .NET custom activity can access secrets from the key vault at runtime.</span></span> <span data-ttu-id="711c0-588">This generic solution can scale to any type of secret, not just a connection string.</span><span class="sxs-lookup"><span data-stu-id="711c0-588">This generic solution can scale to any type of secret, not just a connection string.</span></span>

    <span data-ttu-id="711c0-589">There is an easier workaround, but it's not a best practice.</span><span class="sxs-lookup"><span data-stu-id="711c0-589">There is an easier workaround, but it's not a best practice.</span></span> <span data-ttu-id="711c0-590">You can create a SQL database linked service with connection string settings.</span><span class="sxs-lookup"><span data-stu-id="711c0-590">You can create a SQL database linked service with connection string settings.</span></span> <span data-ttu-id="711c0-591">Then you can create a dataset that uses the linked service and chain the dataset as a dummy input dataset to the custom .NET activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-591">Then you can create a dataset that uses the linked service and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="711c0-592">You can then access the linked service's connection string in the custom activity code.</span><span class="sxs-lookup"><span data-stu-id="711c0-592">You can then access the linked service's connection string in the custom activity code.</span></span> <span data-ttu-id="711c0-593">It should work fine at runtime.</span><span class="sxs-lookup"><span data-stu-id="711c0-593">It should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="711c0-594">Extend the sample</span><span class="sxs-lookup"><span data-stu-id="711c0-594">Extend the sample</span></span>
<span data-ttu-id="711c0-595">You can extend this sample to learn more about Data Factory and Batch features.</span><span class="sxs-lookup"><span data-stu-id="711c0-595">You can extend this sample to learn more about Data Factory and Batch features.</span></span> <span data-ttu-id="711c0-596">For example, to process slices in a different time range, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="711c0-596">For example, to process slices in a different time range, take the following steps:</span></span>

1. <span data-ttu-id="711c0-597">Add the following subfolders in `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, and 2015-11-16-09.</span><span class="sxs-lookup"><span data-stu-id="711c0-597">Add the following subfolders in `inputfolder`: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, and 2015-11-16-09.</span></span> <span data-ttu-id="711c0-598">Place input files in those folders.</span><span class="sxs-lookup"><span data-stu-id="711c0-598">Place input files in those folders.</span></span> <span data-ttu-id="711c0-599">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="711c0-599">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="711c0-600">In the **Diagram** view, double-click **InputDataset** and confirm that the input slices are ready.</span><span class="sxs-lookup"><span data-stu-id="711c0-600">In the **Diagram** view, double-click **InputDataset** and confirm that the input slices are ready.</span></span> <span data-ttu-id="711c0-601">Double-click **OutputDataset** to see the state of the output slices.</span><span class="sxs-lookup"><span data-stu-id="711c0-601">Double-click **OutputDataset** to see the state of the output slices.</span></span> <span data-ttu-id="711c0-602">If they're in the **Ready** state, check the output folder for the output files.</span><span class="sxs-lookup"><span data-stu-id="711c0-602">If they're in the **Ready** state, check the output folder for the output files.</span></span>

1. <span data-ttu-id="711c0-603">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Batch.</span><span class="sxs-lookup"><span data-stu-id="711c0-603">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Batch.</span></span> <span data-ttu-id="711c0-604">For more information on the **concurrency** setting, see "Step 4: Create and run the pipeline with a custom activity."</span><span class="sxs-lookup"><span data-stu-id="711c0-604">For more information on the **concurrency** setting, see "Step 4: Create and run the pipeline with a custom activity."</span></span>

1. <span data-ttu-id="711c0-605">Create a pool with higher/lower **Maximum tasks per VM**.</span><span class="sxs-lookup"><span data-stu-id="711c0-605">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="711c0-606">To use the new pool you created, update the Batch linked service in the data factory solution.</span><span class="sxs-lookup"><span data-stu-id="711c0-606">To use the new pool you created, update the Batch linked service in the data factory solution.</span></span> <span data-ttu-id="711c0-607">For more information on the **Maximum tasks per VM** setting, see "Step 4: Create and run the pipeline with a custom activity."</span><span class="sxs-lookup"><span data-stu-id="711c0-607">For more information on the **Maximum tasks per VM** setting, see "Step 4: Create and run the pipeline with a custom activity."</span></span>

1. <span data-ttu-id="711c0-608">Create a Batch pool with the **autoscale** feature.</span><span class="sxs-lookup"><span data-stu-id="711c0-608">Create a Batch pool with the **autoscale** feature.</span></span> <span data-ttu-id="711c0-609">Automatically scaling compute nodes in a Batch pool is the dynamic adjustment of processing power used by your application.</span><span class="sxs-lookup"><span data-stu-id="711c0-609">Automatically scaling compute nodes in a Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="711c0-610">The sample formula here achieves the following behavior.</span><span class="sxs-lookup"><span data-stu-id="711c0-610">The sample formula here achieves the following behavior.</span></span> <span data-ttu-id="711c0-611">When the pool is initially created, it starts with one VM.</span><span class="sxs-lookup"><span data-stu-id="711c0-611">When the pool is initially created, it starts with one VM.</span></span> <span data-ttu-id="711c0-612">The $PendingTasks metric defines the number of tasks in the running and active (queued) states.</span><span class="sxs-lookup"><span data-stu-id="711c0-612">The $PendingTasks metric defines the number of tasks in the running and active (queued) states.</span></span> <span data-ttu-id="711c0-613">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span><span class="sxs-lookup"><span data-stu-id="711c0-613">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="711c0-614">It ensures that TargetDedicated never goes beyond 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="711c0-614">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="711c0-615">As new tasks are submitted, the pool automatically grows.</span><span class="sxs-lookup"><span data-stu-id="711c0-615">As new tasks are submitted, the pool automatically grows.</span></span> <span data-ttu-id="711c0-616">As tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span><span class="sxs-lookup"><span data-stu-id="711c0-616">As tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="711c0-617">You can adjust startingNumberOfVMs and maxNumberofVMs to your needs.</span><span class="sxs-lookup"><span data-stu-id="711c0-617">You can adjust startingNumberOfVMs and maxNumberofVMs to your needs.</span></span>
 
    <span data-ttu-id="711c0-618">Autoscale formula:</span><span class="sxs-lookup"><span data-stu-id="711c0-618">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="711c0-619">For more information, see [Automatically scale compute nodes in a Batch pool](../../batch/batch-automatic-scaling.md).</span><span class="sxs-lookup"><span data-stu-id="711c0-619">For more information, see [Automatically scale compute nodes in a Batch pool](../../batch/batch-automatic-scaling.md).</span></span>

   <span data-ttu-id="711c0-620">If the pool uses the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service might take 15 to 30 minutes to prepare the VM before running the custom activity.</span><span class="sxs-lookup"><span data-stu-id="711c0-620">If the pool uses the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service might take 15 to 30 minutes to prepare the VM before running the custom activity.</span></span> <span data-ttu-id="711c0-621">If the pool uses a different autoScaleEvaluationInterval, the Batch service might take autoScaleEvaluationInterval plus 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="711c0-621">If the pool uses a different autoScaleEvaluationInterval, the Batch service might take autoScaleEvaluationInterval plus 10 minutes.</span></span>

1. <span data-ttu-id="711c0-622">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span><span class="sxs-lookup"><span data-stu-id="711c0-622">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="711c0-623">You can write your own method to process input data and replace the **Calculate** method call in the **Execute** method with a call to your method.</span><span class="sxs-lookup"><span data-stu-id="711c0-623">You can write your own method to process input data and replace the **Calculate** method call in the **Execute** method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="711c0-624">Next steps: Consume the data</span><span class="sxs-lookup"><span data-stu-id="711c0-624">Next steps: Consume the data</span></span>
<span data-ttu-id="711c0-625">After you process data, you can consume it with online tools such as Power BI.</span><span class="sxs-lookup"><span data-stu-id="711c0-625">After you process data, you can consume it with online tools such as Power BI.</span></span> <span data-ttu-id="711c0-626">Here are links to help you understand Power BI and how to use it in Azure:</span><span class="sxs-lookup"><span data-stu-id="711c0-626">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="711c0-627">Explore a dataset in Power BI</span><span class="sxs-lookup"><span data-stu-id="711c0-627">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="711c0-628">Get started with Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="711c0-628">Get started with Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="711c0-629">Refresh data in Power BI</span><span class="sxs-lookup"><span data-stu-id="711c0-629">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="711c0-630">Azure and Power BI: Basic overview</span><span class="sxs-lookup"><span data-stu-id="711c0-630">Azure and Power BI: Basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="711c0-631">References</span><span class="sxs-lookup"><span data-stu-id="711c0-631">References</span></span>
* [<span data-ttu-id="711c0-632">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="711c0-632">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="711c0-633">Introduction to the Data Factory service</span><span class="sxs-lookup"><span data-stu-id="711c0-633">Introduction to the Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="711c0-634">Get started with Data Factory</span><span class="sxs-lookup"><span data-stu-id="711c0-634">Get started with Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="711c0-635">Use custom activities in a Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="711c0-635">Use custom activities in a Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="711c0-636">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="711c0-636">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="711c0-637">Basics of Batch</span><span class="sxs-lookup"><span data-stu-id="711c0-637">Basics of Batch</span></span>](../../batch/batch-technical-overview.md)
  * [<span data-ttu-id="711c0-638">Overview of Batch features</span><span class="sxs-lookup"><span data-stu-id="711c0-638">Overview of Batch features</span></span>](../../batch/batch-api-basics.md)
  * [<span data-ttu-id="711c0-639">Create and manage a Batch account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="711c0-639">Create and manage a Batch account in the Azure portal</span></span>](../../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="711c0-640">Get started with the Batch client library for .NET</span><span class="sxs-lookup"><span data-stu-id="711c0-640">Get started with the Batch client library for .NET</span></span>](../../batch/quick-run-dotnet.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx
