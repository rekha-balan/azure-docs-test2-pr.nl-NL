---
title: Get started with Azure Data Lake Analytics using Azure PowerShell | Microsoft Docs
description: 'Use Azure PowerShell to create a Data Lake Analytics account, create a Data Lake Analytics job using U-SQL, and submit the job. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/06/2017
ms.author: edmaca
ms.openlocfilehash: 32f115a4d901a43abf1bf69d1c0c72b65ec7368c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553574"
---
# <a name="tutorial-get-started-with-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="646bb-103">Tutorial: get started with Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="646bb-103">Tutorial: get started with Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="646bb-104">Learn how to use the Azure PowerShell to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytic accounts.</span><span class="sxs-lookup"><span data-stu-id="646bb-104">Learn how to use the Azure PowerShell to create Azure Data Lake Analytics accounts, define Data Lake Analytics jobs in [U-SQL](data-lake-analytics-u-sql-get-started.md), and submit jobs to Data Lake Analytic accounts.</span></span> <span data-ttu-id="646bb-105">For more  information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-105">For more  information about Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>

<span data-ttu-id="646bb-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span><span class="sxs-lookup"><span data-stu-id="646bb-106">In this tutorial, you will develop a job that reads a tab separated values (TSV) file and converts it into a comma separated values (CSV) file.</span></span> <span data-ttu-id="646bb-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span><span class="sxs-lookup"><span data-stu-id="646bb-107">To go through the same tutorial using other supported tools, click the tabs on the top of this section.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="646bb-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="646bb-108">Prerequisites</span></span>
<span data-ttu-id="646bb-109">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="646bb-109">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="646bb-110">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="646bb-110">**An Azure subscription**.</span></span> <span data-ttu-id="646bb-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="646bb-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="646bb-112">**A workstation with Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="646bb-112">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="646bb-113">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="646bb-113">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="646bb-114">Create Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="646bb-114">Create Data Lake Analytics account</span></span>
<span data-ttu-id="646bb-115">You must have a Data Lake Analytics account before you can run any jobs.</span><span class="sxs-lookup"><span data-stu-id="646bb-115">You must have a Data Lake Analytics account before you can run any jobs.</span></span> <span data-ttu-id="646bb-116">To create a Data Lake Analytics account, you must specify the following:</span><span class="sxs-lookup"><span data-stu-id="646bb-116">To create a Data Lake Analytics account, you must specify the following:</span></span>

* <span data-ttu-id="646bb-117">**Azure Resource Group**: A Data Lake Analytics account must be created within a Azure Resource group.</span><span class="sxs-lookup"><span data-stu-id="646bb-117">**Azure Resource Group**: A Data Lake Analytics account must be created within a Azure Resource group.</span></span> <span data-ttu-id="646bb-118">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span><span class="sxs-lookup"><span data-stu-id="646bb-118">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="646bb-119">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="646bb-119">You can deploy, update or delete all of the resources for your application in a single, coordinated operation.</span></span>  

    <span data-ttu-id="646bb-120">To enumerate the resource groups in your subscription:</span><span class="sxs-lookup"><span data-stu-id="646bb-120">To enumerate the resource groups in your subscription:</span></span>

        Get-AzureRmResourceGroup

    <span data-ttu-id="646bb-121">To create a new resource group:</span><span class="sxs-lookup"><span data-stu-id="646bb-121">To create a new resource group:</span></span>

        New-AzureRmResourceGroup `
            -Name "<Your resource group name>" `
            -Location "<Azure Data Center>" # For example, "East US 2"
