---
title: Manage Azure Data Lake Analytics using Azure Command-line Interface | Microsoft Docs
description: Learn how to manage Data Lake Analytics accounts, data sources, jobs and users using Azure CLI
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 5fd7d8e851662c62b8dc27e5aeeb039b397228cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661902"
---
# <a name="manage-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="f88b4-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="f88b4-103">Manage Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="f88b4-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure.</span><span class="sxs-lookup"><span data-stu-id="f88b4-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure.</span></span> <span data-ttu-id="f88b4-105">To see management topic using other tools, click the tab select above.</span><span class="sxs-lookup"><span data-stu-id="f88b4-105">To see management topic using other tools, click the tab select above.</span></span>

<span data-ttu-id="f88b4-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="f88b4-106">**Prerequisites**</span></span>

<span data-ttu-id="f88b4-107">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="f88b4-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="f88b4-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f88b4-108">**An Azure subscription**.</span></span> <span data-ttu-id="f88b4-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f88b4-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f88b4-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="f88b4-110">**Azure CLI**.</span></span> <span data-ttu-id="f88b4-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="f88b4-111">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="f88b4-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span><span class="sxs-lookup"><span data-stu-id="f88b4-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="f88b4-113">**Authentication**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="f88b4-113">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="f88b4-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="f88b4-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="f88b4-115">**Switch to the Azure Resource Manager mode**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="f88b4-115">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

<span data-ttu-id="f88b4-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span><span class="sxs-lookup"><span data-stu-id="f88b4-116">**To list the Data Lake Store and Data Lake Analytics commands:**</span></span>

    azure datalake store
    azure datalake analytics

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="f88b4-117">Manage accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-117">Manage accounts</span></span>
<span data-ttu-id="f88b4-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="f88b4-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="f88b4-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span><span class="sxs-lookup"><span data-stu-id="f88b4-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="f88b4-120">You only pay for the time when it is running a job.</span><span class="sxs-lookup"><span data-stu-id="f88b4-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="f88b4-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f88b4-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="f88b4-122">Create accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-122">Create accounts</span></span>
      azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"


### <a name="update-accounts"></a><span data-ttu-id="f88b4-123">Update accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-123">Update accounts</span></span>
<span data-ttu-id="f88b4-124">The following command updates the properties of an existing Data Lake Analytics Account</span><span class="sxs-lookup"><span data-stu-id="f88b4-124">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

    azure datalake analytics account set "<Data Lake Analytics Account Name>"


### <a name="list-accounts"></a><span data-ttu-id="f88b4-125">List accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-125">List accounts</span></span>
<span data-ttu-id="f88b4-126">List Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-126">List Data Lake Analytics accounts</span></span> 

    azure datalake analytics account list

<span data-ttu-id="f88b4-127">List Data Lake Analytics accounts within a specific resource group</span><span class="sxs-lookup"><span data-stu-id="f88b4-127">List Data Lake Analytics accounts within a specific resource group</span></span>

    azure datalake analytics account list -g "<Azure Resource Group Name>"

<span data-ttu-id="f88b4-128">Get details of a specific Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="f88b4-128">Get details of a specific Data Lake Analytics account</span></span>

    azure datalake analytics account show -g "<Azure Resource Group Name>" -n "<Data Lake Analytics Account Name>"

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="f88b4-129">Delete Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-129">Delete Data Lake Analytics accounts</span></span>
      azure datalake analytics account delete "<Data Lake Analytics Account Name>"


<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="f88b4-130">Manage account data sources</span><span class="sxs-lookup"><span data-stu-id="f88b4-130">Manage account data sources</span></span>
<span data-ttu-id="f88b4-131">Data Lake Analytics currently supports the following data sources:</span><span class="sxs-lookup"><span data-stu-id="f88b4-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="f88b4-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f88b4-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="f88b4-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="f88b4-133">Azure Storage</span></span>](../storage/storage-introduction.md)

<span data-ttu-id="f88b4-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span><span class="sxs-lookup"><span data-stu-id="f88b4-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="f88b4-135">The default ADL storage account is used to store job metadata and job audit logs.</span><span class="sxs-lookup"><span data-stu-id="f88b4-135">The default ADL storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="f88b4-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="f88b4-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-adl-storage-account"></a><span data-ttu-id="f88b4-137">Find the default ADL storage account</span><span class="sxs-lookup"><span data-stu-id="f88b4-137">Find the default ADL storage account</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

