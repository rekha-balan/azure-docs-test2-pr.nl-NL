---
title: Browsing and managing storage resources with Server Explorer | Microsoft Docs
description: Browsing and managing storage resources with Server Explorer
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 1c0a2905b5aeedf9b52f123816dc09af1a9c7f51
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556002"
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a><span data-ttu-id="ec448-103">Browsing and Managing Storage Resources with Server Explorer</span><span class="sxs-lookup"><span data-stu-id="ec448-103">Browsing and Managing Storage Resources with Server Explorer</span></span>
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="ec448-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ec448-104">Overview</span></span>
<span data-ttu-id="ec448-105">If you've installed the Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span><span class="sxs-lookup"><span data-stu-id="ec448-105">If you've installed the Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="ec448-106">The Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="ec448-106">The Azure Storage node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="ec448-107">To view Server Explorer in Visual Studio, on the menu bar, choose **View**, **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ec448-107">To view Server Explorer in Visual Studio, on the menu bar, choose **View**, **Server Explorer**.</span></span> <span data-ttu-id="ec448-108">The storage node shows all of the storage accounts that exist under each Azure subscription/certificate you're connected to.</span><span class="sxs-lookup"><span data-stu-id="ec448-108">The storage node shows all of the storage accounts that exist under each Azure subscription/certificate you're connected to.</span></span> <span data-ttu-id="ec448-109">If your storage account doesn't appear, you can add it by following the instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span><span class="sxs-lookup"><span data-stu-id="ec448-109">If your storage account doesn't appear, you can add it by following the instructions [later in this topic](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="ec448-110">Starting in Azure SDK 2.7, you can also use the new Cloud Explorer to view and manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="ec448-110">Starting in Azure SDK 2.7, you can also use the new Cloud Explorer to view and manage your Azure resources.</span></span> <span data-ttu-id="ec448-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="ec448-111">See [Managing Azure Resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) for more information.</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="ec448-112">View and manage storage resources in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec448-112">View and manage storage resources in Visual Studio</span></span>
<span data-ttu-id="ec448-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span><span class="sxs-lookup"><span data-stu-id="ec448-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="ec448-114">The storage emulator account is listed in Server Explorer under the Storage node as the **Development** node.</span><span class="sxs-lookup"><span data-stu-id="ec448-114">The storage emulator account is listed in Server Explorer under the Storage node as the **Development** node.</span></span>

<span data-ttu-id="ec448-115">To see the storage emulator account’s resources, expand the **Development** node.</span><span class="sxs-lookup"><span data-stu-id="ec448-115">To see the storage emulator account’s resources, expand the **Development** node.</span></span> <span data-ttu-id="ec448-116">If the storage emulator hasn’t been started when you expand the **Development** node, it will automatically start.</span><span class="sxs-lookup"><span data-stu-id="ec448-116">If the storage emulator hasn’t been started when you expand the **Development** node, it will automatically start.</span></span> <span data-ttu-id="ec448-117">This can take several seconds.</span><span class="sxs-lookup"><span data-stu-id="ec448-117">This can take several seconds.</span></span> <span data-ttu-id="ec448-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span><span class="sxs-lookup"><span data-stu-id="ec448-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span></span>

<span data-ttu-id="ec448-119">To view resources in a storage account, expand the storage account’s node in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-119">To view resources in a storage account, expand the storage account’s node in Server Explorer.</span></span> <span data-ttu-id="ec448-120">The following sub-nodes appear:</span><span class="sxs-lookup"><span data-stu-id="ec448-120">The following sub-nodes appear:</span></span>

