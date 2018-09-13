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
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="630b8-103">Getting started with Azure Active Directory Reporting</span><span class="sxs-lookup"><span data-stu-id="630b8-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="630b8-104">What it is</span><span class="sxs-lookup"><span data-stu-id="630b8-104">What it is</span></span>
<span data-ttu-id="630b8-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span><span class="sxs-lookup"><span data-stu-id="630b8-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="630b8-106">Here's a list of the reports included:</span><span class="sxs-lookup"><span data-stu-id="630b8-106">Here's a list of the reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="630b8-107">Security reports</span><span class="sxs-lookup"><span data-stu-id="630b8-107">Security reports</span></span>
* <span data-ttu-id="630b8-108">Sign-ins from unknown sources</span><span class="sxs-lookup"><span data-stu-id="630b8-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="630b8-109">Sign-ins after multiple failures</span><span class="sxs-lookup"><span data-stu-id="630b8-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="630b8-110">Sign-ins from multiple geographies</span><span class="sxs-lookup"><span data-stu-id="630b8-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="630b8-111">Sign-ins from IP addresses with suspicious activity</span><span class="sxs-lookup"><span data-stu-id="630b8-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="630b8-112">Irregular sign-in activity</span><span class="sxs-lookup"><span data-stu-id="630b8-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="630b8-113">Sign-ins from possibly infected devices</span><span class="sxs-lookup"><span data-stu-id="630b8-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="630b8-114">Users with anomalous sign-in activity</span><span class="sxs-lookup"><span data-stu-id="630b8-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="630b8-115">Activity reports</span><span class="sxs-lookup"><span data-stu-id="630b8-115">Activity reports</span></span>
* <span data-ttu-id="630b8-116">Application usage: summary</span><span class="sxs-lookup"><span data-stu-id="630b8-116">Application usage: summary</span></span>
* <span data-ttu-id="630b8-117">Application usage: detailed</span><span class="sxs-lookup"><span data-stu-id="630b8-117">Application usage: detailed</span></span>
* <span data-ttu-id="630b8-118">Application dashboard</span><span class="sxs-lookup"><span data-stu-id="630b8-118">Application dashboard</span></span>
* <span data-ttu-id="630b8-119">Account provisioning errors</span><span class="sxs-lookup"><span data-stu-id="630b8-119">Account provisioning errors</span></span>
* <span data-ttu-id="630b8-120">Individual user devices</span><span class="sxs-lookup"><span data-stu-id="630b8-120">Individual user devices</span></span>
* <span data-ttu-id="630b8-121">Individual user Activity</span><span class="sxs-lookup"><span data-stu-id="630b8-121">Individual user Activity</span></span>
* <span data-ttu-id="630b8-122">Groups activity report</span><span class="sxs-lookup"><span data-stu-id="630b8-122">Groups activity report</span></span>
* <span data-ttu-id="630b8-123">Password Reset Registration Activity Report</span><span class="sxs-lookup"><span data-stu-id="630b8-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="630b8-124">Password reset activity</span><span class="sxs-lookup"><span data-stu-id="630b8-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="630b8-125">Audit reports</span><span class="sxs-lookup"><span data-stu-id="630b8-125">Audit reports</span></span>
* <span data-ttu-id="630b8-126">Directory audit report</span><span class="sxs-lookup"><span data-stu-id="630b8-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="630b8-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="630b8-128">How it works</span><span class="sxs-lookup"><span data-stu-id="630b8-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="630b8-129">Reporting pipeline</span><span class="sxs-lookup"><span data-stu-id="630b8-129">Reporting pipeline</span></span>
<span data-ttu-id="630b8-130">The reporting pipeline consists of three main steps.</span><span class="sxs-lookup"><span data-stu-id="630b8-130">The reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="630b8-131">Every time a user signs in, or an authentication is made, the following happens:</span><span class="sxs-lookup"><span data-stu-id="630b8-131">Every time a user signs in, or an authentication is made, the following happens:</span></span>

* <span data-ttu-id="630b8-132">First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.</span><span class="sxs-lookup"><span data-stu-id="630b8-132">First, the user is authenticated (successfully or unsuccessfully), and the result is stored in the Azure Active Directory service databases.</span></span>
* <span data-ttu-id="630b8-133">At regular intervals, all recent sign ins are processed.</span><span class="sxs-lookup"><span data-stu-id="630b8-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="630b8-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span><span class="sxs-lookup"><span data-stu-id="630b8-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="630b8-135">After processing, the reports are written, cached, and served in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="630b8-135">After processing, the reports are written, cached, and served in the Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="630b8-136">Report generation times</span><span class="sxs-lookup"><span data-stu-id="630b8-136">Report generation times</span></span>
<span data-ttu-id="630b8-137">Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old.</span><span class="sxs-lookup"><span data-stu-id="630b8-137">Due to the large volume of authentications and sign ins processed by the Azure AD platform, the most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="630b8-138">In rare cases, it may take up to 8 hours to process the most recent sign-ins.</span><span class="sxs-lookup"><span data-stu-id="630b8-138">In rare cases, it may take up to 8 hours to process the most recent sign-ins.</span></span>

<span data-ttu-id="630b8-139">You can find the most recent processed sign-in by examining the help text at the top of each report.</span><span class="sxs-lookup"><span data-stu-id="630b8-139">You can find the most recent processed sign-in by examining the help text at the top of each report.</span></span>

