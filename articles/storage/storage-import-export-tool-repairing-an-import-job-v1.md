---
title: Repairing an Azure Import/Export import job - v1 | Microsoft Docs
description: Learn how to repair an import job that was created and run using the Azure Import/Export service.
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
ms.openlocfilehash: b374eabcbafa6ffe64c639fb6c89be857ecfc221
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540912"
---
# <a name="repairing-an-import-job"></a><span data-ttu-id="bc13f-103">Repairing an import job</span><span class="sxs-lookup"><span data-stu-id="bc13f-103">Repairing an import job</span></span>
<span data-ttu-id="bc13f-104">The Microsoft Azure Import/Export service may fail to copy some of your files or parts of a file to the Windows Azure Blob service.</span><span class="sxs-lookup"><span data-stu-id="bc13f-104">The Microsoft Azure Import/Export service may fail to copy some of your files or parts of a file to the Windows Azure Blob service.</span></span> <span data-ttu-id="bc13f-105">Some reasons for failures include:</span><span class="sxs-lookup"><span data-stu-id="bc13f-105">Some reasons for failures include:</span></span>  
  
-   <span data-ttu-id="bc13f-106">Corrupted files</span><span class="sxs-lookup"><span data-stu-id="bc13f-106">Corrupted files</span></span>  
  
-   <span data-ttu-id="bc13f-107">Damaged drives</span><span class="sxs-lookup"><span data-stu-id="bc13f-107">Damaged drives</span></span>  
  
-   <span data-ttu-id="bc13f-108">The storage account key changed while the file was being transferred.</span><span class="sxs-lookup"><span data-stu-id="bc13f-108">The storage account key changed while the file was being transferred.</span></span>  
  
<span data-ttu-id="bc13f-109">You can run the Microsoft Azure Import/Export Tool with the import job's copy log files, and the tool will upload the missing files (or parts of a file) to your Windows Azure storage account to complete import job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-109">You can run the Microsoft Azure Import/Export Tool with the import job's copy log files, and the tool will upload the missing files (or parts of a file) to your Windows Azure storage account to complete import job.</span></span>  
  
## <a name="repairimport-parameters"></a><span data-ttu-id="bc13f-110">RepairImport parameters</span><span class="sxs-lookup"><span data-stu-id="bc13f-110">RepairImport parameters</span></span>

<span data-ttu-id="bc13f-111">The following parameters can be specified with **RepairImport**:</span><span class="sxs-lookup"><span data-stu-id="bc13f-111">The following parameters can be specified with **RepairImport**:</span></span> 
  
