---
title: Get started with Azure File storage on Windows | Microsoft Docs
description: Store file data in the cloud with Azure File storage, and mount your cloud file share from an Azure virtual machine (VM) or from an on-premises application running Windows.
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: renash
ms.openlocfilehash: ef1df89d807f8b58b61b4cdea0cbf054d1d22d86
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562701"
---
# <a name="get-started-with-azure-file-storage-on-windows"></a><span data-ttu-id="5ab77-103">Get started with Azure File storage on Windows</span><span class="sxs-lookup"><span data-stu-id="5ab77-103">Get started with Azure File storage on Windows</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

[!INCLUDE [storage-file-overview-include](../../includes/storage-file-overview-include.md)]

<span data-ttu-id="5ab77-104">For information on using File storage with Linux, see [How to use Azure File Storage with Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5ab77-104">For information on using File storage with Linux, see [How to use Azure File Storage with Linux](storage-how-to-use-files-linux.md).</span></span>

<span data-ttu-id="5ab77-105">For information on scalability and performance targets of File storage, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).</span><span class="sxs-lookup"><span data-stu-id="5ab77-105">For information on scalability and performance targets of File storage, see [Azure Storage Scalability and Performance Targets](storage-scalability-targets.md#scalability-targets-for-blobs-queues-tables-and-files).</span></span>

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

[!INCLUDE [storage-file-concepts-include](../../includes/storage-file-concepts-include.md)]

## <a name="video-using-azure-file-storage-with-windows"></a><span data-ttu-id="5ab77-106">Video: Using Azure File storage with Windows</span><span class="sxs-lookup"><span data-stu-id="5ab77-106">Video: Using Azure File storage with Windows</span></span>
<span data-ttu-id="5ab77-107">Here's a video that demonstrates how to create and use Azure File shares on Windows.</span><span class="sxs-lookup"><span data-stu-id="5ab77-107">Here's a video that demonstrates how to create and use Azure File shares on Windows.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-File-Storage-with-Windows/player]
> 
> 

## <a name="about-this-tutorial"></a><span data-ttu-id="5ab77-108">About this tutorial</span><span class="sxs-lookup"><span data-stu-id="5ab77-108">About this tutorial</span></span>
<span data-ttu-id="5ab77-109">This getting started tutorial demonstrates the basics of using Microsoft Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-109">This getting started tutorial demonstrates the basics of using Microsoft Azure File storage.</span></span> <span data-ttu-id="5ab77-110">In this tutorial, we will:</span><span class="sxs-lookup"><span data-stu-id="5ab77-110">In this tutorial, we will:</span></span>

* <span data-ttu-id="5ab77-111">Use Azure portal or PowerShell to create a new Azure File share, add a directory, upload a local file to the share, and list the files in the directory.</span><span class="sxs-lookup"><span data-stu-id="5ab77-111">Use Azure portal or PowerShell to create a new Azure File share, add a directory, upload a local file to the share, and list the files in the directory.</span></span>
* <span data-ttu-id="5ab77-112">Mount the file share, just as you would mount any SMB share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-112">Mount the file share, just as you would mount any SMB share.</span></span>
* <span data-ttu-id="5ab77-113">Use the Azure Storage Client Library for .NET to access the file share from an on-premises application.</span><span class="sxs-lookup"><span data-stu-id="5ab77-113">Use the Azure Storage Client Library for .NET to access the file share from an on-premises application.</span></span> <span data-ttu-id="5ab77-114">Create a console application and perform these actions with the file share:</span><span class="sxs-lookup"><span data-stu-id="5ab77-114">Create a console application and perform these actions with the file share:</span></span>
  * <span data-ttu-id="5ab77-115">Write the contents of a file in the share to the console window.</span><span class="sxs-lookup"><span data-stu-id="5ab77-115">Write the contents of a file in the share to the console window.</span></span>
  * <span data-ttu-id="5ab77-116">Set the quota (maximum size) for the file share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-116">Set the quota (maximum size) for the file share.</span></span>
  * <span data-ttu-id="5ab77-117">Create a shared access signature for a file that uses a shared access policy defined on the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-117">Create a shared access signature for a file that uses a shared access policy defined on the share.</span></span>
  * <span data-ttu-id="5ab77-118">Copy a file to another file in the same storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-118">Copy a file to another file in the same storage account.</span></span>
  * <span data-ttu-id="5ab77-119">Copy a file to a blob in the same storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-119">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="5ab77-120">Use Azure Storage Metrics for troubleshooting</span><span class="sxs-lookup"><span data-stu-id="5ab77-120">Use Azure Storage Metrics for troubleshooting</span></span>

