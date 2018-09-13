---
title: Using the Azure Import/Export service REST API | Microsoft Docs
description: Learn where to find resources for using the Azure Import/Export service REST API, including both how-to and reference material.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552277"
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="4aa3a-103">Using the Azure Import/Export service REST API</span><span class="sxs-lookup"><span data-stu-id="4aa3a-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="4aa3a-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span><span class="sxs-lookup"><span data-stu-id="4aa3a-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="4aa3a-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="4aa3a-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="4aa3a-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span><span class="sxs-lookup"><span data-stu-id="4aa3a-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="4aa3a-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span><span class="sxs-lookup"><span data-stu-id="4aa3a-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="4aa3a-108">Service endpoints</span><span class="sxs-lookup"><span data-stu-id="4aa3a-108">Service endpoints</span></span>

<span data-ttu-id="4aa3a-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span><span class="sxs-lookup"><span data-stu-id="4aa3a-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="4aa3a-110">Versioning</span><span class="sxs-lookup"><span data-stu-id="4aa3a-110">Versioning</span></span>

<span data-ttu-id="4aa3a-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="4aa3a-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="4aa3a-112">Import/Export service operations</span><span class="sxs-lookup"><span data-stu-id="4aa3a-112">Import/Export service operations</span></span>

[<span data-ttu-id="4aa3a-113">Creating an import job</span><span class="sxs-lookup"><span data-stu-id="4aa3a-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="4aa3a-114">Creating an export job</span><span class="sxs-lookup"><span data-stu-id="4aa3a-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="4aa3a-115">Retrieving state information for a job</span><span class="sxs-lookup"><span data-stu-id="4aa3a-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="4aa3a-116">Enumerating jobs</span><span class="sxs-lookup"><span data-stu-id="4aa3a-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="4aa3a-117">Cancelling and deleting jobs</span><span class="sxs-lookup"><span data-stu-id="4aa3a-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="4aa3a-118">Backing Up drive manifests</span><span class="sxs-lookup"><span data-stu-id="4aa3a-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="4aa3a-119">Diagnostics and error recovery for Import/Export jobs</span><span class="sxs-lookup"><span data-stu-id="4aa3a-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="4aa3a-120">Next steps</span><span class="sxs-lookup"><span data-stu-id="4aa3a-120">Next steps</span></span>

* [<span data-ttu-id="4aa3a-121">Storage Import/Export REST</span><span class="sxs-lookup"><span data-stu-id="4aa3a-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
