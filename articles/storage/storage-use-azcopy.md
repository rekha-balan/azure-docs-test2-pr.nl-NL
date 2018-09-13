---
title: Copy or move data to Storage with AzCopy | Microsoft Docs
description: Use the AzCopy utility to move or copy data to or from blob, table, and file content. Copy data to Azure Storage from local files, or copy data within or between storage accounts. Easily migrate your data to Azure Storage.
services: storage
documentationcenter: ''
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: aa155738-7c69-4a83-94f8-b97af4461274
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: f703da63c4243c73cf68d3df9953f73d2462ac1c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549237"
---
# <a name="transfer-data-with-the-azcopy-command-line-utility"></a><span data-ttu-id="66dbb-105">Transfer data with the AzCopy Command-Line Utility</span><span class="sxs-lookup"><span data-stu-id="66dbb-105">Transfer data with the AzCopy Command-Line Utility</span></span>
## <a name="overview"></a><span data-ttu-id="66dbb-106">Overview</span><span class="sxs-lookup"><span data-stu-id="66dbb-106">Overview</span></span>
<span data-ttu-id="66dbb-107">AzCopy is a Windows command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span><span class="sxs-lookup"><span data-stu-id="66dbb-107">AzCopy is a Windows command-line utility designed for copying data to and from Microsoft Azure Blob, File, and Table storage using simple commands with optimal performance.</span></span> <span data-ttu-id="66dbb-108">You can copy data from one object to another within your storage account, or between storage accounts.</span><span class="sxs-lookup"><span data-stu-id="66dbb-108">You can copy data from one object to another within your storage account, or between storage accounts.</span></span>

> [!NOTE]
> <span data-ttu-id="66dbb-109">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="66dbb-109">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="66dbb-110">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation will be helpful.</span><span class="sxs-lookup"><span data-stu-id="66dbb-110">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation will be helpful.</span></span> <span data-ttu-id="66dbb-111">Most importantly, you will need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) in order to start using AzCopy.</span><span class="sxs-lookup"><span data-stu-id="66dbb-111">Most importantly, you will need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) in order to start using AzCopy.</span></span>
> 
> 

