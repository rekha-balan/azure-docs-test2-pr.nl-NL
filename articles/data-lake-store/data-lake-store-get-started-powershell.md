---
title: Use PowerShell to get started with Azure Data Lake Storage Gen1 | Microsoft Docs
description: Use Azure PowerShell to create a Data Lake Store account and perform basic operations
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 06/27/2018
ms.author: nitinme
ms.openlocfilehash: f208722d768e2bccf2e5b4d7b4543f8cbba4f185
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44823841"
---
# <a name="get-started-with-azure-data-lake-storage-gen1-using-azure-powershell"></a><span data-ttu-id="d495b-103">Get started with Azure Data Lake Storage Gen1 using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d495b-103">Get started with Azure Data Lake Storage Gen1 using Azure PowerShell</span></span>
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
>
>

[!INCLUDE [data-lake-storage-gen1-rename-note.md](../../includes/data-lake-storage-gen1-rename-note.md)]

<span data-ttu-id="d495b-107">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Storage Gen1](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d495b-107">Learn how to use Azure PowerShell to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Storage Gen1](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d495b-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d495b-108">Prerequisites</span></span>

* <span data-ttu-id="d495b-109">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="d495b-109">**An Azure subscription**.</span></span> <span data-ttu-id="d495b-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="d495b-110">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="d495b-111">**Azure PowerShell 1.0 or greater**.</span><span class="sxs-lookup"><span data-stu-id="d495b-111">**Azure PowerShell 1.0 or greater**.</span></span> <span data-ttu-id="d495b-112">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="d495b-112">See [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="authentication"></a><span data-ttu-id="d495b-113">Authentication</span><span class="sxs-lookup"><span data-stu-id="d495b-113">Authentication</span></span>
<span data-ttu-id="d495b-114">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span><span class="sxs-lookup"><span data-stu-id="d495b-114">This article uses a simpler authentication approach with Data Lake Store where you are prompted to enter your Azure account credentials.</span></span> <span data-ttu-id="d495b-115">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span><span class="sxs-lookup"><span data-stu-id="d495b-115">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="d495b-116">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="d495b-116">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="d495b-117">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d495b-117">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="d495b-118">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="d495b-118">Create an Azure Data Lake Store account</span></span>
1. <span data-ttu-id="d495b-119">From your desktop, open a new Windows PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="d495b-119">From your desktop, open a new Windows PowerShell window.</span></span> <span data-ttu-id="d495b-120">Enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span><span class="sxs-lookup"><span data-stu-id="d495b-120">Enter the following snippet to log in to your Azure account, set the subscription, and register the Data Lake Store provider.</span></span> <span data-ttu-id="d495b-121">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span><span class="sxs-lookup"><span data-stu-id="d495b-121">When prompted to log in, make sure you log in as one of the subscription admininistrators/owner:</span></span>

        # Log in to your Azure account
        Connect-AzureRmAccount

        # List all the subscriptions associated to your account
        Get-AzureRmSubscription

        # Select a subscription
        Set-AzureRmContext -SubscriptionId <subscription ID>

        # Register for Azure Data Lake Store
        Register-AzureRmResourceProvider -ProviderNamespace "Microsoft.DataLakeStore"
2. <span data-ttu-id="d495b-122">An Azure Data Lake Store account is associated with an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="d495b-122">An Azure Data Lake Store account is associated with an Azure Resource Group.</span></span> <span data-ttu-id="d495b-123">Start by creating an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="d495b-123">Start by creating an Azure Resource Group.</span></span>

        $resourceGroupName = "<your new resource group name>"
        New-AzureRmResourceGroup -Name $resourceGroupName -Location "East US 2"

    <span data-ttu-id="d495b-124">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span><span class="sxs-lookup"><span data-stu-id="d495b-124">![Create an Azure Resource Group](./media/data-lake-store-get-started-powershell/ADL.PS.CreateResourceGroup.png "Create an Azure Resource Group")</span></span>
3. <span data-ttu-id="d495b-125">Create an Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="d495b-125">Create an Azure Data Lake Store account.</span></span> <span data-ttu-id="d495b-126">The name you specify must only contain lowercase letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="d495b-126">The name you specify must only contain lowercase letters and numbers.</span></span>

        $dataLakeStoreName = "<your new Data Lake Store name>"
        New-AzureRmDataLakeStoreAccount -ResourceGroupName $resourceGroupName -Name $dataLakeStoreName -Location "East US 2"

    <span data-ttu-id="d495b-127">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span><span class="sxs-lookup"><span data-stu-id="d495b-127">![Create an Azure Data Lake Store account](./media/data-lake-store-get-started-powershell/ADL.PS.CreateADLAcc.png "Create an Azure Data Lake Store account")</span></span>
4. <span data-ttu-id="d495b-128">Verify that the account is successfully created.</span><span class="sxs-lookup"><span data-stu-id="d495b-128">Verify that the account is successfully created.</span></span>

        Test-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

    <span data-ttu-id="d495b-129">The output for the cmdlet should be **True**.</span><span class="sxs-lookup"><span data-stu-id="d495b-129">The output for the cmdlet should be **True**.</span></span>

## <a name="create-directory-structures-in-your-azure-data-lake-store"></a><span data-ttu-id="d495b-130">Create directory structures in your Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-130">Create directory structures in your Azure Data Lake Store</span></span>
<span data-ttu-id="d495b-131">You can create directories under your Azure Data Lake Store account to manage and store data.</span><span class="sxs-lookup"><span data-stu-id="d495b-131">You can create directories under your Azure Data Lake Store account to manage and store data.</span></span>

1. <span data-ttu-id="d495b-132">Specify a root directory.</span><span class="sxs-lookup"><span data-stu-id="d495b-132">Specify a root directory.</span></span>

        $myrootdir = "/"
2. <span data-ttu-id="d495b-133">Create a new directory called **mynewdirectory** under the specified root.</span><span class="sxs-lookup"><span data-stu-id="d495b-133">Create a new directory called **mynewdirectory** under the specified root.</span></span>

        New-AzureRmDataLakeStoreItem -Folder -AccountName $dataLakeStoreName -Path $myrootdir/mynewdirectory
3. <span data-ttu-id="d495b-134">Verify that the new directory is successfully created.</span><span class="sxs-lookup"><span data-stu-id="d495b-134">Verify that the new directory is successfully created.</span></span>

        Get-AzureRmDataLakeStoreChildItem -AccountName $dataLakeStoreName -Path $myrootdir

    <span data-ttu-id="d495b-135">It should show an output as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="d495b-135">It should show an output as shown in the following screenshot:</span></span>

    <span data-ttu-id="d495b-136">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span><span class="sxs-lookup"><span data-stu-id="d495b-136">![Verify Directory](./media/data-lake-store-get-started-powershell/ADL.PS.Verify.Dir.Creation.png "Verify Directory")</span></span>

## <a name="upload-data-to-your-azure-data-lake-store"></a><span data-ttu-id="d495b-137">Upload data to your Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-137">Upload data to your Azure Data Lake Store</span></span>
<span data-ttu-id="d495b-138">You can upload your data to Data Lake Store directly at the root level, or to a directory that you created within the account.</span><span class="sxs-lookup"><span data-stu-id="d495b-138">You can upload your data to Data Lake Store directly at the root level, or to a directory that you created within the account.</span></span> <span data-ttu-id="d495b-139">The snippets in this section demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="d495b-139">The snippets in this section demonstrate how to upload some sample data to the directory (**mynewdirectory**) you created in the previous section.</span></span>

<span data-ttu-id="d495b-140">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="d495b-140">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="d495b-141">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="d495b-141">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

    Import-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path "C:\sampledata\vehicle1_09142014.csv" -Destination $myrootdir\mynewdirectory\vehicle1_09142014.csv


## <a name="rename-download-and-delete-data-from-your-data-lake-store"></a><span data-ttu-id="d495b-142">Rename, download, and delete data from your Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-142">Rename, download, and delete data from your Data Lake Store</span></span>
<span data-ttu-id="d495b-143">To rename a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="d495b-143">To rename a file, use the following command:</span></span>

    Move-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014.csv -Destination $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="d495b-144">To download a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="d495b-144">To download a file, use the following command:</span></span>

    Export-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Path $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv -Destination "C:\sampledata\vehicle1_09142014_Copy.csv"

<span data-ttu-id="d495b-145">To delete a file, use the following command:</span><span class="sxs-lookup"><span data-stu-id="d495b-145">To delete a file, use the following command:</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014_Copy.csv

<span data-ttu-id="d495b-146">When prompted, enter **Y** to delete the item.</span><span class="sxs-lookup"><span data-stu-id="d495b-146">When prompted, enter **Y** to delete the item.</span></span> <span data-ttu-id="d495b-147">If you have more than one file to delete, you can provide all the paths separated by comma.</span><span class="sxs-lookup"><span data-stu-id="d495b-147">If you have more than one file to delete, you can provide all the paths separated by comma.</span></span>

    Remove-AzureRmDataLakeStoreItem -AccountName $dataLakeStoreName -Paths $myrootdir\mynewdirectory\vehicle1_09142014.csv, $myrootdir\mynewdirectoryvehicle1_09142014_Copy.csv

## <a name="delete-your-azure-data-lake-store-account"></a><span data-ttu-id="d495b-148">Delete your Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="d495b-148">Delete your Azure Data Lake Store account</span></span>
<span data-ttu-id="d495b-149">Use the following command to delete your Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="d495b-149">Use the following command to delete your Data Lake Store account.</span></span>

    Remove-AzureRmDataLakeStoreAccount -Name $dataLakeStoreName

<span data-ttu-id="d495b-150">When prompted, enter **Y** to delete the account.</span><span class="sxs-lookup"><span data-stu-id="d495b-150">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d495b-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="d495b-151">Next steps</span></span>
* [<span data-ttu-id="d495b-152">Performance tuning guidance for using PowerShell with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-152">Performance tuning guidance for using PowerShell with Azure Data Lake Store</span></span>](data-lake-store-performance-tuning-powershell.md)
* [<span data-ttu-id="d495b-153">Use Azure Data Lake Store for big data requirements</span><span class="sxs-lookup"><span data-stu-id="d495b-153">Use Azure Data Lake Store for big data requirements</span></span>](data-lake-store-data-scenarios.md) 
* [<span data-ttu-id="d495b-154">Secure data in Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-154">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="d495b-155">Use Azure Data Lake Analytics with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-155">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="d495b-156">Use Azure HDInsight with Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d495b-156">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
