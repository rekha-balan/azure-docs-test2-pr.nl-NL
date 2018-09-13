---
title: Use PowerShell to get started with Azure Data Lake Store | Microsoft Docs
description: Use Azure PowerShell to create a Data Lake Store account and perform basic operations
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: bf85f369-f9aa-4ca1-9ae7-e03a78eb7290
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/06/2017
ms.author: nitinme
ms.openlocfilehash: c237f2f44e3b9f73278fb0b25b934d8387bacc6e
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554221"
---
# <a name="get-started-with-azure-data-lake-store-using-azure-powershell"></a><span data-ttu-id="0e05e-103">Get started with Azure Data Lake Store using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e05e-103">Get started with Azure Data Lake Store using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI](data-lake-store-get-started-cli.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="0e05e-113">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0e05e-113">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e05e-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0e05e-114">Prerequisites</span></span>
<span data-ttu-id="0e05e-115">Before you begin this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="0e05e-115">Before you begin this tutorial, you must have the following:</span></span>

* <span data-ttu-id="0e05e-116">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-116">**An Azure subscription**.</span></span> <span data-ttu-id="0e05e-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0e05e-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0e05e-118">**Azure PowerShell 1.0 or greater**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-118">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="0e05e-119">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span><span class="sxs-lookup"><span data-stu-id="0e05e-119">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs).</span></span>

