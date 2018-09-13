---
title: Get started with Azure Data Lake Analytics using Azure Command-line Interface | Microsoft Docs
description: 'Learn how to use the Azure Command-line Interface to create a Data Lake Analytics account, create a Data Lake Analytics job using U-SQL, and submit the job. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 651021d4-4591-4c48-b1ef-3ebc4606d66d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 4ec848269ae17e3f034c2415cd0da1ef0dcf1730
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563768"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-azure-command-line-interface-cli"></a><span data-ttu-id="88023-103">Tutorial: get started with Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span><span class="sxs-lookup"><span data-stu-id="88023-103">Tutorial: get started with Azure Data Lake Analytics using Azure Command-line Interface (CLI)</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="88023-104">Learn how to use Azure CLI to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytics accounts.</span><span class="sxs-lookup"><span data-stu-id="88023-104">Learn how to use Azure CLI to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytics accounts.</span></span> <span data-ttu-id="88023-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88023-105">For more information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="88023-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="88023-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span></span> <span data-ttu-id="88023-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span><span class="sxs-lookup"><span data-stu-id="88023-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88023-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="88023-108">Prerequisites</span></span>
<span data-ttu-id="88023-109">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="88023-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="88023-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="88023-110">**An Azure subscription**.</span></span> <span data-ttu-id="88023-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="88023-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="88023-112">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="88023-112">**Azure CLI**.</span></span> <span data-ttu-id="88023-113">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="88023-113">See [Install and configure Azure CLI](../cli-install-nodejs.md).</span></span>
  * <span data-ttu-id="88023-114">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span><span class="sxs-lookup"><span data-stu-id="88023-114">Download and install the **pre-release** [Azure CLI tools](https://github.com/MicrosoftBigData/AzureDataLake/releases) in order to complete this demo.</span></span>
* <span data-ttu-id="88023-115">**Authentication**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="88023-115">**Authentication**, using the following command:</span></span>
  
        azure login
    <span data-ttu-id="88023-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="88023-116">For more information on authenticating using a work or school account, see [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>
* <span data-ttu-id="88023-117">**Switch to the Azure Resource Manager mode**, using the following command:</span><span class="sxs-lookup"><span data-stu-id="88023-117">**Switch to the Azure Resource Manager mode**, using the following command:</span></span>
  
        azure config mode arm

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="88023-118">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="88023-118">Create Data Lake Analytics account</span></span>
<span data-ttu-id="88023-119">You must have a Data Lake Analytics account before you can run any jobs.</span><span class="sxs-lookup"><span data-stu-id="88023-119">You must have a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="88023-120">To create a Data Lake Analytics account, you must specify the following:</span><span class="sxs-lookup"><span data-stu-id="88023-120">To create a Data Lake Analytics account, you must specify the following:</span></span>

* <span data-ttu-id="88023-121">**Azure Resource Group**: A Data Lake Analytics account must be created within a Azure Resource group.</span><span class="sxs-lookup"><span data-stu-id="88023-121">**Azure Resource Group**: A Data Lake Analytics account must be created within a Azure Resource group.</span></span> <span data-ttu-id="88023-122">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span><span class="sxs-lookup"><span data-stu-id="88023-122">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="88023-123">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="88023-123">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span></span>  
  
    <span data-ttu-id="88023-124">To enumerate the resource groups in your subscription:</span><span class="sxs-lookup"><span data-stu-id="88023-124">To enumerate the resource groups in your subscription:</span></span>
  
        azure group list 
  
    <span data-ttu-id="88023-125">To create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="88023-125">To create a new resource group:</span></span>
  
        azure group create -n "<Resource Group Name>" -l "<Azure Location>"
* <span data-ttu-id="88023-126">**Data Lake Analytics account name**</span><span class="sxs-lookup"><span data-stu-id="88023-126">**Data Lake Analytics account name**</span></span>
* <span data-ttu-id="88023-127">**Location**: one of the Azure data centers that supports Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="88023-127">**Location**: one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="88023-128">**Default Data Lake account**: each Data Lake Analytics account has a default Data Lake account.</span><span class="sxs-lookup"><span data-stu-id="88023-128">**Default Data Lake account**: each Data Lake Analytics account has a default Data Lake account.</span></span>
  
    <span data-ttu-id="88023-129">To list the existing Data Lake account:</span><span class="sxs-lookup"><span data-stu-id="88023-129">To list the existing Data Lake account:</span></span>
  
        azure datalake store account list
  
    <span data-ttu-id="88023-130">To create a new Data Lake account:</span><span class="sxs-lookup"><span data-stu-id="88023-130">To create a new Data Lake account:</span></span>
  
        azure datalake store account create "<Data Lake Store Account Name>" "<Azure Location>" "<Resource Group Name>"
  
  > [!NOTE]
  > <span data-ttu-id="88023-131">The Data Lake account name must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="88023-131">The Data Lake account name must only contain lowercase letters and numbers.</span></span>
  > 
  > 

<span data-ttu-id="88023-132">**To create a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="88023-132">**To create a Data Lake Analytics account**</span></span>

        azure datalake analytics account create "<Data Lake Analytics Account Name>" "<Azure Location>" "<Resource Group Name>" "<Default Data Lake Account Name>"

        azure datalake analytics account list
        azure datalake analytics account show "<Data Lake Analytics Account Name>"            

![Data Lake Analytics show account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-cli/data-lake-analytics-show-account-cli.png)

> [!NOTE]
> <span data-ttu-id="88023-134">The Data Lake Analytics account name must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="88023-134">The Data Lake Analytics account name must only contain lowercase letters and numbers.</span></span>
> 
> 

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="88023-135">Upload data to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="88023-135">Upload data to Data Lake Store</span></span>
<span data-ttu-id="88023-136">In this tutorial, you will process some search logs.</span><span class="sxs-lookup"><span data-stu-id="88023-136">In this tutorial, you will process some search logs.</span></span>  <span data-ttu-id="88023-137">The search log can be stored in either Data Lake store or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="88023-137">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span> 

<span data-ttu-id="88023-138">The Azure Portal provides a user interface for copying some sample data files to the default Data Lake account, which include a search log file.</span><span class="sxs-lookup"><span data-stu-id="88023-138">The Azure Portal provides a user interface for copying some sample data files to the default Data Lake account, which include a search log file.</span></span> <span data-ttu-id="88023-139">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data) to upload the data to the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="88023-139">See [Prepare source data](data-lake-analytics-get-started-portal.md#prepare-source-data) to upload the data to the default Data Lake Store account.</span></span>

<span data-ttu-id="88023-140">To upload files using cli, use the following command:</span><span class="sxs-lookup"><span data-stu-id="88023-140">To upload files using cli, use the following command:</span></span>

      azure datalake store filesystem import "<Data Lake Store Account Name>" "<Path>" "<Destination>"
      azure datalake store filesystem list "<Data Lake Store Account Name>" "<Path>"

<span data-ttu-id="88023-141">Data Lake Analytics can also access Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="88023-141">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="88023-142">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="88023-142">For uploading data to Azure Blob storage, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="88023-143">Submit Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="88023-143">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="88023-144">The Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="88023-144">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="88023-145">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="88023-145">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="88023-146">**To create a Data Lake Analytics job script**</span><span class="sxs-lookup"><span data-stu-id="88023-146">**To create a Data Lake Analytics job script**</span></span>

* <span data-ttu-id="88023-147">Create a text file with following U-SQL script, and save the text file to your workstation:</span><span class="sxs-lookup"><span data-stu-id="88023-147">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>
  
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
  
    <span data-ttu-id="88023-148">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="88023-148">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span> 
  
    <span data-ttu-id="88023-149">Don't modify the two paths unless you copy the source file into a different location.</span><span class="sxs-lookup"><span data-stu-id="88023-149">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="88023-150">Data Lake Analytics will create the output folder if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="88023-150">Data Lake Analytics will create the output folder if it doesn't exist.</span></span>
  
    <span data-ttu-id="88023-151">It is simpler to use relative paths for files stored in default data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="88023-151">It is simpler to use relative paths for files stored in default data Lake accounts.</span></span> <span data-ttu-id="88023-152">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="88023-152">You can also use absolute paths.</span></span>  <span data-ttu-id="88023-153">For example</span><span class="sxs-lookup"><span data-stu-id="88023-153">For example</span></span> 
  
        adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
  
    <span data-ttu-id="88023-154">You must use absolute paths to access files in linked Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="88023-154">You must use absolute paths to access files in linked Storage accounts.</span></span>  <span data-ttu-id="88023-155">The syntax for files stored in linked Azure Storage account is:</span><span class="sxs-lookup"><span data-stu-id="88023-155">The syntax for files stored in linked Azure Storage account is:</span></span>
  
        wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
  
  > [!NOTE]
  > <span data-ttu-id="88023-156">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="88023-156">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span></span>      
  > 
  > 

<span data-ttu-id="88023-157">**To submit the job**</span><span class="sxs-lookup"><span data-stu-id="88023-157">**To submit the job**</span></span>

    azure datalake analytics job create  "<Data Lake Analytics Account Name>" "<Job Name>" "<Script>"


<span data-ttu-id="88023-158">The following commands can be used to list jobs, get job details, and cancel jobs:</span><span class="sxs-lookup"><span data-stu-id="88023-158">The following commands can be used to list jobs, get job details, and cancel jobs:</span></span>

```
azure datalake analytics job cancel "<Data Lake Analytics Account Name>" "<Job Id>"
azure datalake analytics job list "<Data Lake Analytics Account Name>"
azure datalake analytics job show "<Data Lake Analytics Account Name>" "<Job Id>"
```

<span data-ttu-id="88023-159">After the job is completed, you can use the following cmdlets to list the file, and download the file:</span><span class="sxs-lookup"><span data-stu-id="88023-159">After the job is completed, you can use the following cmdlets to list the file, and download the file:</span></span>

    azure datalake store filesystem list "<Data Lake Store Account Name>" "/Output"
    azure datalake store filesystem export "<Data Lake Store Account Name>" "/Output/SearchLog-from-Data-Lake.csv" "<Destination>"
    azure datalake store filesystem read "<Data Lake Store Account Name>" "/Output/SearchLog-from-Data-Lake.csv" <Length> <Offset>

## <a name="see-also"></a><span data-ttu-id="88023-160">See also</span><span class="sxs-lookup"><span data-stu-id="88023-160">See also</span></span>
* <span data-ttu-id="88023-161">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="88023-161">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="88023-162">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="88023-162">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="88023-163">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88023-163">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="88023-164">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88023-164">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="88023-165">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="88023-165">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="88023-166">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="88023-166">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>


