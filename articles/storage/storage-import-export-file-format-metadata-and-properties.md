---
title: Azure Import/Export metadata and properties file format | Microsoft Docs
description: Learn how to specify metadata and properties for one or more blobs that are part of an import or export job.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e454140ee0116353f27dc34131fe30041b10e3a3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540644"
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="96ab8-103">Azure Import/Export service metadata and properties file format</span><span class="sxs-lookup"><span data-stu-id="96ab8-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="96ab8-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span><span class="sxs-lookup"><span data-stu-id="96ab8-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="96ab8-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span><span class="sxs-lookup"><span data-stu-id="96ab8-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="96ab8-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span><span class="sxs-lookup"><span data-stu-id="96ab8-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="96ab8-107">Metadata file format</span><span class="sxs-lookup"><span data-stu-id="96ab8-107">Metadata file format</span></span>  
<span data-ttu-id="96ab8-108">The format of a metadata file is as follows:</span><span class="sxs-lookup"><span data-stu-id="96ab8-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="96ab8-109">XML Element</span><span class="sxs-lookup"><span data-stu-id="96ab8-109">XML Element</span></span>|<span data-ttu-id="96ab8-110">Type</span><span class="sxs-lookup"><span data-stu-id="96ab8-110">Type</span></span>|<span data-ttu-id="96ab8-111">Description</span><span class="sxs-lookup"><span data-stu-id="96ab8-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="96ab8-112">Root element</span><span class="sxs-lookup"><span data-stu-id="96ab8-112">Root element</span></span>|<span data-ttu-id="96ab8-113">The root element of the metadata file.</span><span class="sxs-lookup"><span data-stu-id="96ab8-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="96ab8-114">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-114">String</span></span>|<span data-ttu-id="96ab8-115">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-115">Optional.</span></span> <span data-ttu-id="96ab8-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span><span class="sxs-lookup"><span data-stu-id="96ab8-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="96ab8-117">Properties file format</span><span class="sxs-lookup"><span data-stu-id="96ab8-117">Properties file format</span></span>  
<span data-ttu-id="96ab8-118">The format of a properties file is as follows:</span><span class="sxs-lookup"><span data-stu-id="96ab8-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="96ab8-119">XML Element</span><span class="sxs-lookup"><span data-stu-id="96ab8-119">XML Element</span></span>|<span data-ttu-id="96ab8-120">Type</span><span class="sxs-lookup"><span data-stu-id="96ab8-120">Type</span></span>|<span data-ttu-id="96ab8-121">Description</span><span class="sxs-lookup"><span data-stu-id="96ab8-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="96ab8-122">Root element</span><span class="sxs-lookup"><span data-stu-id="96ab8-122">Root element</span></span>|<span data-ttu-id="96ab8-123">The root element of the properties file.</span><span class="sxs-lookup"><span data-stu-id="96ab8-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="96ab8-124">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-124">String</span></span>|<span data-ttu-id="96ab8-125">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-125">Optional.</span></span> <span data-ttu-id="96ab8-126">The last-modified time for the blob.</span><span class="sxs-lookup"><span data-stu-id="96ab8-126">The last-modified time for the blob.</span></span> <span data-ttu-id="96ab8-127">For export jobs only.</span><span class="sxs-lookup"><span data-stu-id="96ab8-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="96ab8-128">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-128">String</span></span>|<span data-ttu-id="96ab8-129">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-129">Optional.</span></span> <span data-ttu-id="96ab8-130">The blob's ETag value.</span><span class="sxs-lookup"><span data-stu-id="96ab8-130">The blob's ETag value.</span></span> <span data-ttu-id="96ab8-131">For export jobs only.</span><span class="sxs-lookup"><span data-stu-id="96ab8-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="96ab8-132">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-132">String</span></span>|<span data-ttu-id="96ab8-133">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-133">Optional.</span></span> <span data-ttu-id="96ab8-134">The size of the blob in bytes.</span><span class="sxs-lookup"><span data-stu-id="96ab8-134">The size of the blob in bytes.</span></span> <span data-ttu-id="96ab8-135">For export jobs only.</span><span class="sxs-lookup"><span data-stu-id="96ab8-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="96ab8-136">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-136">String</span></span>|<span data-ttu-id="96ab8-137">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-137">Optional.</span></span> <span data-ttu-id="96ab8-138">The content type of the blob.</span><span class="sxs-lookup"><span data-stu-id="96ab8-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="96ab8-139">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-139">String</span></span>|<span data-ttu-id="96ab8-140">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-140">Optional.</span></span> <span data-ttu-id="96ab8-141">The blob's MD5 hash.</span><span class="sxs-lookup"><span data-stu-id="96ab8-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="96ab8-142">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-142">String</span></span>|<span data-ttu-id="96ab8-143">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-143">Optional.</span></span> <span data-ttu-id="96ab8-144">The blob's content encoding.</span><span class="sxs-lookup"><span data-stu-id="96ab8-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="96ab8-145">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-145">String</span></span>|<span data-ttu-id="96ab8-146">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-146">Optional.</span></span> <span data-ttu-id="96ab8-147">The blob's content language.</span><span class="sxs-lookup"><span data-stu-id="96ab8-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="96ab8-148">String</span><span class="sxs-lookup"><span data-stu-id="96ab8-148">String</span></span>|<span data-ttu-id="96ab8-149">Optional.</span><span class="sxs-lookup"><span data-stu-id="96ab8-149">Optional.</span></span> <span data-ttu-id="96ab8-150">The cache control string for the blob.</span><span class="sxs-lookup"><span data-stu-id="96ab8-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="96ab8-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="96ab8-151">Next steps</span></span>

<span data-ttu-id="96ab8-152">See [Set blob properties](/rest/api/storageservices/fileservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/fileservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/fileservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span><span class="sxs-lookup"><span data-stu-id="96ab8-152">See [Set blob properties](/rest/api/storageservices/fileservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/fileservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/fileservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