## <a name="authentication"></a><span data-ttu-id="0e05e-120">Authentication</span><span class="sxs-lookup"><span data-stu-id="0e05e-120">Authentication</span></span>
<span data-ttu-id="0e05e-121">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="0e05e-121">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="0e05e-122">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span><span class="sxs-lookup"><span data-stu-id="0e05e-122">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="0e05e-123">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-123">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="0e05e-124">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0e05e-124">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="0e05e-125">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="0e05e-125">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="0e05e-126">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span><span class="sxs-lookup"><span data-stu-id="0e05e-126">From your desktop, open a new Windows PowerShell window, and enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="0e05e-127">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span><span class="sxs-lookup"><span data-stu-id="0e05e-127">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Login-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="0e05e-128">An Azure Data Lake Store account is associated with an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="0e05e-128">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="0e05e-129">Start by creating an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="0e05e-129">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="0e05e-130">![Create an Azure Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="0e05e-130">![Create an Azure Resource Group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="0e05e-131">Create an Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="0e05e-131">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="0e05e-132">The name you specify must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="0e05e-132">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="0e05e-133">![Create an Azure Data Lake Store account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="0e05e-133">![Create an Azure Data Lake Store account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="0e05e-134">Verify that the account is successfully created.</span><span class="sxs-lookup"><span data-stu-id="0e05e-134">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="0e05e-135">The output for this should be **True**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-135">The output for this should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="0e05e-136">Create directory structures in your Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-136">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="0e05e-137">You can create directories under your Azure Data Lake Store account to manage and store data.</span><span class="sxs-lookup"><span data-stu-id="0e05e-137">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="0e05e-138">Specify a root directory.</span><span class="sxs-lookup"><span data-stu-id="0e05e-138">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="0e05e-139">Create a new directory called **mynewdirectory** under the specified root.</span><span class="sxs-lookup"><span data-stu-id="0e05e-139">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="0e05e-140">Verify that the new directory is successfully created.</span><span class="sxs-lookup"><span data-stu-id="0e05e-140">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="0e05e-141">It should show an output like the following:</span><span class="sxs-lookup"><span data-stu-id="0e05e-141">It should show an output like the following:</span></span>

    <span data-ttu-id="0e05e-142">![Verify Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="0e05e-142">![Verify Directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="0e05e-143">Upload data to your Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-143">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="0e05e-144">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span><span class="sxs-lookup"><span data-stu-id="0e05e-144">You can upload your data to Data Lake Store directly at the root level or to a directory that you created within the account.</span></span> <span data-ttu-id="0e05e-145">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="0e05e-145">The snippets below demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="0e05e-146">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="0e05e-146">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="0e05e-147">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="0e05e-147">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="0e05e-148">Rename, download, and delete data from your Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-148">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="0e05e-149">To rename a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e05e-149">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="0e05e-150">To download a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e05e-150">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="0e05e-151">To delete a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="0e05e-151">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="0e05e-152">When prompted, enter **Y** to delete the item.</span><span class="sxs-lookup"><span data-stu-id="0e05e-152">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="0e05e-153">If you have more than one file to delete, you can provide all the paths separated by comma.</span><span class="sxs-lookup"><span data-stu-id="0e05e-153">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="0e05e-154">Delete your Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="0e05e-154">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="0e05e-155">Use the following command to delete your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="0e05e-155">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="0e05e-156">When prompted, enter **Y** to delete the account.</span><span class="sxs-lookup"><span data-stu-id="0e05e-156">When prompted, enter **Y** to delete the account.</span></span>

## <a name="performance-guidance-while-using-powershell"></a><span data-ttu-id="0e05e-157">Performance guidance while using PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e05e-157">Performance guidance while using PowerShell</span></span>

<span data-ttu-id="0e05e-158">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span><span class="sxs-lookup"><span data-stu-id="0e05e-158">Below are the most important settings that can be tuned to get the best performance while using PowerShell to work with Data Lake Store:</span></span>

| <span data-ttu-id="0e05e-159">Property</span><span class="sxs-lookup"><span data-stu-id="0e05e-159">Property</span></span>            | <span data-ttu-id="0e05e-160">Default</span><span class="sxs-lookup"><span data-stu-id="0e05e-160">Default</span></span> | <span data-ttu-id="0e05e-161">Description</span><span class="sxs-lookup"><span data-stu-id="0e05e-161">Description</span></span> |
|---------------------|---------|-------------|
| <span data-ttu-id="0e05e-162">PerFileThreadCount</span><span class="sxs-lookup"><span data-stu-id="0e05e-162">PerFileThreadCount</span></span>  | <span data-ttu-id="0e05e-163">10</span><span class="sxs-lookup"><span data-stu-id="0e05e-163">10</span></span>      | <span data-ttu-id="0e05e-164">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span><span class="sxs-lookup"><span data-stu-id="0e05e-164">This parameter enables you to choose the number of parallel threads for uploading or downloading each file.</span></span> <span data-ttu-id="0e05e-165">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span><span class="sxs-lookup"><span data-stu-id="0e05e-165">This number represents the max threads that can be allocated per file, but you may get less threads depending on your scenario (e.g. if you are uploading a 1KB file, you will get one thread even if you ask for 20 threads).</span></span>  |
| <span data-ttu-id="0e05e-166">ConcurrentFileCount</span><span class="sxs-lookup"><span data-stu-id="0e05e-166">ConcurrentFileCount</span></span> | <span data-ttu-id="0e05e-167">10</span><span class="sxs-lookup"><span data-stu-id="0e05e-167">10</span></span>      | <span data-ttu-id="0e05e-168">This parameter is specifically for uploading or downloading folders.</span><span class="sxs-lookup"><span data-stu-id="0e05e-168">This parameter is specifically for uploading or downloading folders.</span></span> <span data-ttu-id="0e05e-169">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span><span class="sxs-lookup"><span data-stu-id="0e05e-169">This parameter determines the number of concurrent files that can be uploaded or downloaded.</span></span> <span data-ttu-id="0e05e-170">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span><span class="sxs-lookup"><span data-stu-id="0e05e-170">This number represents the maximum number of concurrent files that can be uploaded or downloaded at one time, but you may get less concurrency depending on your scenario (e.g. if you are uploading two files, you will get two concurrent file uploads even if you ask for 15).</span></span> |

<span data-ttu-id="0e05e-171">**Example**</span><span class="sxs-lookup"><span data-stu-id="0e05e-171">**Example**</span></span>

<span data-ttu-id="0e05e-172">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span><span class="sxs-lookup"><span data-stu-id="0e05e-172">This command downloads files from Azure Data Lake Store to the user's local drive using 20 threads per file and 100 concurrent files.</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName <Data Lake Store account name> -PerFileThreadCount 20-ConcurrentFileCount 100 -Path /Powershell/100GB/ -Destination C:\Performance\ -Force -Recurse

### <a name="how-do-i-determine-the-value-to-set-for-these-parameters"></a><span data-ttu-id="0e05e-173">How do I determine the value to set for these parameters?</span><span class="sxs-lookup"><span data-stu-id="0e05e-173">How do I determine the value to set for these parameters?</span></span>

<span data-ttu-id="0e05e-174">Here's some guidance that you can use.</span><span class="sxs-lookup"><span data-stu-id="0e05e-174">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="0e05e-175">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span><span class="sxs-lookup"><span data-stu-id="0e05e-175">**Step 1: Determine the total thread count** - You should start by calculating the total thread count to use.</span></span> <span data-ttu-id="0e05e-176">As a general guideline, you should use 6 threads for each physical core.</span><span class="sxs-lookup"><span data-stu-id="0e05e-176">As a general guideline, you should use 6 threads for each physical core.</span></span>

        Total thread count = total physical cores * 6

    <span data-ttu-id="0e05e-177">**Example**</span><span class="sxs-lookup"><span data-stu-id="0e05e-177">**Example**</span></span>

    <span data-ttu-id="0e05e-178">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span><span class="sxs-lookup"><span data-stu-id="0e05e-178">Assuming you are running the PowerShell commands from a D14 VM that has 16 cores</span></span>

        Total thread count = 16 cores * 6 = 96 threads


* <span data-ttu-id="0e05e-179">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span><span class="sxs-lookup"><span data-stu-id="0e05e-179">**Step 2: Calculate PerFileThreadCount**  - We calculate our PerFileThreadCount based on the size of the files.</span></span> <span data-ttu-id="0e05e-180">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span><span class="sxs-lookup"><span data-stu-id="0e05e-180">For files smaller than 2.5GB, there is no need to change this parameter because the default of 10 is sufficient.</span></span> <span data-ttu-id="0e05e-181">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span><span class="sxs-lookup"><span data-stu-id="0e05e-181">For files larger than 2.5GB, you should use 10 threads as the base for the first 2.5GB and add 1 thread for each additional 256MB increase in file size.</span></span> <span data-ttu-id="0e05e-182">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span><span class="sxs-lookup"><span data-stu-id="0e05e-182">If you are copying a folder with a large range of file sizes, consider grouping them into similar file sizes.</span></span> <span data-ttu-id="0e05e-183">Having dissimilar file sizes may cause non-optimal performance.</span><span class="sxs-lookup"><span data-stu-id="0e05e-183">Having dissimilar file sizes may cause non-optimal performance.</span></span> <span data-ttu-id="0e05e-184">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span><span class="sxs-lookup"><span data-stu-id="0e05e-184">If that's not possible to group similar file sizes, you should set PerFileThreadCount based on the largest file size.</span></span>

        PerFileThreadCount = 10 threads for the first 2.5GB + 1 thread for each additional 256MB increase in file size

    <span data-ttu-id="0e05e-185">**Example**</span><span class="sxs-lookup"><span data-stu-id="0e05e-185">**Example**</span></span>

    <span data-ttu-id="0e05e-186">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span><span class="sxs-lookup"><span data-stu-id="0e05e-186">Assuming you have 100 files ranging from 1GB to 10GB, we use the 10GB as the largest file size for equation, which would read like the following.</span></span>

        PerFileThreadCount = 10 + ((10GB - 2.5GB) / 256MB) = 40 threads

* <span data-ttu-id="0e05e-187">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span><span class="sxs-lookup"><span data-stu-id="0e05e-187">**Step 3: Calculate ConcurrentFilecount** - Use the total thread count and PerFileThreadCount to calculate ConcurrentFileCount based on the following equation.</span></span>

        Total thread count = PerFileThreadCount * ConcurrentFileCount

    <span data-ttu-id="0e05e-188">**Example**</span><span class="sxs-lookup"><span data-stu-id="0e05e-188">**Example**</span></span>

    <span data-ttu-id="0e05e-189">Based on the example values we have been using</span><span class="sxs-lookup"><span data-stu-id="0e05e-189">Based on the example values we have been using</span></span>

        96 = 40 * ConcurrentFileCount

    <span data-ttu-id="0e05e-190">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-190">So, **ConcurrentFileCount** is **2.4**, which we can round off to **2**.</span></span>

### <a name="further-tuning"></a><span data-ttu-id="0e05e-191">Further tuning</span><span class="sxs-lookup"><span data-stu-id="0e05e-191">Further tuning</span></span>

<span data-ttu-id="0e05e-192">You might require further tuning because there is a range of file sizes to work with.</span><span class="sxs-lookup"><span data-stu-id="0e05e-192">You might require further tuning because there is a range of file sizes to work with.</span></span> <span data-ttu-id="0e05e-193">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span><span class="sxs-lookup"><span data-stu-id="0e05e-193">The above calculation works well if all or most of the files are larger and closer to the 10GB range.</span></span> <span data-ttu-id="0e05e-194">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span><span class="sxs-lookup"><span data-stu-id="0e05e-194">If instead, there are many different files sizes with many files being smaller, then you could reduce PerFileThreadCount.</span></span> <span data-ttu-id="0e05e-195">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span><span class="sxs-lookup"><span data-stu-id="0e05e-195">By reducing the PerFileThreadCount, we can increase ConcurrentFileCount.</span></span> <span data-ttu-id="0e05e-196">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span><span class="sxs-lookup"><span data-stu-id="0e05e-196">So, if we assume that most of our files are smaller in the 5GB range, we can re-do our calculation:</span></span>

    PerFileThreadCount = 10 + ((5GB - 2.5GB) / 256MB) = 20

<span data-ttu-id="0e05e-197">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-197">So, **ConcurrentFileCount** will now be 96/20, which is 4.8, rounded off to **4**.</span></span>

<span data-ttu-id="0e05e-198">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span><span class="sxs-lookup"><span data-stu-id="0e05e-198">You can continue to tune these settings by changing the **PerFileThreadCount** up and down depending on the distribution of your file sizes.</span></span>

### <a name="limitation"></a><span data-ttu-id="0e05e-199">Limitation</span><span class="sxs-lookup"><span data-stu-id="0e05e-199">Limitation</span></span>

* <span data-ttu-id="0e05e-200">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span><span class="sxs-lookup"><span data-stu-id="0e05e-200">**Number of files is less than ConcurrentFileCount**: If the number of files you are uploading is smaller than the **ConcurrentFileCount** that you calculated, then you should reduce **ConcurrentFileCount** to be equal to the number of files.</span></span> <span data-ttu-id="0e05e-201">You can use any remaining threads to increase **PerFileThreadCount**.</span><span class="sxs-lookup"><span data-stu-id="0e05e-201">You can use any remaining threads to increase **PerFileThreadCount**.</span></span>

* <span data-ttu-id="0e05e-202">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span><span class="sxs-lookup"><span data-stu-id="0e05e-202">**Too many threads**: If you increase thread count too much without increasing your cluster size, you run the risk of degraded performance.</span></span> <span data-ttu-id="0e05e-203">There can be contention issues when context-switching on the CPU.</span><span class="sxs-lookup"><span data-stu-id="0e05e-203">There can be contention issues when context-switching on the CPU.</span></span>

* <span data-ttu-id="0e05e-204">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span><span class="sxs-lookup"><span data-stu-id="0e05e-204">**Insufficient concurrency**: If the concurrency is not sufficient, then your cluster may be too small.</span></span> <span data-ttu-id="0e05e-205">You can increase the number of nodes in your cluster which will give you more concurrency.</span><span class="sxs-lookup"><span data-stu-id="0e05e-205">You can increase the number of nodes in your cluster which will give you more concurrency.</span></span>

* <span data-ttu-id="0e05e-206">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span><span class="sxs-lookup"><span data-stu-id="0e05e-206">**Throttling errors**: You may see throttling errors if your concurrency is too high.</span></span> <span data-ttu-id="0e05e-207">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span><span class="sxs-lookup"><span data-stu-id="0e05e-207">If you are seeing throttling errors, you should either reduce the concurrency or contact us.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e05e-208">Next steps</span><span class="sxs-lookup"><span data-stu-id="0e05e-208">Next steps</span></span>
* [<span data-ttu-id="0e05e-209">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-209">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0e05e-210">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-210">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0e05e-211">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0e05e-211">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)




