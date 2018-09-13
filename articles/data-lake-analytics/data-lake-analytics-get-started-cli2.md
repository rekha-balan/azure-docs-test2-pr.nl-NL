---
title: Get started with Azure Data Lake Analytics using Azure CLI 2.0 | Microsoft Docs
description: 'Learn how to use the Azure Command-line Interface 2.0 to create a Data Lake Analytics account, create a Data Lake Analytics job using U-SQL, and submit the job. '
services: data-lake-analytics
documentationcenter: ''
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/06/2017
ms.author: jgao
ms.openlocfilehash: 109460cecc4e11c729203af97c9bf1c22b90e61a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564133"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-azure-cli-20-preview"></a><span data-ttu-id="04795-103">Tutorial: get started with Azure Data Lake Analytics using Azure CLI 2.0 (Preview)</span><span class="sxs-lookup"><span data-stu-id="04795-103">Tutorial: get started with Azure Data Lake Analytics using Azure CLI 2.0 (Preview)</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="04795-104">Learn how to use Azure CLI 2.0 to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="04795-104">Learn how to use Azure CLI 2.0 to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytics accounts.</span></span> <span data-ttu-id="04795-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04795-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="04795-106">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="04795-106">In this tutorial, you develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span></span> <span data-ttu-id="04795-107">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span><span class="sxs-lookup"><span data-stu-id="04795-107">To go through the same tutorial using other supported tools, use the dropdown list on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04795-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04795-108">Prerequisites</span></span>
<span data-ttu-id="04795-109">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="04795-109">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="04795-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="04795-110">**An Azure subscription**.</span></span> <span data-ttu-id="04795-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="04795-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="04795-112">**Azure CLI 2.0**.</span><span class="sxs-lookup"><span data-stu-id="04795-112">**Azure CLI 2.0**.</span></span> <span data-ttu-id="04795-113">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="04795-113">See [Install and configure Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="04795-114">**Enable Data Lake Store/Analytics CLI 2.0 Preview**.</span><span class="sxs-lookup"><span data-stu-id="04795-114">**Enable Data Lake Store/Analytics CLI 2.0 Preview**.</span></span> <span data-ttu-id="04795-115">Data Lake Store and Data Lake Analytics CLI 2.0 is still in Preview.</span><span class="sxs-lookup"><span data-stu-id="04795-115">Data Lake Store and Data Lake Analytics CLI 2.0 is still in Preview.</span></span> <span data-ttu-id="04795-116">Run the following commands to enable both:</span><span class="sxs-lookup"><span data-stu-id="04795-116">Run the following commands to enable both:</span></span>

    ```azurecli
    az component update --add dls
    az component update --add dla 
    ```

## <a name="log-in-to-azure"></a><span data-ttu-id="04795-117">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="04795-117">Log in to Azure</span></span>

<span data-ttu-id="04795-118">To log in to your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="04795-118">To log in to your Azure subscription:</span></span>

```azurecli
az login
```

<span data-ttu-id="04795-119">You are requested to browse to a URL, and enter an authentication code.</span><span class="sxs-lookup"><span data-stu-id="04795-119">You are requested to browse to a URL, and enter an authentication code.</span></span>  <span data-ttu-id="04795-120">And then follow the instructions to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="04795-120">And then follow the instructions to enter your credentials.</span></span>

<span data-ttu-id="04795-121">Once you have logged in, the login command lists your subscriptions.</span><span class="sxs-lookup"><span data-stu-id="04795-121">Once you have logged in, the login command lists your subscriptions.</span></span>

<span data-ttu-id="04795-122">To use a specific subscription:</span><span class="sxs-lookup"><span data-stu-id="04795-122">To use a specific subscription:</span></span>