![Help text at the top of each report](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="630b8-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="630b8-142">Getting started</span><span class="sxs-lookup"><span data-stu-id="630b8-142">Getting started</span></span>
### <a name="sign-into-the-azure-classic-portal"></a><span data-ttu-id="630b8-143">Sign into the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="630b8-143">Sign into the Azure classic portal</span></span>
<span data-ttu-id="630b8-144">First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span><span class="sxs-lookup"><span data-stu-id="630b8-144">First, you'll need to sign into the [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="630b8-145">You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="630b8-145">You must also be an Azure subscription service administrator or co-administrator, or be using the "Access to Azure AD" Azure subscription.</span></span>

### <a name="navigate-to-reports"></a><span data-ttu-id="630b8-146">Navigate to Reports</span><span class="sxs-lookup"><span data-stu-id="630b8-146">Navigate to Reports</span></span>
<span data-ttu-id="630b8-147">To view Reports, navigate to the Reports tab at the top of your directory.</span><span class="sxs-lookup"><span data-stu-id="630b8-147">To view Reports, navigate to the Reports tab at the top of your directory.</span></span>

<span data-ttu-id="630b8-148">If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports.</span><span class="sxs-lookup"><span data-stu-id="630b8-148">If this is your first time viewing the reports, you'll need to agree to a dialog box before you can view the reports.</span></span> <span data-ttu-id="630b8-149">This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.</span><span class="sxs-lookup"><span data-stu-id="630b8-149">This is to ensure that it's acceptable for admins in your organization to view this data, which may be considered private information in some countries.</span></span>

![Dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="630b8-151">Explore each report</span><span class="sxs-lookup"><span data-stu-id="630b8-151">Explore each report</span></span>
<span data-ttu-id="630b8-152">Navigate into each report to see the data being collected and the sign-ins processed.</span><span class="sxs-lookup"><span data-stu-id="630b8-152">Navigate into each report to see the data being collected and the sign-ins processed.</span></span> <span data-ttu-id="630b8-153">You can find a [list of all the reports here](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-153">You can find a [list of all the reports here](active-directory-reporting-guide.md).</span></span>

![All reports](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-the-reports-as-csv"></a><span data-ttu-id="630b8-155">Download the reports as CSV</span><span class="sxs-lookup"><span data-stu-id="630b8-155">Download the reports as CSV</span></span>
<span data-ttu-id="630b8-156">Each report can be downloaded as a CSV (comma-separated value) file.</span><span class="sxs-lookup"><span data-stu-id="630b8-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="630b8-157">You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.</span><span class="sxs-lookup"><span data-stu-id="630b8-157">You can use these files in Excel, PowerBI or third-party analysis programs to further analyze your data.</span></span>

<span data-ttu-id="630b8-158">To download any report as a CSV, navigate to the report and click "Download" at the bottom.</span><span class="sxs-lookup"><span data-stu-id="630b8-158">To download any report as a CSV, navigate to the report and click "Download" at the bottom.</span></span>

![Download button](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="630b8-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="630b8-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="630b8-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="630b8-162">Customize alerts for anomalous sign in activity</span><span class="sxs-lookup"><span data-stu-id="630b8-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="630b8-163">Navigate to the "Configure" tab of your directory.</span><span class="sxs-lookup"><span data-stu-id="630b8-163">Navigate to the "Configure" tab of your directory.</span></span>

<span data-ttu-id="630b8-164">Scroll to the "Notifications" section.</span><span class="sxs-lookup"><span data-stu-id="630b8-164">Scroll to the "Notifications" section.</span></span>

<span data-ttu-id="630b8-165">Enable or disable the "Email Notifications of Anomalous sign-ins" section.</span><span class="sxs-lookup"><span data-stu-id="630b8-165">Enable or disable the "Email Notifications of Anomalous sign-ins" section.</span></span>

![The Notifications section](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-the-azure-ad-reporting-api"></a><span data-ttu-id="630b8-167">Integrate with the Azure AD Reporting API</span><span class="sxs-lookup"><span data-stu-id="630b8-167">Integrate with the Azure AD Reporting API</span></span>
<span data-ttu-id="630b8-168">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-168">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="630b8-169">Engage Multi-Factor Authentication on users</span><span class="sxs-lookup"><span data-stu-id="630b8-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="630b8-170">Select a user in a report.</span><span class="sxs-lookup"><span data-stu-id="630b8-170">Select a user in a report.</span></span>

<span data-ttu-id="630b8-171">Click the "Enable MFA" button at the bottom of the screen.</span><span class="sxs-lookup"><span data-stu-id="630b8-171">Click the "Enable MFA" button at the bottom of the screen.</span></span>

![The Multi-Factor Authentication button at the bottom of the screen](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="630b8-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="630b8-174">Learn more</span><span class="sxs-lookup"><span data-stu-id="630b8-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="630b8-175">Audit events</span><span class="sxs-lookup"><span data-stu-id="630b8-175">Audit events</span></span>
<span data-ttu-id="630b8-176">Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-176">Learn about what events are audited in the directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="630b8-177">API Integration</span><span class="sxs-lookup"><span data-stu-id="630b8-177">API Integration</span></span>
<span data-ttu-id="630b8-178">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="630b8-178">See [Getting started with the Reporting API](active-directory-reporting-api-getting-started.md) and the [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="630b8-179">Get in touch</span><span class="sxs-lookup"><span data-stu-id="630b8-179">Get in touch</span></span>
<span data-ttu-id="630b8-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span><span class="sxs-lookup"><span data-stu-id="630b8-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="630b8-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="630b8-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 







