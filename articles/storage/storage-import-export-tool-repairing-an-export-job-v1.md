---
title: Repairing an Azure Import/Export export job - v1 | Microsoft Docs
description: Learn how to repair an export job that was created and run using the Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563403"
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="87b65-103">Repairing an export job</span><span class="sxs-lookup"><span data-stu-id="87b65-103">Repairing an export job</span></span>
<span data-ttu-id="87b65-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span><span class="sxs-lookup"><span data-stu-id="87b65-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="87b65-105">Download any files that the Azure Import/Export service was unable to export.</span><span class="sxs-lookup"><span data-stu-id="87b65-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="87b65-106">Validate that the files on the drive were correctly exported.</span><span class="sxs-lookup"><span data-stu-id="87b65-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="87b65-107">You must have connectivity to Azure Storage to use this functionality.</span><span class="sxs-lookup"><span data-stu-id="87b65-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="87b65-108">The command for repairing an import job is **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="87b65-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="87b65-109">RepairExport parameters</span><span class="sxs-lookup"><span data-stu-id="87b65-109">RepairExport parameters</span></span>

<span data-ttu-id="87b65-110">The following parameters can be specified with **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="87b65-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="87b65-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="87b65-111">Parameter</span></span>|<span data-ttu-id="87b65-112">Description</span><span class="sxs-lookup"><span data-stu-id="87b65-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="87b65-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="87b65-114">Required.</span><span class="sxs-lookup"><span data-stu-id="87b65-114">Required.</span></span> <span data-ttu-id="87b65-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span><span class="sxs-lookup"><span data-stu-id="87b65-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="87b65-116">Each drive must have one and only one repair file.</span><span class="sxs-lookup"><span data-stu-id="87b65-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="87b65-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="87b65-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="87b65-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span><span class="sxs-lookup"><span data-stu-id="87b65-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="87b65-119">The repair file corresponding to the target drive must always be specified.</span><span class="sxs-lookup"><span data-stu-id="87b65-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="87b65-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="87b65-121">Optional.</span><span class="sxs-lookup"><span data-stu-id="87b65-121">Optional.</span></span> <span data-ttu-id="87b65-122">The log directory.</span><span class="sxs-lookup"><span data-stu-id="87b65-122">The log directory.</span></span> <span data-ttu-id="87b65-123">Verbose log files will be written to this directory.</span><span class="sxs-lookup"><span data-stu-id="87b65-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="87b65-124">If no log directory is specified, the current directory will be used as the log directory.</span><span class="sxs-lookup"><span data-stu-id="87b65-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="87b65-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="87b65-126">Required.</span><span class="sxs-lookup"><span data-stu-id="87b65-126">Required.</span></span> <span data-ttu-id="87b65-127">The directory to validate and repair.</span><span class="sxs-lookup"><span data-stu-id="87b65-127">The directory to validate and repair.</span></span> <span data-ttu-id="87b65-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span><span class="sxs-lookup"><span data-stu-id="87b65-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="87b65-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="87b65-130">Optional.</span><span class="sxs-lookup"><span data-stu-id="87b65-130">Optional.</span></span> <span data-ttu-id="87b65-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span><span class="sxs-lookup"><span data-stu-id="87b65-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="87b65-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="87b65-133">Required.</span><span class="sxs-lookup"><span data-stu-id="87b65-133">Required.</span></span> <span data-ttu-id="87b65-134">The name of the storage account for the export job.</span><span class="sxs-lookup"><span data-stu-id="87b65-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="87b65-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="87b65-136">**Required** if and only if a container SAS is not specified.</span><span class="sxs-lookup"><span data-stu-id="87b65-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="87b65-137">The account key for the storage account for the export job.</span><span class="sxs-lookup"><span data-stu-id="87b65-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="87b65-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="87b65-139">**Required** if and only if the storage account key is not specified.</span><span class="sxs-lookup"><span data-stu-id="87b65-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="87b65-140">The container SAS for accessing the blobs associated with the export job.</span><span class="sxs-lookup"><span data-stu-id="87b65-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="87b65-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="87b65-142">Required.</span><span class="sxs-lookup"><span data-stu-id="87b65-142">Required.</span></span> <span data-ttu-id="87b65-143">The path to the drive copy log file.</span><span class="sxs-lookup"><span data-stu-id="87b65-143">The path to the drive copy log file.</span></span> <span data-ttu-id="87b65-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span><span class="sxs-lookup"><span data-stu-id="87b65-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="87b65-145">The copy log file contains information about failed blobs or files which are to be repaired.</span><span class="sxs-lookup"><span data-stu-id="87b65-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="87b65-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="87b65-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="87b65-147">Optional.</span><span class="sxs-lookup"><span data-stu-id="87b65-147">Optional.</span></span> <span data-ttu-id="87b65-148">The path to the export drive's manifest file.</span><span class="sxs-lookup"><span data-stu-id="87b65-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="87b65-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span><span class="sxs-lookup"><span data-stu-id="87b65-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="87b65-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span><span class="sxs-lookup"><span data-stu-id="87b65-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="87b65-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span><span class="sxs-lookup"><span data-stu-id="87b65-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="87b65-152">Using RepairExport mode to correct failed exports</span><span class="sxs-lookup"><span data-stu-id="87b65-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="87b65-153">You can use the Azure Import/Export Tool to download files that failed to export.</span><span class="sxs-lookup"><span data-stu-id="87b65-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="87b65-154">The copy log file will contain a list of files that failed to export.</span><span class="sxs-lookup"><span data-stu-id="87b65-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="87b65-155">The causes of export failures include the following possibilities:</span><span class="sxs-lookup"><span data-stu-id="87b65-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="87b65-156">Damaged drives</span><span class="sxs-lookup"><span data-stu-id="87b65-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="87b65-157">The storage account key changed during the transfer process</span><span class="sxs-lookup"><span data-stu-id="87b65-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="87b65-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span><span class="sxs-lookup"><span data-stu-id="87b65-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="87b65-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span><span class="sxs-lookup"><span data-stu-id="87b65-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="87b65-160">You also need to specify the path to the drive's copy log file that you downloaded.</span><span class="sxs-lookup"><span data-stu-id="87b65-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="87b65-161">The following command line example below runs the tool to repair any files that failed to export:</span><span class="sxs-lookup"><span data-stu-id="87b65-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="87b65-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span><span class="sxs-lookup"><span data-stu-id="87b65-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="87b65-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span><span class="sxs-lookup"><span data-stu-id="87b65-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="87b65-164">The other components of the file downloaded successfully, and the file length was correctly set.</span><span class="sxs-lookup"><span data-stu-id="87b65-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="87b65-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span><span class="sxs-lookup"><span data-stu-id="87b65-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="87b65-166">Using RepairExport to validate drive contents</span><span class="sxs-lookup"><span data-stu-id="87b65-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="87b65-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span><span class="sxs-lookup"><span data-stu-id="87b65-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="87b65-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span><span class="sxs-lookup"><span data-stu-id="87b65-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="87b65-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span><span class="sxs-lookup"><span data-stu-id="87b65-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="87b65-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span><span class="sxs-lookup"><span data-stu-id="87b65-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="87b65-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span><span class="sxs-lookup"><span data-stu-id="87b65-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="87b65-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span><span class="sxs-lookup"><span data-stu-id="87b65-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="87b65-173">The following is an example of a manifest file:</span><span class="sxs-lookup"><span data-stu-id="87b65-173">The following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="87b65-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span><span class="sxs-lookup"><span data-stu-id="87b65-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="87b65-175">For the manifest above, it will go through the following components.</span><span class="sxs-lookup"><span data-stu-id="87b65-175">For the manifest above, it will go through the following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="87b65-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span><span class="sxs-lookup"><span data-stu-id="87b65-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="87b65-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="87b65-177">Next steps</span></span>
 
* [<span data-ttu-id="87b65-178">Setting Up the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="87b65-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="87b65-179">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="87b65-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="87b65-180">Reviewing job status with copy log files</span><span class="sxs-lookup"><span data-stu-id="87b65-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="87b65-181">Repairing an import job</span><span class="sxs-lookup"><span data-stu-id="87b65-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="87b65-182">Troubleshooting the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="87b65-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
