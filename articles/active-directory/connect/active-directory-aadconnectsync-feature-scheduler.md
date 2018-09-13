---
title: 'Azure AD Connect sync: Scheduler | Microsoft Docs'
description: This topic describes the built-in scheduler feature in Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: AndKjell
manager: femila
editor: ''
ms.assetid: 6b1a598f-89c0-4244-9b20-f4aaad5233cf
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/28/2017
ms.author: billmath
ms.openlocfilehash: 30ae6c4ad894b52eb341e9489e8e8f53cc7e342d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550096"
---
# <a name="azure-ad-connect-sync-scheduler"></a>Azure AD Connect sync: Scheduler
This topic describes the built-in scheduler in Azure AD Connect sync (a.k.a. sync engine).

This feature was introduced with build 1.1.105.0 (released February 2016).

## <a name="overview"></a>Overview
Azure AD Connect sync synchronize changes occurring in your on-premises directory using a scheduler. There are two scheduler processes, one for password sync and another for object/attribute sync and maintenance tasks. This topic covers the latter.

In earlier releases, the scheduler for objects and attributes was external to the sync engine. It used Windows task scheduler or a separate Windows service to trigger the synchronization process. The scheduler is with the 1.1 releases built-in to the sync engine and do allow some customization. The new default synchronization frequency is 30 minutes.

The scheduler is responsible for two tasks:

* **Synchronization cycle**. The process to import, sync, and export changes.
* **Maintenance tasks**. Renew keys and certificates for Password reset and Device Registration Service (DRS). Purge old entries in the operations log.

The scheduler itself is always running, but it can be configured to only run one or none of these tasks. For example, if you need to have your own synchronization cycle process, you can disable this task in the scheduler but still run the maintenance task.

## <a name="scheduler-configuration"></a>Scheduler configuration
To see your current configuration settings, go to PowerShell and run `Get-ADSyncScheduler`. It shows you something like this picture:

![GetSyncScheduler](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-scheduler/getsynccyclesettings2016.png)

If you see **The sync command or cmdlet is not available** when you run this cmdlet, then the PowerShell module is not loaded. This problem could happen if you run Azure AD Connect on a domain controller or on a server with higher PowerShell restriction levels than the default settings. If you see this error, then run `Import-Module ADSync` to make the cmdlet available.

