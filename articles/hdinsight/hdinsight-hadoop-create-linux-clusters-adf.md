---
title: Create Azure HDInsight (Hadoop) using Data Factory | Microsoft Docs
description: Learn how to create on-demand Hadoop clusters in HDInsight using Azure Data Factory.
services: hdinsight
documentationcenter: ''
tags: azure-portal
author: spelluru
manager: jhubbard
editor: cgronlun
ms.assetid: 1f3b3a78-4d16-4d99-ba6e-06f7bb185d6a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/23/2017
ms.author: spelluru
ms.openlocfilehash: 344c2899949192d16698d84d4042ddf22c035741
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563218"
---
# <a name="create-on-demand-hadoop-clusters-in-hdinsight-using-azure-data-factory"></a><span data-ttu-id="54cbf-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="54cbf-103">Create on-demand Hadoop clusters in HDInsight using Azure Data Factory</span></span>
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="54cbf-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span><span class="sxs-lookup"><span data-stu-id="54cbf-104">[Azure Data Factory](../data-factory/data-factory-introduction.md) is a cloud-based data integration service that orchestrates and automates the movement and transformation of data.</span></span> <span data-ttu-id="54cbf-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span><span class="sxs-lookup"><span data-stu-id="54cbf-105">It can create a HDInsight Hadoop cluster just-in-time to process an input data slice and delete the cluster when the processing is complete.</span></span> <span data-ttu-id="54cbf-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span><span class="sxs-lookup"><span data-stu-id="54cbf-106">Some of the benefits of using an on-demand HDInsight Hadoop cluster are:</span></span>

- <span data-ttu-id="54cbf-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span><span class="sxs-lookup"><span data-stu-id="54cbf-107">You only pay for the time job is running on the HDInsight Hadoop cluster (plus a brief configurable idle time).</span></span> <span data-ttu-id="54cbf-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span><span class="sxs-lookup"><span data-stu-id="54cbf-108">The billing for HDInsight clusters is pro-rated per minute, whether you are using them or not.</span></span> <span data-ttu-id="54cbf-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span><span class="sxs-lookup"><span data-stu-id="54cbf-109">When you use an on-demand HDInsight linked service in Data Factory, the clusters are created on-demand.</span></span> <span data-ttu-id="54cbf-110">And the clusters are deleted automatically when the jobs are completed.</span><span class="sxs-lookup"><span data-stu-id="54cbf-110">And the clusters are deleted automatically when the jobs are completed.</span></span> <span data-ttu-id="54cbf-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span><span class="sxs-lookup"><span data-stu-id="54cbf-111">Therefore, you only pay for the job running time and the brief idle time (time-to-live setting).</span></span> 
- <span data-ttu-id="54cbf-112">You can create a workflow using a Data Factory pipeline.</span><span class="sxs-lookup"><span data-stu-id="54cbf-112">You can create a workflow using a Data Factory pipeline.</span></span> <span data-ttu-id="54cbf-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-113">For example, you can have the pipeline to copy data from an on-premises SQL Server to an Azure blob storage, process the data by running a Hive script and a Pig script on an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="54cbf-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span><span class="sxs-lookup"><span data-stu-id="54cbf-114">Then, copy the result data to an Azure SQL Data Warehouse for BI applications to consume.</span></span>
- <span data-ttu-id="54cbf-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span><span class="sxs-lookup"><span data-stu-id="54cbf-115">You can schedule the workflow to run periodically (hourly, daily, weekly, monthly, etc.).</span></span>

<span data-ttu-id="54cbf-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span><span class="sxs-lookup"><span data-stu-id="54cbf-116">In Azure Data Factory, a data factory can have one or more data pipelines.</span></span> <span data-ttu-id="54cbf-117">A data pipeline has one or more activities.</span><span class="sxs-lookup"><span data-stu-id="54cbf-117">A data pipeline has one or more activities.</span></span> <span data-ttu-id="54cbf-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-118">There are two types of activities: [Data Movement Activities](../data-factory/data-factory-data-movement-activities.md) and [Data Transformation Activities](../data-factory/data-factory-data-transformation-activities.md).</span></span> <span data-ttu-id="54cbf-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span><span class="sxs-lookup"><span data-stu-id="54cbf-119">You use data movement activities (currently, only Copy Activity) to move data from a source data store to a destination data store.</span></span> <span data-ttu-id="54cbf-120">You use data transformation activities to transform/process data.</span><span class="sxs-lookup"><span data-stu-id="54cbf-120">You use data transformation activities to transform/process data.</span></span> <span data-ttu-id="54cbf-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-121">HDInsight Hive Activity is one of the transformation activities supported by Data Factory.</span></span> <span data-ttu-id="54cbf-122">You use the Hive transformation activity in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="54cbf-122">You use the Hive transformation activity in this tutorial.</span></span> 

<span data-ttu-id="54cbf-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-123">You can configure a hive activity to use your own HDInsight Hadoop cluster or an on-demand HDInsight Hadoop cluster.</span></span> <span data-ttu-id="54cbf-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-124">In this tutorial, the Hive activity in the data factory pipeline is configured to use an on-demand HDInsight cluster.</span></span> <span data-ttu-id="54cbf-125">Therefore, when the activity runs to process a data slice, here is what happens:</span><span class="sxs-lookup"><span data-stu-id="54cbf-125">Therefore, when the activity runs to process a data slice, here is what happens:</span></span> 

1. <span data-ttu-id="54cbf-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span><span class="sxs-lookup"><span data-stu-id="54cbf-126">A HDInsight Hadoop cluster is automatically created for you just-in-time to process the slice.</span></span>  
2. <span data-ttu-id="54cbf-127">The input data is processed by running a HiveQL script on the cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-127">The input data is processed by running a HiveQL script on the cluster.</span></span> 
3. <span data-ttu-id="54cbf-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span><span class="sxs-lookup"><span data-stu-id="54cbf-128">The HDInsight Hadoop cluster is deleted after the processing is complete and the cluster is idle for the configured amount of time (timeToLive setting).</span></span> <span data-ttu-id="54cbf-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span><span class="sxs-lookup"><span data-stu-id="54cbf-129">If the next data slice is available for processing with in this timeToLive idle time, the same cluster is used to process the slice.</span></span>  
      
<span data-ttu-id="54cbf-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span><span class="sxs-lookup"><span data-stu-id="54cbf-130">In this tutorial, the HiveQL script associated with the hive activity performs the following actions:</span></span> 

