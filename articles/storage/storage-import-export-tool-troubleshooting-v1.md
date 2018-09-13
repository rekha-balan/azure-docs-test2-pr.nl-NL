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
# <a name="troubleshooting-the-azure-importexport-tool"></a>Troubleshooting the Azure Import/Export Tool
The Microsoft Azure Import/Export Tool returns error messages if it runs into issues. This topic lists some common issues that users may run into.  
  
## <a name="a-copy-session-fails-what-i-should-do"></a>A copy session fails, what I should do?  
 When a copy session fails, there are two options:  
  
 If the error is retryable, for example if the network share was offline for a short period and now is back online, you can resume the copy session. If the error is not retryable, for example if you specified the wrong source file directory in the command line parameters, you need to abort the copy session. See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a>I can't resume or abort a copy session.  
 If the copy session is the first copy session for a drive, then the error message should state: "The first copy session cannot be resumed or aborted." In this case, you can delete the old journal file and rerun the command.  
  
 If a copy session is not the first one for a drive, it can always be resumed or aborted.  
  
## <a name="i-lost-the-journal-file-can-i-still-create-the-job"></a>I lost the journal file, can I still create the job?  
 The journal file for a drive contains the complete information of copying data to this drive, and it is needed to add more files to the drive and will be used to create an import job. If the journal file is lost, you will have to redo all the copy sessions for the drive.  
  
## <a name="next-steps"></a>Next steps
 
* [Setting up the azure import/export tool](storage-import-export-tool-setup-v1.md)   
* [Preparing hard drives for an import job](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Reviewing job status with copy log files](storage-import-export-tool-reviewing-job-status-v1.md)   
* [Repairing an import job](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Repairing an export job](storage-import-export-tool-repairing-an-export-job-v1.md)
