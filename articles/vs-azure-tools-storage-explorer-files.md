---
title: Using Storage Explorer (Preview) with Azure File storage | Microsoft Docs
description: Learn how learn how to use Storage Explorer (Preview) to work with file shares and files.
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: ''
ms.assetid: ''
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: fb4025d682fe30944a0d88f163ec1b8eb6339704
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564598"
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a><span data-ttu-id="8ad35-103">Using Storage Explorer (Preview) with Azure File storage</span><span class="sxs-lookup"><span data-stu-id="8ad35-103">Using Storage Explorer (Preview) with Azure File storage</span></span>

<span data-ttu-id="8ad35-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span><span class="sxs-lookup"><span data-stu-id="8ad35-104">Azure File storage is a service that offers file shares in the cloud using the standard Server Message Block (SMB) Protocol.</span></span> <span data-ttu-id="8ad35-105">Both SMB 2.1 and SMB 3.0 are supported.</span><span class="sxs-lookup"><span data-stu-id="8ad35-105">Both SMB 2.1 and SMB 3.0 are supported.</span></span> <span data-ttu-id="8ad35-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span><span class="sxs-lookup"><span data-stu-id="8ad35-106">With Azure File storage, you can migrate legacy applications that rely on file shares to Azure quickly and without costly rewrites.</span></span> <span data-ttu-id="8ad35-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span><span class="sxs-lookup"><span data-stu-id="8ad35-107">You can use File storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="8ad35-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span><span class="sxs-lookup"><span data-stu-id="8ad35-108">In this article, you'll learn how to use Storage Explorer (Preview) to work with file shares and files.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8ad35-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8ad35-109">Prerequisites</span></span>

<span data-ttu-id="8ad35-110">To complete the steps in this article, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="8ad35-110">To complete the steps in this article, you'll need the following:</span></span>

- [<span data-ttu-id="8ad35-111">Download and install Storage Explorer (preview)</span><span class="sxs-lookup"><span data-stu-id="8ad35-111">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com/)