1. <span data-ttu-id="54cbf-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-131">Creates an external table that references the raw web log data stored in an Azure Blob storage.</span></span>
2. <span data-ttu-id="54cbf-132">Partitions the raw data by year and month.</span><span class="sxs-lookup"><span data-stu-id="54cbf-132">Partitions the raw data by year and month.</span></span>
3. <span data-ttu-id="54cbf-133">Stores the partitioned data in the Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-133">Stores the partitioned data in the Azure blob storage.</span></span> 

<span data-ttu-id="54cbf-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-134">In this tutorial, the HiveQL script associated with the hive activity creates an external table that references the raw web log data stored in the Azure Blob Storage.</span></span> <span data-ttu-id="54cbf-135">Here are the sample rows for each month in the input file.</span><span class="sxs-lookup"><span data-stu-id="54cbf-135">Here are the sample rows for each month in the input file.</span></span>

```
2014-01-01,02:01:09,SAMPLEWEBSITE,GET,/blogposts/mvc4/step2.png,X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,53175,871
2014-02-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
2014-03-01,02:01:10,SAMPLEWEBSITE,GET,/blogposts/mvc4/step7.png,X-ARR-LOG-ID=d7472a26-431a-4a4d-99eb-c7b4fda2cf4c,80,-,1.54.23.196,Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36,-,http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx,\N,200,0,0,30184,871
```

<span data-ttu-id="54cbf-136">The HiveQL script partitions the raw data by year and month.</span><span class="sxs-lookup"><span data-stu-id="54cbf-136">The HiveQL script partitions the raw data by year and month.</span></span> <span data-ttu-id="54cbf-137">It creates three output folders based on the previous input.</span><span class="sxs-lookup"><span data-stu-id="54cbf-137">It creates three output folders based on the previous input.</span></span> <span data-ttu-id="54cbf-138">Each folder contains a file with entries from each month.</span><span class="sxs-lookup"><span data-stu-id="54cbf-138">Each folder contains a file with entries from each month.</span></span>

```
adfgetstarted/partitioneddata/year=2014/month=1/000000_0
adfgetstarted/partitioneddata/year=2014/month=2/000000_0
adfgetstarted/partitioneddata/year=2014/month=3/000000_0
```

<span data-ttu-id="54cbf-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-139">For a list of Data Factory data transformation activities in addition to Hive activity, see [Transform and analyze using Azure Data Factory](../data-factory/data-factory-data-transformation-activities.md).</span></span>

> [!NOTE]
> <span data-ttu-id="54cbf-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-140">Currently, you can only create HDInsight cluster version 3.2 from Azure Data Factory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="54cbf-141">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="54cbf-141">Prerequisites</span></span>
<span data-ttu-id="54cbf-142">Before you begin the instructions in this article, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="54cbf-142">Before you begin the instructions in this article, you must have the following items:</span></span>

* <span data-ttu-id="54cbf-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="54cbf-143">[Azure subscription](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="54cbf-144">Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="54cbf-144">Azure PowerShell.</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

### <a name="prepare-storage-account"></a><span data-ttu-id="54cbf-145">Prepare storage account</span><span class="sxs-lookup"><span data-stu-id="54cbf-145">Prepare storage account</span></span>
<span data-ttu-id="54cbf-146">You can use up to three storage accounts in this scenario:</span><span class="sxs-lookup"><span data-stu-id="54cbf-146">You can use up to three storage accounts in this scenario:</span></span>

- <span data-ttu-id="54cbf-147">default storage account for the HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="54cbf-147">default storage account for the HDInsight cluster</span></span>
- <span data-ttu-id="54cbf-148">storage account for the input data</span><span class="sxs-lookup"><span data-stu-id="54cbf-148">storage account for the input data</span></span>
- <span data-ttu-id="54cbf-149">storage account for the output data</span><span class="sxs-lookup"><span data-stu-id="54cbf-149">storage account for the output data</span></span>

<span data-ttu-id="54cbf-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span><span class="sxs-lookup"><span data-stu-id="54cbf-150">To simplify the tutorial, you use one storage account to serve the three purposes.</span></span> <span data-ttu-id="54cbf-151">The Azure PowerShell sample script found in this section performs the following tasks:</span><span class="sxs-lookup"><span data-stu-id="54cbf-151">The Azure PowerShell sample script found in this section performs the following tasks:</span></span>

1. <span data-ttu-id="54cbf-152">Log in to Azure.</span><span class="sxs-lookup"><span data-stu-id="54cbf-152">Log in to Azure.</span></span>
2. <span data-ttu-id="54cbf-153">Create an Azure resource group.</span><span class="sxs-lookup"><span data-stu-id="54cbf-153">Create an Azure resource group.</span></span>
3. <span data-ttu-id="54cbf-154">Create an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-154">Create an Azure Storage account.</span></span>
4. <span data-ttu-id="54cbf-155">Create a Blob container in the storage account</span><span class="sxs-lookup"><span data-stu-id="54cbf-155">Create a Blob container in the storage account</span></span>
5. <span data-ttu-id="54cbf-156">Copy the following two files to the Blob container:</span><span class="sxs-lookup"><span data-stu-id="54cbf-156">Copy the following two files to the Blob container:</span></span>

   * <span data-ttu-id="54cbf-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span><span class="sxs-lookup"><span data-stu-id="54cbf-157">Input data file: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log)</span></span>
   * <span data-ttu-id="54cbf-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span><span class="sxs-lookup"><span data-stu-id="54cbf-158">HiveQL script: [https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql](https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql)</span></span>

     <span data-ttu-id="54cbf-159">Both files are stored in a public Blob container.</span><span class="sxs-lookup"><span data-stu-id="54cbf-159">Both files are stored in a public Blob container.</span></span>


<span data-ttu-id="54cbf-160">**To prepare the storage and copy the files using Azure PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="54cbf-160">**To prepare the storage and copy the files using Azure PowerShell:**</span></span>
> [!IMPORTANT]
> <span data-ttu-id="54cbf-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span><span class="sxs-lookup"><span data-stu-id="54cbf-161">Specify names for the Azure resource group and the Azure storage account that will be created by the script.</span></span>
> <span data-ttu-id="54cbf-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span><span class="sxs-lookup"><span data-stu-id="54cbf-162">Write down **resource group name**, **storage account name**, and **storage account key** outputted by the script.</span></span> <span data-ttu-id="54cbf-163">You need them in the next section.</span><span class="sxs-lookup"><span data-stu-id="54cbf-163">You need them in the next section.</span></span>

