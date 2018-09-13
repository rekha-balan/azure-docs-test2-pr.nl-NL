---
title: Sample workflow to prep hard drives for an Azure Import/Export import job | Microsoft Docs
description: See a walkthrough for the complete process of preparing drives for an import job in the Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: ''
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 78d7ce3bbd3205fd995ba331af08d830097c8156
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662866"
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="77677-103">Sample workflow to prepare hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="77677-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="77677-104">This article walks you through the complete process of preparing drives for an import job.</span><span class="sxs-lookup"><span data-stu-id="77677-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="77677-105">Sample data</span><span class="sxs-lookup"><span data-stu-id="77677-105">Sample data</span></span>

<span data-ttu-id="77677-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="77677-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="77677-107">Location</span><span class="sxs-lookup"><span data-stu-id="77677-107">Location</span></span>|<span data-ttu-id="77677-108">Description</span><span class="sxs-lookup"><span data-stu-id="77677-108">Description</span></span>|<span data-ttu-id="77677-109">Data size</span><span class="sxs-lookup"><span data-stu-id="77677-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="77677-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="77677-110">H:\Video\\</span></span> |<span data-ttu-id="77677-111">A collection of videos</span><span class="sxs-lookup"><span data-stu-id="77677-111">A collection of videos</span></span>|<span data-ttu-id="77677-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="77677-112">12 TB</span></span>|
|<span data-ttu-id="77677-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="77677-113">H:\Photo\\</span></span> |<span data-ttu-id="77677-114">A collection of photos</span><span class="sxs-lookup"><span data-stu-id="77677-114">A collection of photos</span></span>|<span data-ttu-id="77677-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="77677-115">30 GB</span></span>|
|<span data-ttu-id="77677-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="77677-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="77677-117">A Blu-Ray™ disk image</span><span class="sxs-lookup"><span data-stu-id="77677-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="77677-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="77677-118">25 GB</span></span>|
|<span data-ttu-id="77677-119">\\\bigshare\john\music\|A collection of music files on a network share</span><span class="sxs-lookup"><span data-stu-id="77677-119">\\\bigshare\john\music\|A collection of music files on a network share</span></span>|<span data-ttu-id="77677-120">10 GB</span><span class="sxs-lookup"><span data-stu-id="77677-120">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="77677-121">Storage account destinations</span><span class="sxs-lookup"><span data-stu-id="77677-121">Storage account destinations</span></span>

<span data-ttu-id="77677-122">The import job will import the data into the following destinations in the storage account:</span><span class="sxs-lookup"><span data-stu-id="77677-122">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="77677-123">Source</span><span class="sxs-lookup"><span data-stu-id="77677-123">Source</span></span>|<span data-ttu-id="77677-124">Destination virtual directory or blob</span><span class="sxs-lookup"><span data-stu-id="77677-124">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="77677-125">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="77677-125">H:\Video\\</span></span> |<span data-ttu-id="77677-126">video/</span><span class="sxs-lookup"><span data-stu-id="77677-126">video/</span></span>|
|<span data-ttu-id="77677-127">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="77677-127">H:\Photo\\</span></span> |<span data-ttu-id="77677-128">photo/</span><span class="sxs-lookup"><span data-stu-id="77677-128">photo/</span></span>|
|<span data-ttu-id="77677-129">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="77677-129">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="77677-130">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="77677-130">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="77677-131">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="77677-131">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="77677-132">music</span><span class="sxs-lookup"><span data-stu-id="77677-132">music</span></span>|

<span data-ttu-id="77677-133">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="77677-133">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="77677-134">Determine hard drive requirements</span><span class="sxs-lookup"><span data-stu-id="77677-134">Determine hard drive requirements</span></span>

<span data-ttu-id="77677-135">Next, to determine how many hard drives are needed, compute the size of the data:</span><span class="sxs-lookup"><span data-stu-id="77677-135">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="77677-136">For this example, two 8TB hard drives should be sufficient.</span><span class="sxs-lookup"><span data-stu-id="77677-136">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="77677-137">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span><span class="sxs-lookup"><span data-stu-id="77677-137">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="77677-138">The tool will distribute data across two hard drives in an optimized way.</span><span class="sxs-lookup"><span data-stu-id="77677-138">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="77677-139">Attach drives and configure the job</span><span class="sxs-lookup"><span data-stu-id="77677-139">Attach drives and configure the job</span></span>
<span data-ttu-id="77677-140">You will attach both disks to the machine and create volumes.</span><span class="sxs-lookup"><span data-stu-id="77677-140">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="77677-141">Then author **dataset.csv** file:</span><span class="sxs-lookup"><span data-stu-id="77677-141">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="77677-142">In addition, you can set the following metadata for all files:</span><span class="sxs-lookup"><span data-stu-id="77677-142">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="77677-143">**UploadMethod:** Windows Azure Import/Export service</span><span class="sxs-lookup"><span data-stu-id="77677-143">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="77677-144">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="77677-144">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="77677-145">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="77677-145">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="77677-146">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span><span class="sxs-lookup"><span data-stu-id="77677-146">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="77677-147">You can also set some properties for the `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="77677-147">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="77677-148">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="77677-148">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="77677-149">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="77677-149">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="77677-150">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="77677-150">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="77677-151">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="77677-151">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="77677-152">Run the Azure Import/Export Tool (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="77677-152">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="77677-153">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span><span class="sxs-lookup"><span data-stu-id="77677-153">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="77677-154">**For the first session:**</span><span class="sxs-lookup"><span data-stu-id="77677-154">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="77677-155">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="77677-155">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="77677-156">**For the second session:**</span><span class="sxs-lookup"><span data-stu-id="77677-156">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="77677-157">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span><span class="sxs-lookup"><span data-stu-id="77677-157">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="77677-158">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="77677-158">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="77677-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="77677-159">Next steps</span></span>

* [<span data-ttu-id="77677-160">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="77677-160">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="77677-161">Quick reference for frequently used commands</span><span class="sxs-lookup"><span data-stu-id="77677-161">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