<span data-ttu-id="5ab77-121">File storage is now supported for all storage accounts, so you can either use an existing storage account, or you can create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-121">File storage is now supported for all storage accounts, so you can either use an existing storage account, or you can create a new storage account.</span></span> <span data-ttu-id="5ab77-122">See [How to create a storage account](storage-create-storage-account.md#create-a-storage-account) for information on creating a new storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-122">See [How to create a storage account](storage-create-storage-account.md#create-a-storage-account) for information on creating a new storage account.</span></span>

## <a name="use-the-azure-portal-to-manage-a-file-share"></a><span data-ttu-id="5ab77-123">Use the Azure portal to manage a file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-123">Use the Azure portal to manage a file share</span></span>
<span data-ttu-id="5ab77-124">The [Azure portal](https://portal.azure.com) provides a user interface for customers to manage file shares.</span><span class="sxs-lookup"><span data-stu-id="5ab77-124">The [Azure portal](https://portal.azure.com) provides a user interface for customers to manage file shares.</span></span> <span data-ttu-id="5ab77-125">From the portal, you can:</span><span class="sxs-lookup"><span data-stu-id="5ab77-125">From the portal, you can:</span></span>

* <span data-ttu-id="5ab77-126">Create your file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-126">Create your file share</span></span>
* <span data-ttu-id="5ab77-127">Upload and download files to and from your file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-127">Upload and download files to and from your file share</span></span>
* <span data-ttu-id="5ab77-128">Monitor the actual usage of each file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-128">Monitor the actual usage of each file share</span></span>
* <span data-ttu-id="5ab77-129">Adjust the share size quota</span><span class="sxs-lookup"><span data-stu-id="5ab77-129">Adjust the share size quota</span></span>
* <span data-ttu-id="5ab77-130">Get the `net use` command to use to mount the file share from a Windows client</span><span class="sxs-lookup"><span data-stu-id="5ab77-130">Get the `net use` command to use to mount the file share from a Windows client</span></span>

### <a name="create-file-share"></a><span data-ttu-id="5ab77-131">Create file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-131">Create file share</span></span>
1. <span data-ttu-id="5ab77-132">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="5ab77-132">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="5ab77-133">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span><span class="sxs-lookup"><span data-stu-id="5ab77-133">On the navigation menu, click **Storage accounts** or **Storage accounts (classic)**.</span></span>
   
    ![Screenshot that shows how to create file share in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-create-share-0.png)
3. <span data-ttu-id="5ab77-135">Choose your storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-135">Choose your storage account.</span></span>
   
    ![Screenshot that shows how to create file share in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-create-share-1.png)
4. <span data-ttu-id="5ab77-137">Choose "Files" service.</span><span class="sxs-lookup"><span data-stu-id="5ab77-137">Choose "Files" service.</span></span>
   
    ![Screenshot that shows how to create file share in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-create-share-2.png)
5. <span data-ttu-id="5ab77-139">Click "File shares" and follow the link to create your first file share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-139">Click "File shares" and follow the link to create your first file share.</span></span>
   
    ![Screenshot that shows how to create file share in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-create-share-3.png)
6. <span data-ttu-id="5ab77-141">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-141">Fill in the file share name and the size of the file share (up to 5120 GB) to create your first file share.</span></span> <span data-ttu-id="5ab77-142">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="5ab77-142">Once the file share has been created, you can mount it from any file system that supports SMB 2.1 or SMB 3.0.</span></span>
   
    ![Screenshot that shows how to create file share in the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-create-share-4.png)

### <a name="upload-and-download-files"></a><span data-ttu-id="5ab77-144">Upload and download files</span><span class="sxs-lookup"><span data-stu-id="5ab77-144">Upload and download files</span></span>
1. <span data-ttu-id="5ab77-145">Choose one file share your already created.</span><span class="sxs-lookup"><span data-stu-id="5ab77-145">Choose one file share your already created.</span></span>
   
    ![Screenshot that shows how to upload and download files from the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-upload-download-1.png)
2. <span data-ttu-id="5ab77-147">Click **Upload** to open the user interface for files uploading.</span><span class="sxs-lookup"><span data-stu-id="5ab77-147">Click **Upload** to open the user interface for files uploading.</span></span>
   
    ![Screenshot that shows how to upload files from the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-upload-download-2.png)
3. <span data-ttu-id="5ab77-149">Right click on one file and choose **Download** to download it into local.</span><span class="sxs-lookup"><span data-stu-id="5ab77-149">Right click on one file and choose **Download** to download it into local.</span></span>
   
    ![Screenshot that shows how to download file from the portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-upload-download-3.png)

### <a name="manage-file-share"></a><span data-ttu-id="5ab77-151">Manage file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-151">Manage file share</span></span>
1. <span data-ttu-id="5ab77-152">Click **Quota** to change the size of the file share (up to 5120 GB).</span><span class="sxs-lookup"><span data-stu-id="5ab77-152">Click **Quota** to change the size of the file share (up to 5120 GB).</span></span>
   
    ![Screenshot that shows how to configure the quota of the file share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-manage-1.png)
2. <span data-ttu-id="5ab77-154">Click **Connect** to get the command line for mounting the file share from Windows.</span><span class="sxs-lookup"><span data-stu-id="5ab77-154">Click **Connect** to get the command line for mounting the file share from Windows.</span></span>
   
    ![Screenshot that shows how to mount the file share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-manage-2.png)
   
    ![Screenshot that shows how to mount the file share](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-manage-3.png)
   
   > [!TIP]
   > <span data-ttu-id="5ab77-157">To find the storage account access key for mounting, click **Settings** of your storage account, and then click **Access keys**.</span><span class="sxs-lookup"><span data-stu-id="5ab77-157">To find the storage account access key for mounting, click **Settings** of your storage account, and then click **Access keys**.</span></span>
   > 
   > 
   
    ![Screenshot that shows how to find the storage account access key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-manage-4.png)
   
    ![Screenshot that shows how to find the storage account access key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/storage-dotnet-how-to-use-files/files-manage-5.png)

## <a name="use-powershell-to-manage-a-file-share"></a><span data-ttu-id="5ab77-160">Use PowerShell to manage a file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-160">Use PowerShell to manage a file share</span></span>
<span data-ttu-id="5ab77-161">Alternatively, you can use Azure PowerShell to create and manage file shares.</span><span class="sxs-lookup"><span data-stu-id="5ab77-161">Alternatively, you can use Azure PowerShell to create and manage file shares.</span></span>

### <a name="install-the-powershell-cmdlets-for-azure-storage"></a><span data-ttu-id="5ab77-162">Install the PowerShell cmdlets for Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-162">Install the PowerShell cmdlets for Azure Storage</span></span>
<span data-ttu-id="5ab77-163">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5ab77-163">To prepare to use PowerShell, download and install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="5ab77-164">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span><span class="sxs-lookup"><span data-stu-id="5ab77-164">See [How to install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) for the install point and installation instructions.</span></span>

> [!NOTE]
> <span data-ttu-id="5ab77-165">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span><span class="sxs-lookup"><span data-stu-id="5ab77-165">It's recommended that you download and install or upgrade to the latest Azure PowerShell module.</span></span>
> 
> 

<span data-ttu-id="5ab77-166">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="5ab77-166">Open an Azure PowerShell window by clicking **Start** and typing **Windows PowerShell**.</span></span> <span data-ttu-id="5ab77-167">The PowerShell window loads the Azure Powershell module for you.</span><span class="sxs-lookup"><span data-stu-id="5ab77-167">The PowerShell window loads the Azure Powershell module for you.</span></span>

### <a name="create-a-context-for-your-storage-account-and-key"></a><span data-ttu-id="5ab77-168">Create a context for your storage account and key</span><span class="sxs-lookup"><span data-stu-id="5ab77-168">Create a context for your storage account and key</span></span>
<span data-ttu-id="5ab77-169">Now, create the storage account context.</span><span class="sxs-lookup"><span data-stu-id="5ab77-169">Now, create the storage account context.</span></span> <span data-ttu-id="5ab77-170">The context encapsulates the storage account name and account key.</span><span class="sxs-lookup"><span data-stu-id="5ab77-170">The context encapsulates the storage account name and account key.</span></span> <span data-ttu-id="5ab77-171">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="5ab77-171">For instructions on copying your account key from the [Azure portal](https://portal.azure.com), see [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys).</span></span>

<span data-ttu-id="5ab77-172">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span><span class="sxs-lookup"><span data-stu-id="5ab77-172">Replace `storage-account-name` and `storage-account-key` with your storage account name and key in the following example.</span></span>

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

### <a name="create-a-new-file-share"></a><span data-ttu-id="5ab77-173">Create a new file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-173">Create a new file share</span></span>
<span data-ttu-id="5ab77-174">Next, create the new share, named `logs`.</span><span class="sxs-lookup"><span data-stu-id="5ab77-174">Next, create the new share, named `logs`.</span></span>

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

<span data-ttu-id="5ab77-175">You now have a file share in File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-175">You now have a file share in File storage.</span></span> <span data-ttu-id="5ab77-176">Next we'll add a directory and a file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-176">Next we'll add a directory and a file.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5ab77-177">The name of your file share must be all lowercase.</span><span class="sxs-lookup"><span data-stu-id="5ab77-177">The name of your file share must be all lowercase.</span></span> <span data-ttu-id="5ab77-178">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ab77-178">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://msdn.microsoft.com/library/azure/dn167011.aspx).</span></span>
> 
> 

### <a name="create-a-directory-in-the-file-share"></a><span data-ttu-id="5ab77-179">Create a directory in the file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-179">Create a directory in the file share</span></span>
<span data-ttu-id="5ab77-180">Next, create a directory in the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-180">Next, create a directory in the share.</span></span> <span data-ttu-id="5ab77-181">In the following example, the directory is named `CustomLogs`.</span><span class="sxs-lookup"><span data-stu-id="5ab77-181">In the following example, the directory is named `CustomLogs`.</span></span>

```powershell
# create a directory in the share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

### <a name="upload-a-local-file-to-the-directory"></a><span data-ttu-id="5ab77-182">Upload a local file to the directory</span><span class="sxs-lookup"><span data-stu-id="5ab77-182">Upload a local file to the directory</span></span>
<span data-ttu-id="5ab77-183">Now upload a local file to the directory.</span><span class="sxs-lookup"><span data-stu-id="5ab77-183">Now upload a local file to the directory.</span></span> <span data-ttu-id="5ab77-184">The following example uploads a file from `C:\temp\Log1.txt`.</span><span class="sxs-lookup"><span data-stu-id="5ab77-184">The following example uploads a file from `C:\temp\Log1.txt`.</span></span> <span data-ttu-id="5ab77-185">Edit the file path so that it points to a valid file on your local machine.</span><span class="sxs-lookup"><span data-stu-id="5ab77-185">Edit the file path so that it points to a valid file on your local machine.</span></span>

```powershell
# upload a local file to the new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

### <a name="list-the-files-in-the-directory"></a><span data-ttu-id="5ab77-186">List the files in the directory</span><span class="sxs-lookup"><span data-stu-id="5ab77-186">List the files in the directory</span></span>
<span data-ttu-id="5ab77-187">To see the file in the directory, you can list all of the directory's files.</span><span class="sxs-lookup"><span data-stu-id="5ab77-187">To see the file in the directory, you can list all of the directory's files.</span></span> <span data-ttu-id="5ab77-188">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span><span class="sxs-lookup"><span data-stu-id="5ab77-188">This command returns the files and subdirectories (if there are any) in the CustomLogs directory.</span></span>

```powershell
# list files in the new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

<span data-ttu-id="5ab77-189">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span><span class="sxs-lookup"><span data-stu-id="5ab77-189">Get-AzureStorageFile returns a list of files and directories for whatever directory object is passed in.</span></span> <span data-ttu-id="5ab77-190">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span><span class="sxs-lookup"><span data-stu-id="5ab77-190">"Get-AzureStorageFile -Share $s" returns a list of files and directories in the root directory.</span></span> <span data-ttu-id="5ab77-191">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span><span class="sxs-lookup"><span data-stu-id="5ab77-191">To get a list of files in a subdirectory, you have to pass the subdirectory to Get-AzureStorageFile.</span></span> <span data-ttu-id="5ab77-192">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="5ab77-192">That's what this does -- the first part of the command up to the pipe returns a directory instance of the subdirectory CustomLogs.</span></span> <span data-ttu-id="5ab77-193">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span><span class="sxs-lookup"><span data-stu-id="5ab77-193">Then that is passed into Get-AzureStorageFile, which returns the files and directories in CustomLogs.</span></span>

### <a name="copy-files"></a><span data-ttu-id="5ab77-194">Copy files</span><span class="sxs-lookup"><span data-stu-id="5ab77-194">Copy files</span></span>
<span data-ttu-id="5ab77-195">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-195">Beginning with version 0.9.7 of Azure PowerShell, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="5ab77-196">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5ab77-196">Below we demonstrate how to perform these copy operations using PowerShell cmdlets.</span></span>

```powershell
# copy a file to the new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob to a file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```

## <a name="mount-the-file-share"></a><span data-ttu-id="5ab77-197">Mount the file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-197">Mount the file share</span></span>
<span data-ttu-id="5ab77-198">With support for SMB 3.0, File storage now supports encryption and persistent handles from SMB 3.0 clients.</span><span class="sxs-lookup"><span data-stu-id="5ab77-198">With support for SMB 3.0, File storage now supports encryption and persistent handles from SMB 3.0 clients.</span></span> <span data-ttu-id="5ab77-199">Support for encryption means that SMB 3.0 clients can mount a file share from anywhere, including from:</span><span class="sxs-lookup"><span data-stu-id="5ab77-199">Support for encryption means that SMB 3.0 clients can mount a file share from anywhere, including from:</span></span>

* <span data-ttu-id="5ab77-200">An Azure virtual machine in the same region (also supported by SMB 2.1)</span><span class="sxs-lookup"><span data-stu-id="5ab77-200">An Azure virtual machine in the same region (also supported by SMB 2.1)</span></span>
* <span data-ttu-id="5ab77-201">An Azure virtual machine in a different region (SMB 3.0 only)</span><span class="sxs-lookup"><span data-stu-id="5ab77-201">An Azure virtual machine in a different region (SMB 3.0 only)</span></span>
* <span data-ttu-id="5ab77-202">An on-premises client application (SMB 3.0 only)</span><span class="sxs-lookup"><span data-stu-id="5ab77-202">An on-premises client application (SMB 3.0 only)</span></span>

<span data-ttu-id="5ab77-203">When a client accesses File storage, the SMB version used depends on the SMB version supported by the operating system.</span><span class="sxs-lookup"><span data-stu-id="5ab77-203">When a client accesses File storage, the SMB version used depends on the SMB version supported by the operating system.</span></span> <span data-ttu-id="5ab77-204">The table below provides a summary of support for Windows clients.</span><span class="sxs-lookup"><span data-stu-id="5ab77-204">The table below provides a summary of support for Windows clients.</span></span> <span data-ttu-id="5ab77-205">Please refer to this blog for more details on [SMB versions](http://blogs.technet.com/b/josebda/archive/2013/10/02/windows-server-2012-r2-which-version-of-the-smb-protocol-smb-1-0-smb-2-0-smb-2-1-smb-3-0-or-smb-3-02-you-are-using.aspx).</span><span class="sxs-lookup"><span data-stu-id="5ab77-205">Please refer to this blog for more details on [SMB versions](http://blogs.technet.com/b/josebda/archive/2013/10/02/windows-server-2012-r2-which-version-of-the-smb-protocol-smb-1-0-smb-2-0-smb-2-1-smb-3-0-or-smb-3-02-you-are-using.aspx).</span></span>

| <span data-ttu-id="5ab77-206">Windows Client</span><span class="sxs-lookup"><span data-stu-id="5ab77-206">Windows Client</span></span> | <span data-ttu-id="5ab77-207">SMB Version Supported</span><span class="sxs-lookup"><span data-stu-id="5ab77-207">SMB Version Supported</span></span> |
|:--- |:--- |
| <span data-ttu-id="5ab77-208">Windows 7</span><span class="sxs-lookup"><span data-stu-id="5ab77-208">Windows 7</span></span> |<span data-ttu-id="5ab77-209">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="5ab77-209">SMB 2.1</span></span> |
| <span data-ttu-id="5ab77-210">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="5ab77-210">Windows Server 2008 R2</span></span> |<span data-ttu-id="5ab77-211">SMB 2.1</span><span class="sxs-lookup"><span data-stu-id="5ab77-211">SMB 2.1</span></span> |
| <span data-ttu-id="5ab77-212">Windows 8</span><span class="sxs-lookup"><span data-stu-id="5ab77-212">Windows 8</span></span> |<span data-ttu-id="5ab77-213">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5ab77-213">SMB 3.0</span></span> |
| <span data-ttu-id="5ab77-214">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="5ab77-214">Windows Server 2012</span></span> |<span data-ttu-id="5ab77-215">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5ab77-215">SMB 3.0</span></span> |
| <span data-ttu-id="5ab77-216">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="5ab77-216">Windows Server 2012 R2</span></span> |<span data-ttu-id="5ab77-217">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5ab77-217">SMB 3.0</span></span> |
| <span data-ttu-id="5ab77-218">Windows 10</span><span class="sxs-lookup"><span data-stu-id="5ab77-218">Windows 10</span></span> |<span data-ttu-id="5ab77-219">SMB 3.0</span><span class="sxs-lookup"><span data-stu-id="5ab77-219">SMB 3.0</span></span> |

### <a name="mount-the-file-share-from-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="5ab77-220">Mount the file share from an Azure virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="5ab77-220">Mount the file share from an Azure virtual machine running Windows</span></span>
<span data-ttu-id="5ab77-221">To demonstrate how to mount an Azure file share, we'll now create an Azure virtual machine running Windows, and remote into it to mount the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-221">To demonstrate how to mount an Azure file share, we'll now create an Azure virtual machine running Windows, and remote into it to mount the share.</span></span>

1. <span data-ttu-id="5ab77-222">First, create a new Azure virtual machine by following the instructions in [Create a Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ab77-222">First, create a new Azure virtual machine by following the instructions in [Create a Windows virtual machine in the Azure portal](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
2. <span data-ttu-id="5ab77-223">Next, remote into the virtual machine by following the instructions in [Log on to a Windows virtual machine using the Azure portal](../virtual-machines/virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5ab77-223">Next, remote into the virtual machine by following the instructions in [Log on to a Windows virtual machine using the Azure portal](../virtual-machines/virtual-machines-windows-connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
3. <span data-ttu-id="5ab77-224">Open a PowerShell window on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ab77-224">Open a PowerShell window on the virtual machine.</span></span>

### <a name="persist-your-storage-account-credentials-for-the-virtual-machine"></a><span data-ttu-id="5ab77-225">Persist your storage account credentials for the virtual machine</span><span class="sxs-lookup"><span data-stu-id="5ab77-225">Persist your storage account credentials for the virtual machine</span></span>
<span data-ttu-id="5ab77-226">Before mounting to the file share, first persist your storage account credentials on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ab77-226">Before mounting to the file share, first persist your storage account credentials on the virtual machine.</span></span> <span data-ttu-id="5ab77-227">This step allows Windows to automatically reconnect to the file share when the virtual machine reboots.</span><span class="sxs-lookup"><span data-stu-id="5ab77-227">This step allows Windows to automatically reconnect to the file share when the virtual machine reboots.</span></span> <span data-ttu-id="5ab77-228">To persist your account credentials, run the `cmdkey` command from the PowerShell window on the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5ab77-228">To persist your account credentials, run the `cmdkey` command from the PowerShell window on the virtual machine.</span></span> <span data-ttu-id="5ab77-229">Replace `<storage-account-name>` with the name of your storage account, and `<storage-account-key>` with your storage account key.</span><span class="sxs-lookup"><span data-stu-id="5ab77-229">Replace `<storage-account-name>` with the name of your storage account, and `<storage-account-key>` with your storage account key.</span></span> <span data-ttu-id="5ab77-230">You have to explicitly specify domain "AZURE" as in sample below.</span><span class="sxs-lookup"><span data-stu-id="5ab77-230">You have to explicitly specify domain "AZURE" as in sample below.</span></span> 

```
cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
```

<span data-ttu-id="5ab77-231">Windows will now reconnect to your file share when the virtual machine reboots.</span><span class="sxs-lookup"><span data-stu-id="5ab77-231">Windows will now reconnect to your file share when the virtual machine reboots.</span></span> <span data-ttu-id="5ab77-232">You can verify that the share has been reconnected by running the `net use` command from a PowerShell window.</span><span class="sxs-lookup"><span data-stu-id="5ab77-232">You can verify that the share has been reconnected by running the `net use` command from a PowerShell window.</span></span>

<span data-ttu-id="5ab77-233">Note that credentials are persisted only in the context in which `cmdkey` runs.</span><span class="sxs-lookup"><span data-stu-id="5ab77-233">Note that credentials are persisted only in the context in which `cmdkey` runs.</span></span> <span data-ttu-id="5ab77-234">If you are developing an application that runs as a service, you will need to persist your credentials in that context as well.</span><span class="sxs-lookup"><span data-stu-id="5ab77-234">If you are developing an application that runs as a service, you will need to persist your credentials in that context as well.</span></span>

### <a name="mount-the-file-share-using-the-persisted-credentials"></a><span data-ttu-id="5ab77-235">Mount the file share using the persisted credentials</span><span class="sxs-lookup"><span data-stu-id="5ab77-235">Mount the file share using the persisted credentials</span></span>
<span data-ttu-id="5ab77-236">Once you have a remote connection to the virtual machine, you can run the `net use` command to mount the file share, using the following syntax.</span><span class="sxs-lookup"><span data-stu-id="5ab77-236">Once you have a remote connection to the virtual machine, you can run the `net use` command to mount the file share, using the following syntax.</span></span> <span data-ttu-id="5ab77-237">Replace `<storage-account-name>` with the name of your storage account, and `<share-name>` with the name of your File storage share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-237">Replace `<storage-account-name>` with the name of your storage account, and `<share-name>` with the name of your File storage share.</span></span>

```
net use <drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name>

example :
net use z: \\samples.file.core.windows.net\logs
```

<span data-ttu-id="5ab77-238">Since you persisted your storage account credentials in the previous step, you do not need to provide them with the `net use` command.</span><span class="sxs-lookup"><span data-stu-id="5ab77-238">Since you persisted your storage account credentials in the previous step, you do not need to provide them with the `net use` command.</span></span> <span data-ttu-id="5ab77-239">If you have not already persisted your credentials, then include them as a parameter passed to the `net use` command, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="5ab77-239">If you have not already persisted your credentials, then include them as a parameter passed to the `net use` command, as shown in the following example.</span></span>

```
net use <drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> /u:AZURE\<storage-account-name> <storage-account-key>

example :
net use z: \\samples.file.core.windows.net\logs /u:AZURE\samples <storage-account-key>
```

<span data-ttu-id="5ab77-240">You can now work with the File Storage share from the virtual machine as you would with any other drive.</span><span class="sxs-lookup"><span data-stu-id="5ab77-240">You can now work with the File Storage share from the virtual machine as you would with any other drive.</span></span> <span data-ttu-id="5ab77-241">You can issue standard file commands from the command prompt, or view the mounted share and its contents from File Explorer.</span><span class="sxs-lookup"><span data-stu-id="5ab77-241">You can issue standard file commands from the command prompt, or view the mounted share and its contents from File Explorer.</span></span> <span data-ttu-id="5ab77-242">You can also run code within the virtual machine that accesses the file share using standard Windows file I/O APIs, such as those provided by the [System.IO namespaces](http://msdn.microsoft.com/library/gg145019.aspx) in the .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="5ab77-242">You can also run code within the virtual machine that accesses the file share using standard Windows file I/O APIs, such as those provided by the [System.IO namespaces](http://msdn.microsoft.com/library/gg145019.aspx) in the .NET Framework.</span></span>

<span data-ttu-id="5ab77-243">You can also mount the file share from a role running in an Azure cloud service by remoting into the role.</span><span class="sxs-lookup"><span data-stu-id="5ab77-243">You can also mount the file share from a role running in an Azure cloud service by remoting into the role.</span></span>

### <a name="mount-the-file-share-from-an-on-premises-client-running-windows"></a><span data-ttu-id="5ab77-244">Mount the file share from an on-premises client running Windows</span><span class="sxs-lookup"><span data-stu-id="5ab77-244">Mount the file share from an on-premises client running Windows</span></span>
<span data-ttu-id="5ab77-245">To mount the file share from an on-premises client, you must first take these steps:</span><span class="sxs-lookup"><span data-stu-id="5ab77-245">To mount the file share from an on-premises client, you must first take these steps:</span></span>

* <span data-ttu-id="5ab77-246">Install a version of Windows which supports SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="5ab77-246">Install a version of Windows which supports SMB 3.0.</span></span> <span data-ttu-id="5ab77-247">Windows will leverage SMB 3.0 encryption to securely transfer data between your on-premises client and the Azure file share in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5ab77-247">Windows will leverage SMB 3.0 encryption to securely transfer data between your on-premises client and the Azure file share in the cloud.</span></span>
* <span data-ttu-id="5ab77-248">Open Internet access for port 445 (TCP Outbound) in your local network, as is required by the SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="5ab77-248">Open Internet access for port 445 (TCP Outbound) in your local network, as is required by the SMB protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="5ab77-249">Some Internet service providers may block port 445, so you may need to check with your service provider.</span><span class="sxs-lookup"><span data-stu-id="5ab77-249">Some Internet service providers may block port 445, so you may need to check with your service provider.</span></span>
> 
> 

### <a name="unmount-the-file-share"></a><span data-ttu-id="5ab77-250">Unmount the file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-250">Unmount the file share</span></span>
<span data-ttu-id="5ab77-251">To unmount the file share, you can use `net use` command with `/delete` option.</span><span class="sxs-lookup"><span data-stu-id="5ab77-251">To unmount the file share, you can use `net use` command with `/delete` option.</span></span>

```
net use <drive-letter> /delete

example :
net use z: /delete
```

## <a name="develop-with-file-storage"></a><span data-ttu-id="5ab77-252">Develop with File storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-252">Develop with File storage</span></span>
<span data-ttu-id="5ab77-253">To write code that calls File storage, you can use the storage client libraries for .NET and Java, or the Azure Storage REST API.</span><span class="sxs-lookup"><span data-stu-id="5ab77-253">To write code that calls File storage, you can use the storage client libraries for .NET and Java, or the Azure Storage REST API.</span></span> <span data-ttu-id="5ab77-254">The example in this section demonstrates how to work with a file share by using the [Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/mt347887.aspx) from a simple console application running on the desktop.</span><span class="sxs-lookup"><span data-stu-id="5ab77-254">The example in this section demonstrates how to work with a file share by using the [Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/mt347887.aspx) from a simple console application running on the desktop.</span></span>

### <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="5ab77-255">Create the console application and obtain the assembly</span><span class="sxs-lookup"><span data-stu-id="5ab77-255">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="5ab77-256">In Visual Studio, create a new Windows console application.</span><span class="sxs-lookup"><span data-stu-id="5ab77-256">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="5ab77-257">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5ab77-257">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="5ab77-258">Select **File** > **New** > **Project**</span><span class="sxs-lookup"><span data-stu-id="5ab77-258">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="5ab77-259">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span><span class="sxs-lookup"><span data-stu-id="5ab77-259">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="5ab77-260">Select **Console App (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="5ab77-260">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="5ab77-261">Enter a name for your application in the **Name:** field</span><span class="sxs-lookup"><span data-stu-id="5ab77-261">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="5ab77-262">Select **OK**</span><span class="sxs-lookup"><span data-stu-id="5ab77-262">Select **OK**</span></span>

<span data-ttu-id="5ab77-263">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-263">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="5ab77-264">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span><span class="sxs-lookup"><span data-stu-id="5ab77-264">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="5ab77-265">In this guide, we use a console application for simplicity.</span><span class="sxs-lookup"><span data-stu-id="5ab77-265">In this guide, we use a console application for simplicity.</span></span>

### <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="5ab77-266">Use NuGet to install the required packages</span><span class="sxs-lookup"><span data-stu-id="5ab77-266">Use NuGet to install the required packages</span></span>
<span data-ttu-id="5ab77-267">There are two packages you need to reference in your project to complete this tutorial:</span><span class="sxs-lookup"><span data-stu-id="5ab77-267">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="5ab77-268">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-268">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="5ab77-269">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span><span class="sxs-lookup"><span data-stu-id="5ab77-269">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="5ab77-270">You can use NuGet to obtain both packages.</span><span class="sxs-lookup"><span data-stu-id="5ab77-270">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="5ab77-271">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="5ab77-271">Follow these steps:</span></span>

1. <span data-ttu-id="5ab77-272">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="5ab77-272">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5ab77-273">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span><span class="sxs-lookup"><span data-stu-id="5ab77-273">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="5ab77-274">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="5ab77-274">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

### <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="5ab77-275">Save your storage account credentials to the app.config file</span><span class="sxs-lookup"><span data-stu-id="5ab77-275">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="5ab77-276">Next, save your credentials in your project's app.config file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-276">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="5ab77-277">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span><span class="sxs-lookup"><span data-stu-id="5ab77-277">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> The latest version of the Azure storage emulator does not support File storage. <span data-ttu-id="5ab77-279">Your connection string must target an Azure storage account in the cloud to work with File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-279">Your connection string must target an Azure storage account in the cloud to work with File storage.</span></span>
> 
> 

### <a name="add-using-directives"></a><span data-ttu-id="5ab77-280">Add using directives</span><span class="sxs-lookup"><span data-stu-id="5ab77-280">Add using directives</span></span>
<span data-ttu-id="5ab77-281">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-281">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage
using Microsoft.WindowsAzure.Storage.File; // Namespace for File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="access-the-file-share-programmatically"></a><span data-ttu-id="5ab77-282">Access the file share programmatically</span><span class="sxs-lookup"><span data-stu-id="5ab77-282">Access the file share programmatically</span></span>
<span data-ttu-id="5ab77-283">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span><span class="sxs-lookup"><span data-stu-id="5ab77-283">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="5ab77-284">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span><span class="sxs-lookup"><span data-stu-id="5ab77-284">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="5ab77-285">Run the console application to see the output.</span><span class="sxs-lookup"><span data-stu-id="5ab77-285">Run the console application to see the output.</span></span>

### <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="5ab77-286">Set the maximum size for a file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-286">Set the maximum size for a file share</span></span>
<span data-ttu-id="5ab77-287">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span><span class="sxs-lookup"><span data-stu-id="5ab77-287">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="5ab77-288">You can also check to see how much data is currently stored on the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-288">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="5ab77-289">By setting the quota for a share, you can limit the total size of the files stored on the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-289">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="5ab77-290">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span><span class="sxs-lookup"><span data-stu-id="5ab77-290">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="5ab77-291">The example below shows how to check the current usage for a share and how to set the quota for the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-291">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="5ab77-292">Generate a shared access signature for a file or file share</span><span class="sxs-lookup"><span data-stu-id="5ab77-292">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="5ab77-293">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-293">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="5ab77-294">You can also create a shared access policy on a file share to manage shared access signatures.</span><span class="sxs-lookup"><span data-stu-id="5ab77-294">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="5ab77-295">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span><span class="sxs-lookup"><span data-stu-id="5ab77-295">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="5ab77-296">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-296">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="5ab77-297">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Blob storage](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="5ab77-297">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Blob storage](storage-dotnet-shared-access-signature-part-2.md).</span></span>

### <a name="copy-files"></a><span data-ttu-id="5ab77-298">Copy files</span><span class="sxs-lookup"><span data-stu-id="5ab77-298">Copy files</span></span>
<span data-ttu-id="5ab77-299">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-299">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="5ab77-300">In the next sections, we demonstrate how to perform these copy operations programmatically.</span><span class="sxs-lookup"><span data-stu-id="5ab77-300">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="5ab77-301">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span><span class="sxs-lookup"><span data-stu-id="5ab77-301">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="5ab77-302">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="5ab77-302">See [Transfer data with the AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5ab77-303">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-303">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="5ab77-304">**Copy a file to another file**</span><span class="sxs-lookup"><span data-stu-id="5ab77-304">**Copy a file to another file**</span></span>

<span data-ttu-id="5ab77-305">The following example copies a file to another file in the same share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-305">The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="5ab77-306">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span><span class="sxs-lookup"><span data-stu-id="5ab77-306">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="5ab77-307">**Copy a file to a blob**</span><span class="sxs-lookup"><span data-stu-id="5ab77-307">**Copy a file to a blob**</span></span>

<span data-ttu-id="5ab77-308">The following example creates a file and copies it to a blob within the same storage account.</span><span class="sxs-lookup"><span data-stu-id="5ab77-308">The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="5ab77-309">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span><span class="sxs-lookup"><span data-stu-id="5ab77-309">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="5ab77-310">You can copy a blob to a file in the same way.</span><span class="sxs-lookup"><span data-stu-id="5ab77-310">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="5ab77-311">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span><span class="sxs-lookup"><span data-stu-id="5ab77-311">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-file-storage-using-metrics"></a><span data-ttu-id="5ab77-312">Troubleshooting File storage using metrics</span><span class="sxs-lookup"><span data-stu-id="5ab77-312">Troubleshooting File storage using metrics</span></span>
<span data-ttu-id="5ab77-313">Azure Storage Analytics now supports metrics for File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-313">Azure Storage Analytics now supports metrics for File storage.</span></span> <span data-ttu-id="5ab77-314">With metrics data, you can trace requests and diagnose issues.</span><span class="sxs-lookup"><span data-stu-id="5ab77-314">With metrics data, you can trace requests and diagnose issues.</span></span>

<span data-ttu-id="5ab77-315">You can enable metrics for File storage from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5ab77-315">You can enable metrics for File storage from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="5ab77-316">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span><span class="sxs-lookup"><span data-stu-id="5ab77-316">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>

<span data-ttu-id="5ab77-317">The following code example shows how to use the Storage Client Library for .NET to enable metrics for File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-317">The following code example shows how to use the Storage Client Library for .NET to enable metrics for File storage.</span></span>

<span data-ttu-id="5ab77-318">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span><span class="sxs-lookup"><span data-stu-id="5ab77-318">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="5ab77-319">Note that while Blob, Table, and Queue storage use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span><span class="sxs-lookup"><span data-stu-id="5ab77-319">Note that while Blob, Table, and Queue storage use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="5ab77-320">Both namespaces must be referenced from your code, however, for the following code to compile.</span><span class="sxs-lookup"><span data-stu-id="5ab77-320">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read the metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="5ab77-321">Also, you can refer to [Azure Files Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span><span class="sxs-lookup"><span data-stu-id="5ab77-321">Also, you can refer to [Azure Files Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span> 

## <a name="file-storage-faq"></a><span data-ttu-id="5ab77-322">File storage FAQ</span><span class="sxs-lookup"><span data-stu-id="5ab77-322">File storage FAQ</span></span>
1. <span data-ttu-id="5ab77-323">**Is Active Directory-based authentication supported by File storage?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-323">**Is Active Directory-based authentication supported by File storage?**</span></span>
   
    <span data-ttu-id="5ab77-324">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span><span class="sxs-lookup"><span data-stu-id="5ab77-324">We currently do not support AD-based authentication or ACLs, but do have it in our list of feature requests.</span></span> <span data-ttu-id="5ab77-325">For now, the Azure Storage account keys are used to provide authentication to the file share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-325">For now, the Azure Storage account keys are used to provide authentication to the file share.</span></span> <span data-ttu-id="5ab77-326">We do offer a workaround using shared access signatures (SAS) via the REST API or the client libraries.</span><span class="sxs-lookup"><span data-stu-id="5ab77-326">We do offer a workaround using shared access signatures (SAS) via the REST API or the client libraries.</span></span> <span data-ttu-id="5ab77-327">Using SAS, you can generate tokens with specific permissions that are valid over a specified time interval.</span><span class="sxs-lookup"><span data-stu-id="5ab77-327">Using SAS, you can generate tokens with specific permissions that are valid over a specified time interval.</span></span> <span data-ttu-id="5ab77-328">For example, you can generate a token with read-only access to a given file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-328">For example, you can generate a token with read-only access to a given file.</span></span> <span data-ttu-id="5ab77-329">Anyone who possesses this token while it is valid has read-only access to that file.</span><span class="sxs-lookup"><span data-stu-id="5ab77-329">Anyone who possesses this token while it is valid has read-only access to that file.</span></span>
   
    <span data-ttu-id="5ab77-330">SAS is only supported via the REST API or client libraries.</span><span class="sxs-lookup"><span data-stu-id="5ab77-330">SAS is only supported via the REST API or client libraries.</span></span> <span data-ttu-id="5ab77-331">When you mount the file share via the SMB protocol,  you can't use a SAS to delegate access to its contents.</span><span class="sxs-lookup"><span data-stu-id="5ab77-331">When you mount the file share via the SMB protocol,  you can't use a SAS to delegate access to its contents.</span></span> 

2. <span data-ttu-id="5ab77-332">**How can I provide access to a specific file over a web browser?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-332">**How can I provide access to a specific file over a web browser?**</span></span>
   <span data-ttu-id="5ab77-333">Using SAS, you can generate tokens with specific permissions that are valid over a specified time interval.</span><span class="sxs-lookup"><span data-stu-id="5ab77-333">Using SAS, you can generate tokens with specific permissions that are valid over a specified time interval.</span></span> <span data-ttu-id="5ab77-334">For example, you can generate a token with read-only access to a particular file for a specific period of time.</span><span class="sxs-lookup"><span data-stu-id="5ab77-334">For example, you can generate a token with read-only access to a particular file for a specific period of time.</span></span> <span data-ttu-id="5ab77-335">Anyone who possesses this url can perform download directly from any web browser while it is valid.</span><span class="sxs-lookup"><span data-stu-id="5ab77-335">Anyone who possesses this url can perform download directly from any web browser while it is valid.</span></span> <span data-ttu-id="5ab77-336">SAS keys can be easily generated from UI like Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="5ab77-336">SAS keys can be easily generated from UI like Storage Explorer.</span></span>

3.   <span data-ttu-id="5ab77-337">**What are different ways to access files in Azure File storage?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-337">**What are different ways to access files in Azure File storage?**</span></span>
    <span data-ttu-id="5ab77-338">You can mount the fileshare on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) or Cloudberry to access files in your file share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-338">You can mount the fileshare on your local machine using SMB 3.0 protocol or use tools like [Storage Explorer](http://storageexplorer.com/) or Cloudberry to access files in your file share.</span></span> <span data-ttu-id="5ab77-339">From your application, you can use Client Libraries, REST API or Powershell to access your files in Azure File share.</span><span class="sxs-lookup"><span data-stu-id="5ab77-339">From your application, you can use Client Libraries, REST API or Powershell to access your files in Azure File share.</span></span>
    
4.   <span data-ttu-id="5ab77-340">**How can I mount Azure file share on my local machine?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-340">**How can I mount Azure file share on my local machine?**</span></span> <span data-ttu-id="5ab77-341">You can mount the file share via the SMB protocol as long as port 445 (TCP Outbound) is open and your client supports the SMB 3.0 protocol (*e.g.*, Windows 8 or Windows Server 2012).</span><span class="sxs-lookup"><span data-stu-id="5ab77-341">You can mount the file share via the SMB protocol as long as port 445 (TCP Outbound) is open and your client supports the SMB 3.0 protocol (*e.g.*, Windows 8 or Windows Server 2012).</span></span> <span data-ttu-id="5ab77-342">Please work with your local ISP provider to unblock the port.</span><span class="sxs-lookup"><span data-stu-id="5ab77-342">Please work with your local ISP provider to unblock the port.</span></span> <span data-ttu-id="5ab77-343">In the interim, you can view your files using Storage Explorer or any other third party such as Cloudberry.</span><span class="sxs-lookup"><span data-stu-id="5ab77-343">In the interim, you can view your files using Storage Explorer or any other third party such as Cloudberry.</span></span>

5. <span data-ttu-id="5ab77-344">**Does the network traffic between an Azure virtual machine and a file share count as external bandwidth that is charged to the subscription?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-344">**Does the network traffic between an Azure virtual machine and a file share count as external bandwidth that is charged to the subscription?**</span></span>
   
    <span data-ttu-id="5ab77-345">If the file share and virtual machine are in different regions, the traffic between them will be charged as external bandwidth.</span><span class="sxs-lookup"><span data-stu-id="5ab77-345">If the file share and virtual machine are in different regions, the traffic between them will be charged as external bandwidth.</span></span>
6. <span data-ttu-id="5ab77-346">**If network traffic is between a virtual machine and a file share in the same region, is it free?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-346">**If network traffic is between a virtual machine and a file share in the same region, is it free?**</span></span>
   
    <span data-ttu-id="5ab77-347">Yes.</span><span class="sxs-lookup"><span data-stu-id="5ab77-347">Yes.</span></span> <span data-ttu-id="5ab77-348">It is free if the traffic is in the same region.</span><span class="sxs-lookup"><span data-stu-id="5ab77-348">It is free if the traffic is in the same region.</span></span>
7. <span data-ttu-id="5ab77-349">**Does connecting from on-premises virtual machines to Azure File Storage depend on Azure ExpressRoute?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-349">**Does connecting from on-premises virtual machines to Azure File Storage depend on Azure ExpressRoute?**</span></span>
   
    <span data-ttu-id="5ab77-350">No.</span><span class="sxs-lookup"><span data-stu-id="5ab77-350">No.</span></span> <span data-ttu-id="5ab77-351">If you don't have ExpressRoute, you can still access the file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span><span class="sxs-lookup"><span data-stu-id="5ab77-351">If you don't have ExpressRoute, you can still access the file share from on-premises as long as you have port 445 (TCP Outbound) open for Internet access.</span></span> <span data-ttu-id="5ab77-352">However, you can use ExpressRoute with File storage if you like.</span><span class="sxs-lookup"><span data-stu-id="5ab77-352">However, you can use ExpressRoute with File storage if you like.</span></span>
8. <span data-ttu-id="5ab77-353">**Is a "File Share Witness" for a failover cluster one of the use cases for Azure File Storage?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-353">**Is a "File Share Witness" for a failover cluster one of the use cases for Azure File Storage?**</span></span>
   
    <span data-ttu-id="5ab77-354">This is not supported currently.</span><span class="sxs-lookup"><span data-stu-id="5ab77-354">This is not supported currently.</span></span>
9. <span data-ttu-id="5ab77-355">**File storage is replicated only via LRS or GRS right now, right?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-355">**File storage is replicated only via LRS or GRS right now, right?**</span></span>  
   
    <span data-ttu-id="5ab77-356">We plan to support RA-GRS but there is no timeline to share yet.</span><span class="sxs-lookup"><span data-stu-id="5ab77-356">We plan to support RA-GRS but there is no timeline to share yet.</span></span>
10. <span data-ttu-id="5ab77-357">**When can I use existing storage accounts for Azure File Storage?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-357">**When can I use existing storage accounts for Azure File Storage?**</span></span>
   
    <span data-ttu-id="5ab77-358">Azure File Storage is now enabled for all storage accounts.</span><span class="sxs-lookup"><span data-stu-id="5ab77-358">Azure File Storage is now enabled for all storage accounts.</span></span>
11. <span data-ttu-id="5ab77-359">**Will a Rename operation also be added to the REST API?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-359">**Will a Rename operation also be added to the REST API?**</span></span>
   
    <span data-ttu-id="5ab77-360">Rename is not yet supported in our REST API.</span><span class="sxs-lookup"><span data-stu-id="5ab77-360">Rename is not yet supported in our REST API.</span></span>
12. <span data-ttu-id="5ab77-361">**Can you have nested shares, in other words, a share under a share?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-361">**Can you have nested shares, in other words, a share under a share?**</span></span>
    
    <span data-ttu-id="5ab77-362">No.</span><span class="sxs-lookup"><span data-stu-id="5ab77-362">No.</span></span> <span data-ttu-id="5ab77-363">The file share is the virtual driver that you can mount, so nested shares are not supported.</span><span class="sxs-lookup"><span data-stu-id="5ab77-363">The file share is the virtual driver that you can mount, so nested shares are not supported.</span></span>
13. <span data-ttu-id="5ab77-364">**Is it possible to specify read-only or write-only permissions on folders within the share?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-364">**Is it possible to specify read-only or write-only permissions on folders within the share?**</span></span>
    
    <span data-ttu-id="5ab77-365">You don't have this level of control over permissions if you mount the file share via SMB.</span><span class="sxs-lookup"><span data-stu-id="5ab77-365">You don't have this level of control over permissions if you mount the file share via SMB.</span></span> <span data-ttu-id="5ab77-366">However, you can achieve this by creating a shared access signature (SAS) via the REST API or client libraries.</span><span class="sxs-lookup"><span data-stu-id="5ab77-366">However, you can achieve this by creating a shared access signature (SAS) via the REST API or client libraries.</span></span>  
14. <span data-ttu-id="5ab77-367">**My performance was slow when trying to unzip files into in File storage. What should I do?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-367">**My performance was slow when trying to unzip files into in File storage. What should I do?**</span></span>
    
    <span data-ttu-id="5ab77-368">To transfer large numbers of files into File storage, we recommend that you use AzCopy, Azure Powershell (Windows), or the Azure CLI (Linux/Unix), as these tools have been optimized for network transfer.</span><span class="sxs-lookup"><span data-stu-id="5ab77-368">To transfer large numbers of files into File storage, we recommend that you use AzCopy, Azure Powershell (Windows), or the Azure CLI (Linux/Unix), as these tools have been optimized for network transfer.</span></span>
15. <span data-ttu-id="5ab77-369">**Patch released to fix slow-performance issue with Azure Files**</span><span class="sxs-lookup"><span data-stu-id="5ab77-369">**Patch released to fix slow-performance issue with Azure Files**</span></span>
    
    <span data-ttu-id="5ab77-370">The Windows team recently released a patch to fix a slow performance issue when the customer accesses Azure Files Storage from Windows 8.1 or Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="5ab77-370">The Windows team recently released a patch to fix a slow performance issue when the customer accesses Azure Files Storage from Windows 8.1 or Windows Server 2012 R2.</span></span> <span data-ttu-id="5ab77-371">For more information, please check out the associated KB article, [Slow performance when you access Azure Files Storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span><span class="sxs-lookup"><span data-stu-id="5ab77-371">For more information, please check out the associated KB article, [Slow performance when you access Azure Files Storage from Windows 8.1 or Server 2012 R2](https://support.microsoft.com/kb/3114025).</span></span>
16. <span data-ttu-id="5ab77-372">**Using Azure File Storage with IBM MQ**</span><span class="sxs-lookup"><span data-stu-id="5ab77-372">**Using Azure File Storage with IBM MQ**</span></span>
    
    <span data-ttu-id="5ab77-373">IBM has released a document to guide IBM MQ customers when configuring Azure File Storage with their service.</span><span class="sxs-lookup"><span data-stu-id="5ab77-373">IBM has released a document to guide IBM MQ customers when configuring Azure File Storage with their service.</span></span> <span data-ttu-id="5ab77-374">For more information, please check out [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span><span class="sxs-lookup"><span data-stu-id="5ab77-374">For more information, please check out [How to setup IBM MQ Multi instance queue manager with Microsoft Azure File Service](https://github.com/ibm-messaging/mq-azure/wiki/How-to-setup-IBM-MQ-Multi-instance-queue-manager-with-Microsoft-Azure-File-Service).</span></span>
17. <span data-ttu-id="5ab77-375">**How do I troubleshoot Azure File Storage errors?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-375">**How do I troubleshoot Azure File Storage errors?**</span></span>
    
    <span data-ttu-id="5ab77-376">You can refer to [Azure Files Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span><span class="sxs-lookup"><span data-stu-id="5ab77-376">You can refer to [Azure Files Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>               

18. <span data-ttu-id="5ab77-377">**How can I enable server side encryption for Azure Files?**</span><span class="sxs-lookup"><span data-stu-id="5ab77-377">**How can I enable server side encryption for Azure Files?**</span></span>
> [!NOTE]
> <span data-ttu-id="5ab77-378">[Server Side Encryption](storage-service-encryption.md) for Azure Files is currently in preview.</span><span class="sxs-lookup"><span data-stu-id="5ab77-378">[Server Side Encryption](storage-service-encryption.md) for Azure Files is currently in preview.</span></span> <span data-ttu-id="5ab77-379">You can contact [SSEDiscussion](mailto:ssediscussions@microsoft.com) if you have questions during the preview.</span><span class="sxs-lookup"><span data-stu-id="5ab77-379">You can contact [SSEDiscussion](mailto:ssediscussions@microsoft.com) if you have questions during the preview.</span></span>

    [Server Side Encryption](storage-service-encryption.md) for Azure Files is currently in preview. During preview, you can enable this feature only on new Azure Resource Manager storage accounts created by using the [Azure portal](https://portal.azure.com). There is no additional charge for enabling this feature. When you enable Storage Service Encryption for Azure File Storage, your data is automatically encrypted for you. 
    
    We plan to support enabling encryption for file storage with [Azure PowerShell](/powershell/resourcemanager/azurerm.storage/v2.7.0/azurerm.storage), [Azure CLI](storage-azure-cli.md), and the [Azure Storage Resource Provider REST API](/rest/api/storagerp/storageaccounts) in the future. 
    See [Storage Service Encryption](storage-service-encryption.md) for more information about encryption at rest in Azure Storage, and you can contact ssediscussions@microsoft.com if you have questions during the preview.

## <a name="next-steps"></a><span data-ttu-id="5ab77-380">Next steps</span><span class="sxs-lookup"><span data-stu-id="5ab77-380">Next steps</span></span>
<span data-ttu-id="5ab77-381">See these links for more information about Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="5ab77-381">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="5ab77-382">Conceptual articles and videos</span><span class="sxs-lookup"><span data-stu-id="5ab77-382">Conceptual articles and videos</span></span>
* [<span data-ttu-id="5ab77-383">Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux</span><span class="sxs-lookup"><span data-stu-id="5ab77-383">Azure Files Storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="5ab77-384">How to use Azure File Storage with Linux</span><span class="sxs-lookup"><span data-stu-id="5ab77-384">How to use Azure File Storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="5ab77-385">Tooling support for File storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-385">Tooling support for File storage</span></span>
* [<span data-ttu-id="5ab77-386">Using Azure PowerShell with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-386">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="5ab77-387">How to use AzCopy with Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-387">How to use AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="5ab77-388">Using the Azure CLI with Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-388">Using the Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="5ab77-389">Troubleshooting Azure File storage problems</span><span class="sxs-lookup"><span data-stu-id="5ab77-389">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="5ab77-390">Reference</span><span class="sxs-lookup"><span data-stu-id="5ab77-390">Reference</span></span>
* [<span data-ttu-id="5ab77-391">Storage Client Library for .NET reference</span><span class="sxs-lookup"><span data-stu-id="5ab77-391">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="5ab77-392">File Service REST API reference</span><span class="sxs-lookup"><span data-stu-id="5ab77-392">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="5ab77-393">Blog posts</span><span class="sxs-lookup"><span data-stu-id="5ab77-393">Blog posts</span></span>
* [<span data-ttu-id="5ab77-394">Azure File storage is now generally available</span><span class="sxs-lookup"><span data-stu-id="5ab77-394">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="5ab77-395">Inside Azure File Storage</span><span class="sxs-lookup"><span data-stu-id="5ab77-395">Inside Azure File Storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="5ab77-396">Introducing Microsoft Azure File Service</span><span class="sxs-lookup"><span data-stu-id="5ab77-396">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="5ab77-397">Persisting connections to Microsoft Azure Files</span><span class="sxs-lookup"><span data-stu-id="5ab77-397">Persisting connections to Microsoft Azure Files</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)