```powershell
$resourceGroupName = "<Azure Resource Group Name>"
$storageAccountName = "<Azure Storage Account Name>"
$location = "East US 2"

$sourceStorageAccountName = "hditutorialdata"  
$sourceContainerName = "adfhiveactivity"

$destStorageAccountName = $storageAccountName
$destContainerName = "adfgetstarted" # don't change this value.

####################################
# Connect to Azure
####################################
#region - Connect to Azure subscription
Write-Host "`nConnecting to your Azure subscription ..." -ForegroundColor Green
try{Get-AzureRmContext}
catch{Login-AzureRmAccount}
#endregion

####################################
# Create a resource group, storage, and container
####################################

#region - create Azure resources
Write-Host "`nCreating resource group, storage account and blob container ..." -ForegroundColor Green

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmStorageAccount `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName `
    -type Standard_LRS `
    -Location $location

$destStorageAccountKey = (Get-AzureRmStorageAccountKey `
    -ResourceGroupName $resourceGroupName `
    -Name $destStorageAccountName)[0].Value

$sourceContext = New-AzureStorageContext `
    -StorageAccountName $sourceStorageAccountName `
    -Anonymous
$destContext = New-AzureStorageContext `
    -StorageAccountName $destStorageAccountName `
    -StorageAccountKey $destStorageAccountKey

New-AzureStorageContainer -Name $destContainerName -Context $destContext
#endregion

####################################
# Copy files
####################################
#region - copy files
Write-Host "`nCopying files ..." -ForegroundColor Green

$blobs = Get-AzureStorageBlob `
    -Context $sourceContext `
    -Container $sourceContainerName

$blobs|Start-AzureStorageBlobCopy `
    -DestContext $destContext `
    -DestContainer $destContainerName

Write-Host "`nCopied files ..." -ForegroundColor Green
Get-AzureStorageBlob -Context $destContext -Container $destContainerName
#endregion

Write-host "`nYou will use the following values:" -ForegroundColor Green
write-host "`nResource group name: $resourceGroupName"
Write-host "Storage Account Name: $destStorageAccountName"
write-host "Storage Account Key: $destStorageAccountKey"