|||  
|-|-|  
|<span data-ttu-id="bc13f-112">**/r:**<RepairFile\></span><span class="sxs-lookup"><span data-stu-id="bc13f-112">**/r:**<RepairFile\></span></span>|<span data-ttu-id="bc13f-113">**Required.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-113">**Required.**</span></span> <span data-ttu-id="bc13f-114">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span><span class="sxs-lookup"><span data-stu-id="bc13f-114">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="bc13f-115">Each drive must have one and only one repair file.</span><span class="sxs-lookup"><span data-stu-id="bc13f-115">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="bc13f-116">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="bc13f-116">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="bc13f-117">To resume an interrupted repair, you should pass in the name of an existing repair file.</span><span class="sxs-lookup"><span data-stu-id="bc13f-117">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="bc13f-118">The repair file corresponding to the target drive must always be specified.</span><span class="sxs-lookup"><span data-stu-id="bc13f-118">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="bc13f-119">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="bc13f-119">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="bc13f-120">**Optional.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-120">**Optional.**</span></span> <span data-ttu-id="bc13f-121">The log directory.</span><span class="sxs-lookup"><span data-stu-id="bc13f-121">The log directory.</span></span> <span data-ttu-id="bc13f-122">Verbose log files will be written to this directory.</span><span class="sxs-lookup"><span data-stu-id="bc13f-122">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="bc13f-123">If no log directory is specified, the current directory will be used as the log directory.</span><span class="sxs-lookup"><span data-stu-id="bc13f-123">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="bc13f-124">**/d:**<TargetDirectories\></span><span class="sxs-lookup"><span data-stu-id="bc13f-124">**/d:**<TargetDirectories\></span></span>|<span data-ttu-id="bc13f-125">**Required.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-125">**Required.**</span></span> <span data-ttu-id="bc13f-126">One or more semicolon-separated directories that contain the original files that were imported.</span><span class="sxs-lookup"><span data-stu-id="bc13f-126">One or more semicolon-separated directories that contain the original files that were imported.</span></span> <span data-ttu-id="bc13f-127">The import drive may also be used, but is not required if alternate locations of original files are available.</span><span class="sxs-lookup"><span data-stu-id="bc13f-127">The import drive may also be used, but is not required if alternate locations of original files are available.</span></span>|  
|<span data-ttu-id="bc13f-128">**/bk:**<BitLockerKey\></span><span class="sxs-lookup"><span data-stu-id="bc13f-128">**/bk:**<BitLockerKey\></span></span>|<span data-ttu-id="bc13f-129">**Optional.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-129">**Optional.**</span></span> <span data-ttu-id="bc13f-130">You should specify the BitLocker key if you want the tool to unlock an encrypted drive where the original files are available.</span><span class="sxs-lookup"><span data-stu-id="bc13f-130">You should specify the BitLocker key if you want the tool to unlock an encrypted drive where the original files are available.</span></span>|  
|<span data-ttu-id="bc13f-131">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="bc13f-131">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="bc13f-132">**Required.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-132">**Required.**</span></span> <span data-ttu-id="bc13f-133">The name of the storage account for the import job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-133">The name of the storage account for the import job.</span></span>|  
|<span data-ttu-id="bc13f-134">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="bc13f-134">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="bc13f-135">**Required** if and only if a container SAS is not specified.</span><span class="sxs-lookup"><span data-stu-id="bc13f-135">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="bc13f-136">The account key for the storage account for the import job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-136">The account key for the storage account for the import job.</span></span>|  
|<span data-ttu-id="bc13f-137">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="bc13f-137">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="bc13f-138">**Required** if and only if the storage account key is not specified.</span><span class="sxs-lookup"><span data-stu-id="bc13f-138">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="bc13f-139">The container SAS for accessing the blobs associated with the import job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-139">The container SAS for accessing the blobs associated with the import job.</span></span>|  
|<span data-ttu-id="bc13f-140">**/CopyLogFile:**<DriveCopyLogFile\></span><span class="sxs-lookup"><span data-stu-id="bc13f-140">**/CopyLogFile:**<DriveCopyLogFile\></span></span>|<span data-ttu-id="bc13f-141">**Required.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-141">**Required.**</span></span> <span data-ttu-id="bc13f-142">Path to the drive copy log file (either verbose log or error log).</span><span class="sxs-lookup"><span data-stu-id="bc13f-142">Path to the drive copy log file (either verbose log or error log).</span></span> <span data-ttu-id="bc13f-143">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-143">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="bc13f-144">The copy log file contains information about failed blobs or files which are to be repaired.</span><span class="sxs-lookup"><span data-stu-id="bc13f-144">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="bc13f-145">**/PathMapFile:**<DrivePathMapFile\></span><span class="sxs-lookup"><span data-stu-id="bc13f-145">**/PathMapFile:**<DrivePathMapFile\></span></span>|<span data-ttu-id="bc13f-146">**Optional.**</span><span class="sxs-lookup"><span data-stu-id="bc13f-146">**Optional.**</span></span> <span data-ttu-id="bc13f-147">Path to a text file that can be used to resolve ambiguities if you have multiple files with the same name that you were importing in the same job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-147">Path to a text file that can be used to resolve ambiguities if you have multiple files with the same name that you were importing in the same job.</span></span> <span data-ttu-id="bc13f-148">The first time the tool is run, it can populate this file with all of the ambiguous names.</span><span class="sxs-lookup"><span data-stu-id="bc13f-148">The first time the tool is run, it can populate this file with all of the ambiguous names.</span></span> <span data-ttu-id="bc13f-149">Subsequent runs of the tool will use this file to resolve the ambiguities.</span><span class="sxs-lookup"><span data-stu-id="bc13f-149">Subsequent runs of the tool will use this file to resolve the ambiguities.</span></span>|  
  
