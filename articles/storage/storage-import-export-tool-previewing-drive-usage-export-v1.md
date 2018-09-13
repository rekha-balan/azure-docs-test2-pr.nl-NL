---
title: Previewing drive usage for an Azure Import/Export export job - v1 | Microsoft Docs
description: Learn how to preview the list of blobs you've selected for an export job in the Azure Import/Export service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7bf74247090f91e17f81a9bc98ebfa78334c8c10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671915"
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="2b4e5-103">Previewing drive usage for an export job</span><span class="sxs-lookup"><span data-stu-id="2b4e5-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="2b4e5-104">Before you create an export job, you need to choose a set of blobs to be exported.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="2b4e5-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="2b4e5-106">Next, you need to determine how many drives you need to send.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="2b4e5-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="2b4e5-108">Command-line parameters</span><span class="sxs-lookup"><span data-stu-id="2b4e5-108">Command-line parameters</span></span>

<span data-ttu-id="2b4e5-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="2b4e5-110">Command-line parameter</span><span class="sxs-lookup"><span data-stu-id="2b4e5-110">Command-line parameter</span></span>|<span data-ttu-id="2b4e5-111">Description</span><span class="sxs-lookup"><span data-stu-id="2b4e5-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="2b4e5-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="2b4e5-113">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-113">Optional.</span></span> <span data-ttu-id="2b4e5-114">The log directory.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-114">The log directory.</span></span> <span data-ttu-id="2b4e5-115">Verbose log files will be written to this directory.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="2b4e5-116">If no log directory is specified, the current directory will be used as the log directory.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="2b4e5-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="2b4e5-118">Required.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-118">Required.</span></span> <span data-ttu-id="2b4e5-119">The name of the storage account for the export job.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="2b4e5-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="2b4e5-121">Required if and only if a container SAS is not specified.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="2b4e5-122">The account key for the storage account for the export job.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="2b4e5-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="2b4e5-124">Required if and only if a storage account key is not specified.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="2b4e5-125">The container SAS for listing the blobs to be exported in the export job.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="2b4e5-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="2b4e5-127">Required.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-127">Required.</span></span> <span data-ttu-id="2b4e5-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="2b4e5-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="2b4e5-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="2b4e5-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="2b4e5-131">Required.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-131">Required.</span></span> <span data-ttu-id="2b4e5-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="2b4e5-133">Command-line example</span><span class="sxs-lookup"><span data-stu-id="2b4e5-133">Command-line example</span></span>

<span data-ttu-id="2b4e5-134">The following example demonstrates the `PreviewExport` command:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="2b4e5-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="2b4e5-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span><span class="sxs-lookup"><span data-stu-id="2b4e5-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="2b4e5-137">Here is an example of the output, with informational logs omitted:</span><span class="sxs-lookup"><span data-stu-id="2b4e5-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="2b4e5-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="2b4e5-138">Next steps</span></span>

* [<span data-ttu-id="2b4e5-139">Azure Import/Export Tool reference</span><span class="sxs-lookup"><span data-stu-id="2b4e5-139">Azure Import/Export Tool reference</span></span>](storage-import-export-tool-how-to-v1.md)
