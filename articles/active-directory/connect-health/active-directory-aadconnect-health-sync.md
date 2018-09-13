---
title: Using Azure AD Connect Health with sync | Microsoft Docs
description: This is the Azure AD Connect Health page that will discuss how to monitor Azure AD Connect sync.
services: active-directory
documentationcenter: ''
author: karavar
manager: samueld
editor: curtand
ms.assetid: 1dfbeaba-bda2-4f68-ac89-1dbfaf5b4015
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/27/2017
ms.author: vakarand
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1845dee149399fe76e307d86cd740b85d2e99974
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554514"
---
# <a name="monitor-azure-ad-connect-sync-with-azure-ad-connect-health"></a>Monitor Azure AD Connect sync with Azure AD Connect Health
The following documentation is specific to monitoring Azure AD Connect (Sync) with Azure AD Connect Health.  For information on monitoring AD FS with Azure AD Connect Health see [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md). Additionally, for information on monitoring Active Directory Domain Services with Azure AD Connect Health see [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md).

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/sync-blade.png)

## <a name="alerts-for-azure-ad-connect-health-for-sync"></a>Alerts for Azure AD Connect Health for sync
The Azure AD Connect Health Alerts for sync section provides you the list of active alerts. Each alert includes relevant information, resolution steps, and links to related documentation. By selecting an active or resolved alert you will see a new blade with additional information, as well as steps you can take to resolve the alert, and links to additional documentation. You can also view historical data on alerts that were resolved in the past.

By selecting an alert you will be provided with additional information as well as steps you can take to resolve the alert and links to additional documentation.

![Azure AD Connect sync error](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/alert.png)

### <a name="limited-evaluation-of-alerts"></a>Limited Evaluation of Alerts
If Azure AD Connect is NOT using the default configuration (for example, if Attribute Filtering is changed from the default configuration to a custom configuration), then the Azure AD Connect Health agent will not upload the error events related to Azure AD Connect.

This limits the evaluation of alerts by the service. You'd will see a banner that indicates this condition in the Azure Portal under your service.

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/banner.png)

You can change this by clicking "Settings" and allowing Azure AD Connect Health agent to upload all error logs.

![Azure AD Connect Health for Sync](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/banner2.png)

## <a name="sync-insight"></a>Sync Insight
Admins Frequently want to know about the time it takes to sync changes to Azure AD and the amount of changes taking place. This feature provides an easy way to visualize this using the below graphs:   

* Latency of sync operations
* Object Change trend

### <a name="sync-latency"></a>Sync Latency
This feature provides a graphical trend of latency of the sync operations (import, export, etc.) for connectors.  This provides a quick and easy way to understand not only the latency of your operations (larger if you have a large set of changes occurring) but also a way to detect anomalies in the latency that may require further investigation.

![Sync Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/synclatency02.png)

By default, only the latency of the 'Export' operation for the Azure AD connector is shown.  To see more operations on the connector or to view operations from other connectors, right-click on the chart,  select Edit Chart or click on the "Edit Latency Chart" button and choose the specific operation and connectors.

### <a name="sync-object-changes"></a>Sync Object Changes
This feature provides a graphical trend of the number of changes that are being evaluated and exported to Azure AD.  Today, trying to gather this information from the sync logs is difficult.  The chart gives you, not only a simpler way of monitoring the number of changes that are occurring in your environment, but also a visual view of the failures that are occurring.

![Sync Latency](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/syncobjectchanges02.png)

## <a name="object-level-synchronization-error-report-preview"></a>Object Level Synchronization Error Report (Preview)
This feature provides a report about synchronization errors that can occur when identity data is synchronized between Windows Server AD and Azure AD using Azure AD Connect.

* The report covers errors recorded by the sync client (Azure AD Connect version 1.1.281.0 or higher)
* It includes the errors that occurred in the last synchronization operation on the sync engine. ("Export" on the Azure AD Connector.)
* Azure AD Connect Health agent for sync must have outbound connectivity to the required end points for the report to include the latest data.
* The report is **updated after every 30 minutes** using the data uploaded by Azure AD Connect Health agent for sync. It provides the following key capabilities

  * Categorization of errors
  * List of objects with error per category
  * All the data about the errors at one place
  * Side by side comparison of Objects with error due to a conflict
  * Download the error report as a CVS (coming soon)

### <a name="categorization-of-errors"></a>Categorization of Errors
The report categorizes the existing synchronization errors in the following categories:

| Category | Description |
| --- | --- |
| Duplicate Attribute |Errors when Azure AD Connect attempts create or update objects with duplicated values of one or more attributes in Azure AD that must be unique in a Tenant, such as proxyAddresses, UserPrincipalName. |
| Data Mismatch |Errors when the soft-match fails to match objects that result in synchronization errors. |
| Data Validation Failure |Errors due to invalid data, such as unsupported characters in critical attributes such as UserPrincipalName, format errors that fail validation before being written in Azure AD. |
| Large Attribute |Errors when one or more attributes are larger than the allowed size, length or count. |
| Other |All other errors that don't fit in the above categories. Based on feedback, this category will be split in sub categories. |

![Sync Error Report Summary](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport01.png)
![Sync Error Report Categories](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport02.png)

### <a name="list-of-objects-with-error-per-category"></a>List of objects with error per category
Drilling into each category will provide the list of objects having the error in that category.
![Sync Error Report List](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport03.png)

### <a name="error-details"></a>Error Details
Following data is available in the detailed view for each error

* Identifiers for the *AD Object* involved
* Identifiers for the *Azure AD Object* involved (as applicable)
* Error description and how to fix
* Related articles

![Sync Error Report Details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/connect-health/media/active-directory-aadconnect-health-sync/errorreport04.png)

### <a name="download-the-error-report-as-csv"></a>Download the error report as CSV
By selecting the "Export" button you can download a CSV file with all the details about all the errors.

## <a name="related-links"></a>Related links
* [Troubleshooting Errors during synchronization](../connect/active-directory-aadconnect-troubleshoot-sync-errors.md)
* [Duplicate Attribute Resiliency](../connect/active-directory-aadconnectsyncservice-duplicate-attribute-resiliency.md)
* [Azure AD Connect Health](active-directory-aadconnect-health.md)
* [Azure AD Connect Health Agent Installation](active-directory-aadconnect-health-agent-install.md)
* [Azure AD Connect Health Operations](active-directory-aadconnect-health-operations.md)
* [Using Azure AD Connect Health with AD FS](active-directory-aadconnect-health-adfs.md)
* [Using Azure AD Connect Health with AD DS](active-directory-aadconnect-health-adds.md)
* [Azure AD Connect Health FAQ](active-directory-aadconnect-health-faq.md)
* [Azure AD Connect Health Version History](active-directory-aadconnect-health-version-history.md)









