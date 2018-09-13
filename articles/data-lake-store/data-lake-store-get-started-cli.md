---
title: Use command-line interface to get started with Azure Data Lake Store | Microsoft Docs
description: Use Azure cross-platform command line to create a Data Lake Store account and perform basic operations
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 380788f3-041d-4ae5-b6be-37ca74ca333d
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/17/2017
ms.author: nitinme
ms.openlocfilehash: f7748dba30c6e0332c166feda25f4aaa93c06efa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554197"
---
# <a name="get-started-with-azure-data-lake-store-using-azure-command-line"></a><span data-ttu-id="4ce95-103">Get started with Azure Data Lake Store using Azure Command Line</span><span class="sxs-lookup"><span data-stu-id="4ce95-103">Get started with Azure Data Lake Store using Azure Command Line</span></span>
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

<span data-ttu-id="4ce95-113">Learn how to use Azure command line interface to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ce95-113">Learn how to use Azure command line interface to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="4ce95-114">The Azure CLI is implemented in Node.js.</span><span class="sxs-lookup"><span data-stu-id="4ce95-114">The Azure CLI is implemented in Node.js.</span></span> <span data-ttu-id="4ce95-115">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span><span class="sxs-lookup"><span data-stu-id="4ce95-115">It can be used on any platform that supports Node.js, including Windows, Mac, and Linux.</span></span> <span data-ttu-id="4ce95-116">The Azure CLI is open source.</span><span class="sxs-lookup"><span data-stu-id="4ce95-116">The Azure CLI is open source.</span></span> <span data-ttu-id="4ce95-117">The source code is managed in GitHub at <a href= "https://github.com/azure/azure-xplat-cli">https://github.com/azure/azure-xplat-cli</a>.</span><span class="sxs-lookup"><span data-stu-id="4ce95-117">The source code is managed in GitHub at <a href= "https://github.com/azure/azure-xplat-cli">https://github.com/azure/azure-xplat-cli</a>.</span></span> <span data-ttu-id="4ce95-118">This article covers only using the Azure CLI with Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ce95-118">This article covers only using the Azure CLI with Data Lake Store.</span></span> <span data-ttu-id="4ce95-119">For a general guide on how to use Azure CLI, see [How to use the Azure CLI][azure-command-line-tools].</span><span class="sxs-lookup"><span data-stu-id="4ce95-119">For a general guide on how to use Azure CLI, see [How to use the Azure CLI][azure-command-line-tools].</span></span>


> [!NOTE]
> For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md). These options have better performance as they use multiple threads to parallelize the data movement.
> 
>

## <a name="prerequisites"></a><span data-ttu-id="4ce95-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4ce95-122">Prerequisites</span></span>
<span data-ttu-id="4ce95-123">Before you begin this article, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="4ce95-123">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="4ce95-124">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="4ce95-124">**An Azure subscription**.</span></span> <span data-ttu-id="4ce95-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4ce95-125">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4ce95-126">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span><span class="sxs-lookup"><span data-stu-id="4ce95-126">**Azure CLI** - See [Install and configure the Azure CLI](../cli-install-nodejs.md) for installation and configuration information.</span></span> <span data-ttu-id="4ce95-127">Make sure you reboot your computer after you install the CLI.</span><span class="sxs-lookup"><span data-stu-id="4ce95-127">Make sure you reboot your computer after you install the CLI.</span></span>

## <a name="authentication"></a><span data-ttu-id="4ce95-128">Authentication</span><span class="sxs-lookup"><span data-stu-id="4ce95-128">Authentication</span></span>

<span data-ttu-id="4ce95-129">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span><span class="sxs-lookup"><span data-stu-id="4ce95-129">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="4ce95-130">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span><span class="sxs-lookup"><span data-stu-id="4ce95-130">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="4ce95-131">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="4ce95-131">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4ce95-132">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4ce95-132">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="login-to-your-azure-subscription"></a><span data-ttu-id="4ce95-133">Login to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="4ce95-133">Login to your Azure subscription</span></span>

1. <span data-ttu-id="4ce95-134">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the `azure login` method.</span><span class="sxs-lookup"><span data-stu-id="4ce95-134">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the `azure login` method.</span></span>

2. <span data-ttu-id="4ce95-135">List the subscriptions that are associated with your account using the `azure account list` command.</span><span class="sxs-lookup"><span data-stu-id="4ce95-135">List the subscriptions that are associated with your account using the `azure account list` command.</span></span>
   
        info:    Executing command account list
        data:    Name              Id                                    Current
        data:    ----------------  ------------------------------------  -------
        data:    Azure-sub-1       ####################################  true
        data:    Azure-sub-2       ####################################  false
   
    <span data-ttu-id="4ce95-136">From the output above, **Azure-sub-1** is currently enabled, and the other subscription is **Azure-sub-2**.</span><span class="sxs-lookup"><span data-stu-id="4ce95-136">From the output above, **Azure-sub-1** is currently enabled, and the other subscription is **Azure-sub-2**.</span></span> 
