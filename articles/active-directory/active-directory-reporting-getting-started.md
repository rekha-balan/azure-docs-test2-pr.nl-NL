---
title: 'Azure Active Directory Reporting: Getting started | Microsoft Docs'
description: Lists the various available reports in Azure Active Directory reporting
services: active-directory
documentationcenter: ''
author: dhanyahk
manager: femila
editor: ''
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/07/2016
ms.author: dhanyahk;markvi
ms.openlocfilehash: 983211e7acc7daff6492f5b939d2097b4dbe151a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549370"
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Getting started with Azure Active Directory Reporting
## <a name="what-it-is"></a>What it is
Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory. Here's a list of the reports included:

### <a name="security-reports"></a>Security reports
* Sign-ins from unknown sources
* Sign-ins after multiple failures
* Sign-ins from multiple geographies
* Sign-ins from IP addresses with suspicious activity
* Irregular sign-in activity
* Sign-ins from possibly infected devices
* Users with anomalous sign-in activity

### <a name="activity-reports"></a>Activity reports
* Application usage: summary
* Application usage: detailed
* Application dashboard
* Account provisioning errors
* Individual user devices
* Individual user Activity
* Groups activity report
* Password Reset Registration Activity Report
* Password reset activity

### <a name="audit-reports"></a>Audit reports
* Directory audit report

> [!TIP]
> For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>How it works
### <a name="reporting-pipeline"></a>Reporting pipeline
The reporting pipeline consists of three main steps. Every time a user signs in, or an authentication is made, the following happens:

* First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.
* At regular intervals, all recent sign ins are processed. At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.
* After processing, the reports are written, cached, and served in the Azure classic portal.

### <a name="report-generation-times"></a>Report generation times
Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old. In rare cases, it may take up to 8 hours to process the most recent sign-ins.

You can find the most recent processed sign-in by examining the help text at the top of each report.

![Help text at the top of each report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Getting started
### <a name="sign-into-the-azure-classic-portal"></a>Sign into the Azure classic portal
First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator. You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.

### <a name="navigate-to-reports"></a>Navigate to Reports
To view Reports, navigate to the Reports tab at the top of your directory.

If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports. This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.

![Dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Explore each report
Navigate into each report to see the data being collected and the sign-ins processed. You can find a [list of all the reports here](active-directory-reporting-guide.md).

![All reports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a>Download the reports as CSV
Each report can be downloaded as a CSV (comma-separated value) file. You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.

To download any report as a CSV, navigate to the report and click "Download" at the bottom.

![Download button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Next steps
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Customize alerts for anomalous sign in activity
Navigate to the "Configure" tab of your directory.

Scroll to the "Notifications" section.

Enable or disable the "Email Notifications of Anomalous sign-ins" section.

![The Notifications section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a>Integrate with the Azure AD Reporting API
See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Engage Multi-Factor Authentication on users
Select a user in a report.

Click the "Enable MFA" button at the bottom of the screen.

![The Multi-Factor Authentication button at the bottom of the screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Learn more
### <a name="audit-events"></a>Audit events
Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>API Integration
See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Get in touch
Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.

> [!TIP]
> For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).
> 
> 







