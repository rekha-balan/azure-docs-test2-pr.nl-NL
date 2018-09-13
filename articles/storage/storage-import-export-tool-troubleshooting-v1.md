---
title: Troubleshooting the Azure Import/Export Tool | Microsoft Docs
description: Learn about some of the common issues seen when using the Azure Import/Export Tool, and how to handle them.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: ''
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 43b5d5a57df6bdda57a31ff0330ec6eff7aa732c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662407"
---
# <a name="troubleshooting-the-azure-importexport-tool"></a><span data-ttu-id="77e76-103">Troubleshooting the Azure Import/Export Tool</span><span class="sxs-lookup"><span data-stu-id="77e76-103">Troubleshooting the Azure Import/Export Tool</span></span>
<span data-ttu-id="77e76-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span><span class="sxs-lookup"><span data-stu-id="77e76-104">The Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="77e76-105">This topic lists some common issues that users may run into.</span><span class="sxs-lookup"><span data-stu-id="77e76-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="77e76-106">A copy session fails, what I should do?</span><span class="sxs-lookup"><span data-stu-id="77e76-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="77e76-107">When a copy session fails, there are two options:</span><span class="sxs-lookup"><span data-stu-id="77e76-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="77e76-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span><span class="sxs-lookup"><span data-stu-id="77e76-108">If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session.</span></span> <span data-ttu-id="77e76-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span><span class="sxs-lookup"><span data-stu-id="77e76-109">If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session.</span></span> <span data-ttu-id="77e76-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span><span class="sxs-lookup"><span data-stu-id="77e76-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="77e76-111">I can't resume or abort a copy session.</span><span class="sxs-lookup"><span data-stu-id="77e76-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="77e76-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span><span class="sxs-lookup"><span data-stu-id="77e76-112">If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="77e76-113">In this case, you can delete the old journal file and rerun the command.</span><span class="sxs-lookup"><span data-stu-id="77e76-113">In this case, you can delete the old journal file and rerun the command.</span></span>  
  
 <span data-ttu-id="77e76-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span><span class="sxs-lookup"><span data-stu-id="77e76-114">If a copy session is not the first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a><span data-ttu-id="77e76-115">I lost the journal file, can I still create the job?</span><span class="sxs-lookup"><span data-stu-id="77e76-115">I lost the journal file, can I still create the job?</span></span>  
 <span data-ttu-id="77e76-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span><span class="sxs-lookup"><span data-stu-id="77e76-116">The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job.</span></span> <span data-ttu-id="77e76-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span><span class="sxs-lookup"><span data-stu-id="77e76-117">If the journal file is lost, you will have to redo all the copy sessions for the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="77e76-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="77e76-118">Next steps</span></span>
 
* [<span data-ttu-id="77e76-119">Setting up the azure import/export tool</span><span class="sxs-lookup"><span data-stu-id="77e76-119">Setting up the azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="77e76-120">Preparing hard drives for an import job</span><span class="sxs-lookup"><span data-stu-id="77e76-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="77e76-121">Reviewing job status with copy log files</span><span class="sxs-lookup"><span data-stu-id="77e76-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="77e76-122">Repairing an import job</span><span class="sxs-lookup"><span data-stu-id="77e76-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="77e76-123">Repairing an export job</span><span class="sxs-lookup"><span data-stu-id="77e76-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