* <span data-ttu-id="ec448-121">Blobs</span><span class="sxs-lookup"><span data-stu-id="ec448-121">Blobs</span></span>
* <span data-ttu-id="ec448-122">Queues</span><span class="sxs-lookup"><span data-stu-id="ec448-122">Queues</span></span>
* <span data-ttu-id="ec448-123">Tables</span><span class="sxs-lookup"><span data-stu-id="ec448-123">Tables</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="ec448-124">Work with Blob Resources</span><span class="sxs-lookup"><span data-stu-id="ec448-124">Work with Blob Resources</span></span>
<span data-ttu-id="ec448-125">The Blobs node displays a list of containers for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-125">The Blobs node displays a list of containers for the selected storage account.</span></span> <span data-ttu-id="ec448-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span><span class="sxs-lookup"><span data-stu-id="ec448-126">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="ec448-127">See [How to use Blob Storage from .NET](storage/storage-dotnet-how-to-use-blobs.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="ec448-127">See [How to use Blob Storage from .NET](storage/storage-dotnet-how-to-use-blobs.md) for more information.</span></span>

### <a name="to-create-a-blob-container"></a><span data-ttu-id="ec448-128">To create a blob container</span><span class="sxs-lookup"><span data-stu-id="ec448-128">To create a blob container</span></span>
1. <span data-ttu-id="ec448-129">Open the shortcut menu for the **Blobs** node, and then choose **Create Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="ec448-129">Open the shortcut menu for the **Blobs** node, and then choose **Create Blob Container**.</span></span>
2. <span data-ttu-id="ec448-130">Enter the name of the new container in the **Create Blob Container** dialog box and then choose **Ok**</span><span class="sxs-lookup"><span data-stu-id="ec448-130">Enter the name of the new container in the **Create Blob Container** dialog box and then choose **Ok**</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ec448-131">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span><span class="sxs-lookup"><span data-stu-id="ec448-131">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>
   > 
   > 

### <a name="to-delete-a-blob-container"></a><span data-ttu-id="ec448-132">To delete a blob container</span><span class="sxs-lookup"><span data-stu-id="ec448-132">To delete a blob container</span></span>
* <span data-ttu-id="ec448-133">Open the shortcut menu for the blob container you want to remove and then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ec448-133">Open the shortcut menu for the blob container you want to remove and then choose **Delete**.</span></span>

### <a name="to-display-a-list-of-the-items-contained-in-a-blob-container"></a><span data-ttu-id="ec448-134">To display a list of the items contained in a blob container</span><span class="sxs-lookup"><span data-stu-id="ec448-134">To display a list of the items contained in a blob container</span></span>
* <span data-ttu-id="ec448-135">Open the shortcut menu for a blob container name in the list and then choose **View Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="ec448-135">Open the shortcut menu for a blob container name in the list and then choose **View Blob Container**.</span></span>
  
    <span data-ttu-id="ec448-136">When you view the contents of a blob container, it appears in a tab known as the blob container view.</span><span class="sxs-lookup"><span data-stu-id="ec448-136">When you view the contents of a blob container, it appears in a tab known as the blob container view.</span></span>
  
    ![VST_SE_BlobDesigner](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    <span data-ttu-id="ec448-138">You can perform the following operations on blobs by using the buttons in the top-right corner of the blob container view:</span><span class="sxs-lookup"><span data-stu-id="ec448-138">You can perform the following operations on blobs by using the buttons in the top-right corner of the blob container view:</span></span>
  
  * <span data-ttu-id="ec448-139">Enter a filter value and apply it</span><span class="sxs-lookup"><span data-stu-id="ec448-139">Enter a filter value and apply it</span></span>
  * <span data-ttu-id="ec448-140">Refresh the list of blobs in the container</span><span class="sxs-lookup"><span data-stu-id="ec448-140">Refresh the list of blobs in the container</span></span>
  * <span data-ttu-id="ec448-141">Upload a file</span><span class="sxs-lookup"><span data-stu-id="ec448-141">Upload a file</span></span>
  * <span data-ttu-id="ec448-142">Delete a blob</span><span class="sxs-lookup"><span data-stu-id="ec448-142">Delete a blob</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ec448-143">Deleting a file from a blob container doesn’t delete the underlying file; it only removes it from the blob container.</span><span class="sxs-lookup"><span data-stu-id="ec448-143">Deleting a file from a blob container doesn’t delete the underlying file; it only removes it from the blob container.</span></span>
    > 
    > 
  * <span data-ttu-id="ec448-144">Open a blob</span><span class="sxs-lookup"><span data-stu-id="ec448-144">Open a blob</span></span>
  * <span data-ttu-id="ec448-145">Save a blob to the local computer</span><span class="sxs-lookup"><span data-stu-id="ec448-145">Save a blob to the local computer</span></span>

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="ec448-146">To create a folder or subfolder in a blob container</span><span class="sxs-lookup"><span data-stu-id="ec448-146">To create a folder or subfolder in a blob container</span></span>
1. <span data-ttu-id="ec448-147">Choose the blob container in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-147">Choose the blob container in Server Explorer.</span></span> <span data-ttu-id="ec448-148">In the container window, choose the **Upload Blob** button.</span><span class="sxs-lookup"><span data-stu-id="ec448-148">In the container window, choose the **Upload Blob** button.</span></span>
   
    ![Uploading a file into a blob folder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. <span data-ttu-id="ec448-150">In the **Upload New File** dialog box, choose the **Browse** button to specify the file you want to upload, and then enter a folder name in the **Folder (optional)** box.</span><span class="sxs-lookup"><span data-stu-id="ec448-150">In the **Upload New File** dialog box, choose the **Browse** button to specify the file you want to upload, and then enter a folder name in the **Folder (optional)** box.</span></span>
   
    <span data-ttu-id="ec448-151">You can add subfolders in container folders by following the same procedure.</span><span class="sxs-lookup"><span data-stu-id="ec448-151">You can add subfolders in container folders by following the same procedure.</span></span> <span data-ttu-id="ec448-152">If you don’t specify a folder name, the file will be uploaded to the top level of the blob container.The file appears in the specified folder in the container.</span><span class="sxs-lookup"><span data-stu-id="ec448-152">If you don’t specify a folder name, the file will be uploaded to the top level of the blob container.The file appears in the specified folder in the container.</span></span>
   
    ![Folder added to a blob container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. <span data-ttu-id="ec448-154">Double-click the folder or press ENTER to see the contents of the folder.</span><span class="sxs-lookup"><span data-stu-id="ec448-154">Double-click the folder or press ENTER to see the contents of the folder.</span></span> <span data-ttu-id="ec448-155">When you’re in the container’s folder, you can navigate back to the root of the container by choosing the **Open Parent Directory** (up arrow) button.</span><span class="sxs-lookup"><span data-stu-id="ec448-155">When you’re in the container’s folder, you can navigate back to the root of the container by choosing the **Open Parent Directory** (up arrow) button.</span></span>

### <a name="to-delete-a-container-folder"></a><span data-ttu-id="ec448-156">To delete a container folder</span><span class="sxs-lookup"><span data-stu-id="ec448-156">To delete a container folder</span></span>
* <span data-ttu-id="ec448-157">Delete all of the files in the folder</span><span class="sxs-lookup"><span data-stu-id="ec448-157">Delete all of the files in the folder</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ec448-158">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder to delete its file contents.</span><span class="sxs-lookup"><span data-stu-id="ec448-158">Because folders in blob containers are virtual folders, you can’t create an empty folder, nor can you delete a folder to delete its file contents.</span></span> <span data-ttu-id="ec448-159">You have to delete the entire contents of a folder to delete the folder.</span><span class="sxs-lookup"><span data-stu-id="ec448-159">You have to delete the entire contents of a folder to delete the folder.</span></span>
  > 
  > 

### <a name="to-filter-blobs-in-a-container"></a><span data-ttu-id="ec448-160">To filter blobs in a container</span><span class="sxs-lookup"><span data-stu-id="ec448-160">To filter blobs in a container</span></span>
<span data-ttu-id="ec448-161">You can filter the blobs that are displayed by specifying a common prefix.</span><span class="sxs-lookup"><span data-stu-id="ec448-161">You can filter the blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="ec448-162">For example, if you enter the prefix `hello` in the filter text box and then choose the **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span><span class="sxs-lookup"><span data-stu-id="ec448-162">For example, if you enter the prefix `hello` in the filter text box and then choose the **Execute** (**!**)button, only blobs that begin with 'hello' appear.</span></span>

![VST_SE_FilterBlobs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> <span data-ttu-id="ec448-164">The filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span><span class="sxs-lookup"><span data-stu-id="ec448-164">The filter field is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="ec448-165">Blobs can only be filtered by prefix.</span><span class="sxs-lookup"><span data-stu-id="ec448-165">Blobs can only be filtered by prefix.</span></span> <span data-ttu-id="ec448-166">The prefix may include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span><span class="sxs-lookup"><span data-stu-id="ec448-166">The prefix may include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="ec448-167">For example, filtering on the prefix HelloFabric/ returns all blobs beginning with that string.</span><span class="sxs-lookup"><span data-stu-id="ec448-167">For example, filtering on the prefix HelloFabric/ returns all blobs beginning with that string.</span></span>
> 
> 

### <a name="to-download-blob-data"></a><span data-ttu-id="ec448-168">To download blob data</span><span class="sxs-lookup"><span data-stu-id="ec448-168">To download blob data</span></span>
* <span data-ttu-id="ec448-169">In **Server Explorer**, open the shortcut menu for one or more blobs and then choose **Open**, or choose the blob name and then choose the **Open** button, or double-click the blob name.</span><span class="sxs-lookup"><span data-stu-id="ec448-169">In **Server Explorer**, open the shortcut menu for one or more blobs and then choose **Open**, or choose the blob name and then choose the **Open** button, or double-click the blob name.</span></span>
  
    <span data-ttu-id="ec448-170">The progress of a blob download appears in the **Azure Activity Log** window.</span><span class="sxs-lookup"><span data-stu-id="ec448-170">The progress of a blob download appears in the **Azure Activity Log** window.</span></span>
  
    <span data-ttu-id="ec448-171">The blob opens in the default editor for that file type.</span><span class="sxs-lookup"><span data-stu-id="ec448-171">The blob opens in the default editor for that file type.</span></span> <span data-ttu-id="ec448-172">If the operating system recognizes the file type, the file opens in a locally installed application; otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span><span class="sxs-lookup"><span data-stu-id="ec448-172">If the operating system recognizes the file type, the file opens in a locally installed application; otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span></span> <span data-ttu-id="ec448-173">The local file that’s created when you download a blob is marked as read-only.</span><span class="sxs-lookup"><span data-stu-id="ec448-173">The local file that’s created when you download a blob is marked as read-only.</span></span>
  
    <span data-ttu-id="ec448-174">Blob data is cached locally and checked against the blob's last modified time in the Blob service.</span><span class="sxs-lookup"><span data-stu-id="ec448-174">Blob data is cached locally and checked against the blob's last modified time in the Blob service.</span></span> <span data-ttu-id="ec448-175">If the blob has been updated since it was last downloaded, it will be downloaded again; otherwise the blob will be loaded from the local disk.</span><span class="sxs-lookup"><span data-stu-id="ec448-175">If the blob has been updated since it was last downloaded, it will be downloaded again; otherwise the blob will be loaded from the local disk.</span></span> <span data-ttu-id="ec448-176">By default a blob is downloaded to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="ec448-176">By default a blob is downloaded to a temporary directory.</span></span> <span data-ttu-id="ec448-177">To download blobs to a specific directory, open the shortcut menu for the selected blob names and choose **Save As**.</span><span class="sxs-lookup"><span data-stu-id="ec448-177">To download blobs to a specific directory, open the shortcut menu for the selected blob names and choose **Save As**.</span></span> <span data-ttu-id="ec448-178">When you save a blob in this manner, the blob file is not opened, and the local file is created with read-write attributes.</span><span class="sxs-lookup"><span data-stu-id="ec448-178">When you save a blob in this manner, the blob file is not opened, and the local file is created with read-write attributes.</span></span>

### <a name="to-upload-blobs"></a><span data-ttu-id="ec448-179">To upload blobs</span><span class="sxs-lookup"><span data-stu-id="ec448-179">To upload blobs</span></span>
* <span data-ttu-id="ec448-180">Choose the **Upload Blob** button when the container is open for viewing in the blob container view.</span><span class="sxs-lookup"><span data-stu-id="ec448-180">Choose the **Upload Blob** button when the container is open for viewing in the blob container view.</span></span>
  
    <span data-ttu-id="ec448-181">You can choose one or more files to upload, and you can upload files of any type.</span><span class="sxs-lookup"><span data-stu-id="ec448-181">You can choose one or more files to upload, and you can upload files of any type.</span></span> <span data-ttu-id="ec448-182">The **Azure Activity Log** shows the progress of the upload.</span><span class="sxs-lookup"><span data-stu-id="ec448-182">The **Azure Activity Log** shows the progress of the upload.</span></span> <span data-ttu-id="ec448-183">For more information about how to work with blob data, see [How to use the Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span><span class="sxs-lookup"><span data-stu-id="ec448-183">For more information about how to work with blob data, see [How to use the Azure Blob Storage Service in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="to-view-logs-transferred-to-blobs"></a><span data-ttu-id="ec448-184">To view logs transferred to blobs</span><span class="sxs-lookup"><span data-stu-id="ec448-184">To view logs transferred to blobs</span></span>
* <span data-ttu-id="ec448-185">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that were created by Azure for these logs.</span><span class="sxs-lookup"><span data-stu-id="ec448-185">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that were created by Azure for these logs.</span></span> <span data-ttu-id="ec448-186">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it’s been deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="ec448-186">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it’s been deployed to Azure.</span></span> <span data-ttu-id="ec448-187">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec448-187">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="to-get-the-url-for-a-blob"></a><span data-ttu-id="ec448-188">To get the URL for a blob</span><span class="sxs-lookup"><span data-stu-id="ec448-188">To get the URL for a blob</span></span>
* <span data-ttu-id="ec448-189">Open the blob’s shortcut menu and then choose **Copy URL**.</span><span class="sxs-lookup"><span data-stu-id="ec448-189">Open the blob’s shortcut menu and then choose **Copy URL**.</span></span>

### <a name="to-edit-a-blob"></a><span data-ttu-id="ec448-190">To edit a blob</span><span class="sxs-lookup"><span data-stu-id="ec448-190">To edit a blob</span></span>
* <span data-ttu-id="ec448-191">Select the blob and then choose the **Open Blob** button.</span><span class="sxs-lookup"><span data-stu-id="ec448-191">Select the blob and then choose the **Open Blob** button.</span></span>
  
    <span data-ttu-id="ec448-192">The file is downloaded to a temporary location and opened on the local computer.</span><span class="sxs-lookup"><span data-stu-id="ec448-192">The file is downloaded to a temporary location and opened on the local computer.</span></span> <span data-ttu-id="ec448-193">You must upload the blob again after you make changes.</span><span class="sxs-lookup"><span data-stu-id="ec448-193">You must upload the blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="ec448-194">Work with Queue Resources</span><span class="sxs-lookup"><span data-stu-id="ec448-194">Work with Queue Resources</span></span>
<span data-ttu-id="ec448-195">Storage services queues are hosted in an Azure storage account and you can use them to allow your cloud service roles to communicate with each other and with other services by a message passing mechanism.</span><span class="sxs-lookup"><span data-stu-id="ec448-195">Storage services queues are hosted in an Azure storage account and you can use them to allow your cloud service roles to communicate with each other and with other services by a message passing mechanism.</span></span> <span data-ttu-id="ec448-196">You can access the queue programmatically through a cloud service and over a web service for external clients.</span><span class="sxs-lookup"><span data-stu-id="ec448-196">You can access the queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="ec448-197">You can also access the queue directly by using Server Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec448-197">You can also access the queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="ec448-198">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span><span class="sxs-lookup"><span data-stu-id="ec448-198">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="ec448-199">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span><span class="sxs-lookup"><span data-stu-id="ec448-199">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span></span> <span data-ttu-id="ec448-200">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the top-left corner:</span><span class="sxs-lookup"><span data-stu-id="ec448-200">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the top-left corner:</span></span>

* <span data-ttu-id="ec448-201">Refresh the view of the queue</span><span class="sxs-lookup"><span data-stu-id="ec448-201">Refresh the view of the queue</span></span>
* <span data-ttu-id="ec448-202">Add a message to the queue</span><span class="sxs-lookup"><span data-stu-id="ec448-202">Add a message to the queue</span></span>
* <span data-ttu-id="ec448-203">Dequeue the topmost message.</span><span class="sxs-lookup"><span data-stu-id="ec448-203">Dequeue the topmost message.</span></span>
* <span data-ttu-id="ec448-204">Clear the entire queue</span><span class="sxs-lookup"><span data-stu-id="ec448-204">Clear the entire queue</span></span>

<span data-ttu-id="ec448-205">The following image shows a queue that contains two messages.</span><span class="sxs-lookup"><span data-stu-id="ec448-205">The following image shows a queue that contains two messages.</span></span>

![Viewing a Queue](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="ec448-207">For more information about storage services queues, see [How to: Use the Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span><span class="sxs-lookup"><span data-stu-id="ec448-207">For more information about storage services queues, see [How to: Use the Queue Storage Service](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="ec448-208">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span><span class="sxs-lookup"><span data-stu-id="ec448-208">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="ec448-209">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec448-209">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://msdn.microsoft.com/library/azure/jj649344.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="ec448-210">Storage services queues are distinct from service bus queues.</span><span class="sxs-lookup"><span data-stu-id="ec448-210">Storage services queues are distinct from service bus queues.</span></span> <span data-ttu-id="ec448-211">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span><span class="sxs-lookup"><span data-stu-id="ec448-211">For more information about service bus queues, see Service Bus Queues, Topics, and Subscriptions.</span></span>
> 
> 

## <a name="work-with-table-resources"></a><span data-ttu-id="ec448-212">Work with Table Resources</span><span class="sxs-lookup"><span data-stu-id="ec448-212">Work with Table Resources</span></span>
<span data-ttu-id="ec448-213">The Azure Table storage service stores large amounts of structured data.</span><span class="sxs-lookup"><span data-stu-id="ec448-213">The Azure Table storage service stores large amounts of structured data.</span></span> <span data-ttu-id="ec448-214">The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="ec448-214">The service is a NoSQL datastore which accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="ec448-215">Azure tables are ideal for storing structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="ec448-215">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="to-create-a-table"></a><span data-ttu-id="ec448-216">To create a table</span><span class="sxs-lookup"><span data-stu-id="ec448-216">To create a table</span></span>
1. <span data-ttu-id="ec448-217">In Server Explorer, select the **Tables** node of the storage account, and then choose **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="ec448-217">In Server Explorer, select the **Tables** node of the storage account, and then choose **Create Table**.</span></span>
2. <span data-ttu-id="ec448-218">In the **Create Table** dialog box, enter a name for the table.</span><span class="sxs-lookup"><span data-stu-id="ec448-218">In the **Create Table** dialog box, enter a name for the table.</span></span>

### <a name="to-view-table-data"></a><span data-ttu-id="ec448-219">To view table data</span><span class="sxs-lookup"><span data-stu-id="ec448-219">To view table data</span></span>
1. <span data-ttu-id="ec448-220">In Server Explorer, open the **Azure** node, and then open the **Storage** node.</span><span class="sxs-lookup"><span data-stu-id="ec448-220">In Server Explorer, open the **Azure** node, and then open the **Storage** node.</span></span>
2. <span data-ttu-id="ec448-221">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-221">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span></span>
3. <span data-ttu-id="ec448-222">Open the shortcut menu for a table and then choose **View Table**.</span><span class="sxs-lookup"><span data-stu-id="ec448-222">Open the shortcut menu for a table and then choose **View Table**.</span></span>
   
    ![An Azure table in Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="ec448-224">The table is organized by entities (shown in rows) and properties (shown in columns).</span><span class="sxs-lookup"><span data-stu-id="ec448-224">The table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="ec448-225">For example, the following illustration shows entities listed in the **Table Designer**:</span><span class="sxs-lookup"><span data-stu-id="ec448-225">For example, the following illustration shows entities listed in the **Table Designer**:</span></span>

### <a name="to-edit-table-data"></a><span data-ttu-id="ec448-226">To edit table data</span><span class="sxs-lookup"><span data-stu-id="ec448-226">To edit table data</span></span>
1. <span data-ttu-id="ec448-227">In the **Table Designer**, open the shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span><span class="sxs-lookup"><span data-stu-id="ec448-227">In the **Table Designer**, open the shortcut menu for an entity (a single row) or a property (a single cell) and then choose **Edit**.</span></span>
   
    ![Add or Edit a Table Entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    <span data-ttu-id="ec448-229">Entities in a single table aren’t required to have the same set of properties (columns).</span><span class="sxs-lookup"><span data-stu-id="ec448-229">Entities in a single table aren’t required to have the same set of properties (columns).</span></span> <span data-ttu-id="ec448-230">Keep in mind the following restrictions on viewing and editing table data.</span><span class="sxs-lookup"><span data-stu-id="ec448-230">Keep in mind the following restrictions on viewing and editing table data.</span></span>
   
   * <span data-ttu-id="ec448-231">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span><span class="sxs-lookup"><span data-stu-id="ec448-231">You can’t view or edit binary data (type byte[]), but you can store it in a table.</span></span>
   * <span data-ttu-id="ec448-232">You can’t edit the **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span><span class="sxs-lookup"><span data-stu-id="ec448-232">You can’t edit the **PartitionKey** or **RowKey** values, because table storage in Azure doesn't support that operation.</span></span>
   * <span data-ttu-id="ec448-233">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span><span class="sxs-lookup"><span data-stu-id="ec448-233">You can’t create a property called Timestamp, Azure Storage services use a property with that name.</span></span>
   * <span data-ttu-id="ec448-234">If you enter a DateTime value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span><span class="sxs-lookup"><span data-stu-id="ec448-234">If you enter a DateTime value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for U.S. English).</span></span>

### <a name="to-add-entities"></a><span data-ttu-id="ec448-235">To add entities</span><span class="sxs-lookup"><span data-stu-id="ec448-235">To add entities</span></span>
1. <span data-ttu-id="ec448-236">In the **Table Designer**, choose the **Add Entity** button, which is near the top-right corner of the table view.</span><span class="sxs-lookup"><span data-stu-id="ec448-236">In the **Table Designer**, choose the **Add Entity** button, which is near the top-right corner of the table view.</span></span>
   
    ![Add Entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. <span data-ttu-id="ec448-238">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span><span class="sxs-lookup"><span data-stu-id="ec448-238">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span></span>
   
    ![Add Entity Dialog Box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    <span data-ttu-id="ec448-240">Enter the values carefully because you can't change them after you close the dialog box unless you delete the entity and add it again.</span><span class="sxs-lookup"><span data-stu-id="ec448-240">Enter the values carefully because you can't change them after you close the dialog box unless you delete the entity and add it again.</span></span>

### <a name="to-filter-entities"></a><span data-ttu-id="ec448-241">To filter entities</span><span class="sxs-lookup"><span data-stu-id="ec448-241">To filter entities</span></span>
<span data-ttu-id="ec448-242">You can customize the set of entities that appear in a table if you use the query builder.</span><span class="sxs-lookup"><span data-stu-id="ec448-242">You can customize the set of entities that appear in a table if you use the query builder.</span></span>

1. <span data-ttu-id="ec448-243">To open the query builder, open a table for viewing.</span><span class="sxs-lookup"><span data-stu-id="ec448-243">To open the query builder, open a table for viewing.</span></span>
2. <span data-ttu-id="ec448-244">Choose the rightmost button on the table view’s toolbar.</span><span class="sxs-lookup"><span data-stu-id="ec448-244">Choose the rightmost button on the table view’s toolbar.</span></span>
   
    <span data-ttu-id="ec448-245">The **Query Builder** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="ec448-245">The **Query Builder** dialog box appears.</span></span> <span data-ttu-id="ec448-246">The following illustration shows a query that's being built in the query builder.</span><span class="sxs-lookup"><span data-stu-id="ec448-246">The following illustration shows a query that's being built in the query builder.</span></span>
   
    ![Query Builder](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. <span data-ttu-id="ec448-248">When you’re done building the query, close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="ec448-248">When you’re done building the query, close the dialog box.</span></span> <span data-ttu-id="ec448-249">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span><span class="sxs-lookup"><span data-stu-id="ec448-249">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span></span>
4. <span data-ttu-id="ec448-250">To run the query, choose the green triangle icon.</span><span class="sxs-lookup"><span data-stu-id="ec448-250">To run the query, choose the green triangle icon.</span></span>
   
    <span data-ttu-id="ec448-251">You can also filter entity data that appears in the **Table Designer** if you enter a WCF Data Services filter string directly in the filter field.</span><span class="sxs-lookup"><span data-stu-id="ec448-251">You can also filter entity data that appears in the **Table Designer** if you enter a WCF Data Services filter string directly in the filter field.</span></span> <span data-ttu-id="ec448-252">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="ec448-252">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span></span> <span data-ttu-id="ec448-253">For information about how to construct filter strings, see [Constructing Filter Strings for the Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec448-253">For information about how to construct filter strings, see [Constructing Filter Strings for the Table Designer](https://msdn.microsoft.com/library/azure/ff683669.aspx).</span></span>
   
    <span data-ttu-id="ec448-254">The following illustration shows an example of a valid filter string:</span><span class="sxs-lookup"><span data-stu-id="ec448-254">The following illustration shows an example of a valid filter string:</span></span>
   
    ![VST_SE_TableFilter](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a><span data-ttu-id="ec448-256">Refresh storage data</span><span class="sxs-lookup"><span data-stu-id="ec448-256">Refresh storage data</span></span>
<span data-ttu-id="ec448-257">When Server Explorer connects to or gets data from a storage account, it might take up to a minute for the operation to complete.</span><span class="sxs-lookup"><span data-stu-id="ec448-257">When Server Explorer connects to or gets data from a storage account, it might take up to a minute for the operation to complete.</span></span> <span data-ttu-id="ec448-258">If it can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ec448-258">If it can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span></span> <span data-ttu-id="ec448-259">To cancel the operation if it’s taking too long, choose the **Stop Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="ec448-259">To cancel the operation if it’s taking too long, choose the **Stop Refresh** button on the Server Explorer toolbar.</span></span>

#### <a name="to-refresh-blob-container-data"></a><span data-ttu-id="ec448-260">To refresh blob container data</span><span class="sxs-lookup"><span data-stu-id="ec448-260">To refresh blob container data</span></span>
* <span data-ttu-id="ec448-261">Select the **Blobs** node beneath **Storage** and choose the **Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="ec448-261">Select the **Blobs** node beneath **Storage** and choose the **Refresh** button on the Server Explorer toolbar.</span></span>
* <span data-ttu-id="ec448-262">To refresh the list of blobs that is displayed, choose the **Execute** button.</span><span class="sxs-lookup"><span data-stu-id="ec448-262">To refresh the list of blobs that is displayed, choose the **Execute** button.</span></span>

#### <a name="to-refresh-table-data"></a><span data-ttu-id="ec448-263">To refresh table data</span><span class="sxs-lookup"><span data-stu-id="ec448-263">To refresh table data</span></span>
* <span data-ttu-id="ec448-264">Select the **Tables** node beneath **Storage** and choose the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="ec448-264">Select the **Tables** node beneath **Storage** and choose the **Refresh** button.</span></span>
* <span data-ttu-id="ec448-265">To refresh the list of entities that is displayed in the **Table Designer**, choose the **Execute** button on the **Table Designer**.</span><span class="sxs-lookup"><span data-stu-id="ec448-265">To refresh the list of entities that is displayed in the **Table Designer**, choose the **Execute** button on the **Table Designer**.</span></span>

#### <a name="to-refresh-queue-data"></a><span data-ttu-id="ec448-266">To refresh queue data</span><span class="sxs-lookup"><span data-stu-id="ec448-266">To refresh queue data</span></span>
* <span data-ttu-id="ec448-267">Select the **Queues** node, and then choose the **Refresh** button.</span><span class="sxs-lookup"><span data-stu-id="ec448-267">Select the **Queues** node, and then choose the **Refresh** button.</span></span>

#### <a name="to-refresh-all-items-in-a-storage-account"></a><span data-ttu-id="ec448-268">To refresh all items in a storage account</span><span class="sxs-lookup"><span data-stu-id="ec448-268">To refresh all items in a storage account</span></span>
* <span data-ttu-id="ec448-269">Choose the account name, and then choose the **Refresh** button on the toolbar for Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-269">Choose the account name, and then choose the **Refresh** button on the toolbar for Server Explorer.</span></span>

### <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="ec448-270">Add storage accounts by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="ec448-270">Add storage accounts by using Server Explorer</span></span>
<span data-ttu-id="ec448-271">There are two ways to add storage accounts by using Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-271">There are two ways to add storage accounts by using Server Explorer.</span></span> <span data-ttu-id="ec448-272">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-272">You can create a new storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

#### <a name="to-create-a-new-storage-account-by-using-server-explorer"></a><span data-ttu-id="ec448-273">To create a new storage account by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="ec448-273">To create a new storage account by using Server Explorer</span></span>
1. <span data-ttu-id="ec448-274">In Server Explorer, open the shortcut menu for the Storage node, and then choose Create Storage Account.</span><span class="sxs-lookup"><span data-stu-id="ec448-274">In Server Explorer, open the shortcut menu for the Storage node, and then choose Create Storage Account.</span></span>
   
    ![Create a new Azure storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. <span data-ttu-id="ec448-276">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ec448-276">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="ec448-277">The Azure subscription to which you want to add the storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-277">The Azure subscription to which you want to add the storage account.</span></span>
   * <span data-ttu-id="ec448-278">The name you want to use for the new storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-278">The name you want to use for the new storage account.</span></span>
   * <span data-ttu-id="ec448-279">The region or affinity group (such as West US or East Asia).</span><span class="sxs-lookup"><span data-stu-id="ec448-279">The region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="ec448-280">The type of replication you want to use for the storage account, such as Geo-Redundant.</span><span class="sxs-lookup"><span data-stu-id="ec448-280">The type of replication you want to use for the storage account, such as Geo-Redundant.</span></span>
3. <span data-ttu-id="ec448-281">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="ec448-281">Choose **Create**.</span></span>
   
    <span data-ttu-id="ec448-282">The new storage account appears in the **Storage** list in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-282">The new storage account appears in the **Storage** list in Solution Explorer.</span></span>

#### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="ec448-283">To attach an existing storage account by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="ec448-283">To attach an existing storage account by using Server Explorer</span></span>
1. <span data-ttu-id="ec448-284">In Server Explorer, open the shortcut menu for the Azure storage node, and then choose **Attach External Storage**.</span><span class="sxs-lookup"><span data-stu-id="ec448-284">In Server Explorer, open the shortcut menu for the Azure storage node, and then choose **Attach External Storage**.</span></span>
   
    ![Adding an existing storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. <span data-ttu-id="ec448-286">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span><span class="sxs-lookup"><span data-stu-id="ec448-286">Select or enter the following information for the new storage account in the **Create Storage Account** dialog box.</span></span>
   
   * <span data-ttu-id="ec448-287">The name of the existing storage account you want to attach.</span><span class="sxs-lookup"><span data-stu-id="ec448-287">The name of the existing storage account you want to attach.</span></span> <span data-ttu-id="ec448-288">You can enter a name or select it from the list.</span><span class="sxs-lookup"><span data-stu-id="ec448-288">You can enter a name or select it from the list.</span></span>
   * <span data-ttu-id="ec448-289">The key for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-289">The key for the selected storage account.</span></span> <span data-ttu-id="ec448-290">This value is typically provided for you when you select a storage account.</span><span class="sxs-lookup"><span data-stu-id="ec448-290">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="ec448-291">If you want Visual Studio to remember the storage account key, select the Remember account key box.</span><span class="sxs-lookup"><span data-stu-id="ec448-291">If you want Visual Studio to remember the storage account key, select the Remember account key box.</span></span>
   * <span data-ttu-id="ec448-292">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span><span class="sxs-lookup"><span data-stu-id="ec448-292">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="ec448-293">See [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span><span class="sxs-lookup"><span data-stu-id="ec448-293">See [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx) for more information about custom endpoints.</span></span>

### <a name="to-view-the-secondary-endpoints"></a><span data-ttu-id="ec448-294">To view the secondary endpoints</span><span class="sxs-lookup"><span data-stu-id="ec448-294">To view the secondary endpoints</span></span>
* <span data-ttu-id="ec448-295">If you created a storage account using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span><span class="sxs-lookup"><span data-stu-id="ec448-295">If you created a storage account using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints.</span></span> <span data-ttu-id="ec448-296">Open the shortcut menu for the account name, and then choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="ec448-296">Open the shortcut menu for the account name, and then choose **Properties**.</span></span>
  
    ![Storage secondary endpoints](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a><span data-ttu-id="ec448-298">To remove a storage account from Server Explorer</span><span class="sxs-lookup"><span data-stu-id="ec448-298">To remove a storage account from Server Explorer</span></span>
* <span data-ttu-id="ec448-299">In Server Explorer, open the shortcut menu for the account name, and then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ec448-299">In Server Explorer, open the shortcut menu for the account name, and then choose **Delete**.</span></span> <span data-ttu-id="ec448-300">If you delete a storage account, any saved key information for that account is also removed.</span><span class="sxs-lookup"><span data-stu-id="ec448-300">If you delete a storage account, any saved key information for that account is also removed.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="ec448-301">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes the reference from Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="ec448-301">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains; it simply removes the reference from Server Explorer.</span></span> <span data-ttu-id="ec448-302">To permanently delete a storage account, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="ec448-302">To permanently delete a storage account, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
  > 
  > 

## <a name="next-steps"></a><span data-ttu-id="ec448-303">Next steps</span><span class="sxs-lookup"><span data-stu-id="ec448-303">Next steps</span></span>
<span data-ttu-id="ec448-304">To learn more about how use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec448-304">To learn more about how use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>