* <span data-ttu-id="646bb-122">**Data Lake Analytics account name**</span><span class="sxs-lookup"><span data-stu-id="646bb-122">**Data Lake Analytics account name**</span></span>
* <span data-ttu-id="646bb-123">**Location**: one of the Azure data centers that supports Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="646bb-123">**Location**: one of the Azure data centers that supports Data Lake Analytics.</span></span>
* <span data-ttu-id="646bb-124">**Default Data Lake account**: each Data Lake Analytics account has a default Data Lake account.</span><span class="sxs-lookup"><span data-stu-id="646bb-124">**Default Data Lake account**: each Data Lake Analytics account has a default Data Lake account.</span></span>

    <span data-ttu-id="646bb-125">To create a new Data Lake account:</span><span class="sxs-lookup"><span data-stu-id="646bb-125">To create a new Data Lake account:</span></span>

        New-AzureRmDataLakeStoreAccount `
            -ResourceGroupName "<Your Azure resource group name>" `
            -Name "<Your Data Lake account name>" `
            -Location "<Azure Data Center>"  # For example, "East US 2"

  > [!NOTE]
  > <span data-ttu-id="646bb-126">The Data Lake account name must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="646bb-126">The Data Lake account name must only contain lowercase letters and numbers.</span></span>
  >
  >

<span data-ttu-id="646bb-127">**To create a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="646bb-127">**To create a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="646bb-128">Open PowerShell ISE from your Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="646bb-128">Open PowerShell ISE from your Windows workstation.</span></span>
2. <span data-ttu-id="646bb-129">Run the following script:</span><span class="sxs-lookup"><span data-stu-id="646bb-129">Run the following script:</span></span>

        $resourceGroupName = "<ResourceGroupName>"
        $dataLakeStoreName = "<DataLakeAccountName>"
        $dataLakeAnalyticsName = "<DataLakeAnalyticsAccountName>"
        $location = "East US 2"

        Write-Host "Create a resource group ..." -ForegroundColor Green
        New-AzureRmResourceGroup `
            -Name  $resourceGroupName `
            -Location $location

        Write-Host "Create a Data Lake account ..."  -ForegroundColor Green
        New-AzureRmDataLakeStoreAccount `
            -ResourceGroupName $resourceGroupName `
            -Name $dataLakeStoreName `
            -Location $location

        Write-Host "Create a Data Lake Analytics account ..."  -ForegroundColor Green
        New-AzureRmDataLakeAnalyticsAccount `
            -Name $dataLakeAnalyticsName `
            -ResourceGroupName $resourceGroupName `
            -Location $location `
            -DefaultDataLake $dataLakeStoreName

        Write-Host "The newly created Data Lake Analytics account ..."  -ForegroundColor Green
        Get-AzureRmDataLakeAnalyticsAccount `
            -ResourceGroupName $resourceGroupName `
            -Name $dataLakeAnalyticsName  

## <a name="upload-data-to-data-lake"></a><span data-ttu-id="646bb-130">Upload data to Data Lake</span><span class="sxs-lookup"><span data-stu-id="646bb-130">Upload data to Data Lake</span></span>
<span data-ttu-id="646bb-131">In this tutorial, you will process some search logs.</span><span class="sxs-lookup"><span data-stu-id="646bb-131">In this tutorial, you will process some search logs.</span></span>  <span data-ttu-id="646bb-132">The search log can be stored in either Data Lake store or Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="646bb-132">The search log can be stored in either Data Lake store or Azure Blob storage.</span></span>

<span data-ttu-id="646bb-133">A sample search log file has been copied to a public Azure Blob container.</span><span class="sxs-lookup"><span data-stu-id="646bb-133">A sample search log file has been copied to a public Azure Blob container.</span></span> <span data-ttu-id="646bb-134">Use the following PowerShell script to download the file to your workstation, and then upload the file to the default Data Lake Store account of your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="646bb-134">Use the following PowerShell script to download the file to your workstation, and then upload the file to the default Data Lake Store account of your Data Lake Analytics account.</span></span>

    $dataLakeStoreName = "<The default Data Lake Store account name>"

    $localFolder = "C:\Tutorials\Downloads\" # A temp location for the file.
    $storageAccount = "adltutorials"  # Don't modify this value.
    $container = "adls-sample-data"  #Don't modify this value.

    # Create the temp location    
    New-Item -Path $localFolder -ItemType Directory -Force

    # Download the sample file from Azure Blob storage
    $context = New-AzureStorageContext -StorageAccountName $storageAccount -Anonymous
    $$blobs = Get-AzureStorageBlob -Container $container -Context $context
    $blobs | Get-AzureStorageBlobContent -Context $context -Destination $localFolder

    # Upload the file to the default Data Lake Store account    
    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $localFolder"SearchLog.tsv" -Destination "/Samples/Data/SearchLog.tsv"