* **AllowedSyncCycleInterval**. The most frequently interval Azure AD allows synchronizations to occur. You cannot synchronize more frequently than this setting and still be supported.
* **CurrentlyEffectiveSyncCycleInterval**. The schedule currently in effect. It has the same value as CustomizedSyncInterval (if set) if it is not more frequent than AllowedSyncInterval. If you use a build before 1.1.281 and you change CustomizedSyncCycleInterval, this change takes effect after next synchronization cycle. From build 1.1.281 the change takes effect immediately.
* **CustomizedSyncCycleInterval**. If you want the scheduler to run at any other frequency than the default 30 minutes, then you configure this setting. In the picture above, the scheduler has been set to run every hour instead. If you set this setting to a value lower than AllowedSyncInterval, then the latter is used.
* **NextSyncCyclePolicyType**. Either Delta or Initial. Defines if the next run should only process delta changes, or if the next run should do a full import and sync. The latter would also reprocess any new or changed rules.
* **NextSyncCycleStartTimeInUTC**. Next time the scheduler starts the next sync cycle.
* **PurgeRunHistoryInterval**. The time operation logs should be kept. These logs can be reviewed in the synchronization service manager. The default is to keep these logs for 7 days.
* **SyncCycleEnabled**. Indicates if the scheduler is running the import, sync, and export processes as part of its operation.
* **MaintenanceEnabled**. Shows if the maintenance process is enabled. It updates the certificates/keys and purges the operations log.
* **StagingModeEnabled**. Shows if [staging mode](active-directory-aadconnectsync-operations.md#staging-mode) is enabled. If this setting is enabled, then it suppresses the exports from running but still run import and synchronization.
* **SchedulerSuspended**. Set by Connect during an upgrade to temporarily block the scheduler from running.

You can change some of these settings with `Set-ADSyncScheduler`. The following parameters can be modified:

* CustomizedSyncCycleInterval
* NextSyncCyclePolicyType
* PurgeRunHistoryInterval
* SyncCycleEnabled
* MaintenanceEnabled

In earlier builds of Azure AD Connect, **isStagingModeEnabled** was exposed in Set-ADSyncScheduler. It is **unsupported** to set this property. The property **SchedulerSuspended** should only be modified by Connect. It is **unsupported** to set this with PowerShell directly.

The scheduler configuration is stored in Azure AD. If you have a staging server, any change on the primary server also affects the staging server (except IsStagingModeEnabled).

### <a name="customizedsynccycleinterval"></a>CustomizedSyncCycleInterval
Syntax: `Set-ADSyncScheduler -CustomizedSyncCycleInterval d.HH:mm:ss`  
d - days, HH - hours, mm - minutes, ss - seconds

Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 03:00:00`  
Changes the scheduler to run every 3 hours.

Example: `Set-ADSyncScheduler -CustomizedSyncCycleInterval 1.0:0:0`  
Changes change the scheduler to run daily.

### <a name="disable-the-scheduler"></a>Disable the scheduler  
If you need to make configuration changes, then you want to disable the scheduler. For example, when you [configure filtering](active-directory-aadconnectsync-configure-filtering.md) or [make changes to synchronization rules](active-directory-aadconnectsync-change-the-configuration.md).

To disable the scheduler, run `Set-ADSyncScheduler -SyncCycleEnabled $false`.

![Disable the scheduler](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-change-the-configuration/schedulerdisable.png)

When you've made your changes, do not forget to enable the scheduler again with `Set-ADSyncScheduler -SyncCycleEnabled $true`.

## <a name="start-the-scheduler"></a>Start the scheduler
The scheduler is by default run every 30 minutes. In some cases, you might want to run a sync cycle in between the scheduled cycles or you need to run a different type.

**Delta sync cycle**  
A delta sync cycle includes the following steps:

* Delta import on all Connectors
* Delta sync on all Connectors
* Export on all Connectors

It could be that you have an urgent change that must be synchronized immediately, which is why you need to manually run a cycle. If you need to manually run a cycle, then from PowerShell run `Start-ADSyncSyncCycle -PolicyType Delta`.

**Full sync cycle**  
If you have made one of the following configuration changes, you need to run a full sync cycle (a.k.a. Initial):

* Added more objects or attributes to be imported from a source directory
* Made changes to the Synchronization rules
* Changed [filtering](active-directory-aadconnectsync-configure-filtering.md) so a different number of objects should be included

If you have made one of these changes, then you need to run a full sync cycle so the sync engine has the opportunity to reconsolidate the connector spaces. A full sync cycle includes the following steps:

* Full Import on all Connectors
* Full Sync on all Connectors
* Export on all Connectors

To initiate a full sync cycle, run `Start-ADSyncSyncCycle -PolicyType Initial` from a PowerShell prompt. This command starts a full sync cycle.

## <a name="stop-the-scheduler"></a>Stop the scheduler
If the scheduler is currently running a synchronization cycle, you might need to stop it. For example if you start the installation wizard and you get this error:

![SyncCycleRunningError](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-scheduler/synccyclerunningerror.png)

When a sync cycle is running, you cannot make configuration changes. You could wait until the scheduler has finished the process, but you can also stop it so you can make your changes immediately. Stopping the current cycle is not harmful and pending changes are processed with next run.

1. Start by telling the scheduler to stop its current cycle with the PowerShell cmdlet `Stop-ADSyncSyncCycle`.
2. If you use a build before 1.1.281, then stopping the scheduler does not stop the current Connector from its current task. To force the Connector to stop, take the following actions: ![StopAConnector](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-scheduler/stopaconnector.png)
   * Start **Synchronization Service** from the start menu. Go to **Connectors**, highlight the Connector with the state **Running**, and select **Stop** from the Actions.

The scheduler is still active and starts again on next opportunity.

## <a name="custom-scheduler"></a>Custom scheduler
The cmdlets documented in this section are only available in build [1.1.130.0](active-directory-aadconnect-version-history.md#111300) and later.

If the built-in scheduler does not satisfy your requirements, then you can schedule the Connectors using PowerShell.

### <a name="invoke-adsyncrunprofile"></a>Invoke-ADSyncRunProfile
You can start a profile for a Connector in this way:

```
Invoke-ADSyncRunProfile -ConnectorName "name of connector" -RunProfileName "name of profile"
```

The names to use for [Connector names](active-directory-aadconnectsync-service-manager-ui-connectors.md) and [Run Profile Names](active-directory-aadconnectsync-service-manager-ui-connectors.md#configure-run-profiles) can be found in the [Synchronization Service Manager UI](active-directory-aadconnectsync-service-manager-ui.md).

![Invoke Run Profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-scheduler/invokerunprofile.png)  

The `Invoke-ADSyncRunProfile` cmdlet is synchronous, that is, it does not return control until the Connector has completed the operation, either successfully or with an error.

When you schedule your Connectors, the recommendation is to schedule them in the following order:

1. (Full/Delta) Import from on-premises directories, such as Active Directory
2. (Full/Delta) Import from Azure AD
3. (Full/Delta) Synchronization from on-premises directories, such as Active Directory
4. (Full/Delta) Synchronization from Azure AD
5. Export to Azure AD
6. Export to on-premises directories, such as Active Directory

This order is how the built-in scheduler runs the Connectors.

### <a name="get-adsyncconnectorrunstatus"></a>Get-ADSyncConnectorRunStatus
You can also monitor the sync engine to see if it is busy or idle. This cmdlet returns an empty result if the sync engine is idle and is not running a Connector. If a Connector is running, it returns the name of the Connector.

```
Get-ADSyncConnectorRunStatus
```

![Connector Run Status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect/media/active-directory-aadconnectsync-feature-scheduler/getconnectorrunstatus.png)  
In the picture above, the first line is from a state where the sync engine is idle. The second line from when the Azure AD Connector is running.

## <a name="scheduler-and-installation-wizard"></a>Scheduler and installation wizard
If you start the installation wizard, then the scheduler is temporarily suspended. This behavior is because it is assumed you make configuration changes and these settings cannot be applied if the sync engine is actively running. For this reason, do not leave the installation wizard open since it stops the sync engine from performing any synchronization actions.

## <a name="next-steps"></a>Next steps
Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.

Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).