## <a name="download-and-install-azcopy"></a><span data-ttu-id="66dbb-112">Download and install AzCopy</span><span class="sxs-lookup"><span data-stu-id="66dbb-112">Download and install AzCopy</span></span>
### <a name="windows"></a><span data-ttu-id="66dbb-113">Windows</span><span class="sxs-lookup"><span data-stu-id="66dbb-113">Windows</span></span>
<span data-ttu-id="66dbb-114">Download the [latest version of AzCopy](http://aka.ms/downloadazcopy).</span><span class="sxs-lookup"><span data-stu-id="66dbb-114">Download the [latest version of AzCopy](http://aka.ms/downloadazcopy).</span></span>

### <a name="maclinux"></a><span data-ttu-id="66dbb-115">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="66dbb-115">Mac/Linux</span></span>
<span data-ttu-id="66dbb-116">AzCopy is not available for Mac/Linux OSs.</span><span class="sxs-lookup"><span data-stu-id="66dbb-116">AzCopy is not available for Mac/Linux OSs.</span></span> <span data-ttu-id="66dbb-117">However, Azure CLI is a suitable alternative for copying data to and from Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="66dbb-117">However, Azure CLI is a suitable alternative for copying data to and from Azure Storage.</span></span> <span data-ttu-id="66dbb-118">Read [Using the Azure CLI with Azure Storage](storage-azure-cli.md) to learn more.</span><span class="sxs-lookup"><span data-stu-id="66dbb-118">Read [Using the Azure CLI with Azure Storage](storage-azure-cli.md) to learn more.</span></span>

## <a name="writing-your-first-azcopy-command"></a><span data-ttu-id="66dbb-119">Writing your first AzCopy command</span><span class="sxs-lookup"><span data-stu-id="66dbb-119">Writing your first AzCopy command</span></span>
<span data-ttu-id="66dbb-120">The basic syntax for AzCopy commands is:</span><span class="sxs-lookup"><span data-stu-id="66dbb-120">The basic syntax for AzCopy commands is:</span></span>

```azcopy
AzCopy /Source:<source> /Dest:<destination> [Options]
```

<span data-ttu-id="66dbb-121">Open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span><span class="sxs-lookup"><span data-stu-id="66dbb-121">Open a command window and navigate to the AzCopy installation directory on your computer - where the `AzCopy.exe` executable is located.</span></span> <span data-ttu-id="66dbb-122">If desired, you can add the AzCopy installation location to your system path.</span><span class="sxs-lookup"><span data-stu-id="66dbb-122">If desired, you can add the AzCopy installation location to your system path.</span></span> <span data-ttu-id="66dbb-123">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-123">By default, AzCopy is installed to `%ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy` or `%ProgramFiles%\Microsoft SDKs\Azure\AzCopy`.</span></span>

<span data-ttu-id="66dbb-124">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span><span class="sxs-lookup"><span data-stu-id="66dbb-124">The following examples demonstrate a variety of scenarios for copying data to and from Microsoft Azure Blobs, Files, and Tables.</span></span> <span data-ttu-id="66dbb-125">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span><span class="sxs-lookup"><span data-stu-id="66dbb-125">Refer to the [AzCopy Parameters](#azcopy-parameters) section for a detailed explanation of the parameters used in each sample.</span></span>

## <a name="blob-download"></a><span data-ttu-id="66dbb-126">Blob: Download</span><span class="sxs-lookup"><span data-stu-id="66dbb-126">Blob: Download</span></span>
### <a name="download-single-blob"></a><span data-ttu-id="66dbb-127">Download single blob</span><span class="sxs-lookup"><span data-stu-id="66dbb-127">Download single blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="66dbb-128">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span><span class="sxs-lookup"><span data-stu-id="66dbb-128">Note that if the folder `C:\myfolder` does not exist, AzCopy will create it and download `abc.txt ` into the new folder.</span></span>

### <a name="download-single-blob-from-secondary-region"></a><span data-ttu-id="66dbb-129">Download single blob from secondary region</span><span class="sxs-lookup"><span data-stu-id="66dbb-129">Download single blob from secondary region</span></span>

```azcopy
AzCopy /Source:https://myaccount-secondary.blob.core.windows.net/mynewcontainer /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="66dbb-130">Note that you must have read-access geo-redundant storage enabled.</span><span class="sxs-lookup"><span data-stu-id="66dbb-130">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="download-all-blobs"></a><span data-ttu-id="66dbb-131">Download all blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-131">Download all blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="66dbb-132">Assume the following blobs reside in the specified container:</span><span class="sxs-lookup"><span data-stu-id="66dbb-132">Assume the following blobs reside in the specified container:</span></span>  

    abc.txt
    abc1.txt
    abc2.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="66dbb-133">After the download operation, the directory `C:\myfolder` will include the following files:</span><span class="sxs-lookup"><span data-stu-id="66dbb-133">After the download operation, the directory `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\vd1\a.txt
    C:\myfolder\vd1\abcd.txt

<span data-ttu-id="66dbb-134">If you do not specify option `/S`, no blobs will be downloaded.</span><span class="sxs-lookup"><span data-stu-id="66dbb-134">If you do not specify option `/S`, no blobs will be downloaded.</span></span>

### <a name="download-blobs-with-specified-prefix"></a><span data-ttu-id="66dbb-135">Download blobs with specified prefix</span><span class="sxs-lookup"><span data-stu-id="66dbb-135">Download blobs with specified prefix</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /Pattern:a /S
```

<span data-ttu-id="66dbb-136">Assume the following blobs reside in the specified container.</span><span class="sxs-lookup"><span data-stu-id="66dbb-136">Assume the following blobs reside in the specified container.</span></span> <span data-ttu-id="66dbb-137">All blobs beginning with the prefix `a` will be downloaded:</span><span class="sxs-lookup"><span data-stu-id="66dbb-137">All blobs beginning with the prefix `a` will be downloaded:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    xyz.txt
    vd1\a.txt
    vd1\abcd.txt

<span data-ttu-id="66dbb-138">After the download operation, the folder `C:\myfolder` will include the following files:</span><span class="sxs-lookup"><span data-stu-id="66dbb-138">After the download operation, the folder `C:\myfolder` will include the following files:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

<span data-ttu-id="66dbb-139">The prefix applies to the virtual directory, which forms the first part of the blob name.</span><span class="sxs-lookup"><span data-stu-id="66dbb-139">The prefix applies to the virtual directory, which forms the first part of the blob name.</span></span> <span data-ttu-id="66dbb-140">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span><span class="sxs-lookup"><span data-stu-id="66dbb-140">In the example shown above, the virtual directory does not match the specified prefix, so it is not downloaded.</span></span> <span data-ttu-id="66dbb-141">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span><span class="sxs-lookup"><span data-stu-id="66dbb-141">In addition, if the option `\S` is not specified, AzCopy will not download any blobs.</span></span>

### <a name="set-the-last-modified-time-of-exported-files-to-be-same-as-the-source-blobs"></a><span data-ttu-id="66dbb-142">Set the last-modified time of exported files to be same as the source blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-142">Set the last-modified time of exported files to be same as the source blobs</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT
```

<span data-ttu-id="66dbb-143">You can also exclude blobs from the download operation based on their last-modified time.</span><span class="sxs-lookup"><span data-stu-id="66dbb-143">You can also exclude blobs from the download operation based on their last-modified time.</span></span> <span data-ttu-id="66dbb-144">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span><span class="sxs-lookup"><span data-stu-id="66dbb-144">For example, if you want to exclude blobs whose last modified time is the same or newer than the destination file, add the `/XN` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XN
```

<span data-ttu-id="66dbb-145">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span><span class="sxs-lookup"><span data-stu-id="66dbb-145">Or if you want to exclude blobs whose last modified time is the same or older than the destination file, add the `/XO` option:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:key /MT /XO
```

## <a name="blob-upload"></a><span data-ttu-id="66dbb-146">Blob: Upload</span><span class="sxs-lookup"><span data-stu-id="66dbb-146">Blob: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="66dbb-147">Upload single file</span><span class="sxs-lookup"><span data-stu-id="66dbb-147">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:"abc.txt"
```

<span data-ttu-id="66dbb-148">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span><span class="sxs-lookup"><span data-stu-id="66dbb-148">If the specified destination container does not exist, AzCopy will create it and upload the file into it.</span></span>

### <a name="upload-single-file-to-virtual-directory"></a><span data-ttu-id="66dbb-149">Upload single file to virtual directory</span><span class="sxs-lookup"><span data-stu-id="66dbb-149">Upload single file to virtual directory</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer/vd /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="66dbb-150">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span><span class="sxs-lookup"><span data-stu-id="66dbb-150">If the specified virtual directory does not exist, AzCopy will upload the file to include the virtual directory in its name (*e.g.*, `vd/abc.txt` in the example above).</span></span>

### <a name="upload-all-files"></a><span data-ttu-id="66dbb-151">Upload all files</span><span class="sxs-lookup"><span data-stu-id="66dbb-151">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /S
```

<span data-ttu-id="66dbb-152">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span><span class="sxs-lookup"><span data-stu-id="66dbb-152">Specifying option `/S` uploads the contents of the specified directory to Blob storage recursively, meaning that all subfolders and their files will be uploaded as well.</span></span> <span data-ttu-id="66dbb-153">For instance, assume the following files reside in folder `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="66dbb-153">For instance, assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="66dbb-154">After the upload operation, the container will include the following files:</span><span class="sxs-lookup"><span data-stu-id="66dbb-154">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="66dbb-155">If you do not specify option `/S`, AzCopy will not upload recursively.</span><span class="sxs-lookup"><span data-stu-id="66dbb-155">If you do not specify option `/S`, AzCopy will not upload recursively.</span></span> <span data-ttu-id="66dbb-156">After the upload operation, the container will include the following files:</span><span class="sxs-lookup"><span data-stu-id="66dbb-156">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="66dbb-157">Upload files matching specified pattern</span><span class="sxs-lookup"><span data-stu-id="66dbb-157">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Pattern:a* /S
```

<span data-ttu-id="66dbb-158">Assume the following files reside in folder `C:\myfolder`:</span><span class="sxs-lookup"><span data-stu-id="66dbb-158">Assume the following files reside in folder `C:\myfolder`:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt
    C:\myfolder\xyz.txt
    C:\myfolder\subfolder\a.txt
    C:\myfolder\subfolder\abcd.txt

<span data-ttu-id="66dbb-159">After the upload operation, the container will include the following files:</span><span class="sxs-lookup"><span data-stu-id="66dbb-159">After the upload operation, the container will include the following files:</span></span>

    abc.txt
    abc1.txt
    abc2.txt
    subfolder\a.txt
    subfolder\abcd.txt

<span data-ttu-id="66dbb-160">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span><span class="sxs-lookup"><span data-stu-id="66dbb-160">If you do not specify option `/S`, AzCopy will only upload blobs that don't reside in a virtual directory:</span></span>

    C:\myfolder\abc.txt
    C:\myfolder\abc1.txt
    C:\myfolder\abc2.txt

### <a name="specify-the-mime-content-type-of-a-destination-blob"></a><span data-ttu-id="66dbb-161">Specify the MIME content type of a destination blob</span><span class="sxs-lookup"><span data-stu-id="66dbb-161">Specify the MIME content type of a destination blob</span></span>
<span data-ttu-id="66dbb-162">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-162">By default, AzCopy sets the content type of a destination blob to `application/octet-stream`.</span></span> <span data-ttu-id="66dbb-163">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-163">Beginning with version 3.1.0, you can explicitly specify the content type via the option `/SetContentType:[content-type]`.</span></span> <span data-ttu-id="66dbb-164">This syntax sets the content type for all blobs in an upload operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-164">This syntax sets the content type for all blobs in an upload operation.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType:video/mp4
```

<span data-ttu-id="66dbb-165">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span><span class="sxs-lookup"><span data-stu-id="66dbb-165">If you specify `/SetContentType` without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.blob.core.windows.net/myContainer/ /DestKey:key /Pattern:ab /SetContentType
```

## <a name="blob-copy"></a><span data-ttu-id="66dbb-166">Blob: Copy</span><span class="sxs-lookup"><span data-stu-id="66dbb-166">Blob: Copy</span></span>
### <a name="copy-single-blob-within-storage-account"></a><span data-ttu-id="66dbb-167">Copy single blob within Storage account</span><span class="sxs-lookup"><span data-stu-id="66dbb-167">Copy single blob within Storage account</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceKey:key /DestKey:key /Pattern:abc.txt
```

<span data-ttu-id="66dbb-168">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-168">When you copy a blob within a Storage account, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-across-storage-accounts"></a><span data-ttu-id="66dbb-169">Copy single blob across Storage accounts</span><span class="sxs-lookup"><span data-stu-id="66dbb-169">Copy single blob across Storage accounts</span></span>

```azcopy
AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="66dbb-170">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-170">When you copy a blob across Storage accounts, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-single-blob-from-secondary-region-to-primary-region"></a><span data-ttu-id="66dbb-171">Copy single blob from secondary region to primary region</span><span class="sxs-lookup"><span data-stu-id="66dbb-171">Copy single blob from secondary region to primary region</span></span>

```azcopy
AzCopy /Source:https://myaccount1-secondary.blob.core.windows.net/mynewcontainer1 /Dest:https://myaccount2.blob.core.windows.net/mynewcontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt
```

<span data-ttu-id="66dbb-172">Note that you must have read-access geo-redundant storage enabled.</span><span class="sxs-lookup"><span data-stu-id="66dbb-172">Note that you must have read-access geo-redundant storage enabled.</span></span>

### <a name="copy-single-blob-and-its-snapshots-across-storage-accounts"></a><span data-ttu-id="66dbb-173">Copy single blob and its snapshots across Storage accounts</span><span class="sxs-lookup"><span data-stu-id="66dbb-173">Copy single blob and its snapshots across Storage accounts</span></span>

```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /SourceKey:key1 /DestKey:key2 /Pattern:abc.txt /Snapshot
```

<span data-ttu-id="66dbb-174">After the copy operation, the target container will include the blob and its snapshots.</span><span class="sxs-lookup"><span data-stu-id="66dbb-174">After the copy operation, the target container will include the blob and its snapshots.</span></span> <span data-ttu-id="66dbb-175">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span><span class="sxs-lookup"><span data-stu-id="66dbb-175">Assuming the blob in the example above has two snapshots, the container will include the following blob and snapshots:</span></span>

    abc.txt
    abc (2013-02-25 080757).txt
    abc (2014-02-21 150331).txt

### <a name="synchronously-copy-blobs-across-storage-accounts"></a><span data-ttu-id="66dbb-176">Synchronously copy blobs across Storage accounts</span><span class="sxs-lookup"><span data-stu-id="66dbb-176">Synchronously copy blobs across Storage accounts</span></span>
<span data-ttu-id="66dbb-177">AzCopy by default copies data between two storage endpoints asynchronously.</span><span class="sxs-lookup"><span data-stu-id="66dbb-177">AzCopy by default copies data between two storage endpoints asynchronously.</span></span> <span data-ttu-id="66dbb-178">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-178">Therefore, the copy operation will run in the background using spare bandwidth capacity that has no SLA in terms of how fast a blob will be copied, and AzCopy will periodically check the copy status until the copying is completed or failed.</span></span>

<span data-ttu-id="66dbb-179">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-179">The `/SyncCopy` option ensures that the copy operation will get consistent speed.</span></span> <span data-ttu-id="66dbb-180">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span><span class="sxs-lookup"><span data-stu-id="66dbb-180">AzCopy performs the synchronous copy by downloading the blobs to copy from the specified source to local memory, and then uploading them to the Blob storage destination.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/myContainer/ /Dest:https://myaccount2.blob.core.windows.net/myContainer/ /SourceKey:key1 /DestKey:key2 /Pattern:ab /SyncCopy
```

<span data-ttu-id="66dbb-181">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span><span class="sxs-lookup"><span data-stu-id="66dbb-181">`/SyncCopy` might generate additional egress cost compared to asynchronous copy, the recommended approach is to use this option in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="file-download"></a><span data-ttu-id="66dbb-182">File: Download</span><span class="sxs-lookup"><span data-stu-id="66dbb-182">File: Download</span></span>
### <a name="download-single-file"></a><span data-ttu-id="66dbb-183">Download single file</span><span class="sxs-lookup"><span data-stu-id="66dbb-183">Download single file</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/myfolder1/ /Dest:C:\myfolder /SourceKey:key /Pattern:abc.txt
```

<span data-ttu-id="66dbb-184">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span><span class="sxs-lookup"><span data-stu-id="66dbb-184">If the specified source is an Azure file share, then you must either specify the exact file name, (*e.g.* `abc.txt`) to download a single file, or specify option `/S` to download all files in the share recursively.</span></span> <span data-ttu-id="66dbb-185">Attempting to specify both a file pattern and option `/S` together will result in an error.</span><span class="sxs-lookup"><span data-stu-id="66dbb-185">Attempting to specify both a file pattern and option `/S` together will result in an error.</span></span>

### <a name="download-all-files"></a><span data-ttu-id="66dbb-186">Download all files</span><span class="sxs-lookup"><span data-stu-id="66dbb-186">Download all files</span></span>

```azcopy
AzCopy /Source:https://myaccount.file.core.windows.net/myfileshare/ /Dest:C:\myfolder /SourceKey:key /S
```

<span data-ttu-id="66dbb-187">Note that any empty folders will not be downloaded.</span><span class="sxs-lookup"><span data-stu-id="66dbb-187">Note that any empty folders will not be downloaded.</span></span>

## <a name="file-upload"></a><span data-ttu-id="66dbb-188">File: Upload</span><span class="sxs-lookup"><span data-stu-id="66dbb-188">File: Upload</span></span>
### <a name="upload-single-file"></a><span data-ttu-id="66dbb-189">Upload single file</span><span class="sxs-lookup"><span data-stu-id="66dbb-189">Upload single file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:abc.txt
```

### <a name="upload-all-files"></a><span data-ttu-id="66dbb-190">Upload all files</span><span class="sxs-lookup"><span data-stu-id="66dbb-190">Upload all files</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /S
```

<span data-ttu-id="66dbb-191">Note that any empty folders will not be uploaded.</span><span class="sxs-lookup"><span data-stu-id="66dbb-191">Note that any empty folders will not be uploaded.</span></span>

### <a name="upload-files-matching-specified-pattern"></a><span data-ttu-id="66dbb-192">Upload files matching specified pattern</span><span class="sxs-lookup"><span data-stu-id="66dbb-192">Upload files matching specified pattern</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.file.core.windows.net/myfileshare/ /DestKey:key /Pattern:ab* /S
```

## <a name="file-copy"></a><span data-ttu-id="66dbb-193">File: Copy</span><span class="sxs-lookup"><span data-stu-id="66dbb-193">File: Copy</span></span>
### <a name="copy-across-file-shares"></a><span data-ttu-id="66dbb-194">Copy across file shares</span><span class="sxs-lookup"><span data-stu-id="66dbb-194">Copy across file shares</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="66dbb-195">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-195">When you copy a file across file shares, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="copy-from-file-share-to-blob"></a><span data-ttu-id="66dbb-196">Copy from file share to blob</span><span class="sxs-lookup"><span data-stu-id="66dbb-196">Copy from file share to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare/ /Dest:https://myaccount2.blob.core.windows.net/mycontainer/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="66dbb-197">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-197">When you copy a file from file share to blob, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>


### <a name="copy-from-blob-to-file-share"></a><span data-ttu-id="66dbb-198">Copy from blob to file share</span><span class="sxs-lookup"><span data-stu-id="66dbb-198">Copy from blob to file share</span></span>

```azcopy
AzCopy /Source:https://myaccount1.blob.core.windows.net/mycontainer/ /Dest:https://myaccount2.file.core.windows.net/myfileshare/ /SourceKey:key1 /DestKey:key2 /S
```
<span data-ttu-id="66dbb-199">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span><span class="sxs-lookup"><span data-stu-id="66dbb-199">When you copy a file from blob to file share, a [server-side copy](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-asynchronous-cross-account-copy-blob.aspx) operation is performed.</span></span>

### <a name="synchronously-copy-files"></a><span data-ttu-id="66dbb-200">Synchronously copy files</span><span class="sxs-lookup"><span data-stu-id="66dbb-200">Synchronously copy files</span></span>
<span data-ttu-id="66dbb-201">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span><span class="sxs-lookup"><span data-stu-id="66dbb-201">You can specify the `/SyncCopy` option to copy data from File Storage to File Storage, from File Storage to Blob Storage and from Blob Storage to File Storage synchronously, AzCopy does this by downloading the source data to local memory and upload it again to destination.</span></span> <span data-ttu-id="66dbb-202">Standard egress cost will apply.</span><span class="sxs-lookup"><span data-stu-id="66dbb-202">Standard egress cost will apply.</span></span>

```azcopy
AzCopy /Source:https://myaccount1.file.core.windows.net/myfileshare1/ /Dest:https://myaccount2.file.core.windows.net/myfileshare2/ /SourceKey:key1 /DestKey:key2 /S /SyncCopy
```

<span data-ttu-id="66dbb-203">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span><span class="sxs-lookup"><span data-stu-id="66dbb-203">When copying from File Storage to Blob Storage, the default blob type is block blob, user can specify option `/BlobType:page` to change the destination blob type.</span></span>

<span data-ttu-id="66dbb-204">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span><span class="sxs-lookup"><span data-stu-id="66dbb-204">Note that `/SyncCopy` might generate additional egress cost comparing to asynchronous copy, the recommended approach is to use this option in the Azure VM which is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="table-export"></a><span data-ttu-id="66dbb-205">Table: Export</span><span class="sxs-lookup"><span data-stu-id="66dbb-205">Table: Export</span></span>
### <a name="export-table"></a><span data-ttu-id="66dbb-206">Export table</span><span class="sxs-lookup"><span data-stu-id="66dbb-206">Export table</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key
```

<span data-ttu-id="66dbb-207">AzCopy writes a manifest file to the specified destination folder.</span><span class="sxs-lookup"><span data-stu-id="66dbb-207">AzCopy writes a manifest file to the specified destination folder.</span></span> <span data-ttu-id="66dbb-208">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-208">The manifest file is used in the import process to locate the necessary data files and perform data validation.</span></span> <span data-ttu-id="66dbb-209">The manifest file uses the following naming convention by default:</span><span class="sxs-lookup"><span data-stu-id="66dbb-209">The manifest file uses the following naming convention by default:</span></span>

    <account name>_<table name>_<timestamp>.manifest

<span data-ttu-id="66dbb-210">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span><span class="sxs-lookup"><span data-stu-id="66dbb-210">User can also specify the option `/Manifest:<manifest file name>` to set the manifest file name.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /Manifest:abc.manifest
```

### <a name="split-export-into-multiple-files"></a><span data-ttu-id="66dbb-211">Split export into multiple files</span><span class="sxs-lookup"><span data-stu-id="66dbb-211">Split export into multiple files</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/mytable/ /Dest:C:\myfolder /SourceKey:key /S /SplitSize:100
```

<span data-ttu-id="66dbb-212">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-212">AzCopy uses a *volume index* in the split data file names to distinguish multiple files.</span></span> <span data-ttu-id="66dbb-213">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span><span class="sxs-lookup"><span data-stu-id="66dbb-213">The volume index consists of two parts, a *partition key range index* and a *split file index*.</span></span> <span data-ttu-id="66dbb-214">Both indexes are zero-based.</span><span class="sxs-lookup"><span data-stu-id="66dbb-214">Both indexes are zero-based.</span></span>

<span data-ttu-id="66dbb-215">The partition key range index will be 0 if user does not specify option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-215">The partition key range index will be 0 if user does not specify option `/PKRS`.</span></span>

<span data-ttu-id="66dbb-216">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-216">For instance, suppose AzCopy generates two data files after the user specifies option `/SplitSize`.</span></span> <span data-ttu-id="66dbb-217">The resulting data file names might be:</span><span class="sxs-lookup"><span data-stu-id="66dbb-217">The resulting data file names might be:</span></span>

    myaccount_mytable_20140903T051850.8128447Z_0_0_C3040FE8.json
    myaccount_mytable_20140903T051850.8128447Z_0_1_0AB9AC20.json

<span data-ttu-id="66dbb-218">Note that the minimum possible value for option `/SplitSize` is 32MB.</span><span class="sxs-lookup"><span data-stu-id="66dbb-218">Note that the minimum possible value for option `/SplitSize` is 32MB.</span></span> <span data-ttu-id="66dbb-219">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span><span class="sxs-lookup"><span data-stu-id="66dbb-219">If the specified destination is Blob storage, AzCopy will split the data file once its sizes reaches the blob size limitation (200GB), regardless of whether option `/SplitSize` has been specified by the user.</span></span>

### <a name="export-table-to-json-or-csv-data-file-format"></a><span data-ttu-id="66dbb-220">Export table to JSON or CSV data file format</span><span class="sxs-lookup"><span data-stu-id="66dbb-220">Export table to JSON or CSV data file format</span></span>
<span data-ttu-id="66dbb-221">AzCopy by default exports tables to JSON data files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-221">AzCopy by default exports tables to JSON data files.</span></span> <span data-ttu-id="66dbb-222">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span><span class="sxs-lookup"><span data-stu-id="66dbb-222">You can specify the option `/PayloadFormat:JSON|CSV` to export the tables as JSON or CSV.</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PayloadFormat:CSV
```

<span data-ttu-id="66dbb-223">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-223">When specifying the CSV payload format, AzCopy will also generate a schema file with file extension `.schema.csv` for each data file.</span></span>

### <a name="export-table-entities-concurrently"></a><span data-ttu-id="66dbb-224">Export table entities concurrently</span><span class="sxs-lookup"><span data-stu-id="66dbb-224">Export table entities concurrently</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:C:\myfolder\ /SourceKey:key /PKRS:"aa#bb"
```

<span data-ttu-id="66dbb-225">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-225">AzCopy will start concurrent operations to export entities when the user specifies option `/PKRS`.</span></span> <span data-ttu-id="66dbb-226">Each operation exports one partition key range.</span><span class="sxs-lookup"><span data-stu-id="66dbb-226">Each operation exports one partition key range.</span></span>

<span data-ttu-id="66dbb-227">Note that the number of concurrent operations is also controlled by option `/NC`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-227">Note that the number of concurrent operations is also controlled by option `/NC`.</span></span> <span data-ttu-id="66dbb-228">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span><span class="sxs-lookup"><span data-stu-id="66dbb-228">AzCopy uses the number of core processors as the default value of `/NC` when copying table entities, even if `/NC` was not specified.</span></span> <span data-ttu-id="66dbb-229">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span><span class="sxs-lookup"><span data-stu-id="66dbb-229">When the user specifies option `/PKRS`, AzCopy uses the smaller of the two values - partition key ranges versus implicitly or explicitly specified concurrent operations - to determine the number of concurrent operations to start.</span></span> <span data-ttu-id="66dbb-230">For more details, type `AzCopy /?:NC` at the command line.</span><span class="sxs-lookup"><span data-stu-id="66dbb-230">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="export-table-to-blob"></a><span data-ttu-id="66dbb-231">Export table to blob</span><span class="sxs-lookup"><span data-stu-id="66dbb-231">Export table to blob</span></span>

```azcopy
AzCopy /Source:https://myaccount.table.core.windows.net/myTable/ /Dest:https://myaccount.blob.core.windows.net/mycontainer/ /SourceKey:key1 /Destkey:key2
```

<span data-ttu-id="66dbb-232">AzCopy will generate a JSON data file into the blob container with following naming convention:</span><span class="sxs-lookup"><span data-stu-id="66dbb-232">AzCopy will generate a JSON data file into the blob container with following naming convention:</span></span>

    <account name>_<table name>_<timestamp>_<volume index>_<CRC>.json

<span data-ttu-id="66dbb-233">The generated JSON data file follows the payload format for minimal metadata.</span><span class="sxs-lookup"><span data-stu-id="66dbb-233">The generated JSON data file follows the payload format for minimal metadata.</span></span> <span data-ttu-id="66dbb-234">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span><span class="sxs-lookup"><span data-stu-id="66dbb-234">For details on this payload format, see [Payload Format for Table Service Operations](http://msdn.microsoft.com/library/azure/dn535600.aspx).</span></span>

<span data-ttu-id="66dbb-235">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-235">Note that when exporting tables to blobs, AzCopy will download the Table entities to local temporary data files and then upload those entities to the blob.</span></span> <span data-ttu-id="66dbb-236">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span><span class="sxs-lookup"><span data-stu-id="66dbb-236">These temporary data files are put into the journal file folder with the default path "<code>%LocalAppData%\Microsoft\Azure\AzCopy</code>", you can specify option /Z:[journal-file-folder] to change the journal file folder location and thus change the temporary data files location.</span></span> <span data-ttu-id="66dbb-237">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span><span class="sxs-lookup"><span data-stu-id="66dbb-237">The temporary data files' size is decided by your table entities' size and the size you specified with the option /SplitSize, although the temporary data file in local disk will be deleted instantly once it has been uploaded to the blob, please make sure you have enough local disk space to store these temporary data files before they are deleted.</span></span>

## <a name="table-import"></a><span data-ttu-id="66dbb-238">Table: Import</span><span class="sxs-lookup"><span data-stu-id="66dbb-238">Table: Import</span></span>
### <a name="import-table"></a><span data-ttu-id="66dbb-239">Import table</span><span class="sxs-lookup"><span data-stu-id="66dbb-239">Import table</span></span>

```azcopy
AzCopy /Source:C:\myfolder\ /Dest:https://myaccount.table.core.windows.net/mytable1/ /DestKey:key /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:InsertOrReplace
```

<span data-ttu-id="66dbb-240">The option `/EntityOperation` indicates how to insert entities into the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-240">The option `/EntityOperation` indicates how to insert entities into the table.</span></span> <span data-ttu-id="66dbb-241">Possible values are:</span><span class="sxs-lookup"><span data-stu-id="66dbb-241">Possible values are:</span></span>

* <span data-ttu-id="66dbb-242">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-242">`InsertOrSkip`: Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="66dbb-243">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-243">`InsertOrMerge`: Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="66dbb-244">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-244">`InsertOrReplace`: Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="66dbb-245">Note that you cannot specify option `/PKRS` in the import scenario.</span><span class="sxs-lookup"><span data-stu-id="66dbb-245">Note that you cannot specify option `/PKRS` in the import scenario.</span></span> <span data-ttu-id="66dbb-246">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-246">Unlike the export scenario, in which you must specify option `/PKRS` to start concurrent operations, AzCopy will by default start concurrent operations when you import a table.</span></span> <span data-ttu-id="66dbb-247">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-247">The default number of concurrent operations started is equal to the number of core processors; however, you can specify a different number of concurrent with option `/NC`.</span></span> <span data-ttu-id="66dbb-248">For more details, type `AzCopy /?:NC` at the command line.</span><span class="sxs-lookup"><span data-stu-id="66dbb-248">For more details, type `AzCopy /?:NC` at the command line.</span></span>

<span data-ttu-id="66dbb-249">Note that AzCopy only supports importing for JSON, not CSV.</span><span class="sxs-lookup"><span data-stu-id="66dbb-249">Note that AzCopy only supports importing for JSON, not CSV.</span></span> <span data-ttu-id="66dbb-250">AzCopy does not support table imports from user-created JSON and manifest files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-250">AzCopy does not support table imports from user-created JSON and manifest files.</span></span> <span data-ttu-id="66dbb-251">Both of these files must come from an AzCopy table export.</span><span class="sxs-lookup"><span data-stu-id="66dbb-251">Both of these files must come from an AzCopy table export.</span></span> <span data-ttu-id="66dbb-252">To avoid errors, please do not modify the exported JSON or manifest file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-252">To avoid errors, please do not modify the exported JSON or manifest file.</span></span>

### <a name="import-entities-to-table-using-blobs"></a><span data-ttu-id="66dbb-253">Import entities to table using blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-253">Import entities to table using blobs</span></span>
<span data-ttu-id="66dbb-254">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-254">Assume a Blob container contains the following: A JSON file representing an Azure Table and its accompanying manifest file.</span></span>

    myaccount_mytable_20140103T112020.manifest
    myaccount_mytable_20140103T112020_0_0_0AF395F1DC42E952.json

<span data-ttu-id="66dbb-255">You can run the following command to import entities into a table using the manifest file in that blob container:</span><span class="sxs-lookup"><span data-stu-id="66dbb-255">You can run the following command to import entities into a table using the manifest file in that blob container:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer /Dest:https://myaccount.table.core.windows.net/mytable /SourceKey:key1 /DestKey:key2 /Manifest:"myaccount_mytable_20140103T112020.manifest" /EntityOperation:"InsertOrReplace"
```

## <a name="other-azcopy-features"></a><span data-ttu-id="66dbb-256">Other AzCopy features</span><span class="sxs-lookup"><span data-stu-id="66dbb-256">Other AzCopy features</span></span>
### <a name="only-copy-data-that-doesnt-exist-in-the-destination"></a><span data-ttu-id="66dbb-257">Only copy data that doesn't exist in the destination</span><span class="sxs-lookup"><span data-stu-id="66dbb-257">Only copy data that doesn't exist in the destination</span></span>
<span data-ttu-id="66dbb-258">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span><span class="sxs-lookup"><span data-stu-id="66dbb-258">The `/XO` and `/XN` parameters allow you to exclude older or newer source resources from being copied, respectively.</span></span> <span data-ttu-id="66dbb-259">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span><span class="sxs-lookup"><span data-stu-id="66dbb-259">If you only want to copy source resources that don't exist in the destination, you can specify both parameters in the AzCopy command:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /XO /XN

    /Source:C:\myfolder /Dest:http://myaccount.file.core.windows.net/myfileshare /DestKey:<destkey> /S /XO /XN

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:http://myaccount.blob.core.windows.net/mycontainer1 /SourceKey:<sourcekey> /DestKey:<destkey> /S /XO /XN

<span data-ttu-id="66dbb-260">Note that this is not supported when either the source or destination is a table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-260">Note that this is not supported when either the source or destination is a table.</span></span>

### <a name="use-a-response-file-to-specify-command-line-parameters"></a><span data-ttu-id="66dbb-261">Use a response file to specify command-line parameters</span><span class="sxs-lookup"><span data-stu-id="66dbb-261">Use a response file to specify command-line parameters</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\copyoperation.txt"
```

<span data-ttu-id="66dbb-262">You can include any AzCopy command-line parameters in a response file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-262">You can include any AzCopy command-line parameters in a response file.</span></span> <span data-ttu-id="66dbb-263">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-263">AzCopy processes the parameters in the file as if they had been specified on the command line, performing a direct substitution with the contents of the file.</span></span>

<span data-ttu-id="66dbb-264">Assume a response file named `copyoperation.txt`, that contains the following lines.</span><span class="sxs-lookup"><span data-stu-id="66dbb-264">Assume a response file named `copyoperation.txt`, that contains the following lines.</span></span> <span data-ttu-id="66dbb-265">Each AzCopy parameter can be specified on a single line</span><span class="sxs-lookup"><span data-stu-id="66dbb-265">Each AzCopy parameter can be specified on a single line</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y

<span data-ttu-id="66dbb-266">or on separate lines:</span><span class="sxs-lookup"><span data-stu-id="66dbb-266">or on separate lines:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer
    /Dest:C:\myfolder
    /SourceKey:<sourcekey>
    /S
    /Y

<span data-ttu-id="66dbb-267">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span><span class="sxs-lookup"><span data-stu-id="66dbb-267">AzCopy will fail if you split the parameter across two lines, as shown here for the `/sourcekey` parameter:</span></span>

    http://myaccount.blob.core.windows.net/mycontainer
     C:\myfolder
    /sourcekey:
    <sourcekey>
    /S
    /Y

### <a name="use-multiple-response-files-to-specify-command-line-parameters"></a><span data-ttu-id="66dbb-268">Use multiple response files to specify command-line parameters</span><span class="sxs-lookup"><span data-stu-id="66dbb-268">Use multiple response files to specify command-line parameters</span></span>
<span data-ttu-id="66dbb-269">Assume a response file named `source.txt` that specifies a source container:</span><span class="sxs-lookup"><span data-stu-id="66dbb-269">Assume a response file named `source.txt` that specifies a source container:</span></span>

    /Source:http://myaccount.blob.core.windows.net/mycontainer

<span data-ttu-id="66dbb-270">And a response file named `dest.txt` that specifies a destination folder in the file system:</span><span class="sxs-lookup"><span data-stu-id="66dbb-270">And a response file named `dest.txt` that specifies a destination folder in the file system:</span></span>

    /Dest:C:\myfolder

<span data-ttu-id="66dbb-271">And a response file named `options.txt` that specifies options for AzCopy:</span><span class="sxs-lookup"><span data-stu-id="66dbb-271">And a response file named `options.txt` that specifies options for AzCopy:</span></span>

    /S /Y

<span data-ttu-id="66dbb-272">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span><span class="sxs-lookup"><span data-stu-id="66dbb-272">To call AzCopy with these response files, all of which reside in a directory `C:\responsefiles`, use this command:</span></span>

```azcopy
AzCopy /@:"C:\responsefiles\source.txt" /@:"C:\responsefiles\dest.txt" /SourceKey:<sourcekey> /@:"C:\responsefiles\options.txt"   
```

<span data-ttu-id="66dbb-273">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span><span class="sxs-lookup"><span data-stu-id="66dbb-273">AzCopy processes this command just as it would if you included all of the individual parameters on the command line:</span></span>

```azcopy
AzCopy /Source:http://myaccount.blob.core.windows.net/mycontainer /Dest:C:\myfolder /SourceKey:<sourcekey> /S /Y
```

### <a name="specify-a-shared-access-signature-sas"></a><span data-ttu-id="66dbb-274">Specify a shared access signature (SAS)</span><span class="sxs-lookup"><span data-stu-id="66dbb-274">Specify a shared access signature (SAS)</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1 /Dest:https://myaccount.blob.core.windows.net/mycontainer2 /SourceSAS:SAS1 /DestSAS:SAS2 /Pattern:abc.txt
```

<span data-ttu-id="66dbb-275">You can also specify a SAS on the container URI:</span><span class="sxs-lookup"><span data-stu-id="66dbb-275">You can also specify a SAS on the container URI:</span></span>

```azcopy
AzCopy /Source:https://myaccount.blob.core.windows.net/mycontainer1/?SourceSASToken /Dest:C:\myfolder /S
```

### <a name="journal-file-folder"></a><span data-ttu-id="66dbb-276">Journal file folder</span><span class="sxs-lookup"><span data-stu-id="66dbb-276">Journal file folder</span></span>
<span data-ttu-id="66dbb-277">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-277">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="66dbb-278">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-278">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="66dbb-279">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-279">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="66dbb-280">If the two command lines match, AzCopy resumes the incomplete operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-280">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="66dbb-281">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-281">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="66dbb-282">If you want to use the default location for the journal file:</span><span class="sxs-lookup"><span data-stu-id="66dbb-282">If you want to use the default location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z
```

<span data-ttu-id="66dbb-283">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-283">If you omit option `/Z`, or specify option `/Z` without the folder path, as shown above, AzCopy creates the journal file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="66dbb-284">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-284">If the journal file already exists, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="66dbb-285">If you want to specify a custom location for the journal file:</span><span class="sxs-lookup"><span data-stu-id="66dbb-285">If you want to specify a custom location for the journal file:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /Z:C:\journalfolder\
```

<span data-ttu-id="66dbb-286">This example creates the journal file if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="66dbb-286">This example creates the journal file if it does not already exist.</span></span> <span data-ttu-id="66dbb-287">If it does exist, then AzCopy resumes the operation based on the journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-287">If it does exist, then AzCopy resumes the operation based on the journal file.</span></span>

<span data-ttu-id="66dbb-288">If you want to resume an AzCopy operation:</span><span class="sxs-lookup"><span data-stu-id="66dbb-288">If you want to resume an AzCopy operation:</span></span>

```azcopy
AzCopy /Z:C:\journalfolder\
```

<span data-ttu-id="66dbb-289">This example resumes the last operation, which may have failed to complete.</span><span class="sxs-lookup"><span data-stu-id="66dbb-289">This example resumes the last operation, which may have failed to complete.</span></span>

### <a name="generate-a-log-file"></a><span data-ttu-id="66dbb-290">Generate a log file</span><span class="sxs-lookup"><span data-stu-id="66dbb-290">Generate a log file</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V
```

<span data-ttu-id="66dbb-291">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-291">If you specify option `/V` without providing a file path to the verbose log, then AzCopy creates the log file in the default location, which is `%SystemDrive%\Users\%username%\AppData\Local\Microsoft\Azure\AzCopy`.</span></span>

<span data-ttu-id="66dbb-292">Otherwise, you can create an log file in a custom location:</span><span class="sxs-lookup"><span data-stu-id="66dbb-292">Otherwise, you can create an log file in a custom location:</span></span>

```azcopy
AzCopy /Source:C:\myfolder /Dest:https://myaccount.blob.core.windows.net/mycontainer /DestKey:key /V:C:\myfolder\azcopy1.log
```

<span data-ttu-id="66dbb-293">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-293">Note that if you specify a relative path following option `/V`, such as `/V:test/azcopy1.log`, then the verbose log is created in the current working directory within a subfolder named `test`.</span></span>

### <a name="specify-the-number-of-concurrent-operations-to-start"></a><span data-ttu-id="66dbb-294">Specify the number of concurrent operations to start</span><span class="sxs-lookup"><span data-stu-id="66dbb-294">Specify the number of concurrent operations to start</span></span>
<span data-ttu-id="66dbb-295">Option `/NC` specifies the number of concurrent copy operations.</span><span class="sxs-lookup"><span data-stu-id="66dbb-295">Option `/NC` specifies the number of concurrent copy operations.</span></span> <span data-ttu-id="66dbb-296">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span><span class="sxs-lookup"><span data-stu-id="66dbb-296">By default, AzCopy starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="66dbb-297">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span><span class="sxs-lookup"><span data-stu-id="66dbb-297">For Table operations, the number of concurrent operations is equal to the number of processors you have.</span></span> <span data-ttu-id="66dbb-298">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span><span class="sxs-lookup"><span data-stu-id="66dbb-298">For Blob and File operations, the number of concurrent operations is equal 8 times the number of processors you have.</span></span> <span data-ttu-id="66dbb-299">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span><span class="sxs-lookup"><span data-stu-id="66dbb-299">If you are running AzCopy across a low-bandwidth network, you can specify a lower number for /NC to avoid failure caused by resource competition.</span></span>

### <a name="run-azcopy-against-azure-storage-emulator"></a><span data-ttu-id="66dbb-300">Run AzCopy against Azure Storage Emulator</span><span class="sxs-lookup"><span data-stu-id="66dbb-300">Run AzCopy against Azure Storage Emulator</span></span>
<span data-ttu-id="66dbb-301">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span><span class="sxs-lookup"><span data-stu-id="66dbb-301">You can run AzCopy against the [Azure Storage Emulator](storage-use-emulator.md) for Blobs:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10000/myaccount/mycontainer/ /Dest:C:\myfolder /SourceKey:key /SourceType:Blob /S
```

<span data-ttu-id="66dbb-302">and Tables:</span><span class="sxs-lookup"><span data-stu-id="66dbb-302">and Tables:</span></span>

```azcopy
AzCopy /Source:https://127.0.0.1:10002/myaccount/mytable/ /Dest:C:\myfolder /SourceKey:key /SourceType:Table
```

## <a name="azcopy-parameters"></a><span data-ttu-id="66dbb-303">AzCopy Parameters</span><span class="sxs-lookup"><span data-stu-id="66dbb-303">AzCopy Parameters</span></span>
<span data-ttu-id="66dbb-304">Parameters for AzCopy are described below.</span><span class="sxs-lookup"><span data-stu-id="66dbb-304">Parameters for AzCopy are described below.</span></span> <span data-ttu-id="66dbb-305">You can also type one of the following commands from the command line for help in using AzCopy:</span><span class="sxs-lookup"><span data-stu-id="66dbb-305">You can also type one of the following commands from the command line for help in using AzCopy:</span></span>

* <span data-ttu-id="66dbb-306">For detailed command-line help for AzCopy: `AzCopy /?`</span><span class="sxs-lookup"><span data-stu-id="66dbb-306">For detailed command-line help for AzCopy: `AzCopy /?`</span></span>
* <span data-ttu-id="66dbb-307">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span><span class="sxs-lookup"><span data-stu-id="66dbb-307">For detailed help with any AzCopy parameter: `AzCopy /?:SourceKey`</span></span>
* <span data-ttu-id="66dbb-308">For command-line examples: `AzCopy /?:Samples`</span><span class="sxs-lookup"><span data-stu-id="66dbb-308">For command-line examples: `AzCopy /?:Samples`</span></span>

### <a name="sourcesource"></a><span data-ttu-id="66dbb-309">/Source:"source"</span><span class="sxs-lookup"><span data-stu-id="66dbb-309">/Source:"source"</span></span>
<span data-ttu-id="66dbb-310">Specifies the source data from which to copy.</span><span class="sxs-lookup"><span data-stu-id="66dbb-310">Specifies the source data from which to copy.</span></span> <span data-ttu-id="66dbb-311">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-311">The source can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="66dbb-312">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-312">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destdestination"></a><span data-ttu-id="66dbb-313">/Dest:"destination"</span><span class="sxs-lookup"><span data-stu-id="66dbb-313">/Dest:"destination"</span></span>
<span data-ttu-id="66dbb-314">Specifies the destination to copy to.</span><span class="sxs-lookup"><span data-stu-id="66dbb-314">Specifies the destination to copy to.</span></span> <span data-ttu-id="66dbb-315">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-315">The destination can be a file system directory, a blob container, a blob virtual directory, a storage file share, a storage file directory, or an Azure table.</span></span>

<span data-ttu-id="66dbb-316">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-316">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="patternfile-pattern"></a><span data-ttu-id="66dbb-317">/Pattern:"file-pattern"</span><span class="sxs-lookup"><span data-stu-id="66dbb-317">/Pattern:"file-pattern"</span></span>
<span data-ttu-id="66dbb-318">Specifies a file pattern that indicates which files to copy.</span><span class="sxs-lookup"><span data-stu-id="66dbb-318">Specifies a file pattern that indicates which files to copy.</span></span> <span data-ttu-id="66dbb-319">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-319">The behavior of the /Pattern parameter is determined by the location of the source data, and the presence of the recursive mode option.</span></span> <span data-ttu-id="66dbb-320">Recursive mode is specified via option /S.</span><span class="sxs-lookup"><span data-stu-id="66dbb-320">Recursive mode is specified via option /S.</span></span>

<span data-ttu-id="66dbb-321">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span><span class="sxs-lookup"><span data-stu-id="66dbb-321">If the specified source is a directory in the file system, then standard wildcards are in effect, and the file pattern provided is matched against files within the directory.</span></span> <span data-ttu-id="66dbb-322">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span><span class="sxs-lookup"><span data-stu-id="66dbb-322">If option /S is specified, then AzCopy also matches the specified pattern against all files in any subfolders beneath the directory.</span></span>

<span data-ttu-id="66dbb-323">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span><span class="sxs-lookup"><span data-stu-id="66dbb-323">If the specified source is a blob container or virtual directory, then wildcards are not applied.</span></span> <span data-ttu-id="66dbb-324">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span><span class="sxs-lookup"><span data-stu-id="66dbb-324">If option /S is specified, then AzCopy interprets the specified file pattern as a blob prefix.</span></span> <span data-ttu-id="66dbb-325">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span><span class="sxs-lookup"><span data-stu-id="66dbb-325">If option /S is not specified, then AzCopy matches the file pattern against exact blob names.</span></span>

<span data-ttu-id="66dbb-326">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span><span class="sxs-lookup"><span data-stu-id="66dbb-326">If the specified source is an Azure file share, then you must either specify the exact file name, (e.g. abc.txt) to copy a single file, or specify option /S to copy all files in the share recursively.</span></span> <span data-ttu-id="66dbb-327">Attempting to specify both a file pattern and option /S together will result in an error.</span><span class="sxs-lookup"><span data-stu-id="66dbb-327">Attempting to specify both a file pattern and option /S together will result in an error.</span></span>

<span data-ttu-id="66dbb-328">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span><span class="sxs-lookup"><span data-stu-id="66dbb-328">AzCopy uses case-sensitive matching when the /Source is a blob container or blob virtual directory, and uses case-insensitive matching in all the other cases.</span></span>

<span data-ttu-id="66dbb-329">The default file pattern used when no file pattern is specified is *.*</span><span class="sxs-lookup"><span data-stu-id="66dbb-329">The default file pattern used when no file pattern is specified is *.*</span></span> <span data-ttu-id="66dbb-330">for a file system location or an empty prefix for an Azure Storage location.</span><span class="sxs-lookup"><span data-stu-id="66dbb-330">for a file system location or an empty prefix for an Azure Storage location.</span></span> <span data-ttu-id="66dbb-331">Specifying multiple file patterns is not supported.</span><span class="sxs-lookup"><span data-stu-id="66dbb-331">Specifying multiple file patterns is not supported.</span></span>

<span data-ttu-id="66dbb-332">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-332">**Applicable to:** Blobs, Files</span></span>

### <a name="destkeystorage-key"></a><span data-ttu-id="66dbb-333">/DestKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="66dbb-333">/DestKey:"storage-key"</span></span>
<span data-ttu-id="66dbb-334">Specifies the storage account key for the destination resource.</span><span class="sxs-lookup"><span data-stu-id="66dbb-334">Specifies the storage account key for the destination resource.</span></span>

<span data-ttu-id="66dbb-335">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-335">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="destsassas-token"></a><span data-ttu-id="66dbb-336">/DestSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="66dbb-336">/DestSAS:"sas-token"</span></span>
<span data-ttu-id="66dbb-337">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span><span class="sxs-lookup"><span data-stu-id="66dbb-337">Specifies a Shared Access Signature (SAS) with READ and WRITE permissions for the destination (if applicable).</span></span> <span data-ttu-id="66dbb-338">Surround the SAS with double quotes, as it may contains special command-line characters.</span><span class="sxs-lookup"><span data-stu-id="66dbb-338">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="66dbb-339">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-339">If the destination resource is a blob container, file share or table, you can either specify this option followed by the SAS token, or you can specify the SAS as part of the destination blob container, file share or table's URI, without this option.</span></span>

<span data-ttu-id="66dbb-340">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-340">If the source and destination are both blobs, then the destination blob must reside within the same storage account as the source blob.</span></span>

<span data-ttu-id="66dbb-341">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-341">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcekeystorage-key"></a><span data-ttu-id="66dbb-342">/SourceKey:"storage-key"</span><span class="sxs-lookup"><span data-stu-id="66dbb-342">/SourceKey:"storage-key"</span></span>
<span data-ttu-id="66dbb-343">Specifies the storage account key for the source resource.</span><span class="sxs-lookup"><span data-stu-id="66dbb-343">Specifies the storage account key for the source resource.</span></span>

<span data-ttu-id="66dbb-344">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-344">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcesassas-token"></a><span data-ttu-id="66dbb-345">/SourceSAS:"sas-token"</span><span class="sxs-lookup"><span data-stu-id="66dbb-345">/SourceSAS:"sas-token"</span></span>
<span data-ttu-id="66dbb-346">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span><span class="sxs-lookup"><span data-stu-id="66dbb-346">Specifies a Shared Access Signature with READ and LIST permissions for the source (if applicable).</span></span> <span data-ttu-id="66dbb-347">Surround the SAS with double quotes, as it may contains special command-line characters.</span><span class="sxs-lookup"><span data-stu-id="66dbb-347">Surround the SAS with double quotes, as it may contains special command-line characters.</span></span>

<span data-ttu-id="66dbb-348">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span><span class="sxs-lookup"><span data-stu-id="66dbb-348">If the source resource is a blob container, and neither a key nor a SAS is provided, then the blob container will be read via anonymous access.</span></span>

<span data-ttu-id="66dbb-349">If the source is a file share or table, a key or a SAS must be provided.</span><span class="sxs-lookup"><span data-stu-id="66dbb-349">If the source is a file share or table, a key or a SAS must be provided.</span></span>

<span data-ttu-id="66dbb-350">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-350">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="s"></a><span data-ttu-id="66dbb-351">/S</span><span class="sxs-lookup"><span data-stu-id="66dbb-351">/S</span></span>
<span data-ttu-id="66dbb-352">Specifies recursive mode for copy operations.</span><span class="sxs-lookup"><span data-stu-id="66dbb-352">Specifies recursive mode for copy operations.</span></span> <span data-ttu-id="66dbb-353">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span><span class="sxs-lookup"><span data-stu-id="66dbb-353">In recursive mode, AzCopy will copy all blobs or files that match the specified file pattern, including those in subfolders.</span></span>

<span data-ttu-id="66dbb-354">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-354">**Applicable to:** Blobs, Files</span></span>

### <a name="blobtypeblock--page--append"></a><span data-ttu-id="66dbb-355">/BlobType:"block" | "page" | "append"</span><span class="sxs-lookup"><span data-stu-id="66dbb-355">/BlobType:"block" | "page" | "append"</span></span>
<span data-ttu-id="66dbb-356">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-356">Specifies whether the destination blob is a block blob, a page blob, or an append blob.</span></span> <span data-ttu-id="66dbb-357">This option is applicable only when you are uploading a blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-357">This option is applicable only when you are uploading a blob.</span></span> <span data-ttu-id="66dbb-358">Otherwise, an error is generated.</span><span class="sxs-lookup"><span data-stu-id="66dbb-358">Otherwise, an error is generated.</span></span> <span data-ttu-id="66dbb-359">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-359">If the destination is a blob and this option is not specified, by default, AzCopy creates a block blob.</span></span>

<span data-ttu-id="66dbb-360">**Applicable to:** Blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-360">**Applicable to:** Blobs</span></span>

### <a name="checkmd5"></a><span data-ttu-id="66dbb-361">/CheckMD5</span><span class="sxs-lookup"><span data-stu-id="66dbb-361">/CheckMD5</span></span>
<span data-ttu-id="66dbb-362">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span><span class="sxs-lookup"><span data-stu-id="66dbb-362">Calculates an MD5 hash for downloaded data and verifies that the MD5 hash stored in the blob or file's Content-MD5 property matches the calculated hash.</span></span> <span data-ttu-id="66dbb-363">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span><span class="sxs-lookup"><span data-stu-id="66dbb-363">The MD5 check is turned off by default, so you must specify this option to perform the MD5 check when downloading data.</span></span>

<span data-ttu-id="66dbb-364">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span><span class="sxs-lookup"><span data-stu-id="66dbb-364">Note that Azure Storage doesn't guarantee that the MD5 hash stored for the blob or file is up-to-date.</span></span> <span data-ttu-id="66dbb-365">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span><span class="sxs-lookup"><span data-stu-id="66dbb-365">It is client's responsibility to update the MD5 whenever the blob or file is modified.</span></span>

<span data-ttu-id="66dbb-366">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span><span class="sxs-lookup"><span data-stu-id="66dbb-366">AzCopy always sets the Content-MD5 property for an Azure blob or file after uploading it to the service.</span></span>  

<span data-ttu-id="66dbb-367">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-367">**Applicable to:** Blobs, Files</span></span>

### <a name="snapshot"></a><span data-ttu-id="66dbb-368">/Snapshot</span><span class="sxs-lookup"><span data-stu-id="66dbb-368">/Snapshot</span></span>
<span data-ttu-id="66dbb-369">Indicates whether to transfer snapshots.</span><span class="sxs-lookup"><span data-stu-id="66dbb-369">Indicates whether to transfer snapshots.</span></span> <span data-ttu-id="66dbb-370">This option is only valid when the source is a blob.</span><span class="sxs-lookup"><span data-stu-id="66dbb-370">This option is only valid when the source is a blob.</span></span>

<span data-ttu-id="66dbb-371">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span><span class="sxs-lookup"><span data-stu-id="66dbb-371">The transferred blob snapshots are renamed in this format: blob-name (snapshot-time).extension</span></span>

<span data-ttu-id="66dbb-372">By default, snapshots are not copied.</span><span class="sxs-lookup"><span data-stu-id="66dbb-372">By default, snapshots are not copied.</span></span>

<span data-ttu-id="66dbb-373">**Applicable to:** Blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-373">**Applicable to:** Blobs</span></span>

### <a name="vverbose-log-file"></a><span data-ttu-id="66dbb-374">/V:[verbose-log-file]</span><span class="sxs-lookup"><span data-stu-id="66dbb-374">/V:[verbose-log-file]</span></span>
<span data-ttu-id="66dbb-375">Outputs verbose status messages into a log file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-375">Outputs verbose status messages into a log file.</span></span>

<span data-ttu-id="66dbb-376">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span><span class="sxs-lookup"><span data-stu-id="66dbb-376">By default, the verbose log file is named AzCopyVerbose.log in `%LocalAppData%\Microsoft\Azure\AzCopy`.</span></span> <span data-ttu-id="66dbb-377">If you specify an existing file location for this option, the verbose log will be appended to that file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-377">If you specify an existing file location for this option, the verbose log will be appended to that file.</span></span>  

<span data-ttu-id="66dbb-378">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-378">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="zjournal-file-folder"></a><span data-ttu-id="66dbb-379">/Z:[journal-file-folder]</span><span class="sxs-lookup"><span data-stu-id="66dbb-379">/Z:[journal-file-folder]</span></span>
<span data-ttu-id="66dbb-380">Specifies a journal file folder for resuming an operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-380">Specifies a journal file folder for resuming an operation.</span></span>

<span data-ttu-id="66dbb-381">AzCopy always supports resuming if an operation has been interrupted.</span><span class="sxs-lookup"><span data-stu-id="66dbb-381">AzCopy always supports resuming if an operation has been interrupted.</span></span>

<span data-ttu-id="66dbb-382">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span><span class="sxs-lookup"><span data-stu-id="66dbb-382">If this option is not specified, or it is specified without a folder path, then AzCopy will create the journal file in the default location, which is %LocalAppData%\Microsoft\Azure\AzCopy.</span></span>

<span data-ttu-id="66dbb-383">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-383">Each time you issue a command to AzCopy, it checks whether a journal file exists in the default folder, or whether it exists in a folder that you specified via this option.</span></span> <span data-ttu-id="66dbb-384">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-384">If the journal file does not exist in either place, AzCopy treats the operation as new and generates a new journal file.</span></span>

<span data-ttu-id="66dbb-385">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-385">If the journal file does exist, AzCopy will check whether the command line that you input matches the command line in the journal file.</span></span> <span data-ttu-id="66dbb-386">If the two command lines match, AzCopy resumes the incomplete operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-386">If the two command lines match, AzCopy resumes the incomplete operation.</span></span> <span data-ttu-id="66dbb-387">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-387">If they do not match, you will be prompted to either overwrite the journal file to start a new operation, or to cancel the current operation.</span></span>

<span data-ttu-id="66dbb-388">The journal file is deleted upon successful completion of the operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-388">The journal file is deleted upon successful completion of the operation.</span></span>

<span data-ttu-id="66dbb-389">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span><span class="sxs-lookup"><span data-stu-id="66dbb-389">Note that resuming an operation from a journal file created by a previous version of AzCopy is not supported.</span></span>

<span data-ttu-id="66dbb-390">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-390">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="parameter-file"></a><span data-ttu-id="66dbb-391">/@:"parameter-file"</span><span class="sxs-lookup"><span data-stu-id="66dbb-391">/@:"parameter-file"</span></span>
<span data-ttu-id="66dbb-392">Specifies a file that contains parameters.</span><span class="sxs-lookup"><span data-stu-id="66dbb-392">Specifies a file that contains parameters.</span></span> <span data-ttu-id="66dbb-393">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span><span class="sxs-lookup"><span data-stu-id="66dbb-393">AzCopy processes the parameters in the file just as if they had been specified on the command line.</span></span>

<span data-ttu-id="66dbb-394">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span><span class="sxs-lookup"><span data-stu-id="66dbb-394">In a response file, you can either specify multiple parameters on a single line, or specify each parameter on its own line.</span></span> <span data-ttu-id="66dbb-395">Note that an individual parameter cannot span multiple lines.</span><span class="sxs-lookup"><span data-stu-id="66dbb-395">Note that an individual parameter cannot span multiple lines.</span></span>

<span data-ttu-id="66dbb-396">Response files can include comments lines that begin with the # symbol.</span><span class="sxs-lookup"><span data-stu-id="66dbb-396">Response files can include comments lines that begin with the # symbol.</span></span>

<span data-ttu-id="66dbb-397">You can specify multiple response files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-397">You can specify multiple response files.</span></span> <span data-ttu-id="66dbb-398">However, note that AzCopy does not support nested response files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-398">However, note that AzCopy does not support nested response files.</span></span>

<span data-ttu-id="66dbb-399">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-399">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="y"></a><span data-ttu-id="66dbb-400">/Y</span><span class="sxs-lookup"><span data-stu-id="66dbb-400">/Y</span></span>
<span data-ttu-id="66dbb-401">Suppresses all AzCopy confirmation prompts.</span><span class="sxs-lookup"><span data-stu-id="66dbb-401">Suppresses all AzCopy confirmation prompts.</span></span>

<span data-ttu-id="66dbb-402">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-402">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="l"></a><span data-ttu-id="66dbb-403">/L</span><span class="sxs-lookup"><span data-stu-id="66dbb-403">/L</span></span>
<span data-ttu-id="66dbb-404">Specifies a listing operation only; no data is copied.</span><span class="sxs-lookup"><span data-stu-id="66dbb-404">Specifies a listing operation only; no data is copied.</span></span>

<span data-ttu-id="66dbb-405">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span><span class="sxs-lookup"><span data-stu-id="66dbb-405">AzCopy will interpret the using of this option as a simulation for running the command line without this option /L and count how many objects will be copied, you can specify option /V at the same time to check which objects will be copied in the verbose log.</span></span>

<span data-ttu-id="66dbb-406">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span><span class="sxs-lookup"><span data-stu-id="66dbb-406">The behavior of this option is also determined by the location of the source data and the presence of the recursive mode option /S and file pattern option /Pattern.</span></span>

<span data-ttu-id="66dbb-407">AzCopy requires LIST and READ permission of this source location when using this option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-407">AzCopy requires LIST and READ permission of this source location when using this option.</span></span>

<span data-ttu-id="66dbb-408">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-408">**Applicable to:** Blobs, Files</span></span>

### <a name="mt"></a><span data-ttu-id="66dbb-409">/MT</span><span class="sxs-lookup"><span data-stu-id="66dbb-409">/MT</span></span>
<span data-ttu-id="66dbb-410">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span><span class="sxs-lookup"><span data-stu-id="66dbb-410">Sets the downloaded file's last-modified time to be the same as the source blob or file's.</span></span>

<span data-ttu-id="66dbb-411">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-411">**Applicable to:** Blobs, Files</span></span>

### <a name="xn"></a><span data-ttu-id="66dbb-412">/XN</span><span class="sxs-lookup"><span data-stu-id="66dbb-412">/XN</span></span>
<span data-ttu-id="66dbb-413">Excludes a newer source resource.</span><span class="sxs-lookup"><span data-stu-id="66dbb-413">Excludes a newer source resource.</span></span> <span data-ttu-id="66dbb-414">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span><span class="sxs-lookup"><span data-stu-id="66dbb-414">The resource will not be copied if the last modified time of the source is the same or newer than destination.</span></span>

<span data-ttu-id="66dbb-415">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-415">**Applicable to:** Blobs, Files</span></span>

### <a name="xo"></a><span data-ttu-id="66dbb-416">/XO</span><span class="sxs-lookup"><span data-stu-id="66dbb-416">/XO</span></span>
<span data-ttu-id="66dbb-417">Excludes an older source resource.</span><span class="sxs-lookup"><span data-stu-id="66dbb-417">Excludes an older source resource.</span></span> <span data-ttu-id="66dbb-418">The resource will not be copied if the last modified time of the source is the same or older than destination.</span><span class="sxs-lookup"><span data-stu-id="66dbb-418">The resource will not be copied if the last modified time of the source is the same or older than destination.</span></span>

<span data-ttu-id="66dbb-419">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-419">**Applicable to:** Blobs, Files</span></span>

### <a name="a"></a><span data-ttu-id="66dbb-420">/A</span><span class="sxs-lookup"><span data-stu-id="66dbb-420">/A</span></span>
<span data-ttu-id="66dbb-421">Uploads only files that have the Archive attribute set.</span><span class="sxs-lookup"><span data-stu-id="66dbb-421">Uploads only files that have the Archive attribute set.</span></span>

<span data-ttu-id="66dbb-422">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-422">**Applicable to:** Blobs, Files</span></span>

### <a name="iarashcnetoi"></a><span data-ttu-id="66dbb-423">/IA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="66dbb-423">/IA:[RASHCNETOI]</span></span>
<span data-ttu-id="66dbb-424">Uploads only files that have any of the specified attributes set.</span><span class="sxs-lookup"><span data-stu-id="66dbb-424">Uploads only files that have any of the specified attributes set.</span></span>

<span data-ttu-id="66dbb-425">Available attributes include:</span><span class="sxs-lookup"><span data-stu-id="66dbb-425">Available attributes include:</span></span>

* <span data-ttu-id="66dbb-426">R = Read-only files</span><span class="sxs-lookup"><span data-stu-id="66dbb-426">R = Read-only files</span></span>
* <span data-ttu-id="66dbb-427">A = Files ready for archiving</span><span class="sxs-lookup"><span data-stu-id="66dbb-427">A = Files ready for archiving</span></span>
* <span data-ttu-id="66dbb-428">S = System files</span><span class="sxs-lookup"><span data-stu-id="66dbb-428">S = System files</span></span>
* <span data-ttu-id="66dbb-429">H = Hidden files</span><span class="sxs-lookup"><span data-stu-id="66dbb-429">H = Hidden files</span></span>
* <span data-ttu-id="66dbb-430">C = Compressed files</span><span class="sxs-lookup"><span data-stu-id="66dbb-430">C = Compressed files</span></span>
* <span data-ttu-id="66dbb-431">N = Normal files</span><span class="sxs-lookup"><span data-stu-id="66dbb-431">N = Normal files</span></span>
* <span data-ttu-id="66dbb-432">E = Encrypted files</span><span class="sxs-lookup"><span data-stu-id="66dbb-432">E = Encrypted files</span></span>
* <span data-ttu-id="66dbb-433">T = Temporary files</span><span class="sxs-lookup"><span data-stu-id="66dbb-433">T = Temporary files</span></span>
* <span data-ttu-id="66dbb-434">O = Offline files</span><span class="sxs-lookup"><span data-stu-id="66dbb-434">O = Offline files</span></span>
* <span data-ttu-id="66dbb-435">I = Non-indexed files</span><span class="sxs-lookup"><span data-stu-id="66dbb-435">I = Non-indexed files</span></span>

<span data-ttu-id="66dbb-436">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-436">**Applicable to:** Blobs, Files</span></span>

### <a name="xarashcnetoi"></a><span data-ttu-id="66dbb-437">/XA:[RASHCNETOI]</span><span class="sxs-lookup"><span data-stu-id="66dbb-437">/XA:[RASHCNETOI]</span></span>
<span data-ttu-id="66dbb-438">Excludes files that have any of the specified attributes set.</span><span class="sxs-lookup"><span data-stu-id="66dbb-438">Excludes files that have any of the specified attributes set.</span></span>

<span data-ttu-id="66dbb-439">Available attributes include:</span><span class="sxs-lookup"><span data-stu-id="66dbb-439">Available attributes include:</span></span>

* <span data-ttu-id="66dbb-440">R = Read-only files</span><span class="sxs-lookup"><span data-stu-id="66dbb-440">R = Read-only files</span></span>
* <span data-ttu-id="66dbb-441">A = Files ready for archiving</span><span class="sxs-lookup"><span data-stu-id="66dbb-441">A = Files ready for archiving</span></span>
* <span data-ttu-id="66dbb-442">S = System files</span><span class="sxs-lookup"><span data-stu-id="66dbb-442">S = System files</span></span>
* <span data-ttu-id="66dbb-443">H = Hidden files</span><span class="sxs-lookup"><span data-stu-id="66dbb-443">H = Hidden files</span></span>
* <span data-ttu-id="66dbb-444">C = Compressed files</span><span class="sxs-lookup"><span data-stu-id="66dbb-444">C = Compressed files</span></span>
* <span data-ttu-id="66dbb-445">N = Normal files</span><span class="sxs-lookup"><span data-stu-id="66dbb-445">N = Normal files</span></span>
* <span data-ttu-id="66dbb-446">E = Encrypted files</span><span class="sxs-lookup"><span data-stu-id="66dbb-446">E = Encrypted files</span></span>
* <span data-ttu-id="66dbb-447">T = Temporary files</span><span class="sxs-lookup"><span data-stu-id="66dbb-447">T = Temporary files</span></span>
* <span data-ttu-id="66dbb-448">O = Offline files</span><span class="sxs-lookup"><span data-stu-id="66dbb-448">O = Offline files</span></span>
* <span data-ttu-id="66dbb-449">I = Non-indexed files</span><span class="sxs-lookup"><span data-stu-id="66dbb-449">I = Non-indexed files</span></span>

<span data-ttu-id="66dbb-450">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-450">**Applicable to:** Blobs, Files</span></span>

### <a name="delimiterdelimiter"></a><span data-ttu-id="66dbb-451">/Delimiter:"delimiter"</span><span class="sxs-lookup"><span data-stu-id="66dbb-451">/Delimiter:"delimiter"</span></span>
<span data-ttu-id="66dbb-452">Indicates the delimiter character used to delimit virtual directories in a blob name.</span><span class="sxs-lookup"><span data-stu-id="66dbb-452">Indicates the delimiter character used to delimit virtual directories in a blob name.</span></span>

<span data-ttu-id="66dbb-453">By default, AzCopy uses / as the delimiter character.</span><span class="sxs-lookup"><span data-stu-id="66dbb-453">By default, AzCopy uses / as the delimiter character.</span></span> <span data-ttu-id="66dbb-454">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span><span class="sxs-lookup"><span data-stu-id="66dbb-454">However, AzCopy supports using any common character (such as @, #, or %) as a delimiter.</span></span> <span data-ttu-id="66dbb-455">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span><span class="sxs-lookup"><span data-stu-id="66dbb-455">If you need to include one of these special characters on the command line, enclose the file name with double quotes.</span></span>

<span data-ttu-id="66dbb-456">This option is only applicable for downloading blobs.</span><span class="sxs-lookup"><span data-stu-id="66dbb-456">This option is only applicable for downloading blobs.</span></span>

<span data-ttu-id="66dbb-457">**Applicable to:** Blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-457">**Applicable to:** Blobs</span></span>

### <a name="ncnumber-of-concurrent-operations"></a><span data-ttu-id="66dbb-458">/NC:"number-of-concurrent-operations"</span><span class="sxs-lookup"><span data-stu-id="66dbb-458">/NC:"number-of-concurrent-operations"</span></span>
<span data-ttu-id="66dbb-459">Specifies the number of concurrent operations.</span><span class="sxs-lookup"><span data-stu-id="66dbb-459">Specifies the number of concurrent operations.</span></span>

<span data-ttu-id="66dbb-460">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span><span class="sxs-lookup"><span data-stu-id="66dbb-460">AzCopy by default starts a certain number of concurrent operations to increase the data transfer throughput.</span></span> <span data-ttu-id="66dbb-461">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span><span class="sxs-lookup"><span data-stu-id="66dbb-461">Note that large number of concurrent operations in a low-bandwidth environment may overwhelm the network connection and prevent the operations from fully completing.</span></span> <span data-ttu-id="66dbb-462">Throttle concurrent operations based on actual available network bandwidth.</span><span class="sxs-lookup"><span data-stu-id="66dbb-462">Throttle concurrent operations based on actual available network bandwidth.</span></span>

<span data-ttu-id="66dbb-463">The upper limit for concurrent operations is 512.</span><span class="sxs-lookup"><span data-stu-id="66dbb-463">The upper limit for concurrent operations is 512.</span></span>

<span data-ttu-id="66dbb-464">**Applicable to:** Blobs, Files, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-464">**Applicable to:** Blobs, Files, Tables</span></span>

### <a name="sourcetypeblob--table"></a><span data-ttu-id="66dbb-465">/SourceType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="66dbb-465">/SourceType:"Blob" | "Table"</span></span>
<span data-ttu-id="66dbb-466">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="66dbb-466">Specifies that the `source` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="66dbb-467">**Applicable to:** Blobs, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-467">**Applicable to:** Blobs, Tables</span></span>

### <a name="desttypeblob--table"></a><span data-ttu-id="66dbb-468">/DestType:"Blob" | "Table"</span><span class="sxs-lookup"><span data-stu-id="66dbb-468">/DestType:"Blob" | "Table"</span></span>
<span data-ttu-id="66dbb-469">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span><span class="sxs-lookup"><span data-stu-id="66dbb-469">Specifies that the `destination` resource is a blob available in the local development environment, running in the storage emulator.</span></span>

<span data-ttu-id="66dbb-470">**Applicable to:** Blobs, Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-470">**Applicable to:** Blobs, Tables</span></span>

### <a name="pkrskey1key2key3"></a><span data-ttu-id="66dbb-471">/PKRS:"key1#key2#key3#..."</span><span class="sxs-lookup"><span data-stu-id="66dbb-471">/PKRS:"key1#key2#key3#..."</span></span>
<span data-ttu-id="66dbb-472">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-472">Splits the partition key range to enable exporting table data in parallel, which increases the speed of the export operation.</span></span>

<span data-ttu-id="66dbb-473">If this option is not specified, then AzCopy uses a single thread to export table entities.</span><span class="sxs-lookup"><span data-stu-id="66dbb-473">If this option is not specified, then AzCopy uses a single thread to export table entities.</span></span> <span data-ttu-id="66dbb-474">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span><span class="sxs-lookup"><span data-stu-id="66dbb-474">For example, if the user specifies /PKRS:"aa#bb", then AzCopy starts three concurrent operations.</span></span>

<span data-ttu-id="66dbb-475">Each operation exports one of three partition key ranges, as shown below:</span><span class="sxs-lookup"><span data-stu-id="66dbb-475">Each operation exports one of three partition key ranges, as shown below:</span></span>

  <span data-ttu-id="66dbb-476">[first-partition-key, aa)</span><span class="sxs-lookup"><span data-stu-id="66dbb-476">[first-partition-key, aa)</span></span>

  <span data-ttu-id="66dbb-477">[aa, bb)</span><span class="sxs-lookup"><span data-stu-id="66dbb-477">[aa, bb)</span></span>

  <span data-ttu-id="66dbb-478">[bb, last-partition-key]</span><span class="sxs-lookup"><span data-stu-id="66dbb-478">[bb, last-partition-key]</span></span>

<span data-ttu-id="66dbb-479">**Applicable to:** Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-479">**Applicable to:** Tables</span></span>

### <a name="splitsizefile-size"></a><span data-ttu-id="66dbb-480">/SplitSize:"file-size"</span><span class="sxs-lookup"><span data-stu-id="66dbb-480">/SplitSize:"file-size"</span></span>
<span data-ttu-id="66dbb-481">Specifies the exported file split size in MB, the minimal value allowed is 32.</span><span class="sxs-lookup"><span data-stu-id="66dbb-481">Specifies the exported file split size in MB, the minimal value allowed is 32.</span></span>

<span data-ttu-id="66dbb-482">If this option is not specified, AzCopy will export table data to single file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-482">If this option is not specified, AzCopy will export table data to single file.</span></span>

<span data-ttu-id="66dbb-483">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span><span class="sxs-lookup"><span data-stu-id="66dbb-483">If the table data is exported to a blob, and the exported file size reaches the 200 GB limit for blob size, then AzCopy will split the exported file, even if this option is not specified.</span></span>

<span data-ttu-id="66dbb-484">**Applicable to:** Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-484">**Applicable to:** Tables</span></span>

### <a name="entityoperationinsertorskip--insertormerge--insertorreplace"></a><span data-ttu-id="66dbb-485">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span><span class="sxs-lookup"><span data-stu-id="66dbb-485">/EntityOperation:"InsertOrSkip" | "InsertOrMerge" | "InsertOrReplace"</span></span>
<span data-ttu-id="66dbb-486">Specifies the table data import behavior.</span><span class="sxs-lookup"><span data-stu-id="66dbb-486">Specifies the table data import behavior.</span></span>

* <span data-ttu-id="66dbb-487">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-487">InsertOrSkip - Skips an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="66dbb-488">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-488">InsertOrMerge - Merges an existing entity or inserts a new entity if it does not exist in the table.</span></span>
* <span data-ttu-id="66dbb-489">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span><span class="sxs-lookup"><span data-stu-id="66dbb-489">InsertOrReplace - Replaces an existing entity or inserts a new entity if it does not exist in the table.</span></span>

<span data-ttu-id="66dbb-490">**Applicable to:** Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-490">**Applicable to:** Tables</span></span>

### <a name="manifestmanifest-file"></a><span data-ttu-id="66dbb-491">/Manifest:"manifest-file"</span><span class="sxs-lookup"><span data-stu-id="66dbb-491">/Manifest:"manifest-file"</span></span>
<span data-ttu-id="66dbb-492">Specifies the manifest file for the table export and import operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-492">Specifies the manifest file for the table export and import operation.</span></span>

<span data-ttu-id="66dbb-493">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span><span class="sxs-lookup"><span data-stu-id="66dbb-493">This option is optional during the export operation, AzCopy will generate a manifest file with predefined name if this option is not specified.</span></span>

<span data-ttu-id="66dbb-494">This option is required during the import operation for locating the data files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-494">This option is required during the import operation for locating the data files.</span></span>

<span data-ttu-id="66dbb-495">**Applicable to:** Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-495">**Applicable to:** Tables</span></span>

### <a name="synccopy"></a><span data-ttu-id="66dbb-496">/SyncCopy</span><span class="sxs-lookup"><span data-stu-id="66dbb-496">/SyncCopy</span></span>
<span data-ttu-id="66dbb-497">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span><span class="sxs-lookup"><span data-stu-id="66dbb-497">Indicates whether to synchronously copy blobs or files between two Azure Storage endpoints.</span></span>

<span data-ttu-id="66dbb-498">AzCopy by default uses server-side asynchronous copy.</span><span class="sxs-lookup"><span data-stu-id="66dbb-498">AzCopy by default uses server-side asynchronous copy.</span></span> <span data-ttu-id="66dbb-499">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="66dbb-499">Specify this option to perform a synchronous copy, which downloads blobs or files to local memory and then uploads them to Azure Storage.</span></span>

<span data-ttu-id="66dbb-500">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span><span class="sxs-lookup"><span data-stu-id="66dbb-500">You can use this option when copying files within Blob storage, within File storage, or from Blob storage to File storage or vice versa.</span></span>

<span data-ttu-id="66dbb-501">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-501">**Applicable to:** Blobs, Files</span></span>

### <a name="setcontenttypecontent-type"></a><span data-ttu-id="66dbb-502">/SetContentType:"content-type"</span><span class="sxs-lookup"><span data-stu-id="66dbb-502">/SetContentType:"content-type"</span></span>
<span data-ttu-id="66dbb-503">Specifies the MIME content type for destination blobs or files.</span><span class="sxs-lookup"><span data-stu-id="66dbb-503">Specifies the MIME content type for destination blobs or files.</span></span>

<span data-ttu-id="66dbb-504">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span><span class="sxs-lookup"><span data-stu-id="66dbb-504">AzCopy sets the content type for a blob or file to application/octet-stream by default.</span></span> <span data-ttu-id="66dbb-505">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span><span class="sxs-lookup"><span data-stu-id="66dbb-505">You can set the content type for all blobs or files by explicitly specifying a value for this option.</span></span>

<span data-ttu-id="66dbb-506">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span><span class="sxs-lookup"><span data-stu-id="66dbb-506">If you specify this option without a value, then AzCopy will set each blob or file's content type according to its file extension.</span></span>

<span data-ttu-id="66dbb-507">**Applicable to:** Blobs, Files</span><span class="sxs-lookup"><span data-stu-id="66dbb-507">**Applicable to:** Blobs, Files</span></span>

### <a name="payloadformatjson--csv"></a><span data-ttu-id="66dbb-508">/PayloadFormat:"JSON" | "CSV"</span><span class="sxs-lookup"><span data-stu-id="66dbb-508">/PayloadFormat:"JSON" | "CSV"</span></span>
<span data-ttu-id="66dbb-509">Specifies the format of the table exported data file.</span><span class="sxs-lookup"><span data-stu-id="66dbb-509">Specifies the format of the table exported data file.</span></span>

<span data-ttu-id="66dbb-510">If this option is not specified, by default AzCopy exports table data file in JSON format.</span><span class="sxs-lookup"><span data-stu-id="66dbb-510">If this option is not specified, by default AzCopy exports table data file in JSON format.</span></span>

<span data-ttu-id="66dbb-511">**Applicable to:** Tables</span><span class="sxs-lookup"><span data-stu-id="66dbb-511">**Applicable to:** Tables</span></span>

## <a name="known-issues-and-best-practices"></a><span data-ttu-id="66dbb-512">Known Issues and Best Practices</span><span class="sxs-lookup"><span data-stu-id="66dbb-512">Known Issues and Best Practices</span></span>
### <a name="limit-concurrent-writes-while-copying-data"></a><span data-ttu-id="66dbb-513">Limit concurrent writes while copying data</span><span class="sxs-lookup"><span data-stu-id="66dbb-513">Limit concurrent writes while copying data</span></span>
<span data-ttu-id="66dbb-514">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span><span class="sxs-lookup"><span data-stu-id="66dbb-514">When you copy blobs or files with AzCopy, keep in mind that another application may be modifying the data while you are copying it.</span></span> <span data-ttu-id="66dbb-515">If possible, ensure that the data you are copying is not being modified during the copy operation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-515">If possible, ensure that the data you are copying is not being modified during the copy operation.</span></span> <span data-ttu-id="66dbb-516">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span><span class="sxs-lookup"><span data-stu-id="66dbb-516">For example, when copying a VHD associated with an Azure virtual machine, make sure that no other applications are currently writing to the VHD.</span></span> <span data-ttu-id="66dbb-517">A good way to do this is by leasing the resource to be copied.</span><span class="sxs-lookup"><span data-stu-id="66dbb-517">A good way to do this is by leasing the resource to be copied.</span></span> <span data-ttu-id="66dbb-518">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span><span class="sxs-lookup"><span data-stu-id="66dbb-518">Alternately, you can create a snapshot of the VHD first and then copy the snapshot.</span></span>

<span data-ttu-id="66dbb-519">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span><span class="sxs-lookup"><span data-stu-id="66dbb-519">If you cannot prevent other applications from writing to blobs or files while they are being copied, then keep in mind that by the time the job finishes, the copied resources may no longer have full parity with the source resources.</span></span>

### <a name="run-one-azcopy-instance-on-one-machine"></a><span data-ttu-id="66dbb-520">Run one AzCopy instance on one machine.</span><span class="sxs-lookup"><span data-stu-id="66dbb-520">Run one AzCopy instance on one machine.</span></span>
<span data-ttu-id="66dbb-521">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span><span class="sxs-lookup"><span data-stu-id="66dbb-521">AzCopy is designed to maximize the utilization of your machine resource to accelerate the data transfer, we recommend you run only one AzCopy instance on one machine, and specify the option `/NC` if you need more concurrent operations.</span></span> <span data-ttu-id="66dbb-522">For more details, type `AzCopy /?:NC` at the command line.</span><span class="sxs-lookup"><span data-stu-id="66dbb-522">For more details, type `AzCopy /?:NC` at the command line.</span></span>

### <a name="enable-fips-compliant-md5-algorithms-for-azcopy-when-you-use-fips-compliant-algorithms-for-encryption-hashing-and-signing"></a><span data-ttu-id="66dbb-523">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span><span class="sxs-lookup"><span data-stu-id="66dbb-523">Enable FIPS compliant MD5 algorithms for AzCopy when you "Use FIPS compliant algorithms for encryption, hashing and signing".</span></span>
<span data-ttu-id="66dbb-524">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span><span class="sxs-lookup"><span data-stu-id="66dbb-524">AzCopy by default uses .NET MD5 implementation to calculate the MD5 when copying objects, but there are some security requirements that need AzCopy to enable FIPS compliant MD5 setting.</span></span>

<span data-ttu-id="66dbb-525">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span><span class="sxs-lookup"><span data-stu-id="66dbb-525">You can create an app.config file `AzCopy.exe.config` with property `AzureStorageUseV1MD5` and put it aside with AzCopy.exe.</span></span>

    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
      <appSettings>
        <add key="AzureStorageUseV1MD5" value="false"/>
      </appSettings>
    </configuration>

<span data-ttu-id="66dbb-526">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span><span class="sxs-lookup"><span data-stu-id="66dbb-526">For property "AzureStorageUseV1MD5" • True - The default value, AzCopy will use .NET MD5 implementation.</span></span>
<span data-ttu-id="66dbb-527">• False – AzCopy will use FIPS compliant MD5 algorithm.</span><span class="sxs-lookup"><span data-stu-id="66dbb-527">• False – AzCopy will use FIPS compliant MD5 algorithm.</span></span>

<span data-ttu-id="66dbb-528">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span><span class="sxs-lookup"><span data-stu-id="66dbb-528">Note that FIPS compliant algorithms is disabled by default on your Windows machine, you can type secpol.msc in your Run window and check this switch at Security Setting->Local Policy->Security Options->System cryptography: Use FIPS compliant algorithms for encryption, hashing and signing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66dbb-529">Next steps</span><span class="sxs-lookup"><span data-stu-id="66dbb-529">Next steps</span></span>
<span data-ttu-id="66dbb-530">For more information about Azure Storage and AzCopy, refer to the following resources.</span><span class="sxs-lookup"><span data-stu-id="66dbb-530">For more information about Azure Storage and AzCopy, refer to the following resources.</span></span>

### <a name="azure-storage-documentation"></a><span data-ttu-id="66dbb-531">Azure Storage documentation:</span><span class="sxs-lookup"><span data-stu-id="66dbb-531">Azure Storage documentation:</span></span>
* [<span data-ttu-id="66dbb-532">Introduction to Azure Storage</span><span class="sxs-lookup"><span data-stu-id="66dbb-532">Introduction to Azure Storage</span></span>](storage-introduction.md)
* [<span data-ttu-id="66dbb-533">How to use Blob storage from .NET</span><span class="sxs-lookup"><span data-stu-id="66dbb-533">How to use Blob storage from .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="66dbb-534">How to use File storage from .NET</span><span class="sxs-lookup"><span data-stu-id="66dbb-534">How to use File storage from .NET</span></span>](storage-dotnet-how-to-use-files.md)
* [<span data-ttu-id="66dbb-535">How to use Table storage from .NET</span><span class="sxs-lookup"><span data-stu-id="66dbb-535">How to use Table storage from .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="66dbb-536">How to create, manage, or delete a storage account</span><span class="sxs-lookup"><span data-stu-id="66dbb-536">How to create, manage, or delete a storage account</span></span>](storage-create-storage-account.md)

### <a name="azure-storage-blog-posts"></a><span data-ttu-id="66dbb-537">Azure Storage blog posts:</span><span class="sxs-lookup"><span data-stu-id="66dbb-537">Azure Storage blog posts:</span></span>
* [<span data-ttu-id="66dbb-538">Introducing Azure Storage Data Movement Library Preview</span><span class="sxs-lookup"><span data-stu-id="66dbb-538">Introducing Azure Storage Data Movement Library Preview</span></span>](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/)
* [<span data-ttu-id="66dbb-539">AzCopy: Introducing synchronous copy and customized content type</span><span class="sxs-lookup"><span data-stu-id="66dbb-539">AzCopy: Introducing synchronous copy and customized content type</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2015/01/13/azcopy-introducing-synchronous-copy-and-customized-content-type.aspx)
* [<span data-ttu-id="66dbb-540">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span><span class="sxs-lookup"><span data-stu-id="66dbb-540">AzCopy: Announcing General Availability of AzCopy 3.0 plus preview release of AzCopy 4.0 with Table and File support</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/10/29/azcopy-announcing-general-availability-of-azcopy-3-0-plus-preview-release-of-azcopy-4-0-with-table-and-file-support.aspx)
* [<span data-ttu-id="66dbb-541">AzCopy: Optimized for Large-Scale Copy Scenarios</span><span class="sxs-lookup"><span data-stu-id="66dbb-541">AzCopy: Optimized for Large-Scale Copy Scenarios</span></span>](http://go.microsoft.com/fwlink/?LinkId=507682)
* [<span data-ttu-id="66dbb-542">AzCopy: Support for read-access geo-redundant storage</span><span class="sxs-lookup"><span data-stu-id="66dbb-542">AzCopy: Support for read-access geo-redundant storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/04/07/azcopy-support-for-read-access-geo-redundant-account.aspx)
* [<span data-ttu-id="66dbb-543">AzCopy: Transfer data with re-startable mode and SAS token</span><span class="sxs-lookup"><span data-stu-id="66dbb-543">AzCopy: Transfer data with re-startable mode and SAS token</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/09/07/azcopy-transfer-data-with-re-startable-mode-and-sas-token.aspx)
* [<span data-ttu-id="66dbb-544">AzCopy: Using cross-account Copy Blob</span><span class="sxs-lookup"><span data-stu-id="66dbb-544">AzCopy: Using cross-account Copy Blob</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2013/04/01/azcopy-using-cross-account-copy-blob.aspx)
* [<span data-ttu-id="66dbb-545">AzCopy: Uploading/downloading files for Azure Blobs</span><span class="sxs-lookup"><span data-stu-id="66dbb-545">AzCopy: Uploading/downloading files for Azure Blobs</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/12/03/azcopy-uploading-downloading-files-for-windows-azure-blobs.aspx)

