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
# <a name="manage-azure-data-lake-analytics-using-the-azure-command-line-interface-cli"></a>Manage Azure Data Lake Analytics using the Azure Command-line Interface (CLI)

[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure CLI. To see management topics using other tools, click the tab select above.


**Prerequisites**

Before you begin this tutorial, you must have the following resources:

* An Azure subscription. See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).

* Azure CLI. See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

   * Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.

* Authenticate by using the `az login` command and select the subscription that you want to use. For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](/cli/azure/authenticate-azure-cli).

   ```azurecli
   az login
   az account set --subscription <subscription id>
   ```

   You can now access the Data Lake Analytics and Data Lake Store commands. Run the following command to list the Data Lake Store and Data Lake Analytics commands:

   ```azurecli
   az dls -h
   az dla -h
   ```

## <a name="manage-accounts"></a>Manage accounts

Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account. Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job. You only pay for the time when it is running a job.  For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).  

### <a name="create-accounts"></a>Create accounts

Run the following command to create a Data Lake account, 

   ```azurecli
   az dla account create --account "<Data Lake Analytics account name>" --location "<Location Name>" --resource-group "<Resource Group Name>" --default-data-lake-store "<Data Lake Store account name>"
   ```

### <a name="update-accounts"></a>Update accounts

The following command updates the properties of an existing Data Lake Analytics Account

   ```azurecli
   az dla account update --account "<Data Lake Analytics Account Name>" --firewall-state "Enabled" --query-store-retention 7
   ```

### <a name="list-accounts"></a>List accounts

List Data Lake Analytics accounts within a specific resource group

   ```azurecli
   az dla account list "<Resource group name>"
   ```

## <a name="get-details-of-an-account"></a>Get details of an account

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

### <a name="delete-an-account"></a>Delete an account

   ```azurecli
   az dla account delete --account "<Data Lake Analytics account name>" --resource-group "<Resource group name>"
   ```

## <a name="manage-data-sources"></a>Manage data sources

Data Lake Analytics currently supports the following two data sources:

* [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md)
* [Azure Storage](../storage/common/storage-introduction.md)

When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account. The default Data Lake storage account is used to store job metadata and job audit logs. After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account. 

### <a name="find-the-default-data-lake-store-account"></a>Find the default Data Lake Store account

You can view the default Data Lake Store account used by running the `az dla account show` command. Default account name is listed under the defaultDataLakeStoreAccount property.

   ```azurecli
   az dla account show --account "<Data Lake Analytics account name>"
   ```

### <a name="add-additional-blob-storage-accounts"></a>Add additional Blob storage accounts

   ```azurecli
   az dla account blob-storage add --access-key "<Azure Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Storage account name>"
   ```

> [!NOTE]
> Only Blob storage short names are supported. Don't use FQDN, for example "myblob.blob.core.windows.net".
> 

### <a name="add-additional-data-lake-store-accounts"></a>Add additional Data Lake Store accounts

The following command updates the specified Data Lake Analytics account with an additional Data Lake Store account:

   ```azurecli
   az dla account data-lake-store add --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Data Lake Store account name>"
   ```

### <a name="update-existing-data-source"></a>Update existing data source

To update an existing Blob storage account key:

   ```azurecli
   az dla account blob-storage update --access-key "<New Blob Storage Account Key>" --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

### <a name="list-data-sources"></a>List data sources:

To list the Data Lake Store accounts:

   ```azurecli
   az dla account data-lake-store list --account "<Data Lake Analytics account name>"
   ```

To list the Blob storage account:

   ```azurecli
   az dla account blob-storage list --account "<Data Lake Analytics account name>"
   ```

![Data Lake Analytics list data source](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-data-source.png)

### <a name="delete-data-sources"></a>Delete data sources:
To delete a Data Lake Store account:

   ```azurecli
   az dla account data-lake-store delete --account "<Data Lake Analytics account name>" --data-lake-store-account-name "<Azure Data Lake Store account name>"
   ```

To delete a Blob storage account:

   ```azurecli
   az dla account blob-storage delete --account "<Data Lake Analytics account name>" --storage-account-name "<Data Lake Store account name>"
   ```

## <a name="manage-jobs"></a>Manage jobs
You must have a Data Lake Analytics account before you can create a job.  For more information, see [Manage Data Lake Analytics accounts](#manage-accounts).

### <a name="list-jobs"></a>List jobs

   ```azurecli
   az dla job list --account "<Data Lake Analytics account name>"
   ```

   ![Data Lake Analytics list data source](./media/data-lake-analytics-manage-use-cli/data-lake-analytics-list-jobs.png)

### <a name="get-job-details"></a>Get job details

   ```azurecli
   az dla job show --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

### <a name="submit-jobs"></a>Submit jobs

> [!NOTE]
> The default priority of a job is 1000, and the default degree of parallelism for a job is 1.
> 
   ```azurecli
   az dla job submit --account "<Data Lake Analytics account name>" --job-name "<Name of your job>" --script "<Script to submit>"
   ```

### <a name="cancel-jobs"></a>Cancel jobs
Use the list command to find the job id, and then use cancel to cancel the job.

   ```azurecli
   az dla job cancel --account "<Data Lake Analytics account name>" --job-identity "<Job Id>"
   ```

## <a name="pipelines-and-recurrences"></a>Pipelines and recurrences

**Get information about pipelines and recurrences**

Use the `az dla job pipeline` commands to see the pipeline information previously submitted jobs.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Use the `az dla job recurrence` commands to see the recurrence information for previously submitted jobs.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="see-also"></a>See also
* [Overview of Microsoft Azure Data Lake Analytics](data-lake-analytics-overview.md)
* [Get started with Data Lake Analytics using Azure portal](data-lake-analytics-get-started-portal.md)
* [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md)
* [Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

