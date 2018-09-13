---
title: Setting properties and metadata using Azure Import/Export | Microsoft Docs
description: Learn how to specify properties and metadata to be set on the destination blobs when running the Azure Import/Export Tool to prepare your drives.
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549109"
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="45cbf-103">Setting properties and metadata during the import process</span><span class="sxs-lookup"><span data-stu-id="45cbf-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="45cbf-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span><span class="sxs-lookup"><span data-stu-id="45cbf-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="45cbf-105">Follow these steps:</span><span class="sxs-lookup"><span data-stu-id="45cbf-105">Follow these steps:</span></span>

1.  <span data-ttu-id="45cbf-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span><span class="sxs-lookup"><span data-stu-id="45cbf-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="45cbf-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span><span class="sxs-lookup"><span data-stu-id="45cbf-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="45cbf-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span><span class="sxs-lookup"><span data-stu-id="45cbf-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="45cbf-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span><span class="sxs-lookup"><span data-stu-id="45cbf-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="45cbf-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span><span class="sxs-lookup"><span data-stu-id="45cbf-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="45cbf-111">Specify blob properties in a text file</span><span class="sxs-lookup"><span data-stu-id="45cbf-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="45cbf-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span><span class="sxs-lookup"><span data-stu-id="45cbf-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="45cbf-113">Here's an example that specifies some property values:</span><span class="sxs-lookup"><span data-stu-id="45cbf-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="45cbf-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="45cbf-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="45cbf-115">Specify blob metadata in a text file</span><span class="sxs-lookup"><span data-stu-id="45cbf-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="45cbf-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span><span class="sxs-lookup"><span data-stu-id="45cbf-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="45cbf-117">Here's an example that specifies some metadata values:</span><span class="sxs-lookup"><span data-stu-id="45cbf-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="45cbf-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="45cbf-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="45cbf-119">Add the path to properties and metadata files in dataset.csv</span><span class="sxs-lookup"><span data-stu-id="45cbf-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="45cbf-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="45cbf-120">Next steps</span></span>

* [<span data-ttu-id="45cbf-121">Import/Export service metadata and properties file format</span><span class="sxs-lookup"><span data-stu-id="45cbf-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
