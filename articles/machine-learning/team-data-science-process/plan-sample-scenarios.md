---
title: Identify advanced analytics scenarios for Azure Machine Learning | Microsoft Docs
description: Select the appropriate scenarios for doing advanced predictive analytics with the Team Data Science Process.
services: machine-learning
documentationcenter: ''
author: deguhath
manager: cgronlun
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.component: team-data-science-process
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2017
ms.author: deguhath
ms.openlocfilehash: bf5ee52c98c173dbdde0a00c5657b8694b363279
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969311"
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="48d55-103">Scenarios for advanced analytics in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="48d55-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="48d55-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](overview.md).</span><span class="sxs-lookup"><span data-stu-id="48d55-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](overview.md).</span></span> <span data-ttu-id="48d55-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="48d55-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="48d55-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span><span class="sxs-lookup"><span data-stu-id="48d55-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="48d55-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span><span class="sxs-lookup"><span data-stu-id="48d55-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="48d55-108">Each of the following sections presents a sample scenario.</span><span class="sxs-lookup"><span data-stu-id="48d55-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="48d55-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span><span class="sxs-lookup"><span data-stu-id="48d55-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="48d55-110">**For all of the following scenarios, you need to:**</span><span class="sxs-lookup"><span data-stu-id="48d55-110">**For all of the following scenarios, you need to:**</span></span>
> <br/>
> 
> * [<span data-ttu-id="48d55-111">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="48d55-111">Create a storage account</span></span>](../../storage/common/storage-quickstart-create-account.md)
>   <br/>
> * [<span data-ttu-id="48d55-112">Create an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="48d55-112">Create an Azure Machine Learning workspace</span></span>](../studio/create-workspace.md)
> 
> 

## <a name="smalllocal"></a><span data-ttu-id="48d55-113">Scenario \#1: Small to medium tabular dataset in a local files</span><span class="sxs-lookup"><span data-stu-id="48d55-113">Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Small to medium local files][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="48d55-115">Additional Azure resources: None</span><span class="sxs-lookup"><span data-stu-id="48d55-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="48d55-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-117">Upload a dataset.</span><span class="sxs-lookup"><span data-stu-id="48d55-117">Upload a dataset.</span></span>
1. <span data-ttu-id="48d55-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span><span class="sxs-lookup"><span data-stu-id="48d55-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <a name="smalllocalprocess"></a><span data-ttu-id="48d55-119">Scenario \#2: Small to medium dataset of local files that require processing</span><span class="sxs-lookup"><span data-stu-id="48d55-119">Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Small to medium local files with processing][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="48d55-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-122">Create an Azure Virtual Machine running IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="48d55-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
1. <span data-ttu-id="48d55-123">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-123">Upload data to an Azure storage container.</span></span>
1. <span data-ttu-id="48d55-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
1. <span data-ttu-id="48d55-125">Transform data to cleaned, tabular form.</span><span class="sxs-lookup"><span data-stu-id="48d55-125">Transform data to cleaned, tabular form.</span></span>
1. <span data-ttu-id="48d55-126">Save transformed data in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="48d55-126">Save transformed data in Azure blobs.</span></span>
1. <span data-ttu-id="48d55-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
1. <span data-ttu-id="48d55-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="48d55-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="largelocal"></a><span data-ttu-id="48d55-130">Scenario \#3: Large dataset of local files, targeting Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="48d55-130">Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Large local files][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="48d55-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-133">Create an Azure Virtual Machine running IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="48d55-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
1. <span data-ttu-id="48d55-134">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-134">Upload data to an Azure storage container.</span></span>
1. <span data-ttu-id="48d55-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="48d55-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
1. <span data-ttu-id="48d55-136">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-136">Transform data to cleaned, tabular form, if needed.</span></span>
1. <span data-ttu-id="48d55-137">Explore data, and create features as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-137">Explore data, and create features as needed.</span></span>
1. <span data-ttu-id="48d55-138">Extract a small-to-medium data sample.</span><span class="sxs-lookup"><span data-stu-id="48d55-138">Extract a small-to-medium data sample.</span></span>
1. <span data-ttu-id="48d55-139">Save the sampled data in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="48d55-139">Save the sampled data in Azure blobs.</span></span>
1. <span data-ttu-id="48d55-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
1. <span data-ttu-id="48d55-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="48d55-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="smalllocaltodb"></a><span data-ttu-id="48d55-143">Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="48d55-143">Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Small to medium local files to SQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="48d55-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="48d55-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
1. <span data-ttu-id="48d55-147">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-147">Upload data to an Azure storage container.</span></span>
1. <span data-ttu-id="48d55-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="48d55-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
1. <span data-ttu-id="48d55-149">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-149">Transform data to cleaned, tabular form, if needed.</span></span>
1. <span data-ttu-id="48d55-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="48d55-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
1. <span data-ttu-id="48d55-151">Load data to SQL Server database running on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="48d55-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="48d55-152">Option \#1: Using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="48d55-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="48d55-153">Login to SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="48d55-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="48d55-154">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="48d55-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="48d55-155">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-155">Create database and target tables.</span></span>
   * <span data-ttu-id="48d55-156">Use one of the bulk import methods to load the data from VM-local files.</span><span class="sxs-lookup"><span data-stu-id="48d55-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="48d55-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span><span class="sxs-lookup"><span data-stu-id="48d55-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="48d55-158">Use ODBC connection string to access SQL Server on VM.</span><span class="sxs-lookup"><span data-stu-id="48d55-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="48d55-159">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-159">Create database and target tables.</span></span>
   * <span data-ttu-id="48d55-160">Use one of the bulk import methods to load the data from VM-local files.</span><span class="sxs-lookup"><span data-stu-id="48d55-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
