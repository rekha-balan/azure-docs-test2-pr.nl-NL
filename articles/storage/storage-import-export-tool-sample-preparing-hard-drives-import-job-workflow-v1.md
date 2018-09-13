---
title: Sample workflow to prep hard drives for an Azure Import/Export import job - v1 | Microsoft Docs
description: See a walkthrough for the complete process of preparing drives for an import job in the Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 313f8c1f3962a943b4c98c530c324ff28aa84c10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556016"
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="a5821-103">Sample workflow to prepare hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="a5821-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="a5821-104">This topic walks you through the complete process of preparing drives for an import job.</span><span class="sxs-lookup"><span data-stu-id="a5821-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="a5821-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="a5821-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="a5821-106">Location</span><span class="sxs-lookup"><span data-stu-id="a5821-106">Location</span></span>|<span data-ttu-id="a5821-107">Description</span><span class="sxs-lookup"><span data-stu-id="a5821-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="a5821-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="a5821-108">H:\Video</span></span>|<span data-ttu-id="a5821-109">A collection of videos, 5 TB in total.</span><span class="sxs-lookup"><span data-stu-id="a5821-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="a5821-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a5821-110">H:\Photo</span></span>|<span data-ttu-id="a5821-111">A collection of photos, 30 GB in total.</span><span class="sxs-lookup"><span data-stu-id="a5821-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="a5821-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a5821-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a5821-113">A Blu-Ray™ disk image, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="a5821-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="a5821-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a5821-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="a5821-115">A collection of music files on a network share, 10 GB in total.</span><span class="sxs-lookup"><span data-stu-id="a5821-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="a5821-116">The import job will import this data into the following destinations in the storage account:</span><span class="sxs-lookup"><span data-stu-id="a5821-116">The import job will import this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="a5821-117">Source</span><span class="sxs-lookup"><span data-stu-id="a5821-117">Source</span></span>|<span data-ttu-id="a5821-118">Destination virtual directory or blob</span><span class="sxs-lookup"><span data-stu-id="a5821-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="a5821-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="a5821-119">H:\Video</span></span>|https://mystorageaccount.blob.core.windows.net/video|  
|<span data-ttu-id="a5821-120">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a5821-120">H:\Photo</span></span>|https://mystorageaccount.blob.core.windows.net/photo|  
|<span data-ttu-id="a5821-121">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a5821-121">K:\Temp\FavoriteMovie.ISO</span></span>|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|<span data-ttu-id="a5821-122">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a5821-122">\\\bigshare\john\music</span></span>|https://mystorageaccount.blob.core.windows.net/music|  
  
<span data-ttu-id="a5821-123">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="a5821-123">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="a5821-124">Next, to determine how many hard drives are needed, compute the size of the data:</span><span class="sxs-lookup"><span data-stu-id="a5821-124">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="a5821-125">For this example, two 3TB hard drives should be sufficient.</span><span class="sxs-lookup"><span data-stu-id="a5821-125">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="a5821-126">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="a5821-126">However, since the source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary to break `H:\Video` into two smaller directories before running the Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="a5821-127">This step yields the following source directories:</span><span class="sxs-lookup"><span data-stu-id="a5821-127">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="a5821-128">Location</span><span class="sxs-lookup"><span data-stu-id="a5821-128">Location</span></span>|<span data-ttu-id="a5821-129">Size</span><span class="sxs-lookup"><span data-stu-id="a5821-129">Size</span></span>|<span data-ttu-id="a5821-130">Destination virtual directory or blob</span><span class="sxs-lookup"><span data-stu-id="a5821-130">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="a5821-131">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="a5821-131">H:\Video1</span></span>|<span data-ttu-id="a5821-132">2.5TB</span><span class="sxs-lookup"><span data-stu-id="a5821-132">2.5TB</span></span>|https://mystorageaccount.blob.core.windows.net/video|  
|<span data-ttu-id="a5821-133">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="a5821-133">H:\Video2</span></span>|<span data-ttu-id="a5821-134">2.5TB</span><span class="sxs-lookup"><span data-stu-id="a5821-134">2.5TB</span></span>|https://mystorageaccount.blob.core.windows.net/video|  
|<span data-ttu-id="a5821-135">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a5821-135">H:\Photo</span></span>|<span data-ttu-id="a5821-136">30GB</span><span class="sxs-lookup"><span data-stu-id="a5821-136">30GB</span></span>|https://mystorageaccount.blob.core.windows.net/photo|  
|<span data-ttu-id="a5821-137">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a5821-137">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="a5821-138">25GB</span><span class="sxs-lookup"><span data-stu-id="a5821-138">25GB</span></span>|https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO|  
|<span data-ttu-id="a5821-139">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a5821-139">\\\bigshare\john\music</span></span>|<span data-ttu-id="a5821-140">10GB</span><span class="sxs-lookup"><span data-stu-id="a5821-140">10GB</span></span>|https://mystorageaccount.blob.core.windows.net/music|  
  
 <span data-ttu-id="a5821-141">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span><span class="sxs-lookup"><span data-stu-id="a5821-141">Note that even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="a5821-142">This way, all video files are maintained under a single `video` container in the storage account.</span><span class="sxs-lookup"><span data-stu-id="a5821-142">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="a5821-143">Next, the above source directories are evenly distributed to the two hard drives:</span><span class="sxs-lookup"><span data-stu-id="a5821-143">Next, the above source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="a5821-144">Hard drive</span><span class="sxs-lookup"><span data-stu-id="a5821-144">Hard drive</span></span>|<span data-ttu-id="a5821-145">Source directories</span><span class="sxs-lookup"><span data-stu-id="a5821-145">Source directories</span></span>|<span data-ttu-id="a5821-146">Total size</span><span class="sxs-lookup"><span data-stu-id="a5821-146">Total size</span></span>|  
