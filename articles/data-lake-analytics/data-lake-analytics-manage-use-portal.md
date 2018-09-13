---
title: Manage Azure Data Lake Analytics using the Azure portal | Microsoft Docs
description: Learn how to manage Data Lake Analytics acounts, data sources, users, and jobs.
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: a0e045f1-73d6-427f-868d-7b55c10f811b
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: 9f3d12bfacd58be4cc5e3f7019cfe973d1dcc549
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563188"
---
# <a name="manage-azure-data-lake-analytics-using-azure-portal"></a><span data-ttu-id="0f56a-103">Manage Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="0f56a-103">Manage Azure Data Lake Analytics using Azure portal</span></span>
[!INCLUDE [manage-selector](../../includes/data-lake-analytics-selector-manage.md)]

<span data-ttu-id="0f56a-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0f56a-104">Learn how to manage Azure Data Lake Analytics accounts, account data sources, users, and jobs using the Azure portal.</span></span> <span data-ttu-id="0f56a-105">To see management topics using other tools, click the tab selector on the top of the page.</span><span class="sxs-lookup"><span data-stu-id="0f56a-105">To see management topics using other tools, click the tab selector on the top of the page.</span></span>

<span data-ttu-id="0f56a-106">**Prerequisites**</span><span class="sxs-lookup"><span data-stu-id="0f56a-106">**Prerequisites**</span></span>

<span data-ttu-id="0f56a-107">Before you begin this tutorial, you must have the following items:</span><span class="sxs-lookup"><span data-stu-id="0f56a-107">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="0f56a-108">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-108">**An Azure subscription**.</span></span> <span data-ttu-id="0f56a-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0f56a-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-accounts"></a><span data-ttu-id="0f56a-110">Manage accounts</span><span class="sxs-lookup"><span data-stu-id="0f56a-110">Manage accounts</span></span>
<span data-ttu-id="0f56a-111">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-111">Before running any Data Lake Analytics jobs, you must have a Data Lake Analytics account.</span></span> <span data-ttu-id="0f56a-112">Unlike Azure HDInsight, you only pay for a Data Lake Analytics account when you run a job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-112">Unlike Azure HDInsight, you only pay for a Data Lake Analytics account when you run a job.</span></span>  <span data-ttu-id="0f56a-113">You only pay for the time when it is running a job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-113">You only pay for the time when it is running a job.</span></span>  <span data-ttu-id="0f56a-114">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f56a-114">For more information, see [Azure Data Lake Analytics Overview](data-lake-analytics-overview.md).</span></span>  

<span data-ttu-id="0f56a-115">**To create a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-115">**To create a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="0f56a-116">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0f56a-116">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0f56a-117">Click **New**, click **Intelligence + analytics**, and then click **Data Lake Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-117">Click **New**, click **Intelligence + analytics**, and then click **Data Lake Analytics**.</span></span>
3. <span data-ttu-id="0f56a-118">Type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="0f56a-118">Type or select the following values:</span></span>
   
    ![Azure Data Lake Analytics portal blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-get-started-portal/data-lake-analytics-portal-create-adla.png)
   
   * <span data-ttu-id="0f56a-120">**Name**: Name the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-120">**Name**: Name the Data Lake Analytics account.</span></span>
   * <span data-ttu-id="0f56a-121">**Subscription**: Choose the Azure subscription used for the Analytics account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-121">**Subscription**: Choose the Azure subscription used for the Analytics account.</span></span>
   * <span data-ttu-id="0f56a-122">**Resource Group**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-122">**Resource Group**.</span></span> <span data-ttu-id="0f56a-123">Select an existing Azure Resource Group or create a new one.</span><span class="sxs-lookup"><span data-stu-id="0f56a-123">Select an existing Azure Resource Group or create a new one.</span></span> <span data-ttu-id="0f56a-124">Azure Resource Manager enables you to work with the resources in your application as a group.</span><span class="sxs-lookup"><span data-stu-id="0f56a-124">Azure Resource Manager enables you to work with the resources in your application as a group.</span></span> <span data-ttu-id="0f56a-125">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f56a-125">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 
   * <span data-ttu-id="0f56a-126">**Location**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-126">**Location**.</span></span> <span data-ttu-id="0f56a-127">Select an Azure data center for the Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-127">Select an Azure data center for the Data Lake Analytics account.</span></span> 
   * <span data-ttu-id="0f56a-128">**Data Lake Store**: Each Data Lake Analytics account has a dependent Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-128">**Data Lake Store**: Each Data Lake Analytics account has a dependent Data Lake Store account.</span></span> <span data-ttu-id="0f56a-129">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="0f56a-129">The Data Lake Analytics account and the dependent Data Lake Store account must be located in the same Azure data center.</span></span> <span data-ttu-id="0f56a-130">Follow the instruction to create a new Data Lake Store account, or select an existing one.</span><span class="sxs-lookup"><span data-stu-id="0f56a-130">Follow the instruction to create a new Data Lake Store account, or select an existing one.</span></span>
