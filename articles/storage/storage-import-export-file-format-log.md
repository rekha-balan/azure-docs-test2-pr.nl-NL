---
title: Azure Import/Export log file format | Microsoft Docs
description: Learn about the format of the log files created when steps are executed for an Import/Export service job.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555203"
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="978b6-103">Azure Import/Export service log file format</span><span class="sxs-lookup"><span data-stu-id="978b6-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="978b6-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span><span class="sxs-lookup"><span data-stu-id="978b6-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="978b6-105">There are two logs that may be written by the Import/Export service:</span><span class="sxs-lookup"><span data-stu-id="978b6-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="978b6-106">The error log is always generated in the event of an error.</span><span class="sxs-lookup"><span data-stu-id="978b6-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="978b6-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span><span class="sxs-lookup"><span data-stu-id="978b6-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="978b6-108">Log file location</span><span class="sxs-lookup"><span data-stu-id="978b6-108">Log file location</span></span>  
<span data-ttu-id="978b6-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span><span class="sxs-lookup"><span data-stu-id="978b6-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="978b6-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="978b6-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="978b6-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span><span class="sxs-lookup"><span data-stu-id="978b6-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="978b6-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span><span class="sxs-lookup"><span data-stu-id="978b6-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="978b6-113">The table below shows the possible options:</span><span class="sxs-lookup"><span data-stu-id="978b6-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="978b6-114">Authentication Method</span><span class="sxs-lookup"><span data-stu-id="978b6-114">Authentication Method</span></span>|<span data-ttu-id="978b6-115">Value of `ImportExportStatesPath`Element</span><span class="sxs-lookup"><span data-stu-id="978b6-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="978b6-116">Location of Log Blobs</span><span class="sxs-lookup"><span data-stu-id="978b6-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="978b6-117">Storage account key</span><span class="sxs-lookup"><span data-stu-id="978b6-117">Storage account key</span></span>|<span data-ttu-id="978b6-118">Default value</span><span class="sxs-lookup"><span data-stu-id="978b6-118">Default value</span></span>|<span data-ttu-id="978b6-119">A container named `waimportexport`, which is the default container.</span><span class="sxs-lookup"><span data-stu-id="978b6-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="978b6-120">For example:</span><span class="sxs-lookup"><span data-stu-id="978b6-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="978b6-121">Storage account key</span><span class="sxs-lookup"><span data-stu-id="978b6-121">Storage account key</span></span>|<span data-ttu-id="978b6-122">User-specified value</span><span class="sxs-lookup"><span data-stu-id="978b6-122">User-specified value</span></span>|<span data-ttu-id="978b6-123">A container named by the user.</span><span class="sxs-lookup"><span data-stu-id="978b6-123">A container named by the user.</span></span> <span data-ttu-id="978b6-124">For example:</span><span class="sxs-lookup"><span data-stu-id="978b6-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="978b6-125">Container SAS</span><span class="sxs-lookup"><span data-stu-id="978b6-125">Container SAS</span></span>|<span data-ttu-id="978b6-126">Default value</span><span class="sxs-lookup"><span data-stu-id="978b6-126">Default value</span></span>|<span data-ttu-id="978b6-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span><span class="sxs-lookup"><span data-stu-id="978b6-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="978b6-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="978b6-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="978b6-129">Container SAS</span><span class="sxs-lookup"><span data-stu-id="978b6-129">Container SAS</span></span>|<span data-ttu-id="978b6-130">User-specified value</span><span class="sxs-lookup"><span data-stu-id="978b6-130">User-specified value</span></span>|<span data-ttu-id="978b6-131">A virtual directory named by the user, beneath the container specified in the SAS.</span><span class="sxs-lookup"><span data-stu-id="978b6-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="978b6-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="978b6-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="978b6-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span><span class="sxs-lookup"><span data-stu-id="978b6-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="978b6-134">The logs are available after processing of the drive is complete.</span><span class="sxs-lookup"><span data-stu-id="978b6-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="978b6-135">Log file format</span><span class="sxs-lookup"><span data-stu-id="978b6-135">Log file format</span></span>  
<span data-ttu-id="978b6-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span><span class="sxs-lookup"><span data-stu-id="978b6-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="978b6-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span><span class="sxs-lookup"><span data-stu-id="978b6-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="978b6-138">The verbose log format is shown below.</span><span class="sxs-lookup"><span data-stu-id="978b6-138">The verbose log format is shown below.</span></span> <span data-ttu-id="978b6-139">The error log has the same structure, but filters out successful operations.</span><span class="sxs-lookup"><span data-stu-id="978b6-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="978b6-140">The following table describes the elements of the log file.</span><span class="sxs-lookup"><span data-stu-id="978b6-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="978b6-141">XML Element</span><span class="sxs-lookup"><span data-stu-id="978b6-141">XML Element</span></span>|<span data-ttu-id="978b6-142">Type</span><span class="sxs-lookup"><span data-stu-id="978b6-142">Type</span></span>|<span data-ttu-id="978b6-143">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="978b6-144">XML Element</span><span class="sxs-lookup"><span data-stu-id="978b6-144">XML Element</span></span>|<span data-ttu-id="978b6-145">Represents a drive log.</span><span class="sxs-lookup"><span data-stu-id="978b6-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="978b6-146">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-146">Attribute, String</span></span>|<span data-ttu-id="978b6-147">The version of the log format.</span><span class="sxs-lookup"><span data-stu-id="978b6-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="978b6-148">String</span><span class="sxs-lookup"><span data-stu-id="978b6-148">String</span></span>|<span data-ttu-id="978b6-149">The drive's hardware serial number.</span><span class="sxs-lookup"><span data-stu-id="978b6-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="978b6-150">String</span><span class="sxs-lookup"><span data-stu-id="978b6-150">String</span></span>|<span data-ttu-id="978b6-151">Status of the drive processing.</span><span class="sxs-lookup"><span data-stu-id="978b6-151">Status of the drive processing.</span></span> <span data-ttu-id="978b6-152">See the `Drive Status Codes` table below for more information.</span><span class="sxs-lookup"><span data-stu-id="978b6-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="978b6-153">Nested XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-153">Nested XML element</span></span>|<span data-ttu-id="978b6-154">Represents a blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="978b6-155">String</span><span class="sxs-lookup"><span data-stu-id="978b6-155">String</span></span>|<span data-ttu-id="978b6-156">The URI of the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="978b6-157">String</span><span class="sxs-lookup"><span data-stu-id="978b6-157">String</span></span>|<span data-ttu-id="978b6-158">The relative path to the file on the drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="978b6-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="978b6-159">DateTime</span></span>|<span data-ttu-id="978b6-160">The snapshot version of the blob, for an export job only.</span><span class="sxs-lookup"><span data-stu-id="978b6-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="978b6-161">Integer</span><span class="sxs-lookup"><span data-stu-id="978b6-161">Integer</span></span>|<span data-ttu-id="978b6-162">The total length of the blob in bytes.</span><span class="sxs-lookup"><span data-stu-id="978b6-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="978b6-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="978b6-163">DateTime</span></span>|<span data-ttu-id="978b6-164">The date/time that the blob was last modified, for an export job only.</span><span class="sxs-lookup"><span data-stu-id="978b6-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="978b6-165">String</span><span class="sxs-lookup"><span data-stu-id="978b6-165">String</span></span>|<span data-ttu-id="978b6-166">The import disposition of the blob, for an import job only.</span><span class="sxs-lookup"><span data-stu-id="978b6-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="978b6-167">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-167">Attribute, String</span></span>|<span data-ttu-id="978b6-168">The status of the import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="978b6-169">Nested XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-169">Nested XML element</span></span>|<span data-ttu-id="978b6-170">Represents a list of page ranges for a page blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="978b6-171">XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-171">XML element</span></span>|<span data-ttu-id="978b6-172">Represents a page range.</span><span class="sxs-lookup"><span data-stu-id="978b6-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="978b6-173">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="978b6-173">Attribute, Integer</span></span>|<span data-ttu-id="978b6-174">Starting offset of the page range in the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="978b6-175">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="978b6-175">Attribute, Integer</span></span>|<span data-ttu-id="978b6-176">Length in bytes of the page range.</span><span class="sxs-lookup"><span data-stu-id="978b6-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="978b6-177">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-177">Attribute, String</span></span>|<span data-ttu-id="978b6-178">Base16-encoded MD5 hash of the page range.</span><span class="sxs-lookup"><span data-stu-id="978b6-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="978b6-179">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-179">Attribute, String</span></span>|<span data-ttu-id="978b6-180">Status of processing the page range.</span><span class="sxs-lookup"><span data-stu-id="978b6-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="978b6-181">Nested XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-181">Nested XML element</span></span>|<span data-ttu-id="978b6-182">Represents a list of blocks for a block blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="978b6-183">XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-183">XML element</span></span>|<span data-ttu-id="978b6-184">Represents a block.</span><span class="sxs-lookup"><span data-stu-id="978b6-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="978b6-185">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="978b6-185">Attribute, Integer</span></span>|<span data-ttu-id="978b6-186">Starting offset of the block in the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="978b6-187">Attribute, Integer</span><span class="sxs-lookup"><span data-stu-id="978b6-187">Attribute, Integer</span></span>|<span data-ttu-id="978b6-188">Length in bytes of the block.</span><span class="sxs-lookup"><span data-stu-id="978b6-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="978b6-189">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-189">Attribute, String</span></span>|<span data-ttu-id="978b6-190">The block ID.</span><span class="sxs-lookup"><span data-stu-id="978b6-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="978b6-191">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-191">Attribute, String</span></span>|<span data-ttu-id="978b6-192">Base16-encoded MD5 hash of the block.</span><span class="sxs-lookup"><span data-stu-id="978b6-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="978b6-193">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-193">Attribute, String</span></span>|<span data-ttu-id="978b6-194">Status of processing the block.</span><span class="sxs-lookup"><span data-stu-id="978b6-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="978b6-195">Nested XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-195">Nested XML element</span></span>|<span data-ttu-id="978b6-196">Represents the blob's metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="978b6-197">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-197">Attribute, String</span></span>|<span data-ttu-id="978b6-198">Status of processing of the blob metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="978b6-199">String</span><span class="sxs-lookup"><span data-stu-id="978b6-199">String</span></span>|<span data-ttu-id="978b6-200">Relative path to the global metadata file.</span><span class="sxs-lookup"><span data-stu-id="978b6-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="978b6-201">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-201">Attribute, String</span></span>|<span data-ttu-id="978b6-202">Base16-encoded MD5 hash of the global metadata file.</span><span class="sxs-lookup"><span data-stu-id="978b6-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="978b6-203">String</span><span class="sxs-lookup"><span data-stu-id="978b6-203">String</span></span>|<span data-ttu-id="978b6-204">Relative path to the metadata file.</span><span class="sxs-lookup"><span data-stu-id="978b6-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="978b6-205">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-205">Attribute, String</span></span>|<span data-ttu-id="978b6-206">Base16-encoded MD5 hash of the metadata file.</span><span class="sxs-lookup"><span data-stu-id="978b6-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="978b6-207">Nested XML element</span><span class="sxs-lookup"><span data-stu-id="978b6-207">Nested XML element</span></span>|<span data-ttu-id="978b6-208">Represents the blob properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="978b6-209">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-209">Attribute, String</span></span>|<span data-ttu-id="978b6-210">Status of processing the blob properties, e.g. file not found, completed.</span><span class="sxs-lookup"><span data-stu-id="978b6-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="978b6-211">String</span><span class="sxs-lookup"><span data-stu-id="978b6-211">String</span></span>|<span data-ttu-id="978b6-212">Relative path to the global properties file.</span><span class="sxs-lookup"><span data-stu-id="978b6-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="978b6-213">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-213">Attribute, String</span></span>|<span data-ttu-id="978b6-214">Base16-encoded MD5 hash of the global properties file.</span><span class="sxs-lookup"><span data-stu-id="978b6-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="978b6-215">String</span><span class="sxs-lookup"><span data-stu-id="978b6-215">String</span></span>|<span data-ttu-id="978b6-216">Relative path to the properties file.</span><span class="sxs-lookup"><span data-stu-id="978b6-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="978b6-217">Attribute, String</span><span class="sxs-lookup"><span data-stu-id="978b6-217">Attribute, String</span></span>|<span data-ttu-id="978b6-218">Base16-encoded MD5 hash of the properties file.</span><span class="sxs-lookup"><span data-stu-id="978b6-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="978b6-219">String</span><span class="sxs-lookup"><span data-stu-id="978b6-219">String</span></span>|<span data-ttu-id="978b6-220">Status of processing the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="978b6-221">Drive status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-221">Drive status codes</span></span>  
<span data-ttu-id="978b6-222">The following table lists the status codes for processing a drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="978b6-223">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-223">Status code</span></span>|<span data-ttu-id="978b6-224">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="978b6-225">The drive has finished processing without any errors.</span><span class="sxs-lookup"><span data-stu-id="978b6-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="978b6-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span><span class="sxs-lookup"><span data-stu-id="978b6-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="978b6-227">The drive has finished with errors in one or more blobs or chunks.</span><span class="sxs-lookup"><span data-stu-id="978b6-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="978b6-228">No disk is found on the drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="978b6-229">The first data volume on the disk is not in NTFS format.</span><span class="sxs-lookup"><span data-stu-id="978b6-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="978b6-230">An unknown failure occurred when performing operations on the drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="978b6-231">No BitLocker encryptable volume is found.</span><span class="sxs-lookup"><span data-stu-id="978b6-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="978b6-232">BitLocker is not enabled on the volume.</span><span class="sxs-lookup"><span data-stu-id="978b6-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="978b6-233">The numerical password key protector does not exist on the volume.</span><span class="sxs-lookup"><span data-stu-id="978b6-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="978b6-234">The numerical password provided cannot unlock the volume.</span><span class="sxs-lookup"><span data-stu-id="978b6-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="978b6-235">Unknown failure has happened when trying to unlock the volume.</span><span class="sxs-lookup"><span data-stu-id="978b6-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="978b6-236">An unknown failure occurred while performing BitLocker operations.</span><span class="sxs-lookup"><span data-stu-id="978b6-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="978b6-237">The manifest file name is invalid.</span><span class="sxs-lookup"><span data-stu-id="978b6-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="978b6-238">The manifest file name is too long.</span><span class="sxs-lookup"><span data-stu-id="978b6-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="978b6-239">The manifest file is not found.</span><span class="sxs-lookup"><span data-stu-id="978b6-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="978b6-240">Access to the manifest file is denied.</span><span class="sxs-lookup"><span data-stu-id="978b6-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="978b6-241">The manifest file is corrupted (the content does not match its hash).</span><span class="sxs-lookup"><span data-stu-id="978b6-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="978b6-242">The manifest content does not conform to the required format.</span><span class="sxs-lookup"><span data-stu-id="978b6-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="978b6-243">The drive ID in the manifest file does not match the one read from the drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="978b6-244">A disk I/O failure occurred while reading from the manifest.</span><span class="sxs-lookup"><span data-stu-id="978b6-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="978b6-245">The export blob list blob does not conform to the required format.</span><span class="sxs-lookup"><span data-stu-id="978b6-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="978b6-246">Access to the blobs in the storage account is forbidden.</span><span class="sxs-lookup"><span data-stu-id="978b6-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="978b6-247">This might be due to invalid storage account key or container SAS.</span><span class="sxs-lookup"><span data-stu-id="978b6-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="978b6-248">And internal error occurred while processing the drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="978b6-249">Blob status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-249">Blob status codes</span></span>  
<span data-ttu-id="978b6-250">The following table lists the status codes for processing a blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="978b6-251">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-251">Status code</span></span>|<span data-ttu-id="978b6-252">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="978b6-253">The blob has finished processing without errors.</span><span class="sxs-lookup"><span data-stu-id="978b6-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="978b6-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="978b6-255">The file name is invalid.</span><span class="sxs-lookup"><span data-stu-id="978b6-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="978b6-256">The file name is too long.</span><span class="sxs-lookup"><span data-stu-id="978b6-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="978b6-257">The file is not found.</span><span class="sxs-lookup"><span data-stu-id="978b6-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="978b6-258">Access to the file is denied.</span><span class="sxs-lookup"><span data-stu-id="978b6-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="978b6-259">The Blob service request to access the blob has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="978b6-260">The Blob service request to access the blob is forbidden.</span><span class="sxs-lookup"><span data-stu-id="978b6-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="978b6-261">This might be due to invalid storage account key or container SAS.</span><span class="sxs-lookup"><span data-stu-id="978b6-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="978b6-262">Failed to rename the blob (for an import job) or the file (for an export job).</span><span class="sxs-lookup"><span data-stu-id="978b6-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="978b6-263">An unexpected change has occurred with the blob (for an export job).</span><span class="sxs-lookup"><span data-stu-id="978b6-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="978b6-264">There is a lease present on the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="978b6-265">A disk or network I/O failure occurred while processing the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="978b6-266">An unknown failure occurred while processing the blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="978b6-267">Import disposition status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-267">Import disposition status codes</span></span>  
<span data-ttu-id="978b6-268">The following table lists the status codes for resolving an import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="978b6-269">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-269">Status code</span></span>|<span data-ttu-id="978b6-270">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="978b6-271">The blob has been created.</span><span class="sxs-lookup"><span data-stu-id="978b6-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="978b6-272">The blob has been renamed per rename import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="978b6-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span><span class="sxs-lookup"><span data-stu-id="978b6-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="978b6-274">The blob has been skipped per `no-overwrite` import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="978b6-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="978b6-276">A prior failure has stopped further processing of the import disposition.</span><span class="sxs-lookup"><span data-stu-id="978b6-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="978b6-277">Page range/block status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-277">Page range/block status codes</span></span>  
<span data-ttu-id="978b6-278">The following table lists the status codes for processing a page range or a block.</span><span class="sxs-lookup"><span data-stu-id="978b6-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="978b6-279">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-279">Status code</span></span>|<span data-ttu-id="978b6-280">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="978b6-281">The page range or block has finished processing without any errors.</span><span class="sxs-lookup"><span data-stu-id="978b6-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="978b6-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="978b6-283">The block is uploaded but not committed.</span><span class="sxs-lookup"><span data-stu-id="978b6-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="978b6-284">The page range or block is corrupted (the content does not match its hash).</span><span class="sxs-lookup"><span data-stu-id="978b6-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="978b6-285">An unexpected end of file has been encountered.</span><span class="sxs-lookup"><span data-stu-id="978b6-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="978b6-286">An unexpected end of blob has been encountered.</span><span class="sxs-lookup"><span data-stu-id="978b6-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="978b6-287">The Blob service request to access the page range or block has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="978b6-288">A disk or network I/O failure occurred while processing the page range or block.</span><span class="sxs-lookup"><span data-stu-id="978b6-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="978b6-289">An unknown failure occurred while processing the page range or block.</span><span class="sxs-lookup"><span data-stu-id="978b6-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="978b6-290">A prior failure has stopped further processing of the page range or block.</span><span class="sxs-lookup"><span data-stu-id="978b6-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="978b6-291">Metadata status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-291">Metadata status codes</span></span>  
<span data-ttu-id="978b6-292">The following table lists the status codes for processing blob metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="978b6-293">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-293">Status code</span></span>|<span data-ttu-id="978b6-294">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="978b6-295">The metadata has finished processing without errors.</span><span class="sxs-lookup"><span data-stu-id="978b6-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="978b6-296">The metadata file name is invalid.</span><span class="sxs-lookup"><span data-stu-id="978b6-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="978b6-297">The metadata file name is too long.</span><span class="sxs-lookup"><span data-stu-id="978b6-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="978b6-298">The metadata file is not found.</span><span class="sxs-lookup"><span data-stu-id="978b6-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="978b6-299">Access to the metadata file is denied.</span><span class="sxs-lookup"><span data-stu-id="978b6-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="978b6-300">The metadata file is corrupted (the content does not match its hash).</span><span class="sxs-lookup"><span data-stu-id="978b6-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="978b6-301">The metadata content does not conform to the required format.</span><span class="sxs-lookup"><span data-stu-id="978b6-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="978b6-302">Writing the metadata XML has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="978b6-303">The Blob service request to access the metadata has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="978b6-304">A disk or network I/O failure occurred while processing the metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="978b6-305">An unknown failure occurred while processing the metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="978b6-306">A prior failure has stopped further processing of the metadata.</span><span class="sxs-lookup"><span data-stu-id="978b6-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="978b6-307">Properties status codes</span><span class="sxs-lookup"><span data-stu-id="978b6-307">Properties status codes</span></span>  
<span data-ttu-id="978b6-308">The following table lists the status codes for processing blob properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="978b6-309">Status code</span><span class="sxs-lookup"><span data-stu-id="978b6-309">Status code</span></span>|<span data-ttu-id="978b6-310">Description</span><span class="sxs-lookup"><span data-stu-id="978b6-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="978b6-311">The properties have finished processing without any errors.</span><span class="sxs-lookup"><span data-stu-id="978b6-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="978b6-312">The properties file name is invalid.</span><span class="sxs-lookup"><span data-stu-id="978b6-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="978b6-313">The properties file name is too long.</span><span class="sxs-lookup"><span data-stu-id="978b6-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="978b6-314">The properties file is not found.</span><span class="sxs-lookup"><span data-stu-id="978b6-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="978b6-315">Access to the properties file is denied.</span><span class="sxs-lookup"><span data-stu-id="978b6-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="978b6-316">The properties file is corrupted (the content does not match its hash).</span><span class="sxs-lookup"><span data-stu-id="978b6-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="978b6-317">The properties content does not conform to the required format.</span><span class="sxs-lookup"><span data-stu-id="978b6-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="978b6-318">Writing the properties XML has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="978b6-319">The Blob service request to access the properties has failed.</span><span class="sxs-lookup"><span data-stu-id="978b6-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="978b6-320">A disk or network I/O failure occurred while processing the properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="978b6-321">An unknown failure occurred while processing the properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="978b6-322">A prior failure has stopped further processing of the properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="978b6-323">Sample logs</span><span class="sxs-lookup"><span data-stu-id="978b6-323">Sample logs</span></span>  
<span data-ttu-id="978b6-324">The following is an example of verbose log.</span><span class="sxs-lookup"><span data-stu-id="978b6-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="978b6-325">The corresponding error log is shown below.</span><span class="sxs-lookup"><span data-stu-id="978b6-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="978b6-326">The follow error log for an import job contains an error about a file not found on the import drive.</span><span class="sxs-lookup"><span data-stu-id="978b6-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="978b6-327">Note that the status of subsequent components is `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="978b6-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="978b6-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span><span class="sxs-lookup"><span data-stu-id="978b6-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="978b6-329">Next steps</span><span class="sxs-lookup"><span data-stu-id="978b6-329">Next steps</span></span>
 
* [<span data-ttu-id="978b6-330">Storage Import/Export REST API</span><span class="sxs-lookup"><span data-stu-id="978b6-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