3. <span data-ttu-id="4ce95-137">Select the subscription you want to work under.</span><span class="sxs-lookup"><span data-stu-id="4ce95-137">Select the subscription you want to work under.</span></span> <span data-ttu-id="4ce95-138">If you want to work under the Azure-sub-2 subscription, use the `azure account set` command.</span><span class="sxs-lookup"><span data-stu-id="4ce95-138">If you want to work under the Azure-sub-2 subscription, use the `azure account set` command.</span></span>
   
        azure account set Azure-sub-2

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="4ce95-139">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="4ce95-139">Create an Azure Data Lake Store account</span></span>
<span data-ttu-id="4ce95-140">Open a command prompt, shell, or a terminal session and run the following commands.</span><span class="sxs-lookup"><span data-stu-id="4ce95-140">Open a command prompt, shell, or a terminal session and run the following commands.</span></span>

1. <span data-ttu-id="4ce95-141">Switch to Azure Resource Manager mode using the following command:</span><span class="sxs-lookup"><span data-stu-id="4ce95-141">Switch to Azure Resource Manager mode using the following command:</span></span>
   
        azure config mode arm
2. <span data-ttu-id="4ce95-142">Create a new resource group.</span><span class="sxs-lookup"><span data-stu-id="4ce95-142">Create a new resource group.</span></span> <span data-ttu-id="4ce95-143">In the following command, provide the parameter values you want to use.</span><span class="sxs-lookup"><span data-stu-id="4ce95-143">In the following command, provide the parameter values you want to use.</span></span>
   
        azure group create <resourceGroup> <location>
   
    <span data-ttu-id="4ce95-144">If the location name contains spaces, put it in quotes.</span><span class="sxs-lookup"><span data-stu-id="4ce95-144">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="4ce95-145">For example "East US 2".</span><span class="sxs-lookup"><span data-stu-id="4ce95-145">For example "East US 2".</span></span>
3. <span data-ttu-id="4ce95-146">Create the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4ce95-146">Create the Data Lake Store account.</span></span>
   
        azure datalake store account create <dataLakeStoreAccountName> <location> <resourceGroup>

## <a name="create-folders-in-your-data-lake-store"></a><span data-ttu-id="4ce95-147">Create folders in your Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-147">Create folders in your Data Lake Store</span></span>
<span data-ttu-id="4ce95-148">You can create folders under your Azure Data Lake Store account to manage and store data.</span><span class="sxs-lookup"><span data-stu-id="4ce95-148">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="4ce95-149">Use the following command to create a folder called "mynewfolder" at the root of the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ce95-149">Use the following command to create a folder called "mynewfolder" at the root of the Data Lake Store.</span></span>

    azure datalake store filesystem create <dataLakeStoreAccountName> <path> --folder

<span data-ttu-id="4ce95-150">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-150">For example:</span></span>

    azure datalake store filesystem create mynewdatalakestore /mynewfolder --folder

## <a name="upload-data-to-your-data-lake-store"></a><span data-ttu-id="4ce95-151">Upload data to your Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-151">Upload data to your Data Lake Store</span></span>
<span data-ttu-id="4ce95-152">You can upload your data to Data Lake Store directly at the root level or to a folder that you created within the account.</span><span class="sxs-lookup"><span data-stu-id="4ce95-152">You can upload your data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="4ce95-153">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="4ce95-153">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="4ce95-154">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="4ce95-154">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="4ce95-155">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="4ce95-155">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    azure datalake store filesystem import <dataLakeStoreAccountName> "<source path>" "<destination path>"

<span data-ttu-id="4ce95-156">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-156">For example:</span></span>

    azure datalake store filesystem import mynewdatalakestore "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" "/mynewfolder/vehicle1_09142014.csv"


## <a name="list-files-in-data-lake-store"></a><span data-ttu-id="4ce95-157">List files in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-157">List files in Data Lake Store</span></span>
<span data-ttu-id="4ce95-158">Use the following command to list the files in a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4ce95-158">Use the following command to list the files in a Data Lake Store account.</span></span>

    azure datalake store filesystem list <dataLakeStoreAccountName> <path>

<span data-ttu-id="4ce95-159">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-159">For example:</span></span>

    azure datalake store filesystem list mynewdatalakestore /mynewfolder

