---
title: Setting properties and metadata using Azure Import/Export - v1 | Microsoft Docs
description: Learn how to specify properties and metadata to be set on the destination blobs when running the Azure Import/Export Tool to prepare your drives. This refers to v1 of the Import/Export Tool.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 6455ce57572f9ec36d0ebae88c1ddd9f40f237bf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550995"
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="9d178-104">Setting properties and metadata during the import process</span><span class="sxs-lookup"><span data-stu-id="9d178-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="9d178-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span><span class="sxs-lookup"><span data-stu-id="9d178-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="9d178-106">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="9d178-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="9d178-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span><span class="sxs-lookup"><span data-stu-id="9d178-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="9d178-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span><span class="sxs-lookup"><span data-stu-id="9d178-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="9d178-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span><span class="sxs-lookup"><span data-stu-id="9d178-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="9d178-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span><span class="sxs-lookup"><span data-stu-id="9d178-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="9d178-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span><span class="sxs-lookup"><span data-stu-id="9d178-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="9d178-112">Specify Blob Properties in a Text File</span><span class="sxs-lookup"><span data-stu-id="9d178-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="9d178-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span><span class="sxs-lookup"><span data-stu-id="9d178-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="9d178-114">Here's an example that specifies some property values:</span><span class="sxs-lookup"><span data-stu-id="9d178-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="9d178-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="9d178-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="9d178-116">Specify Blob Metadata in a Text File</span><span class="sxs-lookup"><span data-stu-id="9d178-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="9d178-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span><span class="sxs-lookup"><span data-stu-id="9d178-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="9d178-118">Here's an example that specifies some metadata values:</span><span class="sxs-lookup"><span data-stu-id="9d178-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="9d178-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="9d178-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="9d178-120">Create a Copy Session Including the Properties or Metadata Files</span><span class="sxs-lookup"><span data-stu-id="9d178-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="9d178-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="9d178-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="9d178-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="9d178-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="9d178-123">Here's an example that specifies both files:</span><span class="sxs-lookup"><span data-stu-id="9d178-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="9d178-124">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d178-124">Next steps</span></span>

* [<span data-ttu-id="9d178-125">Import/Export service metadata and properties file format</span><span class="sxs-lookup"><span data-stu-id="9d178-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
