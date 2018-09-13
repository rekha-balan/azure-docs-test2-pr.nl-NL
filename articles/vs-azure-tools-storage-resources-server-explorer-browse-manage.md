---
title: Browse and manage storage resources by using Server Explorer | Microsoft Docs
description: Browsing and managing storage resources by using Server Explorer
services: visual-studio-online
author: ghogen
manager: douge
assetId: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/24/2017
ms.author: ghogen
ms.openlocfilehash: 74f5508586d073bcccc54894cce6fcde1b83fe18
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776964"
---
# <a name="browse-and-manage-storage-resources-by-using-server-explorer"></a><span data-ttu-id="daf6d-103">Browse and manage storage resources by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="daf6d-103">Browse and manage storage resources by using Server Explorer</span></span>

[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a><span data-ttu-id="daf6d-104">Overview</span><span class="sxs-lookup"><span data-stu-id="daf6d-104">Overview</span></span>

<span data-ttu-id="daf6d-105">If you've installed Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span><span class="sxs-lookup"><span data-stu-id="daf6d-105">If you've installed Azure Tools for Microsoft Visual Studio, you can view blob, queue, and table data from your storage accounts for Azure.</span></span> <span data-ttu-id="daf6d-106">The Azure **Storage** node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="daf6d-106">The Azure **Storage** node in Server Explorer shows data that’s in your local storage emulator account and your other Azure storage accounts.</span></span>

<span data-ttu-id="daf6d-107">To view Server Explorer in Visual Studio, on the menu bar, select **View** > **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-107">To view Server Explorer in Visual Studio, on the menu bar, select **View** > **Server Explorer**.</span></span> <span data-ttu-id="daf6d-108">The **Storage** node shows all of the storage accounts that exist under each Azure subscription or certificate that you're connected to.</span><span class="sxs-lookup"><span data-stu-id="daf6d-108">The **Storage** node shows all of the storage accounts that exist under each Azure subscription or certificate that you're connected to.</span></span> <span data-ttu-id="daf6d-109">If your storage account doesn't appear, you can add it by following the instructions [later in this article](#add-storage-accounts-by-using-server-explorer).</span><span class="sxs-lookup"><span data-stu-id="daf6d-109">If your storage account doesn't appear, you can add it by following the instructions [later in this article](#add-storage-accounts-by-using-server-explorer).</span></span>

<span data-ttu-id="daf6d-110">Starting in Azure SDK 2.7, you can also use Cloud Explorer to view and manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="daf6d-110">Starting in Azure SDK 2.7, you can also use Cloud Explorer to view and manage your Azure resources.</span></span> <span data-ttu-id="daf6d-111">For more information, see [Managing Azure resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="daf6d-111">For more information, see [Managing Azure resources with Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md).</span></span>

## <a name="view-and-manage-storage-resources-in-visual-studio"></a><span data-ttu-id="daf6d-112">View and manage storage resources in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="daf6d-112">View and manage storage resources in Visual Studio</span></span>

<span data-ttu-id="daf6d-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-113">Server Explorer automatically shows a list of blobs, queues, and tables in your storage emulator account.</span></span> <span data-ttu-id="daf6d-114">The storage emulator account is listed in Server Explorer under the **Storage** node as the **Development** node.</span><span class="sxs-lookup"><span data-stu-id="daf6d-114">The storage emulator account is listed in Server Explorer under the **Storage** node as the **Development** node.</span></span>

<span data-ttu-id="daf6d-115">To see the storage emulator account’s resources, expand the **Development** node.</span><span class="sxs-lookup"><span data-stu-id="daf6d-115">To see the storage emulator account’s resources, expand the **Development** node.</span></span> <span data-ttu-id="daf6d-116">If the storage emulator hasn’t been started when you expand the **Development** node, it automatically starts.</span><span class="sxs-lookup"><span data-stu-id="daf6d-116">If the storage emulator hasn’t been started when you expand the **Development** node, it automatically starts.</span></span> <span data-ttu-id="daf6d-117">This process can take several seconds.</span><span class="sxs-lookup"><span data-stu-id="daf6d-117">This process can take several seconds.</span></span> <span data-ttu-id="daf6d-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span><span class="sxs-lookup"><span data-stu-id="daf6d-118">You can continue to work in other areas of Visual Studio while the storage emulator starts.</span></span>

<span data-ttu-id="daf6d-119">To view resources in a storage account, expand the storage account’s node in Server Explorer where you see **Blobs**, **Queues**, and **Tables** nodes.</span><span class="sxs-lookup"><span data-stu-id="daf6d-119">To view resources in a storage account, expand the storage account’s node in Server Explorer where you see **Blobs**, **Queues**, and **Tables** nodes.</span></span>

## <a name="work-with-blob-resources"></a><span data-ttu-id="daf6d-120">Work with blob resources</span><span class="sxs-lookup"><span data-stu-id="daf6d-120">Work with blob resources</span></span>

<span data-ttu-id="daf6d-121">The **Blobs** node displays a list of containers for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-121">The **Blobs** node displays a list of containers for the selected storage account.</span></span> <span data-ttu-id="daf6d-122">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span><span class="sxs-lookup"><span data-stu-id="daf6d-122">Blob containers contain blob files, and you can organize these blobs into folders and subfolders.</span></span> <span data-ttu-id="daf6d-123">For more information, see [How to use Blob storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="daf6d-123">For more information, see [How to use Blob storage from .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

### <a name="to-create-a-blob-container"></a><span data-ttu-id="daf6d-124">To create a blob container</span><span class="sxs-lookup"><span data-stu-id="daf6d-124">To create a blob container</span></span>

1. <span data-ttu-id="daf6d-125">Open the shortcut menu for the **Blobs** node, and then select **Create Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-125">Open the shortcut menu for the **Blobs** node, and then select **Create Blob Container**.</span></span>
1. <span data-ttu-id="daf6d-126">In the **Create Blob Container** dialog box, enter the name of the new container.</span><span class="sxs-lookup"><span data-stu-id="daf6d-126">In the **Create Blob Container** dialog box, enter the name of the new container.</span></span>  
1. <span data-ttu-id="daf6d-127">Select Enter on your keyboard, or you can click or tap outside the name field to save the blob container.</span><span class="sxs-lookup"><span data-stu-id="daf6d-127">Select Enter on your keyboard, or you can click or tap outside the name field to save the blob container.</span></span>

   > [!NOTE]
   > <span data-ttu-id="daf6d-128">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span><span class="sxs-lookup"><span data-stu-id="daf6d-128">The blob container name must begin with a number (0-9) or lowercase letter (a-z).</span></span>

### <a name="to-delete-a-blob-container"></a><span data-ttu-id="daf6d-129">To delete a blob container</span><span class="sxs-lookup"><span data-stu-id="daf6d-129">To delete a blob container</span></span>

<span data-ttu-id="daf6d-130">Open the shortcut menu for the blob container that you want to remove, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-130">Open the shortcut menu for the blob container that you want to remove, and then select **Delete**.</span></span>

### <a name="to-display-a-list-of-the-items-in-a-blob-container"></a><span data-ttu-id="daf6d-131">To display a list of the items in a blob container</span><span class="sxs-lookup"><span data-stu-id="daf6d-131">To display a list of the items in a blob container</span></span>

<span data-ttu-id="daf6d-132">Open the shortcut menu for a blob container name in the list, and then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-132">Open the shortcut menu for a blob container name in the list, and then select **Open**.</span></span>

<span data-ttu-id="daf6d-133">When you view the contents of a blob container, it appears on a tab known as the blob container view.</span><span class="sxs-lookup"><span data-stu-id="daf6d-133">When you view the contents of a blob container, it appears on a tab known as the blob container view.</span></span>

![Blob container view](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)

<span data-ttu-id="daf6d-135">You can perform the following operations on blobs by using the buttons in the upper-right corner of the blob container view:</span><span class="sxs-lookup"><span data-stu-id="daf6d-135">You can perform the following operations on blobs by using the buttons in the upper-right corner of the blob container view:</span></span>

* <span data-ttu-id="daf6d-136">Enter a filter value and apply it.</span><span class="sxs-lookup"><span data-stu-id="daf6d-136">Enter a filter value and apply it.</span></span>
* <span data-ttu-id="daf6d-137">Refresh the list of blobs in the container.</span><span class="sxs-lookup"><span data-stu-id="daf6d-137">Refresh the list of blobs in the container.</span></span>
* <span data-ttu-id="daf6d-138">Upload a file.</span><span class="sxs-lookup"><span data-stu-id="daf6d-138">Upload a file.</span></span>
* <span data-ttu-id="daf6d-139">Delete a blob.</span><span class="sxs-lookup"><span data-stu-id="daf6d-139">Delete a blob.</span></span> <span data-ttu-id="daf6d-140">(Deleting a file from a blob container doesn’t delete the underlying file.</span><span class="sxs-lookup"><span data-stu-id="daf6d-140">(Deleting a file from a blob container doesn’t delete the underlying file.</span></span> <span data-ttu-id="daf6d-141">It only removes it from the blob container.)</span><span class="sxs-lookup"><span data-stu-id="daf6d-141">It only removes it from the blob container.)</span></span>
* <span data-ttu-id="daf6d-142">Open a blob.</span><span class="sxs-lookup"><span data-stu-id="daf6d-142">Open a blob.</span></span>
* <span data-ttu-id="daf6d-143">Save a blob to the local computer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-143">Save a blob to the local computer.</span></span>

### <a name="to-create-a-folder-or-subfolder-in-a-blob-container"></a><span data-ttu-id="daf6d-144">To create a folder or subfolder in a blob container</span><span class="sxs-lookup"><span data-stu-id="daf6d-144">To create a folder or subfolder in a blob container</span></span>

1. <span data-ttu-id="daf6d-145">Choose the blob container in Cloud Explorer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-145">Choose the blob container in Cloud Explorer.</span></span> <span data-ttu-id="daf6d-146">In the container window, select the **Upload Blob** button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-146">In the container window, select the **Upload Blob** button.</span></span>

1. <span data-ttu-id="daf6d-147">In the **Upload New File** dialog box, select the **Browse** button to specify the file that you want to upload, and then enter a folder name in the **Folder (optional)** box.</span><span class="sxs-lookup"><span data-stu-id="daf6d-147">In the **Upload New File** dialog box, select the **Browse** button to specify the file that you want to upload, and then enter a folder name in the **Folder (optional)** box.</span></span>

   ![Uploading a file into a blob folder](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)

   <span data-ttu-id="daf6d-149">You can add subfolders in container folders by following the same step.</span><span class="sxs-lookup"><span data-stu-id="daf6d-149">You can add subfolders in container folders by following the same step.</span></span> <span data-ttu-id="daf6d-150">If you don’t specify a folder name, the file is uploaded to the top level of the blob container.</span><span class="sxs-lookup"><span data-stu-id="daf6d-150">If you don’t specify a folder name, the file is uploaded to the top level of the blob container.</span></span> <span data-ttu-id="daf6d-151">The file appears in the specified folder in the container.</span><span class="sxs-lookup"><span data-stu-id="daf6d-151">The file appears in the specified folder in the container.</span></span>

   ![Folder added to a blob container](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)

1. <span data-ttu-id="daf6d-153">Double-click the folder or select Enter to see the contents of the folder.</span><span class="sxs-lookup"><span data-stu-id="daf6d-153">Double-click the folder or select Enter to see the contents of the folder.</span></span> <span data-ttu-id="daf6d-154">When you’re in the container’s folder, you can go back to the root of the container by selecting the **Open Parent Directory** (arrow) button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-154">When you’re in the container’s folder, you can go back to the root of the container by selecting the **Open Parent Directory** (arrow) button.</span></span>

### <a name="to-delete-a-container-folder"></a><span data-ttu-id="daf6d-155">To delete a container folder</span><span class="sxs-lookup"><span data-stu-id="daf6d-155">To delete a container folder</span></span>

<span data-ttu-id="daf6d-156">Delete all the files in the folder.</span><span class="sxs-lookup"><span data-stu-id="daf6d-156">Delete all the files in the folder.</span></span>

<span data-ttu-id="daf6d-157">Because folders in blob containers are virtual folders, you can't create an empty folder.</span><span class="sxs-lookup"><span data-stu-id="daf6d-157">Because folders in blob containers are virtual folders, you can't create an empty folder.</span></span> <span data-ttu-id="daf6d-158">You also can't delete a folder to delete its file contents, but must instead delete the entire contents of a folder to delete the folder itself.</span><span class="sxs-lookup"><span data-stu-id="daf6d-158">You also can't delete a folder to delete its file contents, but must instead delete the entire contents of a folder to delete the folder itself.</span></span>

### <a name="to-filter-blobs-in-a-container"></a><span data-ttu-id="daf6d-159">To filter blobs in a container</span><span class="sxs-lookup"><span data-stu-id="daf6d-159">To filter blobs in a container</span></span>

<span data-ttu-id="daf6d-160">You can filter the blobs that are displayed by specifying a common prefix.</span><span class="sxs-lookup"><span data-stu-id="daf6d-160">You can filter the blobs that are displayed by specifying a common prefix.</span></span>

<span data-ttu-id="daf6d-161">For example, if you enter the prefix **hello** in the filter text box and then select the **Execute** (**!**) button, only blobs that begin with "hello" appear.</span><span class="sxs-lookup"><span data-stu-id="daf6d-161">For example, if you enter the prefix **hello** in the filter text box and then select the **Execute** (**!**) button, only blobs that begin with "hello" appear.</span></span>

![Filter text box](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

<span data-ttu-id="daf6d-163">The filter text box is case-sensitive and doesn’t support filtering with wildcard characters.</span><span class="sxs-lookup"><span data-stu-id="daf6d-163">The filter text box is case-sensitive and doesn’t support filtering with wildcard characters.</span></span> <span data-ttu-id="daf6d-164">Blobs can be filtered only by prefix.</span><span class="sxs-lookup"><span data-stu-id="daf6d-164">Blobs can be filtered only by prefix.</span></span> <span data-ttu-id="daf6d-165">The prefix can include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span><span class="sxs-lookup"><span data-stu-id="daf6d-165">The prefix can include a delimiter if you are using a delimiter to organize blobs in a virtual hierarchy.</span></span> <span data-ttu-id="daf6d-166">For example, filtering on the prefix "HelloFabric/" returns all blobs that begin with that string.</span><span class="sxs-lookup"><span data-stu-id="daf6d-166">For example, filtering on the prefix "HelloFabric/" returns all blobs that begin with that string.</span></span>

### <a name="to-download-blob-data"></a><span data-ttu-id="daf6d-167">To download blob data</span><span class="sxs-lookup"><span data-stu-id="daf6d-167">To download blob data</span></span>

<span data-ttu-id="daf6d-168">In Cloud Explorer, use any of the following methods:</span><span class="sxs-lookup"><span data-stu-id="daf6d-168">In Cloud Explorer, use any of the following methods:</span></span>

* <span data-ttu-id="daf6d-169">Open the shortcut menu for one or more blobs, and then select **Open**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-169">Open the shortcut menu for one or more blobs, and then select **Open**.</span></span>
* <span data-ttu-id="daf6d-170">Choose the blob name and then select the **Open** button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-170">Choose the blob name and then select the **Open** button.</span></span>
* <span data-ttu-id="daf6d-171">Double-click the blob name.</span><span class="sxs-lookup"><span data-stu-id="daf6d-171">Double-click the blob name.</span></span>

<span data-ttu-id="daf6d-172">The progress of a blob download appears in the **Azure Activity Log** window.</span><span class="sxs-lookup"><span data-stu-id="daf6d-172">The progress of a blob download appears in the **Azure Activity Log** window.</span></span>

<span data-ttu-id="daf6d-173">The blob opens in the default editor for that file type.</span><span class="sxs-lookup"><span data-stu-id="daf6d-173">The blob opens in the default editor for that file type.</span></span> <span data-ttu-id="daf6d-174">If the operating system recognizes the file type, the file opens in a locally installed application.</span><span class="sxs-lookup"><span data-stu-id="daf6d-174">If the operating system recognizes the file type, the file opens in a locally installed application.</span></span> <span data-ttu-id="daf6d-175">Otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span><span class="sxs-lookup"><span data-stu-id="daf6d-175">Otherwise, you're prompted to choose an application that’s appropriate for the file type of the blob.</span></span> <span data-ttu-id="daf6d-176">The local file that’s created when you download a blob is marked as read-only.</span><span class="sxs-lookup"><span data-stu-id="daf6d-176">The local file that’s created when you download a blob is marked as read-only.</span></span>

<span data-ttu-id="daf6d-177">Blob data is cached locally and checked against the blob's last-modified time in Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="daf6d-177">Blob data is cached locally and checked against the blob's last-modified time in Azure Blob storage.</span></span> <span data-ttu-id="daf6d-178">If the blob has been updated since it was last downloaded, it's downloaded again.</span><span class="sxs-lookup"><span data-stu-id="daf6d-178">If the blob has been updated since it was last downloaded, it's downloaded again.</span></span> <span data-ttu-id="daf6d-179">Otherwise, the blob is loaded from the local disk.</span><span class="sxs-lookup"><span data-stu-id="daf6d-179">Otherwise, the blob is loaded from the local disk.</span></span>

<span data-ttu-id="daf6d-180">By default, a blob is downloaded to a temporary directory.</span><span class="sxs-lookup"><span data-stu-id="daf6d-180">By default, a blob is downloaded to a temporary directory.</span></span> <span data-ttu-id="daf6d-181">To download blobs to a specific directory, open the shortcut menu for the selected blob names and select **Save As**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-181">To download blobs to a specific directory, open the shortcut menu for the selected blob names and select **Save As**.</span></span> <span data-ttu-id="daf6d-182">When you save a blob in this manner, the blob file is not opened, and the local file is created with read/write attributes.</span><span class="sxs-lookup"><span data-stu-id="daf6d-182">When you save a blob in this manner, the blob file is not opened, and the local file is created with read/write attributes.</span></span>

### <a name="to-upload-blobs"></a><span data-ttu-id="daf6d-183">To upload blobs</span><span class="sxs-lookup"><span data-stu-id="daf6d-183">To upload blobs</span></span>

<span data-ttu-id="daf6d-184">To upload blobs, select the **Upload Blob** button when the container is open for viewing in the blob container view.</span><span class="sxs-lookup"><span data-stu-id="daf6d-184">To upload blobs, select the **Upload Blob** button when the container is open for viewing in the blob container view.</span></span>

<span data-ttu-id="daf6d-185">You can choose one or more files to upload, and you can upload files of any type.</span><span class="sxs-lookup"><span data-stu-id="daf6d-185">You can choose one or more files to upload, and you can upload files of any type.</span></span> <span data-ttu-id="daf6d-186">The **Azure Activity Log** window shows the progress of the upload.</span><span class="sxs-lookup"><span data-stu-id="daf6d-186">The **Azure Activity Log** window shows the progress of the upload.</span></span> <span data-ttu-id="daf6d-187">For more information about how to work with blob data, see [How to use Azure Blob storage in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span><span class="sxs-lookup"><span data-stu-id="daf6d-187">For more information about how to work with blob data, see [How to use Azure Blob storage in .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).</span></span>

### <a name="to-view-logs-transferred-to-blobs"></a><span data-ttu-id="daf6d-188">To view logs transferred to blobs</span><span class="sxs-lookup"><span data-stu-id="daf6d-188">To view logs transferred to blobs</span></span>

<span data-ttu-id="daf6d-189">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that Azure created for these logs.</span><span class="sxs-lookup"><span data-stu-id="daf6d-189">If you are using Azure Diagnostics to log data from your Azure application and you have transferred logs to your storage account, you’ll see containers that Azure created for these logs.</span></span> <span data-ttu-id="daf6d-190">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it's been deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="daf6d-190">Viewing these logs in Server Explorer is an easy way to identify problems with your application, especially if it's been deployed to Azure.</span></span>

<span data-ttu-id="daf6d-191">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span><span class="sxs-lookup"><span data-stu-id="daf6d-191">For more information about Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](https://msdn.microsoft.com/library/azure/gg433048.aspx).</span></span>

### <a name="to-get-the-url-for-a-blob"></a><span data-ttu-id="daf6d-192">To get the URL for a blob</span><span class="sxs-lookup"><span data-stu-id="daf6d-192">To get the URL for a blob</span></span>

<span data-ttu-id="daf6d-193">Open the blob’s shortcut menu and then select **Copy URL**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-193">Open the blob’s shortcut menu and then select **Copy URL**.</span></span>

### <a name="to-edit-a-blob"></a><span data-ttu-id="daf6d-194">To edit a blob</span><span class="sxs-lookup"><span data-stu-id="daf6d-194">To edit a blob</span></span>

<span data-ttu-id="daf6d-195">Select the blob and then select the **Open Blob** button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-195">Select the blob and then select the **Open Blob** button.</span></span>

<span data-ttu-id="daf6d-196">The file is downloaded to a temporary location and opened on the local computer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-196">The file is downloaded to a temporary location and opened on the local computer.</span></span> <span data-ttu-id="daf6d-197">Upload the blob again after you make changes.</span><span class="sxs-lookup"><span data-stu-id="daf6d-197">Upload the blob again after you make changes.</span></span>

## <a name="work-with-queue-resources"></a><span data-ttu-id="daf6d-198">Work with queue resources</span><span class="sxs-lookup"><span data-stu-id="daf6d-198">Work with queue resources</span></span>

<span data-ttu-id="daf6d-199">Storage services queues are hosted in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-199">Storage services queues are hosted in an Azure storage account.</span></span> <span data-ttu-id="daf6d-200">You can use them to allow your cloud service roles to communicate with each other and with other services by a message-passing mechanism.</span><span class="sxs-lookup"><span data-stu-id="daf6d-200">You can use them to allow your cloud service roles to communicate with each other and with other services by a message-passing mechanism.</span></span> <span data-ttu-id="daf6d-201">You can access the queue programmatically through a cloud service and over a web service for external clients.</span><span class="sxs-lookup"><span data-stu-id="daf6d-201">You can access the queue programmatically through a cloud service and over a web service for external clients.</span></span> <span data-ttu-id="daf6d-202">You can also access the queue directly by using Server Explorer in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf6d-202">You can also access the queue directly by using Server Explorer in Visual Studio.</span></span>

<span data-ttu-id="daf6d-203">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span><span class="sxs-lookup"><span data-stu-id="daf6d-203">When you develop a cloud service that uses queues, you might want to use Visual Studio to create queues and work with them interactively while you develop and test your code.</span></span>

<span data-ttu-id="daf6d-204">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span><span class="sxs-lookup"><span data-stu-id="daf6d-204">In Server Explorer, you can view the queues in a storage account, create and delete queues, open a queue to view its messages, and add messages to a queue.</span></span> <span data-ttu-id="daf6d-205">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the upper-left corner:</span><span class="sxs-lookup"><span data-stu-id="daf6d-205">When you open a queue for viewing, you can view the individual messages, and you can perform the following actions on the queue by using the buttons in the upper-left corner:</span></span>

* <span data-ttu-id="daf6d-206">Refresh the view of the queue.</span><span class="sxs-lookup"><span data-stu-id="daf6d-206">Refresh the view of the queue.</span></span>
* <span data-ttu-id="daf6d-207">Add a message to the queue.</span><span class="sxs-lookup"><span data-stu-id="daf6d-207">Add a message to the queue.</span></span>
* <span data-ttu-id="daf6d-208">Dequeue the topmost message.</span><span class="sxs-lookup"><span data-stu-id="daf6d-208">Dequeue the topmost message.</span></span>
* <span data-ttu-id="daf6d-209">Clear the entire queue.</span><span class="sxs-lookup"><span data-stu-id="daf6d-209">Clear the entire queue.</span></span>

<span data-ttu-id="daf6d-210">The following image shows a queue that contains two messages:</span><span class="sxs-lookup"><span data-stu-id="daf6d-210">The following image shows a queue that contains two messages:</span></span>

![Viewing a queue](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

<span data-ttu-id="daf6d-212">For more information about storage services queues, see [Get started with Azure Queue storage using .NET](http://go.microsoft.com/fwlink/?LinkID=264702).</span><span class="sxs-lookup"><span data-stu-id="daf6d-212">For more information about storage services queues, see [Get started with Azure Queue storage using .NET](http://go.microsoft.com/fwlink/?LinkID=264702).</span></span> <span data-ttu-id="daf6d-213">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span><span class="sxs-lookup"><span data-stu-id="daf6d-213">For information about the web service for storage services queues, see [Queue Service Concepts](http://go.microsoft.com/fwlink/?LinkId=264788).</span></span> <span data-ttu-id="daf6d-214">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://docs.microsoft.com/azure/visual-studio/vs-storage-cloud-services-getting-started-queues).</span><span class="sxs-lookup"><span data-stu-id="daf6d-214">For information about how to send messages to a storage services queue by using Visual Studio, see [Sending Messages to a Storage Services Queue](https://docs.microsoft.com/azure/visual-studio/vs-storage-cloud-services-getting-started-queues).</span></span>

> [!NOTE]
> <span data-ttu-id="daf6d-215">Storage services queues are distinct from Azure Service Bus queues.</span><span class="sxs-lookup"><span data-stu-id="daf6d-215">Storage services queues are distinct from Azure Service Bus queues.</span></span> <span data-ttu-id="daf6d-216">For more information about Service Bus queues, see [Service Bus queues, topics, and subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-queues-topics-subscriptions).</span><span class="sxs-lookup"><span data-stu-id="daf6d-216">For more information about Service Bus queues, see [Service Bus queues, topics, and subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-queues-topics-subscriptions).</span></span>

## <a name="work-with-table-resources"></a><span data-ttu-id="daf6d-217">Work with table resources</span><span class="sxs-lookup"><span data-stu-id="daf6d-217">Work with table resources</span></span>

<span data-ttu-id="daf6d-218">Azure Table storage stores large amounts of structured data.</span><span class="sxs-lookup"><span data-stu-id="daf6d-218">Azure Table storage stores large amounts of structured data.</span></span> <span data-ttu-id="daf6d-219">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="daf6d-219">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="daf6d-220">Azure tables are ideal for storing structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="daf6d-220">Azure tables are ideal for storing structured, non-relational data.</span></span>

### <a name="to-create-a-table"></a><span data-ttu-id="daf6d-221">To create a table</span><span class="sxs-lookup"><span data-stu-id="daf6d-221">To create a table</span></span>

1. <span data-ttu-id="daf6d-222">In Cloud Explorer, select the **Tables** node of the storage account, and then select **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-222">In Cloud Explorer, select the **Tables** node of the storage account, and then select **Create Table**.</span></span>
1. <span data-ttu-id="daf6d-223">In the **Create Table** dialog box, enter a name for the table.</span><span class="sxs-lookup"><span data-stu-id="daf6d-223">In the **Create Table** dialog box, enter a name for the table.</span></span>

### <a name="to-view-table-data"></a><span data-ttu-id="daf6d-224">To view table data</span><span class="sxs-lookup"><span data-stu-id="daf6d-224">To view table data</span></span>

1. <span data-ttu-id="daf6d-225">In Cloud Explorer, open the **Azure** node, and then open the **Storage** node.</span><span class="sxs-lookup"><span data-stu-id="daf6d-225">In Cloud Explorer, open the **Azure** node, and then open the **Storage** node.</span></span>
1. <span data-ttu-id="daf6d-226">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-226">Open the storage account node that you are interested in, and then open the **Tables** node to see a list of tables for the storage account.</span></span>
1. <span data-ttu-id="daf6d-227">Open the shortcut menu for a table, and then select **View Table**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-227">Open the shortcut menu for a table, and then select **View Table**.</span></span>

    ![An Azure table in Solution Explorer](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

<span data-ttu-id="daf6d-229">The table is organized by entities (shown in rows) and properties (shown in columns).</span><span class="sxs-lookup"><span data-stu-id="daf6d-229">The table is organized by entities (shown in rows) and properties (shown in columns).</span></span> <span data-ttu-id="daf6d-230">For example, the next illustration shows entities listed in Table Designer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-230">For example, the next illustration shows entities listed in Table Designer.</span></span>

### <a name="to-edit-table-data"></a><span data-ttu-id="daf6d-231">To edit table data</span><span class="sxs-lookup"><span data-stu-id="daf6d-231">To edit table data</span></span>

<span data-ttu-id="daf6d-232">In Table Designer, open the shortcut menu for an entity (a single row) or a property (a single cell), and then select **Edit**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-232">In Table Designer, open the shortcut menu for an entity (a single row) or a property (a single cell), and then select **Edit**.</span></span>

    ![Add or edit a table entity](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)

<span data-ttu-id="daf6d-233">Entities in a single table aren’t required to have the same set of properties (columns).</span><span class="sxs-lookup"><span data-stu-id="daf6d-233">Entities in a single table aren’t required to have the same set of properties (columns).</span></span> <span data-ttu-id="daf6d-234">Keep in mind the following restrictions on viewing and editing table data:</span><span class="sxs-lookup"><span data-stu-id="daf6d-234">Keep in mind the following restrictions on viewing and editing table data:</span></span>

* <span data-ttu-id="daf6d-235">You can’t view or edit binary data (`type byte[]`), but you can store it in a table.</span><span class="sxs-lookup"><span data-stu-id="daf6d-235">You can’t view or edit binary data (`type byte[]`), but you can store it in a table.</span></span>
* <span data-ttu-id="daf6d-236">You can’t edit the **PartitionKey** or **RowKey** values, because Table storage in Azure doesn't support that operation.</span><span class="sxs-lookup"><span data-stu-id="daf6d-236">You can’t edit the **PartitionKey** or **RowKey** values, because Table storage in Azure doesn't support that operation.</span></span>
* <span data-ttu-id="daf6d-237">You can’t create a property called **Timestamp**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-237">You can’t create a property called **Timestamp**.</span></span> <span data-ttu-id="daf6d-238">Azure storage services use a property with that name.</span><span class="sxs-lookup"><span data-stu-id="daf6d-238">Azure storage services use a property with that name.</span></span>
* <span data-ttu-id="daf6d-239">If you enter a **DateTime** value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for US English).</span><span class="sxs-lookup"><span data-stu-id="daf6d-239">If you enter a **DateTime** value, you must follow a format that's appropriate to the region and language settings of your computer (for example, MM/DD/YYYY HH:MM:SS [AM|PM] for US English).</span></span>

### <a name="to-add-entities"></a><span data-ttu-id="daf6d-240">To add entities</span><span class="sxs-lookup"><span data-stu-id="daf6d-240">To add entities</span></span>

1. <span data-ttu-id="daf6d-241">In Table Designer, select the **Add Entity** button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-241">In Table Designer, select the **Add Entity** button.</span></span>

    ![Add Entity button](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)

1. <span data-ttu-id="daf6d-243">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span><span class="sxs-lookup"><span data-stu-id="daf6d-243">In the **Add Entity** dialog box, enter the values of the **PartitionKey** and **RowKey** properties.</span></span>

    ![Add Entity dialog box](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)

    <span data-ttu-id="daf6d-245">Enter the values carefully.</span><span class="sxs-lookup"><span data-stu-id="daf6d-245">Enter the values carefully.</span></span> <span data-ttu-id="daf6d-246">You can't change them after you close the dialog box unless you delete the entity and add it again.</span><span class="sxs-lookup"><span data-stu-id="daf6d-246">You can't change them after you close the dialog box unless you delete the entity and add it again.</span></span>

### <a name="to-filter-entities"></a><span data-ttu-id="daf6d-247">To filter entities</span><span class="sxs-lookup"><span data-stu-id="daf6d-247">To filter entities</span></span>

<span data-ttu-id="daf6d-248">You can customize the set of entities that appear in a table if you use the query builder.</span><span class="sxs-lookup"><span data-stu-id="daf6d-248">You can customize the set of entities that appear in a table if you use the query builder.</span></span>

1. <span data-ttu-id="daf6d-249">To open the query builder, open a table for viewing.</span><span class="sxs-lookup"><span data-stu-id="daf6d-249">To open the query builder, open a table for viewing.</span></span>
1. <span data-ttu-id="daf6d-250">Select the **Query Builder** button on the table view’s toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-250">Select the **Query Builder** button on the table view’s toolbar.</span></span>

    <span data-ttu-id="daf6d-251">The **Query Builder** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="daf6d-251">The **Query Builder** dialog box appears.</span></span> <span data-ttu-id="daf6d-252">The following illustration shows a query that's being built in the query builder.</span><span class="sxs-lookup"><span data-stu-id="daf6d-252">The following illustration shows a query that's being built in the query builder.</span></span>

    ![Query builder](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
1. <span data-ttu-id="daf6d-254">When you’re done building the query, close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="daf6d-254">When you’re done building the query, close the dialog box.</span></span> <span data-ttu-id="daf6d-255">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span><span class="sxs-lookup"><span data-stu-id="daf6d-255">The resulting text form of the query appears in a text box as a WCF Data Services filter.</span></span>
1. <span data-ttu-id="daf6d-256">To run the query, select the green triangle icon.</span><span class="sxs-lookup"><span data-stu-id="daf6d-256">To run the query, select the green triangle icon.</span></span>

<span data-ttu-id="daf6d-257">You can also filter entity data that appears in Table Designer if you enter a WCF Data Services filter string directly in the filter text box.</span><span class="sxs-lookup"><span data-stu-id="daf6d-257">You can also filter entity data that appears in Table Designer if you enter a WCF Data Services filter string directly in the filter text box.</span></span> <span data-ttu-id="daf6d-258">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="daf6d-258">This kind of string is similar to a SQL WHERE clause but is sent to the server as an HTTP request.</span></span> <span data-ttu-id="daf6d-259">For information about how to construct filter strings, see [Constructing filter strings for the table designer](https://docs.microsoft.com/azure/vs-azure-tools-table-designer-construct-filter-strings).</span><span class="sxs-lookup"><span data-stu-id="daf6d-259">For information about how to construct filter strings, see [Constructing filter strings for the table designer](https://docs.microsoft.com/azure/vs-azure-tools-table-designer-construct-filter-strings).</span></span>

<span data-ttu-id="daf6d-260">The following illustration shows an example of a valid filter string:</span><span class="sxs-lookup"><span data-stu-id="daf6d-260">The following illustration shows an example of a valid filter string:</span></span>

![Filter string](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

## <a name="refresh-storage-data"></a><span data-ttu-id="daf6d-262">Refresh storage data</span><span class="sxs-lookup"><span data-stu-id="daf6d-262">Refresh storage data</span></span>

<span data-ttu-id="daf6d-263">When Server Explorer connects to or gets data from a storage account, the operation might take up to a minute to finish.</span><span class="sxs-lookup"><span data-stu-id="daf6d-263">When Server Explorer connects to or gets data from a storage account, the operation might take up to a minute to finish.</span></span> <span data-ttu-id="daf6d-264">If Server Explorer can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="daf6d-264">If Server Explorer can’t connect, the operation might time out. While data is retrieved, you can continue to work in other parts of Visual Studio.</span></span> <span data-ttu-id="daf6d-265">To cancel the operation if it’s taking too long, select the **Stop Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-265">To cancel the operation if it’s taking too long, select the **Stop Refresh** button on the Server Explorer toolbar.</span></span>

### <a name="to-refresh-blob-container-data"></a><span data-ttu-id="daf6d-266">To refresh blob container data</span><span class="sxs-lookup"><span data-stu-id="daf6d-266">To refresh blob container data</span></span>

* <span data-ttu-id="daf6d-267">Select the **Blobs** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-267">Select the **Blobs** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span></span>
* <span data-ttu-id="daf6d-268">To refresh the list of blobs that is displayed, select the **Execute** button.</span><span class="sxs-lookup"><span data-stu-id="daf6d-268">To refresh the list of blobs that is displayed, select the **Execute** button.</span></span>

### <a name="to-refresh-table-data"></a><span data-ttu-id="daf6d-269">To refresh table data</span><span class="sxs-lookup"><span data-stu-id="daf6d-269">To refresh table data</span></span>

* <span data-ttu-id="daf6d-270">Select the **Tables** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-270">Select the **Tables** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span></span>
* <span data-ttu-id="daf6d-271">To refresh the list of entities that is displayed in Table Designer, select the **Execute** button in Table Designer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-271">To refresh the list of entities that is displayed in Table Designer, select the **Execute** button in Table Designer.</span></span>

### <a name="to-refresh-queue-data"></a><span data-ttu-id="daf6d-272">To refresh queue data</span><span class="sxs-lookup"><span data-stu-id="daf6d-272">To refresh queue data</span></span>

<span data-ttu-id="daf6d-273">Select the **Queues** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-273">Select the **Queues** node beneath **Storage**, and then select the **Refresh** button on the Server Explorer toolbar.</span></span>

### <a name="to-refresh-all-items-in-a-storage-account"></a><span data-ttu-id="daf6d-274">To refresh all items in a storage account</span><span class="sxs-lookup"><span data-stu-id="daf6d-274">To refresh all items in a storage account</span></span>

<span data-ttu-id="daf6d-275">Choose the account name, and then select the **Refresh** button on the Server Explorer toolbar.</span><span class="sxs-lookup"><span data-stu-id="daf6d-275">Choose the account name, and then select the **Refresh** button on the Server Explorer toolbar.</span></span>

## <a name="add-storage-accounts-by-using-server-explorer"></a><span data-ttu-id="daf6d-276">Add storage accounts by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="daf6d-276">Add storage accounts by using Server Explorer</span></span>

<span data-ttu-id="daf6d-277">There are two ways to add storage accounts by using Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-277">There are two ways to add storage accounts by using Server Explorer.</span></span> <span data-ttu-id="daf6d-278">You can create a storage account in your Azure subscription, or you can attach an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-278">You can create a storage account in your Azure subscription, or you can attach an existing storage account.</span></span>

### <a name="to-create-a-storage-account-by-using-server-explorer"></a><span data-ttu-id="daf6d-279">To create a storage account by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="daf6d-279">To create a storage account by using Server Explorer</span></span>

1. <span data-ttu-id="daf6d-280">In Server Explorer, open the shortcut menu for the **Storage** node, and then select **Create Storage Account**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-280">In Server Explorer, open the shortcut menu for the **Storage** node, and then select **Create Storage Account**.</span></span>

1. <span data-ttu-id="daf6d-281">In the **Create Storage Account** dialog box, select or enter the following information:</span><span class="sxs-lookup"><span data-stu-id="daf6d-281">In the **Create Storage Account** dialog box, select or enter the following information:</span></span>

   * <span data-ttu-id="daf6d-282">The Azure subscription to which you want to add the storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-282">The Azure subscription to which you want to add the storage account.</span></span>
   * <span data-ttu-id="daf6d-283">The name that you want to use for the new storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-283">The name that you want to use for the new storage account.</span></span>
   * <span data-ttu-id="daf6d-284">The region or affinity group (such as West US or East Asia).</span><span class="sxs-lookup"><span data-stu-id="daf6d-284">The region or affinity group (such as West US or East Asia).</span></span>
   * <span data-ttu-id="daf6d-285">The type of replication you want to use for the storage account, such as locally redundant.</span><span class="sxs-lookup"><span data-stu-id="daf6d-285">The type of replication you want to use for the storage account, such as locally redundant.</span></span>

   ![Create an Azure storage account](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)

1. <span data-ttu-id="daf6d-287">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-287">Select **Create**.</span></span>

<span data-ttu-id="daf6d-288">The new storage account appears in the **Storage** list in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-288">The new storage account appears in the **Storage** list in Solution Explorer.</span></span>

### <a name="to-attach-an-existing-storage-account-by-using-server-explorer"></a><span data-ttu-id="daf6d-289">To attach an existing storage account by using Server Explorer</span><span class="sxs-lookup"><span data-stu-id="daf6d-289">To attach an existing storage account by using Server Explorer</span></span>

1. <span data-ttu-id="daf6d-290">In Server Explorer, open the shortcut menu for the Azure **Storage** node, and then select **Attach External Storage**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-290">In Server Explorer, open the shortcut menu for the Azure **Storage** node, and then select **Attach External Storage**.</span></span>

    ![Adding an existing storage account](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
1. <span data-ttu-id="daf6d-292">In the **Create Storage Account** dialog box, select or enter the following information:</span><span class="sxs-lookup"><span data-stu-id="daf6d-292">In the **Create Storage Account** dialog box, select or enter the following information:</span></span>

   * <span data-ttu-id="daf6d-293">The name of the existing storage account that you want to attach.</span><span class="sxs-lookup"><span data-stu-id="daf6d-293">The name of the existing storage account that you want to attach.</span></span>
   * <span data-ttu-id="daf6d-294">The key for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-294">The key for the selected storage account.</span></span> <span data-ttu-id="daf6d-295">This value is typically provided for you when you select a storage account.</span><span class="sxs-lookup"><span data-stu-id="daf6d-295">This value is typically provided for you when you select a storage account.</span></span> <span data-ttu-id="daf6d-296">If you want Visual Studio to remember the storage account key, select the **Remember account key** check box.</span><span class="sxs-lookup"><span data-stu-id="daf6d-296">If you want Visual Studio to remember the storage account key, select the **Remember account key** check box.</span></span>
   * <span data-ttu-id="daf6d-297">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span><span class="sxs-lookup"><span data-stu-id="daf6d-297">The protocol to use to connect to the storage account, such as HTTP, HTTPS, or a custom endpoint.</span></span> <span data-ttu-id="daf6d-298">For more information about custom endpoints, see [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx).</span><span class="sxs-lookup"><span data-stu-id="daf6d-298">For more information about custom endpoints, see [How to Configure Connection Strings](https://msdn.microsoft.com/library/azure/ee758697.aspx).</span></span>

### <a name="to-view-the-secondary-endpoints"></a><span data-ttu-id="daf6d-299">To view the secondary endpoints</span><span class="sxs-lookup"><span data-stu-id="daf6d-299">To view the secondary endpoints</span></span>

<span data-ttu-id="daf6d-300">If you created a storage account by using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints by opening the shortcut menu for the account name, and then select **Properties**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-300">If you created a storage account by using the **Read-Access Geo Redundant** replication option, you can view its secondary endpoints by opening the shortcut menu for the account name, and then select **Properties**.</span></span>

![Storage secondary endpoints](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="to-remove-a-storage-account-from-server-explorer"></a><span data-ttu-id="daf6d-302">To remove a storage account from Server Explorer</span><span class="sxs-lookup"><span data-stu-id="daf6d-302">To remove a storage account from Server Explorer</span></span>

<span data-ttu-id="daf6d-303">In Server Explorer, open the shortcut menu for the account name, and then select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="daf6d-303">In Server Explorer, open the shortcut menu for the account name, and then select **Delete**.</span></span> 

<span data-ttu-id="daf6d-304">If you delete a storage account, any saved key information for that account is also removed.</span><span class="sxs-lookup"><span data-stu-id="daf6d-304">If you delete a storage account, any saved key information for that account is also removed.</span></span>

<span data-ttu-id="daf6d-305">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains.</span><span class="sxs-lookup"><span data-stu-id="daf6d-305">If you delete a storage account from Server Explorer, it doesn’t affect your storage account or any data that it contains.</span></span> <span data-ttu-id="daf6d-306">It simply removes the reference from Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="daf6d-306">It simply removes the reference from Server Explorer.</span></span> <span data-ttu-id="daf6d-307">To permanently delete a storage account, use the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="daf6d-307">To permanently delete a storage account, use the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="daf6d-308">Next steps</span><span class="sxs-lookup"><span data-stu-id="daf6d-308">Next steps</span></span>

<span data-ttu-id="daf6d-309">To learn more about how to use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span><span class="sxs-lookup"><span data-stu-id="daf6d-309">To learn more about how to use Azure storage services, see [Accessing the Azure Storage Services](https://msdn.microsoft.com/library/azure/ee405490.aspx).</span></span>
