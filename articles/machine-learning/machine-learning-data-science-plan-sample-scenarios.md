---
title: Identify advanced analytics scenarios for Azure Machine Learning | Microsoft Docs
description: Select the appropriate scenarios for doing advanced predictive analytics with the Team Data Science Process.
services: machine-learning
documentationcenter: ''
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 53aecc1e-5089-42cf-8d44-77678653f92d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 1e747668ccf5de17cd2320aa71d4a6272d4f63af
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550286"
---
# <a name="scenarios-for-advanced-analytics-in-azure-machine-learning"></a><span data-ttu-id="def59-103">Scenarios for advanced analytics in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="def59-103">Scenarios for advanced analytics in Azure Machine Learning</span></span>
<span data-ttu-id="def59-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span><span class="sxs-lookup"><span data-stu-id="def59-104">This article outlines the variety of sample data sources and target scenarios that can be handled by the [Team Data Science Process (TDSP)](data-science-process-overview.md).</span></span> <span data-ttu-id="def59-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span><span class="sxs-lookup"><span data-stu-id="def59-105">The TDSP provides a systematic approach for teams to collaborate on building intelligent applications.</span></span> <span data-ttu-id="def59-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span><span class="sxs-lookup"><span data-stu-id="def59-106">The scenarios presented here illustrate options available in the data processing workflow that depend on the data characteristics, source locations, and target repositories in Azure.</span></span>

<span data-ttu-id="def59-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span><span class="sxs-lookup"><span data-stu-id="def59-107">The **decision tree** for selecting the sample scenarios that is appropriate for your data and objective is presented in the last section.</span></span>

