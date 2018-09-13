---
title: Reviewing Azure Import/Export job status - v1 | Microsoft Docs
description: Learn how to use the log files created when the import or export job was run to see the status of the Import/Export job.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552665"
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="ea32b-103">Reviewing Azure Import/Export job status with copy log files</span><span class="sxs-lookup"><span data-stu-id="ea32b-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="ea32b-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span><span class="sxs-lookup"><span data-stu-id="ea32b-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="ea32b-105">The log file contains detailed status about each file that was imported or exported.</span><span class="sxs-lookup"><span data-stu-id="ea32b-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="ea32b-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span><span class="sxs-lookup"><span data-stu-id="ea32b-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="ea32b-107">Example URLs</span><span class="sxs-lookup"><span data-stu-id="ea32b-107">Example URLs</span></span>

<span data-ttu-id="ea32b-108">The following are example URLs for copy log files for an import job with two drives:</span><span class="sxs-lookup"><span data-stu-id="ea32b-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="ea32b-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span><span class="sxs-lookup"><span data-stu-id="ea32b-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ea32b-110">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea32b-110">Next steps</span></span>
 
 * [<span data-ttu-id="ea32b-111">Setting Up the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="ea32b-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="ea32b-112">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="ea32b-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="ea32b-113">Repairing an import job</span><span class="sxs-lookup"><span data-stu-id="ea32b-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="ea32b-114">Repairing an export job</span><span class="sxs-lookup"><span data-stu-id="ea32b-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="ea32b-115">Troubleshooting the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="ea32b-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