<span data-ttu-id="f88b4-138">The value is listed under properties:datalakeStoreAccount:name.</span><span class="sxs-lookup"><span data-stu-id="f88b4-138">The value is listed under properties:datalakeStoreAccount:name.</span></span>

### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="f88b4-139">Add additional Azure Blob storage accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-139">Add additional Azure Blob storage accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -b "<Azure Blob Storage Account Short Name>" -k "<Azure Storage Account Key>"

> [!NOTE]
> <span data-ttu-id="f88b4-140">Only Blob storage short names are supported.</span><span class="sxs-lookup"><span data-stu-id="f88b4-140">Only Blob storage short names are supported.</span></span>  <span data-ttu-id="f88b4-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="f88b4-141">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="f88b4-142">Add additional Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-142">Add additional Data Lake Store accounts</span></span>
      azure datalake analytics account datasource add -n "<Data Lake Analytics Account Name>" -l "<Data Lake Store Account Name>" [-d]

<span data-ttu-id="f88b4-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span><span class="sxs-lookup"><span data-stu-id="f88b4-143">[-d] is an optional switch to indicate whether the Data Lake being added is the default Data Lake account.</span></span> 

### <a name="update-existing-data-source"></a><span data-ttu-id="f88b4-144">Update existing data source</span><span class="sxs-lookup"><span data-stu-id="f88b4-144">Update existing data source</span></span>
<span data-ttu-id="f88b4-145">To set an existing Data Lake Store account to be the default:</span><span class="sxs-lookup"><span data-stu-id="f88b4-145">To set an existing Data Lake Store account to be the default:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -l "<Azure Data Lake Store Account Name>" -d

<span data-ttu-id="f88b4-146">To update an existing Blob storage account key:</span><span class="sxs-lookup"><span data-stu-id="f88b4-146">To update an existing Blob storage account key:</span></span>

      azure datalake analytics account datasource set -n "<Data Lake Analytics Account Name>" -b "<Blob Storage Account Name>" -k "<New Blob Storage Account Key>"

### <a name="list-data-sources"></a><span data-ttu-id="f88b4-147">List data sources:</span><span class="sxs-lookup"><span data-stu-id="f88b4-147">List data sources:</span></span>
    azure datalake analytics account show "<Data Lake Analytics Account Name>"

