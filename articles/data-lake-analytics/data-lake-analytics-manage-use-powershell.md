---
title: Manage Azure Data Lake Analytics using Azure PowerShell | Microsoft Docs
description: 'Learn how to manage Data Lake Analytics jobs, data sources, users. '
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: ad14d53c-fed4-478d-ab4b-6d2e14ff2097
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 98e2422cfd6a3c3ef9607eb85205a5d68f3b78ff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553196"
---
# <a name="manage-azure-data-lake-analytics-using-azure-powershell"></a><span data-ttu-id="3ff5d-103">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ff5d-103">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="3ff5d-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-104">Learn how to manage Azure Data Lake Analytics accounts, data sources, users, and jobs using the Azure PowerShell.</span></span> <span data-ttu-id="3ff5d-105">To see management topics using other tools, click the tab select above.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-105">To see management topics using other tools, click the tab select above.</span></span>

<span data-ttu-id="3ff5d-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="3ff5d-106">**Prerequisites**</span></span>

<span data-ttu-id="3ff5d-107">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-107">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="3ff5d-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-108">**An Azure subscription**.</span></span> <span data-ttu-id="3ff5d-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<!-- ################################ -->
<!-- ################################ -->


## <a name="install-azure-powershell-10-or-greater"></a><span data-ttu-id="3ff5d-110">Install Azure PowerShell 1.0 or greater</span><span class="sxs-lookup"><span data-stu-id="3ff5d-110">Install Azure PowerShell 1.0 or greater</span></span>
<span data-ttu-id="3ff5d-111">See the Prerequisite section of [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-111">See the Prerequisite section of [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

## <a name="manage-accounts"></a><span data-ttu-id="3ff5d-112">Manage accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-112">Manage accounts</span></span>
<span data-ttu-id="3ff5d-113">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-113">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="3ff5d-114">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-114">Unlike Azure HDInsight, you don't pay for an Analytics account when it is not running a job.</span></span>  <span data-ttu-id="3ff5d-115">You only pay for the time when it is running a job.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-115">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="3ff5d-116">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-116">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

### <a name="create-accounts"></a><span data-ttu-id="3ff5d-117">Create accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-117">Create accounts</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeStoreName = "<DataLakeAccountName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    $location = "<Microsoft Data Center>"

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
        -Name $dataLakeAnalyticsAccountName `
        -ResourceGroupName $resourceGroupName `
        -Location $location `
        -DefaultDataLake $dataLakeStoreName

    Write-Host "The newly created Data Lake Analytics account ..."  -ForegroundColor Green
    Get-AzureRmDataLakeAnalyticsAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $dataLakeAnalyticsAccountName  

<span data-ttu-id="3ff5d-118">You can also use an Azure Resource Group template.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-118">You can also use an Azure Resource Group template.</span></span> <span data-ttu-id="3ff5d-119">A template for creating a Data Lake Analytics account and the dependent Data Lake Store account is in [Appendix A](#appendix-a). Save the template into a file with .json template, and then use the following PowerShell script to call it:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-119">A template for creating a Data Lake Analytics account and the dependent Data Lake Store account is in [Appendix A](#appendix-a). Save the template into a file with .json template, and then use the following PowerShell script to call it:</span></span>

    $AzureSubscriptionID = "<Your Azure Subscription ID>"

    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"
    $DefaultDataLakeStoreAccountName = "<New Data Lake Store Account Name>"
    $DataLakeAnalyticsAccountName = "<New Data Lake Analytics Account Name>"

    $DeploymentName = "MyDataLakeAnalyticsDeployment"
    $ARMTemplateFile = "E:\Tutorials\ADL\ARMTemplate\azuredeploy.json"  # update the Json template path 

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId $AzureSubscriptionID

    # Create the resource group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Create the Data Lake Analytics account with the default Data Lake Store account.
    $parameters = @{"adlAnalyticsName"=$DataLakeAnalyticsAccountName; "adlStoreName"=$DefaultDataLakeStoreAccountName}
    New-AzureRmResourceGroupDeployment -Name $DeploymentName -ResourceGroupName $ResourceGroupName -TemplateFile $ARMTemplateFile -TemplateParameterObject $parameters 


### <a name="list-account"></a><span data-ttu-id="3ff5d-120">List account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-120">List account</span></span>
<span data-ttu-id="3ff5d-121">List Data Lake Analytics accounts within the current subscription</span><span class="sxs-lookup"><span data-stu-id="3ff5d-121">List Data Lake Analytics accounts within the current subscription</span></span>

    Get-AzureRmDataLakeAnalyticsAccount

<span data-ttu-id="3ff5d-122">The output:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-122">The output:</span></span>

    Id         : /subscriptions/xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx/resourceGroups/learn1021rg/providers/Microsoft.DataLakeAnalytics/accounts/learn1021adla
    Location   : eastus2
    Name       : learn1021adla
    Properties : Microsoft.Azure.Management.DataLake.Analytics.Models.DataLakeAnalyticsAccountProperties
    Tags       : {}
    Type       : Microsoft.DataLakeAnalytics/accounts

<span data-ttu-id="3ff5d-123">List Data Lake Analytics accounts within a specific resource group</span><span class="sxs-lookup"><span data-stu-id="3ff5d-123">List Data Lake Analytics accounts within a specific resource group</span></span>

    Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName

<span data-ttu-id="3ff5d-124">Get details of a specific Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-124">Get details of a specific Data Lake Analytics account</span></span>

    Get-AzureRmDataLakeAnalyticsAccount -Name $adlAnalyticsAccountName

<span data-ttu-id="3ff5d-125">Test existence of a specific Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-125">Test existence of a specific Data Lake Analytics account</span></span>

    Test-AzureRmDataLakeAnalyticsAccount -Name $adlAnalyticsAccountName

<span data-ttu-id="3ff5d-126">The cmdlet will return either **True** or **False**.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-126">The cmdlet will return either **True** or **False**.</span></span>

### <a name="delete-data-lake-analytics-accounts"></a><span data-ttu-id="3ff5d-127">Delete Data Lake Analytics accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-127">Delete Data Lake Analytics accounts</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"

    Remove-AzureRmDataLakeAnalyticsAccount -Name $dataLakeAnalyticsAccountName 

<span data-ttu-id="3ff5d-128">Delete Data Lake Analytics account will not delete the dependent Data Lake Storage account.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-128">Delete Data Lake Analytics account will not delete the dependent Data Lake Storage account.</span></span> <span data-ttu-id="3ff5d-129">The following example deletes the Data Lake Analytics account and the default Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-129">The following example deletes the Data Lake Analytics account and the default Data Lake Store account</span></span>

    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    $dataLakeStoreName = (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticAccountName).Properties.DefaultDataLakeAccount

    Remove-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticAccountName 
    Remove-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="3ff5d-130">Manage account data sources</span><span class="sxs-lookup"><span data-stu-id="3ff5d-130">Manage account data sources</span></span>
<span data-ttu-id="3ff5d-131">Data Lake Analytics currently supports the following data sources:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-131">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="3ff5d-132">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="3ff5d-132">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="3ff5d-133">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3ff5d-133">Azure Storage</span></span>](../storage/storage-introduction.md)

<span data-ttu-id="3ff5d-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-134">When you create an Analytics account, you must designate an Azure Data Lake Storage account to be the default storage account.</span></span> <span data-ttu-id="3ff5d-135">The default Data Lake Store account is used to store job metadata and job audit logs.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-135">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="3ff5d-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-136">After you have created an Analytics account, you can add additional Data Lake Storage accounts and/or Azure Storage account.</span></span> 

### <a name="find-the-default-data-lake-store-account"></a><span data-ttu-id="3ff5d-137">Find the default Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-137">Find the default Data Lake Store account</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    $dataLakeStoreName = (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticAccountName).Properties.DefaultDataLakeAccount


### <a name="add-additional-azure-blob-storage-accounts"></a><span data-ttu-id="3ff5d-138">Add additional Azure Blob storage accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-138">Add additional Azure Blob storage accounts</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    $AzureStorageAccountName = "<AzureStorageAccountName>"
    $AzureStorageAccountKey = "<AzureStorageAccountKey>"

    Add-AzureRmDataLakeAnalyticsDataSource -ResourceGroupName $resourceGroupName -Account $dataLakeAnalyticAccountName -AzureBlob $AzureStorageAccountName -AccessKey $AzureStorageAccountKey

### <a name="add-additional-data-lake-store-accounts"></a><span data-ttu-id="3ff5d-139">Add additional Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-139">Add additional Data Lake Store accounts</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    $AzureDataLakeName = "<DataLakeStoreName>"

    Add-AzureRmDataLakeAnalyticsDataSource -ResourceGroupName $resourceGroupName -Account $dataLakeAnalyticAccountName -DataLake $AzureDataLakeName 

### <a name="list-data-sources"></a><span data-ttu-id="3ff5d-140">List data sources:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-140">List data sources:</span></span>
    $resourceGroupName = "<ResourceGroupName>"
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"

    (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticAccountName).Properties.DataLakeStoreAccounts
    (Get-AzureRmDataLakeAnalyticsAccount -ResourceGroupName $resourceGroupName -Name $dataLakeAnalyticAccountName).Properties.StorageAccounts



<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-jobs"></a><span data-ttu-id="3ff5d-141">Manage jobs</span><span class="sxs-lookup"><span data-stu-id="3ff5d-141">Manage jobs</span></span>
<span data-ttu-id="3ff5d-142">You must have a Data Lake Analytics account before you can create a job.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-142">You must have a Data Lake Analytics account before you can create a job.</span></span>  <span data-ttu-id="3ff5d-143">For more information, see [Manage Data Lake Analytics accounts](#manage-data-lake-analytics-accounts).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-143">For more information, see [Manage Data Lake Analytics accounts](#manage-data-lake-analytics-accounts).</span></span>

### <a name="list-jobs"></a><span data-ttu-id="3ff5d-144">List jobs</span><span class="sxs-lookup"><span data-stu-id="3ff5d-144">List jobs</span></span>
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"

    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName

    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName -State Running, Queued
    #States: Accepted, Compiling, Ended, New, Paused, Queued, Running, Scheduling, Starting

    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName -Result Cancelled
    #Results: Cancelled, Failed, None, Successed 

    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName -Name <Job Name>
    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName -Submitter <Job submitter>

    # List all jobs submitted on January 1 (local time)
    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -SubmittedAfter "2015/01/01"
        -SubmittedBefore "2015/01/02"    

    # List all jobs that succeeded on January 1 after 2 pm (UTC time)
    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -State Ended
        -Result Succeeded
        -SubmittedAfter "2015/01/01 2:00 PM -0"
        -SubmittedBefore "2015/01/02 -0"

    # List all jobs submitted in the past hour
    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -SubmittedAfter (Get-Date).AddHours(-1)

### <a name="get-job-details"></a><span data-ttu-id="3ff5d-145">Get job details</span><span class="sxs-lookup"><span data-stu-id="3ff5d-145">Get job details</span></span>
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"
    Get-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName -JobID <Job ID>

### <a name="submit-jobs"></a><span data-ttu-id="3ff5d-146">Submit jobs</span><span class="sxs-lookup"><span data-stu-id="3ff5d-146">Submit jobs</span></span>
    $dataLakeAnalyticsAccountName = "<DataLakeAnalyticsAccountName>"

    #Pass script via path
    Submit-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -Name $jobName `
        -ScriptPath $scriptPath

    #Pass script contents
    Submit-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -Name $jobName `
        -Script $scriptContents

> [!NOTE]
> <span data-ttu-id="3ff5d-147">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-147">The default priority of a job is 1000, and the default degree of parallelism for a job is 1.</span></span>
> 
> 

### <a name="cancel-jobs"></a><span data-ttu-id="3ff5d-148">Cancel jobs</span><span class="sxs-lookup"><span data-stu-id="3ff5d-148">Cancel jobs</span></span>
    Stop-AzureRmDataLakeAnalyticsJob -Account $dataLakeAnalyticAccountName `
        -JobID $jobID


## <a name="manage-catalog-items"></a><span data-ttu-id="3ff5d-149">Manage catalog items</span><span class="sxs-lookup"><span data-stu-id="3ff5d-149">Manage catalog items</span></span>
<span data-ttu-id="3ff5d-150">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-150">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="3ff5d-151">The catalog enables the highest performance possible with data in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-151">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="3ff5d-152">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-152">For more information, see [Use U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md).</span></span>

### <a name="list-catalog-items"></a><span data-ttu-id="3ff5d-153">List catalog items</span><span class="sxs-lookup"><span data-stu-id="3ff5d-153">List catalog items</span></span>
    #List databases
    Get-AzureRmDataLakeAnalyticsCatalogItem `
        -Account $adlAnalyticsAccountName `
        -ItemType Database



    #List tables
    Get-AzureRmDataLakeAnalyticsCatalogItem `
        -Account $adlAnalyticsAccountName `
        -ItemType Table `
        -Path "master.dbo"

### <a name="get-catalog-item-details"></a><span data-ttu-id="3ff5d-154">Get catalog item details</span><span class="sxs-lookup"><span data-stu-id="3ff5d-154">Get catalog item details</span></span>
    #Get a database
    Get-AzureRmDataLakeAnalyticsCatalogItem `
        -Account $adlAnalyticsAccountName `
        -ItemType Database `
        -Path "master"

    #Get a table
    Get-AzureRmDataLakeAnalyticsCatalogItem `
        -Account $adlAnalyticsAccountName `
        -ItemType Table `
        -Path "master.dbo.mytable"

### <a name="test-existence-of--catalog-item"></a><span data-ttu-id="3ff5d-155">Test existence of  catalog item</span><span class="sxs-lookup"><span data-stu-id="3ff5d-155">Test existence of  catalog item</span></span>
    Test-AzureRmDataLakeAnalyticsCatalogItem  `
        -Account $adlAnalyticsAccountName `
        -ItemType Database `
        -Path "master"

### <a name="create-catalog-secret"></a><span data-ttu-id="3ff5d-156">Create catalog secret</span><span class="sxs-lookup"><span data-stu-id="3ff5d-156">Create catalog secret</span></span>
    New-AzureRmDataLakeAnalyticsCatalogSecret  `
            -Account $adlAnalyticsAccountName `
            -DatabaseName "master" `
            -Secret (Get-Credential -UserName "username" -Message "Enter the password")

### <a name="modify-catalog-secret"></a><span data-ttu-id="3ff5d-157">Modify catalog secret</span><span class="sxs-lookup"><span data-stu-id="3ff5d-157">Modify catalog secret</span></span>
    Set-AzureRmDataLakeAnalyticsCatalogSecret  `
            -Account $adlAnalyticsAccountName `
            -DatabaseName "master" `
            -Secret (Get-Credential -UserName "username" -Message "Enter the password")



### <a name="delete-catalog-secret"></a><span data-ttu-id="3ff5d-158">Delete catalog secret</span><span class="sxs-lookup"><span data-stu-id="3ff5d-158">Delete catalog secret</span></span>
    Remove-AzureRmDataLakeAnalyticsCatalogSecret  `
            -Account $adlAnalyticsAccountName `
            -DatabaseName "master"


## <a name="use-azure-resource-manager-groups"></a><span data-ttu-id="3ff5d-159">Use Azure Resource Manager groups</span><span class="sxs-lookup"><span data-stu-id="3ff5d-159">Use Azure Resource Manager groups</span></span>
<span data-ttu-id="3ff5d-160">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-160">Applications are typically made up of many components, for example a web app, database, database server, storage, and 3rd party services.</span></span> <span data-ttu-id="3ff5d-161">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-161">Azure Resource Manager (ARM) enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="3ff5d-162">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-162">You can deploy, update, monitor or delete all of the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="3ff5d-163">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-163">You use a template for deployment and that template can work for different environments such as testing, staging and production.</span></span> <span data-ttu-id="3ff5d-164">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-164">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="3ff5d-165">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-165">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="3ff5d-166">A Data Lake Analytics service can include the following components:</span><span class="sxs-lookup"><span data-stu-id="3ff5d-166">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="3ff5d-167">Azure Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-167">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="3ff5d-168">Required default Azure Data Lake Storage account</span><span class="sxs-lookup"><span data-stu-id="3ff5d-168">Required default Azure Data Lake Storage account</span></span>
* <span data-ttu-id="3ff5d-169">Additional Azure Data Lake Storage accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-169">Additional Azure Data Lake Storage accounts</span></span>
* <span data-ttu-id="3ff5d-170">Additional Azure Storage accounts</span><span class="sxs-lookup"><span data-stu-id="3ff5d-170">Additional Azure Storage accounts</span></span>

<span data-ttu-id="3ff5d-171">You can create all these components under one ARM group to make them easier to manage.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-171">You can create all these components under one ARM group to make them easier to manage.</span></span>

![Azure Data Lake Analytics account and storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="3ff5d-173">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-173">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="3ff5d-174">The ARM group however can be located in a different data center.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-174">The ARM group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="3ff5d-175">See also</span><span class="sxs-lookup"><span data-stu-id="3ff5d-175">See also</span></span>
* [<span data-ttu-id="3ff5d-176">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3ff5d-176">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="3ff5d-177">Get started with Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ff5d-177">Get started with Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="3ff5d-178">Manage Azure Data Lake Analytics using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ff5d-178">Manage Azure Data Lake Analytics using Azure Portal</span></span>](data-lake-analytics-manage-use-portal.md)
* [<span data-ttu-id="3ff5d-179">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span><span class="sxs-lookup"><span data-stu-id="3ff5d-179">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure Portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)

## <a name="appendix-a---data-lake-analytics-arm-template"></a><span data-ttu-id="3ff5d-180">Appendix A - Data Lake Analytics ARM template</span><span class="sxs-lookup"><span data-stu-id="3ff5d-180">Appendix A - Data Lake Analytics ARM template</span></span>
<span data-ttu-id="3ff5d-181">The following ARM template can be used to deploy a Data Lake Analytics account and its dependent Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-181">The following ARM template can be used to deploy a Data Lake Analytics account and its dependent Data Lake Store account.</span></span>  <span data-ttu-id="3ff5d-182">Save it as a json file, and then use PowerShell script to call the template.</span><span class="sxs-lookup"><span data-stu-id="3ff5d-182">Save it as a json file, and then use PowerShell script to call the template.</span></span> <span data-ttu-id="3ff5d-183">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="3ff5d-183">For more information, see [Deploy an application with Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) and [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
        "adlAnalyticsName": {
          "type": "string",
          "metadata": {
            "description": "The name of the Data Lake Analytics account to create."
          }
        },
        "adlStoreName": {
          "type": "string",
          "metadata": {
            "description": "The name of the Data Lake Store account to create."
          }
        }
      },
      "resources": [
        {
          "name": "[parameters('adlStoreName')]",
          "type": "Microsoft.DataLakeStore/accounts",
          "location": "East US 2",
          "apiVersion": "2015-10-01-preview",
          "dependsOn": [ ],
          "tags": { }
        },
        {
          "name": "[parameters('adlAnalyticsName')]",
          "type": "Microsoft.DataLakeAnalytics/accounts",
          "location": "East US 2",
          "apiVersion": "2015-10-01-preview",
          "dependsOn": [ "[concat('Microsoft.DataLakeStore/accounts/',parameters('adlStoreName'))]" ],
          "tags": { },
          "properties": {
            "defaultDataLakeStoreAccount": "[parameters('adlStoreName')]",
            "dataLakeStoreAccounts": [
              { "name": "[parameters('adlStoreName')]" }
            ]
          }
        }
      ],
      "outputs": {
        "adlAnalyticsAccount": {
          "type": "object",
          "value": "[reference(resourceId('Microsoft.DataLakeAnalytics/accounts',parameters('adlAnalyticsName')))]"
        },
        "adlStoreAccount": {
          "type": "object",
          "value": "[reference(resourceId('Microsoft.DataLakeStore/accounts',parameters('adlStoreName')))]"
        }
      }
    }