```azurecli
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="04795-123">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="04795-123">Create Data Lake Analytics account</span></span>
<span data-ttu-id="04795-124">You need a Data Lake Analytics account before you can run any jobs.</span><span class="sxs-lookup"><span data-stu-id="04795-124">You need a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="04795-125">To create a Data Lake Analytics account, you must specify the following items:</span><span class="sxs-lookup"><span data-stu-id="04795-125">To create a Data Lake Analytics account, you must specify the following items:</span></span>

* <span data-ttu-id="04795-126">**Azure Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="04795-126">**Azure Resource Group**.</span></span> <span data-ttu-id="04795-127">A Data Lake Analytics account must be created within a Azure Resource group.</span><span class="sxs-lookup"><span data-stu-id="04795-127">A Data Lake Analytics account must be created within a Azure Resource group.</span></span> <span data-ttu-id="04795-128">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span><span class="sxs-lookup"><span data-stu-id="04795-128">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="04795-129">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="04795-129">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span></span>  
  
    <span data-ttu-id="04795-130">To list the existing resource groups under your subscription:</span><span class="sxs-lookup"><span data-stu-id="04795-130">To list the existing resource groups under your subscription:</span></span>
  
    ```azurecli
    az group list 
    ```

    <span data-ttu-id="04795-131">To create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="04795-131">To create a new resource group:</span></span>
  
    ```azurecli
    az group create --name "<Resource Group Name>" --location "<Azure Location>"
    ```

* <span data-ttu-id="04795-132">**Data Lake Analytics account name**.</span><span class="sxs-lookup"><span data-stu-id="04795-132">**Data Lake Analytics account name**.</span></span> <span data-ttu-id="04795-133">Each Data Lake Analytics account has a name.</span><span class="sxs-lookup"><span data-stu-id="04795-133">Each Data Lake Analytics account has a name.</span></span>
* <span data-ttu-id="04795-134">**Location**.</span><span class="sxs-lookup"><span data-stu-id="04795-134">**Location**.</span></span> <span data-ttu-id="04795-135">Use one of the Azure data centers that supports Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="04795-135">Use one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="04795-136">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="04795-136">**Default Data Lake Store account**: Each Data Lake Analytics account has a default Data Lake Store account.</span></span>
  
    <span data-ttu-id="04795-137">To list the existing Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="04795-137">To list the existing Data Lake Store account:</span></span>

    ```azurecli
    az dls account list
    ```
  
    <span data-ttu-id="04795-138">To create a new Data Lake Store account:</span><span class="sxs-lookup"><span data-stu-id="04795-138">To create a new Data Lake Store account:</span></span>
  
    ```azurecli
    az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
    ```

<span data-ttu-id="04795-139">Use the following syntax to create a Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="04795-139">Use the following syntax to create a Data Lake Analytics account:</span></span>

```azurecli
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

<span data-ttu-id="04795-140">After creating an account, you can use the following commands to list the accounts and show account details:</span><span class="sxs-lookup"><span data-stu-id="04795-140">After creating an account, you can use the following commands to list the accounts and show account details:</span></span>

