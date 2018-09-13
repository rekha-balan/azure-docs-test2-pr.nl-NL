---
title: Manage Azure Data Lake Analytics using Azure Command-line Interface
description: This article describes how to use the Azure CLI to manage Data Lake Analytics jobs, data sources, & users.
services: data-lake-analytics
author: jasonwhowell
ms.author: jasonh
ms.assetid: 4e5a3a0a-6d7f-43ed-aeb5-c3b3979a1e0a
ms.service: data-lake-analytics
ms.topic: conceptual
ms.date: 01/29/2018
ms.openlocfilehash: e265a46533264bbb1d437edbfe1bbfb3306614ad
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44773935"
---
# <a name="manage-azure-data-lake-analytics-using-the-azure-command-line-interface-cli"></a><span data-ttu-id="38b87-103">Manage Azure Data Lake Analytics using the Azure Command-line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="38b87-103">Manage Azure Data Lake Analytics using the Azure Command-line Interface (CLI)</span></span>

[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="38b87-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="38b87-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI.</span></span> <span data-ttu-id="38b87-105">To see management topics using other tools, click the tab select above.</span><span class="sxs-lookup"><span data-stu-id="38b87-105">To see management topics using other tools, click the tab select above.</span></span>


<span data-ttu-id="38b87-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="38b87-106">**Prerequisites**</span></span>

<span data-ttu-id="38b87-107">Before you begin this tutorial, you must have the following resources:</span><span class="sxs-lookup"><span data-stu-id="38b87-107">Before you begin this tutorial, you must have the following resources:</span></span>

* <span data-ttu-id="38b87-108">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="38b87-108">An Azure subscription.</span></span> <span data-ttu-id="38b87-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="38b87-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="38b87-110">Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="38b87-110">Azure CLI.</span></span> <span data-ttu-id="38b87-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="38b87-111">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).</span></span>

   * <span data-ttu-id="38b87-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span><span class="sxs-lookup"><span data-stu-id="38b87-112">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>

* <span data-ttu-id="38b87-113">Authenticate by using the `az login` command and select the subscription that you want to use.</span><span class="sxs-lookup"><span data-stu-id="38b87-113">Authenticate by using the `az login` command and select the subscription that you want to use.</span></span> <span data-ttu-id="38b87-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](/cli/azure/authenticate-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="38b87-114">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](/cli/azure/authenticate-azure-cli).</span></span>

   ```azurecli
   az login
   az account set --subscription <subscription id>
   ```

   <span data-ttu-id="38b87-115">You can now access the Data Lake Analytics and Data Lake Store commands.</span><span class="sxs-lookup"><span data-stu-id="38b87-115">You can now access the Data Lake Analytics and Data Lake Store commands.</span></span> <span data-ttu-id="38b87-116">Run the following command to list the Data Lake Store and Data Lake Analytics commands:</span><span class="sxs-lookup"><span data-stu-id="38b87-116">Run the following command to list the Data Lake Store and Data Lake Analytics commands:</span></span>

   ```azurecli
   az dls -h
   az dla -h
   ```

## <a name="manage-accounts"></a><span data-ttu-id="38b87-117">Manage accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-117">Manage accounts</span></span>

<span data-ttu-id="38b87-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="38b87-118">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="38b87-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span><span class="sxs-lookup"><span data-stu-id="38b87-119">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span> <span data-ttu-id="38b87-120">You only pay for the time when it is running a job.</span><span class="sxs-lookup"><span data-stu-id="38b87-120">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="38b87-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="38b87-121">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="38b87-122">Create accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-122">Create accounts</span></span>

<span data-ttu-id="38b87-123">Run the following command to create a Data Lake account,</span><span class="sxs-lookup"><span data-stu-id="38b87-123">Run the following command to create a Data Lake account,</span></span> 

   ```azurecli
   az dla account create --account "<Data Lake Analytics account name>" --location "<Location Name>" --resource-group "<Resource Group Name>" --default-data-lake-store "<Data Lake Store account name>"
   ```

### <a name="update-accounts"></a><span data-ttu-id="38b87-124">Update accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-124">Update accounts</span></span>

<span data-ttu-id="38b87-125">The following command updates the properties of an existing Data Lake Analytics Account</span><span class="sxs-lookup"><span data-stu-id="38b87-125">The following command updates the properties of an existing Data Lake Analytics Account</span></span>

   ```azurecli
   az dla account update --account "<Data Lake Analytics Account Name>" --firewall-state "Enabled" --query-store-retention 7
   ```

### <a name="list-accounts"></a><span data-ttu-id="38b87-126">List accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-126">List accounts</span></span>

<span data-ttu-id="38b87-127">List Data Lake Analytics accounts within a specific resource group</span><span class="sxs-lookup"><span data-stu-id="38b87-127">List Data Lake Analytics accounts within a specific resource group</span></span>

   ```azurecli
   az dla account list "<Resource group name>"
   ```

## <a name="get-details-of-an-account"></a><span data-ttu-id="38b87-128">Get details of an account</span><span class="sxs-lookup"><span data-stu-id="38b87-128">Get details of an account</span></span>

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

### <a name="delete-an-account"></a><span data-ttu-id="38b87-129">Delete an account</span><span class="sxs-lookup"><span data-stu-id="38b87-129">Delete an account</span></span>

   ```azurecli
   az dla account delete --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

## <a name="manage-data-sources"></a><span data-ttu-id="38b87-130">Manage data sources</span><span class="sxs-lookup"><span data-stu-id="38b87-130">Manage data sources</span></span>

<span data-ttu-id="38b87-131">Data Lake Analytics currently supports the following two data sources:</span><span class="sxs-lookup"><span data-stu-id="38b87-131">Data Lake Analytics currently supports the following two data sources:</span></span>

* [<span data-ttu-id="38b87-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="38b87-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="38b87-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="38b87-133">Azure Storage</span></span>](../storage/common/storage-introduction.md)

<span data-ttu-id="38b87-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span><span class="sxs-lookup"><span data-stu-id="38b87-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="38b87-135">The default Data Lake storage account is used to store job metadata and job audit logs.</span><span class="sxs-lookup"><span data-stu-id="38b87-135">The default Data Lake storage account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="38b87-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="38b87-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="38b87-137">Find the default Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="38b87-137">Find the default Data Lake Store account</span></span>

<span data-ttu-id="38b87-138">You can view the default Data Lake Store account used by running the `az dla account show` command.</span><span class="sxs-lookup"><span data-stu-id="38b87-138">You can view the default Data Lake Store account used by running the `az dla account show` command.</span></span> <span data-ttu-id="38b87-139">Default account name is listed under the defaultDataLakeStoreAccount property.</span><span class="sxs-lookup"><span data-stu-id="38b87-139">Default account name is listed under the defaultDataLakeStoreAccount property.</span></span>

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>"
   ```

### <a name="add-additional-blob-storage-accounts"></a><span data-ttu-id="38b87-140">Add additional Blob storage accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-140">Add additional Blob storage accounts</span></span>

   ```azurecli
   az dla account blob-storage add --access-key "<Azure Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Storage account name>"
   ```

> [!NOTE]
> <span data-ttu-id="38b87-141">Only Blob storage short names are supported.</span><span class="sxs-lookup"><span data-stu-id="38b87-141">Only Blob storage short names are supported.</span></span> <span data-ttu-id="38b87-142">Don't use FQDN, for example "myblob.blob.core.windows.net".</span><span class="sxs-lookup"><span data-stu-id="38b87-142">Don't use FQDN, for example "myblob.blob.core.windows.net".</span></span>
> 

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="38b87-143">Add additional Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="38b87-143">Add additional Data Lake Store accounts</span></span>

<span data-ttu-id="38b87-144">The following command updates the specified Data Lake Analytics account with an additional Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="38b87-144">The following command updates the specified Data Lake Analytics account with an additional Data Lake Store account:</span></span>

   ```azurecli
   az dla account data-lake-store add --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Data Lake Store account name>"
   ```

### <a name="update-existing-data-source"></a><span data-ttu-id="38b87-145">Update existing data source</span><span class="sxs-lookup"><span data-stu-id="38b87-145">Update existing data source</span></span>

<span data-ttu-id="38b87-146">To update an existing Blob storage account key:</span><span class="sxs-lookup"><span data-stu-id="38b87-146">To update an existing Blob storage account key:</span></span>

   ```azurecli
   az dla account blob-storage update --access-key "<New Blob Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

### <a name="list-data-sources"></a><span data-ttu-id="38b87-147">List data sources:</span><span class="sxs-lookup"><span data-stu-id="38b87-147">List data sources:</span></span>

<span data-ttu-id="38b87-148">To list the Data Lake Store accounts:</span><span class="sxs-lookup"><span data-stu-id="38b87-148">To list the Data Lake Store accounts:</span></span>

   ```azurecli
   az dla account data-lake-store list --account "<Data Lake Analytics account name>"
   ```

<span data-ttu-id="38b87-149">To list the Blob storage account:</span><span class="sxs-lookup"><span data-stu-id="38b87-149">To list the Blob storage account:</span></span>

   ```azurecli
   az dla account blob-storage list --account "<Data Lake Analytics account name>"
   ```

![Data Lake Analytics list data source](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a><span data-ttu-id="38b87-151">Delete data sources:</span><span class="sxs-lookup"><span data-stu-id="38b87-151">Delete data sources:</span></span>
<span data-ttu-id="38b87-152">To delete a Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="38b87-152">To delete a Data Lake Store account:</span></span>

   ```azurecli
   az dla account data-lake-store delete --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Azure Data Lake Store account name>"
   ```

<span data-ttu-id="38b87-153">To delete a Blob storage account:</span><span class="sxs-lookup"><span data-stu-id="38b87-153">To delete a Blob storage account:</span></span>

   ```azurecli
   az dla account blob-storage delete --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

## <a name="manage-jobs"></a><span data-ttu-id="38b87-154">Manage jobs</span><span class="sxs-lookup"><span data-stu-id="38b87-154">Manage jobs</span></span>
<span data-ttu-id="38b87-155">You must have a Data Lake Analytics account before you can create a job.</span><span class="sxs-lookup"><span data-stu-id="38b87-155">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="38b87-156">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span><span class="sxs-lookup"><span data-stu-id="38b87-156">For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="38b87-157">List jobs</span><span class="sxs-lookup"><span data-stu-id="38b87-157">List jobs</span></span>

   ```azurecli
   az dla job list --account "<Data Lake Analytics account name>"
   ```

   ![Data Lake Analytics list data source](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a><span data-ttu-id="38b87-159">Get job details</span><span class="sxs-lookup"><span data-stu-id="38b87-159">Get job details</span></span>

   ```azurecli
   az dla job show --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

### <a name="submit-jobs"></a><span data-ttu-id="38b87-160">Submit jobs</span><span class="sxs-lookup"><span data-stu-id="38b87-160">Submit jobs</span></span>

> [!NOTE]
> <span data-ttu-id="38b87-161">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span><span class="sxs-lookup"><span data-stu-id="38b87-161">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
   ```azurecli
   az dla job submit --account "<Data Lake Analytics account name>" --job-name "<Name of your job>" --script "<Script to submit>"
   ```

### <a name="cancel-jobs"></a><span data-ttu-id="38b87-162">Cancel jobs</span><span class="sxs-lookup"><span data-stu-id="38b87-162">Cancel jobs</span></span>
<span data-ttu-id="38b87-163">Use the list command to find the job id, and then use cancel to cancel the job.</span><span class="sxs-lookup"><span data-stu-id="38b87-163">Use the list command to find the job id, and then use cancel to cancel the job.</span></span>

   ```azurecli
   az dla job cancel --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

## <a name="pipelines-and-recurrences"></a><span data-ttu-id="38b87-164">Pipelines and recurrences</span><span class="sxs-lookup"><span data-stu-id="38b87-164">Pipelines and recurrences</span></span>

<span data-ttu-id="38b87-165">**Get information about pipelines and recurrences**</span><span class="sxs-lookup"><span data-stu-id="38b87-165">**Get information about pipelines and recurrences**</span></span>

<span data-ttu-id="38b87-166">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span><span class="sxs-lookup"><span data-stu-id="38b87-166">Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.</span></span>

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

<span data-ttu-id="38b87-167">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span><span class="sxs-lookup"><span data-stu-id="38b87-167">Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.</span></span>

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="see-also"></a><span data-ttu-id="38b87-168">See also</span><span class="sxs-lookup"><span data-stu-id="38b87-168">See also</span></span>
* [<span data-ttu-id="38b87-169">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="38b87-169">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="38b87-170">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="38b87-170">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="38b87-171">Manage Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="38b87-171">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="38b87-172">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="38b87-172">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