Write-host "`nScript completed" -ForegroundColor Green
```

<span data-ttu-id="54cbf-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-164">If you need help with the PowerShell script, see [Using the Azure PowerShell with Azure Storage](../storage/storage-powershell-guide-full.md).</span></span> <span data-ttu-id="54cbf-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span><span class="sxs-lookup"><span data-stu-id="54cbf-165">If you like to use Azure CLI instead, see the [Appendix](#appendix) section for the Azure CLI script.</span></span>

<span data-ttu-id="54cbf-166">**To examine the storage account and the contents**</span><span class="sxs-lookup"><span data-stu-id="54cbf-166">**To examine the storage account and the contents**</span></span>

1. <span data-ttu-id="54cbf-167">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54cbf-167">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54cbf-168">Click **Resource groups** on the left pane.</span><span class="sxs-lookup"><span data-stu-id="54cbf-168">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="54cbf-169">Double-click the resource group name you created in your PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="54cbf-169">Double-click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="54cbf-170">Use the filter if you have too many resource groups listed.</span><span class="sxs-lookup"><span data-stu-id="54cbf-170">Use the filter if you have too many resource groups listed.</span></span>
4. <span data-ttu-id="54cbf-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span><span class="sxs-lookup"><span data-stu-id="54cbf-171">On the **Resources** tile, you shall have one resource listed unless you share the resource group with other projects.</span></span> <span data-ttu-id="54cbf-172">That resource is the storage account with the name you specified earlier.</span><span class="sxs-lookup"><span data-stu-id="54cbf-172">That resource is the storage account with the name you specified earlier.</span></span> <span data-ttu-id="54cbf-173">Click the storage account name.</span><span class="sxs-lookup"><span data-stu-id="54cbf-173">Click the storage account name.</span></span>
5. <span data-ttu-id="54cbf-174">Click the **Blobs** tiles.</span><span class="sxs-lookup"><span data-stu-id="54cbf-174">Click the **Blobs** tiles.</span></span>
6. <span data-ttu-id="54cbf-175">Click the **adfgetstarted** container.</span><span class="sxs-lookup"><span data-stu-id="54cbf-175">Click the **adfgetstarted** container.</span></span> <span data-ttu-id="54cbf-176">You see two folders: **inputdata** and **script**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-176">You see two folders: **inputdata** and **script**.</span></span> 
7. <span data-ttu-id="54cbf-177">Open the folder and check the files in the folders.</span><span class="sxs-lookup"><span data-stu-id="54cbf-177">Open the folder and check the files in the folders.</span></span> <span data-ttu-id="54cbf-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span><span class="sxs-lookup"><span data-stu-id="54cbf-178">The inputdata contains the input.log file with input data and the script folder contains the HiveQL script file.</span></span> 

## <a name="create-a-data-factory-using-resource-manager-template"></a><span data-ttu-id="54cbf-179">Create a data factory using Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="54cbf-179">Create a data factory using Resource Manager template</span></span>
<span data-ttu-id="54cbf-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-180">With the storage account, the input data, and the HiveQL script prepared, you are ready to create an Azure data factory.</span></span> <span data-ttu-id="54cbf-181">There are several methods for creating data factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-181">There are several methods for creating data factory.</span></span> <span data-ttu-id="54cbf-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54cbf-182">In this tutorial, you create a data factory by deploying an Azure Resource Manager template using the Azure portal.</span></span> <span data-ttu-id="54cbf-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy).</span><span class="sxs-lookup"><span data-stu-id="54cbf-183">You can also deploy a Resource Manager template by using [Azure CLI](../azure-resource-manager/resource-group-template-deploy-cli.md) and [Azure PowerShell](../azure-resource-manager/resource-group-template-deploy.md#deploy).</span></span> <span data-ttu-id="54cbf-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-184">For other data factory creation methods, see [Tutorial: Build your first data factory](../data-factory/data-factory-build-your-first-pipeline.md).</span></span>

1. <span data-ttu-id="54cbf-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="54cbf-185">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> <span data-ttu-id="54cbf-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span><span class="sxs-lookup"><span data-stu-id="54cbf-186">The template is located at https://hditutorialdata.blob.core.windows.net/adfhiveactivity/data-factory-hdinsight-on-demand.json.</span></span> <span data-ttu-id="54cbf-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-187">See the [Data Factory entities in the template](#data-factory-entities-in-the-template) section for detailed information about entities defined in the template.</span></span> 

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fadfhiveactivity%2Fdata-factory-hdinsight-on-demand.json" target="_blank"><img src="https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-adf/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="54cbf-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span><span class="sxs-lookup"><span data-stu-id="54cbf-188">Select **Use existing** option for the **Resource group** setting, and select the name of the resource group you created in the previous step (using PowerShell script).</span></span> 
3. <span data-ttu-id="54cbf-189">Enter a name for the data factory (**Data Factory Name**).</span><span class="sxs-lookup"><span data-stu-id="54cbf-189">Enter a name for the data factory (**Data Factory Name**).</span></span> <span data-ttu-id="54cbf-190">This name must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="54cbf-190">This name must be globally unique.</span></span>
4. <span data-ttu-id="54cbf-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span><span class="sxs-lookup"><span data-stu-id="54cbf-191">Enter the **storage account name** and **storage account key** you wrote down in the previous step.</span></span>
5. <span data-ttu-id="54cbf-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-192">Select **I agree to the terms and conditions** stated above after reading through **terms and conditions**.</span></span>
6. <span data-ttu-id="54cbf-193">Select **Pin to dashboard** option.</span><span class="sxs-lookup"><span data-stu-id="54cbf-193">Select **Pin to dashboard** option.</span></span> 
6. <span data-ttu-id="54cbf-194">Click **Purchase/Create**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-194">Click **Purchase/Create**.</span></span> <span data-ttu-id="54cbf-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-195">You see a tile on the Dashboard called **Deploying Template deployment**.</span></span> <span data-ttu-id="54cbf-196">Wait until the **Resource group** blade for your resource group opens.</span><span class="sxs-lookup"><span data-stu-id="54cbf-196">Wait until the **Resource group** blade for your resource group opens.</span></span> <span data-ttu-id="54cbf-197">You can also click the tile titled as your resource group name to open the resource group blade.</span><span class="sxs-lookup"><span data-stu-id="54cbf-197">You can also click the tile titled as your resource group name to open the resource group blade.</span></span> 
6. <span data-ttu-id="54cbf-198">Click the tile to open the resource group if the resource group blade is not already open.</span><span class="sxs-lookup"><span data-stu-id="54cbf-198">Click the tile to open the resource group if the resource group blade is not already open.</span></span> <span data-ttu-id="54cbf-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span><span class="sxs-lookup"><span data-stu-id="54cbf-199">Now you shall see one more data factory resource listed in addition to the storage account resource.</span></span>
7. <span data-ttu-id="54cbf-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span><span class="sxs-lookup"><span data-stu-id="54cbf-200">Click the name of your data factory (value you specified for the **Data Factory Name** parameter).</span></span>
8. <span data-ttu-id="54cbf-201">In the Data Factory blade, click the **Diagram** tile.</span><span class="sxs-lookup"><span data-stu-id="54cbf-201">In the Data Factory blade, click the **Diagram** tile.</span></span> <span data-ttu-id="54cbf-202">The diagram shows one activity with an input dataset, and an output dataset:</span><span class="sxs-lookup"><span data-stu-id="54cbf-202">The diagram shows one activity with an input dataset, and an output dataset:</span></span>

    ![Azure Data Factory HDInsight on-demand Hive activity pipeline diagram](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-pipeline-diagram.png)

    <span data-ttu-id="54cbf-204">The names are defined in the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-204">The names are defined in the Resource Manager template.</span></span>
9. <span data-ttu-id="54cbf-205">Double-click **AzureBlobOutput**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-205">Double-click **AzureBlobOutput**.</span></span>
10. <span data-ttu-id="54cbf-206">On the **Recent updated slices**, you shall see one slice.</span><span class="sxs-lookup"><span data-stu-id="54cbf-206">On the **Recent updated slices**, you shall see one slice.</span></span> <span data-ttu-id="54cbf-207">If the status is **In progress**, wait until it is changed to **Ready**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-207">If the status is **In progress**, wait until it is changed to **Ready**.</span></span> <span data-ttu-id="54cbf-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-208">It usually takes about **20 minutes** to create an HDInsight cluster.</span></span> 

### <a name="check-the-data-factory-output"></a><span data-ttu-id="54cbf-209">Check the data factory output</span><span class="sxs-lookup"><span data-stu-id="54cbf-209">Check the data factory output</span></span>

1. <span data-ttu-id="54cbf-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span><span class="sxs-lookup"><span data-stu-id="54cbf-210">Use the same procedure in the last session to check the containers of the adfgetstarted container.</span></span> <span data-ttu-id="54cbf-211">There are two new containers in addition to **adfgetsarted**:</span><span class="sxs-lookup"><span data-stu-id="54cbf-211">There are two new containers in addition to **adfgetsarted**:</span></span>

   * <span data-ttu-id="54cbf-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="54cbf-212">A container with name that follows the pattern: `adf<yourdatafactoryname>-linkedservicename-datetimestamp`.</span></span> <span data-ttu-id="54cbf-213">This container is the default container for the HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-213">This container is the default container for the HDInsight cluster.</span></span> 
   * <span data-ttu-id="54cbf-214">adfjobs: This container is the container for the ADF job logs.</span><span class="sxs-lookup"><span data-stu-id="54cbf-214">adfjobs: This container is the container for the ADF job logs.</span></span>

     <span data-ttu-id="54cbf-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-215">The data factory output is stored in **afgetstarted** as you configured in the Resource Manager template.</span></span>
2. <span data-ttu-id="54cbf-216">Click **adfgetstarted**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-216">Click **adfgetstarted**.</span></span>
3. <span data-ttu-id="54cbf-217">Double-click **partitioneddata**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-217">Double-click **partitioneddata**.</span></span> <span data-ttu-id="54cbf-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span><span class="sxs-lookup"><span data-stu-id="54cbf-218">You see a **year=2014** folder because all the web logs are dated in year 2014.</span></span>

    ![Azure Data Factory HDInsight on-demand Hive activity pipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-year.png)

    <span data-ttu-id="54cbf-220">If you drill down the list, you shall see three folders for January, February, and March.</span><span class="sxs-lookup"><span data-stu-id="54cbf-220">If you drill down the list, you shall see three folders for January, February, and March.</span></span> <span data-ttu-id="54cbf-221">And there is a log for each month.</span><span class="sxs-lookup"><span data-stu-id="54cbf-221">And there is a log for each month.</span></span>

    ![Azure Data Factory HDInsight on-demand Hive activity pipeline output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/hdinsight/media/hdinsight-hadoop-create-linux-clusters-adf/hdinsight-adf-output-month.png)

## <a name="data-factory-entities-in-the-template"></a><span data-ttu-id="54cbf-223">Data Factory entities in the template</span><span class="sxs-lookup"><span data-stu-id="54cbf-223">Data Factory entities in the template</span></span>
<span data-ttu-id="54cbf-224">Here is how the top-level Resource Manager template for a data factory looks like:</span><span class="sxs-lookup"><span data-stu-id="54cbf-224">Here is how the top-level Resource Manager template for a data factory looks like:</span></span> 

```json
{
    "contentVersion": "1.0.0.0",
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "parameters": { ...
    },
    "variables": { ...
    },
    "resources": [
        {
            "name": "[parameters('dataFactoryName')]",
            "apiVersion": "[variables('apiVersion')]",
            "type": "Microsoft.DataFactory/datafactories",
            "location": "westus",
            "resources": [
                { ... },
                { ... },
                { ... },
                { ... }
            ]
        }
    ]
}
```

### <a name="define-data-factory"></a><span data-ttu-id="54cbf-225">Define data factory</span><span class="sxs-lookup"><span data-stu-id="54cbf-225">Define data factory</span></span>
<span data-ttu-id="54cbf-226">You define a data factory in the Resource Manager template as shown in the following sample:</span><span class="sxs-lookup"><span data-stu-id="54cbf-226">You define a data factory in the Resource Manager template as shown in the following sample:</span></span>  

```json
"resources": [
{
    "name": "[parameters('dataFactoryName')]",
    "apiVersion": "[variables('apiVersion')]",
    "type": "Microsoft.DataFactory/datafactories",
    "location": "westus",
}
```
<span data-ttu-id="54cbf-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-227">The dataFactoryName is the name of the data factory you specify when you deploy the template.</span></span> <span data-ttu-id="54cbf-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span><span class="sxs-lookup"><span data-stu-id="54cbf-228">Data factory is currently only supported in the East US, West US, and North Europe regions.</span></span>
   
### <a name="defining-entities-within-the-data-factory"></a><span data-ttu-id="54cbf-229">Defining entities within the data factory</span><span class="sxs-lookup"><span data-stu-id="54cbf-229">Defining entities within the data factory</span></span>
<span data-ttu-id="54cbf-230">The following Data Factory entities are defined in the JSON template:</span><span class="sxs-lookup"><span data-stu-id="54cbf-230">The following Data Factory entities are defined in the JSON template:</span></span> 

* [<span data-ttu-id="54cbf-231">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="54cbf-231">Azure Storage linked service</span></span>](#azure-storage-linked-service)
* [<span data-ttu-id="54cbf-232">HDInsight on-demand linked service</span><span class="sxs-lookup"><span data-stu-id="54cbf-232">HDInsight on-demand linked service</span></span>](#hdinsight-on-demand-linked-service)
* [<span data-ttu-id="54cbf-233">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="54cbf-233">Azure blob input dataset</span></span>](#azure-blob-input-dataset)
* [<span data-ttu-id="54cbf-234">Azure blob output dataset</span><span class="sxs-lookup"><span data-stu-id="54cbf-234">Azure blob output dataset</span></span>](#azure-blob-output-dataset)
* [<span data-ttu-id="54cbf-235">Data pipeline with a copy activity</span><span class="sxs-lookup"><span data-stu-id="54cbf-235">Data pipeline with a copy activity</span></span>](#data-pipeline)

#### <a name="azure-storage-linked-service"></a><span data-ttu-id="54cbf-236">Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="54cbf-236">Azure Storage linked service</span></span>
<span data-ttu-id="54cbf-237">The Azure Storage linked service links your Azure storage account to the data factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-237">The Azure Storage linked service links your Azure storage account to the data factory.</span></span> <span data-ttu-id="54cbf-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-238">In this tutorial, the same storage account is used as the default HDInsight storage account, input data storage, and output data storage.</span></span> <span data-ttu-id="54cbf-239">Therefore, you define only one Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="54cbf-239">Therefore, you define only one Azure Storage linked service.</span></span> <span data-ttu-id="54cbf-240">In the linked service definition, you specify the name and key of your Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-240">In the linked service definition, you specify the name and key of your Azure storage account.</span></span> <span data-ttu-id="54cbf-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="54cbf-241">See [Azure Storage linked service](../data-factory/data-factory-azure-blob-connector.md#azure-storage-linked-service) for details about JSON properties used to define an Azure Storage linked service.</span></span> 

```json
{
    "name": "[variables('storageLinkedServiceName')]",
    "type": "linkedservices",
    "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('storageAccountName'),';AccountKey=',parameters('storageAccountKey'))]"
        }
    }
}
```
<span data-ttu-id="54cbf-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span><span class="sxs-lookup"><span data-stu-id="54cbf-242">The **connectionString** uses the storageAccountName and storageAccountKey parameters.</span></span> <span data-ttu-id="54cbf-243">You specify values for these parameters while deploying the template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-243">You specify values for these parameters while deploying the template.</span></span>  

#### <a name="hdinsight-on-demand-linked-service"></a><span data-ttu-id="54cbf-244">HDInsight on-demand linked service</span><span class="sxs-lookup"><span data-stu-id="54cbf-244">HDInsight on-demand linked service</span></span>
<span data-ttu-id="54cbf-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span><span class="sxs-lookup"><span data-stu-id="54cbf-245">In the on-demand HDInsight linked service definition, you specify values for configuration parameters that are used by the Data Factory service to create a HDInsight Hadoop cluster at runtime.</span></span> <span data-ttu-id="54cbf-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span><span class="sxs-lookup"><span data-stu-id="54cbf-246">See [Compute linked services](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) article for details about JSON properties used to define an HDInsight on-demand linked service.</span></span>  

```json