```azurecli
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="04795-141">Upload data to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="04795-141">Upload data to Data Lake Store</span></span>
<span data-ttu-id="04795-142">In this tutorial, you process some search logs.</span><span class="sxs-lookup"><span data-stu-id="04795-142">In this tutorial, you process some search logs.</span></span>  <span data-ttu-id="04795-143">The search log can be stored in either Data Lake store or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="04795-143">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span> 

<span data-ttu-id="04795-144">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span><span class="sxs-lookup"><span data-stu-id="04795-144">The Azure portal provides a user interface for copying some sample data files to the default Data Lake Store account, which include a search log file.</span></span> <span data-ttu-id="04795-145">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data) to upload the data to the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="04795-145">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="04795-146">To upload files using CLI 2,0, use the following commands:</span><span class="sxs-lookup"><span data-stu-id="04795-146">To upload files using CLI 2,0, use the following commands:</span></span>

```azurecli
az dls file upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls file list --account "<Data Lake Store Account Name>" --path "<Path>"
```

<span data-ttu-id="04795-147">Data Lake Analytics can also access Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="04795-147">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="04795-148">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="04795-148">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="04795-149">Submit Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="04795-149">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="04795-150">The Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="04795-150">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="04795-151">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="04795-151">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="04795-152">**To create a Data Lake Analytics job script**</span><span class="sxs-lookup"><span data-stu-id="04795-152">**To create a Data Lake Analytics job script**</span></span>

<span data-ttu-id="04795-153">Create a text file with following U-SQL script, and save the text file to your workstation:</span><span class="sxs-lookup"><span data-stu-id="04795-153">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>
  
    @searchlog =
        EXTRACT UserId          int,
                Start           DateTime,
                Region          string,
                Query           string,
                Duration        int?,
                Urls            string,
                ClickedUrls     string
        FROM "/Samples/Data/SearchLog.tsv"
        USING Extractors.Tsv();

    OUTPUT @searchlog   
        TO "/Output/SearchLog-from-Data-Lake.csv"
    USING Outputters.Csv();
  
<span data-ttu-id="04795-154">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="04795-154">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span> 

<span data-ttu-id="04795-155">Don't modify the two paths unless you copy the source file into a different location.</span><span class="sxs-lookup"><span data-stu-id="04795-155">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="04795-156">Data Lake Analytics will create the output folder if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="04795-156">Data Lake Analytics will create the output folder if it doesn't exist.</span></span>

<span data-ttu-id="04795-157">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="04795-157">It is simpler to use relative paths for files stored in default Data Lake Store accounts.</span></span> <span data-ttu-id="04795-158">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="04795-158">You can also use absolute paths.</span></span>  <span data-ttu-id="04795-159">For example:</span><span class="sxs-lookup"><span data-stu-id="04795-159">For example:</span></span>

    adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

<span data-ttu-id="04795-160">You must use absolute paths to access files in linked Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="04795-160">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="04795-161">The syntax for files stored in linked Azure Storage account is:</span><span class="sxs-lookup"><span data-stu-id="04795-161">The syntax for files stored in linked Azure Storage account is:</span></span>

    wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
  
  > [!NOTE]
  > <span data-ttu-id="04795-162">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="04795-162">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span></span>      
  > 
  > 

<span data-ttu-id="04795-163">**To submit jobs**</span><span class="sxs-lookup"><span data-stu-id="04795-163">**To submit jobs**</span></span>

<span data-ttu-id="04795-164">Use the following syntax to submit a job.</span><span class="sxs-lookup"><span data-stu-id="04795-164">Use the following syntax to submit a job.</span></span>

```azurecli
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

<span data-ttu-id="04795-165">For example:</span><span class="sxs-lookup"><span data-stu-id="04795-165">For example:</span></span>

```azurecli
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

<span data-ttu-id="04795-166">**To list jobs and show job details**</span><span class="sxs-lookup"><span data-stu-id="04795-166">**To list jobs and show job details**</span></span>

```azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

<span data-ttu-id="04795-167">**To cancel jobs**</span><span class="sxs-lookup"><span data-stu-id="04795-167">**To cancel jobs**</span></span>

```azurecli
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

##<a name="retrieve-job-results"></a><span data-ttu-id="04795-168">Retrieve job results</span><span class="sxs-lookup"><span data-stu-id="04795-168">Retrieve job results</span></span>

<span data-ttu-id="04795-169">After a job is completed, you can use the following commands to list the output files, and download the files:</span><span class="sxs-lookup"><span data-stu-id="04795-169">After a job is completed, you can use the following commands to list the output files, and download the files:</span></span>

```azurecli
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" 
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

<span data-ttu-id="04795-170">For example:</span><span class="sxs-lookup"><span data-stu-id="04795-170">For example:</span></span>

```azurecli
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="next-steps"></a><span data-ttu-id="04795-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="04795-171">Next steps</span></span>

* <span data-ttu-id="04795-172">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="04795-172">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="04795-173">To see the Data Lake Analytics CLI 2.0 reference document, see[Data Lake Analytics - az dla](https://docs.microsoft.com/cli/azure/dla).</span><span class="sxs-lookup"><span data-stu-id="04795-173">To see the Data Lake Analytics CLI 2.0 reference document, see[Data Lake Analytics - az dla](https://docs.microsoft.com/cli/azure/dla).</span></span>
* <span data-ttu-id="04795-174">To see the Data Lake Store CLI 2.0 reference document, see[Data Lake Store - az dls](https://docs.microsoft.com/cli/azure/dls).</span><span class="sxs-lookup"><span data-stu-id="04795-174">To see the Data Lake Store CLI 2.0 reference document, see[Data Lake Store - az dls](https://docs.microsoft.com/cli/azure/dls).</span></span>
* <span data-ttu-id="04795-175">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="04795-175">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="04795-176">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04795-176">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="04795-177">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="04795-177">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="04795-178">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="04795-178">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="04795-179">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="04795-179">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