|<span data-ttu-id="a5821-147">First Drive</span><span class="sxs-lookup"><span data-stu-id="a5821-147">First Drive</span></span>|<span data-ttu-id="a5821-148">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="a5821-148">H:\Video1</span></span>|<span data-ttu-id="a5821-149">2.5TB + 30GB</span><span class="sxs-lookup"><span data-stu-id="a5821-149">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="a5821-150">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="a5821-150">H:\Photo</span></span>||  
|<span data-ttu-id="a5821-151">Second Drive</span><span class="sxs-lookup"><span data-stu-id="a5821-151">Second Drive</span></span>|<span data-ttu-id="a5821-152">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="a5821-152">H:\Video2</span></span>|<span data-ttu-id="a5821-153">2.5TB + 35GB</span><span class="sxs-lookup"><span data-stu-id="a5821-153">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="a5821-154">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="a5821-154">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="a5821-155">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="a5821-155">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="a5821-156">In addition, you can set the following metadata for all files:</span><span class="sxs-lookup"><span data-stu-id="a5821-156">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="a5821-157">**UploadMethod:** Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="a5821-157">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="a5821-158">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="a5821-158">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="a5821-159">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="a5821-159">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="a5821-160">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span><span class="sxs-lookup"><span data-stu-id="a5821-160">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="a5821-161">You can also set some properties for the `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="a5821-161">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="a5821-162">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="a5821-162">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="a5821-163">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="a5821-163">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="a5821-164">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="a5821-164">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="a5821-165">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="a5821-165">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="a5821-166">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span><span class="sxs-lookup"><span data-stu-id="a5821-166">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="a5821-167">Note that:</span><span class="sxs-lookup"><span data-stu-id="a5821-167">Note that:</span></span>  
  
-   <span data-ttu-id="a5821-168">The first drive is mounted as drive X.</span><span class="sxs-lookup"><span data-stu-id="a5821-168">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="a5821-169">The second drive is mounted as drive Y.</span><span class="sxs-lookup"><span data-stu-id="a5821-169">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="a5821-170">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="a5821-170">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="a5821-171">Preparing disk for import when data is pre-loaded</span><span class="sxs-lookup"><span data-stu-id="a5821-171">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="a5821-172">If the data to be imported is already present on the disk, use the flag /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="a5821-172">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="a5821-173">Value of /t and /srcdir both should point to the disk being prepared for import.</span><span class="sxs-lookup"><span data-stu-id="a5821-173">Value of /t and /srcdir both should point to the disk being prepared for import.</span></span> <span data-ttu-id="a5821-174">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span><span class="sxs-lookup"><span data-stu-id="a5821-174">If not all the data on the disk needs to go to the same destination virtual directory or root of the storage account, run the same command for each directory separately keeping the value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="a5821-175">Do not specify /format as it will wipe the data on the disk.</span><span class="sxs-lookup"><span data-stu-id="a5821-175">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="a5821-176">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span><span class="sxs-lookup"><span data-stu-id="a5821-176">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="a5821-177">Copy sessions - first drive</span><span class="sxs-lookup"><span data-stu-id="a5821-177">Copy sessions - first drive</span></span>

<span data-ttu-id="a5821-178">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span><span class="sxs-lookup"><span data-stu-id="a5821-178">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="a5821-179">**First copy session**</span><span class="sxs-lookup"><span data-stu-id="a5821-179">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="a5821-180">**Second copy session**</span><span class="sxs-lookup"><span data-stu-id="a5821-180">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="a5821-181">Copy sessions - second drive</span><span class="sxs-lookup"><span data-stu-id="a5821-181">Copy sessions - second drive</span></span>
 
<span data-ttu-id="a5821-182">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span><span class="sxs-lookup"><span data-stu-id="a5821-182">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="a5821-183">**First copy session**</span><span class="sxs-lookup"><span data-stu-id="a5821-183">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="a5821-184">**Second copy session**</span><span class="sxs-lookup"><span data-stu-id="a5821-184">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="a5821-185">**Third copy session**</span><span class="sxs-lookup"><span data-stu-id="a5821-185">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="a5821-186">Copy session completion</span><span class="sxs-lookup"><span data-stu-id="a5821-186">Copy session completion</span></span>

<span data-ttu-id="a5821-187">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span><span class="sxs-lookup"><span data-stu-id="a5821-187">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="a5821-188">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="a5821-188">You'll upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="a5821-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5821-189">Next steps</span></span>

* [<span data-ttu-id="a5821-190">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="a5821-190">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="a5821-191">Quick reference for frequently used commands</span><span class="sxs-lookup"><span data-stu-id="a5821-191">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
