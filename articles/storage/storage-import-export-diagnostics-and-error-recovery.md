---
title: Diagnostics and error recovery for Azure Import/Export jobs | Microsoft Docs
description: Learn how to enable verbose logging for Microsoft Azure Import/Export service jobs.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 096cc795-9af6-4335-9fe8-fffa9f239a17
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 0068aae9d6780aa41a070db0eb191d0d5a165d21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563601"
---
# <a name="diagnostics-and-error-recovery-for-azure-importexport-jobs"></a><span data-ttu-id="34956-103">Diagnostics and error recovery for Azure Import/Export jobs</span><span class="sxs-lookup"><span data-stu-id="34956-103">Diagnostics and error recovery for Azure Import/Export jobs</span></span>
<span data-ttu-id="34956-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span><span class="sxs-lookup"><span data-stu-id="34956-104">For each drive processed, the Azure Import/Export service creates an error log in the associated storage account.</span></span> <span data-ttu-id="34956-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span><span class="sxs-lookup"><span data-stu-id="34956-105">You can also enable verbose logging by setting the `LogLevel` property to `Verbose` when calling the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operations.</span></span>

 <span data-ttu-id="34956-106">By default, logs are written to a container named `waimportexport`.</span><span class="sxs-lookup"><span data-stu-id="34956-106">By default, logs are written to a container named `waimportexport`.</span></span> <span data-ttu-id="34956-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span><span class="sxs-lookup"><span data-stu-id="34956-107">You can specify a different name by setting the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="34956-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span><span class="sxs-lookup"><span data-stu-id="34956-108">The logs are stored as block blobs with the following naming convention: `waies/jobname_driveid_timestamp_logtype.xml`.</span></span>

 <span data-ttu-id="34956-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span><span class="sxs-lookup"><span data-stu-id="34956-109">You can retrieve the URI of the logs for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="34956-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span><span class="sxs-lookup"><span data-stu-id="34956-110">The URI for the verbose log is returned in the `VerboseLogUri` property for each drive, while the URI for the error log is returned in the `ErrorLogUri` property.</span></span>

<span data-ttu-id="34956-111">You can use the logging data to identify the following issues.</span><span class="sxs-lookup"><span data-stu-id="34956-111">You can use the logging data to identify the following issues.</span></span>

## <a name="drive-errors"></a><span data-ttu-id="34956-112">Drive errors</span><span class="sxs-lookup"><span data-stu-id="34956-112">Drive errors</span></span>

<span data-ttu-id="34956-113">The following items are classified as drive errors:</span><span class="sxs-lookup"><span data-stu-id="34956-113">The following items are classified as drive errors:</span></span>

-   <span data-ttu-id="34956-114">Errors in accessing or reading the manifest file</span><span class="sxs-lookup"><span data-stu-id="34956-114">Errors in accessing or reading the manifest file</span></span>

-   <span data-ttu-id="34956-115">Incorrect BitLocker keys</span><span class="sxs-lookup"><span data-stu-id="34956-115">Incorrect BitLocker keys</span></span>

-   <span data-ttu-id="34956-116">Drive read/write errors</span><span class="sxs-lookup"><span data-stu-id="34956-116">Drive read/write errors</span></span>

## <a name="blob-errors"></a><span data-ttu-id="34956-117">Blob errors</span><span class="sxs-lookup"><span data-stu-id="34956-117">Blob errors</span></span>

<span data-ttu-id="34956-118">The following items are classified as blob errors:</span><span class="sxs-lookup"><span data-stu-id="34956-118">The following items are classified as blob errors:</span></span>

-   <span data-ttu-id="34956-119">Incorrect or conflicting blob or names</span><span class="sxs-lookup"><span data-stu-id="34956-119">Incorrect or conflicting blob or names</span></span>

-   <span data-ttu-id="34956-120">Missing files</span><span class="sxs-lookup"><span data-stu-id="34956-120">Missing files</span></span>

-   <span data-ttu-id="34956-121">Blob not found</span><span class="sxs-lookup"><span data-stu-id="34956-121">Blob not found</span></span>

-   <span data-ttu-id="34956-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span><span class="sxs-lookup"><span data-stu-id="34956-122">Truncated files (the files on the disk are smaller than specified in the manifest)</span></span>

-   <span data-ttu-id="34956-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span><span class="sxs-lookup"><span data-stu-id="34956-123">Corrupted file content (for import jobs, detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="34956-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span><span class="sxs-lookup"><span data-stu-id="34956-124">Corrupted blob metadata and property files (detected with an MD5 checksum mismatch)</span></span>

-   <span data-ttu-id="34956-125">Incorrect schema for the blob properties and/or metadata files</span><span class="sxs-lookup"><span data-stu-id="34956-125">Incorrect schema for the blob properties and/or metadata files</span></span>

<span data-ttu-id="34956-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span><span class="sxs-lookup"><span data-stu-id="34956-126">There may be cases where some parts of an import or export job do not complete successfully, while the overall job still completes.</span></span> <span data-ttu-id="34956-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span><span class="sxs-lookup"><span data-stu-id="34956-127">In this case, you can either upload or download the missing pieces of the data over network, or you can create a new job to transfer the data.</span></span> <span data-ttu-id="34956-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span><span class="sxs-lookup"><span data-stu-id="34956-128">See the [Azure Import/Export Tool Reference](storage-import-export-tool-how-to-v1.md) to learn how to repair the data over network.</span></span>

## <a name="next-steps"></a><span data-ttu-id="34956-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="34956-129">Next steps</span></span>

* [<span data-ttu-id="34956-130">Using the Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="34956-130">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