> [!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
> 
> 

<span data-ttu-id="def59-108">Each of the following sections presents a sample scenario.</span><span class="sxs-lookup"><span data-stu-id="def59-108">Each of the following sections presents a sample scenario.</span></span> <span data-ttu-id="def59-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span><span class="sxs-lookup"><span data-stu-id="def59-109">For each scenario, a possible data science or advanced analytics flow and supporting Azure resources are listed.</span></span>

> [!NOTE]
> <span data-ttu-id="def59-110">**For all of the following scenarios, you need to:**</span><span class="sxs-lookup"><span data-stu-id="def59-110">**For all of the following scenarios, you need to:**</span></span>
> <br/>
> 
> * [<span data-ttu-id="def59-111">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="def59-111">Create a storage account</span></span>](../storage/storage-create-storage-account.md)
>   <br/>
> * [<span data-ttu-id="def59-112">Create an Azure Machine Learning workspace</span><span class="sxs-lookup"><span data-stu-id="def59-112">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
> 
> 

## <a name="smalllocal"></a><span data-ttu-id="def59-113">Scenario \#1: Small to medium tabular dataset in a local files</span><span class="sxs-lookup"><span data-stu-id="def59-113">Scenario \#1: Small to medium tabular dataset in a local files</span></span>
![Small to medium local files][1]

#### <a name="additional-azure-resources-none"></a><span data-ttu-id="def59-115">Additional Azure resources: None</span><span class="sxs-lookup"><span data-stu-id="def59-115">Additional Azure resources: None</span></span>
1. <span data-ttu-id="def59-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-116">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
2. <span data-ttu-id="def59-117">Upload a dataset.</span><span class="sxs-lookup"><span data-stu-id="def59-117">Upload a dataset.</span></span>
3. <span data-ttu-id="def59-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span><span class="sxs-lookup"><span data-stu-id="def59-118">Build an Azure Machine Learning experiment flow starting with uploaded dataset(s).</span></span>

## <a name="smalllocalprocess"></a><span data-ttu-id="def59-119">Scenario \#2: Small to medium dataset of local files that require processing</span><span class="sxs-lookup"><span data-stu-id="def59-119">Scenario \#2: Small to medium dataset of local files that require processing</span></span>
![Small to medium local files with processing][2]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="def59-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-121">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-122">Create an Azure Virtual Machine running IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="def59-122">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="def59-123">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-123">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="def59-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-124">Pre-process and clean data in IPython Notebook, accessing data from Azure storage container.</span></span>
4. <span data-ttu-id="def59-125">Transform data to cleaned, tabular form.</span><span class="sxs-lookup"><span data-stu-id="def59-125">Transform data to cleaned, tabular form.</span></span>
5. <span data-ttu-id="def59-126">Save transformed data in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="def59-126">Save transformed data in Azure blobs.</span></span>
6. <span data-ttu-id="def59-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-127">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
7. <span data-ttu-id="def59-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-128">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
8. <span data-ttu-id="def59-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="def59-129">Build an Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="largelocal"></a><span data-ttu-id="def59-130">Scenario \#3: Large dataset of local files, targeting Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="def59-130">Scenario \#3: Large dataset of local files, targeting Azure Blobs</span></span>
![Large local files][3]

#### <a name="additional-azure-resources-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="def59-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-132">Additional Azure resources: Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-133">Create an Azure Virtual Machine running IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="def59-133">Create an Azure Virtual Machine running IPython Notebook.</span></span>
2. <span data-ttu-id="def59-134">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-134">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="def59-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="def59-135">Pre-process and clean data in IPython Notebook, accessing data from Azure blobs.</span></span>
4. <span data-ttu-id="def59-136">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="def59-136">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="def59-137">Explore data, and create features as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-137">Explore data, and create features as needed.</span></span>
6. <span data-ttu-id="def59-138">Extract a small-to-medium data sample.</span><span class="sxs-lookup"><span data-stu-id="def59-138">Extract a small-to-medium data sample.</span></span>
7. <span data-ttu-id="def59-139">Save the sampled data in Azure blobs.</span><span class="sxs-lookup"><span data-stu-id="def59-139">Save the sampled data in Azure blobs.</span></span>
8. <span data-ttu-id="def59-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-140">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="def59-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-141">Read the data from Azure blobs using the [Import Data][import-data] module.</span></span>
10. <span data-ttu-id="def59-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="def59-142">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="smalllocaltodb"></a><span data-ttu-id="def59-143">Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="def59-143">Scenario \#4: Small to medium dataset of local files, targeting SQL Server in an Azure Virtual Machine</span></span>
![Small to medium local files to SQL DB in Azure][4]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="def59-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-145">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="def59-146">Create an Azure Virtual Machine running SQL Server + IPython Notebook.</span></span>
2. <span data-ttu-id="def59-147">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-147">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="def59-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="def59-148">Pre-process and clean data in Azure storage container using IPython Notebook.</span></span>
4. <span data-ttu-id="def59-149">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="def59-149">Transform data to cleaned, tabular form, if needed.</span></span>
5. <span data-ttu-id="def59-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="def59-150">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
6. <span data-ttu-id="def59-151">Load data to SQL Server database running on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="def59-151">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="def59-152">Option \#1: Using SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="def59-152">Option \#1: Using SQL Server Management Studio.</span></span>
   
   * <span data-ttu-id="def59-153">Login to SQL Server VM</span><span class="sxs-lookup"><span data-stu-id="def59-153">Login to SQL Server VM</span></span>
   * <span data-ttu-id="def59-154">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="def59-154">Run SQL Server Management Studio.</span></span>
   * <span data-ttu-id="def59-155">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="def59-155">Create database and target tables.</span></span>
   * <span data-ttu-id="def59-156">Use one of the bulk import methods to load the data from VM-local files.</span><span class="sxs-lookup"><span data-stu-id="def59-156">Use one of the bulk import methods to load the data from VM-local files.</span></span>
   
   <span data-ttu-id="def59-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span><span class="sxs-lookup"><span data-stu-id="def59-157">Option \#2: Using IPython Notebook – not advisable for medium and larger datasets</span></span>
   
   <!-- -->    
   * <span data-ttu-id="def59-158">Use ODBC connection string to access SQL Server on VM.</span><span class="sxs-lookup"><span data-stu-id="def59-158">Use ODBC connection string to access SQL Server on VM.</span></span>
   * <span data-ttu-id="def59-159">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="def59-159">Create database and target tables.</span></span>
   * <span data-ttu-id="def59-160">Use one of the bulk import methods to load the data from VM-local files.</span><span class="sxs-lookup"><span data-stu-id="def59-160">Use one of the bulk import methods to load the data from VM-local files.</span></span>
7. <span data-ttu-id="def59-161">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-161">Explore data, create features as needed.</span></span> <span data-ttu-id="def59-162">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="def59-162">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="def59-163">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="def59-163">Only note the necessary query to create them.</span></span>
8. <span data-ttu-id="def59-164">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="def59-164">Decide on a data sample size, if needed and/or desired.</span></span>
9. <span data-ttu-id="def59-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-165">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
10. <span data-ttu-id="def59-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-166">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="def59-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="def59-167">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
11. <span data-ttu-id="def59-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span><span class="sxs-lookup"><span data-stu-id="def59-168">Build Azure Machine Learning experiment flow starting with ingested dataset(s).</span></span>

## <a name="largelocaltodb"></a><span data-ttu-id="def59-169">Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span><span class="sxs-lookup"><span data-stu-id="def59-169">Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM</span></span>
![Large local files to SQL DB in Azure][5]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="def59-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-171">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="def59-172">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="def59-173">Upload data to an Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-173">Upload data to an Azure storage container.</span></span>
3. <span data-ttu-id="def59-174">(Optional) Pre-process and clean data.</span><span class="sxs-lookup"><span data-stu-id="def59-174">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="def59-175">a.</span><span class="sxs-lookup"><span data-stu-id="def59-175">a.</span></span>  <span data-ttu-id="def59-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span><span class="sxs-lookup"><span data-stu-id="def59-176">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="def59-177">b.</span><span class="sxs-lookup"><span data-stu-id="def59-177">b.</span></span>  <span data-ttu-id="def59-178">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="def59-178">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="def59-179">c.</span><span class="sxs-lookup"><span data-stu-id="def59-179">c.</span></span>  <span data-ttu-id="def59-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="def59-180">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="def59-181">Load data to SQL Server database running on an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="def59-181">Load data to SQL Server database running on an Azure VM.</span></span>
   
   <span data-ttu-id="def59-182">a.</span><span class="sxs-lookup"><span data-stu-id="def59-182">a.</span></span>  <span data-ttu-id="def59-183">Login to SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="def59-183">Login to SQL Server VM.</span></span>
   
   <span data-ttu-id="def59-184">b.</span><span class="sxs-lookup"><span data-stu-id="def59-184">b.</span></span>  <span data-ttu-id="def59-185">If data not saved already, download data files from Azure</span><span class="sxs-lookup"><span data-stu-id="def59-185">If data not saved already, download data files from Azure</span></span>
   
       storage container to local-VM folder.
   
   <span data-ttu-id="def59-186">c.</span><span class="sxs-lookup"><span data-stu-id="def59-186">c.</span></span>  <span data-ttu-id="def59-187">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="def59-187">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="def59-188">d.</span><span class="sxs-lookup"><span data-stu-id="def59-188">d.</span></span>  <span data-ttu-id="def59-189">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="def59-189">Create database and target tables.</span></span>
   
   <span data-ttu-id="def59-190">e.</span><span class="sxs-lookup"><span data-stu-id="def59-190">e.</span></span>  <span data-ttu-id="def59-191">Use one of the bulk import methods to load the data.</span><span class="sxs-lookup"><span data-stu-id="def59-191">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="def59-192">f.</span><span class="sxs-lookup"><span data-stu-id="def59-192">f.</span></span>  <span data-ttu-id="def59-193">If table joins are required, create indexes to expedite joins.</span><span class="sxs-lookup"><span data-stu-id="def59-193">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="def59-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="def59-194">For faster loading of large data sizes, it is recommended that you create partitioned tables and bulk import the data in parallel.</span></span> <span data-ttu-id="def59-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="def59-195">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="def59-196">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-196">Explore data, create features as needed.</span></span> <span data-ttu-id="def59-197">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="def59-197">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="def59-198">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="def59-198">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="def59-199">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="def59-199">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="def59-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-200">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="def59-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-201">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="def59-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="def59-202">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="def59-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span><span class="sxs-lookup"><span data-stu-id="def59-203">Simple Azure Machine Learning experiment flow starting with uploaded dataset</span></span>

## <a name="largedbtodb"></a><span data-ttu-id="def59-204">Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="def59-204">Scenario \#6: Large dataset in a SQL Server database on-prem, targeting SQL Server in an Azure Virtual Machine</span></span>
![Large SQL DB on-prem to SQL DB in Azure][6]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="def59-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-206">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="def59-207">Create an Azure Virtual Machine running SQL Server and IPython Notebook server.</span></span>
2. <span data-ttu-id="def59-208">Use one of the data export methods to export the data from SQL Server to dump files.</span><span class="sxs-lookup"><span data-stu-id="def59-208">Use one of the data export methods to export the data from SQL Server to dump files.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="def59-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span><span class="sxs-lookup"><span data-stu-id="def59-209">If you decide to move all data from the on-prem database, an alternate (faster) method to move the full database to the SQL Server instance in Azure.</span></span> <span data-ttu-id="def59-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span><span class="sxs-lookup"><span data-stu-id="def59-210">Skip the steps to export data, create database, and load/import data to the target database and follow the alternate method.</span></span>
   > 
   > 
3. <span data-ttu-id="def59-211">Upload dump files to Azure storage container.</span><span class="sxs-lookup"><span data-stu-id="def59-211">Upload dump files to Azure storage container.</span></span>
4. <span data-ttu-id="def59-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span><span class="sxs-lookup"><span data-stu-id="def59-212">Load the data to a SQL Server database running on an Azure Virtual Machine.</span></span>
   
   <span data-ttu-id="def59-213">a.</span><span class="sxs-lookup"><span data-stu-id="def59-213">a.</span></span>  <span data-ttu-id="def59-214">Login to the SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="def59-214">Login to the SQL Server VM.</span></span>
   
   <span data-ttu-id="def59-215">b.</span><span class="sxs-lookup"><span data-stu-id="def59-215">b.</span></span>  <span data-ttu-id="def59-216">Download data files from an Azure storage container to the local-VM folder.</span><span class="sxs-lookup"><span data-stu-id="def59-216">Download data files from an Azure storage container to the local-VM folder.</span></span>
   
   <span data-ttu-id="def59-217">c.</span><span class="sxs-lookup"><span data-stu-id="def59-217">c.</span></span>  <span data-ttu-id="def59-218">Run SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="def59-218">Run SQL Server Management Studio.</span></span>
   
   <span data-ttu-id="def59-219">d.</span><span class="sxs-lookup"><span data-stu-id="def59-219">d.</span></span>  <span data-ttu-id="def59-220">Create database and target tables.</span><span class="sxs-lookup"><span data-stu-id="def59-220">Create database and target tables.</span></span>
   
   <span data-ttu-id="def59-221">e.</span><span class="sxs-lookup"><span data-stu-id="def59-221">e.</span></span>  <span data-ttu-id="def59-222">Use one of the bulk import methods to load the data.</span><span class="sxs-lookup"><span data-stu-id="def59-222">Use one of the bulk import methods to load the data.</span></span>
   
   <span data-ttu-id="def59-223">f.</span><span class="sxs-lookup"><span data-stu-id="def59-223">f.</span></span>  <span data-ttu-id="def59-224">If table joins are required, create indexes to expedite joins.</span><span class="sxs-lookup"><span data-stu-id="def59-224">If table joins are required, create indexes to expedite joins.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="def59-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span><span class="sxs-lookup"><span data-stu-id="def59-225">For faster loading of large data sizes, create partitioned tables and to bulk import the data in parallel.</span></span> <span data-ttu-id="def59-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="def59-226">For more information, see [Parallel Data Import to SQL Partitioned Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
   > 
   > 
5. <span data-ttu-id="def59-227">Explore data, create features as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-227">Explore data, create features as needed.</span></span> <span data-ttu-id="def59-228">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="def59-228">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="def59-229">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="def59-229">Only note the necessary query to create them.</span></span>
6. <span data-ttu-id="def59-230">Decide on a data sample size, if needed and/or desired.</span><span class="sxs-lookup"><span data-stu-id="def59-230">Decide on a data sample size, if needed and/or desired.</span></span>
7. <span data-ttu-id="def59-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-231">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
8. <span data-ttu-id="def59-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-232">Read the data directly from the SQL Server using the [Import Data][import-data] module.</span></span> <span data-ttu-id="def59-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="def59-233">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
9. <span data-ttu-id="def59-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span><span class="sxs-lookup"><span data-stu-id="def59-234">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

### <a name="alternate-method-to-copy-a-full-database-from-an-on-premises--sql-server-to-azure-sql-database"></a><span data-ttu-id="def59-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="def59-235">Alternate method to copy a full database from an on-premises  SQL Server to Azure SQL Database</span></span>
![Detach local DB and attach to SQL DB in Azure][7]

#### <a name="additional-azure-resources-azure-virtual-machine-sql-server--ipython-notebook-server"></a><span data-ttu-id="def59-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-237">Additional Azure resources: Azure Virtual Machine (SQL Server / IPython Notebook server)</span></span>
<span data-ttu-id="def59-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span><span class="sxs-lookup"><span data-stu-id="def59-238">To replicate the entire SQL Server database in your SQL Server VM, you should copy a database from one location/server to another, assuming that the database can be taken temporarily offline.</span></span> <span data-ttu-id="def59-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span><span class="sxs-lookup"><span data-stu-id="def59-239">You do this in the SQL Server Management Studio Object Explorer, or using the equivalent Transact-SQL commands.</span></span>

1. <span data-ttu-id="def59-240">Detach the database at the source location.</span><span class="sxs-lookup"><span data-stu-id="def59-240">Detach the database at the source location.</span></span> <span data-ttu-id="def59-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="def59-241">For more information, see [Detach a database](https://technet.microsoft.com/library/ms191491\(v=sql.110\).aspx).</span></span>
2. <span data-ttu-id="def59-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="def59-242">In Windows Explorer or Windows Command Prompt window, copy the detached database file or files and log file or files to the target location on the SQL Server VM in Azure.</span></span>
3. <span data-ttu-id="def59-243">Attach the copied files to the target SQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="def59-243">Attach the copied files to the target SQL Server instance.</span></span> <span data-ttu-id="def59-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="def59-244">For more information, see [Attach a Database](https://technet.microsoft.com/library/ms190209\(v=sql.110\).aspx).</span></span>

<span data-ttu-id="def59-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span><span class="sxs-lookup"><span data-stu-id="def59-245">[Move a Database Using Detach and Attach (Transact-SQL)](https://technet.microsoft.com/library/ms187858\(v=sql.110\).aspx)</span></span>

## <a name="largedbtohive"></a><span data-ttu-id="def59-246">Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span><span class="sxs-lookup"><span data-stu-id="def59-246">Scenario \#7: Big data in local files, target Hive database in Azure HDInsight Hadoop clusters</span></span>
![Big data in local target Hive][9]

#### <a name="additional-azure-resources-azure-hdinsight-hadoop-cluster-and-azure-virtual-machine-ipython-notebook-server"></a><span data-ttu-id="def59-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span><span class="sxs-lookup"><span data-stu-id="def59-248">Additional Azure resources: Azure HDInsight Hadoop Cluster and Azure Virtual Machine (IPython Notebook server)</span></span>
1. <span data-ttu-id="def59-249">Create an Azure Virtual Machine running IPython Notebook server.</span><span class="sxs-lookup"><span data-stu-id="def59-249">Create an Azure Virtual Machine running IPython Notebook server.</span></span>
2. <span data-ttu-id="def59-250">Create an Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="def59-250">Create an Azure HDInsight Hadoop cluster.</span></span>
3. <span data-ttu-id="def59-251">(Optional) Pre-process and clean data.</span><span class="sxs-lookup"><span data-stu-id="def59-251">(Optional) Pre-process and clean data.</span></span>
   
   <span data-ttu-id="def59-252">a.</span><span class="sxs-lookup"><span data-stu-id="def59-252">a.</span></span>  <span data-ttu-id="def59-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span><span class="sxs-lookup"><span data-stu-id="def59-253">Pre-process and clean data in IPython Notebook, accessing data from Azure</span></span>
   
       blobs.
   
   <span data-ttu-id="def59-254">b.</span><span class="sxs-lookup"><span data-stu-id="def59-254">b.</span></span>  <span data-ttu-id="def59-255">Transform data to cleaned, tabular form, if needed.</span><span class="sxs-lookup"><span data-stu-id="def59-255">Transform data to cleaned, tabular form, if needed.</span></span>
   
   <span data-ttu-id="def59-256">c.</span><span class="sxs-lookup"><span data-stu-id="def59-256">c.</span></span>  <span data-ttu-id="def59-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span><span class="sxs-lookup"><span data-stu-id="def59-257">Save data to VM-local files (IPython Notebook is running on VM, local drives refer to VM drives).</span></span>
4. <span data-ttu-id="def59-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span><span class="sxs-lookup"><span data-stu-id="def59-258">Upload data to the default container of the Hadoop cluster selected in the step 2.</span></span>
5. <span data-ttu-id="def59-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="def59-259">Load data to Hive database in Azure HDInsight Hadoop cluster.</span></span>
   
   <span data-ttu-id="def59-260">a.</span><span class="sxs-lookup"><span data-stu-id="def59-260">a.</span></span>  <span data-ttu-id="def59-261">Log in to the head node of the Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="def59-261">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="def59-262">b.</span><span class="sxs-lookup"><span data-stu-id="def59-262">b.</span></span>  <span data-ttu-id="def59-263">Open the Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="def59-263">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="def59-264">c.</span><span class="sxs-lookup"><span data-stu-id="def59-264">c.</span></span>  <span data-ttu-id="def59-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="def59-265">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="def59-266">d.</span><span class="sxs-lookup"><span data-stu-id="def59-266">d.</span></span>  <span data-ttu-id="def59-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span><span class="sxs-lookup"><span data-stu-id="def59-267">Run the Hive queries to create database and tables, and load data from blob storage to Hive tables.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="def59-268">If the data is big, users can create the Hive table with partitions.</span><span class="sxs-lookup"><span data-stu-id="def59-268">If the data is big, users can create the Hive table with partitions.</span></span> <span data-ttu-id="def59-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span><span class="sxs-lookup"><span data-stu-id="def59-269">Then, users can use a `for` loop in the Hadoop Command Line on the head node to load data into the Hive table partitioned by partition.</span></span>
   > 
   > 
6. <span data-ttu-id="def59-270">Explore data and create features as needed in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="def59-270">Explore data and create features as needed in Hadoop Command Line.</span></span> <span data-ttu-id="def59-271">Note that the features do not need to be materialized in the database tables.</span><span class="sxs-lookup"><span data-stu-id="def59-271">Note that the features do not need to be materialized in the database tables.</span></span> <span data-ttu-id="def59-272">Only note the necessary query to create them.</span><span class="sxs-lookup"><span data-stu-id="def59-272">Only note the necessary query to create them.</span></span>
   
   <span data-ttu-id="def59-273">a.</span><span class="sxs-lookup"><span data-stu-id="def59-273">a.</span></span>  <span data-ttu-id="def59-274">Log in to the head node of the Hadoop cluster</span><span class="sxs-lookup"><span data-stu-id="def59-274">Log in to the head node of the Hadoop cluster</span></span>
   
   <span data-ttu-id="def59-275">b.</span><span class="sxs-lookup"><span data-stu-id="def59-275">b.</span></span>  <span data-ttu-id="def59-276">Open the Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="def59-276">Open the Hadoop Command Line.</span></span>
   
   <span data-ttu-id="def59-277">c.</span><span class="sxs-lookup"><span data-stu-id="def59-277">c.</span></span>  <span data-ttu-id="def59-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span><span class="sxs-lookup"><span data-stu-id="def59-278">Enter the Hive root directory by command `cd %hive_home%\bin` in Hadoop Command Line.</span></span>
   
   <span data-ttu-id="def59-279">d.</span><span class="sxs-lookup"><span data-stu-id="def59-279">d.</span></span>  <span data-ttu-id="def59-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-280">Run the Hive queries in Hadoop Command Line on the head node of the Hadoop cluster to explore the data and create features as needed.</span></span>
7. <span data-ttu-id="def59-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="def59-281">If needed and/or desired, sample the data to fit in Azure Machine Learning Studio.</span></span>
8. <span data-ttu-id="def59-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span><span class="sxs-lookup"><span data-stu-id="def59-282">Sign in to the [Azure Machine Learning Studio](https://studio.azureml.net/).</span></span>
9. <span data-ttu-id="def59-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span><span class="sxs-lookup"><span data-stu-id="def59-283">Read the data directly from the `Hive Queries` using the [Import Data][import-data] module.</span></span> <span data-ttu-id="def59-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span><span class="sxs-lookup"><span data-stu-id="def59-284">Paste the necessary query which extracts fields, creates features, and samples data if needed directly in the [Import Data][import-data] query.</span></span>
10. <span data-ttu-id="def59-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span><span class="sxs-lookup"><span data-stu-id="def59-285">Simple Azure Machine Learning experiment flow starting with uploaded dataset.</span></span>

## <a name="decisiontree"></a><span data-ttu-id="def59-286">Decision tree for scenario selection</span><span class="sxs-lookup"><span data-stu-id="def59-286">Decision tree for scenario selection</span></span>
- - -
<span data-ttu-id="def59-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span><span class="sxs-lookup"><span data-stu-id="def59-287">The following diagram summarizes the scenarios described above and the Advanced Analytics Process and Technology choices made that take you to each of the itemized scenarios.</span></span> <span data-ttu-id="def59-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span><span class="sxs-lookup"><span data-stu-id="def59-288">Note that data processing, exploration, feature engineering, and sampling may take place in one or more method/environment -- at the source, intermediate, and/or target environments – and may proceed iteratively as needed.</span></span> <span data-ttu-id="def59-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span><span class="sxs-lookup"><span data-stu-id="def59-289">The diagram only serves as an illustration of some of possible flows and does not provide an exhaustive enumeration.</span></span>

![Sample DS process walkthrough scenarios][8]

### <a name="advanced-analytics-in-action-examples"></a><span data-ttu-id="def59-291">Advanced Analytics in action Examples</span><span class="sxs-lookup"><span data-stu-id="def59-291">Advanced Analytics in action Examples</span></span>
<span data-ttu-id="def59-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span><span class="sxs-lookup"><span data-stu-id="def59-292">For end-to-end Azure Machine Learning walkthroughs that employ the Advanced Analytics Process and Technology using public datasets, see:</span></span>

* <span data-ttu-id="def59-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="def59-293">[Team Data Science Process in action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>
* <span data-ttu-id="def59-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="def59-294">[Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md).</span></span>

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-small-in-aml.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-with-processing.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-large.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-db.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-large-to-db.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-db-to-db.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-attach-db.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-sample-scenarios.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-data-science-plan-sample-scenarios/dsp-plan-local-to-hive.png


<!-- Module References -->
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/









