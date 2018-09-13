---
title: Process large-scale datasets using Data Factory and Batch | Microsoft Docs
description: Describes how to process huge amounts of data in an Azure Data Factory pipeline by using parallel processing capability of Azure Batch.
services: data-factory
documentationcenter: ''
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 688b964b-51d0-4faa-91a7-26c7e3150868
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: spelluru
ms.openlocfilehash: 6eac4f4071410fbe7b8d657a87accfe8602c8e08
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554685"
---
# <a name="process-large-scale-datasets-using-data-factory-and-batch"></a><span data-ttu-id="7bb8c-103">Process large-scale datasets using Data Factory and Batch</span><span class="sxs-lookup"><span data-stu-id="7bb8c-103">Process large-scale datasets using Data Factory and Batch</span></span>
<span data-ttu-id="7bb8c-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-104">This article describes an architecture of a sample solution that moves and processes large-scale datasets in an automatic and scheduled manner.</span></span> <span data-ttu-id="7bb8c-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-105">It also provides an end-to-end walkthrough to implement the solution using Azure Data Factory and Azure Batch.</span></span>

<span data-ttu-id="7bb8c-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-106">This article is longer than our typical article because it contains a walkthrough of an entire sample solution.</span></span> <span data-ttu-id="7bb8c-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-107">If you are new to Batch and Data Factory, you can learn about these services and how they work together.</span></span> <span data-ttu-id="7bb8c-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-108">If you know something about the services and are designing/architecting a solution, you may focus just on the [architecture section](#architecture-of-sample-solution) of the article and if you are developing a prototype or a solution, you may also want to try out step-by-step instructions in the [walkthrough](#implementation-of-sample-solution).</span></span> <span data-ttu-id="7bb8c-109">We invite your comments about this content and how you use it.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-109">We invite your comments about this content and how you use it.</span></span>

<span data-ttu-id="7bb8c-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-110">First, let's look at how Data Factory and Batch services can help with processing large datasets in the cloud.</span></span>     

## <a name="why-azure-batch"></a><span data-ttu-id="7bb8c-111">Why Azure Batch?</span><span class="sxs-lookup"><span data-stu-id="7bb8c-111">Why Azure Batch?</span></span>
<span data-ttu-id="7bb8c-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-112">Azure Batch enables you to run large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="7bb8c-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-113">It's a platform service that schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="7bb8c-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-114">With the Batch service, you define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="7bb8c-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-115">You can run on-demand or scheduled jobs, and you don't need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span>

<span data-ttu-id="7bb8c-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-116">See the following articles if you are not familiar with Azure Batch as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>   

* [<span data-ttu-id="7bb8c-117">Basics of Azure Batch</span><span class="sxs-lookup"><span data-stu-id="7bb8c-117">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
* [<span data-ttu-id="7bb8c-118">Batch feature overview</span><span class="sxs-lookup"><span data-stu-id="7bb8c-118">Batch feature overview</span></span>](../batch/batch-api-basics.md)

<span data-ttu-id="7bb8c-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-119">(optional) To learn more about Azure Batch, see the [Learning path for Azure Batch](https://azure.microsoft.com/documentation/learning-paths/batch/).</span></span>

## <a name="why-azure-data-factory"></a><span data-ttu-id="7bb8c-120">Why Azure Data Factory?</span><span class="sxs-lookup"><span data-stu-id="7bb8c-120">Why Azure Data Factory?</span></span>
<span data-ttu-id="7bb8c-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-121">Data Factory is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="7bb8c-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-122">Using the Data Factory service, you can create managed data pipelines that move data from on-premises and cloud data stores to a centralized data store (for example: Azure Blob Storage), and process/transform data using services such as Azure HDInsight and Azure Machine Learning.</span></span> <span data-ttu-id="7bb8c-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-123">You can also schedule data pipelines to run in a scheduled manner (hourly, daily, weekly, etc.) and monitor and manage them at a glance to identify issues and take action.</span></span>

<span data-ttu-id="7bb8c-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-124">See the following articles if you are not familiar with Azure Data Factory as it helps with understanding the architecture/implementation of the solution described in this article.</span></span>  

* [<span data-ttu-id="7bb8c-125">Introduction of Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7bb8c-125">Introduction of Azure Data Factory</span></span>](data-factory-introduction.md)
* [<span data-ttu-id="7bb8c-126">Build your first data pipeline</span><span class="sxs-lookup"><span data-stu-id="7bb8c-126">Build your first data pipeline</span></span>](data-factory-build-your-first-pipeline.md)   

<span data-ttu-id="7bb8c-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-127">(optional) To learn more about Azure Data Factory, see the [Learning path for Azure Data Factory](https://azure.microsoft.com/documentation/learning-paths/data-factory/).</span></span>

## <a name="data-factory-and-batch-together"></a><span data-ttu-id="7bb8c-128">Data Factory and Batch together</span><span class="sxs-lookup"><span data-stu-id="7bb8c-128">Data Factory and Batch together</span></span>
<span data-ttu-id="7bb8c-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-129">Data Factory includes built-in activities such as Copy Activity to copy/move data from a source data store to a destination data store and Hive Activity to process data using Hadoop clusters (HDInsight) on Azure.</span></span> <span data-ttu-id="7bb8c-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-130">See [Data Transformation Activities](data-factory-data-transformation-activities.md) for a list of supported transformation activities.</span></span>

<span data-ttu-id="7bb8c-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-131">It also allows you to create custom .NET activities to move or process data with your own logic and run these activities on an Azure HDInsight cluster or on an Azure Batch pool of VMs.</span></span> <span data-ttu-id="7bb8c-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-132">When you use Azure Batch, you can configure the pool to auto-scale (add or remove VMs based on the workload) based on a formula you provide.</span></span>     

## <a name="architecture-of-sample-solution"></a><span data-ttu-id="7bb8c-133">Architecture of sample solution</span><span class="sxs-lookup"><span data-stu-id="7bb8c-133">Architecture of sample solution</span></span>
<span data-ttu-id="7bb8c-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-134">Even though the architecture described in this article is for a simple solution, it is relevant to complex scenarios such as risk modeling by financial services, image processing and rendering, and genomic analysis.</span></span>

<span data-ttu-id="7bb8c-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-135">The diagram illustrates 1) how Data Factory orchestrates data movement and processing and 2) how Azure Batch processes the data in a parallel manner.</span></span> <span data-ttu-id="7bb8c-136">Download and print the diagram for easy reference (11 x 17 in.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-136">Download and print the diagram for easy reference (11 x 17 in.</span></span> <span data-ttu-id="7bb8c-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-137">or A3 size): [HPC and data orchestration using Azure Batch and Data Factory](http://go.microsoft.com/fwlink/?LinkId=717686).</span></span>

<span data-ttu-id="7bb8c-138">[![Large-scale data processing diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-138">[![Large-scale data processing diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image1.png)](http://go.microsoft.com/fwlink/?LinkId=717686)</span></span>

<span data-ttu-id="7bb8c-139">The following list provides the basic steps of the process.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-139">The following list provides the basic steps of the process.</span></span> <span data-ttu-id="7bb8c-140">The solution includes code and explanations to build the end-to-end solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-140">The solution includes code and explanations to build the end-to-end solution.</span></span>

1. <span data-ttu-id="7bb8c-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-141">**Configure Azure Batch with a pool of compute nodes (VMs)**.</span></span> <span data-ttu-id="7bb8c-142">You can specify the number of nodes and size of each node.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-142">You can specify the number of nodes and size of each node.</span></span>
2. <span data-ttu-id="7bb8c-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-143">**Create an Azure Data Factory instance** that is configured with entities that represent Azure blob storage, Azure Batch compute service, input/output data, and a workflow/pipeline with activities that move and transform data.</span></span>
3. <span data-ttu-id="7bb8c-144">**Create a custom .NET activity in the Data Factory pipeline**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-144">**Create a custom .NET activity in the Data Factory pipeline**.</span></span> <span data-ttu-id="7bb8c-145">The activity is your user code that runs on the Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-145">The activity is your user code that runs on the Azure Batch pool.</span></span>
4. <span data-ttu-id="7bb8c-146">**Store large amounts of input data as blobs in Azure storage**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-146">**Store large amounts of input data as blobs in Azure storage**.</span></span> <span data-ttu-id="7bb8c-147">Data is divided into logical slices (usually by time).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-147">Data is divided into logical slices (usually by time).</span></span>
5. <span data-ttu-id="7bb8c-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-148">**Data Factory copies data that is processed in parallel** to the secondary location.</span></span>
6. <span data-ttu-id="7bb8c-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-149">**Data Factory runs the custom activity using the pool allocated by Batch**.</span></span> <span data-ttu-id="7bb8c-150">Data Factory can run activities concurrently.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-150">Data Factory can run activities concurrently.</span></span> <span data-ttu-id="7bb8c-151">Each activity processes a slice of data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-151">Each activity processes a slice of data.</span></span> <span data-ttu-id="7bb8c-152">The results are stored in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-152">The results are stored in Azure storage.</span></span>
7. <span data-ttu-id="7bb8c-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-153">**Data Factory moves the final results to a third location**, either for distribution via an app, or for further processing by other tools.</span></span>

## <a name="implementation-of-sample-solution"></a><span data-ttu-id="7bb8c-154">Implementation of sample solution</span><span class="sxs-lookup"><span data-stu-id="7bb8c-154">Implementation of sample solution</span></span>
<span data-ttu-id="7bb8c-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-155">The sample solution is intentionally simple and is to show you how to use Data Factory and Batch together to process datasets.</span></span> <span data-ttu-id="7bb8c-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-156">The solution simply counts the number of occurrences of a search term (“Microsoft”) in input files organized in a time series.</span></span> <span data-ttu-id="7bb8c-157">It outputs the count to output files.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-157">It outputs the count to output files.</span></span>

<span data-ttu-id="7bb8c-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-158">**Time**: If you are familiar with basics of Azure, Data Factory, and Batch, and have completed the prerequisites listed below, we estimate this solution takes 1-2 hours to complete.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="7bb8c-159">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7bb8c-159">Prerequisites</span></span>
#### <a name="azure-subscription"></a><span data-ttu-id="7bb8c-160">Azure subscription</span><span class="sxs-lookup"><span data-stu-id="7bb8c-160">Azure subscription</span></span>
<span data-ttu-id="7bb8c-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-161">If you don't have an Azure subscription, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="7bb8c-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-162">See [Free Trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

#### <a name="azure-storage-account"></a><span data-ttu-id="7bb8c-163">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="7bb8c-163">Azure storage account</span></span>
<span data-ttu-id="7bb8c-164">You use an Azure storage account for storing the data in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-164">You use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="7bb8c-165">If you don't have an Azure storage account, see [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-165">If you don't have an Azure storage account, see [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account).</span></span> <span data-ttu-id="7bb8c-166">The sample solution uses blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-166">The sample solution uses blob storage.</span></span>

#### <a name="azure-batch-account"></a><span data-ttu-id="7bb8c-167">Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="7bb8c-167">Azure Batch account</span></span>
<span data-ttu-id="7bb8c-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-168">Create an Azure Batch account using the [Azure portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="7bb8c-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-169">See [Create and manage an Azure Batch account](../batch/batch-account-create-portal.md).</span></span> <span data-ttu-id="7bb8c-170">Note the Azure Batch account name and account key.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-170">Note the Azure Batch account name and account key.</span></span> <span data-ttu-id="7bb8c-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-171">You can also use [New-AzureRmBatchAccount](https://msdn.microsoft.com/library/mt603749.aspx) cmdlet to create an Azure Batch account.</span></span> <span data-ttu-id="7bb8c-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-172">See [Get started with Azure Batch PowerShell cmdlets](../batch/batch-powershell-cmdlets-get-started.md) for detailed instructions on using this cmdlet.</span></span>

<span data-ttu-id="7bb8c-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-173">The sample solution uses Azure Batch (indirectly via an Azure Data Factory pipeline) to process data in a parallel manner on a pool of compute nodes (a managed collection of virtual machines).</span></span>

#### <a name="azure-batch-pool-of-virtual-machines-vms"></a><span data-ttu-id="7bb8c-174">Azure Batch pool of virtual machines (VMs)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-174">Azure Batch pool of virtual machines (VMs)</span></span>
<span data-ttu-id="7bb8c-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-175">Create an **Azure Batch pool** with at least 2 compute nodes.</span></span>

1. <span data-ttu-id="7bb8c-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-176">In the [Azure portal](https://portal.azure.com), click **Browse** in the left menu, and click **Batch Accounts**.</span></span>
2. <span data-ttu-id="7bb8c-177">Select your Azure Batch account to open the **Batch Account** blade.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-177">Select your Azure Batch account to open the **Batch Account** blade.</span></span>
3. <span data-ttu-id="7bb8c-178">Click **Pools** tile.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-178">Click **Pools** tile.</span></span>
4. <span data-ttu-id="7bb8c-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-179">In the **Pools** blade, click Add button on the toolbar to add a pool.</span></span>
   1. <span data-ttu-id="7bb8c-180">Enter an ID for the pool (**Pool ID**).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-180">Enter an ID for the pool (**Pool ID**).</span></span> <span data-ttu-id="7bb8c-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-181">Note the **ID of the pool**; you need it when creating the Data Factory solution.</span></span>
   2. <span data-ttu-id="7bb8c-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-182">Specify **Windows Server 2012 R2** for the Operating System Family setting.</span></span>
   3. <span data-ttu-id="7bb8c-183">Select a **node pricing tier**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-183">Select a **node pricing tier**.</span></span>
   4. <span data-ttu-id="7bb8c-184">Enter **2** as value for the **Target Dedicated** setting.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-184">Enter **2** as value for the **Target Dedicated** setting.</span></span>
   5. <span data-ttu-id="7bb8c-185">Enter **2** as value for the **Max tasks per node** setting.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-185">Enter **2** as value for the **Max tasks per node** setting.</span></span>
   6. <span data-ttu-id="7bb8c-186">Click **OK** to create the pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-186">Click **OK** to create the pool.</span></span>

#### <a name="azure-storage-explorer"></a><span data-ttu-id="7bb8c-187">Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="7bb8c-187">Azure Storage Explorer</span></span>
<span data-ttu-id="7bb8c-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-188">[Azure Storage Explorer 6 (tool)](https://azurestorageexplorer.codeplex.com/) or [CloudXplorer](http://clumsyleaf.com/products/cloudxplorer) (from ClumsyLeaf Software).</span></span> <span data-ttu-id="7bb8c-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-189">You use these tools for inspecting and altering the data in your Azure Storage projects including the logs of your cloud-hosted applications.</span></span>

1. <span data-ttu-id="7bb8c-190">Create a container named **mycontainer** with private access (no anonymous access)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-190">Create a container named **mycontainer** with private access (no anonymous access)</span></span>
2. <span data-ttu-id="7bb8c-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-191">If you are using **CloudXplorer**, create folders and subfolders with the following structure:</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image3.png)

   <span data-ttu-id="7bb8c-192">**Inputfolder** and **outputfolder** are top-level folders in **mycontainer,** and the **inputfolder** has subfolders with date-time stamps (YYYY-MM-DD-HH).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-192">**Inputfolder** and **outputfolder** are top-level folders in **mycontainer,** and the **inputfolder** has subfolders with date-time stamps (YYYY-MM-DD-HH).</span></span>

   <span data-ttu-id="7bb8c-193">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: inputfolder/2015-11-16-00/file.txt, inputfolder/2015-11-16-01/file.txt and so on.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-193">If you are using **Azure Storage Explorer**, in the next step, you need to upload files with names: inputfolder/2015-11-16-00/file.txt, inputfolder/2015-11-16-01/file.txt and so on.</span></span> <span data-ttu-id="7bb8c-194">This step automatically creates the folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-194">This step automatically creates the folders.</span></span>
3. <span data-ttu-id="7bb8c-195">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-195">Create a text file **file.txt** on your machine with content that has the keyword **Microsoft**.</span></span> <span data-ttu-id="7bb8c-196">For example: “test custom activity Microsoft test custom activity Microsoft”.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-196">For example: “test custom activity Microsoft test custom activity Microsoft”.</span></span>
4. <span data-ttu-id="7bb8c-197">Upload the file to the following input folders in Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-197">Upload the file to the following input folders in Azure blob storage.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image4.png)

   <span data-ttu-id="7bb8c-198">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-198">If you are using **Azure Storage Explorer**, upload the file **file.txt** to **mycontainer**.</span></span> <span data-ttu-id="7bb8c-199">Click **Copy** on the toolbar to create a copy of the blob.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-199">Click **Copy** on the toolbar to create a copy of the blob.</span></span> <span data-ttu-id="7bb8c-200">In the **Copy Blob** dialog box, change the **destination blob name** to **inputfolder/2015-11-16-00/file.txt.**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-200">In the **Copy Blob** dialog box, change the **destination blob name** to **inputfolder/2015-11-16-00/file.txt.**</span></span> <span data-ttu-id="7bb8c-201">Repeat this step to create inputfolder/2015-11-16-01/file.txt, inputfolder/2015-11-16-02/file.txt, inputfolder/2015-11-16-03/file.txt, inputfolder/2015-11-16-04/file.txt and so on.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-201">Repeat this step to create inputfolder/2015-11-16-01/file.txt, inputfolder/2015-11-16-02/file.txt, inputfolder/2015-11-16-03/file.txt, inputfolder/2015-11-16-04/file.txt and so on.</span></span> <span data-ttu-id="7bb8c-202">This action automatically creates the folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-202">This action automatically creates the folders.</span></span>
5. <span data-ttu-id="7bb8c-203">Create another container named: **customactivitycontainer**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-203">Create another container named: **customactivitycontainer**.</span></span> <span data-ttu-id="7bb8c-204">You upload the custom activity zip file to this container.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-204">You upload the custom activity zip file to this container.</span></span>

#### <a name="visual-studio"></a><span data-ttu-id="7bb8c-205">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7bb8c-205">Visual Studio</span></span>
<span data-ttu-id="7bb8c-206">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-206">Install Microsoft Visual Studio 2012 or later to create the custom Batch activity to be used in the Data Factory solution.</span></span>

### <a name="high-level-steps-to-create-the-solution"></a><span data-ttu-id="7bb8c-207">High-level steps to create the solution</span><span class="sxs-lookup"><span data-stu-id="7bb8c-207">High-level steps to create the solution</span></span>
1. <span data-ttu-id="7bb8c-208">Create a custom activity that contains the data processing logic.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-208">Create a custom activity that contains the data processing logic.</span></span>
2. <span data-ttu-id="7bb8c-209">Create an Azure data factory that uses the custom activity:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-209">Create an Azure data factory that uses the custom activity:</span></span>

### <a name="create-the-custom-activity"></a><span data-ttu-id="7bb8c-210">Create the custom activity</span><span class="sxs-lookup"><span data-stu-id="7bb8c-210">Create the custom activity</span></span>
<span data-ttu-id="7bb8c-211">The Data Factory custom activity is the heart of this sample solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-211">The Data Factory custom activity is the heart of this sample solution.</span></span> <span data-ttu-id="7bb8c-212">The sample solution uses Azure Batch to run the custom activity.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-212">The sample solution uses Azure Batch to run the custom activity.</span></span> <span data-ttu-id="7bb8c-213">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-213">See [Use custom activities in an Azure Data Factory pipeline](data-factory-use-custom-activities.md) for the basic information to develop custom activities and use them in Azure Data Factory pipelines.</span></span>

<span data-ttu-id="7bb8c-214">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-214">To create a .NET custom activity that you can use in an Azure Data Factory pipeline, you need to create a **.NET Class Library** project with a class that implements that **IDotNetActivity** interface.</span></span> <span data-ttu-id="7bb8c-215">This interface has only one method: **Execute**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-215">This interface has only one method: **Execute**.</span></span> <span data-ttu-id="7bb8c-216">Here is the signature of the method:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-216">Here is the signature of the method:</span></span>

```csharp
public IDictionary<string, string> Execute(
            IEnumerable<LinkedService> linkedServices,
            IEnumerable<Dataset> datasets,
            Activity activity,
            IActivityLogger logger)
```

<span data-ttu-id="7bb8c-217">The method has a few key components that you need to understand.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-217">The method has a few key components that you need to understand.</span></span>

* <span data-ttu-id="7bb8c-218">The method takes four parameters:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-218">The method takes four parameters:</span></span>

  1. <span data-ttu-id="7bb8c-219">**linkedServices**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-219">**linkedServices**.</span></span> <span data-ttu-id="7bb8c-220">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-220">An enumerable list of linked services that link input/output data sources (for example: Azure Blob Storage) to the data factory.</span></span> <span data-ttu-id="7bb8c-221">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-221">In this sample, there is only one linked service of type Azure Storage used for both input and output.</span></span>
  2. <span data-ttu-id="7bb8c-222">**datasets**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-222">**datasets**.</span></span> <span data-ttu-id="7bb8c-223">This is an enumerable list of datasets.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-223">This is an enumerable list of datasets.</span></span> <span data-ttu-id="7bb8c-224">You can use this parameter to get the locations and schemas defined by input and output datasets.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-224">You can use this parameter to get the locations and schemas defined by input and output datasets.</span></span>
  3. <span data-ttu-id="7bb8c-225">**activity**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-225">**activity**.</span></span> <span data-ttu-id="7bb8c-226">This parameter represents the current compute entity - in this case, an Azure Batch service.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-226">This parameter represents the current compute entity - in this case, an Azure Batch service.</span></span>
  4. <span data-ttu-id="7bb8c-227">**logger**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-227">**logger**.</span></span> <span data-ttu-id="7bb8c-228">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-228">The logger lets you write debug comments that surface as the “User” log for the pipeline.</span></span>
* <span data-ttu-id="7bb8c-229">The method returns a dictionary that can be used to chain custom activities together in the future.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-229">The method returns a dictionary that can be used to chain custom activities together in the future.</span></span> <span data-ttu-id="7bb8c-230">This feature is not implemented yet, so return an empty dictionary from the method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-230">This feature is not implemented yet, so return an empty dictionary from the method.</span></span>

#### <a name="procedure-create-the-custom-activity"></a><span data-ttu-id="7bb8c-231">Procedure: Create the custom activity</span><span class="sxs-lookup"><span data-stu-id="7bb8c-231">Procedure: Create the custom activity</span></span>
1. <span data-ttu-id="7bb8c-232">Create a .NET Class Library project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-232">Create a .NET Class Library project in Visual Studio.</span></span>

   1. <span data-ttu-id="7bb8c-233">Launch **Visual Studio 2012**/**2013/2015**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-233">Launch **Visual Studio 2012**/**2013/2015**.</span></span>
   2. <span data-ttu-id="7bb8c-234">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-234">Click **File**, point to **New**, and click **Project**.</span></span>
   3. <span data-ttu-id="7bb8c-235">Expand **Templates**, and select **Visual C\#**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-235">Expand **Templates**, and select **Visual C\#**.</span></span> <span data-ttu-id="7bb8c-236">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-236">In this walkthrough, you use C\#, but you can use any .NET language to develop the custom activity.</span></span>
   4. <span data-ttu-id="7bb8c-237">Select **Class Library** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-237">Select **Class Library** from the list of project types on the right.</span></span>
   5. <span data-ttu-id="7bb8c-238">Enter **MyDotNetActivity** for the **Name**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-238">Enter **MyDotNetActivity** for the **Name**.</span></span>
   6. <span data-ttu-id="7bb8c-239">Select **C:\\ADF** for the **Location**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-239">Select **C:\\ADF** for the **Location**.</span></span> <span data-ttu-id="7bb8c-240">Create the folder **ADF** if it does not exist.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-240">Create the folder **ADF** if it does not exist.</span></span>
   7. <span data-ttu-id="7bb8c-241">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-241">Click **OK** to create the project.</span></span>
2. <span data-ttu-id="7bb8c-242">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-242">Click **Tools**, point to **NuGet Package Manager**, and click **Package Manager Console**.</span></span>
3. <span data-ttu-id="7bb8c-243">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-243">In the **Package Manager Console**, execute the following command to import **Microsoft.Azure.Management.DataFactories**.</span></span>

    ```powershell
    Install-Package Microsoft.Azure.Management.DataFactories
    ```
4. <span data-ttu-id="7bb8c-244">Import the **Azure Storage** NuGet package in to the project.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-244">Import the **Azure Storage** NuGet package in to the project.</span></span> <span data-ttu-id="7bb8c-245">You need this package because you use the Blob storage API in this sample.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-245">You need this package because you use the Blob storage API in this sample.</span></span>

    ```powershell
    Install-Package Azure.Storage
    ```
5. <span data-ttu-id="7bb8c-246">Add the following **using** directives to the source file in the project.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-246">Add the following **using** directives to the source file in the project.</span></span>

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
6. <span data-ttu-id="7bb8c-247">Change the name of the **namespace** to **MyDotNetActivityNS**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-247">Change the name of the **namespace** to **MyDotNetActivityNS**.</span></span>

    ```csharp
    namespace MyDotNetActivityNS
    ```
7. <span data-ttu-id="7bb8c-248">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-248">Change the name of the class to **MyDotNetActivity** and derive it from the **IDotNetActivity** interface as shown below.</span></span>

    ```csharp
    public class MyDotNetActivity : IDotNetActivity
    ```
8. <span data-ttu-id="7bb8c-249">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-249">Implement (Add) the **Execute** method of the **IDotNetActivity** interface to the **MyDotNetActivity** class and copy the following sample code to the method.</span></span> <span data-ttu-id="7bb8c-250">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-250">See the [Execute Method](#execute-method) section for explanation for the logic used in this method.</span></span>

    ```csharp
    /// <summary>
    /// Execute method is the only method of IDotNetActivity interface you must implement.
    /// In this sample, the method invokes the Calculate method to perform the core logic.  
    /// </summary>
    public IDictionary<string, string> Execute(
       IEnumerable<LinkedService> linkedServices,
       IEnumerable<Dataset> datasets,
       Activity activity,
       IActivityLogger logger)
    {
    
       // declare types for input and output data stores
       AzureStorageLinkedService inputLinkedService;
    
       Dataset inputDataset = datasets.Single(dataset => dataset.Name == activity.Inputs.Single().Name);
    
       foreach (LinkedService ls in linkedServices)
           logger.Write("linkedService.Name {0}", ls.Name);
    
       // using First method instead of Single since we are using the same
       // Azure Storage linked service for input and output.
       inputLinkedService = linkedServices.First(
           linkedService =>
           linkedService.Name ==
           inputDataset.Properties.LinkedServiceName).Properties.TypeProperties
           as AzureStorageLinkedService;
    
       string connectionString = inputLinkedService.ConnectionString; // To create an input storage client.
       string folderPath = GetFolderPath(inputDataset);
       string output = string.Empty; // for use later.
    
       // create storage client for input. Pass the connection string.
       CloudStorageAccount inputStorageAccount = CloudStorageAccount.Parse(connectionString);
       CloudBlobClient inputClient = inputStorageAccount.CreateCloudBlobClient();
    
       // initialize the continuation token before using it in the do-while loop.
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
    
           // Calculate method returns the number of occurrences of
           // the search term (“Microsoft”) in each blob associated
           // with the data slice.
           //
           // definition of the method is shown in the next step.
           output = Calculate(blobList, logger, folderPath, ref continuationToken, "Microsoft");
    
       } while (continuationToken != null);
    
       // get the output dataset using the name of the dataset matched to a name in the Activity output collection.
       Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    
       folderPath = GetFolderPath(outputDataset);
    
       logger.Write("Writing blob to the folder: {0}", folderPath);
    
       // create a storage object for the output blob.
       CloudStorageAccount outputStorageAccount = CloudStorageAccount.Parse(connectionString);
       // write the name of the file.
       Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    
       logger.Write("output blob URI: {0}", outputBlobUri.ToString());
       // create a blob and upload the output text.
       CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
       logger.Write("Writing {0} to the output blob", output);
       outputBlob.UploadText(output);
    
       // The dictionary can be used to chain custom activities together in the future.
       // This feature is not implemented yet, so just return an empty dictionary.
       return new Dictionary<string, string>();
    }
    ```
9. <span data-ttu-id="7bb8c-251">Add the following helper methods to the class.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-251">Add the following helper methods to the class.</span></span> <span data-ttu-id="7bb8c-252">These methods are invoked by the **Execute** method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-252">These methods are invoked by the **Execute** method.</span></span> <span data-ttu-id="7bb8c-253">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-253">Most importantly, the **Calculate** method isolates the code that iterates through each blob.</span></span>

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
    /// Iterates through each blob (file) in the folder, counts the number of instances of search term in the file,
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
    <span data-ttu-id="7bb8c-254">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-254">The **GetFolderPath** method returns the path to the folder that the dataset points to and the **GetFileName** method returns the name of the blob/file that the dataset points to.</span></span>

    ```csharp

    "name": "InputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "fileName": "file.txt",
            "folderPath": "mycontainer/inputfolder/{Year}-{Month}-{Day}-{Hour}",
    ```

    <span data-ttu-id="7bb8c-255">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-255">The **Calculate** method calculates the number of instances of keyword **Microsoft** in the input files (blobs in the folder).</span></span> <span data-ttu-id="7bb8c-256">The search term (“Microsoft”) is hard-coded in the code.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-256">The search term (“Microsoft”) is hard-coded in the code.</span></span>

1. <span data-ttu-id="7bb8c-257">Compile the project.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-257">Compile the project.</span></span> <span data-ttu-id="7bb8c-258">Click **Build** from the menu and click **Build Solution**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-258">Click **Build** from the menu and click **Build Solution**.</span></span>
2. <span data-ttu-id="7bb8c-259">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-259">Launch **Windows Explorer**, and navigate to **bin\\debug** or **bin\\release** folder depending on the type of build.</span></span>
3. <span data-ttu-id="7bb8c-260">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-260">Create a zip file **MyDotNetActivity.zip** that contains all the binaries in the **\\bin\\Debug** folder.</span></span> <span data-ttu-id="7bb8c-261">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-261">You may want to include the MyDotNetActivity.**pdb** file so that you get additional details such as line number in the source code that caused the issue when a failure occurs.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image5.png)
4. <span data-ttu-id="7bb8c-262">Upload **MyDotNetActivity.zip** as a blob to the blob container: **customactivitycontainer** in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-262">Upload **MyDotNetActivity.zip** as a blob to the blob container: **customactivitycontainer** in the Azure blob storage that the **StorageLinkedService** linked service in the **ADFTutorialDataFactory** uses.</span></span> <span data-ttu-id="7bb8c-263">Create the blob container **customactivitycontainer** if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-263">Create the blob container **customactivitycontainer** if it does not already exist.</span></span>

#### <a name="execute-method"></a><span data-ttu-id="7bb8c-264">Execute method</span><span class="sxs-lookup"><span data-stu-id="7bb8c-264">Execute method</span></span>
<span data-ttu-id="7bb8c-265">This section provides more details and notes about the code in the Execute method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-265">This section provides more details and notes about the code in the Execute method.</span></span>

1. <span data-ttu-id="7bb8c-266">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-266">The members for iterating through the input collection are found in the [Microsoft.WindowsAzure.Storage.Blob](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.aspx) namespace.</span></span> <span data-ttu-id="7bb8c-267">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-267">Iterating through the blob collection requires using the **BlobContinuationToken** class.</span></span> <span data-ttu-id="7bb8c-268">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-268">In essence, you must use a do-while loop with the token as the mechanism for exiting the loop.</span></span> <span data-ttu-id="7bb8c-269">For more information, see [How to use Blob storage from .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-269">For more information, see [How to use Blob storage from .NET](../storage/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="7bb8c-270">A basic loop is shown here:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-270">A basic loop is shown here:</span></span>

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
   <span data-ttu-id="7bb8c-271">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-271">See the documentation for the [ListBlobsSegmented](https://msdn.microsoft.com/library/jj717596.aspx) method for details.</span></span>
2. <span data-ttu-id="7bb8c-272">The code for working through the set of blobs logically goes within the do-while loop.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-272">The code for working through the set of blobs logically goes within the do-while loop.</span></span> <span data-ttu-id="7bb8c-273">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-273">In the **Execute** method, the do-while loop passes the list of blobs to a method named **Calculate**.</span></span> <span data-ttu-id="7bb8c-274">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-274">The method returns a string variable named **output** that is the result of having iterated through all the blobs in the segment.</span></span>

   <span data-ttu-id="7bb8c-275">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-275">It returns the number of occurrences of the search term (**Microsoft**) in the blob passed to the **Calculate** method.</span></span>

    ```csharp
    output += string.Format("{0} occurrences of the search term \"{1}\" were found in the file {2}.\r\n", wordCount, searchTerm, inputBlob.Name);
    ```
3. <span data-ttu-id="7bb8c-276">Once the **Calculate** method has done the work, it must be written to a new blob.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-276">Once the **Calculate** method has done the work, it must be written to a new blob.</span></span> <span data-ttu-id="7bb8c-277">So for every set of blobs processed, a new blob can be written with the results.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-277">So for every set of blobs processed, a new blob can be written with the results.</span></span> <span data-ttu-id="7bb8c-278">To write to a new blob, first find the output dataset.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-278">To write to a new blob, first find the output dataset.</span></span>

    ```csharp
    // Get the output dataset using the name of the dataset matched to a name in the Activity output collection.
    Dataset outputDataset = datasets.Single(dataset => dataset.Name == activity.Outputs.Single().Name);
    ```
4. <span data-ttu-id="7bb8c-279">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-279">The code also calls a helper method: **GetFolderPath** to retrieve the folder path (the storage container name).</span></span>

    ```csharp
    folderPath = GetFolderPath(outputDataset);
    ```
   <span data-ttu-id="7bb8c-280">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-280">The **GetFolderPath** casts the DataSet object to an AzureBlobDataSet, which has a property named FolderPath.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FolderPath;
    ```
5. <span data-ttu-id="7bb8c-281">The code calls the **GetFileName** method to retrieve the file name (blob name).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-281">The code calls the **GetFileName** method to retrieve the file name (blob name).</span></span> <span data-ttu-id="7bb8c-282">The code is similar to the above code to get the folder path.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-282">The code is similar to the above code to get the folder path.</span></span>

    ```csharp
    AzureBlobDataset blobDataset = dataArtifact.Properties.TypeProperties as AzureBlobDataset;
    
    return blobDataset.FileName;
    ```
6. <span data-ttu-id="7bb8c-283">The name of the file is written by creating a URI object.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-283">The name of the file is written by creating a URI object.</span></span> <span data-ttu-id="7bb8c-284">The URI constructor uses the **BlobEndpoint** property to return the container name.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-284">The URI constructor uses the **BlobEndpoint** property to return the container name.</span></span> <span data-ttu-id="7bb8c-285">The folder path and file name are added to construct the output blob URI.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-285">The folder path and file name are added to construct the output blob URI.</span></span>  

    ```csharp
    // Write the name of the file.
    Uri outputBlobUri = new Uri(outputStorageAccount.BlobEndpoint, folderPath + "/" + GetFileName(outputDataset));
    ```
7. <span data-ttu-id="7bb8c-286">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-286">The name of the file has been written and now you can write the output string from the **Calculate** method to a new blob:</span></span>

    ```csharp
    // Create a blob and upload the output text.
    CloudBlockBlob outputBlob = new CloudBlockBlob(outputBlobUri, outputStorageAccount.Credentials);
    logger.Write("Writing {0} to the output blob", output);
    outputBlob.UploadText(output);
    ```

### <a name="create-the-data-factory"></a><span data-ttu-id="7bb8c-287">Create the data factory</span><span class="sxs-lookup"><span data-stu-id="7bb8c-287">Create the data factory</span></span>
<span data-ttu-id="7bb8c-288">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-288">In the [Create the custom activity](#create-the-custom-activity) section, you created a custom activity and uploaded the zip file with binaries and the PDB file to an Azure blob container.</span></span> <span data-ttu-id="7bb8c-289">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-289">In this section, you create an Azure **data factory** with a **pipeline** that uses the **custom activity**.</span></span>

<span data-ttu-id="7bb8c-290">The input dataset for the custom activity represents the blobs (files) in the input folder (mycontainer\\inputfolder) in blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-290">The input dataset for the custom activity represents the blobs (files) in the input folder (mycontainer\\inputfolder) in blob storage.</span></span> <span data-ttu-id="7bb8c-291">The output dataset for the activity represents the output blobs in the output folder (mycontainer\\outputfolder) in blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-291">The output dataset for the activity represents the output blobs in the output folder (mycontainer\\outputfolder) in blob storage.</span></span>

<span data-ttu-id="7bb8c-292">Drop one or more files in the input folders:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-292">Drop one or more files in the input folders:</span></span>

```
mycontainer -\> inputfolder
    2015-11-16-00
    2015-11-16-01
    2015-11-16-02
    2015-11-16-03
    2015-11-16-04
```

<span data-ttu-id="7bb8c-293">For example, drop one file (file.txt) with the following content into each of the folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-293">For example, drop one file (file.txt) with the following content into each of the folders.</span></span>

```
test custom activity Microsoft test custom activity Microsoft
```

<span data-ttu-id="7bb8c-294">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-294">Each input folder corresponds to a slice in Azure Data Factory even if the folder has 2 or more files.</span></span> <span data-ttu-id="7bb8c-295">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-295">When each slice is processed by the pipeline, the custom activity iterates through all the blobs in the input folder for that slice.</span></span>

<span data-ttu-id="7bb8c-296">You see five output files with the same content.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-296">You see five output files with the same content.</span></span> <span data-ttu-id="7bb8c-297">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-297">For example, the output file from processing the file in the 2015-11-16-00 folder has the following content:</span></span>

```
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
```

<span data-ttu-id="7bb8c-298">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-298">If you drop multiple files (file.txt, file2.txt, file3.txt) with the same content to the input folder, you see the following content in the output file.</span></span> <span data-ttu-id="7bb8c-299">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-299">Each folder (2015-11-16-00, etc.) corresponds to a slice in this sample even though the folder has multiple input files.</span></span>

```csharp
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file2.txt.
2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file3.txt.
```

<span data-ttu-id="7bb8c-300">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-300">The output file has three lines now, one for each input file (blob) in the folder associated with the slice (2015-11-16-00).</span></span>

<span data-ttu-id="7bb8c-301">A task is created for each activity run.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-301">A task is created for each activity run.</span></span> <span data-ttu-id="7bb8c-302">In this sample, there is only one activity in the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-302">In this sample, there is only one activity in the pipeline.</span></span> <span data-ttu-id="7bb8c-303">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-303">When a slice is processed by the pipeline, the custom activity runs on Azure Batch to process the slice.</span></span> <span data-ttu-id="7bb8c-304">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-304">Since there are five slices (each slice can have multiple blobs or file), there are five tasks created in Azure Batch.</span></span> <span data-ttu-id="7bb8c-305">When a task runs on Batch, it is actually the custom activity that is running.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-305">When a task runs on Batch, it is actually the custom activity that is running.</span></span>

<span data-ttu-id="7bb8c-306">The following walkthrough provides additional details.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-306">The following walkthrough provides additional details.</span></span>

#### <a name="step-1-create-the-data-factory"></a><span data-ttu-id="7bb8c-307">Step 1: Create the data factory</span><span class="sxs-lookup"><span data-stu-id="7bb8c-307">Step 1: Create the data factory</span></span>
1. <span data-ttu-id="7bb8c-308">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-308">After logging in to the [Azure portal](https://portal.azure.com/), do the following steps:</span></span>

   1. <span data-ttu-id="7bb8c-309">Click **NEW** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-309">Click **NEW** on the left menu.</span></span>
   2. <span data-ttu-id="7bb8c-310">Click **Data + Analytics** in the **New** blade.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-310">Click **Data + Analytics** in the **New** blade.</span></span>
   3. <span data-ttu-id="7bb8c-311">Click **Data Factory** on the **Data analytics** blade.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-311">Click **Data Factory** on the **Data analytics** blade.</span></span>
2. <span data-ttu-id="7bb8c-312">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-312">In the **New data factory** blade, enter **CustomActivityFactory** for the Name.</span></span> <span data-ttu-id="7bb8c-313">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-313">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="7bb8c-314">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-314">If you receive the error: **Data factory name “CustomActivityFactory” is not available**, change the name of the data factory (for example, **yournameCustomActivityFactory**) and try creating again.</span></span>
3. <span data-ttu-id="7bb8c-315">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-315">Click **RESOURCE GROUP NAME**, and select an existing resource group or create a resource group.</span></span>
4. <span data-ttu-id="7bb8c-316">Verify that you are using the correct subscription and region where you want the data factory to be created.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-316">Verify that you are using the correct subscription and region where you want the data factory to be created.</span></span>
5. <span data-ttu-id="7bb8c-317">Click **Create** on the **New data factory** blade.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-317">Click **Create** on the **New data factory** blade.</span></span>
6. <span data-ttu-id="7bb8c-318">You see the data factory being created in the **Dashboard** of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-318">You see the data factory being created in the **Dashboard** of the Azure portal.</span></span>
7. <span data-ttu-id="7bb8c-319">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-319">After the data factory has been created successfully, you see the data factory page, which shows you the contents of the data factory.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image6.png)

#### <a name="step-2-create-linked-services"></a><span data-ttu-id="7bb8c-320">Step 2: Create linked services</span><span class="sxs-lookup"><span data-stu-id="7bb8c-320">Step 2: Create linked services</span></span>
<span data-ttu-id="7bb8c-321">Linked services link data stores or compute services to an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-321">Linked services link data stores or compute services to an Azure data factory.</span></span> <span data-ttu-id="7bb8c-322">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-322">In this step, you link your **Azure Storage** account and **Azure Batch** account to your data factory.</span></span>

#### <a name="create-azure-storage-linked-service"></a><span data-ttu-id="7bb8c-323">Create Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="7bb8c-323">Create Azure Storage linked service</span></span>
1. <span data-ttu-id="7bb8c-324">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-324">Click the **Author and deploy** tile on the **DATA FACTORY** blade for **CustomActivityFactory**.</span></span> <span data-ttu-id="7bb8c-325">You see the Data Factory Editor.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-325">You see the Data Factory Editor.</span></span>
2. <span data-ttu-id="7bb8c-326">Click **New data store** on the command bar and choose **Azure storage.**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-326">Click **New data store** on the command bar and choose **Azure storage.**</span></span> <span data-ttu-id="7bb8c-327">You should see the JSON script for creating an Azure Storage linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-327">You should see the JSON script for creating an Azure Storage linked service in the editor.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image7.png)

3. <span data-ttu-id="7bb8c-328">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-328">Replace **account name** with the name of your Azure storage account and **account key** with the access key of the Azure storage account.</span></span> <span data-ttu-id="7bb8c-329">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-329">To learn how to get your storage access key, see [View, copy and regenerate storage access keys](../storage/storage-create-storage-account.md#manage-your-storage-account).</span></span>

4. <span data-ttu-id="7bb8c-330">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-330">Click **Deploy** on the command bar to deploy the linked service.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image8.png)

#### <a name="create-azure-batch-linked-service"></a><span data-ttu-id="7bb8c-331">Create Azure Batch linked service</span><span class="sxs-lookup"><span data-stu-id="7bb8c-331">Create Azure Batch linked service</span></span>
<span data-ttu-id="7bb8c-332">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-332">In this step, you create a linked service for your **Azure Batch** account that is used to run the Data Factory custom activity.</span></span>

1. <span data-ttu-id="7bb8c-333">Click **New compute** on the command bar and choose **Azure Batch.**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-333">Click **New compute** on the command bar and choose **Azure Batch.**</span></span> <span data-ttu-id="7bb8c-334">You should see the JSON script for creating an Azure Batch linked service in the editor.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-334">You should see the JSON script for creating an Azure Batch linked service in the editor.</span></span>
2. <span data-ttu-id="7bb8c-335">In the JSON script:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-335">In the JSON script:</span></span>

   1. <span data-ttu-id="7bb8c-336">Replace **account name** with the name of your Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-336">Replace **account name** with the name of your Azure Batch account.</span></span>
   2. <span data-ttu-id="7bb8c-337">Replace **access key** with the access key of the Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-337">Replace **access key** with the access key of the Azure Batch account.</span></span>
   3. <span data-ttu-id="7bb8c-338">Enter the ID of the pool for the **poolName** property **.**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-338">Enter the ID of the pool for the **poolName** property **.**</span></span> <span data-ttu-id="7bb8c-339">For this property, you can specify either pool name or pool ID.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-339">For this property, you can specify either pool name or pool ID.</span></span>
   4. <span data-ttu-id="7bb8c-340">Enter the batch URI for the **batchUri** JSON property.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-340">Enter the batch URI for the **batchUri** JSON property.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="7bb8c-341">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-341">The **URL** from the **Azure Batch account blade** is in the following format: \<accountname\>.\<region\>.batch.azure.com.</span></span> <span data-ttu-id="7bb8c-342">For the **batchUri** property in the JSON, you need to **remove "accountname."**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-342">For the **batchUri** property in the JSON, you need to **remove "accountname."**</span></span> <span data-ttu-id="7bb8c-343">from the URL.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-343">from the URL.</span></span> <span data-ttu-id="7bb8c-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-344">Example: `"batchUri": "https://eastus.batch.azure.com"`.</span></span>
      >
      >

      ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image9.png)

      <span data-ttu-id="7bb8c-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-345">For the **poolName** property, you can also specify the ID of the pool instead of the name of the pool.</span></span>

      > [!NOTE]
      > <span data-ttu-id="7bb8c-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-346">The Data Factory service does not support an on-demand option for Azure Batch as it does for HDInsight.</span></span> <span data-ttu-id="7bb8c-347">You can only use your own Azure Batch pool in an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-347">You can only use your own Azure Batch pool in an Azure data factory.</span></span>
      >
      >
   5. <span data-ttu-id="7bb8c-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-348">Specify **StorageLinkedService** for the **linkedServiceName** property.</span></span> <span data-ttu-id="7bb8c-349">You created this linked service in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-349">You created this linked service in the previous step.</span></span> <span data-ttu-id="7bb8c-350">This storage is used as a staging area for files and logs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-350">This storage is used as a staging area for files and logs.</span></span>
3. <span data-ttu-id="7bb8c-351">Click **Deploy** on the command bar to deploy the linked service.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-351">Click **Deploy** on the command bar to deploy the linked service.</span></span>

#### <a name="step-3-create-datasets"></a><span data-ttu-id="7bb8c-352">Step 3: Create datasets</span><span class="sxs-lookup"><span data-stu-id="7bb8c-352">Step 3: Create datasets</span></span>
<span data-ttu-id="7bb8c-353">In this step, you create datasets to represent input and output data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-353">In this step, you create datasets to represent input and output data.</span></span>

#### <a name="create-input-dataset"></a><span data-ttu-id="7bb8c-354">Create input dataset</span><span class="sxs-lookup"><span data-stu-id="7bb8c-354">Create input dataset</span></span>
1. <span data-ttu-id="7bb8c-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-355">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="7bb8c-356">Replace the JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-356">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="7bb8c-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-357">You create a pipeline later in this walkthrough with start time: 2015-11-16T00:00:00Z and end time: 2015-11-16T05:00:00Z.</span></span> <span data-ttu-id="7bb8c-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-358">It is scheduled to produce data **hourly**, so there are 5 input/output slices (between **00**:00:00 -\> **05**:00:00).</span></span>

    <span data-ttu-id="7bb8c-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-359">The **frequency** and **interval** for the input dataset is set to **Hour** and **1**, which means that the input slice is available hourly.</span></span>

    <span data-ttu-id="7bb8c-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-360">Here are the start times for each slice, which is represented by **SliceStart** system variable in the above JSON snippet.</span></span>

    | <span data-ttu-id="7bb8c-361">**Slice**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-361">**Slice**</span></span> | <span data-ttu-id="7bb8c-362">**Start time**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-362">**Start time**</span></span>          |
    |-----------|-------------------------|
    | <span data-ttu-id="7bb8c-363">1</span><span class="sxs-lookup"><span data-stu-id="7bb8c-363">1</span></span>         | <span data-ttu-id="7bb8c-364">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-364">2015-11-16T**00**:00:00</span></span> |
    | <span data-ttu-id="7bb8c-365">2</span><span class="sxs-lookup"><span data-stu-id="7bb8c-365">2</span></span>         | <span data-ttu-id="7bb8c-366">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-366">2015-11-16T**01**:00:00</span></span> |
    | <span data-ttu-id="7bb8c-367">3</span><span class="sxs-lookup"><span data-stu-id="7bb8c-367">3</span></span>         | <span data-ttu-id="7bb8c-368">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-368">2015-11-16T**02**:00:00</span></span> |
    | <span data-ttu-id="7bb8c-369">4</span><span class="sxs-lookup"><span data-stu-id="7bb8c-369">4</span></span>         | <span data-ttu-id="7bb8c-370">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-370">2015-11-16T**03**:00:00</span></span> |
    | <span data-ttu-id="7bb8c-371">5</span><span class="sxs-lookup"><span data-stu-id="7bb8c-371">5</span></span>         | <span data-ttu-id="7bb8c-372">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-372">2015-11-16T**04**:00:00</span></span> |

    <span data-ttu-id="7bb8c-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-373">The **folderPath** is calculated by using the year, month, day, and hour part of the slice start time (**SliceStart**).</span></span> <span data-ttu-id="7bb8c-374">Therefore, here is how an input folder is mapped to a slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-374">Therefore, here is how an input folder is mapped to a slice.</span></span>

    | <span data-ttu-id="7bb8c-375">**Slice**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-375">**Slice**</span></span> | <span data-ttu-id="7bb8c-376">**Start time**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-376">**Start time**</span></span>          | <span data-ttu-id="7bb8c-377">**Input folder**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-377">**Input folder**</span></span>  |
    |-----------|-------------------------|-------------------|
    | <span data-ttu-id="7bb8c-378">1</span><span class="sxs-lookup"><span data-stu-id="7bb8c-378">1</span></span>         | <span data-ttu-id="7bb8c-379">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-379">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="7bb8c-380">2015-11-16-**00**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-380">2015-11-16-**00**</span></span> |
    | <span data-ttu-id="7bb8c-381">2</span><span class="sxs-lookup"><span data-stu-id="7bb8c-381">2</span></span>         | <span data-ttu-id="7bb8c-382">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-382">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="7bb8c-383">2015-11-16-**01**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-383">2015-11-16-**01**</span></span> |
    | <span data-ttu-id="7bb8c-384">3</span><span class="sxs-lookup"><span data-stu-id="7bb8c-384">3</span></span>         | <span data-ttu-id="7bb8c-385">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-385">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="7bb8c-386">2015-11-16-**02**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-386">2015-11-16-**02**</span></span> |
    | <span data-ttu-id="7bb8c-387">4</span><span class="sxs-lookup"><span data-stu-id="7bb8c-387">4</span></span>         | <span data-ttu-id="7bb8c-388">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-388">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="7bb8c-389">2015-11-16-**03**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-389">2015-11-16-**03**</span></span> |
    | <span data-ttu-id="7bb8c-390">5</span><span class="sxs-lookup"><span data-stu-id="7bb8c-390">5</span></span>         | <span data-ttu-id="7bb8c-391">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-391">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="7bb8c-392">2015-11-16-**04**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-392">2015-11-16-**04**</span></span> |

1. <span data-ttu-id="7bb8c-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-393">Click **Deploy** on the toolbar to create and deploy the **InputDataset** table.</span></span>

#### <a name="create-output-dataset"></a><span data-ttu-id="7bb8c-394">Create output dataset</span><span class="sxs-lookup"><span data-stu-id="7bb8c-394">Create output dataset</span></span>
<span data-ttu-id="7bb8c-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-395">In this step, you create another dataset of type AzureBlob to represent the output data.</span></span>

1. <span data-ttu-id="7bb8c-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-396">In the **Editor** for the Data Factory, click **New dataset** button on the toolbar and click **Azure Blob storage** from the drop-down menu.</span></span>
2. <span data-ttu-id="7bb8c-397">Replace the JSON in the right pane with the following JSON snippet:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-397">Replace the JSON in the right pane with the following JSON snippet:</span></span>

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

    <span data-ttu-id="7bb8c-398">An output blob/file is generated for each input slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-398">An output blob/file is generated for each input slice.</span></span> <span data-ttu-id="7bb8c-399">Here is how an output file is named for each slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-399">Here is how an output file is named for each slice.</span></span> <span data-ttu-id="7bb8c-400">All the output files are generated in one output folder: **mycontainer\\outputfolder**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-400">All the output files are generated in one output folder: **mycontainer\\outputfolder**.</span></span>

    | <span data-ttu-id="7bb8c-401">**Slice**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-401">**Slice**</span></span> | <span data-ttu-id="7bb8c-402">**Start time**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-402">**Start time**</span></span>          | <span data-ttu-id="7bb8c-403">**Output file**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-403">**Output file**</span></span>       |
    |-----------|-------------------------|-----------------------|
    | <span data-ttu-id="7bb8c-404">1</span><span class="sxs-lookup"><span data-stu-id="7bb8c-404">1</span></span>         | <span data-ttu-id="7bb8c-405">2015-11-16T**00**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-405">2015-11-16T**00**:00:00</span></span> | <span data-ttu-id="7bb8c-406">2015-11-16-**00.txt**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-406">2015-11-16-**00.txt**</span></span> |
    | <span data-ttu-id="7bb8c-407">2</span><span class="sxs-lookup"><span data-stu-id="7bb8c-407">2</span></span>         | <span data-ttu-id="7bb8c-408">2015-11-16T**01**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-408">2015-11-16T**01**:00:00</span></span> | <span data-ttu-id="7bb8c-409">2015-11-16-**01.txt**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-409">2015-11-16-**01.txt**</span></span> |
    | <span data-ttu-id="7bb8c-410">3</span><span class="sxs-lookup"><span data-stu-id="7bb8c-410">3</span></span>         | <span data-ttu-id="7bb8c-411">2015-11-16T**02**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-411">2015-11-16T**02**:00:00</span></span> | <span data-ttu-id="7bb8c-412">2015-11-16-**02.txt**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-412">2015-11-16-**02.txt**</span></span> |
    | <span data-ttu-id="7bb8c-413">4</span><span class="sxs-lookup"><span data-stu-id="7bb8c-413">4</span></span>         | <span data-ttu-id="7bb8c-414">2015-11-16T**03**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-414">2015-11-16T**03**:00:00</span></span> | <span data-ttu-id="7bb8c-415">2015-11-16-**03.txt**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-415">2015-11-16-**03.txt**</span></span> |
    | <span data-ttu-id="7bb8c-416">5</span><span class="sxs-lookup"><span data-stu-id="7bb8c-416">5</span></span>         | <span data-ttu-id="7bb8c-417">2015-11-16T**04**:00:00</span><span class="sxs-lookup"><span data-stu-id="7bb8c-417">2015-11-16T**04**:00:00</span></span> | <span data-ttu-id="7bb8c-418">2015-11-16-**04.txt**</span><span class="sxs-lookup"><span data-stu-id="7bb8c-418">2015-11-16-**04.txt**</span></span> |

    <span data-ttu-id="7bb8c-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-419">Remember that all the files in an input folder (for example: 2015-11-16-00) are part of a slice with the start time: 2015-11-16-00.</span></span> <span data-ttu-id="7bb8c-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-420">When this slice is processed, the custom activity scans through each file and produces a line in the output file with the number of occurrences of search term (“Microsoft”).</span></span> <span data-ttu-id="7bb8c-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-421">If there are three files in the folder 2015-11-16-00, there are three lines in the output file: 2015-11-16-00.txt.</span></span>

1. <span data-ttu-id="7bb8c-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-422">Click **Deploy** on the toolbar to create and deploy the **OutputDataset**.</span></span>

#### <a name="step-4-create-and-run-the-pipeline-with-custom-activity"></a><span data-ttu-id="7bb8c-423">Step 4: Create and run the pipeline with custom activity</span><span class="sxs-lookup"><span data-stu-id="7bb8c-423">Step 4: Create and run the pipeline with custom activity</span></span>
<span data-ttu-id="7bb8c-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-424">In this step, you create a pipeline with one activity, the custom activity you created earlier.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7bb8c-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-425">If you haven't uploaded the **file.txt** to input folders in the blob container, do so before creating the pipeline.</span></span> <span data-ttu-id="7bb8c-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-426">The **isPaused** property is set to false in the pipeline JSON, so the pipeline runs immediately as the **start** date is in the past.</span></span>
>
>

1. <span data-ttu-id="7bb8c-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-427">In the Data Factory Editor, click **New pipeline** on the command bar.</span></span> <span data-ttu-id="7bb8c-428">If you do not see the command, click **... (Ellipsis)** to see it.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-428">If you do not see the command, click **... (Ellipsis)** to see it.</span></span>
2. <span data-ttu-id="7bb8c-429">Replace the JSON in the right pane with the following JSON script:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-429">Replace the JSON in the right pane with the following JSON script:</span></span>

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
   <span data-ttu-id="7bb8c-430">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-430">Note the following points:</span></span>

   * <span data-ttu-id="7bb8c-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-431">There is only one activity in the pipeline and that is of type: **DotNetActivity**.</span></span>
   * <span data-ttu-id="7bb8c-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-432">**AssemblyName** is set to the name of the DLL: **MyDotNetActivity.dll**.</span></span>
   * <span data-ttu-id="7bb8c-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-433">**EntryPoint** is set to **MyDotNetActivityNS.MyDotNetActivity**.</span></span> <span data-ttu-id="7bb8c-434">It is basically \<namespace\>.\<classname\> in your code.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-434">It is basically \<namespace\>.\<classname\> in your code.</span></span>
   * <span data-ttu-id="7bb8c-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-435">**PackageLinkedService** is set to **StorageLinkedService** that points to the blob storage that contains the custom activity zip file.</span></span> <span data-ttu-id="7bb8c-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-436">If you are using different Azure Storage accounts for input/output files and the custom activity zip file, you have to create another Azure Storage linked service.</span></span> <span data-ttu-id="7bb8c-437">This article assumes that you are using the same Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-437">This article assumes that you are using the same Azure Storage account.</span></span>
   * <span data-ttu-id="7bb8c-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-438">**PackageFile** is set to **customactivitycontainer/MyDotNetActivity.zip**.</span></span> <span data-ttu-id="7bb8c-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-439">It is in the format: \<containerforthezip\>/\<nameofthezip.zip\>.</span></span>
   * <span data-ttu-id="7bb8c-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-440">The custom activity takes **InputDataset** as input and **OutputDataset** as output.</span></span>
   * <span data-ttu-id="7bb8c-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-441">The **linkedServiceName** property of the custom activity points to the **AzureBatchLinkedService**, which tells Azure Data Factory that the custom activity needs to run on Azure Batch.</span></span>
   * <span data-ttu-id="7bb8c-442">The **concurrency** setting is important.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-442">The **concurrency** setting is important.</span></span> <span data-ttu-id="7bb8c-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-443">If you use the default value, which is 1, even if you have 2 or more compute nodes in the Azure Batch pool, the slices are processed one after another.</span></span> <span data-ttu-id="7bb8c-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-444">Therefore, you are not taking advantage of the parallel processing capability of Azure Batch.</span></span> <span data-ttu-id="7bb8c-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-445">If you set **concurrency** to a higher value, say 2, it means that two slices (corresponds to two tasks in Azure Batch) can be processed at the same time, in which case, both the VMs in the Azure Batch pool are utilized.</span></span> <span data-ttu-id="7bb8c-446">Therefore, set the concurrency property appropriately.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-446">Therefore, set the concurrency property appropriately.</span></span>
   * <span data-ttu-id="7bb8c-447">Only one task (slice) is executed on a VM at any point by default.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-447">Only one task (slice) is executed on a VM at any point by default.</span></span> <span data-ttu-id="7bb8c-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-448">The reason is that, by default, the **Maximum tasks per VM** is set to 1 for an Azure Batch pool.</span></span> <span data-ttu-id="7bb8c-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-449">As part of prerequisites, you created a pool with this property set to 2, so two Data Factory slices can be running on a VM at the same time.</span></span>

    -   <span data-ttu-id="7bb8c-450">**isPaused** property is set to false by default.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-450">**isPaused** property is set to false by default.</span></span> <span data-ttu-id="7bb8c-451">The pipeline runs immediately in this example because the slices start in the past.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-451">The pipeline runs immediately in this example because the slices start in the past.</span></span> <span data-ttu-id="7bb8c-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-452">You can set this property to true to pause the pipeline and set it back to false to restart.</span></span>

    -   <span data-ttu-id="7bb8c-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-453">The **start** time and **end** times are five hours apart and slices are produced hourly, so five slices are produced by the pipeline.</span></span>

1. <span data-ttu-id="7bb8c-454">Click **Deploy** on the command bar to deploy the pipeline.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-454">Click **Deploy** on the command bar to deploy the pipeline.</span></span>

#### <a name="step-5-test-the-pipeline"></a><span data-ttu-id="7bb8c-455">Step 5: Test the pipeline</span><span class="sxs-lookup"><span data-stu-id="7bb8c-455">Step 5: Test the pipeline</span></span>
<span data-ttu-id="7bb8c-456">In this step, you test the pipeline by dropping files into the input folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-456">In this step, you test the pipeline by dropping files into the input folders.</span></span> <span data-ttu-id="7bb8c-457">Let’s start with testing the pipeline with one file per one input folder.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-457">Let’s start with testing the pipeline with one file per one input folder.</span></span>

1. <span data-ttu-id="7bb8c-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-458">In the Data Factory blade in the Azure portal, click **Diagram**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image10.png)
2. <span data-ttu-id="7bb8c-459">In the diagram view, double-click input dataset: **InputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-459">In the diagram view, double-click input dataset: **InputDataset**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image11.png)
3. <span data-ttu-id="7bb8c-460">You should see the **InputDataset** blade with all five slices ready.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-460">You should see the **InputDataset** blade with all five slices ready.</span></span> <span data-ttu-id="7bb8c-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-461">Notice the **SLICE START TIME** and **SLICE END TIME** for each slice.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image12.png)
4. <span data-ttu-id="7bb8c-462">In the **Diagram View**, now click **OutputDataset**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-462">In the **Diagram View**, now click **OutputDataset**.</span></span>
5. <span data-ttu-id="7bb8c-463">You should see that the five output slices are in the Ready state if they have already been produced.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-463">You should see that the five output slices are in the Ready state if they have already been produced.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image13.png)
6. <span data-ttu-id="7bb8c-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-464">Use Azure portal to view the **tasks** associated with the **slices** and see what VM each slice ran on.</span></span> <span data-ttu-id="7bb8c-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-465">See [Data Factory and Batch integration](#data-factory-and-batch-integration) section for details.</span></span>
7. <span data-ttu-id="7bb8c-466">You should see the output files in the **outputfolder** of **mycontainer** in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-466">You should see the output files in the **outputfolder** of **mycontainer** in your Azure blob storage.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image15.png)

   <span data-ttu-id="7bb8c-467">You should see five output files, one for each input slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-467">You should see five output files, one for each input slice.</span></span> <span data-ttu-id="7bb8c-468">Each of the output file should have content similar to the following output:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-468">Each of the output file should have content similar to the following output:</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-00/file.txt.
    ```
   <span data-ttu-id="7bb8c-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-469">The following diagram illustrates how the Data Factory slices map to tasks in Azure Batch.</span></span> <span data-ttu-id="7bb8c-470">In this example, a slice has only one run.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-470">In this example, a slice has only one run.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image16.png)
8. <span data-ttu-id="7bb8c-471">Now, let’s try with multiple files in a folder.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-471">Now, let’s try with multiple files in a folder.</span></span> <span data-ttu-id="7bb8c-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-472">Create files: **file2.txt**, **file3.txt**, **file4.txt**, and **file5.txt** with the same content as in file.txt in the folder: **2015-11-06-01**.</span></span>
9. <span data-ttu-id="7bb8c-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-473">In the output folder, **delete** the output file: **2015-11-16-01.txt**.</span></span>
10. <span data-ttu-id="7bb8c-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-474">Now, in the **OutputDataset** blade, right-click the slice with **SLICE START TIME** set to **11/16/2015 01:00:00 AM**, and click **Run** to rerun/re-process the slice.</span></span> <span data-ttu-id="7bb8c-475">Now, the slice has five files instead of one file.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-475">Now, the slice has five files instead of one file.</span></span>

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image17.png)
11. <span data-ttu-id="7bb8c-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the **outputfolder** of **mycontainer** in your blob storage.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-476">After the slice runs and its status is **Ready**, verify the content in the output file for this slice (**2015-11-16-01.txt**) in the **outputfolder** of **mycontainer** in your blob storage.</span></span> <span data-ttu-id="7bb8c-477">There should be a line for each file of the slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-477">There should be a line for each file of the slice.</span></span>

    ```
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file2.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file3.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file4.txt.
    2 occurrences(s) of the search term "Microsoft" were found in the file inputfolder/2015-11-16-01/file5.txt.
    ```

> [!NOTE]
> <span data-ttu-id="7bb8c-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-478">If you did not delete the output file 2015-11-16-01.txt before trying with five input files, you see one line from the previous slice run and five lines from the current slice run.</span></span> <span data-ttu-id="7bb8c-479">By default, the content is appended to output file if it already exists.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-479">By default, the content is appended to output file if it already exists.</span></span>
>
>

#### <a name="data-factory-and-batch-integration"></a><span data-ttu-id="7bb8c-480">Data Factory and Batch integration</span><span class="sxs-lookup"><span data-stu-id="7bb8c-480">Data Factory and Batch integration</span></span>
<span data-ttu-id="7bb8c-481">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname:job-xxx**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-481">The Data Factory service creates a job in Azure Batch with the name: **adf-poolname:job-xxx**.</span></span>

![Azure Data Factory - Batch jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/data-factory-batch-jobs.png)

<span data-ttu-id="7bb8c-483">A task in the job is created for each activity run of a slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-483">A task in the job is created for each activity run of a slice.</span></span> <span data-ttu-id="7bb8c-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-484">If there are 10 slices ready to be processed, 10 tasks are created in the job.</span></span> <span data-ttu-id="7bb8c-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-485">You can have more than one slice running in parallel if you have multiple compute nodes in the pool.</span></span> <span data-ttu-id="7bb8c-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-486">If the maximum tasks per compute node is set to > 1, there can be more than one slice running on the same compute.</span></span>

<span data-ttu-id="7bb8c-487">In this example, there are five slices, so five tasks in Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-487">In this example, there are five slices, so five tasks in Azure Batch.</span></span> <span data-ttu-id="7bb8c-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span><span class="sxs-lookup"><span data-stu-id="7bb8c-488">With the **concurrency** set to **5** in the pipeline JSON in Azure Data Factory and **Maximum tasks per VM** set to **2** in Azure Batch pool with **2** VMs, the tasks runs fast (check start and end times for tasks).</span></span>

<span data-ttu-id="7bb8c-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-489">Use the portal to view the Batch job and its tasks that are associated with the **slices** and see what VM each slice ran on.</span></span>

![Azure Data Factory - Batch job tasks](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/data-factory-batch-job-tasks.png)

### <a name="debug-the-pipeline"></a><span data-ttu-id="7bb8c-491">Debug the pipeline</span><span class="sxs-lookup"><span data-stu-id="7bb8c-491">Debug the pipeline</span></span>
<span data-ttu-id="7bb8c-492">Debugging consists of a few basic techniques:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-492">Debugging consists of a few basic techniques:</span></span>

1. <span data-ttu-id="7bb8c-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-493">If the input slice is not set to **Ready**, confirm that the input folder structure is correct and file.txt exists in the input folders.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image3.png)
2. <span data-ttu-id="7bb8c-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-494">In the **Execute** method of your custom activity, use the **IActivityLogger** object to log information that helps you troubleshoot issues.</span></span> <span data-ttu-id="7bb8c-495">The logged messages show up in the user\_0.log file.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-495">The logged messages show up in the user\_0.log file.</span></span>

   <span data-ttu-id="7bb8c-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-496">In the **OutputDataset** blade, click the slice to see the **DATA SLICE** blade for that slice.</span></span> <span data-ttu-id="7bb8c-497">You see **activity runs** for that slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-497">You see **activity runs** for that slice.</span></span> <span data-ttu-id="7bb8c-498">You should see one activity run for the slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-498">You should see one activity run for the slice.</span></span> <span data-ttu-id="7bb8c-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-499">If you click **Run** in the command bar, you can start another activity run for the same slice.</span></span>

   <span data-ttu-id="7bb8c-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-500">When you click the activity run, you see the **ACTIVITY RUN DETAILS** blade with a list of log files.</span></span> <span data-ttu-id="7bb8c-501">You see logged messages in the **user\_0.log** file.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-501">You see logged messages in the **user\_0.log** file.</span></span> <span data-ttu-id="7bb8c-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-502">When an error occurs, you see three activity runs because the retry count is set to 3 in the pipeline/activity JSON.</span></span> <span data-ttu-id="7bb8c-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-503">When you click the activity run, you see the log files that you can review to troubleshoot the error.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image18.png)

   <span data-ttu-id="7bb8c-504">In the list of log files, click the **user-0.log**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-504">In the list of log files, click the **user-0.log**.</span></span> <span data-ttu-id="7bb8c-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-505">In the right panel are the results of using the **IActivityLogger.Write** method.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image19.png)

   <span data-ttu-id="7bb8c-506">Check system-0.log for any system error messages and exceptions.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-506">Check system-0.log for any system error messages and exceptions.</span></span>

    ```
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Loading assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Creating an instance of MyDotNetActivityNS.MyDotNetActivity from assembly file MyDotNetActivity...
    
    Trace\_T\_D\_12/6/2015 1:43:35 AM\_T\_D\_\_T\_D\_Verbose\_T\_D\_0\_T\_D\_Executing Module
    
    Trace\_T\_D\_12/6/2015 1:43:38 AM\_T\_D\_\_T\_D\_Information\_T\_D\_0\_T\_D\_Activity e3817da0-d843-4c5c-85c6-40ba7424dce2 finished successfully
    ```
3. <span data-ttu-id="7bb8c-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-507">Include the **PDB** file in the zip file so that the error details have information such as **call stack** when an error occurs.</span></span>
4. <span data-ttu-id="7bb8c-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-508">All the files in the zip file for the custom activity must be at the **top level** with no subfolders.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image20.png)
5. <span data-ttu-id="7bb8c-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-509">Ensure that the **assemblyName** (MyDotNetActivity.dll), **entryPoint** (MyDotNetActivityNS.MyDotNetActivity), **packageFile** (customactivitycontainer/MyDotNetActivity.zip), and **packageLinkedService** (should point to the Azure blob storage that contains the zip file) are set to correct values.</span></span>
6. <span data-ttu-id="7bb8c-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-510">If you fixed an error and want to reprocess the slice, right-click the slice in the **OutputDataset** blade and click **Run**.</span></span>

   ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-data-processing-using-batch/image21.png)

   > [!NOTE]
   > <span data-ttu-id="7bb8c-511">You see a **container** in your Azure Blob storage named: **adfjobs**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-511">You see a **container** in your Azure Blob storage named: **adfjobs**.</span></span> <span data-ttu-id="7bb8c-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-512">This container is not automatically deleted, but you can safely delete it after you are done testing the solution.</span></span> <span data-ttu-id="7bb8c-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: **adf-\<pool ID/name\>:job-0000000001**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-513">Similarly, the Data Factory solution creates an Azure Batch **job** named: **adf-\<pool ID/name\>:job-0000000001**.</span></span> <span data-ttu-id="7bb8c-514">You can delete this job after you test the solution if you like.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-514">You can delete this job after you test the solution if you like.</span></span>
   >
   >
7. <span data-ttu-id="7bb8c-515">The custom activity does not use the **app.config** file from your package.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-515">The custom activity does not use the **app.config** file from your package.</span></span> <span data-ttu-id="7bb8c-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-516">Therefore, if your code reads any connection strings from the configuration file, it does not work at runtime.</span></span> <span data-ttu-id="7bb8c-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-517">The best practice when using Azure Batch is to hold any secrets in an **Azure KeyVault**, use a certificate-based service principal to protect the keyvault, and distribute the certificate to Azure Batch pool.</span></span> <span data-ttu-id="7bb8c-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-518">The .NET custom activity then can access secrets from the KeyVault at runtime.</span></span> <span data-ttu-id="7bb8c-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-519">This solution is a generic one and can scale to any type of secret, not just connection string.</span></span>

    <span data-ttu-id="7bb8c-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-520">There is an easier workaround (but not a best practice): you can create an **Azure SQL linked service** with connection string settings, create a dataset that uses the linked service, and chain the dataset as a dummy input dataset to the custom .NET activity.</span></span> <span data-ttu-id="7bb8c-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-521">You can then access the linked service's connection string in the custom activity code and it should work fine at runtime.</span></span>  

#### <a name="extend-the-sample"></a><span data-ttu-id="7bb8c-522">Extend the sample</span><span class="sxs-lookup"><span data-stu-id="7bb8c-522">Extend the sample</span></span>
<span data-ttu-id="7bb8c-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-523">You can extend this sample to learn more about Azure Data Factory and Azure Batch features.</span></span> <span data-ttu-id="7bb8c-524">For example, to process slices in a different time range, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-524">For example, to process slices in a different time range, do the following steps:</span></span>

1. <span data-ttu-id="7bb8c-525">Add the following subfolders in the **inputfolder**: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-525">Add the following subfolders in the **inputfolder**: 2015-11-16-05, 2015-11-16-06, 201-11-16-07, 2011-11-16-08, 2015-11-16-09 and place input files in those folders.</span></span> <span data-ttu-id="7bb8c-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-526">Change the end time for the pipeline from `2015-11-16T05:00:00Z` to `2015-11-16T10:00:00Z`.</span></span> <span data-ttu-id="7bb8c-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-527">In the **Diagram View**, double-click the **InputDataset**, and confirm that the input slices are ready.</span></span> <span data-ttu-id="7bb8c-528">Double-click **OuptutDataset** to see the state of output slices.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-528">Double-click **OuptutDataset** to see the state of output slices.</span></span> <span data-ttu-id="7bb8c-529">If they are in Ready state, check the outputfolder for the output files.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-529">If they are in Ready state, check the outputfolder for the output files.</span></span>
2. <span data-ttu-id="7bb8c-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-530">Increase or decrease the **concurrency** setting to understand how it affects the performance of your solution, especially the processing that occurs on Azure Batch.</span></span> <span data-ttu-id="7bb8c-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-531">(See Step 4: Create and run the pipeline for more on the **concurrency** setting.)</span></span>
3. <span data-ttu-id="7bb8c-532">Create a pool with higher/lower **Maximum tasks per VM**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-532">Create a pool with higher/lower **Maximum tasks per VM**.</span></span> <span data-ttu-id="7bb8c-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-533">To use the new pool you created, update the Azure Batch linked service in the Data Factory solution.</span></span> <span data-ttu-id="7bb8c-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span><span class="sxs-lookup"><span data-stu-id="7bb8c-534">(See Step 4: Create and run the pipeline for more on the **Maximum tasks per VM** setting.)</span></span>
4. <span data-ttu-id="7bb8c-535">Create an Azure Batch pool with **autoscale** feature.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-535">Create an Azure Batch pool with **autoscale** feature.</span></span> <span data-ttu-id="7bb8c-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-536">Automatically scaling compute nodes in an Azure Batch pool is the dynamic adjustment of processing power used by your application.</span></span> 

    <span data-ttu-id="7bb8c-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-537">The sample formula here achieves the following behavior: When the pool is initially created, it starts with 1 VM.</span></span> <span data-ttu-id="7bb8c-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-538">$PendingTasks metric defines the number of tasks in running + active (queued) state.</span></span>  <span data-ttu-id="7bb8c-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-539">The formula finds the average number of pending tasks in the last 180 seconds and sets TargetDedicated accordingly.</span></span> <span data-ttu-id="7bb8c-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-540">It ensures that TargetDedicated never goes beyond 25 VMs.</span></span> <span data-ttu-id="7bb8c-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-541">So, as new tasks are submitted, pool automatically grows and as tasks complete, VMs become free one by one and the autoscaling shrinks those VMs.</span></span> <span data-ttu-id="7bb8c-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-542">startingNumberOfVMs and maxNumberofVMs can be adjusted to your needs.</span></span>
 
    <span data-ttu-id="7bb8c-543">Autoscale formula:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-543">Autoscale formula:</span></span>

    ``` 
    startingNumberOfVMs = 1;
    maxNumberofVMs = 25;
    pendingTaskSamplePercent = $PendingTasks.GetSamplePercent(180 * TimeInterval_Second);
    pendingTaskSamples = pendingTaskSamplePercent < 70 ? startingNumberOfVMs : avg($PendingTasks.GetSample(180 * TimeInterval_Second));
    $TargetDedicated=min(maxNumberofVMs,pendingTaskSamples);
    ```

   <span data-ttu-id="7bb8c-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-544">See [Automatically scale compute nodes in an Azure Batch pool](../batch/batch-automatic-scaling.md) for details.</span></span>

   <span data-ttu-id="7bb8c-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-545">If the pool is using the default [autoScaleEvaluationInterval](https://msdn.microsoft.com/library/azure/dn820173.aspx), the Batch service could take 15-30 minutes to prepare the VM before running the custom activity.</span></span>  <span data-ttu-id="7bb8c-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-546">If the pool is using a different autoScaleEvaluationInterval, the Batch service could take autoScaleEvaluationInterval + 10 minutes.</span></span>
5. <span data-ttu-id="7bb8c-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-547">In the sample solution, the **Execute** method invokes the **Calculate** method that processes an input data slice to produce an output data slice.</span></span> <span data-ttu-id="7bb8c-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-548">You can write your own method to process input data and replace the Calculate method call in the Execute method with a call to your method.</span></span>

### <a name="next-steps-consume-the-data"></a><span data-ttu-id="7bb8c-549">Next steps: Consume the data</span><span class="sxs-lookup"><span data-stu-id="7bb8c-549">Next steps: Consume the data</span></span>
<span data-ttu-id="7bb8c-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span><span class="sxs-lookup"><span data-stu-id="7bb8c-550">After you process data, you can consume it with online tools like **Microsoft Power BI**.</span></span> <span data-ttu-id="7bb8c-551">Here are links to help you understand Power BI and how to use it in Azure:</span><span class="sxs-lookup"><span data-stu-id="7bb8c-551">Here are links to help you understand Power BI and how to use it in Azure:</span></span>

* [<span data-ttu-id="7bb8c-552">Explore a dataset in Power BI</span><span class="sxs-lookup"><span data-stu-id="7bb8c-552">Explore a dataset in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-service-get-data/)
* [<span data-ttu-id="7bb8c-553">Getting started with the Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="7bb8c-553">Getting started with the Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-getting-started/)
* [<span data-ttu-id="7bb8c-554">Refresh data in Power BI</span><span class="sxs-lookup"><span data-stu-id="7bb8c-554">Refresh data in Power BI</span></span>](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/)
* [<span data-ttu-id="7bb8c-555">Azure and Power BI - basic overview</span><span class="sxs-lookup"><span data-stu-id="7bb8c-555">Azure and Power BI - basic overview</span></span>](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

## <a name="references"></a><span data-ttu-id="7bb8c-556">References</span><span class="sxs-lookup"><span data-stu-id="7bb8c-556">References</span></span>
* [<span data-ttu-id="7bb8c-557">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7bb8c-557">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

  * [<span data-ttu-id="7bb8c-558">Introduction to Azure Data Factory service</span><span class="sxs-lookup"><span data-stu-id="7bb8c-558">Introduction to Azure Data Factory service</span></span>](data-factory-introduction.md)
  * [<span data-ttu-id="7bb8c-559">Get started with Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="7bb8c-559">Get started with Azure Data Factory</span></span>](data-factory-build-your-first-pipeline.md)
  * [<span data-ttu-id="7bb8c-560">Use custom activities in an Azure Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="7bb8c-560">Use custom activities in an Azure Data Factory pipeline</span></span>](data-factory-use-custom-activities.md)
* [<span data-ttu-id="7bb8c-561">Azure Batch</span><span class="sxs-lookup"><span data-stu-id="7bb8c-561">Azure Batch</span></span>](https://azure.microsoft.com/documentation/services/batch/)

  * [<span data-ttu-id="7bb8c-562">Basics of Azure Batch</span><span class="sxs-lookup"><span data-stu-id="7bb8c-562">Basics of Azure Batch</span></span>](../batch/batch-technical-overview.md)
  * [<span data-ttu-id="7bb8c-563">Overview of Azure Batch features</span><span class="sxs-lookup"><span data-stu-id="7bb8c-563">Overview of Azure Batch features</span></span>](../batch/batch-api-basics.md)
  * [<span data-ttu-id="7bb8c-564">Create and manage Azure Batch account in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7bb8c-564">Create and manage Azure Batch account in the Azure portal</span></span>](../batch/batch-account-create-portal.md)
  * [<span data-ttu-id="7bb8c-565">Get started with Azure Batch Library .NET</span><span class="sxs-lookup"><span data-stu-id="7bb8c-565">Get started with Azure Batch Library .NET</span></span>](../batch/batch-dotnet-get-started.md)

[batch-explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch-explorer-walkthrough]: http://blogs.technet.com/b/windowshpc/archive/2015/01/20/azure-batch-explorer-sample-walkthrough.aspx






