- [<span data-ttu-id="8ad35-112">Connect to a Azure storage account or service</span><span class="sxs-lookup"><span data-stu-id="8ad35-112">Connect to a Azure storage account or service</span></span>](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a><span data-ttu-id="8ad35-113">Create a File Share</span><span class="sxs-lookup"><span data-stu-id="8ad35-113">Create a File Share</span></span>

<span data-ttu-id="8ad35-114">All files must reside in a file share, which is simply a logical grouping of files.</span><span class="sxs-lookup"><span data-stu-id="8ad35-114">All files must reside in a file share, which is simply a logical grouping of files.</span></span> <span data-ttu-id="8ad35-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span><span class="sxs-lookup"><span data-stu-id="8ad35-115">An account can contain an unlimited number of file shares, and each share can store an unlimited number of files.</span></span>

<span data-ttu-id="8ad35-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-116">The following steps illustrate how to create a file share within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="8ad35-117">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-117">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-118">In the left pane, expand the storage account within which you wish to create the File Share</span><span class="sxs-lookup"><span data-stu-id="8ad35-118">In the left pane, expand the storage account within which you wish to create the File Share</span></span>

3. <span data-ttu-id="8ad35-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-119">Right-click **File Shares**, and - from the context menu - select **Create File Share**.</span></span>

    ![Create File Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image1.png)

4. <span data-ttu-id="8ad35-121">A text box will appear below the **File Shares** folder.</span><span class="sxs-lookup"><span data-stu-id="8ad35-121">A text box will appear below the **File Shares** folder.</span></span> <span data-ttu-id="8ad35-122">Enter the name for your file share.</span><span class="sxs-lookup"><span data-stu-id="8ad35-122">Enter the name for your file share.</span></span> <span data-ttu-id="8ad35-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span><span class="sxs-lookup"><span data-stu-id="8ad35-123">See the [Share naming rules](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container) section for a list of rules and restrictions on naming file shares.</span></span>

    ![Naming the share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image2.png)

5. <span data-ttu-id="8ad35-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span><span class="sxs-lookup"><span data-stu-id="8ad35-125">Press **Enter** when done to create the file share, or **Esc** to cancel.</span></span> <span data-ttu-id="8ad35-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="8ad35-126">Once the file share has been successfully created, it will be displayed under the **File Shares** folder for the selected storage account.</span></span>

    ![The new share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a><span data-ttu-id="8ad35-128">View a file share's contents</span><span class="sxs-lookup"><span data-stu-id="8ad35-128">View a file share's contents</span></span>

<span data-ttu-id="8ad35-129">File shares contain files and folders (that can also contain files).</span><span class="sxs-lookup"><span data-stu-id="8ad35-129">File shares contain files and folders (that can also contain files).</span></span>

<span data-ttu-id="8ad35-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span><span class="sxs-lookup"><span data-stu-id="8ad35-130">The following steps illustrate how to view the contents of a file share within Storage Explorer (Preview):+</span></span>

1. <span data-ttu-id="8ad35-131">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-131">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-132">In the left pane, expand the storage account containing the file share you wish to view.</span><span class="sxs-lookup"><span data-stu-id="8ad35-132">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="8ad35-133">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-133">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="8ad35-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-134">Right-click the file share you wish to view, and - from the context menu - select **Open**.</span></span> <span data-ttu-id="8ad35-135">You can also double-click the file share you wish to view.</span><span class="sxs-lookup"><span data-stu-id="8ad35-135">You can also double-click the file share you wish to view.</span></span>

    ![Open share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image4.png)

5. <span data-ttu-id="8ad35-137">The main pane will display the file share's contents.</span><span class="sxs-lookup"><span data-stu-id="8ad35-137">The main pane will display the file share's contents.</span></span>
    
    ![The share's contents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a><span data-ttu-id="8ad35-139">Delete a file share</span><span class="sxs-lookup"><span data-stu-id="8ad35-139">Delete a file share</span></span>

<span data-ttu-id="8ad35-140">File shares can be easily created and deleted as needed.</span><span class="sxs-lookup"><span data-stu-id="8ad35-140">File shares can be easily created and deleted as needed.</span></span> <span data-ttu-id="8ad35-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="8ad35-141">(To see how to delete individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="8ad35-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span><span class="sxs-lookup"><span data-stu-id="8ad35-142">The following steps illustrate how to delete a file share within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="8ad35-143">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-143">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-144">In the left pane, expand the storage account containing the file share you wish to view.</span><span class="sxs-lookup"><span data-stu-id="8ad35-144">In the left pane, expand the storage account containing the file share you wish to view.</span></span>

3. <span data-ttu-id="8ad35-145">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-145">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="8ad35-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-146">Right-click the file share you wish to delete, and - from the context menu - select **Delete**.</span></span> <span data-ttu-id="8ad35-147">You can also press **Delete** to delete the currently selected file share.</span><span class="sxs-lookup"><span data-stu-id="8ad35-147">You can also press **Delete** to delete the currently selected file share.</span></span>

    ![Delete](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image6.png)

5. <span data-ttu-id="8ad35-149">Select **Yes** to the confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="8ad35-149">Select **Yes** to the confirmation dialog.</span></span>
    
    ![Confirmation dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a><span data-ttu-id="8ad35-151">Copy a file share</span><span class="sxs-lookup"><span data-stu-id="8ad35-151">Copy a file share</span></span>

<span data-ttu-id="8ad35-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span><span class="sxs-lookup"><span data-stu-id="8ad35-152">Storage Explorer (Preview) enables you to copy a file share to the clipboard, and then paste that file share into another storage account.</span></span> <span data-ttu-id="8ad35-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="8ad35-153">(To see how to copy individual files, refer to the section, [Managing files in a file share](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="8ad35-154">The following steps illustrate how to copy a file share from one storage account to another.</span><span class="sxs-lookup"><span data-stu-id="8ad35-154">The following steps illustrate how to copy a file share from one storage account to another.</span></span>

1. <span data-ttu-id="8ad35-155">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-155">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-156">In the left pane, expand the storage account containing the file share you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="8ad35-156">In the left pane, expand the storage account containing the file share you wish to copy.</span></span>

3. <span data-ttu-id="8ad35-157">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-157">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="8ad35-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-158">Right-click the file share you wish to copy, and - from the context menu - select **Copy File Share**.</span></span>

    ![Copy File Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image8.png)

5. <span data-ttu-id="8ad35-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-160">Right-click the desired "target" storage account into which you want to paste the file share, and - from the context menu - select **Paste File Share**.</span></span>

    ![Paste File Share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-the-sas-for-a-file-share"></a><span data-ttu-id="8ad35-162">Get the SAS for a file share</span><span class="sxs-lookup"><span data-stu-id="8ad35-162">Get the SAS for a file share</span></span>

<span data-ttu-id="8ad35-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="8ad35-163">A [shared access signature (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1) provides delegated access to resources in your storage account.</span></span> <span data-ttu-id="8ad35-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span><span class="sxs-lookup"><span data-stu-id="8ad35-164">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="8ad35-165">The following steps illustrate how to create a SAS for a file share:+</span><span class="sxs-lookup"><span data-stu-id="8ad35-165">The following steps illustrate how to create a SAS for a file share:+</span></span>

1. <span data-ttu-id="8ad35-166">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-166">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span><span class="sxs-lookup"><span data-stu-id="8ad35-167">In the left pane, expand the storage account containing the file share for which you wish to get a SAS.</span></span>

3. <span data-ttu-id="8ad35-168">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-168">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="8ad35-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-169">Right-click the desired file share, and - from the context menu - select **Get Shared Access Signature**.</span></span>

    ![Get Shared Access Signature](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image10.png)

5. <span data-ttu-id="8ad35-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span><span class="sxs-lookup"><span data-stu-id="8ad35-171">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

    ![SAS dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image11.png)

6. <span data-ttu-id="8ad35-173">When you're finished specifying the SAS options, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-173">When you're finished specifying the SAS options, select **Create**.</span></span>

7. <span data-ttu-id="8ad35-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span><span class="sxs-lookup"><span data-stu-id="8ad35-174">A second **Shared Access Signature** dialog will then display that lists the file share along with the URL and QueryStrings you can use to access the storage resource.</span></span> <span data-ttu-id="8ad35-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="8ad35-175">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>
    
    ![Second SAS dialog](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image12.png)

8. <span data-ttu-id="8ad35-177">When done, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-177">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-file-share"></a><span data-ttu-id="8ad35-178">Manage Access Policies for a file share</span><span class="sxs-lookup"><span data-stu-id="8ad35-178">Manage Access Policies for a file share</span></span>

<span data-ttu-id="8ad35-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span><span class="sxs-lookup"><span data-stu-id="8ad35-179">The following steps illustrate how to manage (add and remove) access policies for a file share:+ .</span></span> <span data-ttu-id="8ad35-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span><span class="sxs-lookup"><span data-stu-id="8ad35-180">The Access Policies is used for creating SAS URLs through which people can use to access the Storage File resource during a defined period of time.</span></span>

1. <span data-ttu-id="8ad35-181">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-181">Open Storage Explorer (Preview).</span></span>

2. <span data-ttu-id="8ad35-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="8ad35-182">In the left pane, expand the storage account containing the file share whose access policies you wish to manage.</span></span>

3. <span data-ttu-id="8ad35-183">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-183">Expand the storage account's **File Shares**.</span></span>

4. <span data-ttu-id="8ad35-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-184">Select the desired file share, and - from the context menu - select **Manage Access Policies**.</span></span>

    ![Manage access policies context menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image13.png)

5. <span data-ttu-id="8ad35-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span><span class="sxs-lookup"><span data-stu-id="8ad35-186">The **Access Policies** dialog will list any access policies already created for the selected file share.</span></span>
    
    ![Access Policies](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image14.png)

6. <span data-ttu-id="8ad35-188">Follow these steps depending on the access policy management task:</span><span class="sxs-lookup"><span data-stu-id="8ad35-188">Follow these steps depending on the access policy management task:</span></span>
    
    - <span data-ttu-id="8ad35-189">**Add a new access policy** - Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-189">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="8ad35-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span><span class="sxs-lookup"><span data-stu-id="8ad35-190">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>

    - <span data-ttu-id="8ad35-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-191">**Edit an access policy** - Make any desired edits, and select **Save**.</span></span>

    - <span data-ttu-id="8ad35-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span><span class="sxs-lookup"><span data-stu-id="8ad35-192">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

7. <span data-ttu-id="8ad35-193">Create a new SAS URL using the Access Policy you created earlier:</span><span class="sxs-lookup"><span data-stu-id="8ad35-193">Create a new SAS URL using the Access Policy you created earlier:</span></span>
    
    ![Get SAS](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS name and properties](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a><span data-ttu-id="8ad35-196">Managing files in a file share</span><span class="sxs-lookup"><span data-stu-id="8ad35-196">Managing files in a file share</span></span>

<span data-ttu-id="8ad35-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span><span class="sxs-lookup"><span data-stu-id="8ad35-197">Once you've created a file share, you can upload a file to that file share, download a file to your local computer, open a file on your local computer, and much more.</span></span>

<span data-ttu-id="8ad35-198">The following steps illustrate how to manage the files (and folders) within a file share.</span><span class="sxs-lookup"><span data-stu-id="8ad35-198">The following steps illustrate how to manage the files (and folders) within a file share.</span></span>

1.  <span data-ttu-id="8ad35-199">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="8ad35-199">Open Storage Explorer (Preview).</span></span>

2.  <span data-ttu-id="8ad35-200">In the left pane, expand the storage account containing the file share you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="8ad35-200">In the left pane, expand the storage account containing the file share you wish to manage.</span></span>

3.  <span data-ttu-id="8ad35-201">Expand the storage account's **File Shares**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-201">Expand the storage account's **File Shares**.</span></span>

4.  <span data-ttu-id="8ad35-202">Double-click the file share you wish to view.</span><span class="sxs-lookup"><span data-stu-id="8ad35-202">Double-click the file share you wish to view.</span></span>

5.  <span data-ttu-id="8ad35-203">The main pane will display the file share's contents.</span><span class="sxs-lookup"><span data-stu-id="8ad35-203">The main pane will display the file share's contents.</span></span>

    ![The share's contents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image17.png)

6.  <span data-ttu-id="8ad35-205">The main pane will display the file share's contents.</span><span class="sxs-lookup"><span data-stu-id="8ad35-205">The main pane will display the file share's contents.</span></span>

7.  <span data-ttu-id="8ad35-206">Follow these steps depending on the task you wish to perform:</span><span class="sxs-lookup"><span data-stu-id="8ad35-206">Follow these steps depending on the task you wish to perform:</span></span>

    - <span data-ttu-id="8ad35-207">**Upload files to a file share**</span><span class="sxs-lookup"><span data-stu-id="8ad35-207">**Upload files to a file share**</span></span>

        <span data-ttu-id="8ad35-208">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-208">a.</span></span>  <span data-ttu-id="8ad35-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="8ad35-209">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Upload files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image18.png)
        
        <span data-ttu-id="8ad35-211">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-211">b.</span></span> <span data-ttu-id="8ad35-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span><span class="sxs-lookup"><span data-stu-id="8ad35-212">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Adding files](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image19.png)

        <span data-ttu-id="8ad35-214">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-214">c.</span></span> <span data-ttu-id="8ad35-215">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-215">Select **Upload**.</span></span>

    - <span data-ttu-id="8ad35-216">**Upload a folder to a file share**</span><span class="sxs-lookup"><span data-stu-id="8ad35-216">**Upload a folder to a file share**</span></span>
        
        <span data-ttu-id="8ad35-217">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-217">a.</span></span> <span data-ttu-id="8ad35-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="8ad35-218">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Upload folder menu](https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-files/image20.png)

        <span data-ttu-id="8ad35-220">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-220">b.</span></span> <span data-ttu-id="8ad35-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span><span class="sxs-lookup"><span data-stu-id="8ad35-221">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        <span data-ttu-id="8ad35-222">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-222">c.</span></span> <span data-ttu-id="8ad35-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span><span class="sxs-lookup"><span data-stu-id="8ad35-223">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="8ad35-224">If the target folder doesn’t exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="8ad35-224">If the target folder doesn’t exist, it will be created.</span></span>

        <span data-ttu-id="8ad35-225">d.</span><span class="sxs-lookup"><span data-stu-id="8ad35-225">d.</span></span> <span data-ttu-id="8ad35-226">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-226">Select **Upload**.</span></span>

    - <span data-ttu-id="8ad35-227">**Download a file to your local computer**</span><span class="sxs-lookup"><span data-stu-id="8ad35-227">**Download a file to your local computer**</span></span>
        
        <span data-ttu-id="8ad35-228">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-228">a.</span></span> <span data-ttu-id="8ad35-229">Select the file you wish to download.</span><span class="sxs-lookup"><span data-stu-id="8ad35-229">Select the file you wish to download.</span></span>
        
        <span data-ttu-id="8ad35-230">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-230">b.</span></span> <span data-ttu-id="8ad35-231">On the main pane's toolbar, select **Download**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-231">On the main pane's toolbar, select **Download**.</span></span>
        
        <span data-ttu-id="8ad35-232">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-232">c.</span></span> <span data-ttu-id="8ad35-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span><span class="sxs-lookup"><span data-stu-id="8ad35-233">In the **Specify where to save the downloaded file** dialog, specify the location where you want the file downloaded, and the name you wish to give it.</span></span>

        <span data-ttu-id="8ad35-234">d.</span><span class="sxs-lookup"><span data-stu-id="8ad35-234">d.</span></span> <span data-ttu-id="8ad35-235">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-235">Select **Save**.</span></span>

    - <span data-ttu-id="8ad35-236">**Open a file on your local computer**</span><span class="sxs-lookup"><span data-stu-id="8ad35-236">**Open a file on your local computer**</span></span>
        
        <span data-ttu-id="8ad35-237">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-237">a.</span></span>  <span data-ttu-id="8ad35-238">Select the file you wish to open.</span><span class="sxs-lookup"><span data-stu-id="8ad35-238">Select the file you wish to open.</span></span>
        
        <span data-ttu-id="8ad35-239">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-239">b.</span></span>  <span data-ttu-id="8ad35-240">On the main pane's toolbar, select **Open**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-240">On the main pane's toolbar, select **Open**.</span></span>
        
        <span data-ttu-id="8ad35-241">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-241">c.</span></span>  <span data-ttu-id="8ad35-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span><span class="sxs-lookup"><span data-stu-id="8ad35-242">The file will be downloaded and opened using the application associated with the file's underlying file type.</span></span>

    - <span data-ttu-id="8ad35-243">**Copy a file to the clipboard**</span><span class="sxs-lookup"><span data-stu-id="8ad35-243">**Copy a file to the clipboard**</span></span>

        <span data-ttu-id="8ad35-244">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-244">a.</span></span> <span data-ttu-id="8ad35-245">Select the file you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="8ad35-245">Select the file you wish to copy.</span></span>

        <span data-ttu-id="8ad35-246">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-246">b.</span></span> <span data-ttu-id="8ad35-247">On the main pane's toolbar, select **Copy**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-247">On the main pane's toolbar, select **Copy**.</span></span>

        <span data-ttu-id="8ad35-248">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-248">c.</span></span> <span data-ttu-id="8ad35-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span><span class="sxs-lookup"><span data-stu-id="8ad35-249">In the left pane, navigate to another file share, and double-click it to view it in the main pane.</span></span>

        <span data-ttu-id="8ad35-250">d.</span><span class="sxs-lookup"><span data-stu-id="8ad35-250">d.</span></span> <span data-ttu-id="8ad35-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span><span class="sxs-lookup"><span data-stu-id="8ad35-251">On the main pane's toolbar, select **Paste** to create a copy of the file.</span></span>

    - <span data-ttu-id="8ad35-252">**Delete a file**</span><span class="sxs-lookup"><span data-stu-id="8ad35-252">**Delete a file**</span></span>

        <span data-ttu-id="8ad35-253">a.</span><span class="sxs-lookup"><span data-stu-id="8ad35-253">a.</span></span> <span data-ttu-id="8ad35-254">Select the file you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="8ad35-254">Select the file you wish to delete.</span></span>

        <span data-ttu-id="8ad35-255">b.</span><span class="sxs-lookup"><span data-stu-id="8ad35-255">b.</span></span> <span data-ttu-id="8ad35-256">On the main pane's toolbar, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="8ad35-256">On the main pane's toolbar, select **Delete**.</span></span>

        <span data-ttu-id="8ad35-257">c.</span><span class="sxs-lookup"><span data-stu-id="8ad35-257">c.</span></span> <span data-ttu-id="8ad35-258">Select **Yes** to the confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="8ad35-258">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8ad35-259">Next steps</span><span class="sxs-lookup"><span data-stu-id="8ad35-259">Next steps</span></span>

- <span data-ttu-id="8ad35-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8ad35-260">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com/).</span></span>

- <span data-ttu-id="8ad35-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="8ad35-261">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>




