<span data-ttu-id="646bb-135">The following PowerShell script shows you how to get the default Data Lake Store name for a Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="646bb-135">The following PowerShell script shows you how to get the default Data Lake Store name for a Data Lake Analytics account:</span></span>

    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsName = "<DataLakeAnalyticsAccountName>"
    $dataLakeStoreName = (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticsName).Properties.DefaultDataLakeStoreAccount
    echo $dataLakeStoreName

> [!NOTE]
> <span data-ttu-id="646bb-136">The Azure Portal provides an user interface to copy the sample data files to the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="646bb-136">The Azure Portal provides an user interface to copy the sample data files to the default Data Lake Store account.</span></span> <span data-ttu-id="646bb-137">For instructions, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md#prepare-source-data).</span><span class="sxs-lookup"><span data-stu-id="646bb-137">For instructions, see [Get Started with Azure Data Lake Analytics using Azure Portal](data-lake-analytics-get-started-portal.md#prepare-source-data).</span></span>
>
>

<span data-ttu-id="646bb-138">Data Lake Analytics can also access Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="646bb-138">Data Lake Analytics can also access Azure Blob storage.</span></span>  <span data-ttu-id="646bb-139">For uploading data to Azure Blob storage, see [Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-139">For uploading data to Azure Blob storage, see [Using Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span></span>

## <a name="submit-data-lake-analytics-jobs"></a><span data-ttu-id="646bb-140">Submit Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="646bb-140">Submit Data Lake Analytics jobs</span></span>
<span data-ttu-id="646bb-141">The Data Lake Analytics jobs are written in the U-SQL language.</span><span class="sxs-lookup"><span data-stu-id="646bb-141">The Data Lake Analytics jobs are written in the U-SQL language.</span></span> <span data-ttu-id="646bb-142">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span><span class="sxs-lookup"><span data-stu-id="646bb-142">To learn more about U-SQL, see [Get started with U-SQL language](data-lake-analytics-u-sql-get-started.md) and [U-SQL language reference](http://go.microsoft.com/fwlink/?LinkId=691348).</span></span>

<span data-ttu-id="646bb-143">**To create a Data Lake Analytics job script**</span><span class="sxs-lookup"><span data-stu-id="646bb-143">**To create a Data Lake Analytics job script**</span></span>

* <span data-ttu-id="646bb-144">Create a text file with following U-SQL script, and save the text file to your workstation:</span><span class="sxs-lookup"><span data-stu-id="646bb-144">Create a text file with following U-SQL script, and save the text file to your workstation:</span></span>

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

    <span data-ttu-id="646bb-145">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="646bb-145">This U-SQL script reads the source data file using **Extractors.Tsv()**, and then creates a csv file using **Outputters.Csv()**.</span></span>

    <span data-ttu-id="646bb-146">Don't modify the two paths unless you copy the source file into a different location.</span><span class="sxs-lookup"><span data-stu-id="646bb-146">Don't modify the two paths unless you copy the source file into a different location.</span></span>  <span data-ttu-id="646bb-147">Data Lake Analytics will create the output folder if it doesn't exist.</span><span class="sxs-lookup"><span data-stu-id="646bb-147">Data Lake Analytics will create the output folder if it doesn't exist.</span></span>

    <span data-ttu-id="646bb-148">It is simpler to use relative paths for files stored in default data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="646bb-148">It is simpler to use relative paths for files stored in default data Lake accounts.</span></span> <span data-ttu-id="646bb-149">You can also use absolute paths.</span><span class="sxs-lookup"><span data-stu-id="646bb-149">You can also use absolute paths.</span></span>  <span data-ttu-id="646bb-150">For example</span><span class="sxs-lookup"><span data-stu-id="646bb-150">For example</span></span>

        adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv

    <span data-ttu-id="646bb-151">You must use absolute paths to access  files in  linked Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="646bb-151">You must use absolute paths to access  files in  linked Storage accounts.</span></span>  <span data-ttu-id="646bb-152">The syntax for files stored in linked Azure Storage account is:</span><span class="sxs-lookup"><span data-stu-id="646bb-152">The syntax for files stored in linked Azure Storage account is:</span></span>

        wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv

  > [!NOTE]
  > <span data-ttu-id="646bb-153">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="646bb-153">Azure Blob container with public blobs or public containers access permissions are not currently supported.</span></span>    
  >
  >

<span data-ttu-id="646bb-154">**To submit the job**</span><span class="sxs-lookup"><span data-stu-id="646bb-154">**To submit the job**</span></span>

1. <span data-ttu-id="646bb-155">Open PowerShell ISE from your Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="646bb-155">Open PowerShell ISE from your Windows workstation.</span></span>
2. <span data-ttu-id="646bb-156">Run the following script:</span><span class="sxs-lookup"><span data-stu-id="646bb-156">Run the following script:</span></span>

        $dataLakeAnalyticsName = "<DataLakeAnalyticsAccountName>"
        $usqlScript = "c:\tutorials\data-lake-analytics\copyFile.usql"

        $job = Submit-AzureRmDataLakeAnalyticsJob -Name "convertTSVtoCSV" -AccountName $dataLakeAnalyticsName –ScriptPath $usqlScript

        Wait-AdlJob -Account $dataLakeAnalyticsName -JobId $job.JobId

        Get-AzureRmDataLakeAnalyticsJob -AccountName $dataLakeAnalyticsName -JobId $job.JobId

    <span data-ttu-id="646bb-157">In the script, the U-SQL script file is stored at c:\tutorials\data-lake-analytics\copyFile.usql.</span><span class="sxs-lookup"><span data-stu-id="646bb-157">In the script, the U-SQL script file is stored at c:\tutorials\data-lake-analytics\copyFile.usql.</span></span> <span data-ttu-id="646bb-158">Update the file path accordingly.</span><span class="sxs-lookup"><span data-stu-id="646bb-158">Update the file path accordingly.</span></span>

<span data-ttu-id="646bb-159">After the job is completed, you can use the following cmdlets to list the file, and download the file:</span><span class="sxs-lookup"><span data-stu-id="646bb-159">After the job is completed, you can use the following cmdlets to list the file, and download the file:</span></span>

    $resourceGroupName = "<Resource Group Name>"
    $dataLakeAnalyticName = "<Data Lake Analytic Account Name>"
    $destFile = "C:\tutorials\data-lake-analytics\SearchLog-from-Data-Lake.csv"

    $dataLakeStoreName = (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticName).Properties.DefaultDataLakeAccount

    Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -path "/Output"

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "/Output/SearchLog-from-Data-Lake.csv" -Destination $destFile

## <a name="see-also"></a><span data-ttu-id="646bb-160">See also</span><span class="sxs-lookup"><span data-stu-id="646bb-160">See also</span></span>
* <span data-ttu-id="646bb-161">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="646bb-161">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>
* <span data-ttu-id="646bb-162">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-162">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="646bb-163">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-163">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="646bb-164">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-164">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="646bb-165">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-165">For management tasks, see [Manage Azure Data Lake Analytics using Azure Portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="646bb-166">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="646bb-166">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
