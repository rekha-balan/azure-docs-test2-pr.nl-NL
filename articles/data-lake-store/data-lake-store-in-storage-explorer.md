---
title: Manage Azure Data Lake Store resources in Azure Storage Explorer
description: Learn how to access and manage your Azure Data Lake Store data and resources in Azure Storage Explorer
Keywords: Azure Data Lake Store, Azure Storage Explorer
services: Data Lake Store
documentationcenter: ''
author: jejiang
manager: DJ
editor: Jenny Jiang
ms.assetid: ''
ms.service: data-lake-store
ms.custom: Azure Data Lake Store
ms.devlang: dotnet
ms.topic: article
ms.date: 02/05/2018
ms.author: jejiang
ms.openlocfilehash: 07714b6b5d20f967843e4ce25b5c47679df1b34c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871002"
---
# <a name="manage-azure-data-lake-store-resources-by-using-storage-explorer"></a><span data-ttu-id="e79ac-103">Manage Azure Data Lake Store resources by using Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e79ac-103">Manage Azure Data Lake Store resources by using Storage Explorer</span></span>

<span data-ttu-id="e79ac-104">[Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview) is a service for storing large amounts of unstructured data, such as text or binary data.</span><span class="sxs-lookup"><span data-stu-id="e79ac-104">[Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview) is a service for storing large amounts of unstructured data, such as text or binary data.</span></span> <span data-ttu-id="e79ac-105">You can get access to the data from anywhere via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="e79ac-105">You can get access to the data from anywhere via HTTP or HTTPS.</span></span> <span data-ttu-id="e79ac-106">Data Lake Store in Azure Storage Explorer enables you to access and manage Data Lake Store data and resources, along with other Azure entities like blobs and queues.</span><span class="sxs-lookup"><span data-stu-id="e79ac-106">Data Lake Store in Azure Storage Explorer enables you to access and manage Data Lake Store data and resources, along with other Azure entities like blobs and queues.</span></span> <span data-ttu-id="e79ac-107">Now you can use the same tool to manage your different Azure entities in one place.</span><span class="sxs-lookup"><span data-stu-id="e79ac-107">Now you can use the same tool to manage your different Azure entities in one place.</span></span>

<span data-ttu-id="e79ac-108">Another advantage is that you don't need to have subscription permission to manage Data Lake Store data.</span><span class="sxs-lookup"><span data-stu-id="e79ac-108">Another advantage is that you don't need to have subscription permission to manage Data Lake Store data.</span></span> <span data-ttu-id="e79ac-109">In Storage Explorer, you can attach the Data Lake Store path to the **Local and Attached** node as long as someone grants the permission.</span><span class="sxs-lookup"><span data-stu-id="e79ac-109">In Storage Explorer, you can attach the Data Lake Store path to the **Local and Attached** node as long as someone grants the permission.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e79ac-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e79ac-110">Prerequisites</span></span>
<span data-ttu-id="e79ac-111">To complete the steps in this article, you need the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="e79ac-111">To complete the steps in this article, you need the following prerequisites:</span></span>

*   <span data-ttu-id="e79ac-112">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e79ac-112">An Azure subscription.</span></span> <span data-ttu-id="e79ac-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="e79ac-113">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
*   <span data-ttu-id="e79ac-114">An Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e79ac-114">An Azure Data Lake Store account.</span></span> <span data-ttu-id="e79ac-115">For instructions on how to create one, see [Get started with Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span><span class="sxs-lookup"><span data-stu-id="e79ac-115">For instructions on how to create one, see [Get started with Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-get-started-portal).</span></span>

## <a name="install-storage-explorer"></a><span data-ttu-id="e79ac-116">Install Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e79ac-116">Install Storage Explorer</span></span>