![Data Lake Analytics list data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="f88b4-149">Delete data sources:</span><span class="sxs-lookup"><span data-stu-id="f88b4-149">Delete data sources:</span></span>
<span data-ttu-id="f88b4-150">To delete a Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="f88b4-150">To delete a Data Lake Store account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Azure Data Lake Store Account Name>"

<span data-ttu-id="f88b4-151">To delete a Blob storage account:</span><span class="sxs-lookup"><span data-stu-id="f88b4-151">To delete a Blob storage account:</span></span>

      azure datalake analytics account datasource delete "<Data Lake Analytics Account Name>" "<Blob Storage Account Name>"

## <a name="manage-jobs"></a><span data-ttu-id="f88b4-152">Manage jobs</span><span class="sxs-lookup"><span data-stu-id="f88b4-152">Manage jobs</span></span>
<span data-ttu-id="f88b4-153">You must have a Data Lake Analytics account before you can create a job.</span><span class="sxs-lookup"><span data-stu-id="f88b4-153">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="f88b4-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="f88b4-154">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="f88b4-155">List jobs</span><span class="sxs-lookup"><span data-stu-id="f88b4-155">List jobs</span></span>
      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"

![Data Lake Analytics list data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="f88b4-157">Get job details</span><span class="sxs-lookup"><span data-stu-id="f88b4-157">Get job details</span></span>
      azure datalake analytics job show -n "<Data Lake Analytics Account Name>" -j "<Job ID>"

### <a name="submit-jobs"></a><span data-ttu-id="f88b4-158">Submit jobs</span><span class="sxs-lookup"><span data-stu-id="f88b4-158">Submit jobs</span></span>
> [!NOTE]
> <span data-ttu-id="f88b4-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span><span class="sxs-lookup"><span data-stu-id="f88b4-159">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"

### <a name="cancel-jobs"></a><span data-ttu-id="f88b4-160">Cancel jobs</span><span class="sxs-lookup"><span data-stu-id="f88b4-160">Cancel jobs</span></span>
<span data-ttu-id="f88b4-161">Use the list command to find the job id, and then use cancel to cancel the job.</span><span class="sxs-lookup"><span data-stu-id="f88b4-161">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

      azure datalake analytics job list -n "<Data Lake Analytics Account Name>"
      azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job ID>"

## <a name="manage-catalog"></a><span data-ttu-id="f88b4-162">Manage catalog</span><span class="sxs-lookup"><span data-stu-id="f88b4-162">Manage catalog</span></span>
<span data-ttu-id="f88b4-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="f88b4-163">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="f88b4-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f88b4-164">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="f88b4-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="f88b4-165">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="f88b4-166">List catalog items</span><span class="sxs-lookup"><span data-stu-id="f88b4-166">List catalog items</span></span>
    #List databases
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t database

    #List tables
    azure datalake analytics catalog list -n "<Data Lake Analytics Account Name>" -t table

<span data-ttu-id="f88b4-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span><span class="sxs-lookup"><span data-stu-id="f88b4-167">The types include database, schema, assembly, external data source, table, table valued function or table statistics.</span></span>

### <a name="create-catalog-secret"></a><span data-ttu-id="f88b4-168">Create catalog secret</span><span class="sxs-lookup"><span data-stu-id="f88b4-168">Create catalog secret</span></span>
    azure datalake analytics catalog secret create -n "<Data Lake Analytics Account Name>" <databaseName> <hostUri> <secretName>

### <a name="modify-catalog-secret"></a><span data-ttu-id="f88b4-169">Modify catalog secret</span><span class="sxs-lookup"><span data-stu-id="f88b4-169">Modify catalog secret</span></span>
      azure datalake analytics catalog secret set -n "<Data Lake Analytics Account Name>" <databaseName> <hostUri> <secretName>

### <a name="delete-catalog-secret"></a><span data-ttu-id="f88b4-170">Delete catalog secret</span><span class="sxs-lookup"><span data-stu-id="f88b4-170">Delete catalog secret</span></span>
    azure datalake analytics catalog secrete delete -n "<Data Lake Analytics Account Name>" <databaseName> <hostUri> <secretName>

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-arm-groups"></a><span data-ttu-id="f88b4-171">Use ARM groups</span><span class="sxs-lookup"><span data-stu-id="f88b4-171">Use ARM groups</span></span>
<span data-ttu-id="f88b4-172">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span><span class="sxs-lookup"><span data-stu-id="f88b4-172">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="f88b4-173">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="f88b4-173">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="f88b4-174">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="f88b4-174">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="f88b4-175">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span><span class="sxs-lookup"><span data-stu-id="f88b4-175">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="f88b4-176">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span><span class="sxs-lookup"><span data-stu-id="f88b4-176">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="f88b4-177">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f88b4-177">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="f88b4-178">A Data Lake Analytics service can include the following components:</span><span class="sxs-lookup"><span data-stu-id="f88b4-178">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="f88b4-179">Azure Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="f88b4-179">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="f88b4-180">Required default Azure Data Lake Storage account</span><span class="sxs-lookup"><span data-stu-id="f88b4-180">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="f88b4-181">Additional Azure Data Lake Storage accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-181">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="f88b4-182">Additional Azure Storage accounts</span><span class="sxs-lookup"><span data-stu-id="f88b4-182">Additional Azure Storage accounts</span></span>

<span data-ttu-id="f88b4-183">You can create all these components under one ARM group to make them easier to manage.</span><span class="sxs-lookup"><span data-stu-id="f88b4-183">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Azure Data Lake Analytics account and storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="f88b4-185">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="f88b4-185">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="f88b4-186">The ARM group however can be located in a different data center.</span><span class="sxs-lookup"><span data-stu-id="f88b4-186">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="f88b4-187">See also</span><span class="sxs-lookup"><span data-stu-id="f88b4-187">See also</span></span>
* [<span data-ttu-id="f88b4-188">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="f88b4-188">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="f88b4-189">Get started with Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f88b4-189">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f88b4-190">Manage Azure Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f88b4-190">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="f88b4-191">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="f88b4-191">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)