4. <span data-ttu-id="0f56a-131">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-131">Click **Create**.</span></span> <span data-ttu-id="0f56a-132">It takes you to the portal home screen.</span><span class="sxs-lookup"><span data-stu-id="0f56a-132">It takes you to the portal home screen.</span></span> <span data-ttu-id="0f56a-133">A new tile is added to the StartBoard with the label showing "Deploying Azure Data Lake Analytics".</span><span class="sxs-lookup"><span data-stu-id="0f56a-133">A new tile is added to the StartBoard with the label showing "Deploying Azure Data Lake Analytics".</span></span> <span data-ttu-id="0f56a-134">It takes a few moments to create a Data Lake Analytics account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-134">It takes a few moments to create a Data Lake Analytics account.</span></span> <span data-ttu-id="0f56a-135">When the account is created, the portal opens the account on a new blade.</span><span class="sxs-lookup"><span data-stu-id="0f56a-135">When the account is created, the portal opens the account on a new blade.</span></span>

<span data-ttu-id="0f56a-136">After a Data Lake Analytics account is created, you can add additional Data Lake Store accounts and Azure Storage accounts.</span><span class="sxs-lookup"><span data-stu-id="0f56a-136">After a Data Lake Analytics account is created, you can add additional Data Lake Store accounts and Azure Storage accounts.</span></span> <span data-ttu-id="0f56a-137">For instructions, see [Manage Data lake Analytics account data sources](data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span><span class="sxs-lookup"><span data-stu-id="0f56a-137">For instructions, see [Manage Data lake Analytics account data sources](data-lake-analytics-manage-use-portal.md#manage-account-data-sources).</span></span>

<a name="access-adla-account"></a> <span data-ttu-id="0f56a-138">**To access/open a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-138">**To access/open a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="0f56a-139">Sign on to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0f56a-139">Sign on to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0f56a-140">Click **Data Lake Analytics** on the left menu.</span><span class="sxs-lookup"><span data-stu-id="0f56a-140">Click **Data Lake Analytics** on the left menu.</span></span>  <span data-ttu-id="0f56a-141">If you don't see it, click **More services**, and then click **Data Lake Analytics** under **Intelligence + Analytics**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-141">If you don't see it, click **More services**, and then click **Data Lake Analytics** under **Intelligence + Analytics**.</span></span>
3. <span data-ttu-id="0f56a-142">Click the Data Lake Analytics account that you want to access.</span><span class="sxs-lookup"><span data-stu-id="0f56a-142">Click the Data Lake Analytics account that you want to access.</span></span> <span data-ttu-id="0f56a-143">It opens the account in a new blade.</span><span class="sxs-lookup"><span data-stu-id="0f56a-143">It opens the account in a new blade.</span></span>

<span data-ttu-id="0f56a-144">**To delete a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-144">**To delete a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="0f56a-145">Open the Data Lake Analytics account that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="0f56a-145">Open the Data Lake Analytics account that you want to delete.</span></span> <span data-ttu-id="0f56a-146">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-146">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-147">Click **Delete** from the button menu on the top of the blade.</span><span class="sxs-lookup"><span data-stu-id="0f56a-147">Click **Delete** from the button menu on the top of the blade.</span></span>
3. <span data-ttu-id="0f56a-148">Type the account name, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-148">Type the account name, and then click **Delete**.</span></span>

<span data-ttu-id="0f56a-149">Deleting a Data Lake Analytics account does not delete the dependent Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="0f56a-149">Deleting a Data Lake Analytics account does not delete the dependent Data Lake Store accounts.</span></span> <span data-ttu-id="0f56a-150">For instructions of deleting Data Lake Storage accounts, see [Delete Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#delete-azure-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-150">For instructions of deleting Data Lake Storage accounts, see [Delete Data Lake Store account](../data-lake-store/data-lake-store-get-started-portal.md#delete-azure-data-lake-store-account).</span></span>

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-account-data-sources"></a><span data-ttu-id="0f56a-151">Manage account data sources</span><span class="sxs-lookup"><span data-stu-id="0f56a-151">Manage account data sources</span></span>
<span data-ttu-id="0f56a-152">Data Lake Analytics currently supports the following data sources:</span><span class="sxs-lookup"><span data-stu-id="0f56a-152">Data Lake Analytics currently supports the following data sources:</span></span>

* [<span data-ttu-id="0f56a-153">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0f56a-153">Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-overview.md)
* [<span data-ttu-id="0f56a-154">Azure Storage</span><span class="sxs-lookup"><span data-stu-id="0f56a-154">Azure Storage</span></span>](../storage/storage-introduction.md)

<span data-ttu-id="0f56a-155">When you create a Data Lake Analytics account, you must designate an Azure Data Lake Store account to be the default storage account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-155">When you create a Data Lake Analytics account, you must designate an Azure Data Lake Store account to be the default storage account.</span></span> <span data-ttu-id="0f56a-156">The default Data Lake Store account is used to store job metadata and job audit logs.</span><span class="sxs-lookup"><span data-stu-id="0f56a-156">The default Data Lake Store account is used to store job metadata and job audit logs.</span></span> <span data-ttu-id="0f56a-157">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-157">After you have created a Data Lake Analytics account, you can add additional Data Lake Store accounts and/or Azure Storage account.</span></span> 

<a name="default-adl-account"></a><span data-ttu-id="0f56a-158">**To find the default Data Lake storage account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-158">**To find the default Data Lake storage account**</span></span>

* <span data-ttu-id="0f56a-159">Open the Data Lake Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-159">Open the Data Lake Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-160">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-160">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span> <span data-ttu-id="0f56a-161">The default Data Lake store is shown in **Essential**:</span><span class="sxs-lookup"><span data-stu-id="0f56a-161">The default Data Lake store is shown in **Essential**:</span></span>
  
    ![Azure Data Lake Analytics adds data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-default-adl-storage-account.png)

<span data-ttu-id="0f56a-163">**To add additional data sources**</span><span class="sxs-lookup"><span data-stu-id="0f56a-163">**To add additional data sources**</span></span>

1. <span data-ttu-id="0f56a-164">Open the Data Lake Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-164">Open the Data Lake Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-165">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-165">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-166">Click **Settings** and then click **Data Sources**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-166">Click **Settings** and then click **Data Sources**.</span></span> <span data-ttu-id="0f56a-167">You shall see the default Data Lake Store account listed there.</span><span class="sxs-lookup"><span data-stu-id="0f56a-167">You shall see the default Data Lake Store account listed there.</span></span> 
3. <span data-ttu-id="0f56a-168">Click **Add Data Source**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-168">Click **Add Data Source**.</span></span>
   
    ![Azure Data Lake Analytics add data source](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-add-data-source.png)
   
    <span data-ttu-id="0f56a-170">To add an Azure Data Lake Store account, you need the account name, and access to the account to be able query it.</span><span class="sxs-lookup"><span data-stu-id="0f56a-170">To add an Azure Data Lake Store account, you need the account name, and access to the account to be able query it.</span></span>
    <span data-ttu-id="0f56a-171">To add an Azure Blob storage, you need the storage account and the account key, which can be found by navigating to the storage account in the portal.</span><span class="sxs-lookup"><span data-stu-id="0f56a-171">To add an Azure Blob storage, you need the storage account and the account key, which can be found by navigating to the storage account in the portal.</span></span>

<a name="explore-data-sources"></a><span data-ttu-id="0f56a-172">**To explore data sources**</span><span class="sxs-lookup"><span data-stu-id="0f56a-172">**To explore data sources**</span></span>    

1. <span data-ttu-id="0f56a-173">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-173">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-174">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-174">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-175">Click **Settings** and then click **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-175">Click **Settings** and then click **Data Explorer**.</span></span> 
   
    ![Azure Data Lake Analytics data explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-data-explorer.png)
3. <span data-ttu-id="0f56a-177">Click a Data Lake Store account to open the account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-177">Click a Data Lake Store account to open the account.</span></span>
   
    ![Azure Data Lake Analytics data explorer storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-explore-adls.png)
   
    <span data-ttu-id="0f56a-179">For each Data Lake Store account, you can</span><span class="sxs-lookup"><span data-stu-id="0f56a-179">For each Data Lake Store account, you can</span></span>
   
   * <span data-ttu-id="0f56a-180">**New Folder**: Add new folder.</span><span class="sxs-lookup"><span data-stu-id="0f56a-180">**New Folder**: Add new folder.</span></span>
   * <span data-ttu-id="0f56a-181">**Upload**: Upload files to the Storage account from your workstation.</span><span class="sxs-lookup"><span data-stu-id="0f56a-181">**Upload**: Upload files to the Storage account from your workstation.</span></span>
   * <span data-ttu-id="0f56a-182">**Access**: Configure access permissions.</span><span class="sxs-lookup"><span data-stu-id="0f56a-182">**Access**: Configure access permissions.</span></span>
   * <span data-ttu-id="0f56a-183">**Rename Folder**: Rename a folder.</span><span class="sxs-lookup"><span data-stu-id="0f56a-183">**Rename Folder**: Rename a folder.</span></span>
   * <span data-ttu-id="0f56a-184">**Folder properties**: Show file or folder properties, such as WASB path, WEBHDFS path, last modified time and so on.</span><span class="sxs-lookup"><span data-stu-id="0f56a-184">**Folder properties**: Show file or folder properties, such as WASB path, WEBHDFS path, last modified time and so on.</span></span>
   * <span data-ttu-id="0f56a-185">**Delete Folder**: Delete a folder.</span><span class="sxs-lookup"><span data-stu-id="0f56a-185">**Delete Folder**: Delete a folder.</span></span>

<a name="upload-data-to-adls"></a> <span data-ttu-id="0f56a-186">**To upload files to Data Lake Store account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-186">**To upload files to Data Lake Store account**</span></span>

1. <span data-ttu-id="0f56a-187">From the Portal, click **Browse** from the left menu, and then click **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-187">From the Portal, click **Browse** from the left menu, and then click **Data Lake Store**.</span></span>
2. <span data-ttu-id="0f56a-188">Click the Data Lake Store account that you want to upload data to.</span><span class="sxs-lookup"><span data-stu-id="0f56a-188">Click the Data Lake Store account that you want to upload data to.</span></span> <span data-ttu-id="0f56a-189">To find the default Data Lake Storage account, see [here](#default-adl-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-189">To find the default Data Lake Storage account, see [here](#default-adl-account).</span></span>
3. <span data-ttu-id="0f56a-190">Click **Data Explorer** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="0f56a-190">Click **Data Explorer** from the top menu.</span></span>
4. <span data-ttu-id="0f56a-191">Click **New Directory** to create a new folder, or click a folder name to change folder.</span><span class="sxs-lookup"><span data-stu-id="0f56a-191">Click **New Directory** to create a new folder, or click a folder name to change folder.</span></span>
5. <span data-ttu-id="0f56a-192">Click **Upload** from the top menu to upload file.</span><span class="sxs-lookup"><span data-stu-id="0f56a-192">Click **Upload** from the top menu to upload file.</span></span>

<a name="upload-data-to-wasb"></a> <span data-ttu-id="0f56a-193">**To upload files to Azure Blob storage account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-193">**To upload files to Azure Blob storage account**</span></span>

<span data-ttu-id="0f56a-194">See [Upload data for Hadoop jobs in HDInsight](../hdinsight/hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="0f56a-194">See [Upload data for Hadoop jobs in HDInsight](../hdinsight/hdinsight-upload-data.md).</span></span>  <span data-ttu-id="0f56a-195">The information applies to Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0f56a-195">The information applies to Data Lake Analytics.</span></span>

## <a name="manage-users"></a><span data-ttu-id="0f56a-196">Manage users</span><span class="sxs-lookup"><span data-stu-id="0f56a-196">Manage users</span></span>
<span data-ttu-id="0f56a-197">Data Lake Analytics uses role-based access control with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f56a-197">Data Lake Analytics uses role-based access control with Azure Active Directory.</span></span> <span data-ttu-id="0f56a-198">When you create a Data Lake Analytics account, a "Subscription Admins" role is added to the account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-198">When you create a Data Lake Analytics account, a "Subscription Admins" role is added to the account.</span></span> <span data-ttu-id="0f56a-199">You can add additional users and security groups with the following roles:</span><span class="sxs-lookup"><span data-stu-id="0f56a-199">You can add additional users and security groups with the following roles:</span></span>

| <span data-ttu-id="0f56a-200">Role</span><span class="sxs-lookup"><span data-stu-id="0f56a-200">Role</span></span> | <span data-ttu-id="0f56a-201">Description</span><span class="sxs-lookup"><span data-stu-id="0f56a-201">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0f56a-202">Owner</span><span class="sxs-lookup"><span data-stu-id="0f56a-202">Owner</span></span> |<span data-ttu-id="0f56a-203">Let you manage everything, including access to resources.</span><span class="sxs-lookup"><span data-stu-id="0f56a-203">Let you manage everything, including access to resources.</span></span> |
| <span data-ttu-id="0f56a-204">Contributor</span><span class="sxs-lookup"><span data-stu-id="0f56a-204">Contributor</span></span> |<span data-ttu-id="0f56a-205">Access the portal; submit and monitor jobs.</span><span class="sxs-lookup"><span data-stu-id="0f56a-205">Access the portal; submit and monitor jobs.</span></span> <span data-ttu-id="0f56a-206">To be able to submit jobs, a contributor needs the read or write permission to the Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="0f56a-206">To be able to submit jobs, a contributor needs the read or write permission to the Data Lake Store accounts.</span></span> |
| <span data-ttu-id="0f56a-207">DataLakeAnalyticsDeveloper</span><span class="sxs-lookup"><span data-stu-id="0f56a-207">DataLakeAnalyticsDeveloper</span></span> |<span data-ttu-id="0f56a-208">Submit, monitor and cancel jobs.</span><span class="sxs-lookup"><span data-stu-id="0f56a-208">Submit, monitor and cancel jobs.</span></span>  <span data-ttu-id="0f56a-209">These users can only cancel their own jobs.</span><span class="sxs-lookup"><span data-stu-id="0f56a-209">These users can only cancel their own jobs.</span></span> <span data-ttu-id="0f56a-210">They cannot manage their own account, for instance, add users, change permissions, or delete the account.</span><span class="sxs-lookup"><span data-stu-id="0f56a-210">They cannot manage their own account, for instance, add users, change permissions, or delete the account.</span></span> <span data-ttu-id="0f56a-211">To be able to run jobs, they need read or write access to the Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="0f56a-211">To be able to run jobs, they need read or write access to the Data Lake Store accounts</span></span> |
| <span data-ttu-id="0f56a-212">Reader</span><span class="sxs-lookup"><span data-stu-id="0f56a-212">Reader</span></span> |<span data-ttu-id="0f56a-213">Lets you view everything, but not make any changes.</span><span class="sxs-lookup"><span data-stu-id="0f56a-213">Lets you view everything, but not make any changes.</span></span> |
| <span data-ttu-id="0f56a-214">DevTest Labs User</span><span class="sxs-lookup"><span data-stu-id="0f56a-214">DevTest Labs User</span></span> |<span data-ttu-id="0f56a-215">Lets you view everything, and connect, start, restart, and shutdown virtual machines.</span><span class="sxs-lookup"><span data-stu-id="0f56a-215">Lets you view everything, and connect, start, restart, and shutdown virtual machines.</span></span> |
| <span data-ttu-id="0f56a-216">User Access Administrator</span><span class="sxs-lookup"><span data-stu-id="0f56a-216">User Access Administrator</span></span> |<span data-ttu-id="0f56a-217">Lets you manage user access to Azure resources.</span><span class="sxs-lookup"><span data-stu-id="0f56a-217">Lets you manage user access to Azure resources.</span></span> |

<span data-ttu-id="0f56a-218">For information on creating Azure Active Directory users and security groups, See [What is Azure Active Directory](../active-directory/active-directory-whatis.md).</span><span class="sxs-lookup"><span data-stu-id="0f56a-218">For information on creating Azure Active Directory users and security groups, See [What is Azure Active Directory](../active-directory/active-directory-whatis.md).</span></span>

<span data-ttu-id="0f56a-219">**To add users or security groups to a Data Lake Analytics account**</span><span class="sxs-lookup"><span data-stu-id="0f56a-219">**To add users or security groups to a Data Lake Analytics account**</span></span>

1. <span data-ttu-id="0f56a-220">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-220">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-221">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-221">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-222">Click **Settings**, and then click **Users**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-222">Click **Settings**, and then click **Users**.</span></span> <span data-ttu-id="0f56a-223">You can also click **Access** on the **Essentials** title bar as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0f56a-223">You can also click **Access** on the **Essentials** title bar as shown in the following screenshot:</span></span>
   
    ![Azure Data Lake Analytics account add users](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-access-button.png)
3. <span data-ttu-id="0f56a-225">From the **User** blade, click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-225">From the **User** blade, click **Add**.</span></span>
4. <span data-ttu-id="0f56a-226">Select a role and add a user, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-226">Select a role and add a user, and then click **OK**.</span></span>

>[!NOTE]
><span data-ttu-id="0f56a-227">If this user or security group needs to submit jobs, they need to be given permission on the Data Lake Store as well.</span><span class="sxs-lookup"><span data-stu-id="0f56a-227">If this user or security group needs to submit jobs, they need to be given permission on the Data Lake Store as well.</span></span> <span data-ttu-id="0f56a-228">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md)</span><span class="sxs-lookup"><span data-stu-id="0f56a-228">For more information, see [Secure data stored in Data Lake Store](../data-lake-store/data-lake-store-secure-data.md)</span></span>
>

<!-- ################################ -->
<!-- ################################ -->
## <a name="manage-jobs"></a><span data-ttu-id="0f56a-229">Manage jobs</span><span class="sxs-lookup"><span data-stu-id="0f56a-229">Manage jobs</span></span>
<span data-ttu-id="0f56a-230">You must have a Data Lake Analytics account before you can run any U-SQL jobs.</span><span class="sxs-lookup"><span data-stu-id="0f56a-230">You must have a Data Lake Analytics account before you can run any U-SQL jobs.</span></span>  <span data-ttu-id="0f56a-231">For more information, see [Manage Data Lake Analytics accounts](#manage-data-lake-analytics-accounts).</span><span class="sxs-lookup"><span data-stu-id="0f56a-231">For more information, see [Manage Data Lake Analytics accounts](#manage-data-lake-analytics-accounts).</span></span>

<a name="create-job"></a><span data-ttu-id="0f56a-232">**To create a job**</span><span class="sxs-lookup"><span data-stu-id="0f56a-232">**To create a job**</span></span>

1. <span data-ttu-id="0f56a-233">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-233">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-234">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-234">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-235">Click **New Job**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-235">Click **New Job**.</span></span>
   
    ![create Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-create-job-button.png)
   
    <span data-ttu-id="0f56a-237">You shall see a new blade similar to:</span><span class="sxs-lookup"><span data-stu-id="0f56a-237">You shall see a new blade similar to:</span></span>
   
    ![create Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-new-job.png)
   
    <span data-ttu-id="0f56a-239">For each job, you can configure</span><span class="sxs-lookup"><span data-stu-id="0f56a-239">For each job, you can configure</span></span>

    |<span data-ttu-id="0f56a-240">Name</span><span class="sxs-lookup"><span data-stu-id="0f56a-240">Name</span></span>|<span data-ttu-id="0f56a-241">Description</span><span class="sxs-lookup"><span data-stu-id="0f56a-241">Description</span></span>|
    |----|-----------|
    |<span data-ttu-id="0f56a-242">Job Name</span><span class="sxs-lookup"><span data-stu-id="0f56a-242">Job Name</span></span>|<span data-ttu-id="0f56a-243">Enter the name of the job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-243">Enter the name of the job.</span></span>|
    |<span data-ttu-id="0f56a-244">Priority</span><span class="sxs-lookup"><span data-stu-id="0f56a-244">Priority</span></span>|<span data-ttu-id="0f56a-245">Lower number has higher priority.</span><span class="sxs-lookup"><span data-stu-id="0f56a-245">Lower number has higher priority.</span></span> <span data-ttu-id="0f56a-246">If two jobs are both queued, the one with lower priority runs first</span><span class="sxs-lookup"><span data-stu-id="0f56a-246">If two jobs are both queued, the one with lower priority runs first</span></span>|
    |<span data-ttu-id="0f56a-247">Parallelism</span><span class="sxs-lookup"><span data-stu-id="0f56a-247">Parallelism</span></span> |<span data-ttu-id="0f56a-248">Max number of compute processes that can happen at the same time.</span><span class="sxs-lookup"><span data-stu-id="0f56a-248">Max number of compute processes that can happen at the same time.</span></span> <span data-ttu-id="0f56a-249">Increasing this number can improve performance but can also increase cost.</span><span class="sxs-lookup"><span data-stu-id="0f56a-249">Increasing this number can improve performance but can also increase cost.</span></span>|
    |<span data-ttu-id="0f56a-250">Script</span><span class="sxs-lookup"><span data-stu-id="0f56a-250">Script</span></span>|<span data-ttu-id="0f56a-251">Enter the U-SQL script for the job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-251">Enter the U-SQL script for the job.</span></span>|

    <span data-ttu-id="0f56a-252">Using the same interface, you can also explore the link data sources, and add additional files to the linked data sources.</span><span class="sxs-lookup"><span data-stu-id="0f56a-252">Using the same interface, you can also explore the link data sources, and add additional files to the linked data sources.</span></span> 
1. <span data-ttu-id="0f56a-253">Click **Submit Job** if you want to submit the job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-253">Click **Submit Job** if you want to submit the job.</span></span>

<span data-ttu-id="0f56a-254">**To submit a job**</span><span class="sxs-lookup"><span data-stu-id="0f56a-254">**To submit a job**</span></span>

<span data-ttu-id="0f56a-255">See [Create Data Lake Analytics jobs](#create-job).</span><span class="sxs-lookup"><span data-stu-id="0f56a-255">See [Create Data Lake Analytics jobs](#create-job).</span></span>

<a name="monitor-jobs"></a><span data-ttu-id="0f56a-256">**To monitor jobs**</span><span class="sxs-lookup"><span data-stu-id="0f56a-256">**To monitor jobs**</span></span>

1. <span data-ttu-id="0f56a-257">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-257">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-258">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-258">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span> <span data-ttu-id="0f56a-259">The Job Management panel shows the basic job information:</span><span class="sxs-lookup"><span data-stu-id="0f56a-259">The Job Management panel shows the basic job information:</span></span>
   
    ![manage Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-manage-jobs.png)
2. <span data-ttu-id="0f56a-261">Click **Job Management** as shown in the previous screenshot.</span><span class="sxs-lookup"><span data-stu-id="0f56a-261">Click **Job Management** as shown in the previous screenshot.</span></span>
   
    ![manage Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-manage-jobs-details.png)
3. <span data-ttu-id="0f56a-263">Click a job from the lists.</span><span class="sxs-lookup"><span data-stu-id="0f56a-263">Click a job from the lists.</span></span> <span data-ttu-id="0f56a-264">Or click **Filter** to help you to find the jobs:</span><span class="sxs-lookup"><span data-stu-id="0f56a-264">Or click **Filter** to help you to find the jobs:</span></span>
   
    ![filter Azure Data Lake Analytics U-SQL jobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-filter-jobs.png)
   
    <span data-ttu-id="0f56a-266">You can filter jobs by **Time Range**, **Job Name**, and **Author**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-266">You can filter jobs by **Time Range**, **Job Name**, and **Author**.</span></span>
4. <span data-ttu-id="0f56a-267">Click **Resubmit** if you want to resubmit the job.</span><span class="sxs-lookup"><span data-stu-id="0f56a-267">Click **Resubmit** if you want to resubmit the job.</span></span>

<span data-ttu-id="0f56a-268">**To resubmit a job**</span><span class="sxs-lookup"><span data-stu-id="0f56a-268">**To resubmit a job**</span></span>

<span data-ttu-id="0f56a-269">See [Monitor Data Lake Analytics jobs](#monitor-jobs).</span><span class="sxs-lookup"><span data-stu-id="0f56a-269">See [Monitor Data Lake Analytics jobs](#monitor-jobs).</span></span>

## <a name="monitor-account-usage"></a><span data-ttu-id="0f56a-270">Monitor account usage</span><span class="sxs-lookup"><span data-stu-id="0f56a-270">Monitor account usage</span></span>
<span data-ttu-id="0f56a-271">**To monitor account usage**</span><span class="sxs-lookup"><span data-stu-id="0f56a-271">**To monitor account usage**</span></span>

1. <span data-ttu-id="0f56a-272">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-272">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-273">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-273">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span> <span data-ttu-id="0f56a-274">The Usage panel shows the usage:</span><span class="sxs-lookup"><span data-stu-id="0f56a-274">The Usage panel shows the usage:</span></span>
   
    ![monitor Azure Data Lake Analytics usage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-monitor-usage.png)
2. <span data-ttu-id="0f56a-276">Double-click the pane to see more details.</span><span class="sxs-lookup"><span data-stu-id="0f56a-276">Double-click the pane to see more details.</span></span>

## <a name="view-u-sql-catalog"></a><span data-ttu-id="0f56a-277">View U-SQL catalog</span><span class="sxs-lookup"><span data-stu-id="0f56a-277">View U-SQL catalog</span></span>
<span data-ttu-id="0f56a-278">The [U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md) is used to structure data and code so they can be shared by U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="0f56a-278">The [U-SQL catalog](data-lake-analytics-use-u-sql-catalog.md) is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="0f56a-279">The catalog enables the highest performance possible with data in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0f56a-279">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span> <span data-ttu-id="0f56a-280">From the Azure portal, you are able to view U-SQL catalog.</span><span class="sxs-lookup"><span data-stu-id="0f56a-280">From the Azure portal, you are able to view U-SQL catalog.</span></span>

<span data-ttu-id="0f56a-281">**To browse U-SQL catalog**</span><span class="sxs-lookup"><span data-stu-id="0f56a-281">**To browse U-SQL catalog**</span></span>

1. <span data-ttu-id="0f56a-282">Open the Analytics account that you want to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-282">Open the Analytics account that you want to manage.</span></span> <span data-ttu-id="0f56a-283">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span><span class="sxs-lookup"><span data-stu-id="0f56a-283">For instructions, see [Access Data Lake Analytics accounts](#access-adla-account).</span></span>
2. <span data-ttu-id="0f56a-284">Click **Data Explorer** from the top menu.</span><span class="sxs-lookup"><span data-stu-id="0f56a-284">Click **Data Explorer** from the top menu.</span></span>
3. <span data-ttu-id="0f56a-285">Expand **Catalog**, expand **master**, expand \*\*Tables, or **Table Valued Functions**, or **Assemblies**.</span><span class="sxs-lookup"><span data-stu-id="0f56a-285">Expand **Catalog**, expand **master**, expand \*\*Tables, or **Table Valued Functions**, or **Assemblies**.</span></span> <span data-ttu-id="0f56a-286">The following screenshot shows one table valued function.</span><span class="sxs-lookup"><span data-stu-id="0f56a-286">The following screenshot shows one table valued function.</span></span>
   
    ![Azure Data Lake Analytics data explorer storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-explore-catalog.png)

<!-- ################################ -->
<!-- ################################ -->
## <a name="use-azure-resource-manager-groups"></a><span data-ttu-id="0f56a-288">Use Azure Resource Manager groups</span><span class="sxs-lookup"><span data-stu-id="0f56a-288">Use Azure Resource Manager groups</span></span>
<span data-ttu-id="0f56a-289">Applications are typically made up of many components, for example a web app, database, database server, storage, and third-party services.</span><span class="sxs-lookup"><span data-stu-id="0f56a-289">Applications are typically made up of many components, for example a web app, database, database server, storage, and third-party services.</span></span> <span data-ttu-id="0f56a-290">Azure Resource Manager enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span><span class="sxs-lookup"><span data-stu-id="0f56a-290">Azure Resource Manager enables you to work with the resources in your application as a group, referred to as an Azure Resource Group.</span></span> <span data-ttu-id="0f56a-291">You can deploy, update, monitor, or delete all the resources for your application in a single, coordinated operation.</span><span class="sxs-lookup"><span data-stu-id="0f56a-291">You can deploy, update, monitor, or delete all the resources for your application in a single, coordinated operation.</span></span> <span data-ttu-id="0f56a-292">You use a template for deployment and that template can work for different environments such as testing, staging, and production.</span><span class="sxs-lookup"><span data-stu-id="0f56a-292">You use a template for deployment and that template can work for different environments such as testing, staging, and production.</span></span> <span data-ttu-id="0f56a-293">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span><span class="sxs-lookup"><span data-stu-id="0f56a-293">You can clarify billing for your organization by viewing the rolled-up costs for the entire group.</span></span> <span data-ttu-id="0f56a-294">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f56a-294">For more information, see [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span> 

<span data-ttu-id="0f56a-295">A Data Lake Analytics service can include the following components:</span><span class="sxs-lookup"><span data-stu-id="0f56a-295">A Data Lake Analytics service can include the following components:</span></span>

* <span data-ttu-id="0f56a-296">Azure Data Lake Analytics account</span><span class="sxs-lookup"><span data-stu-id="0f56a-296">Azure Data Lake Analytics account</span></span>
* <span data-ttu-id="0f56a-297">Required default Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="0f56a-297">Required default Azure Data Lake Store account</span></span>
* <span data-ttu-id="0f56a-298">Additional Azure Data Lake Store accounts</span><span class="sxs-lookup"><span data-stu-id="0f56a-298">Additional Azure Data Lake Store accounts</span></span>
* <span data-ttu-id="0f56a-299">Additional Azure Storage accounts</span><span class="sxs-lookup"><span data-stu-id="0f56a-299">Additional Azure Storage accounts</span></span>

<span data-ttu-id="0f56a-300">You can create all these components under one Resource Management group to make them easier to manage.</span><span class="sxs-lookup"><span data-stu-id="0f56a-300">You can create all these components under one Resource Management group to make them easier to manage.</span></span>

![Azure Data Lake Analytics account and storage](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-manage-use-portal/data-lake-analytics-arm-structure.png)

<span data-ttu-id="0f56a-302">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span><span class="sxs-lookup"><span data-stu-id="0f56a-302">A Data Lake Analytics account and the dependent storage accounts must be placed in the same Azure data center.</span></span>
<span data-ttu-id="0f56a-303">The Resource Management group however can be located in a different data center.</span><span class="sxs-lookup"><span data-stu-id="0f56a-303">The Resource Management group however can be located in a different data center.</span></span>  

## <a name="see-also"></a><span data-ttu-id="0f56a-304">See also</span><span class="sxs-lookup"><span data-stu-id="0f56a-304">See also</span></span>
* [<span data-ttu-id="0f56a-305">Overview of Microsoft Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="0f56a-305">Overview of Microsoft Azure Data Lake Analytics</span></span>](data-lake-analytics-overview.md)
* [<span data-ttu-id="0f56a-306">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="0f56a-306">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0f56a-307">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f56a-307">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
* [<span data-ttu-id="0f56a-308">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="0f56a-308">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)















