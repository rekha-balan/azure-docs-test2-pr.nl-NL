---
title: Manage Azure Blob Storage resources with Storage Explorer (Preview) | Microsoft Docs
description: Manage Azure Blob Containers and Blobs with Storage Explorer (Preview)
services: storage
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 22f904bf9c2388f809a2b22eba42ff955af7ad6c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556078"
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a><span data-ttu-id="f2e6e-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span><span class="sxs-lookup"><span data-stu-id="f2e6e-103">Manage Azure Blob Storage resources with Storage Explorer (Preview)</span></span>
## <a name="overview"></a><span data-ttu-id="f2e6e-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f2e6e-104">Overview</span></span>
<span data-ttu-id="f2e6e-105">[Azure Blob Storage](storage/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-105">[Azure Blob Storage](storage/storage-dotnet-how-to-use-blobs.md) is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span>
<span data-ttu-id="f2e6e-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-106">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span> <span data-ttu-id="f2e6e-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-107">In this article, you'll learn how to use Storage Explorer (Preview) to work with blob containers and blobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2e6e-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f2e6e-108">Prerequisites</span></span>
<span data-ttu-id="f2e6e-109">To complete the steps in this article, you'll need the following:</span><span class="sxs-lookup"><span data-stu-id="f2e6e-109">To complete the steps in this article, you'll need the following:</span></span>

* [<span data-ttu-id="f2e6e-110">Download and install Storage Explorer (preview)</span><span class="sxs-lookup"><span data-stu-id="f2e6e-110">Download and install Storage Explorer (preview)</span></span>](http://www.storageexplorer.com)
* [<span data-ttu-id="f2e6e-111">Connect to a Azure storage account or service</span><span class="sxs-lookup"><span data-stu-id="f2e6e-111">Connect to a Azure storage account or service</span></span>](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a><span data-ttu-id="f2e6e-112">Create a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-112">Create a blob container</span></span>
<span data-ttu-id="f2e6e-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-113">All blobs must reside in a blob container, which is simply a logical grouping of blobs.</span></span> <span data-ttu-id="f2e6e-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-114">An account can contain an unlimited number of containers, and each container can store an unlimited number of blobs.</span></span>

<span data-ttu-id="f2e6e-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-115">The following steps illustrate how to create a blob container within Storage Explorer (Preview).</span></span>

1. <span data-ttu-id="f2e6e-116">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-116">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-117">In the left pane, expand the storage account within which you wish to create the blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-117">In the left pane, expand the storage account within which you wish to create the blob container.</span></span>
3. <span data-ttu-id="f2e6e-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-118">Right-click **Blob Containers**, and - from the context menu - select **Create Blob Container**.</span></span>

   ![Create blob containers context menu][0]
4. <span data-ttu-id="f2e6e-120">A text box will appear below the **Blob Containers** folder.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-120">A text box will appear below the **Blob Containers** folder.</span></span> <span data-ttu-id="f2e6e-121">Enter the name for your blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-121">Enter the name for your blob container.</span></span> <span data-ttu-id="f2e6e-122">See the [Container naming rules](storage/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-122">See the [Container naming rules](storage/storage-dotnet-how-to-use-blobs.md#create-a-container) section for a list of rules and restrictions on naming blob containers.</span></span>

   ![Create Blob Containers text box][1]
5. <span data-ttu-id="f2e6e-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-124">Press **Enter** when done to create the blob container, or **Esc** to cancel.</span></span> <span data-ttu-id="f2e6e-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-125">Once the blob container has been successfully created, it will be displayed under the **Blob Containers** folder for the selected storage account.</span></span>

   ![Blob Container created][2]

## <a name="view-a-blob-containers-contents"></a><span data-ttu-id="f2e6e-127">View a blob container's contents</span><span class="sxs-lookup"><span data-stu-id="f2e6e-127">View a blob container's contents</span></span>
<span data-ttu-id="f2e6e-128">Blob containers contain blobs and folders (that can also contain blobs).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-128">Blob containers contain blobs and folders (that can also contain blobs).</span></span>

<span data-ttu-id="f2e6e-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span><span class="sxs-lookup"><span data-stu-id="f2e6e-129">The following steps illustrate how to view the contents of a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="f2e6e-130">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-130">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-131">In the left pane, expand the storage account containing the blob container you wish to view.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-131">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="f2e6e-132">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-132">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-133">Right-click the blob container you wish to view, and - from the context menu - select **Open Blob Container Editor**.</span></span>
   <span data-ttu-id="f2e6e-134">You can also double-click the blob container you wish to view.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-134">You can also double-click the blob container you wish to view.</span></span>

   ![Open blob container editor context menu][19]
5. <span data-ttu-id="f2e6e-136">The main pane will display the blob container's contents.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-136">The main pane will display the blob container's contents.</span></span>

   ![Blob container editor][3]

## <a name="delete-a-blob-container"></a><span data-ttu-id="f2e6e-138">Delete a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-138">Delete a blob container</span></span>
<span data-ttu-id="f2e6e-139">Blob containers can be easily created and deleted as needed.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-139">Blob containers can be easily created and deleted as needed.</span></span> <span data-ttu-id="f2e6e-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="f2e6e-140">(To see how to delete individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="f2e6e-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span><span class="sxs-lookup"><span data-stu-id="f2e6e-141">The following steps illustrate how to delete a blob container within Storage Explorer (Preview):</span></span>

1. <span data-ttu-id="f2e6e-142">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-142">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-143">In the left pane, expand the storage account containing the blob container you wish to view.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-143">In the left pane, expand the storage account containing the blob container you wish to view.</span></span>
3. <span data-ttu-id="f2e6e-144">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-144">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-145">Right-click the blob container you wish to delete, and - from the context menu - select **Delete**.</span></span>
   <span data-ttu-id="f2e6e-146">You can also press **Delete** to delete the currently selected blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-146">You can also press **Delete** to delete the currently selected blob container.</span></span>

   ![Delete blob container context menu][4]
5. <span data-ttu-id="f2e6e-148">Select **Yes** to the confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-148">Select **Yes** to the confirmation dialog.</span></span>

   ![Delete blob Container confirmation][5]

## <a name="copy-a-blob-container"></a><span data-ttu-id="f2e6e-150">Copy a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-150">Copy a blob container</span></span>
<span data-ttu-id="f2e6e-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-151">Storage Explorer (Preview) enables you to copy a blob container to the clipboard, and then paste that blob container into another storage account.</span></span> <span data-ttu-id="f2e6e-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span><span class="sxs-lookup"><span data-stu-id="f2e6e-152">(To see how to copy individual blobs, refer to the section, [Managing blobs in a blob container](#managing-blobs-in-a-blob-container).)</span></span>

<span data-ttu-id="f2e6e-153">The following steps illustrate how to copy a blob container from one storage account to another.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-153">The following steps illustrate how to copy a blob container from one storage account to another.</span></span>

1. <span data-ttu-id="f2e6e-154">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-154">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-155">In the left pane, expand the storage account containing the blob container you wish to copy.</span></span>
3. <span data-ttu-id="f2e6e-156">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-156">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-157">Right-click the blob container you wish to copy, and - from the context menu - select **Copy Blob Container**.</span></span>

   ![Copy blob container context menu][6]
5. <span data-ttu-id="f2e6e-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-159">Right-click the desired "target" storage account into which you want to paste the blob container, and - from the context menu - select **Paste Blob Container**.</span></span>

   ![Paste blob container context menu][7]

## <a name="get-the-sas-for-a-blob-container"></a><span data-ttu-id="f2e6e-161">Get the SAS for a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-161">Get the SAS for a blob container</span></span>
<span data-ttu-id="f2e6e-162">A [shared access signature (SAS)](storage/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-162">A [shared access signature (SAS)](storage/storage-dotnet-shared-access-signature-part-1.md) provides delegated access to resources in your storage account.</span></span>
<span data-ttu-id="f2e6e-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-163">This means that you can grant a client limited permissions to objects in your storage account for a specified period of time and with a specified set of permissions, without having to share your account access keys.</span></span>

<span data-ttu-id="f2e6e-164">The following steps illustrate how to create a SAS for a blob container:</span><span class="sxs-lookup"><span data-stu-id="f2e6e-164">The following steps illustrate how to create a SAS for a blob container:</span></span>

1. <span data-ttu-id="f2e6e-165">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-165">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-166">In the left pane, expand the storage account containing the blob container for which you wish to get a SAS.</span></span>
3. <span data-ttu-id="f2e6e-167">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-167">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-168">Right-click the desired blob container, and - from the context menu - select **Get Shared Access Signature**.</span></span>

   ![Get SAS context menu][8]
5. <span data-ttu-id="f2e6e-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-170">In the **Shared Access Signature** dialog, specify the policy, start and expiration dates, time zone, and access levels you want for the resource.</span></span>

   ![Get SAS options][9]
6. <span data-ttu-id="f2e6e-172">When you're finished specifying the SAS options, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-172">When you're finished specifying the SAS options, select **Create**.</span></span>
7. <span data-ttu-id="f2e6e-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-173">A second **Shared Access Signature** dialog will then display that lists the blob container along with the URL and QueryStrings you can use to access the storage resource.</span></span>
   <span data-ttu-id="f2e6e-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-174">Select **Copy** next to the URL you wish to copy to the clipboard.</span></span>

   ![Copy SAS URLs][10]
8. <span data-ttu-id="f2e6e-176">When done, select **Close**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-176">When done, select **Close**.</span></span>

## <a name="manage-access-policies-for-a-blob-container"></a><span data-ttu-id="f2e6e-177">Manage Access Policies for a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-177">Manage Access Policies for a blob container</span></span>
<span data-ttu-id="f2e6e-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span><span class="sxs-lookup"><span data-stu-id="f2e6e-178">The following steps illustrate how to manage (add and remove) access policies for a blob container:</span></span>

1. <span data-ttu-id="f2e6e-179">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-179">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-180">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="f2e6e-181">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-181">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-182">Select the desired blob container, and - from the context menu - select **Manage Access Policies**.</span></span>

   ![Manage access policies context menu][11]
5. <span data-ttu-id="f2e6e-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-184">The **Access Policies** dialog will list any access policies already created for the selected blob container.</span></span>

   ![Access Policy options][12]        
6. <span data-ttu-id="f2e6e-186">Follow these steps depending on the access policy management task:</span><span class="sxs-lookup"><span data-stu-id="f2e6e-186">Follow these steps depending on the access policy management task:</span></span>

   * <span data-ttu-id="f2e6e-187">**Add a new access policy** - Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-187">**Add a new access policy** - Select **Add**.</span></span> <span data-ttu-id="f2e6e-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-188">Once generated, the **Access Policies** dialog will display the newly added access policy (with default settings).</span></span>
   * <span data-ttu-id="f2e6e-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-189">**Edit an access policy** -  Make any desired edits, and select **Save**.</span></span>
   * <span data-ttu-id="f2e6e-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-190">**Remove an access policy** - Select **Remove** next to the access policy you wish to remove.</span></span>

## <a name="set-the-public-access-level-for-a-blob-container"></a><span data-ttu-id="f2e6e-191">Set the Public Access Level for a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-191">Set the Public Access Level for a blob container</span></span>
<span data-ttu-id="f2e6e-192">By default, every blob container is set to "No public access".</span><span class="sxs-lookup"><span data-stu-id="f2e6e-192">By default, every blob container is set to "No public access".</span></span>

<span data-ttu-id="f2e6e-193">The following steps illustrate how to specify a public access level for a blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-193">The following steps illustrate how to specify a public access level for a blob container.</span></span>

1. <span data-ttu-id="f2e6e-194">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-194">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-195">In the left pane, expand the storage account containing the blob container whose access policies you wish to manage.</span></span>
3. <span data-ttu-id="f2e6e-196">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-196">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-197">Select the desired blob container, and - from the context menu - select **Set Public Access Level**.</span></span>

   ![Set public access level context menu][13]
5. <span data-ttu-id="f2e6e-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-199">In the **Set Container Public Access Level** dialog, specify the desired access level.</span></span>

   ![Set public access level options][14]
6. <span data-ttu-id="f2e6e-201">Select **Apply**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-201">Select **Apply**.</span></span>

## <a name="managing-blobs-in-a-blob-container"></a><span data-ttu-id="f2e6e-202">Managing blobs in a blob container</span><span class="sxs-lookup"><span data-stu-id="f2e6e-202">Managing blobs in a blob container</span></span>
<span data-ttu-id="f2e6e-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-203">Once you've created a blob container, you can upload a blob to that blob container, download a blob to your local computer, open a blob on your local computer, and much more.</span></span>

<span data-ttu-id="f2e6e-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-204">The following steps illustrate how to manage the blobs (and folders) within a blob container.</span></span>

1. <span data-ttu-id="f2e6e-205">Open Storage Explorer (Preview).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-205">Open Storage Explorer (Preview).</span></span>
2. <span data-ttu-id="f2e6e-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-206">In the left pane, expand the storage account containing the blob container you wish to manage.</span></span>
3. <span data-ttu-id="f2e6e-207">Expand the storage account's **Blob Containers**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-207">Expand the storage account's **Blob Containers**.</span></span>
4. <span data-ttu-id="f2e6e-208">Double-click the blob container you wish to view.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-208">Double-click the blob container you wish to view.</span></span>
5. <span data-ttu-id="f2e6e-209">The main pane will display the blob container's contents.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-209">The main pane will display the blob container's contents.</span></span>

   ![View blob container][3]
6. <span data-ttu-id="f2e6e-211">The main pane will display the blob container's contents.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-211">The main pane will display the blob container's contents.</span></span>
7. <span data-ttu-id="f2e6e-212">Follow these steps depending on the task you wish to perform:</span><span class="sxs-lookup"><span data-stu-id="f2e6e-212">Follow these steps depending on the task you wish to perform:</span></span>

   * <span data-ttu-id="f2e6e-213">**Upload files to a blob container**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-213">**Upload files to a blob container**</span></span>

     1. <span data-ttu-id="f2e6e-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-214">On the main pane's toolbar, select **Upload**, and then **Upload Files** from the drop-down menu.</span></span>

        ![Upload files menu][15]
     2. <span data-ttu-id="f2e6e-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-216">In the **Upload files** dialog, select the ellipsis (**…**) button on the right side of the **Files** text box to select the file(s) you wish to upload.</span></span>

        ![Upload files options][16]
     3. <span data-ttu-id="f2e6e-218">Specify the type of **Blob type**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-218">Specify the type of **Blob type**.</span></span> <span data-ttu-id="f2e6e-219">The article [Get started with Azure Blob storage using .NET](storage/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-219">The article [Get started with Azure Blob storage using .NET](storage/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="f2e6e-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-220">Optionally, specify a target folder into which the selected file(s) will be uploaded.</span></span> <span data-ttu-id="f2e6e-221">If the target folder doesn’t exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-221">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="f2e6e-222">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-222">Select **Upload**.</span></span>
   * <span data-ttu-id="f2e6e-223">**Upload a folder to a blob container**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-223">**Upload a folder to a blob container**</span></span>

     1. <span data-ttu-id="f2e6e-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-224">On the main pane's toolbar, select **Upload**, and then **Upload Folder** from the drop-down menu.</span></span>

        ![Upload folder menu][17]
     2. <span data-ttu-id="f2e6e-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-226">In the **Upload folder** dialog, select the ellipsis (**…**) button on the right side of the **Folder** text box to select the folder whose contents you wish to upload.</span></span>

        ![Upload folder options][18]
     3. <span data-ttu-id="f2e6e-228">Specify the type of **Blob type**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-228">Specify the type of **Blob type**.</span></span> <span data-ttu-id="f2e6e-229">The article [Get started with Azure Blob storage using .NET](storage/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-229">The article [Get started with Azure Blob storage using .NET](storage/storage-dotnet-how-to-use-blobs.md#blob-service-concepts) explains the differences between the various blob types.</span></span>
     4. <span data-ttu-id="f2e6e-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-230">Optionally, specify a target folder into which the selected folder's contents will be uploaded.</span></span> <span data-ttu-id="f2e6e-231">If the target folder doesn’t exist, it will be created.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-231">If the target folder doesn’t exist, it will be created.</span></span>
     5. <span data-ttu-id="f2e6e-232">Select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-232">Select **Upload**.</span></span>
   * <span data-ttu-id="f2e6e-233">**Download a blob to your local computer**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-233">**Download a blob to your local computer**</span></span>

     1. <span data-ttu-id="f2e6e-234">Select the blob you wish to download.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-234">Select the blob you wish to download.</span></span>
     2. <span data-ttu-id="f2e6e-235">On the main pane's toolbar, select **Download**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-235">On the main pane's toolbar, select **Download**.</span></span>
     3. <span data-ttu-id="f2e6e-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-236">In the **Specify where to save the downloaded blob** dialog, specify the location where you want the blob downloaded, and the name you wish to give it.</span></span>  
     4. <span data-ttu-id="f2e6e-237">Select **Save**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-237">Select **Save**.</span></span>
   * <span data-ttu-id="f2e6e-238">**Open a blob on your local computer**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-238">**Open a blob on your local computer**</span></span>

     1. <span data-ttu-id="f2e6e-239">Select the blob you wish to open.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-239">Select the blob you wish to open.</span></span>
     2. <span data-ttu-id="f2e6e-240">On the main pane's toolbar, select **Open**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-240">On the main pane's toolbar, select **Open**.</span></span>
     3. <span data-ttu-id="f2e6e-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-241">The blob will be downloaded and opened using the application associated with the blob's underlying file type.</span></span>
   * <span data-ttu-id="f2e6e-242">**Copy a blob to the clipboard**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-242">**Copy a blob to the clipboard**</span></span>

     1. <span data-ttu-id="f2e6e-243">Select the blob you wish to copy.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-243">Select the blob you wish to copy.</span></span>
     2. <span data-ttu-id="f2e6e-244">On the main pane's toolbar, select **Copy**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-244">On the main pane's toolbar, select **Copy**.</span></span>
     3. <span data-ttu-id="f2e6e-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-245">In the left pane, navigate to another blob container, and double-click it to view it in the main pane.</span></span>
     4. <span data-ttu-id="f2e6e-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-246">On the main pane's toolbar, select **Paste** to create a copy of the blob.</span></span>
   * <span data-ttu-id="f2e6e-247">**Delete a blob**</span><span class="sxs-lookup"><span data-stu-id="f2e6e-247">**Delete a blob**</span></span>

     1. <span data-ttu-id="f2e6e-248">Select the blob you wish to delete.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-248">Select the blob you wish to delete.</span></span>
     2. <span data-ttu-id="f2e6e-249">On the main pane's toolbar, select **Delete**.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-249">On the main pane's toolbar, select **Delete**.</span></span>
     3. <span data-ttu-id="f2e6e-250">Select **Yes** to the confirmation dialog.</span><span class="sxs-lookup"><span data-stu-id="f2e6e-250">Select **Yes** to the confirmation dialog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2e6e-251">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2e6e-251">Next steps</span></span>
* <span data-ttu-id="f2e6e-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-252">View the [latest Storage Explorer (Preview) release notes and videos](http://www.storageexplorer.com).</span></span>
* <span data-ttu-id="f2e6e-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="f2e6e-253">Learn how to [create applications using Azure blobs, tables, queues, and files](https://azure.microsoft.com/documentation/services/storage/).</span></span>

[0]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png




