{
    "type": "linkedservices",
    "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "HDInsightOnDemand",
        "typeProperties": {
            "osType": "linux",
            "version": "3.2",
            "clusterSize": 1,
            "sshUserName": "myuser",                            
            "sshPassword": "MyPassword!",
            "timeToLive": "00:30:00",
            "linkedServiceName": "[variables('storageLinkedServiceName')]"
        }
    }
}
```
<span data-ttu-id="54cbf-247">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="54cbf-247">Note the following points:</span></span> 

* <span data-ttu-id="54cbf-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span><span class="sxs-lookup"><span data-stu-id="54cbf-248">The Data Factory creates a **Linux-based** HDInsight cluster for you.</span></span>
* <span data-ttu-id="54cbf-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-249">The HDInsight Hadoop cluster is created in the same region as the storage account.</span></span>
* <span data-ttu-id="54cbf-250">Notice the *timeToLive* setting.</span><span class="sxs-lookup"><span data-stu-id="54cbf-250">Notice the *timeToLive* setting.</span></span> <span data-ttu-id="54cbf-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="54cbf-251">The data factory deletes the cluster automatically after the cluster is being idle for 30 minutes.</span></span>
* <span data-ttu-id="54cbf-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span><span class="sxs-lookup"><span data-stu-id="54cbf-252">The HDInsight cluster creates a **default container** in the blob storage you specified in the JSON (**linkedServiceName**).</span></span> <span data-ttu-id="54cbf-253">HDInsight does not delete this container when the cluster is deleted.</span><span class="sxs-lookup"><span data-stu-id="54cbf-253">HDInsight does not delete this container when the cluster is deleted.</span></span> <span data-ttu-id="54cbf-254">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="54cbf-254">This behavior is by design.</span></span> <span data-ttu-id="54cbf-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="54cbf-255">With on-demand HDInsight linked service, a HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (**timeToLive**) and is deleted when the processing is done.</span></span>

<span data-ttu-id="54cbf-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span><span class="sxs-lookup"><span data-stu-id="54cbf-256">See [On-demand HDInsight Linked Service](../data-factory/data-factory-compute-linked-services.md#azure-hdinsight-on-demand-linked-service) for details.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54cbf-257">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-257">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="54cbf-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="54cbf-258">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="54cbf-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span><span class="sxs-lookup"><span data-stu-id="54cbf-259">The names of these containers follow a pattern: "adf**yourdatafactoryname**-**linkedservicename**-datetimestamp".</span></span> <span data-ttu-id="54cbf-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-260">Use tools such as [Microsoft Storage Explorer](http://storageexplorer.com/) to delete containers in your Azure blob storage.</span></span>

#### <a name="azure-blob-input-dataset"></a><span data-ttu-id="54cbf-261">Azure blob input dataset</span><span class="sxs-lookup"><span data-stu-id="54cbf-261">Azure blob input dataset</span></span>
<span data-ttu-id="54cbf-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span><span class="sxs-lookup"><span data-stu-id="54cbf-262">In the input dataset definition, you specify the names of blob container, folder, and file that contains the input data.</span></span> <span data-ttu-id="54cbf-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="54cbf-263">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span> 

```json

