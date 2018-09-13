---
title: Quick reference for Azure Import/Export Tool import job commands | Microsoft Docs
description: Azure Import/Export Tool command reference for frequently used import job commands.
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e9377e0c5001cf5be220e19e06ff96c1e058e853
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550976"
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="567a1-103">Quick reference for frequently used commands for import jobs</span><span class="sxs-lookup"><span data-stu-id="567a1-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="567a1-104">This article provides a quick reference for some frequently used commands.</span><span class="sxs-lookup"><span data-stu-id="567a1-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="567a1-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="567a1-105">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="567a1-106">First session</span><span class="sxs-lookup"><span data-stu-id="567a1-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="567a1-107">Second session</span><span class="sxs-lookup"><span data-stu-id="567a1-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="567a1-108">Abort latest session</span><span class="sxs-lookup"><span data-stu-id="567a1-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="567a1-109">Resume latest interrupted session</span><span class="sxs-lookup"><span data-stu-id="567a1-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-to-latest-session"></a><span data-ttu-id="567a1-110">Add drives to latest session</span><span class="sxs-lookup"><span data-stu-id="567a1-110">Add drives to latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="567a1-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="567a1-111">Next steps</span></span>

* [<span data-ttu-id="567a1-112">Sample workflow to prepare hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="567a1-112">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