## <a name="using-the-repairimport-command"></a><span data-ttu-id="bc13f-150">Using the RepairImport command</span><span class="sxs-lookup"><span data-stu-id="bc13f-150">Using the RepairImport command</span></span>  
<span data-ttu-id="bc13f-151">To repair import data by streaming the data over the network, you must specify the directories that contain the original files you were importing using the `/d` parameter.</span><span class="sxs-lookup"><span data-stu-id="bc13f-151">To repair import data by streaming the data over the network, you must specify the directories that contain the original files you were importing using the `/d` parameter.</span></span> <span data-ttu-id="bc13f-152">You must also specify the copy log file that you downloaded from your storage account.</span><span class="sxs-lookup"><span data-stu-id="bc13f-152">You must also specify the copy log file that you downloaded from your storage account.</span></span> <span data-ttu-id="bc13f-153">A typical command line to repair an import job with partial failures looks like:</span><span class="sxs-lookup"><span data-stu-id="bc13f-153">A typical command line to repair an import job with partial failures looks like:</span></span>  
  
```  
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log  
```  
  
<span data-ttu-id="bc13f-154">The following is an example of a copy log file.</span><span class="sxs-lookup"><span data-stu-id="bc13f-154">The following is an example of a copy log file.</span></span> <span data-ttu-id="bc13f-155">In this case, one 64K piece of a file was corrupted on the drive that was shipped for the import job.</span><span class="sxs-lookup"><span data-stu-id="bc13f-155">In this case, one 64K piece of a file was corrupted on the drive that was shipped for the import job.</span></span> <span data-ttu-id="bc13f-156">Since this is the only failure indicated, the rest of the blobs in the job were successfully imported.</span><span class="sxs-lookup"><span data-stu-id="bc13f-156">Since this is the only failure indicated, the rest of the blobs in the job were successfully imported.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
 <DriveId>9WM35C2V</DriveId>  
 <Blob Status="CompletedWithErrors">  
 <BlobPath>pictures/animals/koala.jpg</BlobPath>  
 <FilePath>\animals\koala.jpg</FilePath>  
 <Length>163840</Length>  
 <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
 <PageRangeList>  
  <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted" />  
 </PageRangeList>  
 </Blob>  
 <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
<span data-ttu-id="bc13f-157">When this copy log is passed to the Azure Import/Export Tool, the tool will try to finish the import for this file by copying the missing contents across the network.</span><span class="sxs-lookup"><span data-stu-id="bc13f-157">When this copy log is passed to the Azure Import/Export Tool, the tool will try to finish the import for this file by copying the missing contents across the network.</span></span> <span data-ttu-id="bc13f-158">Following the example above, the tool will look for the original file `\animals\koala.jpg` within the two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span><span class="sxs-lookup"><span data-stu-id="bc13f-158">Following the example above, the tool will look for the original file `\animals\koala.jpg` within the two directories `C:\Users\bob\Pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="bc13f-159">If the file `C:\Users\bob\Pictures\animals\koala.jpg` exists, the Azure Import/Export Tool will copy the missing range of data to the corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span><span class="sxs-lookup"><span data-stu-id="bc13f-159">If the file `C:\Users\bob\Pictures\animals\koala.jpg` exists, the Azure Import/Export Tool will copy the missing range of data to the corresponding blob `http://bobmediaaccount.blob.core.windows.net/pictures/animals/koala.jpg`.</span></span>  
  
## <a name="resolving-conflicts-when-using-repairimport"></a><span data-ttu-id="bc13f-160">Resolving conflicts when using RepairImport</span><span class="sxs-lookup"><span data-stu-id="bc13f-160">Resolving conflicts when using RepairImport</span></span>  
<span data-ttu-id="bc13f-161">In some situations, the tool may not be able to find or open the necessary file for one of the following reasons: the file could not be found, the file is not accessible, the file name is ambiguous, or the content of the file is no longer correct.</span><span class="sxs-lookup"><span data-stu-id="bc13f-161">In some situations, the tool may not be able to find or open the necessary file for one of the following reasons: the file could not be found, the file is not accessible, the file name is ambiguous, or the content of the file is no longer correct.</span></span>  
  