1. <span data-ttu-id="48d55-161">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-161">Explore data, create features as needed.</span></span> <span data-ttu-id="48d55-162">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="48d55-163">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="48d55-163">Only note the necessary query to create them.</span></span>
1. <span data-ttu-id="48d55-164">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="48d55-164">Decide on a data sample size, if needed and/or desired.</span></span>
1. <span data-ttu-id="48d55-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="48d55-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="48d55-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
1. <span data-ttu-id="48d55-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="48d55-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="largelocaltodb"></a><span data-ttu-id="48d55-169">Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span><span class="sxs-lookup"><span data-stu-id="48d55-169">Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Large local files to SQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="48d55-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="48d55-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
1. <span data-ttu-id="48d55-173">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-173">Upload data to an Azure storage container.</span></span>
1. <span data-ttu-id="48d55-174">(Optional) Pre-process and clean data.</span><span class="sxs-lookup"><span data-stu-id="48d55-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="48d55-175">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-175">a.</span></span>  <span data-ttu-id="48d55-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span><span class="sxs-lookup"><span data-stu-id="48d55-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="48d55-177">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-177">b.</span></span>  <span data-ttu-id="48d55-178">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="48d55-179">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-179">c.</span></span>  <span data-ttu-id="48d55-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="48d55-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
1. <span data-ttu-id="48d55-181">Load data to SQL Server database running on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="48d55-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="48d55-182">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-182">a.</span></span>  <span data-ttu-id="48d55-183">Login to SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="48d55-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="48d55-184">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-184">b.</span></span>  <span data-ttu-id="48d55-185">If data not saved already, download data files from Azure</span><span class="sxs-lookup"><span data-stu-id="48d55-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="48d55-186">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-186">c.</span></span>  <span data-ttu-id="48d55-187">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="48d55-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="48d55-188">d.</span><span class="sxs-lookup"><span data-stu-id="48d55-188">d.</span></span>  <span data-ttu-id="48d55-189">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="48d55-190">e.</span><span class="sxs-lookup"><span data-stu-id="48d55-190">e.</span></span>  <span data-ttu-id="48d55-191">Use one of the bulk import methods to load the data.</span><span class="sxs-lookup"><span data-stu-id="48d55-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="48d55-192">f.</span><span class="sxs-lookup"><span data-stu-id="48d55-192">f.</span></span>  <span data-ttu-id="48d55-193">If table joins are required, create indexes to expedite joins.</span><span class="sxs-lookup"><span data-stu-id="48d55-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="48d55-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="48d55-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="48d55-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="48d55-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
1. <span data-ttu-id="48d55-196">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-196">Explore data, create features as needed.</span></span> <span data-ttu-id="48d55-197">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="48d55-198">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="48d55-198">Only note the necessary query to create them.</span></span>
1. <span data-ttu-id="48d55-199">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="48d55-199">Decide on a data sample size, if needed and/or desired.</span></span>
1. <span data-ttu-id="48d55-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="48d55-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="48d55-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
1. <span data-ttu-id="48d55-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span><span class="sxs-lookup"><span data-stu-id="48d55-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <a name="largedbtodb"></a><span data-ttu-id="48d55-204">Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="48d55-204">Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Large SQL DB on-prem to SQL DB in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="48d55-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="48d55-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
1. <span data-ttu-id="48d55-208">Use one of the data export methods to export the data from SQL Server to dump files.</span><span class="sxs-lookup"><span data-stu-id="48d55-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="48d55-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span><span class="sxs-lookup"><span data-stu-id="48d55-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="48d55-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span><span class="sxs-lookup"><span data-stu-id="48d55-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
1. <span data-ttu-id="48d55-211">Upload dump files to Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="48d55-211">Upload dump files to Azure storage container.</span></span>
1. <span data-ttu-id="48d55-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="48d55-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="48d55-213">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-213">a.</span></span>  <span data-ttu-id="48d55-214">Login to the SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="48d55-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="48d55-215">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-215">b.</span></span>  <span data-ttu-id="48d55-216">Download data files from an Azure storage container to the local-VM folder.</span><span class="sxs-lookup"><span data-stu-id="48d55-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="48d55-217">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-217">c.</span></span>  <span data-ttu-id="48d55-218">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="48d55-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="48d55-219">d.</span><span class="sxs-lookup"><span data-stu-id="48d55-219">d.</span></span>  <span data-ttu-id="48d55-220">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="48d55-221">e.</span><span class="sxs-lookup"><span data-stu-id="48d55-221">e.</span></span>  <span data-ttu-id="48d55-222">Use one of the bulk import methods to load the data.</span><span class="sxs-lookup"><span data-stu-id="48d55-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="48d55-223">f.</span><span class="sxs-lookup"><span data-stu-id="48d55-223">f.</span></span>  <span data-ttu-id="48d55-224">If table joins are required, create indexes to expedite joins.</span><span class="sxs-lookup"><span data-stu-id="48d55-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="48d55-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="48d55-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="48d55-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="48d55-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
1. <span data-ttu-id="48d55-227">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-227">Explore data, create features as needed.</span></span> <span data-ttu-id="48d55-228">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="48d55-229">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="48d55-229">Only note the necessary query to create them.</span></span>
1. <span data-ttu-id="48d55-230">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="48d55-230">Decide on a data sample size, if needed and/or desired.</span></span>
1. <span data-ttu-id="48d55-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="48d55-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="48d55-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
1. <span data-ttu-id="48d55-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span><span class="sxs-lookup"><span data-stu-id="48d55-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="48d55-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="48d55-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Detach local DB and attach to SQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="48d55-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="48d55-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span><span class="sxs-lookup"><span data-stu-id="48d55-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="48d55-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span><span class="sxs-lookup"><span data-stu-id="48d55-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="48d55-240">Detach the database at the source location.</span><span class="sxs-lookup"><span data-stu-id="48d55-240">Detach the database at the source location.</span></span> <span data-ttu-id="48d55-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="48d55-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
1. <span data-ttu-id="48d55-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="48d55-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
1. <span data-ttu-id="48d55-243">Attach the copied files to the target SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="48d55-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="48d55-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="48d55-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="48d55-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="48d55-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <a name="largedbtohive"></a><span data-ttu-id="48d55-246">Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="48d55-246">Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big data in local target Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="48d55-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="48d55-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="48d55-249">Create an Azure Virtual Machine running IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="48d55-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
1. <span data-ttu-id="48d55-250">Create an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="48d55-250">Create an Azure HDInsight Hadoop cluster.</span></span>
1. <span data-ttu-id="48d55-251">(Optional) Pre-process and clean data.</span><span class="sxs-lookup"><span data-stu-id="48d55-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="48d55-252">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-252">a.</span></span>  <span data-ttu-id="48d55-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span><span class="sxs-lookup"><span data-stu-id="48d55-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="48d55-254">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-254">b.</span></span>  <span data-ttu-id="48d55-255">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="48d55-256">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-256">c.</span></span>  <span data-ttu-id="48d55-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="48d55-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
1. <span data-ttu-id="48d55-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span><span class="sxs-lookup"><span data-stu-id="48d55-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
1. <span data-ttu-id="48d55-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="48d55-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="48d55-260">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-260">a.</span></span>  <span data-ttu-id="48d55-261">Log in to the head node of the Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="48d55-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="48d55-262">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-262">b.</span></span>  <span data-ttu-id="48d55-263">Open the Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="48d55-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="48d55-264">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-264">c.</span></span>  <span data-ttu-id="48d55-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="48d55-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="48d55-266">d.</span><span class="sxs-lookup"><span data-stu-id="48d55-266">d.</span></span>  <span data-ttu-id="48d55-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="48d55-268">If the data is big, users can create the Hive table with partitions.</span><span class="sxs-lookup"><span data-stu-id="48d55-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="48d55-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span><span class="sxs-lookup"><span data-stu-id="48d55-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
1. <span data-ttu-id="48d55-270">Explore data and create features as needed in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="48d55-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="48d55-271">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="48d55-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="48d55-272">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="48d55-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="48d55-273">a.</span><span class="sxs-lookup"><span data-stu-id="48d55-273">a.</span></span>  <span data-ttu-id="48d55-274">Log in to the head node of the Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="48d55-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="48d55-275">b.</span><span class="sxs-lookup"><span data-stu-id="48d55-275">b.</span></span>  <span data-ttu-id="48d55-276">Open the Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="48d55-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="48d55-277">c.</span><span class="sxs-lookup"><span data-stu-id="48d55-277">c.</span></span>  <span data-ttu-id="48d55-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="48d55-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="48d55-279">d.</span><span class="sxs-lookup"><span data-stu-id="48d55-279">d.</span></span>  <span data-ttu-id="48d55-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
1. <span data-ttu-id="48d55-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="48d55-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
1. <span data-ttu-id="48d55-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="48d55-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
1. <span data-ttu-id="48d55-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="48d55-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="48d55-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="48d55-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
1. <span data-ttu-id="48d55-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span><span class="sxs-lookup"><span data-stu-id="48d55-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <a name="decisiontree"></a><span data-ttu-id="48d55-286">Decision tree for scenario selection</span><span class="sxs-lookup"><span data-stu-id="48d55-286">Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="48d55-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span><span class="sxs-lookup"><span data-stu-id="48d55-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="48d55-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span><span class="sxs-lookup"><span data-stu-id="48d55-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="48d55-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span><span class="sxs-lookup"><span data-stu-id="48d55-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Sample DS process walkthrough scenarios][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="48d55-291">Advanced Analytics in action Examples</span><span class="sxs-lookup"><span data-stu-id="48d55-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="48d55-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span><span class="sxs-lookup"><span data-stu-id="48d55-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="48d55-293">[Team Data Science Process in action: using SQL Server](sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="48d55-293">[Team Data Science Process in action: using SQL Server](sql-walkthrough.md).</span></span>
* <span data-ttu-id="48d55-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="48d55-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](hive-walkthrough.md).</span></span>

[1]: ./media/plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: ./media/plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: ./media/plan-sample-scenarios/dsp-plan-local-large.png
[4]: ./media/plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: ./media/plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: ./media/plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: ./media/plan-sample-scenarios/dsp-plan-attach-db.png
[8]: ./media/plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: ./media/plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
