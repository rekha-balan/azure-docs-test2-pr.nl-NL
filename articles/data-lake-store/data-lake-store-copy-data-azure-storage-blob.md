---
title: Copy data from Azure Storage Blobs into Data Lake Store| Microsoft Docs
description: Use AdlCopy tool to copy data from Azure Storage Blobs to Data Lake Store
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: dc273ef8-96ef-47a6-b831-98e8a777a5c1
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: ffbfbd2d5e3389a5898ad60a15b5c34070d4a1dc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552501"
---
# <a name="copy-data-from-azure-storage-blobs-to-data-lake-store"></a><span data-ttu-id="f9b9f-103">Copy data from Azure Storage Blobs to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9b9f-103">Copy data from Azure Storage Blobs to Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [Using DistCp](data-lake-store-copy-data-wasb-distcp.md)
> * [Using AdlCopy](data-lake-store-copy-data-azure-storage-blob.md)
> 
> 

<span data-ttu-id="f9b9f-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), to copy data from the following sources:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-106">Azure Data Lake Store provides a command line tool, [AdlCopy](http://aka.ms/downloadadlcopy), to copy data from the following sources:</span></span>

* <span data-ttu-id="f9b9f-107">From Azure Storage Blobs into Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-107">From Azure Storage Blobs into Data Lake Store.</span></span> <span data-ttu-id="f9b9f-108">You cannot use AdlCopy to copy data from Data Lake Store to Azure Storage blobs.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-108">You cannot use AdlCopy to copy data from Data Lake Store to Azure Storage blobs.</span></span>
* <span data-ttu-id="f9b9f-109">Between two Azure Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-109">Between two Azure Data Lake Store accounts.</span></span> 

<span data-ttu-id="f9b9f-110">Also, you can use the AdlCopy tool in two different modes:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-110">Also, you can use the AdlCopy tool in two different modes:</span></span>

* <span data-ttu-id="f9b9f-111">**Standalone**, where the tool uses Data Lake Store resources to perform the task.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-111">**Standalone**, where the tool uses Data Lake Store resources to perform the task.</span></span>
* <span data-ttu-id="f9b9f-112">**Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-112">**Using a Data Lake Analytics account**, where the units assigned to your Data Lake Analytics account are used to perform the copy operation.</span></span> <span data-ttu-id="f9b9f-113">You might want to use this option when you are looking to perform the copy tasks in a predictable manner.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-113">You might want to use this option when you are looking to perform the copy tasks in a predictable manner.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9b9f-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f9b9f-114">Prerequisites</span></span>
<span data-ttu-id="f9b9f-115">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-115">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f9b9f-116">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-116">**An Azure subscription**.</span></span> <span data-ttu-id="f9b9f-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f9b9f-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f9b9f-118">**Azure Storage Blobs** container with some data.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-118">**Azure Storage Blobs** container with some data.</span></span>
* <span data-ttu-id="f9b9f-119">**An Azure Data Lake Store account**.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-119">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="f9b9f-120">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f9b9f-120">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="f9b9f-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how to create a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-121">**Azure Data Lake Analytics account (optional)** - See [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md) for instructions on how to create a Data Lake Store account.</span></span>
* <span data-ttu-id="f9b9f-122">**AdlCopy tool**.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-122">**AdlCopy tool**.</span></span> <span data-ttu-id="f9b9f-123">Install the AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span><span class="sxs-lookup"><span data-stu-id="f9b9f-123">Install the AdlCopy tool from [http://aka.ms/downloadadlcopy](http://aka.ms/downloadadlcopy).</span></span>

## <a name="syntax-of-the-adlcopy-tool"></a><span data-ttu-id="f9b9f-124">Syntax of the AdlCopy tool</span><span class="sxs-lookup"><span data-stu-id="f9b9f-124">Syntax of the AdlCopy tool</span></span>
<span data-ttu-id="f9b9f-125">Use the following syntax to work with the AdlCopy tool</span><span class="sxs-lookup"><span data-stu-id="f9b9f-125">Use the following syntax to work with the AdlCopy tool</span></span>

    AdlCopy /Source <Blob or Data Lake Store source> /Dest <Data Lake Store destination> /SourceKey <Key for Blob account> /Account <Data Lake Analytics account> /Unit <Number of Analytics units> /Pattern 

<span data-ttu-id="f9b9f-126">The parameters in the syntax are described below:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-126">The parameters in the syntax are described below:</span></span>

| <span data-ttu-id="f9b9f-127">Option</span><span class="sxs-lookup"><span data-stu-id="f9b9f-127">Option</span></span> | <span data-ttu-id="f9b9f-128">Description</span><span class="sxs-lookup"><span data-stu-id="f9b9f-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f9b9f-129">Source</span><span class="sxs-lookup"><span data-stu-id="f9b9f-129">Source</span></span> |<span data-ttu-id="f9b9f-130">Specifies the location of the source data in the Azure storage blob.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-130">Specifies the location of the source data in the Azure storage blob.</span></span> <span data-ttu-id="f9b9f-131">The source can be a blob container, a blob, or another Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-131">The source can be a blob container, a blob, or another Data Lake Store account.</span></span> |
| <span data-ttu-id="f9b9f-132">Dest</span><span class="sxs-lookup"><span data-stu-id="f9b9f-132">Dest</span></span> |<span data-ttu-id="f9b9f-133">Specifies the Data Lake Store destination to copy to.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-133">Specifies the Data Lake Store destination to copy to.</span></span> |
| <span data-ttu-id="f9b9f-134">SourceKey</span><span class="sxs-lookup"><span data-stu-id="f9b9f-134">SourceKey</span></span> |<span data-ttu-id="f9b9f-135">Specifies the storage access key for the Azure storage blob source.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-135">Specifies the storage access key for the Azure storage blob source.</span></span> <span data-ttu-id="f9b9f-136">This is required only if the source is a blob container or a blob.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-136">This is required only if the source is a blob container or a blob.</span></span> |
| <span data-ttu-id="f9b9f-137">Account</span><span class="sxs-lookup"><span data-stu-id="f9b9f-137">Account</span></span> |<span data-ttu-id="f9b9f-138">**Optional**.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-138">**Optional**.</span></span> <span data-ttu-id="f9b9f-139">Use this if you want to use Azure Data Lake Analytics account to run the copy job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-139">Use this if you want to use Azure Data Lake Analytics account to run the copy job.</span></span> <span data-ttu-id="f9b9f-140">If you use the /Account option in the syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account to run the job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-140">If you use the /Account option in the syntax but do not specify a Data Lake Analytics account, AdlCopy uses a default account to run the job.</span></span> <span data-ttu-id="f9b9f-141">Also, if you use this option, you must add the source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-141">Also, if you use this option, you must add the source (Azure Storage Blob) and destination (Azure Data Lake Store) as data sources for your Data Lake Analytics account.</span></span> |
| <span data-ttu-id="f9b9f-142">Units</span><span class="sxs-lookup"><span data-stu-id="f9b9f-142">Units</span></span> |<span data-ttu-id="f9b9f-143">Specifies the number of Data Lake Analytics units that will be used for the copy job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-143">Specifies the number of Data Lake Analytics units that will be used for the copy job.</span></span> <span data-ttu-id="f9b9f-144">This option is mandatory if you use the **/Account** option to specify the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-144">This option is mandatory if you use the **/Account** option to specify the Data Lake Analytics account.</span></span> |
| <span data-ttu-id="f9b9f-145">Pattern</span><span class="sxs-lookup"><span data-stu-id="f9b9f-145">Pattern</span></span> |<span data-ttu-id="f9b9f-146">Specifies a regex pattern that indicates which blobs or files to copy.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-146">Specifies a regex pattern that indicates which blobs or files to copy.</span></span> <span data-ttu-id="f9b9f-147">AdlCopy uses case-sensitive matching.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-147">AdlCopy uses case-sensitive matching.</span></span> <span data-ttu-id="f9b9f-148">The default pattern used when no pattern is specified is to copy all items.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-148">The default pattern used when no pattern is specified is to copy all items.</span></span> <span data-ttu-id="f9b9f-149">Specifying multiple file patterns is not supported.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-149">Specifying multiple file patterns is not supported.</span></span> |

## <a name="use-adlcopy-as-standalone-to-copy-data-from-an-azure-storage-blob"></a><span data-ttu-id="f9b9f-150">Use AdlCopy (as standalone) to copy data from an Azure Storage blob</span><span class="sxs-lookup"><span data-stu-id="f9b9f-150">Use AdlCopy (as standalone) to copy data from an Azure Storage blob</span></span>
1. <span data-ttu-id="f9b9f-151">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-151">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="f9b9f-152">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-152">Run the following command to copy a specific blob from the source container to a Data Lake Store:</span></span>
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>
   
    <span data-ttu-id="f9b9f-153">For example:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-153">For example:</span></span>
   
        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

    >[AZURE.NOTE] The syntax above specifies the file to be copied to a folder in the Data Lake Store account. AdlCopy tool creates a folder if the specified folder name does not exist.

    <span data-ttu-id="f9b9f-156">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-156">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="f9b9f-157">You will see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-157">You will see an output similar to the following:</span></span>

        Initializing Copy.
        Copy Started.
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.

1. <span data-ttu-id="f9b9f-158">You can also copy all the blobs from one container to the Data Lake Store account using the following command:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-158">You can also copy all the blobs from one container to the Data Lake Store account using the following command:</span></span>
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/ /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container>        
   
    <span data-ttu-id="f9b9f-159">For example:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-159">For example:</span></span>
   
        AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ==

### <a name="performance-considerations"></a><span data-ttu-id="f9b9f-160">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="f9b9f-160">Performance considerations</span></span>

<span data-ttu-id="f9b9f-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on the blob storage side.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-161">If you are copying from an Azure Blob Storage account, you may be throttled during copy on the blob storage side.</span></span> <span data-ttu-id="f9b9f-162">This will degrade the performance of your copy job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-162">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="f9b9f-163">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f9b9f-163">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="use-adlcopy-as-standalone-to-copy-data-from-another-data-lake-store-account"></a><span data-ttu-id="f9b9f-164">Use AdlCopy (as standalone) to copy data from another Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="f9b9f-164">Use AdlCopy (as standalone) to copy data from another Data Lake Store account</span></span>
<span data-ttu-id="f9b9f-165">You can also use AdlCopy to copy data between two Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-165">You can also use AdlCopy to copy data between two Data Lake Store accounts.</span></span>

1. <span data-ttu-id="f9b9f-166">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-166">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="f9b9f-167">Run the following command to copy a specific file from one Data Lake Store account to another.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-167">Run the following command to copy a specific file from one Data Lake Store account to another.</span></span>
   
        AdlCopy /Source adl://<source_adls_account>.azuredatalakestore.net/<path_to_file> /dest adl://<dest_adls_account>.azuredatalakestore.net/<path>/
   
    <span data-ttu-id="f9b9f-168">For example:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-168">For example:</span></span>
   
        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/909f2b.log /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/
   
   > [!NOTE]
   > The syntax above specifies the file to be copied to a folder in the destination Data Lake Store account. AdlCopy tool creates a folder if the specified folder name does not exist.
   > 
   > 
   
    <span data-ttu-id="f9b9f-171">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-171">You will be prompted to enter the credentials for the Azure subscription under which you have your Data Lake Store account.</span></span> <span data-ttu-id="f9b9f-172">You will see an output similar to the following:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-172">You will see an output similar to the following:</span></span>
   
        Initializing Copy.
        Copy Started.|
        100% data copied.
        Finishing Copy.
        Copy Completed. 1 file copied.
3. <span data-ttu-id="f9b9f-173">The following command copies all files from a specific folder in the source Data Lake Store account to a folder in the destination Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-173">The following command copies all files from a specific folder in the source Data Lake Store account to a folder in the destination Data Lake Store account.</span></span>
   
        AdlCopy /Source adl://mydatastore.azuredatalakestore.net/mynewfolder/ /dest adl://mynewdatalakestore.azuredatalakestore.net/mynewfolder/

### <a name="performance-considerations"></a><span data-ttu-id="f9b9f-174">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="f9b9f-174">Performance considerations</span></span>

<span data-ttu-id="f9b9f-175">When using AdlCopy as a standalone tool, the copy is run on shared, Azure managed resources.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-175">When using AdlCopy as a standalone tool, the copy is run on shared, Azure managed resources.</span></span> <span data-ttu-id="f9b9f-176">The performance you may get in this environment depends on system load and available resources.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-176">The performance you may get in this environment depends on system load and available resources.</span></span> <span data-ttu-id="f9b9f-177">This mode is best used for small transfers on an ad hoc basis.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-177">This mode is best used for small transfers on an ad hoc basis.</span></span> <span data-ttu-id="f9b9f-178">No parameters need to be tuned when using AdlCopy as a standalone tool.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-178">No parameters need to be tuned when using AdlCopy as a standalone tool.</span></span>

## <a name="use-adlcopy-with-data-lake-analytics-account-to-copy-data"></a><span data-ttu-id="f9b9f-179">Use AdlCopy (with Data Lake Analytics account) to copy data</span><span class="sxs-lookup"><span data-stu-id="f9b9f-179">Use AdlCopy (with Data Lake Analytics account) to copy data</span></span>
<span data-ttu-id="f9b9f-180">You can also use your Data Lake Analytics account to run the AdlCopy job to copy data from Azure storage blobs to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-180">You can also use your Data Lake Analytics account to run the AdlCopy job to copy data from Azure storage blobs to Data Lake Store.</span></span> <span data-ttu-id="f9b9f-181">You would typically use this option when the data to be moved is in the range of gigabytes and terabytes, and you want better and predictable performance throughput.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-181">You would typically use this option when the data to be moved is in the range of gigabytes and terabytes, and you want better and predictable performance throughput.</span></span>

<span data-ttu-id="f9b9f-182">To use your Data Lake Analytics account with AdlCopy to copy from an Azure Storage Blob, the source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-182">To use your Data Lake Analytics account with AdlCopy to copy from an Azure Storage Blob, the source (Azure Storage Blob) must be added as a data source for your Data Lake Analytics account.</span></span> <span data-ttu-id="f9b9f-183">For instructions on adding additional data sources to your Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span><span class="sxs-lookup"><span data-stu-id="f9b9f-183">For instructions on adding additional data sources to your Data Lake Analytics account, see [Manage Data Lake Analytics account data sources](../data-lake-analytics/data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span></span>

> [!NOTE]
> If you are copying from an Azure Data Lake Store account as the source using a Data Lake Analytics account, you do not need to associate the Data Lake Store account with the Data Lake Analytics account. The requirement to associate the source store with the Data Lake Analytics account is only when the source is an Azure Storage account.
> 
> 

<span data-ttu-id="f9b9f-186">Run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-186">Run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Account <data_lake_analytics_account> /Unit <number_of_data_lake_analytics_units_to_be_used>

<span data-ttu-id="f9b9f-187">For example:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-187">For example:</span></span>

    AdlCopy /Source https://mystorage.blob.core.windows.net/mycluster/example/data/gutenberg/ /dest swebhdfs://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Account mydatalakeanalyticaccount /Units 2

<span data-ttu-id="f9b9f-188">Similarly, run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-188">Similarly, run the following command to copy from an Azure Storage blob to a Data Lake Store account using Data Lake Analytics account:</span></span>

    AdlCopy /Source adl://mysourcedatalakestore.azuredatalakestore.net/mynewfolder/ /dest adl://mydestdatastore.azuredatalakestore.net/mynewfolder/ /Account mydatalakeanalyticaccount /Units 2

### <a name="performance-considerations"></a><span data-ttu-id="f9b9f-189">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="f9b9f-189">Performance considerations</span></span>

<span data-ttu-id="f9b9f-190">When copying data in the range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-190">When copying data in the range of terabytes, using AdlCopy with your own Azure Data Lake Analytics account provides better and more predictable performance.</span></span> <span data-ttu-id="f9b9f-191">The parameter that should be tuned is the number of Azure Data Lake Analytics Units to use for the copy job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-191">The parameter that should be tuned is the number of Azure Data Lake Analytics Units to use for the copy job.</span></span> <span data-ttu-id="f9b9f-192">Increasing the number of units will increase the performance of your copy job.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-192">Increasing the number of units will increase the performance of your copy job.</span></span> <span data-ttu-id="f9b9f-193">Each file to be copied can use maximum one unit.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-193">Each file to be copied can use maximum one unit.</span></span> <span data-ttu-id="f9b9f-194">Specifying more units than the number of files being copied will not increase performance.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-194">Specifying more units than the number of files being copied will not increase performance.</span></span>

## <a name="use-adlcopy-to-copy-data-using-pattern-matching"></a><span data-ttu-id="f9b9f-195">Use AdlCopy to copy data using pattern matching</span><span class="sxs-lookup"><span data-stu-id="f9b9f-195">Use AdlCopy to copy data using pattern matching</span></span>
<span data-ttu-id="f9b9f-196">In this section, you learn how to use AdlCopy to copy data from a source (in our example below we use Azure Storage Blob) to a destination Data Lake Store account using pattern matching.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-196">In this section, you learn how to use AdlCopy to copy data from a source (in our example below we use Azure Storage Blob) to a destination Data Lake Store account using pattern matching.</span></span> <span data-ttu-id="f9b9f-197">For example, you can use the steps below to copy all files with .csv extension from the source blob to the destination.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-197">For example, you can use the steps below to copy all files with .csv extension from the source blob to the destination.</span></span>

1. <span data-ttu-id="f9b9f-198">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-198">Open a command prompt and navigate to the directory where AdlCopy is installed, typically `%HOMEPATH%\Documents\adlcopy`.</span></span>
2. <span data-ttu-id="f9b9f-199">Run the following command to copy all files with \*.csv extension from a specific blob from the source container to a Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-199">Run the following command to copy all files with \*.csv extension from a specific blob from the source container to a Data Lake Store:</span></span>
   
        AdlCopy /source https://<source_account>.blob.core.windows.net/<source_container>/<blob name> /dest swebhdfs://<dest_adls_account>.azuredatalakestore.net/<dest_folder>/ /sourcekey <storage_account_key_for_storage_container> /Pattern *.csv
   
    <span data-ttu-id="f9b9f-200">For example:</span><span class="sxs-lookup"><span data-stu-id="f9b9f-200">For example:</span></span>
   
        AdlCopy /source https://mystorage.blob.core.windows.net/mycluster/HdiSamples/HdiSamples/FoodInspectionData/ /dest adl://mydatalakestore.azuredatalakestore.net/mynewfolder/ /sourcekey uJUfvD6cEvhfLoBae2yyQf8t9/BpbWZ4XoYj4kAS5Jf40pZaMNf0q6a8yqTxktwVgRED4vPHeh/50iS9atS5LQ== /Pattern *.csv

## <a name="billing"></a><span data-ttu-id="f9b9f-201">Billing</span><span class="sxs-lookup"><span data-stu-id="f9b9f-201">Billing</span></span>
* <span data-ttu-id="f9b9f-202">If you use the AdlCopy tool as standalone you will be billed for egress costs for moving data, if the source Azure Storage account is not in the same region as the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-202">If you use the AdlCopy tool as standalone you will be billed for egress costs for moving data, if the source Azure Storage account is not in the same region as the Data Lake Store.</span></span>
* <span data-ttu-id="f9b9f-203">If you use the AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-203">If you use the AdlCopy tool with your Data Lake Analytics account, standard [Data Lake Analytics billing rates](https://azure.microsoft.com/pricing/details/data-lake-analytics/) will apply.</span></span>

## <a name="considerations-for-using-adlcopy"></a><span data-ttu-id="f9b9f-204">Considerations for using AdlCopy</span><span class="sxs-lookup"><span data-stu-id="f9b9f-204">Considerations for using AdlCopy</span></span>
* <span data-ttu-id="f9b9f-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-205">AdlCopy (for version 1.0.5), supports copying data from sources that collectively have more than thousands of files and folders.</span></span> <span data-ttu-id="f9b9f-206">However, if you encounter issues copying a large dataset, you can distribute the files/folders into different sub-folders and use the path to those sub-folders as the source instead.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-206">However, if you encounter issues copying a large dataset, you can distribute the files/folders into different sub-folders and use the path to those sub-folders as the source instead.</span></span>

## <a name="performance-considerations-for-using-adlcopy"></a><span data-ttu-id="f9b9f-207">Performance considerations for using AdlCopy</span><span class="sxs-lookup"><span data-stu-id="f9b9f-207">Performance considerations for using AdlCopy</span></span>

<span data-ttu-id="f9b9f-208">AdlCopy supports copying data containing thousands of files and folders.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-208">AdlCopy supports copying data containing thousands of files and folders.</span></span> <span data-ttu-id="f9b9f-209">However, if you encounter issues copying a large dataset, you can distribute the files/folders into smaller sub-folders.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-209">However, if you encounter issues copying a large dataset, you can distribute the files/folders into smaller sub-folders.</span></span> <span data-ttu-id="f9b9f-210">AdlCopy was built for ad hoc copies.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-210">AdlCopy was built for ad hoc copies.</span></span> <span data-ttu-id="f9b9f-211">If you are trying to copy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around the copy operations.</span><span class="sxs-lookup"><span data-stu-id="f9b9f-211">If you are trying to copy data on a recurring basis, you should consider using [Azure Data Factory](../data-factory/data-factory-azure-datalake-connector.md) that provides full management around the copy operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f9b9f-212">Next steps</span><span class="sxs-lookup"><span data-stu-id="f9b9f-212">Next steps</span></span>
* [<span data-ttu-id="f9b9f-213">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9b9f-213">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f9b9f-214">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9b9f-214">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f9b9f-215">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f9b9f-215">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