<span data-ttu-id="4ce95-160">The output of this should be similar to the following:</span><span class="sxs-lookup"><span data-stu-id="4ce95-160">The output of this should be similar to the following:</span></span>

    info:    Executing command datalake store filesystem list
    data:    accessTime: 1446245025257
    data:    blockSize: 268435456
    data:    group: NotSupportYet
    data:    length: 1589881
    data:    modificationTime: 1446245105763
    data:    owner: NotSupportYet
    data:    pathSuffix: vehicle1_09142014.csv
    data:    permission: 777
    data:    replication: 0
    data:    type: FILE
    data:    ------------------------------------------------------------------------------------
    info:    datalake store filesystem list command OK

## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="4ce95-161">Rename, download, and delete data from your Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-161">Rename, download, and delete data from your Data Lake Store</span></span>
* <span data-ttu-id="4ce95-162">**To rename a file**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4ce95-162">**To rename a file**, use the following command:</span></span>
  
        azure datalake store filesystem move <dataLakeStoreAccountName> <path/old_file_name> <path/new_file_name>
  
    <span data-ttu-id="4ce95-163">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-163">For example:</span></span>
  
        azure datalake store filesystem move mynewdatalakestore /mynewfolder/vehicle1_09142014.csv /mynewfolder/vehicle1_09142014_copy.csv
* <span data-ttu-id="4ce95-164">**To download a file**, use the following command.</span><span class="sxs-lookup"><span data-stu-id="4ce95-164">**To download a file**, use the following command.</span></span> <span data-ttu-id="4ce95-165">Make sure the destination path you specify already exists.</span><span class="sxs-lookup"><span data-stu-id="4ce95-165">Make sure the destination path you specify already exists.</span></span>
  
        azure datalake store filesystem export <dataLakeStoreAccountName> <source_path> <destination_path>
  
    <span data-ttu-id="4ce95-166">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-166">For example:</span></span>
  
        azure datalake store filesystem export mynewdatalakestore /mynewfolder/vehicle1_09142014_copy.csv "C:\mysampledata\vehicle1_09142014_copy.csv"
* <span data-ttu-id="4ce95-167">**To delete a file**, use the following command:</span><span class="sxs-lookup"><span data-stu-id="4ce95-167">**To delete a file**, use the following command:</span></span>
  
        azure datalake store filesystem delete <dataLakeStoreAccountName> <path>
  
    <span data-ttu-id="4ce95-168">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-168">For example:</span></span>
  
        azure datalake store filesystem delete mynewdatalakestore /mynewfolder/vehicle1_09142014_copy.csv
  
    <span data-ttu-id="4ce95-169">When prompted, enter **Y** to delete the item.</span><span class="sxs-lookup"><span data-stu-id="4ce95-169">When prompted, enter **Y** to delete the item.</span></span>

## <a name="view-the-access-control-list-for-a-folder-in-data-lake-store"></a><span data-ttu-id="4ce95-170">View the access control list for a folder in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-170">View the access control list for a folder in Data Lake Store</span></span>
<span data-ttu-id="4ce95-171">Use the following command to view the ACLs on a Data Lake Store folder.</span><span class="sxs-lookup"><span data-stu-id="4ce95-171">Use the following command to view the ACLs on a Data Lake Store folder.</span></span> <span data-ttu-id="4ce95-172">In the current release, ACLs can be set only on the root of the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4ce95-172">In the current release, ACLs can be set only on the root of the Data Lake Store.</span></span> <span data-ttu-id="4ce95-173">So, the path parameter below will always be root (/).</span><span class="sxs-lookup"><span data-stu-id="4ce95-173">So, the path parameter below will always be root (/).</span></span>

    azure datalake store permissions show <dataLakeStoreName> <path>

<span data-ttu-id="4ce95-174">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-174">For example:</span></span>

    azure datalake store permissions show mynewdatalakestore /


## <a name="delete-your-data-lake-store-account"></a><span data-ttu-id="4ce95-175">Delete your Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="4ce95-175">Delete your Data Lake Store account</span></span>
<span data-ttu-id="4ce95-176">Use the following command to delete a Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="4ce95-176">Use the following command to delete a Data Lake Store account.</span></span>

    azure datalake store account delete <dataLakeStoreAccountName>

<span data-ttu-id="4ce95-177">For example:</span><span class="sxs-lookup"><span data-stu-id="4ce95-177">For example:</span></span>

    azure datalake store account delete mynewdatalakestore

<span data-ttu-id="4ce95-178">When prompted, enter **Y** to delete the account.</span><span class="sxs-lookup"><span data-stu-id="4ce95-178">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ce95-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="4ce95-179">Next steps</span></span>
* [<span data-ttu-id="4ce95-180">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-180">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="4ce95-181">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-181">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="4ce95-182">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4ce95-182">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../cli-install-nodejs.md
