---
title: Back up Azure Stack | Microsoft Docs
description: Perform an on-demand backup on Azure Stack with backup in place.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: 9565DDFB-2CDB-40CD-8964-697DA2FFF70A
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/05/2018
ms.author: jeffgilb
ms.reviewer: hectorl
ms.openlocfilehash: a11de2a4580515f6a358438a706e5be3f5543e28
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856662"
---
# <a name="back-up-azure-stack"></a>Back up Azure Stack

*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*

Perform an on-demand backup on Azure Stack with backup in place. For instructions on configuring the PowerShell environment, see [Install PowerShell for Azure Stack ](azure-stack-powershell-install.md). To sign in to Azure Stack, see [Using the administrator portal in Azure Stack](azure-stack-manage-portals.md).

## <a name="start-azure-stack-backup"></a>Start Azure Stack backup

### <a name="start-a-new-backup-without-job-progress-tracking"></a>Start a new backup without job progress tracking
Use Start-AzSBackup to start a new backup immediately with no job progress tracking.

```powershell
   Start-AzsBackup -Force
```

### <a name="start-azure-stack-backup-with-job-progress-tracking"></a>Start Azure Stack backup with job progress tracking
Use Start-AzSBackup to start a new backup with the -AsJob variable to track backup job progress.

```powershell
    $backupjob = Start-AzsBackup -Force -AsJob 
    "Start time: " + $backupjob.PSBeginTime;While($backupjob.State -eq "Running"){("Job is currently: " `
    + $backupjob.State+" ;Duration: " + (New-TimeSpan -Start ($backupjob.PSBeginTime) `
    -End (Get-Date)).Minutes);Start-Sleep -Seconds 30};$backupjob.Output

    if($backupjob.State -eq "Completed"){Get-AzsBackup | where {$_.BackupId -eq $backupjob.Output.BackupId}}
```

## <a name="confirm-backup-has-completed"></a>Confirm backup has completed

### <a name="confirm-backup-has-completed-using-powershell"></a>Confirm backup has completed using PowerShell
Use the following PowerShell commands to ensure that backup has completed successfully:

```powershell
   Get-AzsBackup
```

The result should look like the following output:

```powershell
    BackupDataVersion : 1.0.1
    BackupId          : <backup ID>
    RoleStatus        : {NRP, SRP, CRP, KeyVaultInternalControlPlane...}
    Status            : Succeeded
    CreatedDateTime   : 7/6/2018 6:46:24 AM
    TimeTakenToCreate : PT20M32.364138S
    DeploymentID      : <deployment ID>
    StampVersion      : 1.1807.0.41
    OemVersion        : 
    Id                : /subscriptions/<subscription ID>/resourceGroups/System.local/providers/Microsoft.Backup.Admin/backupLocations/local/backups/<backup ID>
    Name              : local/<local name>
    Type              : Microsoft.Backup.Admin/backupLocations/backups
    Location          : local
    Tags              : {}
```

### <a name="confirm-backup-has-completed-in-the-administration-portal"></a>Confirm backup has completed in the administration portal
Use the Azure Stack administration portal to verify that backup has completed successfully by following these steps:

1. Open the [Azure Stack administration portal](azure-stack-manage-portals.md).
2. Select **All services**, and then under the **ADMINISTRATION** category select > **Infrastructure backup**. Choose **Configuration** in the **Infrastructure backup** blade.
3. Find the **Name** and **Date Completed** of the backup in **Available backups** list.
4. Verify the **State** is **Succeeded**.

## <a name="next-steps"></a>Next steps

Learn more about the workflow for recovering from a data loss event. See [Recover from catastrophic data loss](azure-stack-backup-recover-data.md).