{
    "type": "datasets",
    "name": "[variables('blobInputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}

```

<span data-ttu-id="54cbf-264">Notice the following specific settings in the JSON definition:</span><span class="sxs-lookup"><span data-stu-id="54cbf-264">Notice the following specific settings in the JSON definition:</span></span> 

```json
"fileName": "input.log",
"folderPath": "adfgetstarted/inputdata",
```

#### <a name="azure-blob-output-dataset"></a><span data-ttu-id="54cbf-265">Azure Blob output dataset</span><span class="sxs-lookup"><span data-stu-id="54cbf-265">Azure Blob output dataset</span></span>
<span data-ttu-id="54cbf-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span><span class="sxs-lookup"><span data-stu-id="54cbf-266">In the output dataset definition, you specify the names of blob container and folder that holds the output data.</span></span> <span data-ttu-id="54cbf-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span><span class="sxs-lookup"><span data-stu-id="54cbf-267">See [Azure Blob dataset properties](../data-factory/data-factory-azure-blob-connector.md#dataset-properties) for details about JSON properties used to define an Azure Blob dataset.</span></span>  

```json

{
    "type": "datasets",
    "name": "[variables('blobOutputDatasetName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "[variables('storageLinkedServiceName')]",
        "typeProperties": {
            "folderPath": "adfgetstarted/partitioneddata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Month",
            "interval": 1,
            "style": "EndOfInterval"
        }
    }
}
```

<span data-ttu-id="54cbf-268">The folderPath specifies the path to the folder that holds the output data:</span><span class="sxs-lookup"><span data-stu-id="54cbf-268">The folderPath specifies the path to the folder that holds the output data:</span></span> 

```json
"folderPath": "adfgetstarted/partitioneddata",
```

<span data-ttu-id="54cbf-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#Availability) setting is as follows:</span><span class="sxs-lookup"><span data-stu-id="54cbf-269">The [dataset availability](../data-factory/data-factory-create-datasets.md#Availability) setting is as follows:</span></span>

```json
"availability": {
    "frequency": "Month",
    "interval": 1,
    "style": "EndOfInterval"
},
```

<span data-ttu-id="54cbf-270">In Azure Data Factory, output dataset availability drives the pipeline.</span><span class="sxs-lookup"><span data-stu-id="54cbf-270">In Azure Data Factory, output dataset availability drives the pipeline.</span></span> <span data-ttu-id="54cbf-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span><span class="sxs-lookup"><span data-stu-id="54cbf-271">In this example, the slice is produced monthly on the last day of month (EndOfInterval).</span></span> <span data-ttu-id="54cbf-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-272">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

#### <a name="data-pipeline"></a><span data-ttu-id="54cbf-273">Data pipeline</span><span class="sxs-lookup"><span data-stu-id="54cbf-273">Data pipeline</span></span>
<span data-ttu-id="54cbf-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-274">You define a pipeline that transforms data by running Hive script on an on-demand Azure HDInsight cluster.</span></span> <span data-ttu-id="54cbf-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span><span class="sxs-lookup"><span data-stu-id="54cbf-275">See [Pipeline JSON](../data-factory/data-factory-create-pipelines.md#pipeline-json) for descriptions of JSON elements used to define a pipeline in this example.</span></span> 

```json
{
    "type": "datapipelines",
    "name": "[parameters('dataFactoryName')]",
    "dependsOn": [
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('storageLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedServices/', variables('hdInsightOnDemandLinkedServiceName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobInputDatasetName'))]",
        "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/datasets/', variables('blobOutputDatasetName'))]"
    ],
    "apiVersion": "[variables('apiVersion')]",
    "properties": {
        "description": "Azure Data Factory pipeline with an Hadoop Hive activity",
        "activities": [
            {
                "type": "HDInsightHive",
                "typeProperties": {
                    "scriptPath": "adfgetstarted/script/partitionweblogs.hql",
                    "scriptLinkedService": "[variables('storageLinkedServiceName')]",
                    "defines": {
                        "inputtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/inputdata')]",
                        "partitionedtable": "[concat('wasb://adfgetstarted@', parameters('storageAccountName'), '.blob.core.windows.net/partitioneddata')]"
                    }
                },
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "policy": {
                    "concurrency": 1,
                    "retry": 3
                },
                "name": "RunSampleHiveActivity",
                "linkedServiceName": "HDInsightOnDemandLinkedService"
            }
        ],
        "start": "2016-01-01T00:00:00Z",
        "end": "2016-01-31T00:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="54cbf-276">The pipeline contains one activity, HDInsightHive activity.</span><span class="sxs-lookup"><span data-stu-id="54cbf-276">The pipeline contains one activity, HDInsightHive activity.</span></span> <span data-ttu-id="54cbf-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span><span class="sxs-lookup"><span data-stu-id="54cbf-277">As both start and end dates are in January 2016, data for only one month (a slice) is processed.</span></span> <span data-ttu-id="54cbf-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span><span class="sxs-lookup"><span data-stu-id="54cbf-278">Both *start* and *end* of the activity have a past date, so the Data Factory processes data for the month immediately.</span></span> <span data-ttu-id="54cbf-279">If the end is a future date, the data factory creates another slice when the time comes.</span><span class="sxs-lookup"><span data-stu-id="54cbf-279">If the end is a future date, the data factory creates another slice when the time comes.</span></span> <span data-ttu-id="54cbf-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-280">For more information, see [Data Factory Scheduling and Execution](../data-factory/data-factory-scheduling-and-execution.md).</span></span>

## <a name="clean-up-the-tutorial"></a><span data-ttu-id="54cbf-281">Clean up the tutorial</span><span class="sxs-lookup"><span data-stu-id="54cbf-281">Clean up the tutorial</span></span>

### <a name="delete-the-blob-containers-created-by-on-demand-hdinsight-cluster"></a><span data-ttu-id="54cbf-282">Delete the blob containers created by on-demand HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="54cbf-282">Delete the blob containers created by on-demand HDInsight cluster</span></span>
<span data-ttu-id="54cbf-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span><span class="sxs-lookup"><span data-stu-id="54cbf-283">With on-demand HDInsight linked service, an HDInsight cluster is created every time a slice needs to be processed unless there is an existing live cluster (timeToLive); and the cluster is deleted when the processing is done.</span></span> <span data-ttu-id="54cbf-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span><span class="sxs-lookup"><span data-stu-id="54cbf-284">For each cluster, Azure Data Factory creates a blob container in the Azure blob storage used as the default stroage account for the cluster.</span></span> <span data-ttu-id="54cbf-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span><span class="sxs-lookup"><span data-stu-id="54cbf-285">Even though HDInsight cluster is deleted, the default blob storage container and the associated storage account are not deleted.</span></span> <span data-ttu-id="54cbf-286">This behavior is by design.</span><span class="sxs-lookup"><span data-stu-id="54cbf-286">This behavior is by design.</span></span> <span data-ttu-id="54cbf-287">As more slices are processed, you see many containers in your Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="54cbf-287">As more slices are processed, you see many containers in your Azure blob storage.</span></span> <span data-ttu-id="54cbf-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span><span class="sxs-lookup"><span data-stu-id="54cbf-288">If you do not need them for troubleshooting of the jobs, you may want to delete them to reduce the storage cost.</span></span> <span data-ttu-id="54cbf-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span><span class="sxs-lookup"><span data-stu-id="54cbf-289">The names of these containers follow a pattern: `adfyourdatafactoryname-linkedservicename-datetimestamp`.</span></span>

<span data-ttu-id="54cbf-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span><span class="sxs-lookup"><span data-stu-id="54cbf-290">Delete the **adfjobs** and **adfyourdatafactoryname-linkedservicename-datetimestamp** folders.</span></span> <span data-ttu-id="54cbf-291">The adfjobs container contains job logs from Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-291">The adfjobs container contains job logs from Azure Data Factory.</span></span> 

### <a name="delete-the-resource-group"></a><span data-ttu-id="54cbf-292">Delete the resource group</span><span class="sxs-lookup"><span data-stu-id="54cbf-292">Delete the resource group</span></span>
<span data-ttu-id="54cbf-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span><span class="sxs-lookup"><span data-stu-id="54cbf-293">[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) is used to deploy, manage, and monitor your solution as a group.</span></span>  <span data-ttu-id="54cbf-294">Deleting a resource group deletes all the components inside the group.</span><span class="sxs-lookup"><span data-stu-id="54cbf-294">Deleting a resource group deletes all the components inside the group.</span></span>  

1. <span data-ttu-id="54cbf-295">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="54cbf-295">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="54cbf-296">Click **Resource groups** on the left pane.</span><span class="sxs-lookup"><span data-stu-id="54cbf-296">Click **Resource groups** on the left pane.</span></span>
3. <span data-ttu-id="54cbf-297">Click the resource group name you created in your PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="54cbf-297">Click the resource group name you created in your PowerShell script.</span></span> <span data-ttu-id="54cbf-298">Use the filter if you have too many resource groups listed.</span><span class="sxs-lookup"><span data-stu-id="54cbf-298">Use the filter if you have too many resource groups listed.</span></span> <span data-ttu-id="54cbf-299">It opens the resource group in a new blade.</span><span class="sxs-lookup"><span data-stu-id="54cbf-299">It opens the resource group in a new blade.</span></span>
4. <span data-ttu-id="54cbf-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span><span class="sxs-lookup"><span data-stu-id="54cbf-300">On the **Resources** tile, you shall have the default storage account and the data factory listed unless you share the resource group with other projects.</span></span>
5. <span data-ttu-id="54cbf-301">Click **Delete** on the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="54cbf-301">Click **Delete** on the top of the blade.</span></span> <span data-ttu-id="54cbf-302">Doing so deletes the storage account and the data stored in the storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-302">Doing so deletes the storage account and the data stored in the storage account.</span></span>
6. <span data-ttu-id="54cbf-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="54cbf-303">Enter the resource group name to confirm deletion, and then click **Delete**.</span></span>

<span data-ttu-id="54cbf-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-304">In case you don't want to delete the storage account when you delete the resource group, consider the following architecture by separating the business data from the default storage account.</span></span> <span data-ttu-id="54cbf-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span><span class="sxs-lookup"><span data-stu-id="54cbf-305">In this case, you have one resource group for the storage account with the business data, and the other resource group for the default storage account for HDInsight linked service and the data factory.</span></span> <span data-ttu-id="54cbf-306">When you delete the second resource group, it does not impact the business data storage account.</span><span class="sxs-lookup"><span data-stu-id="54cbf-306">When you delete the second resource group, it does not impact the business data storage account.</span></span> <span data-ttu-id="54cbf-307">To do so:</span><span class="sxs-lookup"><span data-stu-id="54cbf-307">To do so:</span></span>

* <span data-ttu-id="54cbf-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-308">Add the following to the top-level resource group along with the Microsoft.DataFactory/datafactories resource in your Resource Manager template.</span></span> <span data-ttu-id="54cbf-309">It creates a storage account:</span><span class="sxs-lookup"><span data-stu-id="54cbf-309">It creates a storage account:</span></span>

    ```json
    {
        "name": "[parameters('defaultStorageAccountName')]",
        "type": "Microsoft.Storage/storageAccounts",
        "location": "[parameters('location')]",
        "apiVersion": "[variables('defaultApiVersion')]",
        "dependsOn": [ ],
        "tags": {

        },
        "properties": {
            "accountType": "Standard_LRS"
        }
    },
    ```
* <span data-ttu-id="54cbf-310">Add a new linked service point to the new storage account:</span><span class="sxs-lookup"><span data-stu-id="54cbf-310">Add a new linked service point to the new storage account:</span></span>

    ```json
    {
        "dependsOn": [ "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]" ],
        "type": "linkedservices",
        "name": "[variables('defaultStorageLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "AzureStorage",
            "typeProperties": {
                "connectionString": "[concat('DefaultEndpointsProtocol=https;AccountName=',parameters('defaultStorageAccountName'),';AccountKey=',listKeys(resourceId('Microsoft.Storage/storageAccounts', variables('defaultStorageAccountName')), variables('defaultApiVersion')).key1)]"
            }
        }
    },
    ```
* <span data-ttu-id="54cbf-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span><span class="sxs-lookup"><span data-stu-id="54cbf-311">Configure the HDInsight ondemand linked service with an additional dependsOn and an additionalLinkedServiceNames:</span></span>

    ```json
    {
        "dependsOn": [
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('defaultStorageLinkedServiceName'))]",
            "[concat('Microsoft.DataFactory/dataFactories/', parameters('dataFactoryName'), '/linkedservices/', variables('storageLinkedServiceName'))]"

        ],
        "type": "linkedservices",
        "name": "[variables('hdInsightOnDemandLinkedServiceName')]",
        "apiVersion": "[variables('apiVersion')]",
        "properties": {
            "type": "HDInsightOnDemand",
            "typeProperties": {
                "osType": "linux",
                "version": "3.2",
                "clusterSize": 1,
                "sshUserName": "myuser",                            
                "sshPassword": "MyPassword!",
                "timeToLive": "00:30:00",
                "linkedServiceName": "[variables('storageLinkedServiceName')]",
                "additionalLinkedServiceNames": "[variables('defaultStorageLinkedServiceName')]"
            }
        }
    },            
    ```
## <a name="next-steps"></a><span data-ttu-id="54cbf-312">Next steps</span><span class="sxs-lookup"><span data-stu-id="54cbf-312">Next steps</span></span>
<span data-ttu-id="54cbf-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span><span class="sxs-lookup"><span data-stu-id="54cbf-313">In this article, you have learned how to use Azure Data Factory to create on-demand HDInsight cluster to process Hive jobs.</span></span> <span data-ttu-id="54cbf-314">To read more:</span><span class="sxs-lookup"><span data-stu-id="54cbf-314">To read more:</span></span>

* [<span data-ttu-id="54cbf-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="54cbf-315">Hadoop tutorial: Get started using Linux-based Hadoop in HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="54cbf-316">Create Linux-based Hadoop clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="54cbf-316">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="54cbf-317">HDInsight documentation</span><span class="sxs-lookup"><span data-stu-id="54cbf-317">HDInsight documentation</span></span>](https://azure.microsoft.com/documentation/services/hdinsight/)
* [<span data-ttu-id="54cbf-318">Data factory documentation</span><span class="sxs-lookup"><span data-stu-id="54cbf-318">Data factory documentation</span></span>](https://azure.microsoft.com/documentation/services/data-factory/)

## <a name="appendix"></a><span data-ttu-id="54cbf-319">Appendix</span><span class="sxs-lookup"><span data-stu-id="54cbf-319">Appendix</span></span>

### <a name="azure-cli-script"></a><span data-ttu-id="54cbf-320">Azure CLI script</span><span class="sxs-lookup"><span data-stu-id="54cbf-320">Azure CLI script</span></span>
<span data-ttu-id="54cbf-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span><span class="sxs-lookup"><span data-stu-id="54cbf-321">You can use Azure CLI instead of using Azure PowerShell to do the tutorial.</span></span> <span data-ttu-id="54cbf-322">To use Azure CLI, first install Azure CLI as per the following instructions: [!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]</span><span class="sxs-lookup"><span data-stu-id="54cbf-322">To use Azure CLI, first install Azure CLI as per the following instructions: [!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]</span></span>

#### <a name="use-azure-cli-to-prepare-the-storage-and-copy-the-files"></a><span data-ttu-id="54cbf-323">Use Azure CLI to prepare the storage and copy the files</span><span class="sxs-lookup"><span data-stu-id="54cbf-323">Use Azure CLI to prepare the storage and copy the files</span></span>

```
azure login

azure config mode arm

azure group create --name "<Azure Resource Group Name>" --location "East US 2"

azure storage account create --resource-group "<Azure Resource Group Name>" --location "East US 2" --type "LRS" <Azure Storage Account Name>

azure storage account keys list --resource-group "<Azure Resource Group Name>" "<Azure Storage Account Name>"
azure storage container create "adfgetstarted" --account-name "<Azure Storage AccountName>" --account-key "<Azure Storage Account Key>"

azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/inputdata/input.log" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
azure storage blob copy start "https://hditutorialdata.blob.core.windows.net/adfhiveactivity/script/partitionweblogs.hql" --dest-account-name "<Azure Storage Account Name>" --dest-account-key "<Azure Storage Account Key>" --dest-container "adfgetstarted"
```

<span data-ttu-id="54cbf-324">The container name is *adfgetstarted*.</span><span class="sxs-lookup"><span data-stu-id="54cbf-324">The container name is *adfgetstarted*.</span></span> <span data-ttu-id="54cbf-325">Keep it as it is.</span><span class="sxs-lookup"><span data-stu-id="54cbf-325">Keep it as it is.</span></span> <span data-ttu-id="54cbf-326">Otherwise you need to update the Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="54cbf-326">Otherwise you need to update the Resource Manager template.</span></span> <span data-ttu-id="54cbf-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="54cbf-327">If you need help with this CLI script, see [Using the Azure CLI with Azure Storage](../storage/storage-azure-cli.md).</span></span>