<span data-ttu-id="bc13f-162">An ambiguous error could occur if the tool is trying to locate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span><span class="sxs-lookup"><span data-stu-id="bc13f-162">An ambiguous error could occur if the tool is trying to locate `\animals\koala.jpg` and there is a file with that name under both `C:\Users\bob\pictures` and `X:\BobBackup\photos`.</span></span> <span data-ttu-id="bc13f-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on the import job drives.</span><span class="sxs-lookup"><span data-stu-id="bc13f-163">That is, both `C:\Users\bob\pictures\animals\koala.jpg` and `X:\BobBackup\photos\animals\koala.jpg` exist on the import job drives.</span></span>  
  
<span data-ttu-id="bc13f-164">The `/PathMapFile` option will allow you to resolve these errors.</span><span class="sxs-lookup"><span data-stu-id="bc13f-164">The `/PathMapFile` option will allow you to resolve these errors.</span></span> <span data-ttu-id="bc13f-165">You can specify the name of the file which will contains the list of files that the tool was not able to correctly identify.</span><span class="sxs-lookup"><span data-stu-id="bc13f-165">You can specify the name of the file which will contains the list of files that the tool was not able to correctly identify.</span></span> <span data-ttu-id="bc13f-166">The following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span><span class="sxs-lookup"><span data-stu-id="bc13f-166">The following is an example command line that would populate `9WM35C2V_pathmap.txt`:</span></span>  
  
```
WAImportExport.exe RepairImport /r:C:\WAImportExport\9WM35C2V.rep /d:C:\Users\bob\Pictures;X:\BobBackup\photos /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C2V.log /PathMapFile:C:\WAImportExport\9WM35C2V_pathmap.txt  
```
  
<span data-ttu-id="bc13f-167">The tool will then write the problematic file paths to `9WM35C2V_pathmap.txt`, one on each line.</span><span class="sxs-lookup"><span data-stu-id="bc13f-167">The tool will then write the problematic file paths to `9WM35C2V_pathmap.txt`, one on each line.</span></span> <span data-ttu-id="bc13f-168">For instance, the file may contain the following entries after running the command:</span><span class="sxs-lookup"><span data-stu-id="bc13f-168">For instance, the file may contain the following entries after running the command:</span></span>  
 
```
\animals\koala.jpg  
\animals\kangaroo.jpg  
```
  
 <span data-ttu-id="bc13f-169">For each file in the list, you should attempt to locate and open the file to ensure it is available to the tool.</span><span class="sxs-lookup"><span data-stu-id="bc13f-169">For each file in the list, you should attempt to locate and open the file to ensure it is available to the tool.</span></span> <span data-ttu-id="bc13f-170">If you wish to tell the tool explicitly where to find a file, you can modify the path map file and add the path to each file on the same line, separated by a tab character:</span><span class="sxs-lookup"><span data-stu-id="bc13f-170">If you wish to tell the tool explicitly where to find a file, you can modify the path map file and add the path to each file on the same line, separated by a tab character:</span></span>  
  
```
\animals\koala.jpg           C:\Users\bob\Pictures\animals\koala.jpg  
\animals\kangaroo.jpg        X:\BobBackup\photos\animals\kangaroo.jpg  
```
  
<span data-ttu-id="bc13f-171">After making the necessary files available to the tool, or updating the path map file, you can rerun the tool to complete the import process.</span><span class="sxs-lookup"><span data-stu-id="bc13f-171">After making the necessary files available to the tool, or updating the path map file, you can rerun the tool to complete the import process.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bc13f-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc13f-172">Next steps</span></span>
 
* [<span data-ttu-id="bc13f-173">Setting Up the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="bc13f-173">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="bc13f-174">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="bc13f-174">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="bc13f-175">Reviewing job status with copy log files</span><span class="sxs-lookup"><span data-stu-id="bc13f-175">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="bc13f-176">Repairing an export job</span><span class="sxs-lookup"><span data-stu-id="bc13f-176">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="bc13f-177">Troubleshooting the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="bc13f-177">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