<span data-ttu-id="e79ac-117">Install the newest Azure Storage Explorer bits from the [product webpage](https://azure.microsoft.com/features/storage-explorer/).</span><span class="sxs-lookup"><span data-stu-id="e79ac-117">Install the newest Azure Storage Explorer bits from the [product webpage](https://azure.microsoft.com/features/storage-explorer/).</span></span> <span data-ttu-id="e79ac-118">The installation supports Windows, Linux, and Mac versions.</span><span class="sxs-lookup"><span data-stu-id="e79ac-118">The installation supports Windows, Linux, and Mac versions.</span></span>

## <a name="connect-to-an-azure-subscription"></a><span data-ttu-id="e79ac-119">Connect to an Azure subscription</span><span class="sxs-lookup"><span data-stu-id="e79ac-119">Connect to an Azure subscription</span></span>

1. <span data-ttu-id="e79ac-120">In Storage Explorer, select the plug-in icon on the left.</span><span class="sxs-lookup"><span data-stu-id="e79ac-120">In Storage Explorer, select the plug-in icon on the left.</span></span>
       
   ![Plug-in icon](./media/data-lake-store-in-storage-explorer/plug-in-icon.png)
 
2. <span data-ttu-id="e79ac-122">Select **Add an Azure Account**, and then select **Sign-in**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-122">Select **Add an Azure Account**, and then select **Sign-in**.</span></span>

   !["Connect to Azure Storage" dialog box](./media/data-lake-store-in-storage-explorer/connect-to-azure-subscription.png)

2. <span data-ttu-id="e79ac-124">In the **Sign in to your account** dialog box, enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="e79ac-124">In the **Sign in to your account** dialog box, enter your Azure credentials.</span></span>

    ![Dialog box for Azure sign-in](./media/data-lake-store-in-storage-explorer/sign-in.png)

3. <span data-ttu-id="e79ac-126">Select your subscription from the list, and then select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-126">Select your subscription from the list, and then select **Apply**.</span></span>

    ![Subscription information and "Apply" button](./media/data-lake-store-in-storage-explorer/apply-subscription.png)

    <span data-ttu-id="e79ac-128">The **EXPLORER** pane is updated and displays the accounts in the selected subscription.</span><span class="sxs-lookup"><span data-stu-id="e79ac-128">The **EXPLORER** pane is updated and displays the accounts in the selected subscription.</span></span>

    ![Account list](./media/data-lake-store-in-storage-explorer/account-list.png)

<span data-ttu-id="e79ac-130">You have successfully connected Azure Data Lake Store to your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e79ac-130">You have successfully connected Azure Data Lake Store to your Azure subscription.</span></span>

## <a name="connect-to-data-lake-store"></a><span data-ttu-id="e79ac-131">Connect to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e79ac-131">Connect to Data Lake Store</span></span>
<span data-ttu-id="e79ac-132">You can access resources that don't exist in your subscription if someone gives you the URI for the resources.</span><span class="sxs-lookup"><span data-stu-id="e79ac-132">You can access resources that don't exist in your subscription if someone gives you the URI for the resources.</span></span> <span data-ttu-id="e79ac-133">You can then connect to Data Lake Store by using the URI after you sign in.</span><span class="sxs-lookup"><span data-stu-id="e79ac-133">You can then connect to Data Lake Store by using the URI after you sign in.</span></span>
1. <span data-ttu-id="e79ac-134">Open Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="e79ac-134">Open Storage Explorer.</span></span>
2. <span data-ttu-id="e79ac-135">In the left pane, expand **Local and Attached**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-135">In the left pane, expand **Local and Attached**.</span></span>
3. <span data-ttu-id="e79ac-136">Right-click **Data Lake Store**, and then select **Connect to Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-136">Right-click **Data Lake Store**, and then select **Connect to Data Lake Store**.</span></span>

      !["Connect to Data Lake Store" on the shortcut menu](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-uri-attach.png)

4. <span data-ttu-id="e79ac-138">Enter the URI.</span><span class="sxs-lookup"><span data-stu-id="e79ac-138">Enter the URI.</span></span> <span data-ttu-id="e79ac-139">The tool browses to the location of the URL that you just entered.</span><span class="sxs-lookup"><span data-stu-id="e79ac-139">The tool browses to the location of the URL that you just entered.</span></span>

      !["Connect to Data Lake Store" dialog box, with the text box for entering the URI](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-uri-attach-dialog.png)

      ![Result of connecting to Data Lake Store](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-attach-finish.png)

## <a name="view-an-azure-data-lake-store-accounts-contents"></a><span data-ttu-id="e79ac-142">View an Azure Data Lake Store account's contents</span><span class="sxs-lookup"><span data-stu-id="e79ac-142">View an Azure Data Lake Store account's contents</span></span>
<span data-ttu-id="e79ac-143">An Azure Data Lake Store account's resources contain folders and files.</span><span class="sxs-lookup"><span data-stu-id="e79ac-143">An Azure Data Lake Store account's resources contain folders and files.</span></span>

<span data-ttu-id="e79ac-144">The following steps illustrate how to view the contents of a Data Lake Store account within Storage Explorer:</span><span class="sxs-lookup"><span data-stu-id="e79ac-144">The following steps illustrate how to view the contents of a Data Lake Store account within Storage Explorer:</span></span>

1. <span data-ttu-id="e79ac-145">Open Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="e79ac-145">Open Storage Explorer.</span></span>
2. <span data-ttu-id="e79ac-146">In the left pane, expand the subscription that contains the Azure Data Lake Store account that you want to view.</span><span class="sxs-lookup"><span data-stu-id="e79ac-146">In the left pane, expand the subscription that contains the Azure Data Lake Store account that you want to view.</span></span>
3. <span data-ttu-id="e79ac-147">Expand **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-147">Expand **Data Lake Store**.</span></span>
4. <span data-ttu-id="e79ac-148">Right-click the Azure Data Lake Store account node that you want to view, and then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-148">Right-click the Azure Data Lake Store account node that you want to view, and then select **Open**.</span></span> <span data-ttu-id="e79ac-149">You can also double-click the Data Lake Store account to open it.</span><span class="sxs-lookup"><span data-stu-id="e79ac-149">You can also double-click the Data Lake Store account to open it.</span></span> 
   
   <span data-ttu-id="e79ac-150">The main pane displays the Data Lake Store account's contents.</span><span class="sxs-lookup"><span data-stu-id="e79ac-150">The main pane displays the Data Lake Store account's contents.</span></span>

   ![Main pane with a list of folders](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-toolbar-mainpane.png) 

## <a name="manage-resources-in-azure-data-lake-store"></a><span data-ttu-id="e79ac-152">Manage resources in Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="e79ac-152">Manage resources in Azure Data Lake Store</span></span>

<span data-ttu-id="e79ac-153">You can manage Azure Data Lake Store resources by doing following operations:</span><span class="sxs-lookup"><span data-stu-id="e79ac-153">You can manage Azure Data Lake Store resources by doing following operations:</span></span>
*   <span data-ttu-id="e79ac-154">Browse through Data Lake Store resources across multiple Azure Data Lake accounts.</span><span class="sxs-lookup"><span data-stu-id="e79ac-154">Browse through Data Lake Store resources across multiple Azure Data Lake accounts.</span></span>  
*   <span data-ttu-id="e79ac-155">Use a connection string to connect to and manage Data Lake Store directly.</span><span class="sxs-lookup"><span data-stu-id="e79ac-155">Use a connection string to connect to and manage Data Lake Store directly.</span></span> 
*   <span data-ttu-id="e79ac-156">View Data Lake Store resources shared by others through an ACL under **Local and Attached**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-156">View Data Lake Store resources shared by others through an ACL under **Local and Attached**.</span></span>
*   <span data-ttu-id="e79ac-157">Perform file and folder CRUD operations: support recursive folders and multi-selected files.</span><span class="sxs-lookup"><span data-stu-id="e79ac-157">Perform file and folder CRUD operations: support recursive folders and multi-selected files.</span></span> 
*   <span data-ttu-id="e79ac-158">Drag, drop, and add a folder to quickly access recent locations.</span><span class="sxs-lookup"><span data-stu-id="e79ac-158">Drag, drop, and add a folder to quickly access recent locations.</span></span> <span data-ttu-id="e79ac-159">This operation mirrors the desktop File Explorer experience.</span><span class="sxs-lookup"><span data-stu-id="e79ac-159">This operation mirrors the desktop File Explorer experience.</span></span> 
*   <span data-ttu-id="e79ac-160">Copy and open an Azure Data Lake hyperlink in Storage Explorer with one click.</span><span class="sxs-lookup"><span data-stu-id="e79ac-160">Copy and open an Azure Data Lake hyperlink in Storage Explorer with one click.</span></span> 
*   <span data-ttu-id="e79ac-161">Display Activity Log in the lower-right pane to view activity status.</span><span class="sxs-lookup"><span data-stu-id="e79ac-161">Display Activity Log in the lower-right pane to view activity status.</span></span>
*   <span data-ttu-id="e79ac-162">Display folder statistics and file properties.</span><span class="sxs-lookup"><span data-stu-id="e79ac-162">Display folder statistics and file properties.</span></span>

## <a name="manage-resources-in-azure-storage-explorer"></a><span data-ttu-id="e79ac-163">Manage resources in Azure Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="e79ac-163">Manage resources in Azure Storage Explorer</span></span>
<span data-ttu-id="e79ac-164">After you create an Azure Data Lake Store account, you can:</span><span class="sxs-lookup"><span data-stu-id="e79ac-164">After you create an Azure Data Lake Store account, you can:</span></span>

* <span data-ttu-id="e79ac-165">Upload folders and files, download folders and files, and open resources on your local computer.</span><span class="sxs-lookup"><span data-stu-id="e79ac-165">Upload folders and files, download folders and files, and open resources on your local computer.</span></span>
* <span data-ttu-id="e79ac-166">Pin to **Quick Access**, create a new folder, copy a URL, and select all.</span><span class="sxs-lookup"><span data-stu-id="e79ac-166">Pin to **Quick Access**, create a new folder, copy a URL, and select all.</span></span>
* <span data-ttu-id="e79ac-167">Copy and paste, rename, delete, get folder statistics, and refresh.</span><span class="sxs-lookup"><span data-stu-id="e79ac-167">Copy and paste, rename, delete, get folder statistics, and refresh.</span></span>

<span data-ttu-id="e79ac-168">The following items illustrate how to manage resources within an Azure Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e79ac-168">The following items illustrate how to manage resources within an Azure Data Lake Store account.</span></span> <span data-ttu-id="e79ac-169">Follow the steps for the task that you want to perform.</span><span class="sxs-lookup"><span data-stu-id="e79ac-169">Follow the steps for the task that you want to perform.</span></span>

### <a name="upload-files"></a><span data-ttu-id="e79ac-170">Upload files</span><span class="sxs-lookup"><span data-stu-id="e79ac-170">Upload files</span></span>

1. <span data-ttu-id="e79ac-171">On the main pane's toolbar, select **Upload**, and then select **Upload Files** on the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-171">On the main pane's toolbar, select **Upload**, and then select **Upload Files** on the drop-down menu.</span></span>

   !["Upload Files" menu item](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-upload-files-menu.png) 

2. <span data-ttu-id="e79ac-173">In the **Select files to upload** dialog box, select the files that you want to upload.</span><span class="sxs-lookup"><span data-stu-id="e79ac-173">In the **Select files to upload** dialog box, select the files that you want to upload.</span></span>

   ![Dialog box for uploading files](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-upload-files-dialog.png)

3. <span data-ttu-id="e79ac-175">Select **Open** to begin the upload.</span><span class="sxs-lookup"><span data-stu-id="e79ac-175">Select **Open** to begin the upload.</span></span>

### <a name="upload-a-folder"></a><span data-ttu-id="e79ac-176">Upload a folder</span><span class="sxs-lookup"><span data-stu-id="e79ac-176">Upload a folder</span></span>

1. <span data-ttu-id="e79ac-177">On the main pane's toolbar, select **Upload**, and then select **Upload Folder** on the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-177">On the main pane's toolbar, select **Upload**, and then select **Upload Folder** on the drop-down menu.</span></span>

   !["Upload Folder" menu item](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-upload-folder-menu.png) 
     
2. <span data-ttu-id="e79ac-179">In the **Select folder to upload** dialog box, select a folder that you want to upload.</span><span class="sxs-lookup"><span data-stu-id="e79ac-179">In the **Select folder to upload** dialog box, select a folder that you want to upload.</span></span> <span data-ttu-id="e79ac-180">Then click **Select Folder**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-180">Then click **Select Folder**.</span></span>

   ![Dialog box for uploading folders](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-upload-folder-dialog.png)      

   <span data-ttu-id="e79ac-182">The upload starts.</span><span class="sxs-lookup"><span data-stu-id="e79ac-182">The upload starts.</span></span>

   ![Dialog box with the upload in progress](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-upload-folder-drag.png) 

> [!NOTE] 
> <span data-ttu-id="e79ac-184">You can directly drag the folders and files on a local computer to start uploading.</span><span class="sxs-lookup"><span data-stu-id="e79ac-184">You can directly drag the folders and files on a local computer to start uploading.</span></span> 
       
### <a name="download-folders-or-files-to-your-local-computer"></a><span data-ttu-id="e79ac-185">Download folders or files to your local computer</span><span class="sxs-lookup"><span data-stu-id="e79ac-185">Download folders or files to your local computer</span></span>

1. <span data-ttu-id="e79ac-186">Select the folders or files that you want to download.</span><span class="sxs-lookup"><span data-stu-id="e79ac-186">Select the folders or files that you want to download.</span></span>
2. <span data-ttu-id="e79ac-187">On the main pane's toolbar, select **Download**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-187">On the main pane's toolbar, select **Download**.</span></span>
3. <span data-ttu-id="e79ac-188">In the **Select a folder to save the downloaded files into** dialog box, specify the location and the name.</span><span class="sxs-lookup"><span data-stu-id="e79ac-188">In the **Select a folder to save the downloaded files into** dialog box, specify the location and the name.</span></span>
4. <span data-ttu-id="e79ac-189">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-189">Select **Save**.</span></span>

### <a name="open-a-folder-or-file-from-your-local-computer"></a><span data-ttu-id="e79ac-190">Open a folder or file from your local computer</span><span class="sxs-lookup"><span data-stu-id="e79ac-190">Open a folder or file from your local computer</span></span>

1. <span data-ttu-id="e79ac-191">Select the folder or file that you want to open.</span><span class="sxs-lookup"><span data-stu-id="e79ac-191">Select the folder or file that you want to open.</span></span>
2. <span data-ttu-id="e79ac-192">On the main pane's toolbar, select **Open**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-192">On the main pane's toolbar, select **Open**.</span></span> <span data-ttu-id="e79ac-193">Or right-click the selected folder or file, and then select **Open** on the shortcut menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-193">Or right-click the selected folder or file, and then select **Open** on the shortcut menu.</span></span>

<span data-ttu-id="e79ac-194">The file is downloaded and opened through the application that's associated with the underlying file type.</span><span class="sxs-lookup"><span data-stu-id="e79ac-194">The file is downloaded and opened through the application that's associated with the underlying file type.</span></span> <span data-ttu-id="e79ac-195">Or the folder is opened in the main pane.</span><span class="sxs-lookup"><span data-stu-id="e79ac-195">Or the folder is opened in the main pane.</span></span>

![Opened file](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-open.png) 

### <a name="copy-folders-or-files-to-the-clipboard"></a><span data-ttu-id="e79ac-197">Copy folders or files to the clipboard</span><span class="sxs-lookup"><span data-stu-id="e79ac-197">Copy folders or files to the clipboard</span></span>

1. <span data-ttu-id="e79ac-198">Select the folders or files that you want to copy.</span><span class="sxs-lookup"><span data-stu-id="e79ac-198">Select the folders or files that you want to copy.</span></span>
2. <span data-ttu-id="e79ac-199">On the main pane's toolbar, select **Copy**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-199">On the main pane's toolbar, select **Copy**.</span></span> <span data-ttu-id="e79ac-200">Or right-click the selected folders or files, and then select **Copy** on the shortcut menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-200">Or right-click the selected folders or files, and then select **Copy** on the shortcut menu.</span></span>
3. <span data-ttu-id="e79ac-201">In the left pane, browse to another Data Lake Store account, and double-click it to view it in the main pane.</span><span class="sxs-lookup"><span data-stu-id="e79ac-201">In the left pane, browse to another Data Lake Store account, and double-click it to view it in the main pane.</span></span>
4. <span data-ttu-id="e79ac-202">On the main pane's toolbar, select **Paste** to create a copy.</span><span class="sxs-lookup"><span data-stu-id="e79ac-202">On the main pane's toolbar, select **Paste** to create a copy.</span></span> <span data-ttu-id="e79ac-203">Or select **Paste** on the destination's shortcut menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-203">Or select **Paste** on the destination's shortcut menu.</span></span>

![Selections for copying a folder](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-copy-paste.png)

> [!NOTE] 
> <span data-ttu-id="e79ac-205">Copy/paste operations across storage types are not supported.</span><span class="sxs-lookup"><span data-stu-id="e79ac-205">Copy/paste operations across storage types are not supported.</span></span> <span data-ttu-id="e79ac-206">You can copy Data Lake Store folders or files and paste them in another Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="e79ac-206">You can copy Data Lake Store folders or files and paste them in another Data Lake Store account.</span></span> <span data-ttu-id="e79ac-207">But you *cannot* copy Data Lake Store folders or files and paste them to Azure Blob storage or the other way around.</span><span class="sxs-lookup"><span data-stu-id="e79ac-207">But you *cannot* copy Data Lake Store folders or files and paste them to Azure Blob storage or the other way around.</span></span>
> 
> <span data-ttu-id="e79ac-208">The copy/paste operation works by downloading the folders or files to the local computer and then uploading them to the destination.</span><span class="sxs-lookup"><span data-stu-id="e79ac-208">The copy/paste operation works by downloading the folders or files to the local computer and then uploading them to the destination.</span></span> <span data-ttu-id="e79ac-209">The tool *does not* perform the action in the back end.</span><span class="sxs-lookup"><span data-stu-id="e79ac-209">The tool *does not* perform the action in the back end.</span></span> <span data-ttu-id="e79ac-210">The copy/paste operation on large files is slow.</span><span class="sxs-lookup"><span data-stu-id="e79ac-210">The copy/paste operation on large files is slow.</span></span> <span data-ttu-id="e79ac-211">The optimization of high-performance file copy/move is underway.</span><span class="sxs-lookup"><span data-stu-id="e79ac-211">The optimization of high-performance file copy/move is underway.</span></span>

### <a name="delete-folders-or-files"></a><span data-ttu-id="e79ac-212">Delete folders or files</span><span class="sxs-lookup"><span data-stu-id="e79ac-212">Delete folders or files</span></span>

1. <span data-ttu-id="e79ac-213">Select the folders or files that you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e79ac-213">Select the folders or files that you want to delete.</span></span>
2. <span data-ttu-id="e79ac-214">On the main pane's toolbar, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-214">On the main pane's toolbar, select **Delete**.</span></span> <span data-ttu-id="e79ac-215">Or right-click the selected folders or files, and then select **Delete** on the shortcut menu.</span><span class="sxs-lookup"><span data-stu-id="e79ac-215">Or right-click the selected folders or files, and then select **Delete** on the shortcut menu.</span></span>
3. <span data-ttu-id="e79ac-216">Select **Yes** in the confirmation dialog box.</span><span class="sxs-lookup"><span data-stu-id="e79ac-216">Select **Yes** in the confirmation dialog box.</span></span>

![Selections for deleting a folder](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-delete.png)

### <a name="pin-to-quick-access"></a><span data-ttu-id="e79ac-218">Pin to Quick Access</span><span class="sxs-lookup"><span data-stu-id="e79ac-218">Pin to Quick Access</span></span>

1. <span data-ttu-id="e79ac-219">Select the folder that you want to pin.</span><span class="sxs-lookup"><span data-stu-id="e79ac-219">Select the folder that you want to pin.</span></span>
2. <span data-ttu-id="e79ac-220">On the main pane's toolbar, select **Pin to Quick access**.</span><span class="sxs-lookup"><span data-stu-id="e79ac-220">On the main pane's toolbar, select **Pin to Quick access**.</span></span>

   <span data-ttu-id="e79ac-221">In the left pane, the selected folder is added to the **Quick Access** node.</span><span class="sxs-lookup"><span data-stu-id="e79ac-221">In the left pane, the selected folder is added to the **Quick Access** node.</span></span>

   ![Selections for pinning a folder to "Quick Access"](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-quick-access.png)

<span data-ttu-id="e79ac-223">After you pin a folder to the **Quick Access** node, you can easily access the resources.</span><span class="sxs-lookup"><span data-stu-id="e79ac-223">After you pin a folder to the **Quick Access** node, you can easily access the resources.</span></span>

### <a name="use-deep-links"></a><span data-ttu-id="e79ac-224">Use deep links</span><span class="sxs-lookup"><span data-stu-id="e79ac-224">Use deep links</span></span>
<span data-ttu-id="e79ac-225">If you have a URL, you can enter the URL into the address path in File Explorer or a browser.</span><span class="sxs-lookup"><span data-stu-id="e79ac-225">If you have a URL, you can enter the URL into the address path in File Explorer or a browser.</span></span> <span data-ttu-id="e79ac-226">Then Storage Explorer.exe runs automatically to go to the location of the URL.</span><span class="sxs-lookup"><span data-stu-id="e79ac-226">Then Storage Explorer.exe runs automatically to go to the location of the URL.</span></span>

![Deep link in File Explorer](./media/data-lake-store-in-storage-explorer/storageexplorer-adls-deep-link.png)


## <a name="next-steps"></a><span data-ttu-id="e79ac-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="e79ac-228">Next steps</span></span>
* <span data-ttu-id="e79ac-229">View the [latest Storage Explorer release notes and videos](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="e79ac-229">View the [latest Storage Explorer release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="e79ac-230">Learn how to [manage Azure Cosmos DB in Azure Storage Explorer](https://docs.microsoft.com/azure/cosmos-db/storage-explorer).</span><span class="sxs-lookup"><span data-stu-id="e79ac-230">Learn how to [manage Azure Cosmos DB in Azure Storage Explorer](https://docs.microsoft.com/azure/cosmos-db/storage-explorer).</span></span>
* <span data-ttu-id="e79ac-231">[Get started with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span><span class="sxs-lookup"><span data-stu-id="e79ac-231">[Get started with Storage Explorer](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer).</span></span>
* <span data-ttu-id="e79ac-232">[Get started with Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span><span class="sxs-lookup"><span data-stu-id="e79ac-232">[Get started with Azure Data Lake Store](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-overview).</span></span>
* <span data-ttu-id="e79ac-233">Watch a [YouTube video about how to use Azure Cosmos DB in Azure Storage Explorer](https://www.youtube.com/watch?v=iNIbg1DLgWo&feature=youtu.be).</span><span class="sxs-lookup"><span data-stu-id="e79ac-233">Watch a [YouTube video about how to use Azure Cosmos DB in Azure Storage Explorer](https://www.youtube.com/watch?v=iNIbg1DLgWo&feature=youtu.be).</span></span>
